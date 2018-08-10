---
author: philrw
categories:
- Tech
comments: true
date: "2006-11-23T00:32:00Z"
link: https://philrw.wordpress.com/2006/11/22/hooray-for-recipient-delimiters-geek-alert/
slug: hooray-for-recipient-delimiters-geek-alert
tags:
- computery
title: Hooray for recipient delimiters (geek alert)
wordpress_id: 245
---

I’ve spent the last day integrating the amavisnewsql plugin with Squirrelmail and figuring out how to use my custom and separate alias maps and virtual alias maps in postfix. The workaround came by putting the alias map hash in the virtual_alias_maps list. This treated all of my local alases like virtual aliases and caused Postfix to rewrite them so that the amavis-new SQL lookup would match my custom SpamAssassin level settings to me and not ignore the email that was previously addressed to my alias and, amavis thought, to someone else.

I have now changed the recipient delimiters from + to - in the hopes that 1) I won’t have to edit my alias table every time I want to give a website a new e-mail address (for avoiding and tracking spam) and, 2) some websites see the “+” character as invalid for email addresses. So woo-hoo to that!

Now I had some special aliases that had dashes in them, such as “me-mycellphone” to send me SMS directly without the sender having to remember my blasted SMS email address, and I thought changing the delimiter could have a negative effect on that. But after testing it I’m happy to say that the custom aliases with the “-” character still work fine, in addition to making up as many as I want along the way without having to edit the alias file via the recipient delimiter specification. Just remember to change it in local.cf **and** amavisd.conf.

For a postmaster geek, life is good. :slightly_smiling_face:

http://borosenclave.com/index.php?p=106 (link broken)
