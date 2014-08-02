---
layout: post
title:  "OpenVZ container TUN/TAP"
date:   2014-06-01
categories: server openvz
---

While trying to use an OpenVZ container as an OpenVPN client, 
it seemed the container could not create the TUN device.

See
[https://openvz.org/VPN_via_the_TUN/TAP_device](https://openvz.org/VPN_via_the_TUN/TAP_device)

OpenVZ containers have no TUN/TAP device.
It is possible to grant the container access to tun/tap by doing :

{% highlight bash %}
  CTID=101
  vzctl set $CTID --devnodes net/tun:rw --save
  vzctl set $CTID --devices c:10:200:rw --save
  vzctl set $CTID --capability net_admin:on --save
  vzctl exec $CTID mkdir -p /dev/net
  vzctl exec $CTID mknod /dev/net/tun c 10 200
  vzctl exec $CTID chmod 600 /dev/net/tun
{% endhighlight %}
