---
title: "System Center Configuration Manager privacy statement - Configuration Manager Cmdlet Library | Microsoft Docs"
description: "Learn about how Microsoft collects and uses data related to the System Center Configuration Manager Cmdlet Library."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: 5
caps.handback.revision: 0
author: Brendunsms.author: brendunsmanager: angrobe

---
# System Center Configuration Manager privacy statement - Configuration Manager Cmdlet Library*Applies to: System Center Configuration Manager (Current Branch)*
This privacy statement covers the features for the System Center Configuration Manager Cmdlet Library.  

## Usage Data  
 **What This Feature Does:**   
The System Center Configuration Manager Cmdlet Library lets you manage a Configuration Manager hierarchy by using Windows PowerShell cmdlets and scripts. The Cmdlet Library collects information about how you use the cmdlets included in the library in order to identify trends and usage patterns.  The Cmdlet Library also collects the types and numbers of errors you encounter while using the cmdlets.  

 **Information Collected, Processed, or Transmitted:**   
The usage data collected includes starting, stopping and terminating of cmdlets; running of deprecated cmdlets and activity metrics for SMS provider operations related to the cmdlets. This information is not personally identifiable.  Error information collected includes errors returned by cmdlets and error details for exception errors. Some error detail reports might inadvertently contain individual identifiers, such as a serial number for a device that is connected to your computer. The Cmdlet library filters and anonymizes the information contained in the error reports to remove any individual identifiers before transmission to Microsoft.  

 **Use of Information:**   
We use this information to improve the quality, security and integrity of the products and services we offer.  

 **Choice/Control:**   
This Usage Data feature is enabled by default. The System Center Configuration Manager Cmdlet Library includes two registry keys to control this functionality.  

 To fully opt out you need to set these two registry key values, one for each of the Event Tracing for Windows (ETW) providers:  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (opts out of Usage Data for the drive provider)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (opts out of Usage Data for the cmdlets)  

 Changes to the Usage Data settings are specific to the computer where they are made.  

 For more information about how to configure Usage Data (collection), see the [System Center Configuration Manager Cmdlet Library documentation](https://technet.microsoft.com/en-us/library/dn958404.aspx).  

## Update Check  
 **What This Feature Does:**   
The System Center Configuration Manager Cmdlet Library automatically checks for library updates on a daily basis, and notifies you to download the updated library.  

 **Information Collected, Processed, or Transmitted:**   
The Cmdlet Library update check will download a small text file from the Microsoft Download Center to do a version check.   This file is not stored locally.  The Cmdlet Library will not automatically upgrade the software.  

 **Use of Information:**   
We use this information to improve the quality, security and integrity of the products and services we offer.  

 **Choice/Control:**   
The Update Check is enabled by default.  The System Center Configuration Manager Cmdlet Library includes these cmdlets to control the update notification functionality:  

-   `Get-CMCmdletUpdateCheck` gets the update feature configuration and will indicate if user policy is being overridden by system policy.  

-   `Send-CMCmdletUpdateCheck` lets you perform an unscheduled update check. An unscheduled check does not consider policy settings.  

-   `Set-CMCmdletUpdateCheck` configures the update check settings on a per-user or per-system basis. You must be running as an administrator to set system settings.  

 You can find more information about to configure the update check in the [System Center Configuration Manager Cmdlet Library documentation](https://technet.microsoft.com/en-us/library/dn958404.aspx).  
