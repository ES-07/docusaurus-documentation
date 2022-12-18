---
sidebar_label: 'Sites Management API'
---

# Backend Sites Management API

The information model of the Sites Management API was designed in this way:

![Information Model](../../../static/img/db.png)

It has 6 entities:
 * Person
 * Property Owner
 * Security Manager
 * Intrusion 
 * Buildings
 * Device


The relationship between them are:
* A Person can be a Property Owner or a Security Manager;
* A Propert Owner can have multiple Buildings (1:N);
* A Building has multiple devices (1:N);
* A Intrusion is only recognized if a device is triggered (1:1).
