---
title: Planning for operating system deployment interoperability
titleSuffix: "Configuration Manager"
description: "Understand interoperability issues when different System Center Configuration Manager sites in a single hierarchy use different versions."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Planning for operating system deployment interoperability in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

When different System Center Configuration Manager sites in a single hierarchy use different versions, some Configuration Manager functionality is not available. Typically, functionality from the newer version of Configuration Manager is not accessible at sites or by clients that run a lower version. For more information, see [Interoperability between different versions of System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

 Consider the following when you upgrade the top-level site in your hierarchy and other sites in your hierarchy run Configuration Manager with a lower version:  

-   Client installation package  

    -   The source for the default client installation package is automatically upgraded and all distribution points in the hierarchy are updated with the new client installation package, even on distribution points at sites in the hierarchy that are at a lower version.  

    -   Clients that run the new version cannot be assigned to sites that have not yet been upgraded to the new version. Assignment is blocked at the management point.  

-   Boot images  

    -   When you upgrade the top-level site to the latest version of Configuration Manager, the default boot images (x86 and x64) are automatically updated to Windows ADK for Windows 10-based boot images, which use Windows PE 10. The files that are associated with the default boot images are updated with the latest Configuration Manager version of the files. Custom boot images are not updated automatically. You will need to update custom boot images manually, which includes older Windows PE versions.  

    -   Avoid the use of dynamic media when your site hierarchy contains sites with different versions of Configuration Manager. Instead, use site-based media to contact a specific management point until all sites are upgraded to the same version of Configuration Manager.  

    -   Verify that the latest Configuration Manager boot images contain the desired customization, and then update all distribution points at the sites with the latest version of  Configuration Manager with the new boot images.  

-   User State Migration Tool (USMT)  

    -   When you upgrade the top-level site to the latest version of Configuration Manager, the default USMT package is automatically updated to the latest version. Custom USMT packages are not updated automatically. You will need to manually update these packages.  

-   New task sequence steps  

    -   Periodically, new task sequence steps are introduced with new versions of Configuration Manager. When you deploy a task sequence with a new step to older clients, the task sequence step will fail. Before you deploy a task sequence with a new step, make sure the clients in the target collection are updated to the new version.  

-   Operating system deployment media  

    -   All media (bootable, capture, prestaged, and stand-alone) must be updated with the new Configuration Manager client package when the site is updated to a new version.  

-   Third-party extensions to operating system deployment  

    -   When you have third-party extensions to operating system deployment and you have different versions of Configuration Manager sites or Configuration Manager clients, a mixed hierarchy, there might be issues with the extensions.  

 While you are actively upgrading sites in your hierarchy, use the following sections to help you with operating system deployments.  

## Latest version of Configuration Manager sites in a mixed hierarchy  
 When you upgrade a site to latest version of Configuration Manager, task sequences that reference the default client installation package will automatically start to deploy the latest Configuration Manager client version. Task sequences that reference a custom client installation package will continue to deploy the version of the client that is contained in that custom package (likely a previous Configuration Manager client version), and must be updated to avoid task sequence deployment failures. When you have a task sequence that is configured to use a custom client installation package, you must update the task sequence step to use the latest Configuration Manager version of the client installation package or update the custom package to use the latest Configuration Manager client installation source.  

> [!IMPORTANT]  
>  Do not deploy a task sequence that references the latest Configuration Manager client installation package to clients in an older Configuration Manager site. When clients assigned to an older Configuration Manager site are upgraded to the latest Configuration Manager client version, Configuration Manager blocks the assignment to the older Configuration Manager site. Therefore, the client is no longer assigned to any site and will be unmanaged until you manually assign the client to latest Configuration Manager site or reinstall the older Configuration Manager version of the client on the computer.  

## Older versions of Configuration Manager in a Mixed Hierarchy  
 When you have upgraded your central administration site to the latest version of Configuration Manager, you must take the following step to ensure that operating system deployment task sequences that you deploy to clients assigned to an older  Configuration Manager site (not yet upgraded to the latest version of Configuration Manager) do not leave those clients in an unmanaged state.  

-   Create a task sequence that you will use to deploy to clients only in a Configuration Manager site. Likely, you will make a copy of a task sequence that you use to deploy to clients in the latest version of Configuration Manager site and then modify the task sequence so you can deploy it to clients in an older Configuration Manager site. Then, configure the task sequence to reference a custom client installation package that uses the older Configuration Manager client installation source. If you do not already have a custom client installation package that references the older Configuration Manager client installation source then you must manually create one.  
