---
author: philrw
categories:
- Personal
- Rants and Raves
- Tech
comments: true
date: "2013-06-12T17:10:56Z"
link: https://philrw.wordpress.com/2013/06/12/secure-synchronous-voice-ostn/
slug: secure-synchronous-voice-ostn
tags:
- OSTN
- security
- telephony
- VoIP
title: 'Secure Synchronous Voice: OSTN'
wordpress_id: 79926
---

Okay, folks, it's time to talk security again. I've proselytized [email security](https://blog.rosenberg-watt.com/2012/05/23/google-privacy-inquiries-get-little-cooperation-nytimes-com/) and [two-factor authentication](https://blog.rosenberg-watt.com/2011/05/17/official-google-blog-advanced-sign-in-security-for-your-google-account/) in the past, and now I'm going to tell you about voice calls. I was going to say phone calls, but we're way beyond -- and in many ways simpler than -- the traditional telephone model.<!--more-->

## But first, some fundamentals...

Back a long time ago (10 or 20 years ago), people had to use the phone company to connect their calls. They would pay Ma Bell a monthly fee and get a phone number in return. The phone companies took care of connecting all the calls for us. There were laws to protect persons from eavesdropping, and to wiretap someone meant that you had to physically connect a device to the phone line somewhere along the signal path between your phone and grandma's phone. (Gotta get that secret family recipe for chocolate chip cookies...)

Jump-cut to now: Customers still have the same experience, i.e., pick up a phone, dial a number, etc., but the technology between the two endpoints (you and grandma) is significantly different. It's all electronic and digital and computerized and stuff. What this essentially means for you is that if someone wanted to record your phone call (never mind the metadata about it), all he would have to do is check a little box somewhere or enter your phone number or some other thing that identifies you in a computer database somewhere and -- BAM -- all of your calls are being recorded or otherwise monitored. (Note: this is a bit different than snooping email because as the servers along the route store and forward the email, they're _supposed_ to make a copy of your email -- it's by design. Betcha didn't know that, did ya?)

So maybe the NSA isn't recording our phone calls. Maybe they don't have humans listening in. But that doesn't mean that fancy dancy computer programs aren't listening for certain words or phrases automatically. Police departments do something similar with automatic license plate scanning to find stolen vehicles. Courts have said that it's not special treatment if _everyone_ gets scanned, that way human prejudice doesn't play into it.

At any rate, the point is that anyone along your network path can record your phone calls, especially if it's Internet-based or digital. I'm not so worried about the government doing it as I am concerned with the possibility that creative criminals could listen in on your conversations. (Most crimes are crimes of opportunity, and digital technology makes it very easy.) True, most phone calls are exceptionally boring, but every once in a while I need to tell someone a bank account number, credit card number, or PIN over the phone because they haven't friggin' implemented secure email yet!!! And all my calling is done over the public Internet (see: it's CHEAP) that eventually connects me to the POTS (plain ol' telephone service). Heck, if _I_ can record and decode a phone call over my home network, _it ain't that hard, folks._

## What's the answer?

So, what if you could have totally encrypted calls that just, oh, I don't know, _bypassed_ all this antiquated and expensive telephone infrastructure. After all, every computer and mobile phone nowadays has Internet access, right? Could I use something easier to remember like an email address or username or something? Couldn't my Android phone call your iPhone directly using the Internet and we could have the two devices talk to each other without any other servers or anything in the way? Well good news: now you can! And it's super easy, too. Plus, it's kinda fun and you feel a little bit like James Bond when you make a call.

I won't go into all of the technical details but trust me when I say that it is neigh impossible to intercept your voice calls over this new "standard." You look at a four-character code that your phones have exchanged and verify it with the person on the other end to make sure they see the same code, too (that's the James Bond part I was talking about -- I like to use international phonetics like "alpha," "bravo," and so on). They're calling it [OSTN](https://dev.guardianproject.info/projects/ostn/wiki?title=OSTN), for Open Source (or Secure, or whatever) Telephony Network, and it's based on current best practices and available tech for VoIP (Voice over Internet Protocol) and security [[See here](https://guardianproject.info/2013/06/12/carrier-grade-verizon-and-the-nsa/) for a blog about it]. All you need is a computer and/or a smartphone (you obviously have one, how else could you read this), an email address to register your account, and an IQ of about 100, give or take one standard deviation. [Ostel](https://ostel.co/) is the name of the service and at the moment you can call me at prw@ostel.co. It's like using Skype, only better because it's free and **open source** and stuff. (Nobody really knows [how secure Sykpe is](http://en.wikipedia.org/wiki/Skype_security#Flaws_and_potential_flaws) 'cause they won't tell anybody.) Plus they have a very good [privacy policy](https://ostel.co/privacy) that doesn't save any identifying information.

Oh, by the way, I should also mention that the default technology used in OSTN to get your voice from point A to point B is _twice_ as clear as normal phone calls. Seriously, I do this stuff for a living. Once you've experienced HD Voice (or wideband, or G.722, or whatever you want to call it), you'll never want to go back to regular (narrowband) phone calls again.

And did I mention it's free?

To summarize:

1. Encrypted like spy technology

2. Twice as clear as regular phone calls

3. Free

