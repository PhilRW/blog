---
author: philrw
categories:
- Personal
- Tech
comments: true
date: "2011-03-16T18:40:09Z"
link: https://philrw.wordpress.com/2011/03/16/asterisk-gafachi-t-38-finally-working/
slug: asterisk-gafachi-t-38-finally-working
tags:
- Asterisk
- Gafachi
- T.38
- telephony
title: Asterisk + Gafachi + T.38 = Finally Working
wordpress_id: 3204
---

I thought I'd share what I learned about configuring [Asterisk ](http://www.asterisk.org/)1.8 to work with [Gafachi ](http://www.gafachi.com/)inbound T.38 faxing. It took many days of trial and error but I finally have a configuration that works.<!--more-->

Here are the ingredients:



	
  * Asterisk 1.8 (using SVN-branch-1.8-r310834)

	
  * [spandsp](http://www.soft-switch.org/downloads/spandsp/) 0.0.5

	
  * res_fax and res_fax_spandsp


You must use spandsp-0.0.5, since spandsp-0.0.6 causes a segmentation fault in Asterisk. Also remember to either delete app_fax.so from your modules directory or put a noload statement in modules.conf, otherwise Asterisk will crash on startup.

It is not necessary to place t38pt_udptl=yes in the [general] section of sip.conf. It will suffice to place it in your [gafachi1?] peer. Also place insecure=invite and reinvite=yes in your [gafachi1?] peer. As of this version of Asterisk, the maxdatagram= setting is completely ignored, or at least I can find no way to make Asterisk honor the setting in the SIP INVITEs. _sip show peer gafachi1?_ shows the specified maxdatagram but the actual SIP SDP message does not honor that setting.

I have my Gafachi fax DID going to ReceiveFax(filename) in my dialplan and it's working correctly.

Also be aware that some advanced home firewalls randomly reassign outgoing ports. This was breaking my udptl port range implementation, and I needed to turn on static port mapping for outgoing NAT in my firewall to get T.38 faxing to work.

It took about 4 days of tweaking, recompiling, restarting, and reloading to find a configuration that works. Gafachi has no instructions specifically for Asterisk 1.8 on their website, but fortunately the insecure=invite seemed to take care of the authentication issue.

Aside from Asterisk module and peer configuration, my dialplan calls efax4asterisk.sh which needed tweaking for my system. Because Asterisk runs as -U asterisk I had to preface the mutt command with sudo -u asterisk, otherwise mutt failed to send the received fax in an email. Of course that makes it necessary to edit the sudoers command with visudo to allow asterisk to run sudo mutt passwordless.

Note: This uses Asterisk as the T.38 endpoint. Heaven help he who has a T.38-capable SIP ATA connected to a physical fax machine.
