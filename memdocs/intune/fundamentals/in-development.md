---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 01/04/2022
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
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. In addition to the information in this article:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description will move from this article to [What's new](whats-new.md).  
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

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

### Deploy DMG-type applications to managed macOS devices<!-- 1171356 -->
You will be able to upload and deploy DMG-type applications to managed Macs from Microsoft Endpoint Manager using the **required** assignment type. DMG is the file extension for Apple disk image files. DMG-type apps are deployed using the Intune MDM agent for macOS devices. You can add a DMG app from [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **macOS** > **Add** > **macOS app (DMG)**. 

### Password complexity for Android devices<!-- 9321870 -->
The **Require device lock** setting in Intune will be extended to include values (**Low Complexity**, **Medium Complexity**, and **High Complexity**). If the device lock doesn't meet the minimum password requirement, you'll be able to **warn**, **wipe data**, or **block** the end user from accessing a managed account in a managed app. 

This feature targets devices that operate on Android 11+. For devices that operate on Android 10 and earlier, setting a complexity value of **Low**, **Medium**, or **High** will default to the expected behavior for **Low Complexity**. For related information, see [Android app protection policy settings in Microsoft Intune](..\apps\app-protection-policy-settings-android.md).

<!-- ***********************************************-->

## Device security

### New Account protection policy to configure users in local groups on devices<!--5663034 -->
We’re adding a new policy under endpoint security Account protection that you can use to manage the local user groups on a device. The settings are from the [Windows Client Management CSP - LocalUsersAndGroups](/windows/client-management/mdm/policy-csp-localusersandgroups).  (**Endpoint security** > **Account protection** > **Local Group Restrictions**).

With this capability, when configuring the policy you’ll be able to select users from the Azure AD group picker, or manually add users by their SID.

<!-- ***********************************************-->

## Device configuration

### Use Collect diagnostics to collect additional details from Windows 365 devices through Intune remote actions<!--  12636207 -->
Intune’s remote action to [*Collect diagnostics*](../remote-actions/collect-diagnostics.md) will soon collect additional details from Windows 365 (Coud-PC) devices.  (**Devices** > **Windows** > *select a Windows 365 device* > **Collect diagnostics**)

The new details for Windows 365 devices include the following registry data:
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\AddIns\WebRTC Redirector 
- HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Teams\

### Automatic device clean-up rules support for Android Enterprise devices<!-- 9797532 -->
Intune supports the creation of rules to automatically remove devices that appear to be inactive, stale, or unresponsive. You'll soon be able to use these clean-up rules with Android Enterprise devices that previously did not support them. This support is coming for:
- Android Enterprise Fully Managed
- Android Enterprise Dedicated
- Android Enterprise Corporate-Owned with Work Profile

To learn more about clean-up rules, see [Automatically delete devices with cleanup rules](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules).

### Choose a user or device scope when creating Windows VPN profiles<!-- 10685553 -->
You will be able to create a VPN profile for Windows devices that configures VPN settings (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **VPN** for profile).

When you create a profile, there's a new **Use this VPN profile with a user/device scope** setting that lets you apply the profile to the user scope or the device scope:
- **User scope**: The VPN profile is installed within the user's account on the device.
- **Device scope**: The VPN profile is installed in the device context and applies to all users on the device.

Existing VPN profiles will apply to their existing scope, and are not impacted by this change. Currently, all VPN profiles are installed in the user scope *except* for the profiles with device tunnel enabled, which requires device scope.

For more information on VPN settings you can currently configure, see [Windows device settings to add VPN connections using Intune](../configuration/vpn-settings-windows-10.md).

Applies to:
- Windows 11
- Windows 10

### New device restriction settings for Android Enterprise corporate-owned devices with a work profile<!-- 10982232 -->
On Android Enterprise devices, you can configure settings that control features on devices (**Devices** > **Configuration Profiles** > **Create profile** > **Android Enterprise** for platform > **Device restrictions** for profile type).

For Android Enterprise corporate-owned devices with a work profile, there are new settings:
- Restrict searching work contacts and displaying work contact caller-ID in personal profile
- Restrict copy and paste between work and personal profiles
- Restrict data sharing between work and personal profiles

For more information on the settings that you can currently configure, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android Enterprise corporate-owned work profile (COPE)

### Use filters to assign proactive remediation scripts for endpoint analytics and to assign Endpoint Security policies in the Endpoint Manager admin center (public preview)<!-- 7566953 7591178  -->

In the Endpoint Manager admin center, you can create filters and then use these filters when assigning apps and policies. You'll be able to use filters to assign the following policies:

- [Windows PowerShell scripts for proactive remediations in endpoint analytics](../../analytics/proactive-remediations.md) (**Reports** > **Endpoint analytics** > **Proactive remediations**)
- [Endpoint security policies](../protect/endpoint-security-policy.md), such as account protection, antivirus, and attack surface reduction

For more information on filters, see [Use filters (preview) when assigning your apps, policies, and profiles](filters.md).

Applies to:

- macOS

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot  

### Changes to the account protection policy in endpoint security<!--  7492116   -->

We're reworking the account protection policy in endpoint security to use the new API for Windows Hello for Business. The new API will result in a more consistent experience. 

The new API is *./Device/Vendor/MSFT/PassportForWork*, which includes more options that can help reduce conflicts. This API replaces *./User/Vendor/MSFT/PassportForWork* (**Endpoint security** > **Account protection**).

After the change, only new policies then you create will use the new API. Your existing policies won't be affected by this change and will continue to use the older API.

<!-- ***********************************************
## Role-based access control
-->

<!-- ***********************************************-->
## Scripting

### Intune Data Warehouse updates<!-- 9370034 -->

The `applicationInventory` entity will be removed from the Intune Data Warehouse in an upcoming Intune service release. We're introducing a more complete and accurate dataset that will be available in the UI and via our export API. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

<!-- ***********************************************-->
<!--## Security-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
