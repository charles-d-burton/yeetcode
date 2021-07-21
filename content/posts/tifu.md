---
title: "Tifu"
date: 2021-07-20T21:10:43-06:00
draft: false
---

Today I fucked up.  I tried to crash an entire satellite constellation.  It was a simple mistake really
I was messing around with some our stupid system to deploy changes.  We had a really old system based on a dead version of Unix and our configuration management was some ancient version of RCS.  I'm pretty sure that nobody had used it in ages or made changes of any kind because what happened was me being a new hotshit member of the team.  I thought it would be helpful to add the ability for every machine on our network to have the ability to use `bash` instead of only `tcsh` and `csh`.  I made a change to the `/etc/shells` file in the RCS repo and distributed it.  Little did I know that the telemetry input boxes were reading from that file to get their shell and their bootcode.  It turns out that they needed a specific shell defined so that they could boot correctly.  When I distributed the files it overwrote the file on the servers that the telemetry boxes were connected to.  Now, this didn't have an immediate effect.  These machines were ancient and would occasionally reboot.  So when the rebooted they just wouldn't come back up.  Eventually we were down to a single telemetry machine before we figured out what had happened.  Corrected the file and suddenly everything came back online.

