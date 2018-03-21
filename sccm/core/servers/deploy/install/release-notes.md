---
title: Release notes
titleSuffix: Configuration Manager
description: Learn about urgent issues that are not yet fixed in the product or covered in a Microsoft Knowledge Base article.
ms.custom: na
ms.date: 03/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Release notes for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

With Configuration Manager, product release notes are limited to urgent issues. These issues aren't yet fixed in the product, or detailed in a Microsoft Knowledge Base article.  

Feature-specific documentation includes information about known issues that affect core scenarios.  

> [!TIP]  
>  This topic contains release notes for the current branch of Configuration Manager. For information on the technical preview branch, see [Technical Preview for System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

For information about the new features introduced with different versions, see the following articles:
- [What's new in version 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)
- [What's new in version 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [What's new in version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  



## Setup and upgrade  


### When using redistributable files from the CD.Latest folder, setup fails with a manifest verification error
<!-- 510080, 490569  -->

When you run setup from the CD.Latest folder created for version 1606, and use the redistributable files included with that CD.Latest folder, setup fails with the following errors in the Configuration Manager Setup log:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

#### Workaround
Use one of the following options:
 - During Setup, choose to download the most current redistributable files from Microsoft. Use the latest redistributable files instead of the files included in the CD.Latest folder.
 - Manually delete the *cd.latest\redist\languagepack\zhh* folder, and then run Setup again.


### Setup command-line option JoinCEIP must be specified
<!--510806-->
*Applies to: Configuration Manager version 1802*

Starting in Configuration Manager version 1802, the Customer Experience Improvement Program (CEIP) feature is removed from the product. When [automating installation](/sccm/core/servers/deploy/install/command-line-options-for-setup) of a new site from a command-line or unattended script, setup returns an error that a required parameter is missing. 

#### Workaround
While it has no affect on the outcome of the setup process, include the **JoinCEIP** parameter in your setup command line.

 > [!Note]  
 > The EnableSQM parameter for [console setup](/sccm/core/servers/deploy/install/install-consoles) is not required.



<!-- ## Backup and recovery  -->


## Client deployment and upgrade

### Azure AD-enabled clients can't communicate with management point
<!--501089-->
*Applies to: Configuration Manager version 1706*
<!--also fixed in 1710 HFRU-->
In the scenario to [install and assign Configuration Manager Windows 10 clients using Azure AD for authentication](/sccm/core/clients/deploy/deploy-clients-cmg-azure), client communication fails when the HTTPS-enabled management point uses alternate database credentials. 

#### Workaround
Mitigate this issue with one of the following actions:
- Update the site to the latest version, and apply the latest hotfix
- Change the credentials that the management point uses.


<!-- ## Operating system deployment  -->



## Software updates

### Servicing plans create many duplicate software update groups and deployments by default  
<!-- 474326 -->
By default, the Create Servicing Plan wizard currently runs after every software updates synchronization. Each time the wizard runs, it creates a new software update group and deployment. If you have a software updates synchronization schedule that runs several times a day, the Create Servicing Plan wizard creates multiple software update groups and deployments each day.  

#### Workaround
 After you create a serving plan, open the properties for the servicing plan, go to the **Evaluation Schedule** tab,  select **Run the rule on a schedule**, click **Customize**, and create a custom schedule. For example, you can have the servicing plan run every 60 days.  



## Mobile device management  

### You can no longer deploy Windows Phone 8.1 VPN profiles to Windows 10
<!-- 503274  -->
*Applies to: Configuration Manager version 1710*

You can't create a VPN profile, using the Windows Phone 8.1 workflow, which is also applicable to Windows 10 devices. For these profiles, the creation wizard no longer shows the Supported Platforms page. Windows Phone 8.1 is automatically selected on the back-end. The Supported Platforms page is available in the profile properties, but it doesn't display the Windows 10 options.

#### Workaround
 Use the Windows 10 VPN profile workflow for Windows 10 devices. If this option isn't feasible for your environment, contact support. Support can help you add the Windows 10 targeting.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
