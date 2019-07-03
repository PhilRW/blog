---

title: "The Great FTTH Saga"
date: 2019-04-17T12:53:53-06:00
draft: false
categories:
- Tech
tags:
- internet
- ftth
- Comcast
- install
---

After many years of waiting, paitiently calling and messaging Comcast every 6 months, and a many disapppointments, the great [Fiber to the Home](https://en.wikipedia.org/wiki/Fiber_to_the_x) saga is finally coming to an end.

<!--more-->

# Previously on FTTH

Previously every time I contacted Comcast, they said that my house was within range of fiber and that they would start the process. This involved doing some calculations based on their existing network maps and then sending a field crew out to do a survey on foot. I always seemed to pass that step.

Then I would fail whatever internal criteria Comcast had for running fiber to my home. The last time they said something about my house being too far from the nearest servicable node.

But in the interim something changed. I believe it was due to the fact that Comcast upgraded my area to N+0 topology. That basically means they get rid of all the amps in the area and put nodes out as far as possible (where the amps used to be). To do this, they needed to run fiber to the existing amps and replace them with nodes. After that happened — this time around I was approved.

I decided to communicate with them through Reddit. Their customer service team is generally pretty responsive on that platform. They started the process as usual and over the course of many weeks, little bits of information trickled in. Here's a timeline:

* Jan 26: Initial inquiry.

* Feb 3: 
  
  > I'm in the process of reaching out to our local leadership now to have them see what can be done about bringing Gigabit Pro service to the area.
  
* Feb 7:

  > "...you do qualify for Gigabit Pro at this time. However, we're working on surveying the area to see what needs to be done to install it.

  (I've heard this before.)

* Feb 11: Outside fiber contracter called me with questions. (That was a new one for me.)

* Feb 14:

  > "...we haven't forgotten about you.

* Feb 22:

  > I'm still talking with the construction team to try to get some updates for you.

* Mar 12:

  > We were having some trouble getting the construction team and the sales team in touch with each other, but we're making some progress.

* Mar 13:

  > ...everything was forwarded to the finance team so we're just waiting to hear back from them now.

* Mar 19:

  > Looks like the financial team approved the order and now we're waiting on permits.

* Apr 4:

  > I touched base with our local partners this morning and they confirmed that permits are approved, locates have been called in, and they're moving towards scheduling a bore.

For reference, the name of the Comcast's service offering is called Gigabit Pro and it will cost $1000 to install + $300/month for 2Gbps symmetric service + $20/month equipment rental. I was paying $200/month for DOCSIS 3.1 with 1Gbps/35Mbps down/up. Upstream will be at least 57x faster on fiber.

# Ext. Street - A Boring Situation

On April 15, "no parking" signs were set up on my block. Around noon a utility locator crew showed up at my door and wanted to get a head start on marking the sewer line. We rescheduled for the next morning since I was at work at the time. I learned from them that the bore was scheduled for the next day.

![ROAD WORK AHEAD: an empty street with yellow cones on either side](/images/IMG_20190415_153642995.jpg)

The morning of April 16 the locator crew showed up, as well as a streetload of construction equipment.

![trucks lining both sides of the street](/images/IMG_20190416_133708849.jpg)

The locator crew had some trouble finding the sewer line once it went underneath my garage, but since the sewer in the street was 11 feet deep, the boring crew was not at any risk of collision until they got to my house since they went at about 2 feet of depth from the pole to the house.

The crew bored underground from a spot parallel to the back of my house to the utility pole.

![boring machine in front yard](/images/IMG_20190416_134312219_HDR.jpg)

![boring machine as seen from street](/images/IMG_20190416_134350428_HDR.jpg)

Then they attached to the end of the conduit and pulled it through the bore.

![crew feeding conduit](/images/IMG_20190416_134338560_HDR.jpg)

Repeating the process, they turned the machine 90 degrees and bored between the garage and the back of the house. It was tricky and the locator operator said it took them seven attempts. Initially they were going to go under the sewer line (which was at a depth of 2'3") but they ended up going over it. Apparently my soil has lots of rocks in it.

I knew that already.

![crew boring towards house](/images/IMG_20190416_140340437_HDR.jpg)

Ultimately I was left with this at the base of the pole:

![utility pole and in-ground box labeled with fiber warning](/images/IMG_20190416_140015817_HDR.jpg)

And, after another crew came on the 17th to connect the conduit and pull the fiber through, this at the back of the house:

![a few inches of conduit stick up above ground next to siding](/images/IMG_20190417_123627876_HDR.jpg)

Ignore that hole in the siding. I'll fix that.

By early afternoon on the 17th, all the traffic signs and cones were gone and the exterior contractors had finished. It was now up to Comcast.

----

Then around noon on the 18th, Comcast said, "The project manager let us know that the bore permit is in, design is done, and they're now waiting on the equipment to arrive. He's not sure when it will arrive however he'll keep us posted."

:man_facepalming:

# Int. Basement - Yes We Conduit

The morning of Monday the 22nd, the interior contractor called me to set up the install for the morning of Wednesday the 24th.

At 10 a.m. the contractor showed up to run the interior fiber. It took them a few hours to run the interior conduit and pull fiber from the server rack out to the vault near the pole.

![two trucks](/images/IMG_20190424_124349924_HDR.jpg)

![assembling the outside fiber entry point](/images/IMG_20190424_105523297.jpg)

![assembled fiber entry point](/images/IMG_20190424_124221080_HDR.jpg)

![the orange conduit holds the yellow fiber](/images/IMG_20190424_124630999.jpg)

![interior of rack mount fiber patch panel](/images/IMG_20190424_124742031.jpg)

They indicated that the fiber splicer(s) would potentially show up later that week or early the next…

...and they were right. Upon approaching my home at 16:00 on Tuesday the 30th, I saw two vans outside my house.

![two vans parked on the street](/images/IMG_20190430_160156882_HDR.jpg)

The splicers took about an hour to test everything and they informed me that they tested about 39,000 feet of fiber back to the headend. They told me to call Comcast and get them to hook me up. :sunglasses:

----

# Hiatus Update: Jun 19

It's been almost two months since the last activity from Comcast. I received this today from their Reddit rep:

> Good morning. I heard back from the project manager. He let me know that there is some additional equipment that needs to be installed. He's working with the proper teams to get that done. I'll keep you informed with progress.

# Update: Jun 27

I received a call from Comcast today asking me to confirm the service order and installation time. It's scheduled for Tuesday, July 2, 1300-1500. She asked me if I'd be using "[my] own modem" for this service and I explained to her that it's a $10K piece of equipment so no, I would be renting theirs.

# Update: Jun 28

I received an email from Comcast Business with my static IP information and some basic information on what they would be providing.

# Update: Jul 02

Two techs in two vans showed up at about 13:45.

![the final two vans](/images/IMG_20190702_153749002_HDR.jpg)

After a minor kerfuffle with the remote/headend SFP tuned to the wrong frequency, the "light" looked good at -15. They installed the Juniper ACX2100 and proceeded to the next step, which was tuning the local SFP+ module to the right frequencies….

…Which they could not accomplish even using a different router and different SFP+ modules. They finally gave up at 17:52 after all the rest of their support staff had left for the day. The plan was to reconvene later (possibly the next day).

I asked about how many of these residential installs they did and they said mine was the first.

# Roll Credits

The tech Daniel called in the morning and said he'd be back at 10 am. He was there on the dot. They had managed to tune the SFP+ to the proper channels at the headend.

He finally got the connectivity test working at 13:00 after multiple calls to different techs and tech supports.

Then at 15:00 he finally finished. Turns out Comcast's documentation for the techs was inadequate. We basically had to *guess* the correct IPv6 addresses from the P2P link range they gave us. Hint: Comcast's doing it like IPv4 with a /126. The 2nd IP in the subnet is the router and the 3rd IP is the local address. But hey — it only took 5 hours!

----

And then there was fiber internet.

And it was good.

![Google Fiber Speed test screen shot: 1532 Mbps down/710 Mbps up](/images/Screen Shot 2019-07-03 at 5.21.03 PM.png)

I'm still looking for a speedtest server that will handle 2 Gbps.