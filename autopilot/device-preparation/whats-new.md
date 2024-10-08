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
ms.date: 09/18/2024
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

## Windows Autopilot Device Preparation Support in Azure China 21Vianet

Date added: *September 18, 2024*

As part of the 2409 Intune release, we're announcing support for Windows Autopilot Device Preparation policy in the [Azure China 21Vianet](/mem/intune/fundamentals/china) cloud. Customers with tenants located in China can now provision devices and manage through Microsoft Intune. For an overview, see [Overview of Windows Autopilot device preparation](overview.md). For a tutorial on how to set up Windows Autopilot device preparation, see [Windows Autopilot device preparation scenarios](tutorial/scenarios.md).

<!-- MAXADO-9313795 / INADO-28687730 -->

## enrollmentProfileName property is now populated with the Device preparation policy name

Date added: *September 13, 2024*

As part of the 2409 Intune release, the **enrollmentProfileName** property is now populated with the Device preparation policy name during Autopilot device preparation deployments. The Enrollment profile property of Intune and Microsoft Entra device objects are automatically populated with the name of the Device preparation policy that was applied to the device during provisioning. The **enrollmentProfileName** property enables admins to configure assignment filters and dynamic groups based on the **enrollmentProfileName** property for configurations post-enrollment.

<!-- INADO-28533819 -->

## Diagnostics logs automatically available in Windows Autopilot device preparation deployment status report

Date added: *August 23, 2024*

Admins can now download diagnostics logs for failed Autopilot device preparation deployments directly from the **Windows Autopilot device preparation deployment status** report. Logs are available for download in the **Device deployment details** when you select a failed deployment under the **Device** tab. Logs are automatically collected when an error occurs during deployment.

## Windows Autopilot device preparation deployment status report available in the Monitor tab under Enrollment

Date added: *August 21, 2024*

In addition to the [Devices | Monitor](reporting-monitoring.md#accessing-reports-and-near-real-time-monitoring) page, admins can now easily access the **Windows Autopilot device preparation deployment status** report from the **Monitor** tab in the **Devices | Enrollment** page starting with the Intune 2408 monthly release. The report can be found using the following steps:

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
