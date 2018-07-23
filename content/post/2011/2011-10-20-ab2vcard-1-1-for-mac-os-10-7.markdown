---
author: philrw
categories:
- Personal
- Tech
comments: true
date: "2011-10-20T18:13:53Z"
link: https://philrw.wordpress.com/2011/10/20/ab2vcard-1-1-for-mac-os-10-7/
slug: ab2vcard-1-1-for-mac-os-10-7
tags:
- language
- Mac
- programming
- solution
title: ab2vcard 1.1 for Mac OS 10.7+
wordpress_id: 3620
---

I was using [ab2vcard](http://scottstuff.net/ab2vcard/) to sync my Mac OS X Address Book with my PBX. It was working great for many years. Then Apple up and removed [Rosetta](http://www.apple.com/asia/rosetta/) support from Mac OS 10.7 Lion and I was up the creek. So I hacked together a klugey fix by importing the source code into Xcode 4 and recompiling and ta-da! It works.

If anyone wants the new binary, let me know and I'll post it here. Otherwise you're probably already adept enough to recompile it for Intel on your own. This was my first foray into Xcode and Objective-C.
