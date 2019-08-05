---
title: OS deployment interoperability
titleSuffix: Configuration Manager
description: Understand interoperability issues when different System Center Configuration Manager sites in a single hierarchy use different versions.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Plan for OS deployment interoperability

*Applies to: System Center Configuration Manager (Current Branch)*

When different System Center Configuration Manager sites in a single hierarchy use different versions, some Configuration Manager functionality isn't available. Typically, functionality from the newer version of Configuration Manager isn't accessible at sites or by clients that run a lower version. For more information, see [Interoperability between different versions of System Center Configuration Manager](/sccm/core/plan-design/hierarchy/interoperability-between-different-versions).  


## Objects

Consider the following objects when you upgrade the top-level site in your hierarchy and other sites in your hierarchy run Configuration Manager with a lower version:  

### Client installation package  

- The source for the default client installation package is automatically upgraded. All distribution points in the hierarchy are updated with the new client installation package. This behavior happens even on distribution points at sites in the hierarchy that are at a lower version.  

- You can't assign new version clients to sites that you haven't yet upgraded to the new version. Assignment is blocked at the management point.  

### Boot images  

- When you upgrade the top-level site to the latest version of Configuration Manager, it automatically updates the default boot images (x86 and x64). The update uses the Windows ADK for Windows 10, which includes Windows PE 10. The files that are associated with the default boot images are updated with the latest Configuration Manager version of the files. The site doesn't automatically update custom boot images. You need to manually update custom boot images, which include older Windows PE versions.  

- When your site hierarchy contains sites with different versions of Configuration Manager, avoid the use of dynamic media. Instead, use site-based media to contact a specific management point. After you update all sites to the same version of Configuration Manager, you can use dynamic media again.

- Verify that the latest Configuration Manager boot images include your customizations. Then update all distribution points at the new version sites with the latest version of the new boot images.  

### User State Migration Tool (USMT)  

When you upgrade the top-level site to the latest version of Configuration Manager, it automatically updates the default USMT package to the latest version. It doesn't automatically update any custom USMT packages. You need to manually update these packages.  

### New task sequence steps  

Periodically, new task sequence steps are introduced with new versions of Configuration Manager. When you deploy a task sequence with a new step to older clients, the task sequence step fails. Before you deploy a task sequence with a new step, make sure the clients in the target collection are updated to the new version.  

### OS deployment media  

When the site is updated to a new version, update all media with the new Configuration Manager client package. These media types include bootable, capture, prestaged, and stand-alone.

### Third-party extensions to OS deployment  

When you have third-party extensions to OS deployment and you have different versions of Configuration Manager sites or Configuration Manager clients, there might be issues with the extensions.  


## Latest version of Configuration Manager sites in a mixed hierarchy  

When you upgrade a site to latest version of Configuration Manager, task sequences that reference the default client installation package automatically start to deploy the latest Configuration Manager client version.

Task sequences that reference a custom client installation package continue to deploy the version of the client that's contained in that custom package. Custom packages likely include an earlier version of the Configuration Manager client. To avoid task sequence deployment failures, update any custom client installation packages to the latest version.

When you configure a task sequence to use a custom client installation package, do one of the following actions:

- Update the task sequence step to use the latest Configuration Manager version of the client installation package
- Update the custom package to use the latest Configuration Manager client installation source

> [!IMPORTANT]  
> Don't deploy a task sequence that references the latest Configuration Manager client installation package to clients in an older Configuration Manager site. When clients assigned to an older Configuration Manager site are upgraded to the latest Configuration Manager client version, Configuration Manager blocks the assignment to the older Configuration Manager site. These clients are no longer assigned to any site. Until you manually assign the client to the latest Configuration Manager site, or reinstall the older Configuration Manager version of the client on the computer, these clients are unmanaged.


## Older versions of Configuration Manager in a mixed hierarchy  

When you upgrade your central administration site to the latest version of Configuration Manager, make sure that OS deployment task sequences that you deploy don't leave those clients in an unmanaged state. For example, if you deploy to clients assigned to an older Configuration Manager site that you haven't yet upgraded to the latest version of Configuration Manager.

Make a copy of a task sequence that you use to deploy to clients in the latest version of Configuration Manager site. Then modify the task sequence so you can deploy it to clients in an older Configuration Manager site. Configure the task sequence to reference a custom client installation package that uses the older Configuration Manager client installation source. If you don't already have a custom client installation package that references the older Configuration Manager client installation source, manually create one.  

> [!Important]  
> Starting in version 1902, you can't deploy a package or task sequence to a client version 5.7730 or earlier. To work around this limitation, upgrade the client to a later version.<!-- SCCMDocs-pr issue #3493 -->
