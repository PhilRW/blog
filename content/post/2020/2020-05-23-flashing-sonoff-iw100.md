---
title: "Flashing Sonoff IW100"
date: 2020-05-23T17:06:35-06:00
draft: false
categories:
- Tech
tags:
- home automation
- esphome
- sonoff
- iw100
---

I hadn't found anything on the internet yet describing how to flash a [Sonoff IW100 smart socket](https://www.itead.cc/sonoff-iw100-iw101.html), so I thought I'd share my experience.

<!--more-->

The RX and TX pins are labeled as they would be conneted to a UART flasher. Wire RX to RX and TX to TX. It's weird, but that's how they did it.

Unlike the S31 which has a mechanical button connected to GPIO0, the IW100 has a capacitive button. To short GPIO0 to allow for flashing, use a small F/F jumper to connect GND to TOUCH on the header pins that connect to the front panel capacitive button/LED board. Connect everything together, plug in the USB UART programmer, and quickly upload your firmware.

That is all. Proceed as usual. It is an ESP8285.