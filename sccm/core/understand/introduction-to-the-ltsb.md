---
title: "Introduction to the Long-Term Servicing Branch"
description: "Learn about the Long-Term Servicing Branch of System Center Configuration Manager."
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid:  694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Introduction to the Long-Term Servicing Branch of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Long-Term Servicing Branch)*

The Long-Term Servicing Branch (LTSB) of System Center Configuration Manager is a distinct branch of Configuration Manager that is designed as an install option available to all customers. However, it is the only option for customers who let lapse their Software Assurance (SA) or equivalent subscription rights for Configuration Manager.


Based on Configuration Manager version 1606, the LTSB has reduced functionality when compared to the Current Branch of Configuration Manager.

 > [!TIP]   
 > If you were looking for information about the branches of **Windows Server**, see [Windows Server 2016 new Current Branch for Business servicing option]( https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/).

## Features that are not available in the LTSB of Configuration Manager
The Current Branch of Configuration Manager supports the following functionality that is not available when you use the LTSB:

-   In-console updates that add new features and improvements.
-   Support for newly released operating systems to use as site servers and clients.
-   Use of a Microsoft Intune Subscription to support:
    -   Intune in a hybrid mobile device management (MDM) configuration
    -   On-premises MDM
-   The Windows 10 Servicing Dashboard and Servicing Plans, including support for recent Windows 10 Current Branch (CB) and Current Branch for Business (CBB) versions.  
-   Support for future releases of Windows Server and Windows 10 LTSB
-   Asset Intelligence
-   Cloud-based distribution points
-   Exchange Online as an Exchange Connector    

Although support for these features is not available with the LTSB, some features remain visible in the Configuration Manager console, but cannot be selected or used.


## Find documentation for the LTSB
The LTSB is based on Current Branch version 1606. For product documentation use the [Current Branch documentation](https://docs.microsoft.com/sccm/), with caveats and limitations that are specific to the LTSB. Those caveats and limitations are identified in the following on-line topics:

-	  [Introduction to the  Long-Term Servicing Branch](introduction-to-the-ltsb.md): (This topic)
-	  [Install the  Long-Term Servicing Branch](install-the-ltsb.md)
-	  [Upgrade the  Long-Term Servicing Branch to the Current Branch](convert-to-current-branch.md)
-	  [Supported Configurations for the Long-Term Servicing Branch](supported-configurations-for-ltsb.md)
-   [Manage the Long-Term Servicing Branch of Configuration Manager](manage-the-ltsb.md)

When you reference Current Branch documentation for the LTSB, details that apply to version 1606 also apply to the LTSB. Features or details that are introduced with version 1610 or later are not supported by the LTSB.


## Licensing overview for the LTSB   
Customers with active Software Assurance (SA) on System Center Configuration Manager licenses, or with equivalent subscription rights as of October 1, 2016, have rights to use the October 2016 version 1606 release of System Center Configuration Manager. Customers with rights to System Center Configuration Manager on or after October 1, 2016, will find two licensed options upon installation: Current Branch and Long-Term Servicing Branch (LTSB).

Customers that have perpetual rights to System Center Configuration Manager, or that allow SA or subscription to lapse after October 1, can install the version of System Center Configuration Manager LTSB that is current at the time of lapse.

[Complete terms and conditions for the products you purchase through Microsoft Volume Licensing programs can be found here](http://go.microsoft.com/fwlink/?LinkId=800052).

See [System Center Configuration Manager licensing and branches](learn-more-editions.md) for more information about licensing for Configuration Manager branches.

## Next Steps

If you decide that the Configuration Manager LTSB is the correct branch for your environment, [install a new LTSB](/sccm/core/understand/install-the-ltsb#install-a-new-site) site as part of a new hierarchy, or [upgrade a System Center 2012 Configuration Manager site](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager) and hierarchy.

If you do not have installation media, see [System Center 2016 documentation](https://technet.microsoft.com/system-center-docs/system-center) for information on how to get System Center 2016, which includes media you can use to install the System Center Configuration Manager LTSB.  
