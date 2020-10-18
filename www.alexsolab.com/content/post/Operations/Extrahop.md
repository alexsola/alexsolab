---
title: "Extrahop: Applications containers"
date: 2016-10-09T20:05:22+01:00
draft: false
---

**Disclaimer alert:** as this was something we did at work, I will use code names for applications, calls, etc. There will be no real data shown. I need to keep the privacy statement. But Extrahop is an external product.

Yesterday I helped a friend in building some custom monitoring for an application we support (from now on I will call The Application aka TA) and a specific call (Which from now on will be The Call aka TC). For this we used Extrahop. If you are not familiar with it, here comes a brief description: Extrahop captures a replica of your traffic taken using port mirroring in the switches, and parses all important data. Allowing you to analyse it afterwards. This tool has many features. For more information, refer to the links section below.

So we had this problem: Sometimes, for many different reasons, one loadbalancer that is in front of a farm of servers (round-robbin among them with session stickiness based on source IP) gets full and not allows more connections to succeed. When this happens, one specific call from TA cannot happen. And this creates an outage on some part of the system. Which is not good. Apart from implementing the corresponding alarm based on the connection number in the loadbalancer, we wanted  to have also a check on TC, so we could detect this failure even in cases the loadbalancer is good. For this we decided to go for three Extrahop characteristics: Triggers, Alarms and Applications. I must admit I enjoyed this.

This was my first hands-on into a production Extrahop system. I had some practice in a training we had, but never with real applications in the real world. And also, in the training we saw triggers but we never set an alarm or an application, so there was a lot new to me. Apart of the memory factor: I had the training a long ago, so most of the details were gone. Said this the following makes more sense. As my first satisfactory action to face my memory problem was succeed with no pain thanks to the fantastic help system you have integrated. It has even video tutorials, so after finding and reading the pages for triggers and alarms, I watch a video tutorial (about 10 minutes) for the application part. So was very easy to implement one environment, and replicate the idea to other 3. 

An Application in Extrahop is a logical container to treat a specific application. You define how this application works (using triggers, a powerful scripting engine) and associate this with hosts that have it, alarms that defines thresholds in which trigger warnings or errors, locations, etc.

# Links:

Extrahop official webpage: [https://www.extrahop.com](https://www.extrahop.com)
