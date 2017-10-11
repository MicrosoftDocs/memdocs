---
title: "Object Security"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 9df97bf6-6255-4348-a522-22e50af490b0searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager Object Security
Although only the [SMS_UserInstancePermissions Server WMI Class](../../../develop/reference/misc/sms_userinstancepermissions-server-wmi-class.md) is commonly used in System Center Configuration Manager scripting, you can also use the following Configuration Manager classes for Configuration Manager object security:  

-   `SMS_UserInstancePermissions Server WMI Class` Each instance of this class represents all the rights for a particular user or group for that instance.  

-   [SMS_UserInstancePermissionNames Server WMI Class](../../../develop/reference/misc/sms_userinstancepermissionnames-server-wmi-class.md) Each instance of this class represents a particular right for a particular user or group on a particular instance. This class is useful for display purposes because the rights are already parsed into a form that you can read, but it takes more scripting to achieve the same results as the `SMS_UserInstancePermissions Server WMI Class`.  

-   [SMS_UserClassPermissions Server WMI Class](../../../develop/reference/misc/sms_userclasspermissions-server-wmi-class.md) Each instance of this class represents all the rights for a particular user or group for a particular class.  

-   [SMS_UserClassPermissionNames Server WMI Class](../../../develop/reference/misc/sms_userclasspermissionnames-server-wmi-class.md) Each instance of this class represents a particular right for a particular user or group for a particular class. The class is useful for display purposes because the rights are already parsed into a form that you can read, but it takes more scripting to achieve the same results as the `SMS_UserClassPermissions Server WMI Class`.  

## Delegate Verb  
 The delegate verb in Configuration Manager provides administrators with a way of allowing users to assign to other users the instance permissions to an object in a very limited way. The rights that a user is allowed to assign (or revoke) to other users are limited to the instance rights that have been explicitly granted to that user. When a user creates a secured object, that user is automatically granted explicit instance rights to that object (usually read, modify, and delete).  

 To some extent, these explicitly granted rights provide the user with a certain level of ownership of the object. With the delegate right, this ownership is extended to the control of the default group of instance rights. To limit which rights a user can delegate, only rights explicitly granted to them (not a group to which they belong) can be delegated. A user can also remove other users (or groups) instance rights if the user has the delegate permission and explicit rights to an object (this is why a user is said to own an object if they have explicit instance rights). Users with administrator rights still have full control of administering permissions.  

 A common scenario for using the delegate verb is when a user has create and delegate rights for an object type and wants to create an object and allow members of a user group to see it. They create an instance of the object and then delegate read permissions for the instance to the user group.  

 The delegate verb is applicable to the follow Configuration Manager classes:  

-   `SMS_Collection`  

-   `SMS_Package`  

-   `SMS_Advertisement`  

-   `SMS_Site`  

-   `SMS_Query`  

-   `SMS_Report`  

-   `SMS_MeteredProductRule`  

## System Resource (SMS_R_System) as a Secured Resource  
 Secured resources are resources (the SMS_R_* classes) that require collection read rights to be viewed. If the user has class-level collection read rights, the user can see all the instances of a secured resource. If the user only has instance-level read rights to certain collections, the user only has rights to see resources that are a members of those collections. `SMS_R_User` and `SMS_R_UserGroup` are secured resources in SMS 2.0. In SMS 2003, `SMS_R_System` (the system resource) is also a secured resource.  

 Inventory instances (SMS_G_System_*) are secured similarly with the read resource verb. If a user has class-level rights, that user can see inventory data belonging to all resources. If the user does not have class-level rights, the user can see only inventory data for inventory that belongs to resources that are members of collections to which the user has instance-level read resource rights. Conversely, if a user has read resource rights to a collection, a user can see the inventory data for the members of that collection. This has not been affected by the change in security to `SMS_R_System`. Read resource rights cannot be granted to a user without granting read rights. When a user does not have the appropriate class-level collection rights, resource security is enforced through collection limiting.  

## Securing File Submissions to a Configuration Manager Server  
 The recommended location for copying data discovery record (DDR) files and Managed Information Format (MIF) files that not related to existing Configuration Manager clients is directly in the site server inboxes. This requires administrator level permissions on the site server to be granted to the application that is  copying these files. These are located as follows:  

 DDR files: \<SMS>/inboxes/ddm.box  

 MIF files: \<SMS>/inboxes/inventry.box  

## See Also  
 [About Configuration Manager Objects](../../../develop/core/understand/about-configuration-manager-objects.md)   
 [Configuration Manager Association Classes](../../../develop/core/understand/association-classes.md)   
 [Configuration Manager Bit Field Properties](../../../develop/core/understand/configuration-manager-bit-field-properties.md)   
 [Configuration Manager Date and Time Formats](../../../develop/core/understand/date-and-time-formats.md)   
 [Configuration Manager Embedded Objects](../../../develop/core/understand/embedded-objects.md)   
 [Configuration Manager Extended WMI Query Language](../../../develop/core/understand/extended-wmi-query-language.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)   
 [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md)   
 [Configuration Manager Special Queries](../../../develop/core/understand/special-queries.md)   
 [Configuration Manager Errors](../../../develop/core/understand/configuration-manager-errors.md)
