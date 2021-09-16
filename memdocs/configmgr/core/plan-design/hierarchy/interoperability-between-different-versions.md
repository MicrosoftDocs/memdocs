---
title: Interoperability between versions
titleSuffix: Configuration Manager
description: Learn how to avoid conflicts between multiple Configuration Manager hierarchies on the same network.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Interoperability between different versions of Configuration Manager

*Applies to: Configuration Manager (current branch)*

You can install and operate multiple, independent hierarchies of Configuration Manager on the same network. However, because different hierarchies of Configuration Manager don't interoperate outside of the migration process, each hierarchy requires configurations to prevent conflicts between them. Additionally, you can create certain configurations to help resources that you manage interact with the site systems from the correct hierarchy.  

## Current branch and earlier versions

Sites of different versions can't coexist in the same Configuration Manager hierarchy. The only exceptions are during the process of the following upgrade scenarios:

- From System Center 2012 Configuration Manager to Configuration Manager current branch
- From one Configuration Manager current branch version to a newer version using in-console updates

You can deploy a Configuration Manager current branch site and hierarchy side by side with an existing System Center 2012 Configuration Manager site or hierarchy. Plan to prevent clients from either version from trying to join a site from the other version.

For example, if two or more Configuration Manager hierarchies have [overlapping boundaries](../../servers/deploy/configure/define-site-boundaries-and-boundary-groups.md#overlapping-boundaries) that include the same network locations, assign each new client to a specific site instead of using automatic site assignment. For more information, see [How to assign clients to a site](../../clients/deploy/assign-clients-to-a-site.md).  

Additionally, you can't install a client from System Center 2012 Configuration Manager on a computer that hosts a site system role from Configuration Manager current branch. You also can't you install a Configuration Manager current branch client on a computer that hosts a site system role from System Center 2012 Configuration Manager.  

The following clients and connections aren't supported:  

- Any System Center 2012 Configuration Manager or earlier computer client version  

- Any System Center 2012 Configuration Manager or earlier device management client  

- Windows CE Platform Builder device management client (any version)  

- System Center Mobile Device Manager VPN connection  

### Client site assignment considerations

Configuration Manager clients can be assigned to only a single primary site. You can't predict the actual site assignment of a client when all of the following conditions are true:

- You use automatic site assignment to assign clients to a site during client installation
- More than one boundary group includes the same boundary
- The boundary groups have different assigned sites

If boundaries overlap across multiple Configuration Manager sites and hierarchies, clients might not be assigned to the site you expect, or might not get assigned to a site at all.  

Configuration Manager current branch clients check the version of the site before they complete site assignment. If site boundaries overlap, you can't assign clients to a site with a previous version. However, earlier System Center 2012 Configuration Manager clients might incorrectly be assigned to a later Configuration Manager current branch site.  

To prevent clients from unintentionally being assigned to the wrong site when two hierarchies have overlapping boundaries, configure client installation parameters to assign clients to a specific site.  

## Limitations in a mixed-version hierarchy

When you upgrade a Configuration Manager current branch hierarchy, there are times when different sites will have different versions. For example, first you upgrade the central administration site. Because of site maintenance windows, you don't upgrade the primary sites until a later time and date.  

When different sites in a single hierarchy run different versions, some functionality isn't available. This behavior can affect how you manage Configuration Manager objects in the Configuration Manager console, and which functionality is available to clients. Typically, functionality from the newer version of Configuration Manager isn't accessible at sites or to clients that run a lower service pack version.  

### Network access account

You upgrade the central administration site to Configuration Manager current branch. You view the network access account details from a Configuration Manager console that's connected to this updated site. It doesn't display account details from sites that still run System Center 2012 Configuration Manager.

After you upgrade the primary site to the same version as the central administration site, the account details are visible in the console.

The same behavior applies when you update between versions of Configuration Manager.

### Boot images for OS deployment

#### When upgrading from System Center 2012 Configuration Manager to Configuration Manager current branch

When the top-level site of a hierarchy upgrades to Configuration Manager current branch, it automatically updates the default boot images to use the Windows Assessment and Deployment Kit (ADK) version 10. Use these boot images only for deployments to clients at Configuration Manager current branch sites. For more information, see [Planning for OS deployment interoperability](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).

#### When upgrading between Configuration Manager current branch versions

As long as new versions of Configuration Manager don't update the version of Windows ADK that's in use, there's no effect on boot images.

### New task sequence steps

When you create a task sequence with a step introduced in one version of Configuration Manager that's not available in an earlier version, you might have the following issues:

- An error occurs when you try to edit the task sequence from a site that's running a previous version of Configuration Manager.

- The task sequence doesn't run on a computer that runs a previous version of the Configuration Manager client.

### Client to down-level management point communications

A Configuration Manager client that communicates with a management point from a site that runs a lower version than the client can only use functionality that the down-level version of Configuration Manager supports. For example, if you deploy content from a Configuration Manager current branch site that was recently upgraded to a client that communicates with a management point that hasn't yet upgraded to that version, that client can't use new functionality from the latest version.

### Package and task sequence deployments to legacy clients

<!-- SCCMDocs-pr issue #3493 -->

You can't deploy a package or task sequence to a client version 5.7730 or earlier. To work around this limitation, upgrade the client to a later version.

### Orchestration groups

Orchestration groups can't be used in a mixed-version hierarchy. <!--SCCMDocs-pr issue ##5056, 6389000-->

### Assign site systems as clients to the same site

<!-- 9606023 -->
If you install the Configuration Manager client on site systems, assign them to the same site. Roles like the management point and distribution point have shared binary files between the role and the client. These collocated clients should always be the same version as the site system role.

For example, for a management point in site XYZ, assign the client installed on this site system server to site XYZ.

## Configuration Manager console  

This section contains information about the use of the Configuration Manager console in an environment that has a mix of Configuration Manager versions.  

### An environment with both System Center 2012 Configuration Manager and Configuration Manager current branch

To manage a Configuration Manager site, both the console and the site the console connects to must run the same version of Configuration Manager. For example, you can't use a System Center 2012 Configuration Manager console to manage a Configuration Manager current branch site, or the other way around.

It's not supported to install both the System Center 2012 Configuration Manager console and the Configuration Manager current branch console on the same computer.

### An environment with multiple versions of Configuration Manager

Configuration Manager current branch doesn't support installing more than a single Configuration Manager console on a computer. To use multiple consoles that are specific to different versions of Configuration Manager, install the different consoles on separate computers.

During the process of updating sites in a hierarchy to a new version, you can connect a console to a site that runs a newer version and view information about other sites in that hierarchy. However, this configuration isn't recommended. It's possible that differences between the console version and Configuration Manager site version can result in data issues. Some features that are available in the latest product version won't be available in the console.

It's not supported to manage a site when using a console with a version that doesn't match the site version. Doing so might cause loss of data and can put your site at risk. For example, it's not supported to use a console from version 2103 to manage a site that runs version 2010.

## Next steps

[Use the Configuration Manager client software for extended interoperability with future versions of a Current Branch site](../../understand/interoperability-client.md)
