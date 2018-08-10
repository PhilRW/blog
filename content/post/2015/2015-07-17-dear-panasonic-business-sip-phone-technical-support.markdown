---
author: philrw
categories:
- Personal
- Tech
comments: true
date: "2015-07-17T20:34:30Z"
link: https://philrw.wordpress.com/2015/07/17/dear-panasonic-business-sip-phone-technical-support/
slug: dear-panasonic-business-sip-phone-technical-support
tags:
- bugs
- technology
- telephony
- wireless
title: 'Dear Panasonic Business SIP Phone Technical Support:'
wordpress_id: 85757
---

I can't figure out how to reach you. What is your phone number? What is your email address? These things I may never know.

Anyway, I need to report a bug in the latest version of your KX-TGP600 phone's firmware, and you leave me no choice but to post it publicly on my blog. I can only hope someone who works for you will find this, as I really like the KX-TGP600 otherwise.

You claim wideband audio support, but you screwed up the SDP for G722. It should read:

    a=rtpmap:9 G722/8000

but instead it reads:

    a=rtpmap:9 G722/16000

This is wrong. My PBX doesn't know what to do with that. (It complains, "Found unknown media description format G722 for ID 9".)

Please, [read the RFC](https://www.ietf.org/rfc/rfc3551.txt) (see section 4.5.2), fix the firmware, and get back to me. I want my HD voice calls, dammit! That was one of the reasons for me to get the phone, but it won't talk wideband with my SIP server (Asterisk). All of my other HD SIP phones get it right. Do you not perform basic interoperability testing before releasing a product?

Thanks.
