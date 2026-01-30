---
title: What's new in Windows Autopilot device preparation
description: News and resources about the latest updates of Windows Autopilot device preparation. # RSS subscription is based on this description so don't change. If the description needs to change, update RSS URL in the Tip in the article.
ms.date: 11/21/2025
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: whats-new
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

## Windows Autopilot device preparation in automatic mode for Windows 365 Enterprise, Windows 365 Frontline in dedicated mode, and Windows 365 Cloud Apps is in public preview  

Date added: *November 21, 2025*  

Use Windows Autopilot device preparation policies in automatic flow to provision Windows 365 Enterprise, Windows 365 Frontline in dedicated mode, and Windows 365 Cloud Apps. The policy can be included in the Cloud PC provisioning policy and applies immediately after the Cloud PCs are created to deliver apps and scripts to the device before a user logs in. You can monitor deployment status in the [Windows Autopilot device preparation deployment report](reporting-monitoring.md). For a tutorial, see [Step by step tutorial for Windows Autopilot device preparation in automatic mode for Windows 365 in Intune](tutorial/automatic/automatic-workflow.md).  

For related information, see the following articles:  
- [Create provisioning policies for Windows 365](/windows-365/enterprise/create-provisioning-policy)  
- [Windows 365 Cloud Apps](/windows-365/enterprise/cloud-apps)  
- [Use Autopilot device preparation with Cloud PCs](/windows-365/enterprise/autopilot-device-preparation) 

## Installation of monthly security update releases during Windows Autopilot device preparation

Date added: *September 3, 2025*<br>
Date updated: *September 9, 2025*

> [!IMPORTANT]
>
> As of September 9, 2025, this capability is delayed to help ensure delivery of the best possible experience. Automatic installation of monthly security update isn't available yet. This post will be updated with a revised timeline as soon as it's available.

