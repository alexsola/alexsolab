---
title: "QNX: Introduction to an RTOS (Part 1)"
date: 2016-10-13T19:21:51+01:00
draft: false
---

Again, a newbe here. Exploring this awesome OS: QNX RTOS. First, I think the concept of “RTOS” should be explained. At least, what I understand an RTOS is. RTOS stands for RealTime Operating System. The idea, very roughly,  is that whatever event comes into the system, it should react to it and give a proper response within 1ms, in other words, the processing boundaries (time that will take to process something) are known in advance. Seems I was not very far… I am adding the link to Wikipedia at the bottom (links section). These systems are widely used in embedded devices that requires very low response times, for instance: missile tracking systems, software driven cars, the equipment in the cockpit of a military plane, medical equipment, etc.

My experience with it comes from long, long time ago… first time I saw it was around 1999 and I was really shocked when a friend of mine came with a 3.9″ diskette with a whole OS in it. I was more impressed even when, not only it was true, it also came with some example software and a complete graphical environment. I was so amazed that I made a copy of that wonder disk and later on I installed it in a partition of my workstation…. for nothing… I did nothing with it apart form playing solitaire or watch the OpenGL demo of some 3D text rotating in a window. I had no easy internet access on those days, so documentation was also not that easy to find… From then till now, I have installed it for a while, and again, doing nothing with it… mainly because I had no time to read the docs and test properly. So I decided to start going into it a bit more and, this time, I installed a VM and has started to read documentation.

![qnx photon 001](/img/qnx_Photon_001.png "The Photon graphical environment, very lightweight.")

This time, I am in the good path. I have only read some introduction section and some ideas about the microkernel and the approach. And is very interesting, mainly the idea of network oriented system it has: all nodes in the network has an unique identifier and they interact using IPCs to create an abstraction layer as if they were a single system. The kernel is basically an scheduler and a system for messages to be delivered. Processes access hardware through services. Which are user process governing HW and offering its features as a service. This resembles me the fundamentals of Plan9 (Idea: maybe a “QNX vs Plan9” page? will think about it).

# Links
* Wikipedia definition: [https://en.wikipedia.org/wiki/Real-time_operating_system](https://en.wikipedia.org/wiki/Real-time_operating_system)
* Official QNX webpage: [http://www.qnx.com/content/qnx/en.html](http://www.qnx.com/content/qnx/en.html)
