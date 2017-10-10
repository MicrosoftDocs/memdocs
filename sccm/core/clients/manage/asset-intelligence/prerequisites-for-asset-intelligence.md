---
title: "Asset Intelligence Prerequisites"
titleSuffix: "Configuration Manager"
description: "Get the prerequisites for Asset Intelligence in System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
caps.latest.revision: 10
caps.handback.revision: 0
author: andredm7 
ms.author: andredm 
manager: angrobe

---
# Prerequisites for Asset Intelligence in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Asset Intelligence in System Center Configuration Manager has external dependencies and dependencies within the product.  

## Dependencies external to Configuration Manager  
 The following table provides the dependencies for Asset Intelligence that are external to Configuration Manager.  

|Dependency|More Information|  
|----------------|----------------------|  
|Auditing of Success Logon Events Prerequisites|Four Asset Intelligence reports display information gathered from the Windows Security event logs on client computers. If the Security event log settings are not configured to log all Success logon events, these reports contain no data even if the appropriate hardware inventory reporting class is enabled.<br /><br /> The following Asset Intelligence reports depend on collected Windows Security event log information:<br /><br /> -   Hardware 03A - Primary Computer Users<br />-   Hardware 03B - Computers for a Specific Primary Console User<br />-   Hardware 04A - Shared (Multi-user) Computers<br />-   Hardware 05A - Console Users on a Specific Computer<br /><br /> To enable the Hardware Inventory Client Agent to inventory the information required to support these reports, you must first modify the Windows Security event log settings on clients to log all Success logon events, and enable the **SMS_SystemConsoleUser** hardware inventory reporting class. For more information about modifying Security event log settings to log all Success logon events, see [Enable auditing of success logon events](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents).|  

> [!NOTE]  
>  The **SMS_SystemConsoleUser** hardware inventory reporting class retains successful logon event data for only the previous 90 days of the Security event log, regardless of the length of the log. If the Security event log has fewer than 90 days of data, the entire log is read.  

## Dependencies Internal to Configuration Manager  
 The following table provides the dependencies for Asset Intelligence that are internal to Configuration Manager.  

|Dependency|More Information|  
|----------------|----------------------|  
|Client Agent Prerequisites|The Asset Intelligence reports depend on client information that is obtained through client hardware and software inventory reports. To obtain the information necessary for all Asset Intelligence reports, the following client agents must be enabled:<br /><br /> -   Hardware Inventory Client Agent<br />-   Software Metering Client Agent|  
|Hardware Inventory Client Agent Dependencies|To collect inventory data required for some Asset Intelligence reports, the Hardware Inventory Client Agent must be enabled. In addition, some hardware inventory reporting classes that Asset Intelligence reports depend on must be enabled on primary site server computers.<br /><br /> For information about enabling the Hardware Inventory Client Agent, see [How to extend hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).|  
|Software Metering Client Agent Dependencies|A number of Asset Intelligence software reports depend on the Software Metering Client Agent for data. For information about enabling the Software Metering Client Agent, see [Monitor app usage with software metering in System Center Configuration Manager](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).<br /><br /> The following Asset Intelligence reports depend on the Software Metering Client Agent to provide data:<br /><br /> -   Software 07A - Recently Used Executables by Number of Computers<br />-   Software 07B - Computers that Recently Used a Specified Executable<br />-   Software 07C - Recently Used Executables on a Specific Computer<br />-   Software 08A - Recently Used Executables by Number of Users<br />-   Software 08B - Users that Recently Used a Specified Executable<br />-   Software 08C - Recently Used Executables by a Specified User|  
|Asset Intelligence Hardware Inventory Reporting Class Prerequisites|Asset Intelligence reports in Configuration Manager depend on specific hardware inventory reporting classes. Until the hardware inventory reporting classes are enabled and clients have reported hardware inventory based on these classes, the associated Asset Intelligence reports do not contain any data. You can enable the following hardware inventory reporting classes to support Asset Intelligence reporting requirements:<br /><br /> -   SMS_SystemConsoleUsage<sup>1</sup><br />-   SMS_SystemConsoleUser<sup>1</sup><br />-   SMS_InstalledSoftware<br />-   SMS_AutoStartSoftware<br />-   SMS_BrowserHelperObject<br />-   Win32_USBDevice<br />-   SMS_InstalledExecutable<br />-   SMS_SoftwareShortcut<br />-   SoftwareLicensingService<br />-   SoftwareLicensingProduct<br />-   SMS_SoftwareTag<br /><br /> <sup>1</sup> By default, the **SMS_SystemConsoleUsage** and **SMS_SystemConsoleUser** Asset Intelligence hardware inventory reporting classes are enabled.<br /><br /> You can edit the Asset Intelligence hardware inventory reporting classes in the Configuration Manager console, in the **Assets and Compliance** workspace, when you click the **Asset Intelligence** node. For more information, see the [Enable Asset Intelligence hardware inventory reporting classes](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) section in the [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) topic.|  
|Reporting services point|The reporting services point site system role must be installed before software updates reports can be displayed. For more information about creating a reporting services point, see [Configuring Reporting in Configuration Manager](http://go.microsoft.com/fwlink/p/?LinkId=232661).|  
