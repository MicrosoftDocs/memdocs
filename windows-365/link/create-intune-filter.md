---
# required metadata
title: Create an Intune filter for Windows 365 Link devices
titleSuffix:
description: Learn how to create an Intune filter for Windows 365 Link devices
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/19/2024
ms.topic: overview
ms.service: windows-365-link
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: sajelaci
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; intro-hub-or-landing
ms.collection:
- M365-identity-device-management
- tier2
---

# Create an Intune filter for Windows 365 Link devices

To help with [setting up your organization's environment to support Windows 365 Link](deployment-overview.md), you can use filters when assigning Intune polices. Such a filter can be used on any policy assignment to include or exclude Windows 365 Link devices.

To create a filter exclusively including Windows 365 Link devices:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) >**Tenant administration** > **Filters** > **Create** > **Managed devices**.
2. Provide a **Filter name**, like *Windows 365 Link devices*, and an optional **Description**.
3. For **Platform**, select **Windows 10 and later** > **Next**.
4. Select the following values:
    - **Property**: **operatingSystemSKU (Operating System SKU)**.
    - **Operator**: **Equals**.
    - **Value**: **WCPC (Widnows PC (210))**.
5. Select **Next**.
6. On the **Review + create** page, select **Create**.  

This new filter can now be used on various policy assignments to include or exclude Windows 365 Link devices for [supported Windows workloads](/mem/intune/fundamentals/filters-supported-workloads#windows-1011).

For more information, see [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](/mem/intune/fundamentals/filters).

<!-- ########################## -->
## Next steps

[Optimize enrollment restrictions to let Windows 365 Link devices enroll](enrollment-restrictions.md).
