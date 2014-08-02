---
layout: post
title:  "OpenVZ problem : Quota on syscall"
date:   2014-05-30
categories: openvz problem quota
---


From :
[http://serverguru.blogspot.be/2009/09/vzquota-error-quota-on-syscall-for-id.html](http://serverguru.blogspot.be/2009/09/vzquota-error-quota-on-syscall-for-id.html)

Reason: The vzquota of that particular vps still running in the server. So you
have to drop the quota before applying the new changes.

remove /var/vzquota/quota. and drop the particular quota

 * rm /var/vzquota/quota.110
 * vzquota drop 110
 * vzctl start 110

