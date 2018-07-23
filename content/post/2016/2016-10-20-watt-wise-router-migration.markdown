---
author: philrw
categories:
- Tech
comments: true
date: "2016-10-20T16:22:42Z"
link: https://philrw.wordpress.com/2016/10/20/watt-wise-router-migration/
slug: watt-wise-router-migration
tags:
- computery
title: Watt-wise router migration
wordpress_id: 86156
---

As part of a small project at work, I get to play around with this -- shall we say _electrically efficient_ -- routing hardware. My reasons for switching (including having a virtualized router that was causing me some headaches) and install notes are basically the same as his, with a couple of exceptions:

<!--more-->


  * I like to use ddrescue instead of dd for writing the install image to the USB drive, since it gives me a nice completion percentage and estimated time remaining. (I learned that some old USB drives I have are _really slow_.)

  * After installation, I tried multiple times to restore my existing configuration. The default console speed on my previous install was 9600, so that needs to be taken into account when connecting via USB serial console cable after the config restores and the device resets. I thought the dang thing was stuck.

  * I had some issues with DNS latency absolutely _killing_ my install and upgrade times. Once I had restored the config, my DNS Resolver sources the /var/unbound/pfb_dnsbl.conf file created by pfBlocker, but since pfBlocker hadn't been installed or run yet, DNS wouldn't start, so I ended up installing it _before_ the restore, and then manually running a force update after the restore. That fixed the DNS issues.

> After some frustration with stability and latency connecting my virtual pfSense router to my cable and DSL modems, I decided to switch to a physical box. I selected the Netgate RCC-VE 2440 as my hardware platform, since it's the same box that pfSense themselves use as their OEM bundle. It also checks all the boxes with a dual-core Atom CPU, four Gigabit Ethernet ports, and low-power fanless design. Here's my first impression and installation notes!


Source: _[The Ideal pfSense Platform: Netgate RCC-VE 2440 - Stephen Foskett, Pack Rat](http://blog.fosketts.net/2015/09/21/the-ideal-pfsense-platform-netgate-rcc-ve-2440/)_
