---
title: "Plan9: Test Plan9 VMs (Part 1)"
date: 2016-10-06T18:59:46+01:00
draft: false
---

For most of the people, Plan 9 is an underrated film directed by Ed Wood. But for others, who have seen the light, there is another Plan 9…. The operating system.  Created by the same great minds that crafted and designed Unix and C…. First of all, I am not an expert in PLan9 but a curious engineer that is interested in grid computing. I will write another post about my thoughts about this awesome operating system, but if you want to have more information now I recommend visiting the official documentation from the creators themselves:


![Glenda](/img/Glenda_NoMuyBien.png "Glenda, Plan9's "Pet"")

[http://plan9.bell-labs.com](http://plan9.bell-labs.com)

This page is about a setup I want to play with. But to be clear on the description of the project, I have to define some aspects of Plan 9:

* Plan 9 continues with the Unix premises and addresses any resources as files. So in Plan 9 everything is a file, with basic files operations like open, close, read, write and few more.
* In Plan 9, everything is service oriented, so when a process wants to make use of a resource needs to do so by requesting it to the service governing that resource.
* All processes and servers talk in p9. P9 is a message based protocol to communicate everything.
* In Plan9 exist the following types of nodes:
  * Authentication node: Is a CPU running the authentication server.
  * File system server: Is a server offering services of file system in the network.
  * CPU server: Is a server which offers cpu services to the network.
  * Terminal: The client program and host.
* One important concept in Plan9 is the name space. The name space represents all  files (and by definition, resources in general) the user can access in a given session.  Every session has its own name space and it changes dynamically while jumping from one host to the other.
* Every Terminal offers the resources from the host it is run. So when running drawterm (client program to access plan9) from my system, I am exposing my CPU as service and my filesystem. This way, for instance, transfer of files is transparent among my workstation and the remote server.

![Plan9 Desktop 001](/img/plan9_screenshot_001.png "Example desktop of Plan9 through Drawterm. What is seen here is the Rio interface.")

Above, the default desktop of one of the nodes in the grid (Plan9n1, actually). To implement a scenario where Plan9 makes sense, I think more than one system is needed. To achieve this (and in the meantime I order some RaspberryPI’s to make a real cluster), I wan to use virtualisation. As Plan9 requires very little memory to run, and I am not measuring performance, I am creating 4 virtual machines in Virtualbox with following characteristics each:

* 1 CPU
* 512Mb RAM
* 2GB HDD

I have assigned the following names and roles:

* Plan9n1: cpu server, file server, authentication server
* Plan9n2: cpu server
* Plan9n3: cpu server, file server (replica)
* Plan9n4: cpu server, venti server (filesystem archiver)

In next chapter, I will explain a bit more in detail what is going to be the goal of this project, and will clarify which stage of it I am at the moment. Then will make some pages to explain how to get to that point, and from there we will investigate how to achieve the solution.
