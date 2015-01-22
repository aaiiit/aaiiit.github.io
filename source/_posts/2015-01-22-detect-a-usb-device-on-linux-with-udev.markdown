---
layout: post
title: "Detect a USB device on linux with udev"
date: 2015-01-22 17:02:34 +0100
comments: true
categories: 
---

I needed a way to start an application when a device is
connected to the RPi.  In this example the barcodescanner
software should start when we connect the scanner.
Adding a udev rule should do the trick.


  * First get the ID of the specific device

    {% highlight bash %}
    lsusb

    Bus 001 Device 006: ID 05f9:2214 PSC Scanning, Inc. 
    Bus 001 Device 004: ID 0a5f:0015 Zebra
    {% endhighlight %}

  * Add the rules file located in /etc/udev/rules.d/,
    for instance /etc/udev/rules.d/85-custom_usb_device_rules.rules

  * Add the rule to detect scanner and start software, the idVendor 
  and idProduct point to the ID we got from lsusb
    {% highlight bash %}
    ACTION=="add",SUBSYSTEM=="usb",ATTR{idVendor}=="05f9",
    ATTR{idProduct}=="2214",RUN+="/etc/init.d/barcodescanner start"
    {% endhighlight %}

  * Reload the rules or reboot
    {% highlight bash %}
    udevadm control --reload-rules
    {% endhighlight %}

