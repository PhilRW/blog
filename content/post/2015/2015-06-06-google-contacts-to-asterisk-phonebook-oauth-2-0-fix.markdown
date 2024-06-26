---
title: Google Contacts to Asterisk Phonebook -- OAuth 2.0 Fix
author: philrw
categories:
- Tech
comments: true
date: "2015-06-06T03:04:31Z"
link: https://philrw.wordpress.com/2015/06/05/google-contacts-to-asterisk-phonebook-oauth-2-0-fix/
slug: google-contacts-to-asterisk-phonebook-oauth-2-0-fix
tags:
- Asterisk
- code
- Google
- Python
- telephony
wordpress_id: 85727
---

Google deprecated legacy access to their [Contacts API](https://developers.google.com/google-apps/contacts/v3/), so I updated [googlecontacts.py](http://pbxinaflash.com/community/index.php?threads/google-contacts-to-asterisk-phonebook.10943/) to use OAuth 2.0.

UPDATE: [Now on GitHub](https://github.com/PhilRW/gcontacts-asterisk)!
<!--more-->

``` python
#!/usr/bin/env python
# Original By: John Baab
# Email: rhpot1991@ubuntu.com
# Updated By: Jay Schulman
# Email: info@jayschulman.com
# Updated Again By: Philip Rosenberg-Watt
# Purpose: syncs contacts from google to asterisk server
# Updates: Updating for Google API v3 with support for Google Apps using OAuth2
# Requirements: python, gdata python client, asterisk
#
# License:
#
# This Package is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public
# License as published by the Free Software Foundation; either
# version 3 of the License, or (at your option) any later version.
#
# This package is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# General Public License for more details.
#
# You should have received a copy of the GNU General Public
# License along with this package; if not, write to the Free Software
# Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
#
# On Debian & Ubuntu systems, a complete copy of the GPL can be found under
# /usr/share/common-licenses/GPL-3, or (at your option) any later version

import atom,re,sys,os
import json
import gdata.data
import gdata.auth
import gdata.contacts
import gdata.contacts.client
import gdata.contacts.data
import argparse
from oauth2client import client
from oauth2client import file
from oauth2client import tools

# Native application Client ID JSON from the Google Developers Console,
# store in the same directory as this script:
CLIENT_SECRETS_JSON = 'YOUR CLIENT SECRETS HERE.json'


parent_parsers = [tools.argparser]
parser = argparse.ArgumentParser(parents=parent_parsers)
parser.add_argument("--allgroups", help="only works in combination with --group to show members with multiple groups", action="store_true", default=False)
parser.add_argument("--anygroup", help="show members of any user-created group (not My Contacts), OVERRIDES other options", action="store_true", default=False)
parser.add_argument("--asterisk", help="send commands to Asterisk instead of printing to console", action='store_true', default=False)
parser.add_argument("--dbname", help="database tree to use")
parser.add_argument("--delete", help="delete the existing database first", action='store_true', default=False)
parser.add_argument('--group', action="append", help='group name, can use multiple times')
args = parser.parse_args()


if args.dbname is None:
    args.dbname = "cidname"

phone_map = {2: ["A", "B", "C"],
             3: ["D", "E", "F"],
             4: ["G", "H", "I"],
             5: ["J", "K", "L"],
             6: ["M", "N", "O"],
             7: ["P", "Q", "R", "S"],
             8: ["T", "U", "V"],
             9: ["W", "X", "Y", "Z"]}

phone_map_one2one = {}
for k, v in phone_map.items():
    for l in v:
        phone_map_one2one[l] = str(k)

def phone_translate(phone_number):
    new_number = ""
    for l in phone_number:    
        if l.upper() in phone_map_one2one.keys():
            new_number += phone_map_one2one[l.upper()]
        else:
            l = re.sub('[^0-9]', '', l)
            new_number += l
    if len(new_number) == 11 and new_number[0] == "1":
        new_number = new_number[1:]
    return new_number


def get_auth_token():
    scope = 'https://www.googleapis.com/auth/contacts.readonly'
    user_agent = __name__
    client_secrets = os.path.join(os.path.dirname(__file__), CLIENT_SECRETS_JSON)
    filename = os.path.splitext(__file__)[0] + '.dat'

    flow = client.flow_from_clientsecrets(client_secrets, scope=scope, message=tools.message_if_missing(client_secrets))

    storage = file.Storage(filename)
    credentials = storage.get()
    if credentials is None or credentials.invalid:
        credentials = tools.run_flow(flow, storage, args)

    j = json.loads(open(filename).read())

    return gdata.gauth.OAuth2Token(j['client_id'], j['client_secret'], scope, user_agent, access_token = j['access_token'], refresh_token = j['refresh_token'])


def add_to_asterisk(dbname, cid, name):
    command = "asterisk -rx 'database put " + dbname + " " + cid + " "" + name + ""'"
    if args.asterisk:
        os.system(command.encode('utf8'))
    else:
        print command.encode('utf8')


def main():
    # Change this if you aren't in the US.  If you have more than one country code in your contacts,
    # then use an empty string and make sure that each number has a country code.
    country_code = ""

    token = get_auth_token()
    gd_client = gdata.contacts.client.ContactsClient()
    gd_client = token.authorize(gd_client)
    qry = gdata.contacts.client.ContactsQuery(max_results=2000)
    feed = gd_client.GetContacts(query=qry)

    groups = {}
    gq = gd_client.GetGroups()
    for e in gq.entry:
        striptext = "System Group: "
        groupname = e.title.text
        if groupname.startswith(striptext):
            groupname = groupname[len(striptext):]
        groups[e.id.text] = groupname
 
    # delete all of our contacts before we refetch them, this will allow deletions
    if args.delete:
        command = "asterisk -rx 'database deltree %s'" % args.dbname
        if args.asterisk:
            os.system(command)
        else:
            print command

    # for each phone number in the contacts
    for i, entry in enumerate(feed.entry):

        glist = []
        for grp in entry.group_membership_info:
            glist.append(groups[grp.href])

        name = None

        if entry.organization is not None and entry.organization.name is not None:
            name = entry.organization.name.text
            
        if entry.title.text is not None:
            name = entry.title.text
                
        if entry.nickname is not None:
            name = entry.nickname.text
                
        for r in entry.relation:
            if r.label == "CID":
                name = r.text
                break
    
        for phone in entry.phone_number:
            # Strip out any non numeric characters and convert to UTF-8
#             phone.text = re.sub('[^0-9]', '', phone.text)
            phone.text = unicode(phone.text, 'utf8')
            phone.text = phone_translate(phone.text)
     
            # Remove leading digit if it exists, we will add this again later for all numbers
            # Only if a country code is defined.
            if country_code != "":
                phone.text = re.compile('^+?%s' % country_code, '', phone.text)
                
            phone.text = country_code + phone.text
    
            name = name.replace("'",'')
            name = name.replace('"','')
    
            if args.anygroup:
                if (("My Contacts" in glist and len(glist) > 1) or
                    ("My Contacts" not in glist and len(glist) > 0)):
                    add_to_asterisk(args.dbname, phone.text, name)
            else:
                if args.group:
                    if args.allgroups:
                        if set(args.group).issubset(glist):
                            add_to_asterisk(args.dbname, phone.text, name)
                    else:
                        for g in args.group:
                            if g in glist:
                                add_to_asterisk(args.dbname, phone.text, name)
                else:
                    add_to_asterisk(args.dbname, phone.text, name)


if __name__ == '__main__':
    main()
```

