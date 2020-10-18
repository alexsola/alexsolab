---
title: "Plan9: Test Plan9 VMs (Part 2)"
date: 2016-10-14T19:38:20+01:00
draft: flase
---

As we saw in the previous part, this chapter will define the project in details, and will explain the current situation and what I think are the next steps I should take. The first thing we need to remember is the description of the environment we did in the previous part. But in case it cannot be remembered, here is a summary:

* The environment is composed of 4 VMS:
  * 1 CPU
  * 512Mb of RAM
  * 2GB HDD
* The following names and services distribution:
  * Plan9n1: cpu server, file server, authentication server
  * Plan9n2: cpu server
  * Plan9n3: cpu server, file server (replica)
  * Plan9n4: cpu server, venti server (filesystem archiver)

To be more clear, please, see the following diagram:

![plan9 diagram 001](/img/Plan9_VM_Experiment_TransparentBG.png "High level diagram of what I try to achieve")

We have CPU nodes, all of them authenticate to the same authentication server. All of them will mount same Fossil filesystem from Plan9n1. There will be an underlaying layer for replication, among Plan9n1 and Plan9n3, and an archiving service available on Plan9n4.

To run CPU services, the kernel needs to be recompiled to enable this feature. So all VM nodes will run the same kernel. As they are all accessing the same Fossil FS, all of them share interesting files (like /lib/ndb/local).

The point I am now, is that I have all 4 CPU servers running, the Auth server and the Fossil server in Plan9n1. In other words, still needs to configure the Fossil replica and the Venti server. But the rest is pretty much done. There are though more steps to do after this configuration is achieved, but that will be discussed later on. By now, this is all for this post.

Will continue in Plan9: Test Plan9 VMs (Part 3). There I will show my machines so far and will comment on some of the configuration details.
