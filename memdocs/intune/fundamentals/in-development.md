---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 10/29/2021
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

### Update Android Company Portal and Intune apps for custom notifications<!-- 12473860  -->
We will be making service side updates to custom notifications in Intune's November (2111) service release which require users to have updated to recent versions of the Android Company Portal (version 5.0.5291.0, released in October 2021) or Android Intune app (version 2021.09.04, released in September 2021) for the best user experience. If users do not update prior to Intune's November (2111) service release and they are sent a custom notification, they will instead receive a notification telling them to update their app to view the notification. Once they update their app, they will see the message sent by your organization in the Notifications section in the app.

### New ADMX settings for Edge 95 and Edge updater<!-- 12426698 -->
New ADMX settings for Edge 95 and Edge updater have been added to Administrative Templates. This includes support for "Target Channel override" which allows customers to opt into the **[Extended Stable](https://blogs.windows.com/msedgedev/2021/07/15/opt-in-extended-stable-release-cycle/)** release cycle option at any point using Group Policy or through Intune. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Configuration profiles** > **Create profile**. Then, select **Platform** > **Windows 10 and later** and **Profile** > **Templates** > **Administrative Templates**. For related information, see [Overview of the Microsoft Edge channels](/deployedge/microsoft-edge-channels), [Microsoft Edge Browser Policy Documentation](/deployedge/microsoft-edge-policies), and [Configure Microsoft Edge policy settings in Microsoft Intune](../configuration/administrative-templates-configure-edge.md).

### New privacy consent screen during Company Portal installation <!-- 6600502 -->
People installing the Company Portal app for the first time from certain app stores, such as those in China, may see a new privacy consent screen during installation. The screen explains what information Microsoft collects and how it's used. Users must agree to the terms before they can use the app. Users who installed Company Portal prior to this release will not see the new screen.  

### New RBAC permission for Win32 app supersedence and dependency relationships<!-- 11126374 -->
A new Microsoft Endpoint Manager permission will be added to create and edit Win32 app supersedence and dependency relationships with other apps. The permission will be available under the **Mobile apps** category by selecting **Relate**. Starting in the 2202 service release, MEM admins will need this permission to add supersedence and dependency apps when creating or editing a Win32 app in Microsoft Endpoint Manager admin center. To find this permission when it is available, in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Roles** > **All roles** > **Create**. This permission will be added to the following built-in roles:
- Application Manager
- School administrator
For related information, see [Create a custom role in Intune](..\fundamentals\create-custom-role.md).

### Filter improvements when displaying platform-specific app lists<!-- 10994275 -->
Filters will be improved when displaying platform-specific app lists in the Microsoft Endpoint Manager admin center. Previously, when navigating to a platform-specific app list, you could not use the **App type** filter on the list. With this change, you will be able to apply filters (including the **App Type** and **Assignment status** filters) on the platform-specific list of apps. For related information, see [Intune reports](../fundamentals/reports.md).

### Password complexity for Android devices<!-- 9321870 -->
The **Require device lock** setting in Intune will be extended to include values (**Low Complexity**, **Medium Complexity**, and **High Complexity**). If the device lock doesn’t meet the minimum password requirement, you will be able to **warn**, **wipe data**, or **block** the end user from accessing a managed account in a managed app. This feature targets devices that operate on Android 11+. For devices operating on Android 11 and earlier, setting a complexity value of **Low**, **Medium**, or **High** will default to the expected behavior for **Low Complexity**. For related information, see [Android app protection policy settings in Microsoft Intune](..\apps\app-protection-policy-settings-android.md).

### Enable app update priority for Managed Google Play apps<!-- 7810180 -->
You'll be able to set the update priority of Managed Google Play apps on dedicated, fully managed, and corporate-owned with a work profile Android Enterprise devices. Select **High Priority** to update an app as soon as the developer has published the app, regardless of charge status, Wi-Fi capability, or end user activity on the device. For related information, see [Add Managed Google Play apps to Android Enterprise devices with Intune](..\apps\apps-add-android-for-work.md).

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

## Device security

### Adding 13 BitLocker settings to settings catalog<!-- 10956191 -->  
13 settings from the [BitLocker configuration service provider (CSP)](/windows/client-management/mdm/bitlocker-csp) are being added to the Microsoft Intune settings catalog. To access the settings when they become available, go to **Devices** > **Configuration profiles** and create a settings catalog profile for devices running Windows 10 and later. Settings will be under the **BitLocker** category. For more information about the settings catalog, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

### View BitLocker recovery keys for tenant attached devices<!-- 8509415 -->
You’ll soon be able to view the BitLocker recovery key for tenant-attached devices in the Microsoft Endpoint Manager admin center. The recovery keys continue to be stored on-premises for tenant-attached devices, but the visibility in the admin center is intended to assist your Helpdesk scenarios from within the admin center. 

To view the keys, your Intune account will need Intune RBAC permissions to view BitLocker keys and must also be associated with an on-premises user that has the related on-premises permissions of Collection Role, with Read Permission > Read BitLocker Recovery Key Permission.

When this capability become available, users with the correct permissions can view keys by going to **Devices** > **Windows devices** > *select a tenant-attached device* > **Recovery keys**.

This capability will be supported with Configuration Manager sites that run version 2107 or later. An update rollup for version 2107 will be required to support Azure AD joined devices.

### Updates for Security Baselines<!-- 9549108,  10873848 -->
We’ll soon release updates to the following [security baselines​](../protect/security-baselines.md):

- **Security baseline for Windows 10 and later** (Applies to Windows 10 and Windows 11)
- **Windows 365 Security Baseline (Preview)**

See the available baselines in the Microsoft Endpoint Manager admin center:  **Endpoint security** > **Security baselines**.

Updated baseline versions bring support for recent settings to help you maintain the best-practice configurations recommended by the respective product teams.  

Plan to [update your baselines](../protect/security-baselines-configure.md#change-the-baseline-version-for-a-profile) to the latest version. To understand what's changed between versions, see [Compare baseline versions](../protect/security-baselines.md#compare-baseline-versions) to learn how to export a .CSV file that shows the changes.

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

### Duplicate a settings catalog profile<!-- 9666635 -->      
Settings catalog profiles will soon support duplication. A new **Duplicate** button will be added so that you can copy and repurpose an existing profile. The copy will contain the same setting configurations and scope tags as the original profile, but won't have any assignments. For more information about how to duplicate profiles, see [Duplicate a policy](../protect/endpoint-security-policy.md#duplicate-a-policy).

### MDM support data to refresh automatically in Group Policy analytics tool<!-- 7852080 -->
Whenever Microsoft makes changes to the mappings in Intune, the **MDM Support** column in the GP analytics tool will automatically update to reflect the changes. The automation is an improvement over the current behavior, which requires you to reimport your group policy object (GPO) to refresh data.

### Non-applicable status entries will no longer be shown in the **Device Install Status** report<!-- 12419387 -->
Based on a selected app, the **Device Install Status** report provides a list of devices and status information for the selected app. App installation details related to the device includes **UPN**, **Platform**, **Version**, **Status**, **Status details**, and **Last check-in**. If the device's platform differs from the application's platform, rather then showing **Not Applicable** for the **Status details** of the entry, the entry will no longer be provided. For example, if an Android app has been select and the app is targeted to an iOS device, rather than providing a **Not Applicable** device status value, the device status for that entry will not be shown in the **Device Install Status** report.  To find this report, in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All Apps** > *Select an app* > **Device Install status**. For related information, see [Device Install Status report for apps (Operational)](../fundamentals/reports.md#device-install-status-report-for-apps-operational).

### Create custom settings for Device Compliance for Windows 10/11 devices (public preview)<!--7536730 -->
As a public preview, device compliance policy for Windows 10 and Windows 11 devices will support adding custom settings to a device compliance policy. Results from custom settings will report back along with other compliance details.
 
To use custom settings, you must first define those settings through the use of two files:
 
- **JSON** – The JSON file lists custom settings, compliance values, and remediation information.
- **PowerShell** – A PowerShell script that’s deployed to devices and runs to determine their state based on the related JSON file.
 
After creating and uploading the two files as a script, you create a standard Compliance policy that also includes your custom settings script. (**Endpoint security** > **Device compliance** > **Create Policy** > **Windows 10 and later**). Options for custom settings will appear in a new category named *Custom Compliance* that will be available on the *Compliance settings* page for creating a policy.

### New details for Windows devices available in the Microsoft Endpoint Manager admin center<!-- 6208666 -->
Soon, new details will be available for Windows 10 and Windows 11 devices. This information will be visible when viewing the device on the **All devices** pane in the Microsoft Endpoint Manager admin center, and as part of the All device *export*.
 
The following device properties will be collected and available in the admin center:

- System Management BIOS version
- TPM Manufacturer version
- TPM Manufacturer ID

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
