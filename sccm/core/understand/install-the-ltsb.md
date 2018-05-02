---
title: "Install a site using the 1606 baseline media "
titleSuffix: "Configuration Manager"
description: "Install or upgrade to the LTSB for System Center Configuration Manager."
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Install and upgrade with the version 1606 baseline media for System Center Configuration Manager

*Applies to:  System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*

When you run Setup from the version 1606 baseline media for Configuration Manager, you can install the Long-Term Servicing Branch or a Current branch site of System Center Configuration Manager.

The baseline media is available on DVD as part of Microsoft System Center 2016, or from System Center Configuration Manager (Current Branch and Long-Term Servicing Branch 1606) release. To learn about baseline media, see [Baseline and update versions](/sccm/core/servers/manage/updates#baseline-and-udpate-versions).


When you use the version 1606 baseline media, the site you install or upgrade to is:
- A *Current Branch site* that is equivalent to a site that was first installed using the 1511 baseline media, and then updated to version 1606 plus the 1606 hotfix rollup - KB3186654.
-	An *LTSB site* that is equivalent to the Current Branch site that runs version 1606 plus the 1606 hotfix rollup - KB3186654. The baseline media already includes the hotfix rollup.  But, the LTSB does not support all of the features or capabilities available with the Current Branch, as detailed in [Introduction to the Long-Term Servicing Branch of System Center Configuration Manager](introduction-to-the-ltsb.md).

If you are not familiar with the different branches of System Center Configuration Manager, see [Which branch of Configuration Manager should I use](which-branch-should-i-use.md).




## Changes to Setup with the 1606 baseline media
The 1606 baseline media introduces the following changes to Setup for Configuration Manager.

### Branch and edition
When you run Setup, you are now presented with a Licensing page where you can select the branch of Configuration Manager you want to install. You can choose either the Current Branch or LTSB as a licensed installation, or you can choose an Evaluation edition of the Current Branch as a non-licensed installation.

For more information, see [Licensing and branches for System Center Configuration Manager](learn-more-editions.md).

### Software Assurance expiration
During Setup, you have the option to enter the **Software Assurance expiration date** value. This is an optional value that you can specify as a convenient reminder.

> [!NOTE]
> Microsoft does not validate the expiration date you enter and will not use this date for license validation.  Instead, you can use it as a reminder of your expiration date. This is useful because Configuration Manager periodically checks for new software updates offered online, and your software assurance license status should be current to be eligible to use these additional updates.    

- You can specify the date value on the **Product Key** page of the Setup Wizard when you run Setup from the System Center Configuration Manager version 1606 baseline media.
- You can also specify this date by selecting **Hierarchy Settings Properties** > **Licensing** in the Configuration Manager console.

For more information, see "Software Assurance agreements" in [Licensing and branches for System Center Configuration Manager](learn-more-editions.md).


### Additional pre-upgrade configurations
Prior to starting an upgrade of System Center 2012 Configuration Manager to the LTSB, you must take the following additional steps as part of pre-upgrade checklist.  
Uninstall the site system roles that the LTSB does not support:
- Asset Intelligence synchronization point
- Microsoft Intune connector
- Cloud-based distribution points

For more information, see [Upgrade to System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).


### New scripted installation options
The version 1606 baseline media supports a new unattended script file key for scripted installations of a new top-level site. This applies to installing a new stand-alone primary site or adding a central administration site as part of a site expansion scenario.

When using an unattended script to install a licensed branch, you must add the following section, key names, and values to the Options section of your script. You don't need to use these values to script the install of an Evaluation edition of the Current Branch:  

 **SABranchOptions**
- 	**Key Name: SAActive**
  - Values: 0 or 1.  
  - Details:  0 installs a non-licensed Evaluation edition of Current Branch, and 1 installs a licensed edition.   

- **CurrentBranch**
  - Values: 0 or 1.  
  - Details:  0 installs the Long-Term Servicing Branch, and 1 installs the Current Branch.  

For example, to install a licensed Current Branch edition you would use:

  **Key Name: SABranchOptions**
   -	**SAActive = 1**
   - **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** only works with Setup from the baseline media. It does not apply when you run Setup from the CD.Latest folder of a site you previously installed using the version 1606 baseline media.
>
> **SABranchOptions** does not apply to scripted upgrades from System Center 2012 Configuration Manager and always results in the Current Branch.

For more information, see [Use a command line to install System Center Configuration Manager sites](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites).


## Install a new site
When you use the 1606 baseline media to install a new site of either branch, use the site planning, preparation, and installation procedures documented in the [Installing System Center Configuration Manager sites](/sccm/core/servers/deploy/install/installing-sites) topic with the addition of the following considerations for Setup:

- During Setup you must choose the branch of Configuration Manager that you want to install, and you can specify details for your Software Assurance agreement.
- All sites in the same hierarchy must run the same branch. It is not supported to have a hierarchy with a mix of LTSB and Current Branch at different sites.
-	New scripted installation. For more information, see "New scripted installation options" earlier in this article.

## Expand a stand-alone primary site
You can expand a stand-alone primary site that runs the LTSB.  The process is no different than that used for a Current Branch site with one caveat:

- When installing the new central administration site you must use Setup from the original source media you used to install the LTSB site. Running Setup from the CD.Latest folder for this scenario is not supported.

For more information about expanding a site, see "Expand a stand-alone primary site" in [Install a site using the Setup Wizard](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).

## Upgrade from System Center 2012 Configuration Manager
When you upgrade from System Center 2012 Configuration Manager, use the site planning, preparation, and procedures as documented in the [Upgrade to System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) topic, but with the following changes:

**Upgrade to the Current Branch:**
- During Setup, you must choose the Current Branch, and you can specify details for your Software Assurance agreement.
- 	New scripted installation. For more information, see "New scripted installation options" earlier in this article.

**Upgrade to the LTSB:**  
- Additional steps to following in the pre-upgrade checklist.
- During Setup you must choose the LTSB, and you can specify details for your Software Assurance agreement.
- You can only upgrade a site that runs System Center 2012 Configuration Manager with Service Pack 1, System Center 2012 Configuration Manager with Service Pack 2, System Center 2012 R2 Configuration Manager with Service Pack 1, or System Center 2012 R2 Configuration Manager with no service pack.

### In-place upgrade paths for the 1606 baseline media
You can use the 1606 baseline media to upgrade the following to a licensed edition of System Center Configuration Manager:
- System Center 2012 R2 Configuration Manager with Service Pack 1
- System Center 2012 R2 Configuration Manager with no service pack (this requires the use of the baseline media for version 1606 that was rereleased on December 15th, 2016.)
- System Center 2012 Configuration Manager with Service Pack 2
- System Center 2012 Configuration Manager with Service Pack 1 (this requires the use of the baseline media for version 1606 that was rereleased on December 15th, 2016.)


You can also use this media to upgrade a non-licensed Evaluation edition of Current Branch to a fully licensed version of the Current Branch.

This media does not support the upgrade of:
- Other versions of System Center 2012 Configuration Manager.
- Configuration Manager 2007 or earlier.
- A release candidate installation of System Center Configuration Manager.

## About the CD.Latest folder and the LTSB
The following are limitations on using the media that Configuration Manager creates in the CD.Latest folder on the site server. These limits apply to sites that run the LTSB:

Media in the CD.Latest folder is supported for:
- Site recovery.
- Site maintenance.
- Installing additional child primary sites.

Media in the CD.Latest folder is not supported for:  
- Installing a central administration site as part of a site expansion scenario.

For more information, see [the CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder).

## Backup, recovery, and site maintenance for the LTSB
To back up, recover, or run site maintenance on a site that runs the LTSB, use the guidance and procedures from [Backup and recovery for System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  

Use Configuration Manager Setup from the CD.Latest folder of the backup of your LTSB site.
