---
author: philrw
categories:
- Tech
comments: true
date: "2009-12-29T03:06:13Z"
link: https://philrw.wordpress.com/2009/12/28/fetchmail-m-bash-script-printer-and-gcal/
slug: fetchmail-m-bash-script-printer-and-gcal
tags:
- scripting
title: 'fetchmail -m bash script: printer and gcal'
wordpress_id: 42
---

I just wrote this little bash script as a fetchmail MTA/destination. It automatically prints and adds to my gcal any new appointments scheduled for my by Fastteks. Since they have a crappy web calendar and only send notifications via plaintext email, I wrote this script to automate some things for me. Every five minutes it removes unnecessary information, sends it to my office printer, and adds an appointment to my business Google calendar all automatically.

In addition to fetchmail, this script needs gcalcli.

Cool.

``` bash
#!/bin/sh

PRINTER=BrotherMFC9840CDW

TMPFILE=/tmp/emailprint.tmp
cat $1 > $TMPFILE

if [ -f $TMPFILE ]
then
sed -e ‘/^First Follow-up Call Action Taken/d’ -e
‘/^Follow-up /d’ -e ‘/^Conclusion/d’ -e ‘/^Use end date/d’ -e
‘/^Message-ID:/d’ -e ‘/^X-Forwarded-/d’ -e ‘/^Repeat Type/d’ -e
‘/^Repeat End Date/d’ -e ‘/^Frequency/d’ -e ‘/^Group/d’ -e ‘/^Satisfied
with Results/d’ -e ‘/^Content-T/d’ -e ‘/^Mime-Version:/d’ -e ‘/^
/d’ -e ‘/^   /d’ -e ‘/^Message-Id:/d’ -e ‘/^Please
look on Fastteks Solution Center/d’ -e ‘/^http:/d’ -e ‘/^Received:/d’ -e
‘/^Return-Path:/d’ -e ‘/^Received-SPF:/d’ -e ‘/^Delivered-To:/d’ -e
‘/^Authentication-Results:/d’ -e ‘/^X-IronPort-Anti-Spam-/d’ -e
‘/^X-Mailer:/d’ -e ‘/^Customer Number/d’ -i $TMPFILE
#       cat $TMPFILE
lp -s -d $PRINTER $TMPFILE
fi

if [ -f $TMPFILE ]
then

WHAT=`cat $TMPFILE | grep “A new appointment
has been made for you by ” | sed -e ‘s/.*Brief Description //’ -e
‘s/”//g’`
STREET=`cat $TMPFILE | grep “^Address” | sed -e ‘s/^Address //’ -e ‘s/”//g’`
CITY=`cat $TMPFILE | grep “^City” | sed -e ‘s/^City //’ -e ‘s/”//g’ -e ‘s/,//’ -e ‘s/(.*) /1/’`
STATE=`cat $TMPFILE | grep “^State” | sed -e ‘s/^State //’ -e ‘s/”//g’`
ZIP=`cat $TMPFILE | grep “^Zip Code” | sed -e ‘s/^Zip Code //’ -e ‘s/”//g’`
DATE=`cat $TMPFILE | grep “^Date” | tail -n 1 | sed ‘s/^Date: //’`
TIME=`cat $TMPFILE | grep “^Time” | sed ‘s/^Time: //’`
WHERE=”$STREET, $ZIP”
WHEN=”$DATE $TIME”

CMDTXT=“FT: $WHAT at $WHERE $WHEN”
GCOMMAND=”/usr/bin/gcalcli quick ‘$CMDTXT’”

if [ -n “$WHAT” ]
then
sh -c “$GCOMMAND”
fi

fi

if [ -f $TMPFILE ]
then
rm $TMPFILE
fi
```