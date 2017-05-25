---
title: "Endpoint Protection | Microsoft Docs"
description: "Learn how to manage antimalware policies and Windows Firewall security for client computers in your Configuration Manager hierarchy."
ms.custom: na
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
caps.latest.revision: 11
author: NathBarn
ms.author: nathbarn
manager: angrobe

---
# Endpoint Protection

*Applies to: System Center Configuration Manager (Current Branch)*

Endpoint Protection in System Center Configuration Manager lets you to manage antimalware policies and Windows Firewall security for client computers in your Configuration Manager hierarchy.  

> [!IMPORTANT]  
>  You must be licensed to use Endpoint Protection to manage clients in your Configuration Manager hierarchy.  

 When you use Endpoint Protection with Configuration Manager, you have the following benefits:  

-   Configure antimalware policies, Windows Firewall settings, and manage Windows Defender Advanced Threat Protection to selected groups of computers  
-   Use Configuration Manager software updates to download the latest antimalware definition files to keep client computers up-to-date  
-   Send email notifications, use in-console monitoring, and view reports to keep administrative users informed when malware is detected on client computers  

Beginning with Windows 10 and Windows Server 2016 computers, Windows Defender is already installed. For these operating systems, a management client for Windows Defender is installed when the Configuration Manager client installs. On Windows 8.1 and earlier computers, the Endpoint Protection client is installed with the Configuration Manager client. Windows Defender and the Endpoint Protection client have the following capabilities:  

-   Malware and spyware detection and remediation  
-   Rootkit detection and remediation  
-   Critical vulnerability assessment and automatic definition and engine updates  
-   Network vulnerability detection through Network Inspection System  
-   Integration with Cloud Protection Service to report malware to Microsoft. When you join this service, the Endpoint Protection client or Windows Defender can download the latest definitions from the Malware Protection Center when unidentified malware is detected on a computer.  

> [!NOTE]  
>  The Endpoint Protection client can be installed on a server that runs Hyper-V and on guest virtual machines with supported operating systems. To prevent excessive CPU usage, Endpoint Protection actions have a built-in randomized delay so that protection services do not run simultaneously.  

 In addition, Endpoint Protection in Configuration Manager lets you to manage Windows Firewall settings in the Configuration Manager console.  

 [Example scenario: Using System Center Endpoint Protection to protect computers from malware in System Center Configuration Manager](scenarios-endpoint-protection.md) Endpoint Protection and the Windows Firewall.  


## Managing Malware with Endpoint Protection  
 Endpoint Protection in Configuration Manager allows you to create antimalware policies that contain settings for Endpoint Protection client configurations. You can then deploy these antimalware policies to client computers and monitor them in the **Endpoint Protection Status** node under **Security** in the **Monitoring** workspace, or by using Configuration Manager reports.  

 Additional information:  

-   [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md) - Create, deploy, and monitor antimalware policies with a list of the settings that you can configure  

-   [How to monitor Endpoint Protection in System Center Configuration Manager](monitor-endpoint-protection.md) - Monitoring activity reports, infected client computers, and more.  

-   [How to manage antimalware policies and firewall settings for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-firewall.md) - Remediate malware found on client computers  


## Managing Windows Firewall with Endpoint Protection  
 Endpoint Protection in Configuration Manager provides basic management of the Windows Firewall on client computers. For each network profile, you can configure the following settings:  

-   Enable or disable the Windows Firewall.  

-   Block incoming connections, including those in the list of allowed programs.  

-   Notify the user when Windows Firewall blocks a new program.  

> [!NOTE]  
>  Endpoint Protection supports managing the Windows Firewall only.  


 For more information about how to create and deploy Windows Firewall policies for Endpoint Protection, see [How to create and deploy Windows Firewall policies for Endpoint Protection in System Center Configuration Manager](create-windows-firewall-policies.md).  


## Windows Defender Advanced Threat Protection

Starting with version 1606 of Configuration Manager (current branch), Endpoint Protection can help manage and monitor Windows Defender Advanced Threat Protection (ATP). Windows Defender ATP is a new service that will help enterprises to detect, investigate, and respond to advanced attacks on their networks. See [Windows Defender Advanced Threat Protection](windows-defender-advanced-threat-protection.md).

## Endpoint Protection Workflow  
 Use the following diagram to help you understand the workflow to implement Endpoint Protection in your Configuration Manager hierarchy.  

 ![Endpoint Protection Workflow](../media/Endpoint-Protection-Workflow.gif)  

## Endpoint Protection Client for Mac Computers and Linux Servers  
 System Center Endpoint Protection includes an Endpoint Protection client for Linux and for Mac computers. These clients are not supplied with Configuration Manager; instead, you must download the following products from the [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

-   System Center 2012 Endpoint Protection for the Mac  

-   System Center 2012 Endpoint Protection for Linux  


> [!IMPORTANT]  
>  You must be a Microsoft Volume License customer to download the Endpoint Protection installation files for Linux and the Mac.  

 These products cannot be managed from the Configuration Manager console. However, a System Center Operations Manager management pack is supplied with the installation files, which allows you to manage the client for Linux by using Operations Manager.  

### How to get the Endpoint Protection client for Mac computers and Linux servers

Use the following steps to download the image file containing the Endpoint Protection client software and documentation for Mac computers and Linux servers.
1. Login to the [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Select the **Downloads and Keys** tab at the top of the website.
3. Filter on product **System Center Endpoint Protection (current branch)**.
4. Click link to **Download**
5. Click **Continue**. You should see several files, including one named: **System Center Endpoint Protection (current branch - version 1606) for Linux OS and Macintosh OS Multilanguage	32/64 bit	1507 MB	ISO**.
6. Click the arrow icon to download the file. The file name is **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_EptProt_Lin_Mac_MLF_X21-30777.ISO**.

 For more information about how to install and manage the Endpoint Protection clients for Linux and Mac computers, use the documentation that accompanies these products, which is located in the **Documentation** folder.
