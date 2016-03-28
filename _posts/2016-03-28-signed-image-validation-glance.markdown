---
layout: post
title:  "Glance Signed Image Validation"
date:   2016-03-26
categories: security
tags: glance signed-image on-boot openstack
author: "sicarie @ Hewlett Packard Enterprise"
---

## Glance Signed Image Validation

A new addition to the OpenStack Security Guide is 
[Signed Image Validation](http://docs.openstack.org/security-guide/instance-management/security-services-for-instances.html)
in the Glance service. This will now allow boot-time assurance that an
image has not been tampered with before it is booted. The steps for doing
this are

1. A signature of the image is created
2. A Keystone service context is created
3. The image signature is encoded and uploaded to Castellan
4. The image is uploaded to the Glance service
5. The `verify_glance_signatures` is set to `True` in the 
   `/etc/nova/nova.conf` file

A detailed list of the specific actions for each step is located at
[Adding Signed Images to Glance](http://docs.openstack.org/openstack-ops/content/user_facing_images.html#add_signed_images).

Once the configuration details above have been taken, when an image with
a signature hash in its metadata is referenced as the boot image, the
Nova service will securely copy the image from Glance, and compare a
hash of the copied image against the signature in from the metadata. If
this hash matches the image will boot, giving the user assurance it
has not been tampered with.
