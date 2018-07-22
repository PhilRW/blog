---
author: philrw
categories:
- Tech
comments: true
date: "2017-11-17T19:06:40Z"
link: https://philrw.wordpress.com/2017/11/17/decisions-made-easy/
slug: decisions-made-easy
tags:
- renewable energy
- solar power
- technology
title: Decisions Made Easy
wordpress_id: 87167
---

![/images/screen-shot-2017-11-17-at-11-58-00.png](/images/screen-shot-2017-11-17-at-11-58-00.png)

Data makes decisions easier. Let's look at an example:

<!--more-->


  1. We recently got solar panels on our house. We're producing power and all is good.

  2. The electric company ([Xcel](https://en.wikipedia.org/wiki/Xcel_Energy)) recently made an optional billing rate available called Time-of-Use metering (TOU). Our current flat-rate (tier 1, <500KWh/month) billing is roughly 9¢/[KWh](https://en.wikipedia.org/wiki/Kilowatt_hour). TOU rates charge you differently depending on what time of day it is, since "peak" power costs them more to deliver. Here are the approximate _wintertime_ TOU rates:


    1. 8¢/KWh Off-Peak 21:00-09:00


    2. 10¢/KWh Shoulder 09:00-21:00


    3. 14¢/KWh On-Peak 14:00-18:00 weekdays (non-holidays)	

      4. Xcel will credit us into a virtual "solar bank" for electricity at the rate and time we generate it under TOU metering, or a simple KWh solar bank under flat-rate metering.

  3. Which plan would be worth more to us?


A lot of factors go into this calculation. With flat-rate it's easy, just look at the net meter at the end of the month and see whether it's positive or negative to find out whether you owe money or built up your "solar bank." With TOU it's not so easy. You have to calculate your net usage depending on summer/winter, time of day, and the cost for that time of day.

Fortunately I wrote a program to figure that out. Combined with a [home energy meter](https://aeotec.com/z-wave-home-energy-measure), [SmartThings](https://en.wikipedia.org/wiki/SmartThings), and a [logging server](https://www.influxdata.com/), I was able to calculate the difference.

We only have data for a few days so far but the results are telling:


    2017-11-12 Sun: TOU $-0.48 vs flat-rate $-0.25
    2017-11-13 Mon: TOU $-0.71 vs flat-rate $-0.31
    2017-11-14 Tue: TOU $-0.31 vs flat-rate $ 0.00
    2017-11-15 Wed: TOU $-0.37 vs flat-rate $ 0.11
    2017-11-16 Thu: TOU $-0.19 vs flat-rate $ 0.12
    ==================
    On-peak:  $  -1.51
    Shoulder: $  -5.19
    Off-peak: $   4.65
    ==================
    TOU Sum:  $  -2.05
    Flat Sum: $  -0.33


Switching to TOU net metering shows a >6x increase in profitability (given immediate monetization) over the past 5 days.

Now, things could (and will) change. It's _not_ always sunny in [where I live]. Xcel could (and will) raise its rates in the future which would make the flat-rate KWh bank worth more (...but by >6x)?

Still, the data doesn't lie. It may be inaccurate -- and the [home energy meter](https://aeotec.com/z-wave-home-energy-measure) I used to collect this data does show some drift compared to Xcel's power meter -- but it doesn't demonstrate bias. Data has no emotional investment or opinions.

Not [_that_ Data](https://en.wikipedia.org/wiki/Data_(Star_Trek)) (sorry).

So... we've applied for TOU pricing. Combined with solar generation it's a no-brainer, although making the decision does require some smarts. Were we not solar producers, the decision might be more difficult.

I'll have to run that scenario for fun.


