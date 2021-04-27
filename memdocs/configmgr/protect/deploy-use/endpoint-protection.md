---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: Learn how to manage antimalware policies and Windows Defender Firewall security for clients.
ms.date: 03/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: mestew
ms.author: mstewart
manager: dougeby
---

# Endpoint Protection

*Applies to: Configuration Manager (current branch)*

Endpoint Protection manages antimalware policies and Windows Defender Firewall security for client computers in your Configuration Manager hierarchy.  

> [!IMPORTANT]  
>  You must be licensed to use Endpoint Protection to manage clients in your Configuration Manager hierarchy.  

 When you use Endpoint Protection with Configuration Manager, you have the following benefits:  

-   Configure antimalware policies, Windows Defender Firewall settings, and manage Microsoft Defender Advanced Threat Protection to selected groups of computers  
-   Use Configuration Manager software updates to download the latest antimalware definition files to keep client computers up-to-date  
-   Send email notifications, use in-console monitoring, and view reports. These actions inform administrative users when malware is detected on client computers.  

Beginning with Windows 10 and Windows Server 2016 computers, Microsoft Defender Antivirus is already installed. For these operating systems, a management client for Microsoft Defender Antivirus is installed when the Configuration Manager client installs. On Windows 8.1 and earlier computers, the Endpoint Protection client is installed with the Configuration Manager client. Microsoft Defender Antivirus and the Endpoint Protection client have the following capabilities:  

-   Malware and spyware detection and remediation  
-   Rootkit detection and remediation  
-   Critical vulnerability assessment and automatic definition and engine updates  
-   Network vulnerability detection through Network Inspection System  
-   Integration with Cloud Protection Service to report malware to Microsoft. When you join this service, the Endpoint Protection client or Microsoft Defender Antivirus downloads the latest definitions from the Malware Protection Center when unidentified malware is detected on a computer.  

> [!NOTE]  
>  The Endpoint Protection client can be installed on a server that runs Hyper-V and on guest virtual machines with supported operating systems. To prevent excessive CPU usage, Endpoint Protection actions have a built-in randomized delay so that protection services do not run simultaneously.  

 In addition, you manage Windows Defender Firewall settings with Endpoint Protection in the Configuration Manager console.  

 [Example scenario: Using System Center Endpoint Protection to protect computers from malware](scenarios-endpoint-protection.md) Endpoint Protection and the Windows Defender Firewall.  


## Managing Malware with Endpoint Protection  
 Endpoint Protection in Configuration Manager allows you to create antimalware policies that contain settings for Endpoint Protection client configurations. Deploy these antimalware policies to client computers. Then monitor compliance in the **Endpoint Protection Status** node under **Security** in the **Monitoring** workspace. Also use Endpoint Protection reports in the **Reporting** node.  

 Additional information:  

-   [How to create and deploy antimalware policies for Endpoint Protection](endpoint-antimalware-policies.md) - Create, deploy, and monitor antimalware policies with a list of the settings that you can configure  

-   [How to monitor Endpoint Protection](monitor-endpoint-protection.md) - Monitoring activity reports, infected client computers, and more.  

-   [How to manage antimalware policies and firewall settings for Endpoint Protection](endpoint-antimalware-firewall.md) - Remediate malware found on client computers  

-   [Log files for Endpoint Protection](../../core/plan-design/hierarchy/log-files.md#BKMK_EPLog)  


## Managing Windows Defender Firewall with Endpoint Protection  
 Endpoint Protection in Configuration Manager provides basic management of the Windows Defender Firewall on client computers. For each network profile, you can configure the following settings:  

-   Enable or disable the Windows Defender Firewall.  

-   Block incoming connections, including those in the list of allowed programs.  

-   Notify the user when Windows Defender Firewall blocks a new program.  

> [!NOTE]  
>  Endpoint Protection supports managing the Windows Defender Firewall only.  


 For more information, see [How to create and deploy Windows Defender Firewall policies for Endpoint Protection](create-windows-firewall-policies.md).  


## Microsoft Defender for Endpoint

Microsoft Defender for Endpoint manages and monitors Microsoft Defender Advanced Threat Protection (ATP), formerly known as Windows Defender ATP. The Microsoft Defender for Endpoint service helps enterprises detect, investigate, and respond to advanced attacks on the corporate network. For more information, see [Microsoft Defender Advanced Threat Protection](defender-advanced-threat-protection.md).

## Endpoint Protection Workflow  
 Use the following diagram to help you understand the workflow to implement Endpoint Protection in your Configuration Manager hierarchy.  

 ![Endpoint Protection Workflow](../media/Endpoint-Protection-Workflow.gif)  
