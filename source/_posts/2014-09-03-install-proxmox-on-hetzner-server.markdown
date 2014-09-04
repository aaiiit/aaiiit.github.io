---
layout: post
title: "Install Proxmox on Hetzner server"
date: 2014-09-03 13:10:15 +0200
comments: true
categories: 
---

* Boot in rescue mode
* Set root passwd
* Install image

  {% highlight bash %}
  installimage
  {% endhighlight %}

* Configure partitions

  Use LVM so that we can take snapshots and live dumps.

  {% highlight bash %}
Filesystem                Size  Used Avail Use% Mounted on
udev                       10M     0   10M   0% /dev
tmpfs                     1.2G  340K  1.2G   1% /run
/dev/mapper/vg0-root       50G  3.0G   44G   7% /
tmpfs                     5.0M     0  5.0M   0% /run/lock
tmpfs                     3.6G  3.1M  3.6G   1% /run/shm
/dev/md0                  496M   40M  430M   9% /boot
/dev/mapper/vg0-tmp       5.0G   33M  5.0G   1% /tmp
/dev/mapper/vg0-home       20G   33M   20G   1% /home
/dev/mapper/vg0-backup     75G   33M   75G   1% /backup
/dev/mapper/vg0-vservers  500G  1.2G  499G   1% /vservers

  {% endhighlight %}

* Reboot
* Install suwappu::base

  {% highlight bash %}
  knife bootstrap <hw-node> -r 'suwappu::base'
  {% endhighlight %}

* Add ssh-key to root and user
* Install sudo and configure for user
* Login to https://hw-node:8006
* Add storage

  Datacenter -> Storage add /vservers
    - backup
    - disk image
    - container

* Put in some containers
