---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 03/04/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals

# optional metadata

#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. Also:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description will move from this article to [What's new](whats-new.md).
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

<!-- Common categories: use this order:
## Microsoft Intune Suite
## App management
## Device configuration
## Device enrollment
## Device management
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Tenant administration
## Notices
-->

<!-- ***********************************************-->

## App management

### Extended capabilities for Managed Google Play apps on personally-owned Android devices with a work profile<!-- 26554642  -->

There will be new capabilities extended to work profile devices. The following capabilities were previously available only on corporate-owned devices:

- **Available apps for device groups**: You'll soon be able to use Intune to make apps available for device groups through the Managed Google Play store. Previously, apps could only be made available to user groups.

- **Update priority setting**: You'll soon be able to use Intune to configure the app update priority on devices with a work profile. To learn more about this setting, see [Update a Managed Google Play app](../apps/apps-add-android-for-work.md#update-a-managed-google-play-app).

- **Required apps display as available in Managed Google Play**: You'll soon be able to use Intune to make required apps available for users through the Managed Google Play store. Apps that are part of existing policies will now display as available.

Applies to:

- Android Enterprise personally owned devices with a work profile

### Managed app assignment filters for Windows MAM<!-- 24801139  -->

You'll be able to use managed app assignment filters for Window MAM app protection policies and app configuration policies.

For information about Windows MAM, see [Data protection for Windows MAM](../apps/protect-mam-windows.md).

For more information about assignment filters, see [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](../fundamentals/filters.md).

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies now provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

### Company Portal automatically installed on Android Enterprise dedicated devices<!-- 6423852  -->

Intune Company Portal will now be automatically installed on all Android Enterprise dedicated devices to ensure the appropriate handling of app protection policies. Users won't be able to see or launch the Company Portal, and there are no requirements for users to interact with it. Admins will notice that the Company Portal is automatically installed on their Android Enterprise dedicated devices, without the ability to uninstall.

### Support for multi-SIM iOS/iPadOS device inventory<!-- 17016690  -->

You'll be able to view the service subscription fields on devices that have multiple SIM cards installed under the per-device Hardware section. The inventory fields that are capable of reporting multiple values to Intune are:

- **ICCID**
- **IMEI**
- **MEID**
- **Phone number**

These fields will default to using labels returned by the device, such as: *Primary*, *Secondary*, *CTSubscriptionSlotOne*, and *CTSubscriptionSlotTwo*. These returned labels may be displayed in the language of the local device that is reporting its inventory to Intune.

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### New BIOS device configuration profile for OEMs<!-- 9278502  -->

There will be a new **BIOS configuration and other settings** device configuration policy for OEMs. OEMs can use this new policy to enable or disable different BIOS features that secure device. In the Intune device configuration policy, you add the BIOS configuration file, and then assign the policy to your devices.