[Monthly security update releases](/windows/deployment/update/release-cycle#monthly-security-update-release), also known as Windows quality updates, are installed during a Windows Autopilot device preparation deployment as part of the Windows out-of-box experience (OOBE). The monthly security update releases are installed after the device preparation page completes. These updates can't be disabled for Windows Autopilot device preparation deployments. Installation of monthly security update releases during OOBE normally adds 20-40 minutes to the provisioning process. Installation of monthly security update releases also might require restarts.

More details regarding automatic installation of monthly security update releases can be found in the article [Install Windows monthly security update releases](/intune/intune-service/enrollment/windows-enrollment-status#windows-monthly-security-update-release-details). However, this article is in regards to using the Enrollment Status Page (ESP) with Windows Autopilot. Windows Autopilot device preparation doesn't use the ESP, so the **Install Windows quality updates (might restart the device)** setting mentioned in this article isn't applicable to Windows Autopilot device preparation.

For more information, see [Get ready for Windows quality updates out of the box](https://techcommunity.microsoft.com/blog/windows-itpro-blog/get-ready-for-windows-quality-updates-out-of-the-box/4434498).  

## Deliver Enterprise App Catalog (EAM) apps during Autopilot device preparation

Date added: *June 26, 2025*

Autopilot device preparation now supports Enterprise App Catalog apps. Microsoft Intune Enterprise App Management enables IT admins to easily manage applications from the Enterprise App Catalog. With Intune's 2506 release, you can now select apps from the Enterprise App Catalog in the device preparation policy. This allows you to ensure those apps are delivered before the user can access the desktop.

For related information, see [Add an Enterprise App Catalog app to Microsoft Intune](/intune/intune-service/apps/apps-add-enterprise-app).

## Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode is in public preview

Date added: *April 2, 2025*

We've introduced a new flow for Windows Autopilot device preparation which can be used to provision [Windows 365 Frontline in shared mode](/windows-365/enterprise/introduction-windows-365-frontline). Admins can now choose **Automatic** when creating a Windows Autopilot device preparation policy to prepare a policy for Cloud PCs. The policy can then be included in the Cloud PC provisioning policy to ensure the policy is assigned to all Cloud PCs after they're created. The new Automatic policy allows admins to select up to 10 apps and up to 10 scripts which are delivered before a user accesses the Cloud PC. Deployments can then be monitored in the [Windows Autopilot device preparation deployment report](reporting-monitoring.md).

With the new mode, admins can make sure their Cloud PCs are secured with required software and scripts before the end user logs in!

For a tutorial on Windows Autopilot device preparation in automatic mode for Windows 365, see [Step by step tutorial for Windows Autopilot device preparation in automatic mode for Windows 365 in Intune](tutorial/automatic/automatic-workflow.md).

For more information, see the following articles:

- [Windows 365 Frontline Cloud PC in shared mode - Quick Start Guide](https://techcommunity.microsoft.com/discussions/windows365discussions/windows-365-frontline-cloud-pc-in-shared-mode-%E2%80%93-quick-start-guide/4399905).
- [Use automated Autopilot device preparation with Windows 365 Frontline Cloud PCs in shared mode (preview)](/windows-365/enterprise/autopilot-device-preparation).

## Diagnostics logs automatically available in Windows Autopilot device preparation deployment status report

Date added: *October 9, 2024*

Admins can now download diagnostics logs for failed Autopilot device preparation deployments directly from the **Windows Autopilot device preparation deployment status** report. Logs are available for download in the **Device deployment details** when you select a failed deployment under the **Device** tab. Logs are automatically collected when an error occurs during deployment.

## Windows Autopilot Device Preparation Support in Intune operated by 21Vianet in China

Date added: *September 18, 2024*

As part of the 2409 Intune release, we're announcing support for Windows Autopilot Device Preparation policy in [Intune operated by 21Vianet in China](/mem/intune-service/fundamentals/china) cloud. Customers with tenants located in China can now provision devices and manage through Microsoft Intune. For an overview, see [Overview of Windows Autopilot device preparation](overview.md). For a tutorial on how to set up Windows Autopilot device preparation, see [Windows Autopilot device preparation scenarios](tutorial/scenarios.md).

<!-- MAXADO-9313795 / INADO-28687730 -->

## enrollmentProfileName property is now populated with the Device preparation policy name

Date added: *September 13, 2024*

As part of the 2409 Intune release, the **enrollmentProfileName** property is now populated with the Device preparation policy name during Autopilot device preparation deployments. The Enrollment profile property of Intune and Microsoft Entra device objects are automatically populated with the name of the Device preparation policy that was applied to the device during provisioning. The **enrollmentProfileName** property enables admins to configure assignment filters and dynamic groups based on the **enrollmentProfileName** property for configurations post-enrollment.

<!-- INADO-28533819 -->

## Windows Autopilot device preparation deployment status report available in the Monitor tab under Enrollment

Date added: *August 21, 2024*

In addition to the [Devices | Monitor](reporting-monitoring.md#accessing-reports-and-near-real-time-monitoring) page, admins can now easily access the **Windows Autopilot device preparation deployment status** report from the **Monitor** tab in the **Devices | Enrollment** page. The report can be found using the following steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Navigate to **Home** > **Devices** >  **Device onboarding | Enrollment**.
1. Select the **Monitor** tab in the **Devices | Enrollment** page.

## Corporate identifiers can now be used with Windows Autopilot device preparation

Date added: *July 8, 2024*

Customers who are blocking personal device enrollments can now use Windows Autopilot device preparation by pre-uploading the model, manufacturer, and serial number for all devices which deploys with Windows Autopilot device preparation. For more information, see [Add Windows corporate identifiers](/mem/intune-service/enrollment/corporate-identifiers-add#add-windows-corporate-identifiers).

## Additional role-based access control (RBAC) permissions for Managed apps and Mobile apps

Date added: *June 18, 2024*

We added additional RBAC permissions for **Managed apps** and **Mobile apps** for the Windows Autopilot device preparation administrator role. For more information, see [Required RBAC permissions](requirements.md?tabs=rbac#required-rbac-permissions).

## Initial release of Windows Autopilot device preparation

Date added: *June 3, 2024*

Windows Autopilot device preparation is generally available. For an overview, see [Overview of Windows Autopilot device preparation](overview.md). For a tutorial on how to set up Windows Autopilot device preparation, see [Windows Autopilot device preparation scenarios](tutorial/scenarios.md).

## Related content

- [What's new in Windows Autopilot](../whats-new.md).
- [What's new in Microsoft Intune](/mem/intune-service/fundamentals/whats-new).
- [What's new in Windows client](/windows/whats-new/).
