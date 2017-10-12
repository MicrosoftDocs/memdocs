---
title: Plan for Endpoint Protection
titleSuffix: "Configuration Manager"
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
caps.latest.revision: 16
author: NathBarnms.author: nathbarn
manager: angrobe

---
# Planning for Endpoint Protection in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*

Endpoint Protection in System Center Configuration Manager lets you to manage antimalware policies and Windows Firewall security for client computers in your Configuration Manager hierarchy.  

> [!IMPORTANT]  
>  You must be licensed to use Endpoint Protection to manage clients in your Configuration Manager hierarchy.  

When you use Endpoint Protection with Configuration Manager, you have the following benefits:  

-   Configure antimalware policies, Windows Firewall settings, and manage Windows Defender Advanced Threat Protection to selected groups of computers  

-   Use Configuration Manager software updates to download the latest antimalware definition files to keep client computers up-to-date  

-   Send email notifications, use in-console monitoring, and view reports to keep administrative users informed when malware is detected on client computers  

Windows 10 computers don't require any additional client for endpoint protection management. On Windows 8.1 and earlier computers, Endpoint Protection installs its own client in addition to the Configuration Manager client. The Endpoint Protection client has the following capabilities:  

-   Malware and spyware detection and remediation  

-   Rootkit detection and remediation  

-   Critical vulnerability assessment and automatic definition and engine updates  

-   Network vulnerability detection through Network Inspection System  

-   Integration with Cloud Protection Service to report malware to Microsoft. When you join this service, Windows Defender or the Endpoint Protection client can download the latest definitions from the Malware Protection Center when unidentified malware is detected on a computer.  

> [!NOTE]  
>  The Endpoint Protection client can be installed on a server that runs Hyper-V and on guest virtual machines with supported operating systems. To prevent excessive CPU usage, Endpoint Protection actions have a built-in, randomized delay so that services do not run simultaneously.  

  In addition, Endpoint Protection in Configuration Manager lets you to manage Windows Firewall settings in the Configuration Manager console.  

 [Example scenario: Using System Center Endpoint Protection to protect computers from malware in System Center Configuration Manager](../deploy-use/scenarios-endpoint-protection.md) shows how you might configure and manage Endpoint Protection and the Windows Firewall.  

## Managing Malware with Endpoint Protection  

Endpoint Protection in Configuration Manager allows you to create antimalware policies that contain settings for Endpoint Protection client configurations. You can then deploy these antimalware policies to client computers and monitor them in the **Endpoint Protection Status** node in the **Monitoring** workspace, or by using Configuration Manager reports.  

 Additional information:  

-   [Create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../deploy-use/endpoint-antimalware-policies.md) - Create, deploy, and monitor antimalware policies with a list of the settings that you can configure  

-   [Monitor Endpoint Protection in System Center Configuration Manager](../deploy-use/monitor-endpoint-protection.md) - Monitoring activity reports, infected client computers, and more.   

-   [Manage antimalware policies and firewall settings for Endpoint Protection in System Center Configuration Manager](../deploy-use/endpoint-antimalware-firewall.md) - You can change policy priority for [antimalware](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies) or [firewall](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies), [remediate malware found on client computers](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware), and other tasks

## Managing Windows Firewall with Endpoint Protection  
 Endpoint Protection in Configuration Manager provides basic management of the Windows Firewall on client computers. For each network profile, you can configure the following settings:  

-   Enable or disable the Windows Firewall.  

-   Block incoming connections, including those in the list of allowed programs.  

-   Notify the user when Windows Firewall blocks a new program.  

> [!NOTE]  
>  Endpoint Protection supports managing the Windows Firewall only.  

  For more information about how to create and deploy Windows Firewall policies for Endpoint Protection, see [How to create and deploy Windows Firewall policies for Endpoint Protection in System Center Configuration Manager](../deploy-use/create-windows-firewall-policies.md).  

## Windows Defender Advanced Threat Protection

Starting with version 1606 of Configuration Manager (current branch), Endpoint Protection can help manage and monitor Windows Defender Advanced Threat Protection (ATP). Windows Defender ATP is a new service that will help enterprises to detect, investigate, and respond to advanced attacks on their networks. See [Windows Defender Advanced Threat Protection](../deploy-use/windows-defender-advanced-threat-protection.md).

## Endpoint Protection Workflow  
 Use the following diagram to help you understand the workflow to implement Endpoint Protection in your Configuration Manager hierarchy.  

 ![Endpoint Protection Workflow](../media/Endpoint-Protection-Workflow.gif)

## Endpoint Protection Client for Mac Computers and Linux Servers  
 System Center includes an Endpoint Protection client for Linux and for Mac computers. These clients are not supplied with Configuration Manager; instead, you must download the following products from the [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

> [!IMPORTANT]  
>  You must be a Microsoft Volume License customer to download the Endpoint Protection installation files for Linux and the Mac.  

 These products cannot be managed from the Configuration Manager console. However, a System Center Operations Manager management pack is supplied with the installation files, which allows you to manage the client for Linux by using Operations Manager.  

 For more information about how to install and manage the Endpoint Protection clients for Linux and Mac computers, use the documentation that accompanies these products, which is located in the **Documentation** folder.

## Best Practices for Endpoint Protection in Configuration Manager  
 Use the following best practices for Endpoint Protection in System Center 2012 Configuration Manager.  

### Configure custom client settings for Endpoint Protection  
 When you configure client settings for Endpoint Protection, do not use the default client settings because they apply settings to all computers in your hierarchy. Instead, configure custom client settings and assign these settings to collections of computers in your hierarchy.  

 When you configure custom client settings, you can do the following:  

-   Customize antimalware and security settings for different parts of your organization.  
-   Test the effects of running Endpoint Protection on a small group of computers before you deploy it to the entire hierarchy.  
-   Add more clients to the collection over time to phase your deployment of the Endpoint Protection client.  

### Distributing definition updates by using software updates  
 If you are using Configuration Manager software updates to distribute definition updates, consider placing definition updates in a package that does not contain other software updates. This keeps the size of the definition update package smaller which allows it to replicate to distribution points more quickly.
