---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 3/1/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1

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
- This page and the [What's new](whats-new.md) page are updated periodically. Check back for additional updates.
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
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## App management


### Android Enterprise system app support in work profiles<!-- 5291507  -->
You'll be able to deploy Android Enterprise system apps for Android Enterprise Work Profile devices. System apps are apps that do not appear in the Managed Google Play Store and come pre-installed on the device. Once a system app is deployed, you'll be unable to uninstall, hide, or otherwise remove the system app. Note that this feature is planned to be released on or near the 2101 release timeframe. For related information about system apps, see [Add Android Enterprise system apps to Microsoft Intune](../apps/apps-ae-system.md).


<!-- ***********************************************-->

## Device configuration

### More Microsoft Edge settings and categories temporarily removed in Settings Catalog for macOS devices<!-- 9220407 -->
On macOS devices, you can use the Settings Catalog to configure Microsoft Edge version 77 and newer (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings Catalog**). More Microsoft Edge settings are added. Temporarily, the setting categories are removed. To find settings, use the search feature in the Settings Catalog. For a list of settings, [Microsoft Edge - Policies](/DeployEdge/microsoft-edge-policies) is a good resource.

For more information on the Settings Catalog, see [Use the settings catalog to configure settings](../configuration/settings-catalog.md).

Applies to:
- macOS 
- Microsoft Edge 
 
<!-- ***********************************************-->
## Device enrollment

### Microsoft Endpoint Manager ending support for Android 5.x<!--9058248 -->
In a future update, Microsoft Endpoint Manager will stop supporting Android 5.x devices.

### Increasing recommended maximum number of iOS/iPadOS and macOS devices per enrollment token<!--8568668 -->
Currently, we recommend that you don't exceed 60,000 iOS/iPadOS or macOS devices per Automated Device Enrollment (ADE) token. In a future update, this recommended limit will increase to 200,000 devices per token. For more information about ADE tokens, see [Automatically enroll iOS/iPadOS devices by using Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios#supported-volume.md).


<!-- ***********************************************-->
## Device management

### Windows 10 Enterprise multi-session support (public preview)<!--8666391 -->
This support will give users a familiar Windows 10 experience while you get the cost advantages of multi-session and existing per-user M365 licensing. This upcoming support will let you:

- Host multiple concurrent user sessions using the  new Remote Desktop Session Host exclusive to Windows Virtual Desktop on Azure.
- Manage multi-session remote desktops with device-based configurations like a shared, user-less Windows 10 Enterprise client.
- Automatically enroll Hybrid Azure AD joined virtual machines in Intune and target them with OS scope policies and apps.
 
### Use Intune policy to expedite installation of Windows 10 quality updates<!-- 5584682  -->
As part of a public preview, you’ll soon be able to use Intune’s *Windows 10 quality updates* policy to expedite installation of the most recent Windows 10 updates to devices you manage with Intune. (**Devices** > **Windows 10 quality updates (preview)** > **Create profile**).

When you expedite an update, devices can start the download and install of the update as soon as possible, without having to wait for the device to check in for updates. Other than expediting the install of the update, use of this policy leaves your existing update deployment policies and processes untouched.

### Locate device remote action for Windows 10 devices<!--710717-->
You'll be able to use a new locate device remote action to get the geographical location of a device. Supported devices include:
- Windows 10 version 20H2 (10.0.19042.789) or later
- Windows 10 version 2004 (10.0.19041.789) or later
- Windows 10 version 1909 (10.0.18363.1350) or later
- Windows 10 version 1809 (10.0.17763.1728) or later

To see the new action, sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Devices** > **Windows** > choose a Windows 10 > **Locate device**.

This action will work in a similar manner as the current [Locate device action for Apple devices](..\remote-actions\device-locate.md) (but will not include any lost mode functionality).

<!-- ***********************************************-->
## Intune apps

### End users can restart an app install from the Company Portal<!-- 652935  -->
Using the Company Portal, end users will be able to restart an app installation if the progress seems to have stalled or is frozen. This functionality is allowed if the app installation progress has not changed in two hours.


### Microsoft Launcher configuration keys<!-- 8980621 -->
For Android Enterprise fully managed devices, the Microsoft Launcher for Intune app will provide additional customization. You'll be able to configure the set of apps and weblinks, as well as the order, that are displayed in Launcher. The app set and position (order) of app configurations have been merged together to simplify home screen customization. For related information, see [Configure Microsoft Launcher](../apps/configure-microsoft-launcher.md).

### Improved notification experience in the iOS/iPadOS Company Portal app<!-- 7219429  -->
The Company Portal app will store, as well as display, push notifications sent to your users' iOS/iPadOS devices from the Microsoft Endpoint Manager console. Users who have opted in to receive Company Portal push notifications will be able to view and manage the customized stored messages that you send to their devices in the **Notifications** tab of the Company Portal. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

### Microsoft Edge for macOS devices will be a universal app<!-- 9076329  -->
When you deploy Microsoft Edge for macOS devices from Microsoft Endpoint Manager, it will deploy the new universal version of the app that runs natively on Apple Silicon Macs. The same deployment will install the x64 version of the app on Intel Macs. To add Microsoft Edge for macOS, sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Apps** > **All apps** > **Add**. In the **App type** list under **Microsoft Edge, version 77 and later**, select **macOS**. For related information, see [Add Microsoft Edge to macOS devices using Microsoft Intune](../apps/apps-edge-macos.md).

### Additional configuration keys for the Microsoft Launcher app<!-- 9364310  -->
You'll be able to set folder configuration settings for Microsoft Launcher on Android Enterprise corporate owned fully managed devices. By using an app configuration policy and configuration key values, you will be able to set values for folder shape, folder opened to full screen, and folder scroll direction. Also, you will now be able to position the folder on the home screen in addition to positioning apps and web links. Additionally, you can choose to allow end users to modify the folder style values within the app. For more information about Microsoft Launcher, see [Configure Microsoft Launcher for Android Enterprise with Intune](..\apps\configure-microsoft-launcher.md).

### Intune management agent for macOS devices will be a universal app<!-- 9294405  -->
When you deploy shell scripts or custom attributes for macOS devices from Microsoft Endpoint Manager, it will deploy the new universal version of the Intune management agent app that runs natively on Apple Silicon Mac machines. The same deployment will install the x64 version of the app on Intel Mac machines. For related information, see [Microsoft Intune management agent for macOS](../apps/macos-shell-scripts.md#microsoft-intune-management-agent-for-macos). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Account protection policy changes in Endpoint security<!--  7492116   --> 
We’re reworking the endpoint security Account protection policy to use the new APIs for Windows Hello for Business. The new APIs will result in a more consistent experience. The new API is *./Device/Vendor/MSFT/PassportForWork*, which includes more options that can help reduce conflicts.   This API replaces the use of  *./User/Vendor/MSFT/PassportForWork*.  (**Endpoint security** > **Account protection**)
 
After the change, only new policies you then create will use the new API. Your existing policies won’t be affected by this change and will continue to use the older API.

### Organizational report focused on device configuration<!-- 8455708  --> 
We'll be releasing a new **Device configuration** organizational report. This report will replace the existing **Assignment status** report found in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Devices** > **Monitor**. The **Device configuration** report will allow you to generate a list of profiles in the tenant that have devices in a state of success, error, conflict, or pending. You can use filters for the profile type, OS, and state. The returned results will provide search, sort, filter, pagination, and export capabilities. In addition to device configuration details, this report will provide resource access details, and new settings catalog profile details. For related information, see [Intune Reports](../fundamentals/reports.md).

### Update of column names in All devices view and Export report<!-- 8854380  -->
We'll be updating the column names in the All devices view and the Export report to be "Primary User UPN", "Primary User email address", and "Primary User display name" to accurately reflect the data these columns provide.

### Export Intune reports using Graph API v1.0 or beta<!-- 8090911  -->
Intune reporting export API will be available in Graph v1.0, and will continue to be available in Graph beta. For related information, see [Intune reports](../fundamentals/reports.md) and [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md). 


<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## Scripting

### Update when exporting Intune reports using the Graph API<!-- 8764428  -->
When you use the Graph API to export Intune reports without selecting any columns for the devices report, you'll receive the default column set. To reduce confusion, we'll be removing columns from the default column set starting January 2021. The columns being removed are `PhoneNumberE164Format`, `_ComputedComplianceState`, `_OS`, and `OSDescription`. These columns will still be available for selection if you need them, but only explicitly, and not by default. If you have built automation around the default columns of the device export, and that automation uses any of these columns, you need to refactor your processes to explicitly select these and any other relevant columns. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).


### Export localized Intune report data using Graph APIs<!-- 8612346 -->
You'll be able to specify that the report data that you export from the Microsoft Endpoint Manager reporting export [API](../fundamentals/reports-export-graph-apis.md) can contain localized columns only, or localized and non-localized columns. The localized and non-localized columns option will be selected by default for most reports, which will prevent breaking changes. For more information about reports, see [Intune reports](../fundamentals/reports.md) and [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

<!-- ***********************************************-->
## Security

### Improved flow for conditional access on Surface Duo devices<!-- 7552043  -->
We’re streamlining the conditional access flow on Surface Duo devices. These changes happen automatically and won't require any configuration updates by administrators. (**Endpoint security** > **Conditional access**)

- We’re improving the redirection to the Company Portal app when access to a resource is blocked by conditional access. Instead of being sent to the Google Play store listing of the Company Portal app, users will be sent directly to the Company Portal app that’s preinstalled on their Duo device.
- For devices that are enrolled as personally-owned work profile, when a user tries to sign in to a personal version of an app using their work credentials, they will be sent to the work version of Company Portal where guidance messaging is shown. Currently, the user is sent to the Google Play store listing of the personal version of the Company Portal app, where they must reenable the personal Company Portal to see the guidance messaging.



<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
