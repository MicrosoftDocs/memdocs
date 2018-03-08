---
title: "Which branch should I use"
titleSuffix: "Configuration Manager"
description: "Learn the differences between available branches of System Center Configuration Manager."
ms.custom: na
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
caps.latest.revision: 0
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# Which branch of Configuration Manager should I use?

*Applies to: System Center Configuration Manager (Current Branch, Long-Term Servicing Branch, and Technical Preview)*


Beginning in October of 2016, there are three branches of System Center Configuration Manager available. Use this topic to help choose the right branch for you.

> [!TIP]  
> All sites in a hierarchy must run the same branch. It is not supported to have a hierarchy with different branches at different sites.

## Current Branch of System Center Configuration Manager
This is a licensed branch for use in a production environment where you want the option to get the latest features and functionalities. This is the branch to use if you have one of the following: System Center Datacenter, System Center Standard, System Center Configuration Manager, or equivalent subscription rights. For more about Software Assurance and licensing options, see [Licensing and branches for System Center Configuration Manager](learn-more-editions.md).


>  [!TIP]
> The Current Branch can be installed as an evaluation edition that does not require a license. An evaluation edition can be used for 180 days, and it supports upgrade to a licensed edition of the Current Branch.

The Current Branch is updated several times a year with new features. Each update version is supported for one year after its release. You must update to a newer version of the Current Branch on or before expiration of that one-year period. Updates to newer versions are available as in-console updates.

