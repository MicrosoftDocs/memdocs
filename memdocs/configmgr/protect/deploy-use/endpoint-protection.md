---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: Learn how to manage antimalware policies and Windows Firewall security for clients.
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

Endpoint Protection manages antimalware policies and Windows Firewall security for client computers in your Configuration Manager hierarchy.  

> [!IMPORTANT]  
>  You must be licensed to use Endpoint Protection to manage clients in your Configuration Manager hierarchy.  

 When you use Endpoint Protection with Configuration Manager, you have the following benefits:  

-   Configure antimalware policies, Windows Firewall settings, and manage Microsoft Defender Advanced Threat Protection to selected groups of computers  
-   Use Configuration Manager software updates to download the latest antimalware definition files to keep client computers up-to-date  
-   Send email notifications, use in-console monitoring, and view reports. These actions inform administrative users when malware is detected on client computers.  

Beginning with Windows 10 and Windows Server 2016 computers, Windows Defender is already installed. For these operating systems, a management client for Windows Defender is installed when the Configuration Manager client installs. On Windows 8.1 and earlier computers, the Endpoint Protection client is installed with the Configuration Manager client. Windows Defender and the Endpoint Protection client have the following capabilities:  

-   Malware and spyware detection and remediation  
-   Rootkit detection and remediation  
-   Critical vulnerability assessment and automatic definition and engine updates  
-   Network vulnerability detection through Network Inspection System  
-   Integration with Cloud Protection Service to report malware to Microsoft. When you join this service, the Endpoint Protection client or Windows Defender downloads the latest definitions from the Malware Protection Center when unidentified malware is detected on a computer.  

> [!NOTE]  
>  The Endpoint Protection client can be installed on a server that runs Hyper-V and on guest virtual machines with supported operating systems. To prevent excessive CPU usage, Endpoint Protection actions have a built-in randomized delay so that protection services do not run simultaneously.  

 In addition, you manage Windows Firewall settings with Endpoint Protection in the Configuration Manager console.  

 [Example scenario: Using System Center Endpoint Protection to protect computers from malware](scenarios-endpoint-protection.md) Endpoint Protection and the Windows Firewall.  


## Managing Malware with Endpoint Protection  
 Endpoint Protection in Configuration Manager allows you to create antimalware policies that contain settings for Endpoint Protection client configurations. Deploy these antimalware policies to client computers. Then monitor compliance in the **Endpoint Protection Status** node under **Security** in the **Monitoring** workspace. Also use Endpoint Protection reports in the **Reporting** node.  

 Additional information:  

-   [How to create and deploy antimalware policies for Endpoint Protection](endpoint-antimalware-policies.md) - Create, deploy, and monitor antimalware policies with a list of the settings that you can configure  

-   [How to monitor Endpoint Protection](monitor-endpoint-protection.md) - Monitoring activity reports, infected client computers, and more.  

-   [How to manage antimalware policies and firewall settings for Endpoint Protection](endpoint-antimalware-firewall.md) - Remediate malware found on client computers  

-   [Log files for Endpoint Protection](../../core/plan-design/hierarchy/log-files.md#BKMK_EPLog)  


## Managing Windows Firewall with Endpoint Protection  
 Endpoint Protection in Configuration Manager provides basic management of the Windows Firewall on client computers. For each network profile, you can configure the following settings:  

-   Enable or disable the Windows Firewall.  

-   Block incoming connections, including those in the list of allowed programs.  

-   Notify the user when Windows Firewall blocks a new program.  

> [!NOTE]  
>  Endpoint Protection supports managing the Windows Firewall only.  


 For more information, see [How to create and deploy Windows Firewall policies for Endpoint Protection](create-windows-firewall-policies.md).  


## Microsoft Defender Advanced Threat Protection

Endpoint Protection manages and monitors Microsoft Defender Advanced Threat Protection (ATP), formerly known as Windows Defender ATP. The Microsoft Defender ATP service helps enterprises detect, investigate, and respond to advanced attacks on the corporate network. For more information, see [Microsoft Defender Advanced Threat Protection](windows-defender-advanced-threat-protection.md).

## Endpoint Protection Workflow  
 Use the following diagram to help you understand the workflow to implement Endpoint Protection in your Configuration Manager hierarchy.  

 ![Endpoint Protection Workflow](../media/Endpoint-Protection-Workflow.gif)  



## Endpoint Protection Client for Mac Computers and Linux Servers  

> [!Important]  
> Support for System Center Endpoint Protection (SCEP) for Mac and Linux (all versions) ends on December 31, 2018. Availability of new virus definitions for SCEP for Mac and SCEP for Linux may be discontinued after the end of support. For more information, see [End of support blog post](https://go.microsoft.com/fwlink/?linkid=870182).  

 System Center Endpoint Protection includes an Endpoint Protection client for Linux and for Mac computers. These clients aren't supplied with Configuration Manager. Download the following products from the [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx):  

-   System Center Endpoint Protection for Mac  

-   System Center Endpoint Protection for Linux  


> [!Note]  
>  You must be a Microsoft Volume License customer to download the Endpoint Protection installation files for Linux and the Mac.  

 These products can't be managed from the Configuration Manager console. A System Center Operations Manager management pack is supplied with the installation files, which allows you to manage the client for Linux.  

### How to get the Endpoint Protection client for Mac computers and Linux servers

Use the following steps to download the image file containing the Endpoint Protection client software and documentation for Mac computers and Linux servers.
1. Sign in to the [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Select the **Downloads and Keys** tab at the top of the website.
3. Filter on product **System Center Endpoint Protection (current branch)**.
4. Click link to **Download**
5. Click **Continue**. You should see several files, including one named: **System Center Endpoint Protection (current branch - version 1606) for Linux OS and Macintosh OS Multilanguage 32/64 bit 1878 MB ISO**.
6. To download the file, click the arrow icon. The file name is **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050.ISO**.

The January 2018 update (X21-67050) includes the following versions:

- System Center Endpoint Protection for Mac 4.5.32.0 (support for macOS 10.13 High Sierra)
- System Center Endpoint Protection for Linux 4.5.20.0 

  For more information about how to install and manage the Endpoint Protection clients for Linux and Mac computers, use the documentation that accompanies these products. This product documentation is in the **Documentation** folder of the .ISO file.
