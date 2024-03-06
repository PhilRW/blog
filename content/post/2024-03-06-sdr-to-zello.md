---
title: "SDR to Zello: Boulder"
date: 2024-03-06T11:55:50-07:00
draft: false
categories:
- Tech
- Ham
tags:
- software
- computery
- software engineering
- amateur radio
- SDR
- linux
- Zello
---

To promote my own personal situational awareness (especially during fire season which is pretty much all year), I combined some radio + software magic and created a couple of feeds of police and fire dispatch in Boulder County. I thought I would share this with the community. Enjoy!

<!--more-->

I created a software project that generates custom scanner feeds based on audio files of digital radio transmissions decoded from SDR receivers. One of the things this project does is feed the various talkgroups/transmissions into channels in Zello, a walkie-talkie-like app for smartphones. The software is a mess and not ready to share yet, but I thought I'd share a couple of the channels it feeds.

Please keep in mind the successful operation of these channels depends on many components, including the reliability of my electricity, internet connection, computers running the feeds, and the SDR devices decoding the transmissions. Any one of these could fail at any time and I am but one humble software engineer doing this in my spare time for fun. Please help me keep it fun. 😀

That being said, right now I have two main channels for monitoring local dispatch:
 - [Boulder County Scanner 02](https://zello.me/k/ivfAi): City and County Fire dispatch
 - [Boulder County Scanner 03](https://zello.me/k/ivq8Q): City and County Police/Sheriff dispatch

The cool thing about this project is that, unlike a traditional scanner, you don't miss any transmissions. They queue up in order received. There may be a bit of a delay depending on how busy the radio systems are, but the transmissions will generally go through. Dispatchers also acknowledge transmissions with the current time (in 24-hour format), so you know how long of a delay there is.

Right now my receiption of the Boulder (the city) radio system is marginal at best (since I am not actually in the city of Boulder), so their transmissions may be garbled sometimes. The county uses a different system that I have no problems receiving.

ℹ️ Note: Zello incorporates a rate limit into their API, but they don't *tell* you what it is, so sometimes when things get super busy, the Zello channels don't work at all. I'm in the process of experimenting with different delays.
