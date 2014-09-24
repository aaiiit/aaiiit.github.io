---
layout: post
title: "Adding a VPN client to Suwappu Network"
date: 2014-09-24 13:51:31 +0200
comments: true
categories: 
---

To add an OpenVPN client to the Suwappu network, you need to do the following :

  * Login to openvpn.suwappu.net
  * cd /etc/openvpn/easy-rsa
  * source ./vars
  * /etc/openvpn/easy-rsa/suwappu_host_keys <client-name>
  * Logout OpenVPN server
  * cp /var/lib/vz/private/1003/tmp/<client-name>.tar.gz /vservers/containers/private/1012/home/tom/
  * knife bootstrap <client-name> -r 'suwappu::openvpn-client'
