---
title: "Install a site using the 1606 baseline media  | System Center Configuration Manager"
description: "Learn about using the 1606 baseline media to install or upgrade sites for System Center Configuration Manager."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid:  f4f9a5fd-f573-4b99-ad93-b2c76812e922
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Install and upgrade with the version 1606 baseline media for System Center Configuration Manager


Use this topic to learn about running Configuration Manager Setup when you use the version 1606 baseline media from Microsoft System Center 2016. You can use this media to install a new site, or upgrade from System Center 2012 Configuration Manager with Service Pack 2 or System Center 2012 R2 Configuration Manager with Service Pack 1. During Setup, you can choose to install the Current Branch or Long-Term Servicing Branch (LTSB).

When you use the version 1606 baseline media, the site you install (or upgrade to) is:
- **A Current Branch site** that is equivalent to a site that was first installed using the 1511 baseline media, and then updated to version 1606 plus the 1606 hotfix rollup - KB3186654.
-	**A LTSB site** that is equivalent to the Current Branch site that runs version 1606 plus the 1606 hotfix rollup - KB3186654 (the baseline media already includes the hotfix rollup).  However, the LTSB does not support all of the features or capabilities available with the Current Branch, as detailed in [Introduction to the Long-Term Servicing Branch of System Center Configuration Manager](introduction-to-the-ltsb.md).

If you are not familiar with the different branches of System Center Configuration Manager, see [Which branch of Configuration Manager should I use](which-branch-should-i-use.md).


## Changes to Setup with the 1606 baseline media
The 1606 baseline media introduces the following changes to Setup for Configuration Manager.

### Branch and edition
When you run Setup, you are now presented with a Licensing page where you can select the branch of Configuration Manager you want to install. You can choose either the Current Branch or LTSB as a licensed install, or you can choose an Evaluation edition of the Current Branch as a non-licensed install.

For more information see [Licensing and branches for System Center Configuration Manager](learn-more-editions.md).

## Software Assurance expiration
During Setup, you have the option to enter the **Software Assurance expiration date**. This is an optional value you can specify as a convenient reminder.

> ![NOTE]
> Microsoft does not validate the expiration date you entered and will not use this date for license validation.  Instead, you can use it as a reminder of your expiration date. This is useful because Configuration Manager periodically checks for new software updates offered online and your software assurance license status should be current to be eligible to use these additional updates.    

- You can specify the value on the **Product Key** page of the Setup Wizard when you run Setup from the System Center Configuration Manager version 1606 baseline media
- You can also specify this date on the **Licensing** tab of the **Hierarchy Settings Properties** in the Configuration Manager console

For more information see *Software Assurance agreements* in [Licensing and branches for System Center Configuration Manager](learn-more-editions.md).

### In-place upgrade paths for the 1606 baseline media
You can use the 1606 baseline media to upgrade the following to a licensed edition of System Center Configuration Manager:
- System Center 2012 Configuration Manager with Service Pack 2
- System Center 2012 R2 Configuration Manager with Service Pack 1

You can also use this media to upgrade a non-licensed Evaluation edition of Current Branch to a fully licensed version of the Current Branch.

This media does not support upgrade of:
- Other versions of System Center 2012 Configuration Manager
- Configuration Manager 2007 or earlier
- A release candidate install of System Center Configuration Manager

### Additional pre-upgrade configurations
Prior to starting an upgrade of System Center 2012 Configuration Manager to the LTSB, you must take the following additional steps as part of pre-upgrade checklist.  
Uninstall the site system roles not supported by the LTSB:
- Asset Intelligence synchronization point
- Microsoft Intune connector
- Cloud-based distribution points

For more information, see [Upgrade to System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).


### New scripted install options
The version 1606 baseline media supports a new unattended script file key for scripted installs of a new top-level site. This applies to installing a new stand-alone primary site or adding a central administration site as part of a site expansion scenario.

When using an unattended script to install a licensed branch, you must add the following section, key names, and values to the Options section of your script (you do not need to use these values to script the install of an Evaluation edition of the Current Branch):  

 **SABranchOptions**
- 	**Key Name: SSActive**
  - Values: 0 or 1  
  - Details:  0 installs a non-licensed Evaluation edition of Current Branch, and 1 installs a licensed edition.   

- **CurrentBranch**
  - Values: 0 or 1  
  - Details:  0 installs the Current Branch, and 1 installs the Long-Term Servicing Branch.  

For example, to install a licensed Current Branch edition you would use:

  **Key Name: SABranchOptions**
   -	**SSActive = 1**
   - **CurrentBranch = 0**

Important:
SABranchOptions  only works with Setup from the baseline media. It does not apply when you run Setup from the CD.Latest folder of a site you previously installed using the version 1606 baseline media.
SABranchOptions does not apply to scripted upgrades from System Center 2012 Configuration Manager and always results in the Current Branch.
 For more information, see Use a command line to install System Center Configuration Manager sites

> ![IMPORTANT]  
> **SABranchOptions** only works with Setup from the baseline media. It does not apply when you run Setup from the CD.Latest folder of a site you previously installed using the version 1606 baseline media.
>
> **SABranchOptions** does not apply to scripted upgrades from System Center 2012 Configuration Manager and always results in the Current Branch.

For more information, see [Use a command line to install System Center Configuration Manager sites](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites).


## Install a new site
When you use the 1606 baseline media to install a new site of either branch, use the site planning, preparation, and installation procedures documented in the [Installing System Center Configuration Manager sites](/sccm/core/servers/deploy/install) topic with the addition of the following considerations for Setup:

- During Setup you must choose the branch of Configuration Manager that you want to install, and you can specify details for your Software Assurance agreement.
-	New scripted install options

## Expand a stand-alone primary site
You can expand a stand-alone primary site that runs the LTSB.  The process is no different than that used for a Current Branch site with one caveat:

- When installing the new central administration site you must use Setup from the original source media you used to install the LTSB site. (It is not supported to run Setup from the CD.Latest folder for this scenario).

For more information about expanding a site, see *Expand a stand-alone primary site* in [Install a site using the Setup Wizard](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-site).

## Upgrade from System Center 2012 Configuration Manager
When you upgrade from System Center 2012 Configuration Manager use the site planning, preparation, and procedures as documented in the [Upgrade to System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) topic, but with the following changes:

**Upgrade to the Current Branch:**
- During Setup, you must choose the Current Branch, and you can specify details for your Software Assurance agreement
- 	New scripted install options

**Upgrade to the LTSB:**  
- Additional steps to following in the pre-upgrade check list
- During Setup you must choose the LTSB, and you can specify details for your Software Assurance agreement
- You can only upgrade a site that runs System Center 2012 Configuration Manager with Service Pack 2 or System Center 2012 R2 Configuration Manager with Service Pack 1

## About the CD.Latest folder and the LTSB
The following are caveats to using the media that Configuration Manager creates in the CD.Latest folder on the site server. These apply to sites that run the LTSB:
Media in the CD.Latest folder is supported for:
- Site recovery
- Site maintenance
- Installing additional child primary sites

Media in the CD.Latest folder is not supported for:  
- Installing a central administration site as part of a site expansion scenario.

For more information, see [the CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder)

## Backup, recovery, and site maintenance for the LTSB
To backup, recover, or run site maintenance on a site that runs the LTSB, use the guidance and procedures from [Backup and recovery for System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  

Use Configuration Manager Setup from the CD.Latest folder of the backup of your LTSB site.
