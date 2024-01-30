---
title: Configuration Manager SEDO
ms.date: 09/20/2016
description: SEDO in SDK provides a mechanism for assigning and unassigning locks to globally replicated SDK provider objects in the context of a site, computer, and user.
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual
ms.assetid: fd4859e5-3443-47b0-9b07-b41063c8b2aa
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Configuration Manager SEDO
Configuration Manager SEDO (Serialized Editing of Distributed Objects) in the Configuration Manager SDK provides a mechanism for assigning and unassigning locks to globally replicated SDK provider objects in the context of a site, computer and user. SEDO-enabled objects are globally replicated SDK provider objects that require the user to obtain a lock if that user wishes to edit and save that object. When the user obtains that lock, the lock will be assigned to that user, the user's computer and the site in which the computer resides. While that lock is assigned, no other user or computer will be able to edit that object until the user releases the lock.  

 Only SEDO-enabled objects require users to obtain a lock before editing them. The SEDO-enabled objects are the following:  

-   SMS_Application  

-   SMS_AuthorizationList  

-   SMS_BootImagePackage  

-   SMS_ConfigurationBaselineInfo  

-   SMS_ConfigurationItem  

-   SMS_DeploymentType  

-   SMS_Driver  

-   SMS_DriverPackage  

-   SMS_GlobalCondition  

-   SMS_ImagePackage  

-   SMS_OperatingSystemInstallPackage  

-   SMS_Package  

-   SMS_SoftwareUpdatesPackage  

-   SMS_TaskSequencePackage  

## Implicit and Explicit Lock Requests  
 To prevent SEDO from breaking current SDK application functionalities, SEDO supports both implicit and explicit lock requests. In the case of implicit requests, if the lock is already assigned to the local site and the user attempts to edit a SEDO-enabled object, then SEDO will automatically attempt to retrieve the lock. If SEDO succeeds in obtaining the lock from the local site and the user edits the object, then that object will be saved at the user's request, without having to make an explicit programmatic lock request.  

 However, if the lock is not assigned to the local site and a transfer of the lock from another site must be requested, a request must be sent to the remote site that contains the lock. This request must be made explicitly by the user.  

 For more information, and to learn how to explicitly request a lock, see [How to Acquire a Lock on a SEDO-Enabled Object](../../../develop/core/understand/how-to-acquire-a-lock-on-a-sedo-enabled-object.md).  

## Implicit and Explicit Lock Releases  
 SEDO also supports both implicit and explicit lock releases. In the case of implicit releases, when a user saves an object using a `Put()` method, SEDO will attempt to automatically release the lock. Otherwise, the release must be explicitly made.  

 To learn how to explicitly and implicitly release a lock, see [How to Release a Lock on a SEDO-Enabled Object](../../../develop/core/understand/how-to-release-a-lock-on-a-sedo-enabled-object.md).  

## See also

- [How to Acquire a Lock on a SEDO-Enabled Object](../../../develop/core/understand/how-to-acquire-a-lock-on-a-sedo-enabled-object.md)  

- [How to Release a Lock on a SEDO-Enabled Object](../../../develop/core/understand/how-to-release-a-lock-on-a-sedo-enabled-object.md)  
