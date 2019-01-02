---
title: Hybrid MDM with Microsoft Intune
titleSuffix: Configuration Manager
description: Learn about hybrid mobile device management (MDM) with Configuration Manager and Microsoft Intune.
ms.date: 11/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Hybrid MDM with Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

> [!Important]  
> As of August 14, 2018, hybrid mobile device management is a [deprecated feature](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).
> <!--Intune feature 2683117-->  
> Since launching on Azure over a year ago, Intune has added hundreds of new customer-requested and market-leading service capabilities. It now offers far more capabilities than those offered through hybrid mobile device management (MDM). Intune on Azure provides a more integrated, streamlined administrative experience for your enterprise mobility needs.
> 
> As a result, most customers choose Intune on Azure over hybrid MDM. The number of customers using hybrid MDM continues to decrease as more customers move to the cloud. Therefore, on September 1, 2019, Microsoft will retire the hybrid MDM service offering. Please plan your [migration to Intune on Azure](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) for your MDM needs. 
> 
> This change doesn't affect on-premises Configuration Manager or [co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview). If you're unsure whether you're using hybrid MDM, go to the **Administration** workspace of the Configuration Manager console, expand **Cloud Services**, and click **Microsoft Intune Subscriptions**. If you have a Microsoft Intune subscription set up, your tenant is configured for hybrid MDM.
> 
> **How does this affect me?**
> 
> - Microsoft will support your hybrid MDM usage for the next year. The feature will continue to receive major bug fixes. Microsoft will support existing functionality on new OS versions, such as enrollment on iOS 12. There will be no new features for hybrid MDM.  
> 
> - If you migrate to Intune on Azure before the end of the hybrid MDM offering, there should be no end user impact.  
> 
> - Licensing remains the same. Intune on Azure licenses are included with hybrid MDM.  
> 
> - The conditional access and on-premises MDM features in Configuration Manager aren't deprecated. Upcoming changes to Configuration Manager will allow these features to function without hybrid MDM. 
> 
> - On September 1, 2019, any remaining hybrid MDM devices will no longer receive policy, apps, or security updates.  
> 
> **What do I need to do to prepare for this change?**
> 
> - Start planning your migration for MDM from the ConfigMgr console to Azure. Many customers, including Microsoft IT, have gone through this process. For more information, see this [Microsoft case study](https://aka.ms/Intune_MSFT).  
> 
> - Review the following tools and documentation to simplify the process of moving from hybrid MDM to Intune on Azure:  
>     - [Import Configuration Manager data to Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data)  
>     - [Migrate hybrid MDM users and devices to Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  
> 
> - Contact your partner of record or FastTrack for assistance. [FastTrack for Microsoft 365](https://aka.ms/hybrid_fasttrack) can assist in your migration from hybrid MDM to Intune on Azure. 
> 
> For more information, see [the Intune support blog post](https://aka.ms/hybrid_notification).



With the hybrid mobile device management (MDM) feature of Configuration Manager, manage iOS, Windows, and Android devices. All management tasks are handled from the Configuration Manager console where you perform the rest of your management tasks seamlessly integrated with Microsoft Intune's online service over the internet. Use Configuration Manager to let users access company resources on their devices in a secure, managed way. By using device management, you protect company data while letting users enroll their personal or company-owned devices to access company data. 

This article assumes that you use Configuration Manager to manage computers. It also assumes that you're interested in extending the Configuration Manager console with Intune to manage mobile devices. 



## Capabilities

Hybrid MDM supports the following management capabilities on devices:

-   Retire and wipe devices  

-   Configure compliance settings such as passwords, security, roaming, encryption, and wireless communication  

-   Deploy line-of-business (LOB) apps to devices  

-   Deploy apps to devices that connect to Windows Store, Windows Phone Store, App Store, or Google Play  

-   Collect hardware inventory  

-   Collect software inventory by using built-in reports  

To read about what new features are available for hybrid MDM, see [What's new in hybrid mobile device management](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management).



## Hybrid MDM enrollment

To bring devices into hybrid management, those devices must be enrolled with the service. How devices enroll devices depends on the device type, ownership, and the level of management needed.

- **"Bring your own device" (BYOD)**: Users enroll their personal phones, tablets, or PCs  

- **Corporate-owned device (COD)**: Enable management scenarios like remote wipe, shared devices, or user affinity for a device  

- If you use [Exchange ActiveSync](/sccm/mdm/plan-design/device-enrollment-methods#mobile-device-management-with-exchange-activesync-and-configuration-manager), either on-premises or hosted in the cloud, you can enable simple Intune management without enrollment. Windows PCs can also be managed using [Intune client software](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
