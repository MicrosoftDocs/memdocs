---
title: What's new in Windows Autopilot device preparation
description: News and resources about the latest updates of Windows Autopilot device preparation. # RSS subscription is based on this description so don't change. If the description needs to change, update RSS URL in the Tip in the article.
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.reviewer: jubaptis
ms.date: 08/21/2024
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: conceptual
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation: What's new

> [!TIP]
>
> RSS can be used to notify when new features for Windows Autopilot device preparation are added to this page. For example, the following RSS link includes this article:
>
> ``` url
> https://learn.microsoft.com/api/search/rss?search=%22News+and+resources+about+the+latest+updates+of+Windows+Autopilot+device+preparation.%22&locale=en-us&%24filter=
> ```
>
> This example includes the `&locale=en-us` variable. The `locale` variable is required, but it can be changed to another supported locale. For example, `&locale=es-es`.
>
> For more information on using RSS for notifications, see [How to use the docs](/mem/use-docs#notifications) in the Intune documentation.

<!-- INADO-28533819 -->

## Windows Autopilot device preparation deployment status report available in the Monitor tab under Enrollment

Date added: *August 21, 2024*

In addition to the [Devices | Monitor](reporting-monitoring.md#accessing-reports-and-near-real-time-monitoring) page, admins can now easily access the **Windows Autopilot device preparation deployment status** report from the **Monitor** tab in the **Devices | Enrollment** page. The report can be found using the following steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Navigate to **Home** > **Devices** >  **Device onboarding | Enrollment**.
1. Select the **Monitor** tab in the **Devices | Enrollment** page.

## Corporate identifiers can now be used with Windows Autopilot device preparation

Date added: *July 8, 2024*

Customers who are blocking personal device enrollments can now use Windows Autopilot device preparation by pre-uploading the model, manufacturer, and serial number for all devices which will deploy with Autopilot device preparation. For more information, see [Add Windows corporate identifiers](/mem/intune/enrollment/corporate-identifiers-add#add-windows-corporate-identifiers).

## Additional role-based access control (RBAC) permissions for Managed apps and Mobile apps

Date added: *June 18, 2024*

We added additional RBAC permissions for **Managed apps** and **Mobile apps** for the Windows Autopilot device preparation administrator role. For more information, see [Required RBAC permissions](requirements.md?tabs=rbac#required-rbac-permissions).

## Initial release of Windows Autopilot device preparation

Date added: *June 3, 2024*

Windows Autopilot device preparation is generally available. For an overview, see [Overview of Windows Autopilot device preparation](overview.md). For a tutorial on how to set up Windows Autopilot device preparation, see [Windows Autopilot device preparation scenarios](tutorial/scenarios.md).
