---
title: "Privacy statement for Configuration Manager cmdletlLibrary"
description: "Learn about how Microsoft collects and uses data related to the System Center Configuration Manager cmdlet library."
ms.custom: na
ms.date: 1/3/2017
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
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# System Center Configuration Manager privacy statement - Configuration Manager cmdlet library

*Applies to: System Center Configuration Manager (Current Branch)*

This privacy statement covers the features for the System Center Configuration Manager Cmdlet Library.  

## Usage data  
 **What this feature does:**   
The System Center Configuration Manager cmdlet library lets you manage a Configuration Manager hierarchy by using Windows PowerShell cmdlets and scripts. The cmdlet library collects information about how you use the cmdlets in the library to identify trends and usage patterns. The cmdlet library also collects the types and numbers of errors that you encounter when you use the cmdlets.  

 **Information collected, processed, or transmitted:**   
The collected usage data includes starting, stopping and terminating of cmdlets, running of deprecated cmdlets, and activity metrics for Systems Management Server (SMS) provider operations that are related to the cmdlets. This information is not personally identifiable.  Collected error information includes errors that cmdlets return and error details for exception errors. Some error detail reports might inadvertently contain individual identifiers, like a serial number for a device that is connected to your computer. The cmdlet library filters and anonymizes information that's in the error reports to remove individual identifiers before transmission to Microsoft.  

 **Use of information:**   
We use this information to improve the quality, security, and integrity of the products and services we offer.  

 **Choice/control:**   
This usage data feature is enabled by default. The System Center Configuration Manager cmdlet library has two registry keys that control this functionality.  

 To fully opt out you need to set these two registry key values, one for each of the Event Tracing for Windows (ETW) providers:  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (opts out of Usage Data for the drive provider)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (opts out of Usage Data for the cmdlets)  

 Changes to the Usage Data settings are specific to the computer where they are made.  

 For more about how to configure usage data (collection), see the [System Center Configuration Manager Cmdlet Library documentation](https://technet.microsoft.com/en-us/library/dn958404.aspx).   
