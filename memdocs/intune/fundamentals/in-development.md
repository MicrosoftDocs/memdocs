---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 10/1/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals

# optional metadata

#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# In development for Microsoft Intune

To help in your readiness and planning, this page lists Intune UI updates and features that are in development but not yet released. In addition to the information on this page:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in Office message center.
- When a feature enters production, whether it's a preview or generally available, the feature description will move from this page to [What's new](whats-new.md).
- This page and the [What's new](whats-new.md) page are updated periodically. Check back for more updates.
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

> [!NOTE]
> This page reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This page doesn't describe all features in development.

**RSS feed**: Find out when this page is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**This article was last updated on the date listed under the title above.**

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control

-->

<!-- ***********************************************-->
## App management

### Export underlying discovered apps list data<!-- 9370255  -->

In addition to exporting the summarized discovered apps list data, you'll also be able export the more extensive underlying data. The current summarized export experience provides summarized aggregate data, however the new experience will also provide the raw data. The raw data export will give you the entire dataset, which is used to create the summarized aggregate report. The raw data will be a list of every device and each app discovered for that device. This functionality is being added to the Intune console to replace the Intune Data Warehouse Application Inventories dataset, which will be removed in an upcoming Intune service release. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **Monitor** > **Discovered apps** > **Export** to display the export options. For related information, see [Intune discovered apps](../apps/app-discovered-apps.md) and [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

### Unified delivery of Azure AD Enterprise and Office Online applications in the Android Company Portal<!-- 1817862  -->

Last year, we announced [Unified delivery of Azure AD Enterprise and Office Online applications in the Company Portal website](../fundamentals/whats-new-archive.md#unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal). This feature will be supported for users who get their apps directly from the Android Company Portal. On the **Customization** pane of Intune, select to **Hide** or **Show** both **Azure AD Enterprise applications** and **Office Online applications** in the Company Portal. Each end user will see their entire application catalog from the chosen Microsoft service. By default, each additional app source will be set to **Hide**. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Customization** to find this configuration setting. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

### Manage iOS/iPadOS Universal Links using App Protection Policies<!-- 2850827  -->

You'll be able to configure both Managed Universal Links and Universal Link Exemptions for iOS/IPadOS apps via Application Protection Policy (APP) settings.  Managed Universal Links will allow http/s links to open into the registered APP protected application instead of the protected browser.  Universal Link Exemptions allow http/s links to open into the registered unprotected application instead of the protected browser. For related information, see [Universal Links support](../apps/app-protection-policy.md#universal-links-support).

### Block or allow personal apps for Android Enterprise corporate-owned work profile devices<!-- 8925033  -->

In device configuration, you'll be able to create a list of personal apps that will be blocked or allowed on the device. You'll have the choice to leave the setting as not configured, or create a list of blocked or allowed apps in the personal profile. This setting will be available in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Android** > **Configuration profiles** > **Create profile**. For information about Android Enterprise corporate-owned work profile device settings, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

### Connected app support for Android personally-owned and corporate-owned work profiles<!-- 9206112  -->

You'll be able to allow users to turn on Connected apps experiences for supported apps. This app configuration setting will enable users to connect the app information across the work and personal app instances. For example, connecting a calendar app can show work and personal events together. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Apps** > **App configuration policies** > **Add** > **Managed devices**.

<!-- ***********************************************-->
## Device configuration

### Use filters to assign Endpoint analytics proactive remediations scripts and Endpoint Security policies in Endpoint Manager admin center - public preview<!-- 7566953 7591178  -->

In the Endpoint Manager admin center, you can create filters, and then use these filters when assigning apps and policies. You'll be able to use filters to assign the following policies:

- [Endpoint analytics proactive remediations Windows PowerShell scripts](../../analytics/proactive-remediations.md) (**Reports** > **Endpoint analytics** > **Proactive remediations**)
- [Endpoint Security policies](../protect/endpoint-security-policy.md), including Account protection, Antivirus, Attack surface reduction, and more.

For more information on filters, see [Use filters (preview) when assigning your apps, policies, and profiles](filters.md).

Applies to:

- macOS
- Windows 10 and newer

### Manage Windows 10 security updates for Windows 10 Enterprise multi-session VMs<!-- 8682461  -->

You’ll soon be able to use the Settings Catalog to deploy Windows 10 quality updates to Windows 10 Enterprise multi-session virtual machines. (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 or later** > **Settings catalog**)

To find the relevant settings, in the Settings Catalog, [use the Settings filter to focus on the OS type of Enterprise multi-session](../fundamentals/azure-virtual-desktop-multi-session.md#to-configure-policies). Then select the Windows Update for Business category where you’ll now see only those settings that are supported for multi-session VMs.

The Windows Update settings for quality updates that you’ll soon be able to use with multi-session VMs include:

- Active Hours End
- Active Hours Max Range
- Active Hours Start
- Block "Pause Updates" ability
- Configure Deadline Grace Period
- Defer Quality Updates Period (Days)
- Pause Quality Updates Start Time
- Quality Update Deadline Period (Days)

<!-- ***********************************************-->
## Device enrollment

### Four new Shared iPad enrollment settings<!--9684925 -->

Four new settings will be available for Shared iPad devices. These settings get applied at the time of Automated Device Enrollment.

- For iPadOS 14.5 and later in Shared iPad mode:
  - Require Shared iPad temporary setting only: When set to Yes, users only see the Guest Welcome pane, and can only sign in as a guest user. Users can't sign in with a Managed Apple ID.
  - Maximum seconds of inactivity until temporary session logs out: If there isn't any activity after the value you enter, then the temporary session automatically signs out.
  - Maximum seconds of inactivity until user session logs out: If there isn't any activity after the value you enter, then the user session automatically signs out.
- For iPadOS 13.0 and later in Shared iPad mode:
  - Maximum seconds after screen lock before password is required for Shared iPad.

### Use filters on Windows Enrollment Status Page profile assignments<!-- 7423484  -->

Filters allows you to include or exclude devices in policy or app assignments based on different device properties. When you create an Enrollment Status Page (ESP) profile, you'll be able to use filters when assigning the profile. The **All users** and **All devices** assignment options will also be available. You will be able to find this setting in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Enroll devices** > **Enrollment Status Page** > **Create**. For more information about filters, see [Use filters when assigning your apps, policies, and profiles](../fundamentals/filters.md). For more information about ESP profiles, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

### Filter enrollment restriction assignments by device type <!-- 9284419  -->

New assignment filters in **Enrollment Restrictions** will let you include or exclude restrictions based on device type. For example, you can allow personal devices, while blocking Windows 10 Home devices, by applying the **OSVersion** assignment filter. These filters will be released for public preview and supported for Windows and Apple devices, with Android support coming at a later date. For more information about how to use filters, see [Create a filter](../fundamentals/filters.md).

<!-- ***********************************************-->
## Device management

### Tenant attach: Offboarding <!--9412904 -->

While we know customers get enormous value by enabling tenant attach with Configuration Manager, there are rare cases where you might need to offboard a hierarchy. For example, you may need to offboard from the cloud following a disaster recovery scenario where the on-premises environment was removed. You'll soon be able to offboard a Configuration Manager environment from the Microsoft Endpoint Manager admin center.

### Intune moving to support iOS/iPadOS 13 and higher later this year<!-- 9964998 idrady-->

Later this year, Apple is expected to release iOS 15. Microsoft Intune, including the Intune Company Portal and Intune app protection policies will require [iOS/iPadOS 13 and higher](supported-devices-browsers.md) shortly after the release of iOS 15.

### Intune moving to support  macOS 10.15 and later with the release of macOS 12<!-- 10154527 -->

Apple is expected to release macOS 12 (Monterey) in the fall of 2021. Microsoft Intune, including the Company Portal and Intune MDM agent, will require macOS 10.15 (Catalina) and later shortly after the release of macOS 12.

### New settings when configuring Kerberos single sign-on extension on iOS/iPadOS and macOS<!-- 10175092  -->

There will be new device feature settings available when configuring the Kerberos SSO extension on iOS/iPadOS and macOS devices. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **iOS/iPadOS** or **macOS** > **Configuration profiles** > **Create profile** > select **Device features** for profile > **Single sign-on app extension** > **Kerberos** for SSO app extension type. For related information, see [iOS/iPadOS device feature settings](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) and [macOS device feature settings in Intune](../configuration/macos-device-features-settings.md#single-sign-on-app-extension).  

<!-- ***********************************************-->
## Intune apps

### Intune management agent for macOS devices will be a universal app<!-- 9294405  -->

When you deploy shell scripts or custom attributes for macOS devices from Microsoft Endpoint Manager, it will deploy the new universal version of the Intune management agent app that runs natively on Apple Silicon Mac machines. The same deployment will install the x64 version of the app on Intel Mac machines. For related information, see [Microsoft Intune management agent for macOS](../apps/macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).

### Improved flow when saving logs in Android Company Portal app<!-- 10414688  -->

In the Android Company Portal app, when users need to download a copy of the Android Company Portal logs they will be prompted to choose a folder location. In the Android Company Portal app, users will select **Settings** > **Diagnostic logs** > **SAVE LOGS** to choose the folder location.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Account protection policy changes in Endpoint security<!--  7492116   -->

We’re reworking the endpoint security Account protection policy to use the new APIs for Windows Hello for Business. The new APIs will result in a more consistent experience. The new API is *./Device/Vendor/MSFT/PassportForWork*, which includes more options that can help reduce conflicts.   This API replaces the use of  *./User/Vendor/MSFT/PassportForWork*.  (**Endpoint security** > **Account protection**)

After the change, only new policies you then create will use the new API. Your existing policies won’t be affected by this change and will continue to use the older API.

<!-- ***********************************************
## Role-based access control
-->

<!-- ***********************************************-->
## Scripting

### Intune Data Warehouse updates<!-- 9370034 -->

The  `applicationInventory`  entity will be removed from the Intune Data Warehouse in an upcoming Intune service release. We're introducing a more complete and accurate dataset that will be available in the UI and via our export API. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

<!-- ***********************************************-->
<!--## Security-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
