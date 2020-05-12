---
title: Privacy statement for cmdlets
titleSuffix: Configuration Manager
description: Learn about how Microsoft collects and uses data related to the Configuration Manager cmdlets
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby


--- 

# Configuration Manager cmdlet library privacy statement

*Applies to: Configuration Manager (current branch)*

This privacy statement covers the features for the Configuration Manager Cmdlet Library.  

## Usage data  

#### What this feature does

The Configuration Manager cmdlet library lets you manage a Configuration Manager hierarchy by using Windows PowerShell cmdlets and scripts. The cmdlet library collects information about how you use the cmdlets in the library to identify trends and usage patterns. The cmdlet library also collects the types and numbers of errors that you receive when you use the cmdlets.  

#### Information collected, processed, or transmitted
   
The collected usage data includes starting, stopping, and terminating of cmdlets, running of deprecated cmdlets, and activity metrics for SMS Provider operations that are related to the cmdlets. This information isn't personally identifiable. Collected error information includes errors that cmdlets return and error details for exception errors. Some error detail reports might inadvertently include individual identifiers, like a serial number for a device that is connected to your computer. The cmdlet library filters and anonymizes information that's in the error reports to remove individual identifiers before transmission to Microsoft.  

#### Use of information
   
Microsoft uses this information to improve the quality, security, and integrity of the products and services they offer.  

#### Choice/control   

This usage data feature is enabled by default. The Configuration Manager cmdlet library has two registry keys that control this functionality.  

 To fully opt out, set these two registry key values. They are for each of the Event Tracing for Windows (ETW) providers:  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (opts out of usage data for the drive provider)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (opts out of usage data for the cmdlets)  

  Changes to the usage data settings are specific to the computer where they're made.  


## Next steps

[Configuration Manager Cmdlet Library documentation](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   