To install the Current Branch as a new site or as an upgrade from System Center 2012 Configuration Manager with Service Pack 2 or System Center 2012 R2 Configuration Manager with Service Pack 1, you use [baseline media](/sccm/core/servers/manage/updates#baseline-and-update-versions) for System Center Configuration Manager that comes as a DVD with System Center 2016, or that is available as part of a standalone release of System Center Configuration Manager. Access to this media depends on how you have licensed System Center Configuration Manager. Later baseline versions, like 1702 do not support install of the LTSB.

You can also use the baseline media to install a new site that is an evaluation edition of the Current Branch. If you want to install only an evaluation edition, you can get software from the [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) website.

>  [!NOTE]
> Use baseline media to install sites for a new Configuration Manager hierarchy. If you have previously installed a baseline version like version 1511, use in-console updates to update your sites to a new version, like 1606.
>
> Sites that are updated using in-console updates result in sites that are the same as the new site installed using the baseline media.
>
> For more information see [Updates for System Center Configuration Manager](/sccm/core/servers/manage/updates).

**Features of the Current Branch**
- Receives [in-console updates](/sccm/core/servers/manage/install-in-console-updates) that make new features available for use.
- Receives in-console updates that deliver security and quality fixes to existing features.
- Supports out-of-band updates when necessary. See [Use the update registration tool](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) or [Use the hotfix installer](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Can interoperate with Microsoft Intune and other cloud-based services and infrastructure.
- Supports [migration of data](/sccm/core/migration/migrate-data-between-hierarchies) to and from other Configuration Manager installations.
- Supports upgrade from previous versions of Configuration Manager.
- Supports installation as an evaluation edition, from which you can later upgrade to a fully licensed installation.

The initial release of the Current Branch was version 1511. Subsequent updates include versions 1602, 1606, and so on. Each version remains in support for one year, and Microsoft recommends that you update to the newest version soon after its release. You can wait up to one year before updating to a newer version, and you can also skip an update to install the newest version available. Because each version is cumulative, if you skip over an update and install the newest version, you will still get access to all features and improvements from previous versions.

For more information, see [Support for Current Branch versions](/sccm/core/servers/manage/current-branch-versions-supported).

**Update options**
- With active Software Assurance, you can install in-console updates for Current Branch versions.  
- There is no option to convert the Current Branch to a Technical Preview. Technical Previews are separate installations that do not require a license.
- There is no option to convert your Current Branch to the Long-Term Servicing Branch (LTSB). You must uninstall the Current Branch and then install the LTSB as a new installation.

##  Long-Term Servicing Branch of System Center Configuration
This is a licensed branch for use in production for Configuration Manager customers who are using the Current Branch and have allowed their Configuration Manager Software Assurance (SA) or equivalent subscription rights to expire after October 1, 2016. For more about Software Assurance and licensing options, see [Licensing and branches for System Center Configuration Manager](learn-more-editions.md).

The LTSB is based on version 1606. This branch does not receive in-console updates that deliver new features or update existing capabilities. However, critical security fixes are provided. To install the LTSB, you must use the version 1606 [baseline media](/sccm/core/servers/manage/updates#baseline-and-update-versions) that you get as a DVD with System Center 2016 or System Center Configuration Manager.

To install the LTSB as a new site or as an upgrade from a supported Configuration Manager 2012 site, use the version 1606 [baseline media](/sccm/core/servers/manage/updates#baseline-and-update-versions) that you get as a DVD with System Center 2016 or System Center Configuration Manager (Current Branch and Long-Term Servicing Branch 1606) release. You can use baseline media to install a new site that runs version 1606 of the Current Branch, or a new site that runs the Long-Term Servicing Branch.

> [!TIP]  
> To learn about System Center 2016, see [System Center 2016 documentation](https://docs.microsoft.com/system-center/index). This documentation also identifies how to get System Center 2016, which requires a Microsoft license agreement or similar rights.

> To find System Center Configuration Manager version 1606 in the Volume Licensing Service Center (VLSC), go to the **Downloads and Keys** tab of the [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), search for "system center config," and then select **System Center Config Mgr (current branch and LTSB)**.

> You can also get an evaluation edition of System Center 2016 from the [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).

**Features of the LTSB**
-	Receives in-console updates that deliver critical security fixes
- Provides an installation option when your SA agreement or equivalent rights to Configuration Manager have expired
- Supports upgrade (conversion) to the Current Branch when you have a current SA agreement or equivalent rights to Configuration Manager

**Limitations**  
The LTSB is based on the Current Branch version 1606 and has the following limitations:
- The LTSB is supported for 10 years of critical security updates after its general availability (October of 2016), after which, support for this branch expires. For more about the support lifecycle, see [Microsoft Lifecycle Policy](https://support.microsoft.com/lifecycle).
- Supports a limited set list of server and client operating systems and related technologies, like SQL Server versions. For more about what is supported with this branch, see [Supported Configurations for the Long-Term Servicing Branch](supported-configurations-for-ltsb.md).
- Does not receive updates for new features.
- Does not support adding a Microsoft Intune Subscription, which prevents the use of:
  -	Intune in a hybrid MDM configuration
 - On-premises MDM
-	Does not support use of the Windows 10 Servicing Dashboard, servicing plans, Windows 10 Current Branch (CB), or Current Branch for Business (CBB).
- Does not support future releases of Windows 10 LTSB and Windows Server.
-	No support for Asset Intelligence.
-	No support for cloud-based distribution points.
-	No support for Support for Exchange Online as an Exchange Connector.
-	Does not support any pre-release features.



**Update options**
- You can convert your LTSB install to a Current Branch installation. Conversion to the current branch is supported before or after support for the LTSB expires.

  To convert, you must have an active Software Assurance agreement with Microsoft. For more information, see the following links:
  - [Upgrade the Long-Term Servicing Branch to the Current Branch](convert-to-current-branch.md)
  - [Licensing and branches for System Center Configuration Manager](learn-more-editions.md)
  - [Baseline and update versions](/sccm/core/servers/manage/updates#baseline-and-update-versions) in [Updates for Configuration Manager](/sccm/core/servers/manage/updates)
- There is no option to convert the LTSB to a Technical Preview. Technical Previews are separate installations that do not require a license.
-	You cannot upgrade an evaluation edition of the Current Branch to an LTSB installation.


## Technical Preview for System Center Configuration Manager
The Technical Preview is for use in a lab environment where you want to learn about and try out the newest features being developed for Configuration Manager. The Technical Preview is not supported in a production environment and does not require you to have a Software Assurance license agreement.

To install a new site that runs the Technical Preview, use the latest [baseline media for the System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview). After you install the Technical Preview, new versions are available as in-console updates each month.

**Features of the Technical Preview**
-  Based on recent baseline versions of the Current Branch
-  Receives in-console updates that update your installation to the latest Technical Preview version
-  Includes new features that are being developed and for which our developers would like your feedback
-  Receives updates that apply only to the Technical Preview branch

**Limitations**
-  [Support is limited](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), including only a single primary site and up to 10 clients.  
-  Cannot be upgraded to a Current Branch or LTSB.
-  Does not support using migration to import or export data to another Configuration Manager installation.
-  Does not support upgrade from a previous version of Configuration Manager.
-  Does not support installation as an evaluation edition.

Features that are first introduced in a Technical Preview are often added to the Current Branch in a later update. Each new Technical Preview version includes the features from previous technical previews, even after those features have been added to the Current Branch.

For more information, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).

**Update options**
-	You can install any in-console update for a new Technical Preview version.
-	There is no option to convert a Technical Preview to the Current Branch or LTSB.


## Identify your branch and version
When you view version information for a Configuration Manager site, you also confirm the branch.

**Version**   
To check the version of your site, in the console go to **About System Center Configuration Manager** at the upper-left corner of the console where the **Site version** appears. See [Baseline and Update versions](/sccm/core/servers/manage/updates#bkmk_Baselines) for a list of site versions.

**Branch**  
To confirm the branch of your site (as the LTSB or Current Branch), in the console go to **Administration** > **Site Configuration** > **Sites**, and open **Hierarchy Settings**. If there is an option to convert to the Current Branch and it is active, the site runs the LTSB version. When the site runs the Current Branch, this option is grayed out.
For information about the different versions of Configuration Manager, see "Baseline and update versions" in [Updates for Configuration Manager](/sccm/core/servers/manage/updates).
