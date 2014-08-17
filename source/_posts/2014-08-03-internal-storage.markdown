---
layout: post
title: "Internal Storage"
date: 2014-08-03 13:59:13 +0200
comments: true
categories: 
---

Storage server
--------------

Using a Raspberry PI model B with external hdd's as a NAS.
Device is identified as 'storage' on the network.
HDD's are mounted in /mnt.  Right now only data-1 is mounted.
Clients use /data-1 as mountpoint.

# NFS mounts
storage:/mnt/data-1	/data-1	nfs	defaults	0	0


TODO
----

  * Setup rights so that clients can write to it
  * Create bootscript so that all necessary services are started

      After booting storage NFS can not be started because rpcbind
      is not started.  First start rpcbind then nfs-common and nfs-kernel
