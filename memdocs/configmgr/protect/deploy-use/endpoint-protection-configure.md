---
title: Configure Endpoint Protection
titleSuffix: Configuration Manager
description: Learn how to set up Configuration Manager to update and distribute malware definitions for Windows Defender.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Configure Endpoint Protection

*Applies to: Configuration Manager (current branch)*

Before you can use Endpoint Protection to manage security and malware on Configuration Manager client computers, you must perform the configuration steps detailed in this article.  

## How to Configure Endpoint Protection in Configuration Manager  
 Endpoint Protection in Configuration Manager has external dependencies and dependencies in the product.  

### Steps to Configure Endpoint Protection in Configuration Manager  
 Use the following table for the steps, details, and more information about how to configure Endpoint Protection.  

> [!IMPORTANT]  
>  If you manage endpoint protection for Windows 10 or later computers, then you must configure Configuration Manager to update and distribute malware definitions for Windows Defender. Windows Defender is included in Windows 10 and later but custom client settings for Endpoint Protection (**Step 5** below) are still required. </br> </br>


|Steps|Details|  
|-----------|-------------|  
|**Step 1:** [Create an Endpoint Protection point site system role](endpoint-protection-site-role.md)|The Endpoint Protection point site system role must be installed before you can use Endpoint Protection. It must be installed on one site system server only, and it must be installed at the top of the hierarchy on a central administration site or a stand-alone primary site. |  
|**Step 2:** [Configure alerts for Endpoint Protection](endpoint-configure-alerts.md)|Alerts inform the administrator when specific events have occurred, such as a malware infection. Alerts are displayed in the **Alerts** node of the **Monitoring** workspace, or optionally can be emailed to specified users. |  
|**Step 3:** [Configure definition update sources for Endpoint Protection clients](endpoint-definition-updates.md)|Endpoint Protection can be configured to use various sources to download definition updates. |  
|**Step 4:** [Configure the default antimalware policy and create custom antimalware policies](endpoint-antimalware-policies.md)|The default antimalware policy is applied when the Endpoint Protection client is installed. Any custom policies you have deployed are applied by default, within 60 minutes of deploying the client. Ensure that you have configured antimalware policies before you deploy the Endpoint Protection client. |  
|**Step 5:** [Configure custom client settings for Endpoint Protection](endpoint-protection-configure-client.md)|Use custom client settings to configure Endpoint Protection settings for collections of computers in your hierarchy.<br /><br /> Note: Do not configure the default Endpoint Protection client settings unless you are sure that you want these settings applied to all computers in your hierarchy. |  
