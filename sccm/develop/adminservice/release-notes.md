---
title: Admin service release notes
titleSuffix: Configuration Manager
description: Information about changes to the administration service with each Configuration Manager release
ms.date: 03/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0a3dea00-39c9-49f2-ba07-19b70994a2b5
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Administration service release notes

*Applies to: Configuration Manager (current branch)*

## Changes in version 2002

<!-- 5728365 -->
Starting in version 2002, the administration service automatically uses the site's self-signed certificate. This change helps reduce the friction for easier use of the administration service. The site always generates this certificate. Now the administration service ignores the Enhanced HTTP site setting, as it always uses the site's certificate even if no other site system is using Enhanced HTTP. For more information, see <!-- need link -->

## Changes in version 1910
<!-- 4651 -->

- The WMI route now supports static WMI methods. For example:

    ```rest
    Verb: Post
    URI: https://<ProviderFQDN>/AdminService/wmi/SMS_Admin.GetAdminExtendedData
    Body: {"Type":1}
    ```

- The Configuration Manager console now sends console connection health information through the administration service.

- Use OData query options **startswith** and **endswith** on WMI route. For example: `https://<ProviderFQDN>/AdminService/wmi/SMS_Collection?$filter=startswith(Name,'All') eq true`

- Use the Power BI Desktop feature to get data from an **OData feed**. You can then see all WMI entities and their objects in Power BI Desktop to create custom reports.

- The **v1** route exposes the **Device** class. For example: `https://<ProviderFQDN>/AdminService/v1/Device`

> [!TIP]
> For more examples, see [How to use the administration service](/configmgr/develop/adminservice/usage).

### Classes available to the WMI route in version 1910

- SMS_ReplicationGroup
- SMS_BoundaryGroup
- SMS_G_System_DISK
- SMS_G_System_LOGICAL_DISK
- SMS_G_System_OPERATING_SYSTEM
- SMS_G_System_PARTITION
- SMS_G_System_PHYSICAL_DISK
- SMS_G_System_PHYSICAL_MEMORY
- SMS_G_System_X86_PC_MEMORY
- SMS_DistributionDPStatus
- SMS_WinPEOptionalComponentInfo
- SMS_OSDeploymentKitWinPEOptionalComponent
- SMS_WinPEOptionalComponentInBootImage
- SMS_G_System_AdvancedThreatProtectionHealthStatus
- SMS_SearchFolder
- SMS_DPStatusDetails
