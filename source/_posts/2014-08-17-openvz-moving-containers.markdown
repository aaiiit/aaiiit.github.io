---
layout: post
title: "OpenVZ moving containers"
date: 2014-08-17 13:59:13 +0200
comments: true
categories: 
---

OpenVZ moving containers
------------------------

When moving OpenVZ containers on the hdd to another location you have to do some other changes to :

  - Edit /etc/vz/conf/<ctid>.conf and change private path to new location
  - Drop vzquota on container
      vzquota drop <ctid>

  Then you probably should reinitialize quota and turn it back on again,
  but that's for another time.  Need to look into it.
