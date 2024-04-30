---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 05/01/2024
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

### Device IPv4 and IPv6 addresses available from Managed Home Screen<!-- 25994445 -->

IPv4 and IPv6 addresses will both be available from the Device Information page of Managed Home Screen (MHS).

### Migrated to .NET MAUI from Xamarin<!-- 27143739 -->

Xamarin.Forms has evolved into .NET Multi-platform App UI (MAUI). Existing Xamarin projects should be migrated to .NET MAUI. For more information about upgrading Xamarin projects to .NET, see the [Upgrade from Xamarin to .NET & .NET MAUI](/dotnet/maui/migration/?WT.mc_id=dotnet-35129-website) documentation.

Xamarin support will end on May 1, 2024 for all Xamarin SDKs including Xamarin.Forms and Intune App SDK Xamarin Bindings. For Intune support on Android and iOS platforms, see [Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android) and [Microsoft Intune App SDK for MAUI.iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies now provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

<!-- *********************************************** -->

## Device configuration

### New settings available in the macOS settings catalog<!-- 26970197 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

We will add new settings in the macOS Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **macOS** for platform > **Settings catalog** for profile type.

**Microsoft AutoUpdate (MAU)**:

- Microsoft Teams (work or school)
- Microsoft Teams classic

**Microsoft Defender > Features**:

- Use Data Loss Prevention
- Use System Extensions

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:

- macOS

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

### Define corporate device identifiers for Windows<!-- 25873757 -->

Microsoft Intune will support corporate device identifiers for Windows devices. You will be able to upload a CSV file with model, manufacturer, and serial number to identify corporate machines ahead of enrolling. When a device that matches the model, manufacturer, and serial number criteria enrolls, it will be marked as corporate and managed appropriately.

### Intune adding support for Red Hat Enterprise Linux<!-- 25160548 -->

Microsoft Intune will support device management for Red Hat Enterprise Linux. You'll be able to enroll and manage Red Hat Enterprise Linux devices, and assign standard compliance policies, custom configuration scripts, and compliance scripts.

Applies to:

- Red Hat Enterprise Linux 9
- Red Hat Enterprise Linux 8

### Account-driven Apple User Enrollment to be generally available for iOS/iPadOS 15+ devices<!-- 10277062 -->

Intune will support account-driven Apple User Enrollment, the new and improved version of Apple User Enrollment, for devices running iOS/iPadOS 15 and later. This new enrollment method utilizes just-in-time registration, removing the Company Portal app for iOS as an enrollment requirement. Device users will be able to initiate enrollment directly in the Settings app, resulting in a shorter and more efficient onboarding experience. For more information, see [Set up account driven Apple User Enrollment](../enrollment/apple-account-driven-user-enrollment.md) on Microsoft Learn.

If you prefer, you can continue to target iOS/iPadOS devices using the Apple User Enrollment method that requires Company Portal. Devices running iOS/iPadOS 14.8.1 and earlier will be unaffected by this update and can continue to use the method with Company Portal.

#### RBAC changes coming to enrollment platform restrictions <!-- 25036419 -->

We're updating RBAC for enrollment platform restrictions. Enrollment platform restrictions will be read-only for all roles except the Intune Service Administrator. The Intune Service Administrator will be able to create and edit enrollment platform restrictions.

<!-- *********************************************** -->

## Device management

### New version of Windows hardware attestation report<!-- 15425680 -->

We're introducing a new version of the Windows hardware attestation report that shows the value of settings attested by Device Health Attestation and Microsoft Azure Attestation for Windows 10/11. The Windows hardware attestation report will be built on a new reporting infrastructure, and updated to reflect new settings added to Microsoft Azure Attestation. The report will be available in the admin center under **Reports** > **Device Compliance** > **Reports**. The Windows health attestation report that exists today under **Devices** > **Monitor** will be retired.

### Optional feature updates<!--12769586 -->

With the introduction of Optional Feature updates, Feature updates will be made available to end users as Optional updates. End users will see the update in the **Windows Update** settings page in the same way it is shown for consumer devices.

End users can then easily opt-in to try out the next feature update and provide feedback. When it is time to roll out the feature as a **required** update, then admins will be able to change the setting on the policy, and update the rollout settings so that the update is deployed as a **required** update to devices that do not yet have it installed.

For more information on Feature updates, see [Feature updates for Windows 10 and later policy in Intune](..//protect/windows-10-feature-updates.md).

### End-user access to BitLocker Recovery Keys for enrolled Windows devices<!-- 8077173 -->

End-users will be able to view the BitLocker Recovery Key for enrolled Windows devices in the Web Company Portal. This capability will reduce helpdesk calls in the event they get locked out of their corporate machines. End users can access their enrolled Windows device's Recovery Key by clicking on **View Recovery Key** under their device after logging into the Web Company Portal. This is a similar experience to the MyAccount website, which allows end users see their recovery keys as well.

Access to BitLocker recovery keys by end-users can be prevented when not allowed within your organization by using the Microsoft Entra ID toggle **Restrict non-admin users from recovering the BitLocker key(s) for their owned device**. For more information about how to prevent access to BitLocker recovery keys, see [Manage device identities using the Microsoft Entra admin center](/entra/identity/devices/manage-device-identities).

<!-- *********************************************** -->

## Device security

### Updated security baseline for Microsoft Defender for Endpoint<!-- 26504935 -->

We're working on an update to the Intune security baseline for **Microsoft Defender for Endpoint**. The new baseline, **version 24H1**, will use the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline will represent the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

### Defender for Endpoint security settings support in government cloud environments<!-- 24191406 -->

Customer tenants in US Government Community (GCC) High, and Department of Defense (DoD) environments will soon be able to use Intune to manage the Defender security settings on the devices you've onboarded to Defender without enrolling those devices with Intune. This capability is known as [Defender for Endpoint security settings management](../protect/mde-security-integration.md).

For more information about the Intune features supported in GCC High and DoD environments, see [Intune US Government service description](../fundamentals/intune-govt-service-description.md).

### Updated security baseline for Windows 365 Cloud PC<!-- 26504698 -->

We're working on an update to the Intune security baseline for **Windows 365 Cloud PC**. The new baseline version will use the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline will represent the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

### Support for Intune Device control policy for devices managed by Microsoft Defender for Endpoint<!-- 15466620 -->

You'll be able to use the endpoint security policy for *Device control* (Attack surface reduction policy) from the Microsoft Intune with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Device control** policies are part of endpoint security [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

Applies to the following when you use the *Windows 10, Windows 11, and Windows Server* platform:

- Windows 10
- Windows 11

When this change takes effect, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive this policy will get it.

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

## Tenant administration

### Customize your Intune admin center experience<!-- 24155584 -->

You will be able to better customize your Intune admin center experience by using collapsible navigation and favorites. The left navigation menus in the Intune admin center will be updated to support expanding and collapsing each subsection of the menu. In addition, you will be able to set admin center pages as favorites.

By default, menu sections will be expanded and provide the same experience today. You will be able to choose your portal menu behavior by selecting the **Settings** gear icon at the top right to display the **Portal settings**. Then, you can select **Appearance + startup views** and set the **Service menu behavior** to **Collapsed** or **Expanded** as the default portal option. Each menu section will retain the expanded or collapsed state that you choose. Additionally, selecting the star icon next to a page on the left nav will add the page to a **Favorites** section near the top of the menu.

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
