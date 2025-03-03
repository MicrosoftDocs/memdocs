---
title: Object Security
description: The delegate verb in Configuration Manager provides administrators with a way of allowing users to assign to other users the instance permissions to an object in a very limited way.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: article
ms.assetid: 9df97bf6-6255-4348-a522-22e50af490b0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Configuration Manager Object Security

## Delegate Verb  
 The delegate verb in Configuration Manager provides administrators with a way of allowing users to assign to other users the instance permissions to an object in a very limited way. The rights that a user is allowed to assign (or revoke) to other users are limited to the instance rights that have been explicitly granted to that user. When a user creates a secured object, that user is automatically granted explicit instance rights to that object (usually read, modify, and delete).  

 To some extent, these explicitly granted rights provide the user with a certain level of ownership of the object. With the delegate right, this ownership is extended to the control of the default group of instance rights. To limit which rights a user can delegate, only rights explicitly granted to them (not a group to which they belong) can be delegated. A user can also remove other users (or groups) instance rights if the user has the delegate permission and explicit rights to an object (this is why a user is said to own an object if they have explicit instance rights). Users with administrator rights still have full control of administering permissions.  

 A common scenario for using the delegate verb is when a user has created and delegated rights for an object type and wants to create an object and allow members of a user group to see it. They create an instance of the object and then delegate read permissions for the instance to the user group.  

 The delegate verb is applicable to the following Configuration Manager classes:  

-   `SMS_Collection`  

-   `SMS_Package`  

-   `SMS_Advertisement`  

-   `SMS_Site`  

-   `SMS_Query`  

-   `SMS_Report`  

-   `SMS_MeteredProductRule`  

## System Resource (SMS_R_System) as a Secured Resource  
 Secured resources are resources (the SMS_R_* classes) that require collection read rights to be viewed. If the user has class-level collection read rights, the user can see all the instances of a secured resource. If the user only has instance-level read rights to certain collections, the user only has rights to see resources that are members of those collections. `SMS_R_User` and `SMS_R_UserGroup` are secured resources in SMS 2.0. In SMS 2003, `SMS_R_System` (the system resource) is also a secured resource.  

 Inventory instances (SMS_G_System_*) are secured similarly with the read resource verb. If a user has class-level rights, that user can see inventory data belonging to all resources. If the user doesn't have class-level rights, the user can see only inventory data for inventory that belongs to resources that are members of collections to which the user has instance-level read resource rights. Conversely, if a user has read resource rights to a collection, a user can see the inventory data for the members of that collection. This hasn't been affected by the change in security to `SMS_R_System`. Read resource rights can't be granted to a user without granting read rights. When a user doesn't have the appropriate class-level collection rights, resource security is enforced through collection limiting.  

## Securing File Submissions to a Configuration Manager Server  
 The recommended location for copying data discovery record (DDR) files and Managed Information Format (MIF) files that not related to existing Configuration Manager clients is directly in the site server inboxes. This requires administrator level permissions on the site server to be granted to the application that is  copying these files. These are located as follows:  

 DDR files: \<SMS>/inboxes/ddm.box  

 MIF files: \<SMS>/inboxes/inventry.box  

## See Also  
 [Objects overview](configuration-manager-objects-overview.md)
 [Configuration Manager Association Classes](../../../develop/core/understand/association-classes.md)   
 [Configuration Manager Bit Field Properties](../../../develop/core/understand/configuration-manager-bit-field-properties.md)   
 [Configuration Manager Date and Time Formats](../../../develop/core/understand/date-and-time-formats.md)   
 [Configuration Manager Embedded Objects](../../../develop/core/understand/embedded-objects.md)   
 [Configuration Manager Extended WMI Query Language](../../../develop/core/understand/extended-wmi-query-language.md)   
 [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md)   
 [Configuration Manager Special Queries](../../../develop/core/understand/special-queries.md)   
 [About errors](about-configuration-manager-errors.md)