For example, admins can use the [Dell Command tool](https://www.dell.com/support/kbdoc/000108963/how-to-use-and-troubleshoot-dell-command-update-to-update-all-drivers-bios-and-firmware-for-your-system) (opens Dell's website) to create the BIOS configuration file. Then, they add this file to the new Intune policy.

Applies to

- Windows 10 and later

### New settings available in the Windows settings catalog<!-- 26763724  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

- **DODisallowCacheServerDownloadsOnVPN** - This setting blocks downloads from Microsoft Connected Cache servers when the device connects using VPN. By default, the device is allowed to download from Microsoft Connected Cache when connected using VPN.

- **DOSetHoursToLimitBackgroundDownloadBandwidth** - This setting specifies the maximum background download bandwidth. Delivery Optimization uses this bandwidth during and outside business hours across all concurrent download activities as a percentage of available download bandwidth.

- **DOSetHoursToLimitForegroundDownloadBandwidth** - This setting specifies the maximum foreground download bandwidth. Delivery Optimization uses this bandwidth during and outside business hours across all concurrent download activities as a percentage of available download bandwidth.

- **DOVpnKeywords** - This policy allows you to set one or more keywords used to recognize VPN connections.

For more information on these settings, see [Policy CSP - DeliveryOptimization](/windows/client-management/mdm/policy-csp-deliveryoptimization).

Applies to:

- Windows 10 and later

### New settings available in the Apple settings catalog<!-- 26551582  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

#### iOS/iPadOS

**Declarative Device Management (DDM) > Passcode**:

- Maximum Passcode Age In Days
- Minimum Complex Characters
- Require Alphanumeric Passcode

**Restrictions**:

- Allow Marketplace App Installation

#### macOS

**Declarative Device Management (DDM) > Passcode**:

- Change At Next Auth
- Custom Regex
- Failed Attempts Reset In Minutes
- Maximum Passcode Age In Days
- Minimum Complex Characters
- Require Alphanumeric Passcode

### The macOS Company Portal app will support platform SSO (public preview)<!-- 24325427  -->

In Intune, you can configure the Enterprise SSO plug-in on Apple devices using a device configuration profile (**Devices** > **Configuration** > **Create** > **macOS** for platform > **Settings Catalog** for profile > **Authentication** > **Extensible Single sign-on (SSO)**).

The Company Portal app version will support the platform SSO settings for macOS 13 and later. Platform SSO allows you to sync your Microsoft Entra ID password to local accounts on Macs using the Enterprise Single Sign-On extension.

For more information on the Enterprise SSO plug-in, see:

- [Use Intune to deploy the Microsoft Enterprise SSO plug-in for Apple devices](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)
- [Microsoft Entra ID and the Microsoft Enterprise SSO plug-in overview for Apple devices](/azure/active-directory/develop/apple-sso-plugin)

Applies to:

- macOS 13 and later

<!-- *********************************************** -->

## Device enrollment

### RBAC changes coming to enrollment settings for Windows Hello for Business<!-- 25661866   -->

We're updating RBAC in the enrollment area for Windows Hello for Business. Enrollment settings related to Windows Hello for Business will be read-only for all roles except the Intune Service Administrator. The Intune Service Administrator will be able to edit enrollment settings.

<!-- *********************************************** -->

## Device management

### New compliance settings for Android work profile, personal devices<!-- 24743927  -->

New compliance settings will let you add restrictions to the work profile password on a personal device without impacting the device password. Settings will be available in Microsoft Intune compliance policies under **Android Enterprise personally-owned work profiles** >**System Security** > **Work Profile Security**, and include:

- Require a password to unlock work profile
- Number of days until password expires
- Number of previous passwords to prevent reuse
- Maximum minutes of inactivity before password is required
- Password complexity
- Required password type
- Minimum password length

Company Portal will enforce the settings and mark the device as noncompliant if the work profile password fails to meet your requirements. Intune compliance settings take precedence over the respective Intune configuration settings. For example, if the password complexity in your compliance policy is set to *medium* and the one in your configuration profile is set to *high*, Intune will prioritize and enforce the compliance setting.

Applies to:

- Android Enterprise personally owned devices with a work profile

### End-user access to BitLocker Recovery Keys for enrolled Windows devices<!-- 8077173 -->

End-users will be able to view the BitLocker Recovery Key for enrolled Windows devices in the Web Company Portal. This capability will reduce helpdesk calls in the event they get locked out of their corporate machines. End users can access their enrolled Windows device's Recovery Key by clicking on **View Recovery Key** under their device after logging into the Web Company Portal. This is a similar experience to the MyAccount website, which allows end users see their recovery keys as well.

Access to BitLocker recovery keys by end-users can be prevented when not allowed within your organization by using the Microsoft Entra ID toggle **Restrict non-admin users from recovering the BitLocker key(s) for their owned device**. For more information about how to prevent access to BitLocker recovery keys, see [Manage device identities using the Microsoft Entra admin center](/entra/identity/devices/manage-device-identities).

### Introducing a remote action to pause the config refresh enforcement interval<!--24249019  -->

In the Windows Settings Catalog, you can configure **Config Refresh**. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check in to Intune. The device will replay and re-enforce settings based on previously received policy to minimize the chance for configuration drift.

To support this feature, a remote action will be added to allow a pause in action. If an admin needs to make changes or run remediation on a device for troubleshooting or maintenance, they can issue a pause from Intune for a specified period. When the period expires, settings will be enforced again.

The remote action **Pause config refresh** can be accessed from the device summary page.

For information on currently available Remote actions, see [Remote actions](../remote-actions/device-management.md).

<!-- *********************************************** -->

## Device security

### Defender for Endpoint security settings support in government cloud environments<!-- 24191406  -->

Customer tenants in US Government Community (GCC) High, and Department of Defense (DoD) environments will soon be able to use Intune to manage the Defender security settings on the devices you’ve onboarded to Defender without enrolling those devices with Intune. This capability is known as [Defender for Endpoint security settings management](../protect/mde-security-integration.md).

For more information about the Intune features supported in GCC High and DoD environments, see [Intune US Government service description](../fundamentals/intune-govt-service-description.md).

### Updated security baseline for Windows version 23H2<!-- 25021947 -->

We’re working on an update to the Intune security baseline for Windows. The updated security baseline is based on the **version 23H2** of the Group Policy security baseline found in the [Security Compliance Toolkit and Baselines](https://www.microsoft.com/en-us/download/details.aspx?id=55319) from the Microsoft Download Center, and includes only the settings that are applicable to devices managed through Intune. Use of this updated baseline can help you maintain best-practice configurations for your Windows devices.

Use of [Intune security baselines](../protect/security-baselines.md) can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations, which you can modify to meet the requirements of your organization.

### Improvements for Intune deployments of Microsoft Defender for Endpoint<!-- 26314441  -->

We’re improving and simplifying the experience, workflow, and reporting details when using Intune’s [endpoint detection and response](../protect/endpoint-security-edr-policy.md) (EDR) policy to deploy Microsoft Defender for Endpoint. These changes will apply for Windows devices managed by Intune and the tenant-attach scenario. These improvements include:

- Changes to dashboards and reports to improve the visibility of your Defender EDR deployment numbers.
- A tenant-wide deployment option for Intune EDR policy that streamlines deployments of Defender for Endpoint to applicable devices.
- Changes to Intune’s endpoint security Overview page to provide consolidated dashboard reports for the device signals from Defender on your managed devices.

Applies to the following through cloud and tenant attach endpoints:

- Windows 10
- Windows 11

### HTML formatting supported in noncompliance email notifications <!-- 24197255   -->

HTML formatting will be supported in noncompliance email notifications for all platforms. You'll be able to use supported HTML tags to add formatting such as italics, URL links, and bulleted lists to your organization's messages.

### Support for Intune Device control policy for devices managed by Microsoft Defender for Endpoint<!-- 15466620 -->

You'll be able to use the endpoint security policy for *Device control* (Attack surface reduction policy) from the Microsoft Intune with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Device control** policies are part of endpoint security [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

  Applies to the following when you use the *Windows 10, Windows 11, and Windows Server* platform:
  - Windows 10
  - Windows 11

When this change takes effect, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive this policy will get it.

<!-- *********************************************** -->

## Monitor and troubleshoot

### Intune support of Microsoft 365 remote application diagnostics<!-- 17409991  -->

The Microsoft 365 remote application diagnostics will allow Intune admins to request Intune App Protection logs and Microsoft 365 application logs (where applicable) directly from the Intune console. Admins will find this report in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Summary** > *App protection**.

This feature is exclusive to applications that are under Intune App Protection management. If supported, the application specific logs are gathered and stored within dedicated storage solutions for each application. Currently, Outlook mobile logs are supported in version 2403, with support for additional applications coming soon.

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
