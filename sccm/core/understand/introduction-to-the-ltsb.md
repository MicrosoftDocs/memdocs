---
title: "Introduction to the Long-Term Servicing Branch | System Center Configuration Manager"
description: "Learn about the Long-Term Servicing Branch of System Center Configuration Manager."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid:  694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: 0
author: Brendunsms.author: brendunsmanager: angrobe

---
# Introduction to the Long-Term Servicing Branch of System Center Configuration Manager


Use this topic to learn about the  Long-Term Servicing Branch (LTSB) of Configuration Manager and understand the documentation for this branch.


The LTSB is a distinct branch of Configuration Manager that is based on version 1606 of the Current Branch. When compared to the Current Branch, the LTSB has [reduced functionality](#features-that-are-not-available-in-the-ltsb-of-configuration-manager). It is designed for customers who have [allowed their Software Assurance (SA) or equivalent subscription rights to lapse](/sccm/core/understand/learn-more-editions#software-assurance-and-the-ltsb).

**Licensing overview:**   
Customers with active Software Assurance (SA) on System Center Configuration Manager licenses or with equivalent subscription rights as of October 1, 2016 have next version rights to the October 2016 release of System Center Configuration Manager. Customers with rights to System Center Configuration Manager on or after October 1, 2016 will find two licensed options upon installation: Current Branch and Long-Term Servicing Branch (LTSB).

**Licensing specifics:**  
[Complete terms and conditions for the products you purchase through Microsoft Volume Licensing programs can be found here](http://go.microsoft.com/fwlink/?LinkId=800052).

Customers that have perpetual rights to System Center Configuration Manager, or that allow SA or subscription to lapse after October 1, can install the version of System Center Configuration Manager LTSB that is current at the time of lapse.
- For information about Software Assurance and license requirements for System Center Configuration Manager, see [System Center Configuration Manager licensing and branches](learn-more-editions.md).
-	For information about the differences between the different branches, see [Which branch of Configuration Manager should I use](which-branch-should-i-use.md).

To install a new site or upgrade from a supported System Center 2012 Configuration Manager site to the LTSB, you use the version 1606 baseline media. This baseline media is availalbe on DVD as part of Microsoft System Center 2016. Baseline media that can install the LTSB can also be used to install the Current Branch version 1606 of Configuration Manager. To learn about baseline media, see [Baseline and update versions](/sccm/core/servers/manage/updates#baseline-and-update-versions).

For information on how to install a LTSB site, see [Install and Upgrade for the Long-Term Servicing Branch](install-the-ltsb.md). See the [System Center 2016 documentation](https:\technet.microsoft.com\system-center-docs\System-Center-2016) for information on how to get System Center 2016.

> [!IMPORTANT]
> All sites in a hierarchy must run the same branch. It is not supported to have a hierarchy with a mix of LTSB and Current Branch at different sites.
>
> Similarly, when you use recovery you must restore the site or site database to its original branch. You cannot recover a Current Branch site database to a LTSB installation, or vice versa.


## Features that are not available in the LTSB of Configuration Manager
When compared to the Current Branch, the LTSB has the following support limitations:

- Does not receive updates for new features.
- Does not support adding a Microsoft Intune Subscription, which prevents the use of:
  -	Intune in a hybrid MDM configuration
	- On-premises MDM
-	Does not support use of the Windows 10 Servicing Dashboard, Servicing Plans, and does not support Windows 10 Current Branch and CBB
-	No support for Asset Intelligence
-	No support for cloud-based distribution points
-	No support for Support for Exchange Online as an Exchange Connector
-	Does not support any pre-release features


Although support for these features is not included in the LTSB, some features remain visible in the Configuration Manager console, but cannot be selected or used.

In addition, new operating systems that are added as supported by the Current Branch will not be supported by the LTSB.

## Documentation for the LTSB
Because the LTSB is based on the version 1606 Current Branch, the documentation you use for the LTSB is the [on-line documentation that applies to the Current Branch](https://docs.microsoft.com/sccm/), with the caveats and limitations that are specific to the LTSB as identified in the following topics:  

-	[Introduction to the  Long-Term Servicing Branch](introduction-to-the-ltsb.md)  - (This topic)

-	[Which branch of Configuration Manager should I use](which-branch-should-i-use.md) – Information about the different System Center Configuration Manager branches, so you can be sure to install the best branch for your needs.

-	[Install the  Long-Term Servicing Branch](install-the-ltsb.md) - How to install a new LTSB site, or upgrade a System Center 2012 Configuration Manager site to the LTSB.

-	[Upgrade the  Long-Term Servicing Branch to the Current Branch](convert-to-current-branch.md) – How to convert your LTSB installation to a Current Branch installation.

-	[Licensing and branches for System Center Configuration Manager](learn-more-editions.md) – Information about Software Assurance and related license requirement for System Center Configuration Manager.
-	[Supported Configurations for the Long-Term Servicing Branch](supported-configurations-for-ltsb) - The versions and requirements for operating system and dependent products like SQL Server that you can use with the LTSB.

-	[Use the Long-Term Servicing Branch client with a Current Branch site](convert-to-current-branch.md) – Information about using a client from the LTSB with a Current Branch site so that critical infrastructure can use a client that does not regularly update.

To help you distinguish which branch specific documentation applies to, use the following guide:  
-	Topics with a header of *Applies to: Current Branch* apply to both the Current Branch, and the  Long-Term Servicing Branch (though parts of the topic might only apply to a newer version of the Current Branch).

-	To identify parts of a topic that do not apply to the LTSB, features and changes that are introduced after version 1606 of the Current Branch are identified with wording like ‘Beginning with version 1610’. Because these were introduced after the 1606 version of Current Branch, they are not available with the LTSB.

### Similarities between the Current Branch and the LTSB
Because the LTSB is based on the Current Branch version 1606 (with some exceptions like Intune integration and cloud-related features), most tasks for planning deploying, configuring and managing the two branches are identical.

For example, the LTSB supports the same number of sites, site types, clients, and general infrastructure as the Current Branch. Therefore, you use the guidance found in the site and hierarchy planning and design topics for the Current Branch. Similarly, for features supported by both branches like Software Updates or Operating System Deployment, you use the guidance found in those sections of the Current Branch documentation with the caveats of not having access to the changes introduced after the 1606 version of the Current Branch.


## How to identify your branch and version
When you view version information for a Configuration Manager site, you also confirm the branch.

To check the version of your site, in the console go to **About System Center Configuration Manager** at the top-left corner of the console where the **Site version** displays as **5.0.8412.1000**.

To confirm the branch of your site (as LTSB or Current Branch), in the console go to **Administration** > **Site Configuration** > **Sites**, and open **Hierarchy Settings**.  If there is an option to convert to the Current Branch and it is active, the site runs the LTSB version. When the site runs the Current Branch, this option is grayed out.

For information about the different versions of Configuration Manager, see **Baseline and update versions** in the [Updates for Configuration Manager](/sccm/core/servers/manage/updates) topic.

## Exceptions for using the LTSB
### Updates and servicing of the LTSB
Only critical security updates are made available as in-console updates in the LTSB.

However, information about regular updates for the subsequent Current Branch releases are visible in the console. Because these are not made available to the LTSB these updates are not downloaded, and cannot be installed.

To support in-console updates for critical security fixes, an LTSB site requires the use of [the service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point). You can configure this site system role in off-line or on-line mode, as is done for the Current Branch. The LTSB collects and submits the same telemetry and usage data as the Current Branch.

The LTSB supports the use of the Hotfix Installer and Update Registration tool, as documented for the Current Branch.

For general information about updates and servicing, see [Updates for Configuration Manager](/sccm/core/servers/manage/updates).

### Changes for site expansion and the CD.Latest folder
When you run the LTSB and are expanding a stand-alone primary site by installing a new central administration site, you must use Setup and the source files from the version 1606 baseline media from the System Center 2016 suite.  (For the Current Branch, you run Setup and use source files from the CD.Latest folder.)

Although you do not run Setup for site expansion from the CD.Latest folder, you continue to use the CD.Latest folder for site recovery, and to install a new child primary site when your first LTSB site was a central administration site.

For more information about site expansion, see  [Expand a stand-alone primary site](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site) in [Use the Setup Wizard to install sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).
For more information about the CD.Latest folder, see [The CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder).
