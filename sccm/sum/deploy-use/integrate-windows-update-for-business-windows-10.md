---
title: "Integration with Windows Update for Business in Windows 10"
ms.custom: na
ms.date: 2016-08-10
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-sum
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
caps.latest.revision: 11
author: Dougeby
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Integration with Windows Update for Business in Windows 10
Windows Update for Business (WUfB) allows you to keep Windows 10-based devices in your organization always up to date with the latest security defenses and Windows features when these devices connect directly to the Windows Update (WU) service. Configuration Manager has the ability to differentiate between Windows 10 computers that use WUfB and WSUS for getting software updates .  
  
 Some Configuration Manager features are no longer available when Configuration Manager clients  are configured to receive updates from WU, which includes WUfB or Windows Insiders:  
  
-   Windows Update compliance reporting:  
  
    -   Configuration Manager will be unaware of the updates that are published to WU. The Configuration Manager clients configured to received updates from WU will display **unknown** for these updates in the Configuration Manager console.  
  
    -   Troubleshooting overall compliance status is difficult  because **unknown** status used to be only for the clients that hadn't reported scan status back from WSUS.  Now it also includes Configuration Manager clients that receive updates from WU.  
  
    -   Conditional access (for corporate resources) based on update compliance status will not work as expected for clients that receive updates from WU because they would never meet compliance from Configuration Manager.  
  
    -   Definition Updates compliance is part of overall update compliance reporting and will not work as expected either.  Definition update compliance is also part of conditional access evaluation  
  
-   Overall Endpoint Protection reporting for Defender based on update compliance status will not return accurate results because of the   missing scan data.  
  
-   Configuration Manager will not be able to deploy Microsoft updates,  such as Office, IE,  and Visual Studio to clients that are connected to WUfB to receive updates.  
  
-   Configuration Manager will not be able to deploy 3rd party updates that are published to WSUS and managed through Configuration Manager to clients that are connected to WUfB to receive updates.  
  
-   Configuration Manager full client deployment that uses the software updates infrastructure will not work for clients that are connected to WUfB to receive updates.  
  
## Identify clients that use  WUfB for Windows 10 updates  
 Use the following procedure to identify  clients that use WUfB to get Windows 10 updates and upgrades, configure these clients to stop using WSUS to get updates, and deploy a client agent setting to disable   the software updates workflow for these clients.  
  
 **Prerequisites**  
  
-   Clients that run Windows 10 Desktop Pro or Windows 10 Enterprise Edition version 1511 or later  
  
-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) is deployed and clients use WUfB to get Windows 10 updates and upgrades.  
  
#### To identify clients that use WUfB  
  
1.  Disable the Windows Update Agent so it doesn't scan against WSUS,  if it was previously enabled.   
    The registry key **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer** can be set to indicate whether the computer is scanning against WSUS or Windows Update.  When the value is  2, it’s not scanning against WSUS.  
  
2.  There is a new attribute,  **UseWUServer**, under the **Windows Update** node in Configuration Manager Resource Explorer.  
  
3.  Create a collection based on the **UseWUServer** attribute for all the computers that are connected via WUfB for updates and upgrades.  
  
4.  Create a  client agent setting to disable the software update workflow and deploy the setting to the collection of computers that are connected directly to WUfB.  
  
5.  The computers that are managed via WUfB will display **Unknown** in the compliance status and won’t be counted as part of the overall compliance percentage.  
  
## See Also  
 [Manage software updates in System Center Configuration Manager](../../sup/deploy-use/manage-software-updates.md)