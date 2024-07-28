---
# required metadata
title: What's new in Microsoft Intune
titleSuffix:
description: Find out what's new in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/25/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier2
- M365-identity-device-management
- highseo
---

# What's new in Microsoft Intune

Learn what's new each week in Microsoft Intune.

You can also read:

- [**Important notices**](#notices)
- [Past releases](whats-new-archive.md) in the What's new archive
- Information about [how Intune service updates are released](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728)

> [!NOTE]
> Each [monthly update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) can take up to three days to rollout and will be in the following order:
>
> - Day 1: Asia Pacific (APAC)
> - Day 2: Europe, Middle East, Africa (EMEA)
> - Day 3: North America
> - Day 4+: Intune for Government
>
> Some features roll out over several weeks and might not be available to all customers in the first week.
>
> For a list of upcoming Intune feature releases, see [In development for Microsoft Intune](../fundamentals/in-development.md).
>
> For new information about Windows Autopilot solutions, see:
>
> - [Windows Autopilot device preparation: What's new](/autopilot/device-preparation/whats-new).
> - [Windows Autopilot: What's new](/autopilot/whats-new).

You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Get notified when this page is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us` -->

<!-- Common categories - in this order:

### Microsoft Intune Suite
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
### Scripts
### Tenant administration

-->

## Week of July 22, 2024 (Service release 2407)

### App management

#### Intune support for additional macOS app types from the Company Portal<!-- 26133163 -->

Intune supports the capability to deploy DMG and PKG apps as **Available** in the Intune macOS Company Portal. This capability enables end users to browse and install agent-deployed applications using Company Portal for macOS. This capability requires a minimum version of the Intune agent for macOS v2407.005 and Intune Company Portal for macOS v5.2406.2.

#### Newly available Enterprise App Catalog apps for Intune<!-- 28691663 -->

The Enterprise App Catalog has updated to include additional apps. For a complete list of supported apps, see [Apps available in the Enterprise App Catalog](../apps/apps-enterprise-app-management.md#apps-available-in-the-enterprise-app-catalog).

#### The Intune App SDK and Intune App Wrapping Tool are now in a different GitHub repo<!-- 27264674, 27264632 -->

The Intune App SDK and Intune App Wrapping Tool have moved to a different GitHub repository and a new account. There are redirects in place for all existing repositories. In addition, the Intune sample applications are also included in this move. This change relates to both Android and iOS platforms.

### Device configuration

#### New clipboard transfer direction settings available in the Windows settings catalog <!-- 28748086 --> 

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

**Administrative Templates > Windows Components > Remote Desktop Services > Remote Desktop Session Host > Device and Resource Redirection**:

- Restrict clipboard transfer from server to client
- Restrict clipboard transfer from server to client (User)
- Restrict clipboard transfer from client to server
- Restrict clipboard transfer from client to server (User)

For more information on configuring the clipboard transfer direction in Azure Virtual Desktop, go to [Configure the clipboard transfer direction and types of data that can be copied in Azure Virtual Desktop](/azure/virtual-desktop/clipboard-transfer-direction-data-types).

Applies to:

- Windows 11
- Windows 10

#### New settings available in the Apple settings catalog <!-- 28052449 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Restrictions**:

- Allow Auto Dim

##### macOS

**Privacy > Privacy Preferences Policy Control**:

- Bluetooth Always

#### Android Enterprise has new values for the Allow access to all apps in Google Play store setting<!-- 28367525 -->

In an Intune device restrictions configuration policy, you can configure the **Allow access to all apps in Google Play store** setting using the **Allow** and **Not configured** options (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully managed, dedicated and corporate-owned work profile > Device restrictions** for profile type > **Applications).

The available options are updated to **Allow**, **Block**, and **Not configured**.

There is no impact to existing profiles using this setting.

For more information on this setting and the values you can currently configure, see [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:

- Android Enterprise Fully managed, dedicated and corporate-owned work profile

### Device enrollment

#### New support for Red Hat Enterprise Linux<!-- 25160548 -->

Microsoft Intune now supports device management for Red Hat Enterprise Linux. You can enroll and manage Red Hat Enterprise Linux devices, and assign standard compliance policies, custom configuration scripts, and compliance scripts. For more information, see [Deployment guide: Manage Linux devices in Microsoft Intune](deployment-guide-platform-linux.md) and [Enrollment guide: Enroll Linux desktop devices in Microsoft Intune](deployment-guide-enrollment-linux.md).

Applies to:

- Red Hat Enterprise Linux 9
- Red Hat Enterprise Linux 8

#### New Intune report and device action for Windows enrollment attestation (public preview)<!-- 12581956 -->

Use the new device attestation status report in Microsoft Intune to find out if a device has attested and enrolled securely while being hardware-backed. From the report, you can attempt remote attestation via a new device action.

For more information, see:

- [Windows enrollment attestation](../enrollment/windows-enrollment-attestation.md)
- [Intune Reports](../fundamentals/reports.md#device-attestation-status-report)

### Device management

#### Consolidation of Intune profiles for identity protection and account protection <!-- 24810271 -->

We have consolidated the Intune profiles that were related to identity and account protection, into a single new profile named *Account protection*. This new profile is found in the [account protection policy node of endpoint security](../protect/endpoint-security-account-protection-policy.md), and is now the only profile template that remains available when creating new policy instances for identity and account protection. The new profile includes Windows Hello for Business settings for both users and devices, and settings for Windows Credential Guard.

Because this new profile uses Intune’s unified settings format for device management, the profiles settings are also available through the settings catalog, and help to improve the reporting experience in the Intune admin center.

You can continue to use any instances of the following profile templates that you already have in place, but Intune no longer supports creating new instances of these profiles:

- **Identity protection** – previously available from *Devices* > *Configuration* > *Create* > *New Policy* > *Windows 10 and later* > *Templates* > *Identity Protection*
- **Account protection (Preview)** – previously available from *Endpoint Security* > *Account protection* > *Windows 10 and later* > *Account protection (Preview)*

Applies to:

- Windows 10
- Windows 11

#### New `operatingSystemVersion` filter property with new comparison operators (preview) <!-- 10033345 -->

There's a new `operatingSystemVersion` filter property. This property:

- Is in [public preview](public-preview.md) and still being developed. So, some features, like **Preview devices**, don't work yet.

- Should be used instead of the existing `OSVersion` property. The `OSVersion` property is being deprecated.

  When `operatingSystemVersion` is generally available (GA), the `OSVersion` property will retire, and you won't be able to create new filters using this property. Existing filters that use `OSVersion` continue to work.

- Has new comparison operators:

  - `GreaterThan`: Use for version value types.

    - Allowed values: `-gt` | `gt`
    - Example: `(device.operatingSystemVersion -gt 10.0.22000.1000)`

  - `GreaterThanOrEquals`: Use for version value types.

    - Allowed values: `-ge` | `ge`
    - Example: `(device.operatingSystemVersion -ge 10.0.22000.1000)`

  - `LessThan`: Use for version value types.

    - Allowed values: `-lt | lt`
    - Example: `(device.operatingSystemVersion -lt 10.0.22000.1000)`

  - `LessThanOrEquals`: Use for version value types.

    - Allowed values: `-le` | `le`
    - Example: `(device.operatingSystemVersion -le 10.0.22000.1000)`

For managed devices, `operatingSystemVersion` applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

For managed apps, `operatingSystemVersion` applies to:

- Android
- iOS/iPadOS
- Windows

For more information on filters and the device properties you can use, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Filter properties](filters-device-properties.md)

#### Government community cloud (GCC) support for Remote Help for macOS devices<!-- 25568551 -->

GCC customers can now use Remote Help for macOS devices on both web app and native application.

Applies to:

- macOS 12, 13 and 14

For more information, see:

- [Remote Help on macOS](../fundamentals/remote-help-macos.md)
- [Microsoft Intune for US Government GCC service description](../fundamentals/intune-govt-service-description.md)

### Device security

#### Updated security baseline for Windows 365 Cloud PC<!-- 26504698 -->

You can now deploy the Intune security baseline for **Windows 365 Cloud PC**. This new baseline is based on Windows **version 24H1**. This new baseline version uses the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

To view the new baselines included settings with their default configurations, see, [Windows 365 baseline settings version 24H1](../protect/security-baseline-settings-windows-365.md?pivots=win365-24h1).

### Intune apps

#### Newly available protected apps for Intune<!-- 28334000, 28157519, 28311088, 28156655, 28246919, 28246936 -->

The following protected apps are now available for Microsoft Intune:

- Asana: Work in one place (Android) by Asana, Inc.
- Goodnotes 6 (iOS) by Time Base Technology Limited
- Riskonnect Resilience by Riskonnect, Inc.
- Beakon Mobile App by Beakon Mobile Team
- HCSS Plans: Revision control (iOS) by Heavy Construction Systems Specialists, Inc.
- HCSS Field: Time, cost, safety (iOS) by Heavy Construction Systems Specialists, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).
## Week of July 22, 2024  

### Device enrollment  

#### Just-in-time registration and compliance remediation available for all iOS/iPadOS enrollments<!-- 27759589 -->  

You can now configure just-in-time (JIT) registration and JIT compliance remediation for all Apple iOS and iPadOS enrollments. These Intune-supported features improve the enrollment experience because they can take the place of the Intune Company Portal app for device registration and compliance checks. We recommend setting up JIT registration and compliance remediation for new enrollments, and to improve the experience for existing enrolled devices. For more information, see [Set up just in time registration in Microsoft Intune](../enrollment/set-up-just-in-time-registration.md).   

## Week of July 15, 2024

### Device management

#### New setting in the Device Control profile for Attack surface reduction policy<!-- 28761508 -->

We've added a new category and setting to the Device Control profile for the *Windows 10, Windows 11, and Windows Server* platform of Intune [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

The new setting is **Allow Storage Card**, and found in the new **System** category of the profile. This setting is also available from the Intune [settings catalog](../configuration/settings-catalog.md).

for the Windows devices.

This setting controls whether the user is allowed to use the storage card for device storage, and can prevent programmatic access to the storage card. For more information on this new setting, see [AllowStorageCard](/windows/client-management/mdm/policy-csp-system?branch=main&branchFallbackFrom=pr-en-us-15655&WT.mc_id=Portal-fx#allowstoragecard) in the Windows documentation.

## Week of July 8, 2024

### Device management

#### Copilot in Intune now has the device query feature using Kusto Query Language (KQL) (public preview)<!-- 24874816 -->
When you use Copilot in Intune, there's a new device query feature that uses KQL.
Use this feature to ask questions about your devices using a natural language. If device query can answer your question, Copilot generates the KQL query you can run to get the data you want.

To learn more about how you can currently use Copilot in Intune, see [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md).

### Monitor and Troubleshoot

#### New actions for policies, profiles, and apps<!-- 15283153 -->

You can now remove, reinstall, and reapply individual policies, profiles, and apps for iOS/iPadOS devices and Android corporate owned devices. You can apply these actions without changing assignments or group membership. These actions are intended to help resolve customer challenges that are external to Intune. Also, these actions can help to quickly restore end user productivity.

For more information, see [Remove apps and configuration](../remote-actions/remove-apps-config.md)

### App management

#### MAC address available from the Managed Home Screen app<!-- 25994454 -->

MAC address details are now available from the **Device Information** page of the Managed Home Screen (MHS) app. For information about MHS, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### New configuration capabilities for Managed Home Screen<!-- 25013268 -->

You can now configure Managed Home Screen (MHS) to enable a virtual app-switcher button that allows end users to easily navigate between apps on their kiosk devices from MHS. You can select between a floating or swipe-up app-switcher button. The configuration key is `virtual_app_switcher_type` and the possible values are `none`, `float`, and `swipe_up`. For information related to configuring the Managed Home Screen app, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

### Device enrollment

#### Update for Apple user and device enrollments with Company Portal <!-- 27557088 -->

We've made changes to the device registration process for Apple devices enrolling with Intune Company Portal. Previously, Microsoft Entra device registration occurred during enrollment. With this change, registration occurs after enrollment.

Existing enrolled devices are not affected by this change. For new user or device enrollments that utilize Company Portal, users must return to Company Portal to complete registration:

- For iOS users: Users with notifications enabled will be prompted to return to the Company Portal app for iOS. If they disable notifications, they won't be alerted, but still need to return to Company Portal to complete registration.

- For macOS devices: The Company Portal app for macOS will detect the installation of the management profile and automatically register the device, unless the user closes the app. If they close the app, they must reopen it to complete registration.

If you're using dynamic groups, which rely on device registration to work, it's important for users to complete device registration. Update your user guidance and admin documentation as needed. If you're using Conditional Access (CA) policies, no action is required. When users attempt to sign in to a CA-protected app, they will be prompted to return to Company Portal to complete registration. 

These changes are currently rolling out and will be made available to all Microsoft Intune tenants by the end of July. There's no change to the Company Portal user interface. For more information about device enrollment for Apple devices, see: 

- [Enrollment guide: Enroll macOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-macos.md#device-enrollment-end-user-tasks)
- [Enrollment guide: Enroll iOS and iPadOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-ios-ipados.md#user-and-device-enrollment-end-user-tasks)

## Week of June 24, 2024

### Device enrollment

#### Add corporate device identifiers for Windows<!-- 25873757 -->

Microsoft Intune now supports corporate device identifiers for devices running Windows 11, version 22H2 and later so that you can identify corporate machines ahead of enrollment. When a device that matches the model, manufacturer, and serial number criteria enrolls, Microsoft Intune will mark it as a corporate device and enable the appropriate management capabilities. For more information, see [Add corporate identifiers](../enrollment/corporate-identifiers-add.md).

## Week of June 17, 2024 (Service release 2406)

### Microsoft Intune Suite

#### Endpoint Privilege Management support for MSI and PowerShell file types<!-- 25230336 -->

Endpoint Privilege Management (EPM) *elevation rules* now support the elevation of Windows Installer and PowerShell files in addition to executable files that were previously supported. The new file extensions that EPM supports include:

- .msi
- .ps1

For information about using EPM, see [Endpoint Privilege Management](../protect/epm-overview.md).

#### View the certification authority key type in Microsoft Cloud PKI properties<!-- 27032276 -->

A new Microsoft Cloud PKI property called *CA keys* is available in the admin center and shows the type of certification authority keys used for signing and encryption. The property displays one of the following values:

- HSM: Indicates the use of a hardware security module-backed key.
- SW: Indicates the use of a software-backed key.

Certification authorities created with a licensed Intune Suite or Cloud PKI standalone add-on use HSM signing and encryption keys. Certification authorities created during a trial period use software-backed signing and encryption keys. For more information about Microsoft Cloud PKI, see [Overview of Microsoft Cloud PKI for Microsoft Intune](../protect/microsoft-cloud-pki-overview.md).

### App management

#### US GCC and GCC High support for Managed Home Screen<!-- 25827679 -->

Managed Home Screen (MHS) now supports sign-in for the US Government Community (GCC), US Government Community (GCC) High, and U.S. Department of Defense (DoD) environments. For more information, see [Configure the Managed Home Screen](../apps/app-configuration-managed-home-screen-app.md) and [Microsoft Intune for US Government GCC service description](../fundamentals/intune-govt-service-description.md).

Applies to:

- Android Enterprise

#### Updates to the Managed Apps report<!-- 26711898 -->

The Managed Apps report now provides details about Enterprise App Catalog apps for a specific device. For more information about this report, see [Managed Apps report](../fundamentals/reports.md#managed-apps-report-operational).

### Device configuration

#### New settings available in the Apple settings catalog <!--27175914 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Restrictions**:

- Allow Web Distribution App Installation

**System Configuration > Font**:

- Font
- Name

##### macOS

**Privacy > Privacy Preferences Policy Control**:

- Bluetooth Always

Applies to:

- iOS/iPadOS
- macOS

#### OS Version picker available for configuring managed iOS/iPadOS DDM software updates using the settings catalog<!-- 27565292 -->

Using the [Intune settings catalog](../configuration/settings-catalog.md), you can configure Apple's declarative device management (DDM) feature to manage software updates on iOS/iPadOS devices.

When you configure a managed software update policy using the settings catalog, you can:

- Select a target OS version from a list of updates made available by Apple.
- Manually enter the target OS version, if needed.

For more information about configuring managed software update profiles in Intune, see [Use the settings catalog to configure managed software updates](../protect/managed-software-updates-ios-macos.md).

Applies to:

- iOS/iPadOS

#### Intune admin center UI updates at Devices > By platform<!-- 25104008 -->

In the Intune admin center, you can select **Devices** > **By platform**, and view the policy options for the platform you select. These platform-specific pages are updated and include tabs for navigation.

For a walkthrough of the Intune admin center, see [Tutorial: Walkthrough Microsoft Intune admin center](tutorial-walkthrough-endpoint-manager.md).

### Device enrollment

### RBAC changes to enrollment platform restrictions for Windows<!-- 25036419 -->

We've updated role-based access controls (RBAC) for all enrollment platform restrictions in the Microsoft Intune admin center. The Global Administrator and Intune Service Administrator roles can create, edit, delete, and reprioritize enrollment platform restrictions. For all other built-in Intune roles, restrictions are read-only.

**Applies to:**

- Android
- Apple
- Windows 10/11

It's important to know that with these changes:

- Scope tag behavior doesn't change. You can apply and use scope tags as usual.
- If an assigned role or permission is currently preventing a user from viewing enrollment platform restrictions, nothing changes. The user will still be unable to view enrollment platform restrictions in the admin center.

For more information, see [Create device platform restrictions](../enrollment/create-device-platform-restrictions.md).

### Device management

### Updates to replace Wandera with Jamf is complete in the Intune admin center<!-- 26525211 -->

We've completed rebranding in the Microsoft Intune admin center to support replacing Wandera with Jamf. This includes updates to the name of the Mobile Threat Defense connector, which is now *Jamf*, and changes to the minimum required platforms to use the Jamf connector:

- Android 11 and later
- iOS / iPadOS 15.6 and later

For information about Jamf and other Mobile Threat Defense (MTD) vendors that Intune supports, see [Mobile Threat Defense partners](../protect/mobile-threat-defense.md).

### Intune apps

#### Newly available protected apps for Intune<!-- 28033401, 28035558, 27795962, 27795905, 27831146, 27795905 -->

The following protected apps are now available for Microsoft Intune:

- Atom Edge (iOS) by Arlanto GmbH
- HP Advance for Intune by HP Inc.
- IntraActive by Fellowmind
- Microsoft Azure (Android) by Microsoft Corporation
- Mobile Helix Link for Intune by Mobile Helix
- VPSX Print for Intune by Levi, Ray & Shoup, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md)

### Monitor and troubleshoot

#### View BitLocker recovery key in Company Portal apps for iOS and macOS<!-- 26615990 -->

End users can view the BitLocker recovery key for an enrolled Windows device and the FileVault recovery key for an enrolled Mac in the Company Portal app for iOS and Company Portal app for macOS. This capability will reduce helpdesk calls in the event the end user gets locked out of their corporate machines. End users can access the recovery key for an enrolled device by signing into the Company Portal app and selecting **Get recovery key**. This experience is similar to the recovery process on the Company Portal website, which also allows end users to see recovery keys.

You can prevent end users within your organization from accessing BitLocker recovery keys by configuring the **Restrict non-admin users from recovering the BitLocker keys for their owned device** setting in Microsoft Entra ID.

Applies to:

- macOS
- Windows 10/11

For more information, see:

- [Manage BitLocker policy for Windows devices with Intune](../protect/encrypt-devices.md)
- [Get recovery key for Windows](../user-help/get-recovery-key-windows.md)
- [Use FileVault disk encryption for macOS with Intune](../protect/encrypt-devices-filevault.md)
- [Get recovery key for Mac](../user-help/get-recovery-key-cpweb.md)
- [Manage device identities using the Microsoft Entra admin center](/entra/identity/devices/manage-device-identities#configure-device-settings)

### Role-based access control

#### New granular RBAC controls for Intune endpoint security<!-- 5475572 -->

We’ve begun to replace the role-based access control (RBAC) rights to endpoint security policies that are granted by the *Security baselines* permission with a series of more granular permissions for specific endpoint security tasks. This change can help you assign the specific rights your Intune admins require to do specific jobs instead of relying on either the [built-in](../fundamentals/role-based-access-control.md#built-in-roles) *Endpoint Security Manager* role or a [custom role](../fundamentals/create-custom-role.md) that includes the *Security baseline* permission. Prior to this change, the *Security baseline* permission grants rights across all endpoint security policies.

The following new RBAC permissions are available for endpoint security workloads:

- App Control for Business
- Attack surface reduction
- Endpoint detection and response

Each new permission supports the following rights for the related policy:

- Assign
- Create
- Delete
- Read
- Update
- View Reports

Each time we add a new granular permission for an endpoint security policy to Intune, those same rights are removed from the *Security baselines* permission. If you use custom roles with the *Security baselines* permission, the new RBAC permission is assigned automatically to your custom roles with the same rights that were granted through the *Security baseline* permission. This auto-assignment ensures your admins continue to have the same permissions they have today.

For more information about current RBAC permissions and built-in roles, see:

- [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md)
- [Built-in role permissions for Microsoft Intune](../fundamentals/role-based-access-control-reference.md)
- [Assign role-based access controls for endpoint security policy](../protect/endpoint-security-policy.md#assign-role-based-access-controls-for-endpoint-security-policy) in *Manage device security with endpoint security policies in Microsoft Intune*.

> [!IMPORTANT]
>
> With this release, the granular permission of **Antivirus** for endpoint security policies might be temporarily visible in some Tenants. This permission is not released and isn't supported for use. Configurations of the *Antivirus* permission are ignored by Intune. When *Antivirus* becomes available to use as a granular permission, it's availability will be announced in this [What's new in Microsoft Intune](../fundamentals/whats-new.md) article.

## Week of June 3, 2024

### Device enrollment

#### New enrollment time grouping feature for devices <!-- 16902437 -->

Enrollment time grouping is a new, faster way to group devices during enrollment. When it's configured, Intune adds devices to the appropriate group without requiring inventory discovery and dynamic membership evaluations. To set up enrollment time grouping, you must configure a static Microsoft Entra security group in each enrollment profile. After a device enrolls, Intune adds it to the static security group and delivers assigned apps and policies.

This feature is available for Windows 11 devices enrolling via Windows Autopilot device preparation. For more information, see [Enrollment time grouping in Microsoft Intune](../enrollment/enrollment-time-grouping.md).

## Week of May 27, 2024

### Microsoft Intune Suite

#### New primary endpoint for Remote Help

To improve the experience for [Remote Help](../fundamentals/remote-help.md) on Windows, Web, and macOS devices, we have updated the primary endpoint for Remote Help:

- Old primary endpoint: `https://remoteassistance.support.services.microsoft.com`
- New primary endpoint: `https://remotehelp.microsoft.com`

If you use Remote Help and have firewall rules that block the new primary endpoint, admins and users might experience connectivity issues or disruptions when using Remove Help.

To support the new primary endpoint on Windows devices, upgrade Remote Help to version 5.1.124.0. Web and macOS devices don't require an updated version of Remote Help to make use of the new primary endpoint.

Applies to:

- macOS 11, 12, 13 and 14
- Windows 10/11
- Windows 11 on ARM64 devices
- Windows 10 on ARM64 devices
- Windows 365

For information on the newest version of Remote Help, see the *March 13, 2024* entry for [What's New for Remote Help](../fundamentals/remote-help-windows.md#march-13-2024). For information about Intune endpoints for Remote Help, see [Remote Help](../fundamentals/intune-endpoints.md#remote-help) in *Network endpoints for Microsoft Intune*.

### Device management

### Evaluate compliance of Windows Subsystem for Linux (public preview)<!-- 24557103 -->

Now in a public preview, Microsoft Intune supports compliance checks for instances of Windows Subsystem for Linux (WSL) running on a Windows host device.

With this preview you can create a custom compliance script that evaluates the required distribution and version of WSL. WSL compliance results are included in the overall compliance state of the host device.

Applies to:

- Windows 10
- Windows 11

For information about this capability, see [Evaluate compliance of Windows Subsystem for Linux (public preview)](../protect/compliance-wsl.md).

## Week of May 20, 2024 (Service release 2405)

### Device configuration

#### New settings available in the macOS settings catalog<!-- 26970197 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the macOS Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

**Microsoft AutoUpdate (MAU)**:

- Microsoft Teams (work or school)
- Microsoft Teams classic

**Microsoft Defender > Features**:

- Use Data Loss Prevention
- Use System Extensions

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:

- macOS

### Device enrollment

#### Stage Android device enrollment to reduce end-user steps<!-- 15503468 -->

To reduce the enrollment time for end users, Microsoft Intune supports device staging for Android Enterprise devices. With *device staging*, you can stage an enrollment profile and complete all related enrollment steps for workers receiving these devices:

- Corporate-owned fully managed devices
- Corporate-owned devices with a work profile

When frontline workers receive the devices, all they have to do is connect to Wi-Fi and sign in to their work account. A new *device staging token* is required to enable this feature. For more information, see [Device staging overview](../enrollment/device-staging-overview.md).

### Device management

#### End user access to BitLocker Recovery Keys for enrolled Windows devices<!-- 8077173 -->

End users can now view the BitLocker Recovery Key for enrolled Windows devices from the Company Portal website. This capability can reduce helpdesk calls in the event the end user gets locked out of their corporate machines. End users can access the recovery key for an enrolled device by signing into the Company Portal website and selecting **Show recovery key**. This experience is similar to the MyAccount website, which also allows end users to see recovery keys.

You can prevent end users within your organization from accessing BitLocker recovery keys by configuring the Entra ID toggle **Restrict non-admin users from recovering the BitLocker key(s) for their owned device**.

For more information, see:

- [Manage device identities using the Microsoft Entra admin center](/entra/identity/devices/manage-device-identities#configure-device-settings)
- [Get recovery key for Windows](../user-help/get-recovery-key-windows.md)
- [Manage BitLocker policy for Windows devices with Intune](../protect/encrypt-devices.md)

#### New version of Windows hardware attestation report<!-- 15425680 -->

We've released a new version of the Windows hardware attestation report that shows the value of settings attested by Device Health Attestation and Microsoft Azure Attestation for Windows 10/11. The Windows hardware attestation report is built on a new reporting infrastructure, and reports on new settings added to Microsoft Azure Attestation. The report is available in the admin center under **Reports** > **Device Compliance** > **Reports**.

For more information, see [Intune reports](reports.md#windows-hardware-attestation-report-organizational).

The Windows health attestation report previously available under **Devices** > **Monitor** has been retired.

Applies to:

- Windows 10
- Windows 11

#### Optional Feature updates<!--12769586 -->

Feature updates can now be made available to end users as **Optional** updates, with the introduction of **Optional** Feature updates. End users will see the update in the **Windows Update** settings page in the same way that it's shown for consumer devices.

End users can easily opt in to try out the next Feature update and provide feedback. When it's time to roll out the feature as a **Required** update, then admins can change the setting on the policy, and update the rollout settings so that the update is deployed as a **Required** update to devices that do not yet have it installed.

For more information on Optional Feature updates, see [Feature updates for Windows 10 and later policy in Intune](..//protect/windows-10-feature-updates.md#create-and-assign-feature-updates-for-windows-10-and-later-policy).

Applies to:

- Windows 10
- Windows 11

### Device security

#### Updated security baseline for Microsoft Defender for Endpoint<!-- 26504935 -->

You can now deploy the Intune security baseline for **Microsoft Defender for Endpoint**. The new baseline, **version 24H1**, uses the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

### Intune apps

#### Newly available protected apps for Intune<!-- 27575008, 27575336 -->

The following protected apps are now available for Microsoft Intune:

- Fellow.app by Fellow Insights Inc
- Unique Moments by Unique AG

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of May 6, 2024

### Device management

#### Intune and the macOS Company Portal app support Platform SSO (public preview)<!-- 24325427 -->

On Apple devices, you can use Microsoft Intune and the Microsoft Enterprise SSO plug-in to configure single sign-on (SSO) for apps and websites that support Microsoft Entra authentication, including Microsoft 365.

On macOS devices, Platform SSO is available in public preview. Platform SSO expands the SSO app extension by allowing you to configure different authentication methods, simplify the sign-in process for users, and reduce the number of passwords they need to remember.

Platform SSO is included in the Company Portal app version 5.2404.0 and newer.

For more information on Platform SSO and to get started, see:

- [Configure Platform SSO for macOS devices in Microsoft Intune](../configuration/platform-sso-macos.md)
- [Single sign-on (SSO) overview and options for Apple devices in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)

Applies to:

- macOS 13 and later

### Tenant administration

#### Customize your Intune admin center experience<!-- 24155584 -->

You can now customize your Intune admin center experience by using collapsible navigation and favorites. The left navigation menus in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) are updated to support expanding and collapsing each subsection of the menu. In addition, you can set admin center pages as favorites. This portal capability will gradually roll out over the next week.

By default, menu sections are expanded. You can choose your portal menu behavior by selecting the **Settings** gear icon at the top right to display the **Portal settings**. Then, select **Appearance + startup views** and set the **Service menu behavior** to **Collapsed** or **Expanded** as the default portal option. Each menu section retains the expanded or collapsed state that you choose. Additionally, selecting the star icon next to a page on the left navigation adds the page to a **Favorites** section near the top of the menu.

For related information, see [Change the Portal settings](../fundamentals/tutorial-walkthrough-endpoint-manager.md#change-the-portal-settings).

## Week of April 29, 2024

### App management

#### Updates to the Managed Home Screen experience<!-- 24990268 -->

We recently released and improved the Managed Home Screen experience, which is now Generally Available. The app has been redesigned to improve the core workflows throughout the application. The updated design offers a more usable and supportable experience.

With the release, we stop investing in previous Managed Home Screen workflows. New features and fixes for Managed Home Screen are only added to the new experience. During August 2024, the new experience will automatically be enabled for all devices.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md) and [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

#### Require end users to enter PIN to resume activity on Managed Home Screen<!-- 9322838 -->

In Intune, you can require end users to enter their session PIN to resume activity on Managed Home Screen after the device is inactive for a specified period of time. Set the **Minimum inactive time before session PIN is required** setting to the number of seconds the device is inactive before the end user must input their session PIN.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Device IPv4 and IPv6 details available from Managed Home Screen<!-- 25994445 -->

IPv4 and IPv6 connectivity details are now both available from the **Device Information** page of the Managed Home Screen app. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](..\remote-actions\collect-diagnostics.md).

#### Updates to Managed Home Screen sign-in support<!-- 25597636 -->

Managed Home Screen now supports domainless sign-in. Admins can configure a domain name, which will be automatically appended to usernames upon sign-in. Also, Managed Home Screen supports a custom login hint text to be displayed to users during the sign-in process.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md) and [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

#### Allow end users to control Android Enterprise device auto-rotation<!-- 9322838 -->

In Intune, you can now expose a setting in the Managed Home Screen app that allows the end user to turn on and off the device's auto-rotation. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Allow end users to adjust Android Enterprise device screen brightness<!-- 9322834 -->

In Intune, you can expose settings in the Managed Home Screen app to adjust screen brightness for Android Enterprise devices. You can choose to expose a setting in the app to allow end users to access a brightness slider to adjust the device screen brightness. Also, you can expose a setting to allow end users to toggle adaptive brightness.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Migrated to .NET MAUI from Xamarin<!-- 27143739 -->

Xamarin.Forms has evolved into .NET Multi-platform App UI (MAUI). Existing Xamarin projects should be migrated to .NET MAUI. For more information about upgrading Xamarin projects to .NET, see the [Upgrade from Xamarin to .NET & .NET MAUI](/dotnet/maui/migration/?WT.mc_id=dotnet-35129-website) documentation.

Xamarin support ended as of May 1, 2024 for all Xamarin SDKs including Xamarin.Forms and Intune App SDK Xamarin Bindings. For Intune support on Android and iOS platforms, see [Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android)and [Microsoft Intune App SDK for MAUI.iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).

## Week of April 22, 2024 (Service release 2404)

### App management

#### Auto update available with Win32 app supersedence<!-- 17644510 -->

Win32 app supersedence provides the capability to supersede apps deployed as available with **auto-update** intent. For example, if you deploy a Win32 app (app A) as available and installed by users on their device, you can create a new Win32 app (app B) to supersede app A using **auto-update**. All targeted devices and users with app A installed as available from the Company Portal are superseded with app B. Also, only app B shows in the Company Portal. You can find the **auto-update** feature for available app supersedence as a toggle under the **Available assignment** in the **Assignments** tab.

For more information about app supersedence, see [Add Win32 app supersedence](../apps/apps-win32-supersedence.md).

### Device configuration

#### Error message is shown when OEMConfig policy exceeds 500 KB on Android Enterprise devices<!-- 15326924 -->

On Android Enterprise devices, you can use an OEMConfig device configuration profile to add, create and/or customize OEM specific settings.

When you create an OEMConfig policy that exceeds 500 KB, then the following error is shown in the Intune admin center:

`Profile is larger than 500KB. Adjust profile settings to decrease the size.`

Previously, OEMConfig policies that exceeded 500 KB were shown as pending.

For more information on OEMConfig profiles, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:

- Android Enterprise

### Device security

#### Windows Firewall CSP changes for processing Firewall Rules<!-- 10734904 -->

Windows changed how the Firewall configuration service provider (CSP) enforces rules from Atomic blocks of firewall rules. The Windows Firewall CSP on a device implements the firewall rule settings from your [Intune endpoint security Firewall policies](../protect/endpoint-security-firewall-policy.md). The change of CSP behavior now enforces an all-or-nothing application of firewall rules from each Atomic block of rules.

- Previously, the CSP on a device would go through the firewall rules in an Atomic block of rules - one rule (or setting) at a time with the goal of applying all the rules in that Atomic block, or none of them. If the CSP encountered any issue with applying any rule from the block to the device, the CSP wouldn't only stop that rule, but also cease to process subsequent rules without trying to apply them. However, rules that applied successfully before a rule failed, would remain applied to the device. This behavior can lead to a partial deployment of firewall rules on a device, since the rules that were applied before a rule failed to apply aren't reversed.

- With the change to the Firewall CSP, when any rule in the block is unsuccessful in applying to the device, all the rules from that same Atomic block that were applied successfully are rolled back. This behavior ensures the desired all-or-nothing behavior is implemented and prevents a partial deployment of firewall rules from that block. For example, if a device receives an Atomic block of firewall rules that has a misconfigured rule that can't apply, or has a rule that isn't compatible with the devices operating system, then the CSP fails all the rules from that block, And, it rolls back any rules that applied to that device.

This change of Firewall CSP behavior is available on devices that run the following Windows versions or later:

- Windows 11 21H2
- Windows 11 22H2
- Windows 10 21H2

For more information on the subject of how the Windows Firewall CSP uses Atomic blocks to contain firewall rules, see the note near the top of [Firewall CSP](/windows/client-management/mdm/firewall-csp) in the Windows documentation.

For troubleshooting guidance, see the Intune support blog [How to trace and troubleshoot the Intune Endpoint Security Firewall rule creation process](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-trace-and-troubleshoot-the-intune-endpoint-security/ba-p/3261452).

#### CrowdStrike – New mobile threat defense partner<!-- 16882021 -->

We added [CrowdStrike Falcon](../protect/crowdstrike-falcon-defense-connector.md) as an integrated Mobile Threat Defense (MTD) partner with Intune. By configuring the CrowdStrike connector in Intune, you can control mobile device access to corporate resources using Conditional Access that's based on risk assessment in your compliance policies.

With the Intune 2404 service release, the CrowdStrike connector is now available in the admin center. However, it isn't useable until CrowdStrike publishes the required App Configuration profile details necessary to support iOS and Android devices. The profile details are expected sometime after second week of May.

### Intune apps

#### Newly available protected apps for Intune<!-- 26825160, 26954999, 26891466, 27184602 -->

The following protected apps are now available for Microsoft Intune:

- Asana: Work in one place by Asana, Inc.
- Freshservice for Intune by Freshworks, Inc.
- Kofax Power PDF Mobile by Tungsten Automation Corporation
- Remote Desktop by Microsoft Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Windows update distribution report<!--16579592 -->

The Windows update distribution report in Intune provides a summarized report. This report shows:

- The number of devices that are on each quality update level.
- The percentage of coverage for each update across Intune managed devices, including co-managed devices.

You can drill down further in the report for each quality update that aggregates devices based on the Windows 10/11 feature version and the update statuses.

Finally, the admins can get the list of devices that aggregate to the numbers shown in the previous two reports, which can also be exported and used for troubleshooting and analysis along with the Windows Update for business reports.

For more information on Windows update distribution reports, see [Windows Update reports on Intune](../protect/windows-update-reports.md#windows-update-distribution-report).

Applies to:

- Windows 10
- Windows 11

#### Intune support of Microsoft 365 remote application diagnostics<!-- 17409991 -->

The Microsoft 365 remote application diagnostics allows Intune admins to request Intune app protection logs and Microsoft 365 application logs (where applicable) directly from the Intune console. You can find this report in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot** > *select a user* > **Summary** > *App protection**. This feature is exclusive to applications that are under Intune app protection management. If supported, the application specific logs are gathered and stored within dedicated storage solutions for each application.

For more information, see [Collect diagnostics from an Intune managed device](../remote-actions/collect-diagnostics.md).

#### Remote Help supports full control of a macOS device<!--22985205 -->

Remote Help now supports helpdesk connecting to a user's device and requesting full control of the macOS device.

For more information, see:

- [Remote Help on macOS](../fundamentals/remote-help-macos.md)
- [Remote Help Web App](../fundamentals/remote-help-webapp.md)

Applies to:

- macOS 12, 13 and 14

## Week of April 15, 2024

### Intune apps

#### Newly available protected app for Intune<!-- 26740168 -->

The following protected app is now available for Microsoft Intune:

- Atom Edge by Arlanto Apps

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of April 1, 2024

### Device management

#### Copilot in Intune is available in the Intune admin center (public preview)<!-- 24105429 26122887 24205474 24205510 24205460 26113632-->

Copilot in Intune is integrated in the Intune admin center, and can help you get information quickly. You can use Copilot in Intune for the following tasks:

✅ **Copilot can help you manage your settings and policies**

- **Copilot tooltip on settings**: When you add settings to a policy or review settings in an existing policy, there's a new Copilot tooltip. When you select the tooltip, you get AI generated guidance based on Microsoft content and recommendations. You can see what each setting does, how the setting works, any recommended values, if the setting is configured in another policy, and more.

- **Policy summarizer**: On existing policies, you get a Copilot summary of the policy. The summary describes what the policy does, the users and groups assigned to the policy, and the settings in the policy. This feature can help you understand the impact of a policy and its settings on your users and devices.

✅ **Copilot shows device details and can help troubleshoot**

- **All about a device**: On a device, you can use Copilot to get key information about the device, including its properties, configuration, and status information.

- **Device compare**: Use Copilot to compare the hardware properties and device configurations of two devices. This feature helps you determine what's different between two devices with similar configurations, especially when troubleshooting.

- **Error code analyzer**: Use Copilot in the device view to analyze an error code. This feature helps you understand what the error means and provides a potential resolution.

✅ **Intune capabilities in Copilot for Security**

Intune has capabilities available in the Copilot for Security portal. SOC Analysts and IT admins can use these capabilities to get more information on policies, devices, group membership, and more. On a single device, you can get more specific information that's unique to Intune, like compliance status, device type, and more.

You can also ask Copilot to tell you about a user's devices and get a quick summary of critical information. For example, the output shows links to the user's devices in Intune, device ID, enrollment date, last check-in date, and compliance status. If you're an IT admin and reviewing a user, then this data provides a quick summary.

As a SOC analyst that's investigating a suspicious or potentially compromised user or device, information like enrollment date and last check-in can help you make informed decisions.

For more information on these features, see:

- [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md)
- [Access your Microsoft Intune data in Copilot for Security](../copilot/security-copilot.md)

Applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

#### GCC customers can use Remote Help for Windows and Android devices<!-- 10613615 25825071-->

The [Microsoft Intune Suite](intune-add-ons.md) includes advanced endpoint management and security features, including Remote Help.

On Windows and enrolled Android Enterprise dedicated devices, you can use remote help on US Government GCC environments.

For more information on these features, see:

- [Microsoft Intune for US Government GCC service description](intune-govt-service-description.md)
- [Use Remote Help with Microsoft Intune](remote-help.md)

Applies to:

- Windows 10/11
- Windows 10/11 on ARM64 devices
- Windows 365
- Samsung and Zebra devices enrolled as Android Enterprise dedicated devices

### Device configuration

#### New BIOS device configuration profile for OEMs<!-- 9278502 -->

There's a new **BIOS configuration and other settings** device configuration policy for OEMs. Admins can use this new policy to enable or disable different BIOS features that secure device. In the Intune device configuration policy, you add the BIOS configuration file, deploy a Win32 app, and then assign the policy to your devices.

For example, admins can use the [Dell Command tool](https://www.dell.com/support/kbdoc/000108963/how-to-use-and-troubleshoot-dell-command-update-to-update-all-drivers-bios-and-firmware-for-your-system) (opens Dell's website) to create the BIOS configuration file. Then, they add this file to the new Intune policy.

For more information on this feature, see [Use BIOS configuration profiles on Windows devices in Microsoft Intune](../configuration/bios-configuration.md).

Applies to

- Windows 10 and later

## Week of March 25, 2024 (Service release 2403)

### Microsoft Intune Suite

#### New elevation type for Endpoint Privilege Management<!-- 25230692 wndraft wnready-->

Endpoint Privilege Management has a new file elevation type, **support approved**. Endpoint Privilege Management is a feature component of the Microsoft Intune Suite and is also available as a standalone [Intune add-on](../fundamentals/intune-add-ons.md).

A support-approved elevation gives you a third option for both the default elevation response and the elevation type for each rule. Unlike automatic or user confirmed, a support-approved elevation request requires Intune administrators to manage which files can run as elevated on a case-by-case basis.

With support approved elevations, users can request approval to elevate an application that isn't explicitly allowed for elevation by automatic or user approved rules. This takes the form of an elevation request that must be reviewed by an Intune administrator who can approve or deny the elevation request.

When the request is approved, users are notified that the application can now be run as elevated, and they have 24 hours from the time of approval to do so before the elevation approval expires.

Applies to:

- Windows 10
- Windows 11

For more information on this new capability, see [Support approved elevation requests](../protect/epm-support-approved.md).

### App management

#### Extended capabilities for Managed Google Play apps on personally owned Android devices with a work profile<!-- 26554642 -->

There are new capabilities extended to work profile devices. The following capabilities were previously available only on corporate-owned devices:

- **Available apps for device groups**: You can use Intune to make apps available for device groups through the Managed Google Play store. Previously, apps could only be made available to user groups.

- **Update priority setting**: You can use Intune to configure the app update priority on devices with a work profile. To learn more about this setting, see [Update a Managed Google Play app](../apps/apps-add-android-for-work.md#update-a-managed-google-play-app).

- **Required apps display as available in Managed Google Play**: You can use Intune to make required apps available for users through the Managed Google Play store. Apps that are part of existing policies now display as available.

These new capabilities will follow a phased rollout over multiple months.

Applies to:

- Android Enterprise personally owned devices with a work profile

### Device configuration

#### New settings available in the Apple settings catalog<!-- 26551582 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Declarative Device Management (DDM) > Passcode**:

- Maximum Passcode Age In Days
- Minimum Complex Characters
- Require Alphanumeric Passcode

**Restrictions**:

- Allow Marketplace App Installation

##### macOS

**Declarative Device Management (DDM) > Passcode**:

- Change At Next Auth
- Custom Regex
- Failed Attempts Reset In Minutes
- Maximum Passcode Age In Days
- Minimum Complex Characters
- Require Alphanumeric Passcode

**Full Disk Encryption > FileVault**:

- Recovery Key Rotation In Months

#### New settings available in the Windows settings catalog<!-- 26763724, 26170998, + 26801723 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

- **Delivery optimization**:

  - **DO Disallow Cache Server Downloads On VPN** - This setting blocks downloads from Microsoft Connected Cache servers when the device connects using VPN. By default, the device is allowed to download from Microsoft Connected Cache when connected using VPN.

  - **DO Set Hours To Limit Background Download Bandwidth** - This setting specifies the maximum background download bandwidth. Delivery Optimization uses this bandwidth during and outside business hours across all concurrent download activities as a percentage of available download bandwidth.

  - **DO Set Hours To Limit Foreground Download Bandwidth** - This setting specifies the maximum foreground download bandwidth. Delivery Optimization uses this bandwidth during and outside business hours across all concurrent download activities as a percentage of available download bandwidth.

  - **DO Vpn Keywords** - This policy allows you to set one or more keywords used to recognize VPN connections.

- **Messaging**:

  - **Allow Message Sync** - This policy setting allows the backup and restore of cellular text messages to Microsoft's cloud services.

- **Microsoft Defender Antivirus**:

  - **Specify the maximum depth to scan archive files**
  - **Specify the maximum size of archive files to be scanned**

For more information on these settings, see:

- [Policy CSP - DeliveryOptimization](/windows/client-management/mdm/policy-csp-deliveryoptimization)
- [Policy CSP - Messaging](/windows/client-management/mdm/policy-csp-messaging#allowmessagesync)
- [Policy CSP - ADMX_MicrosoftDefenderAntivirus](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus)

Applies to:

- Windows 10 and later

#### New archive file scan settings added to Antivirus policy for Windows devices<!-- 26801723 -->

We added the following two settings to the *Microsoft Defender Antivirus* profile for [endpoint security Antivirus policy](../protect/endpoint-security-antivirus-policy.md#antivirus-profiles) that apply to Windows 10 and Windows 11 devices:

- [Specify the maximum depth to scan archive files](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#scan_archivemaxdepth) - This setting allows you to configure the maximum directory depth level into which archive files such as .ZIP or .CAB are unpacked during scanning.
- [Specify the maximum size of archive files to be scanned](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#scan_archivemaxsize) - This setting allows you to configure the maximum size of archive files such as .ZIP or .CAB that are scanned. The value represents file size in kilobytes (KB).

With Antivirus policy, you can manage these settings on devices enrolled by Intune and on devices managed through the [Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.

Both settings are also available in the [settings catalog](../configuration/settings-catalog.md) at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type > **Defender**.

Applies to:

- Windows 10
- Windows 11

#### Updates to assignment filters<!-- 12798031, 24801139 -->

You can use [Intune assignment filters](filters.md) to assign a policy based on rules you create.

Now, you can:

- Use managed app assignment filters for Window MAM app protection policies and app configuration policies.
- Filter your existing assignment filters by **Platform**, and by the **Managed apps** or **Managed devices** filter type. When you have many filters, this feature makes it easier to find specific filters you created.

For more information on these features, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Data protection for Windows MAM](../apps/protect-mam-windows.md)

This feature applies to:

- **Managed devices** on the following platforms:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows 10/11

- **Managed apps** on the following platforms:

  - Android
  - iOS/iPadOS
  - Windows

### Device management

#### New compliance setting lets you verify device integrity using hardware-backed security features<!-- 12391862 -->

A new compliance setting called **Check strong integrity using hardware-backed security features** lets you verify device integrity using hardware-backed key attestation. If you configure this setting, strong integrity attestation is added to Google Play's integrity verdict evaluation. Devices must meet device integrity to remain compliant. Microsoft Intune marks devices that don't support this type of integrity check as noncompliant.

This setting is available in profiles for Android Enterprise fully managed, dedicated, and corporate-owned work profile, under **Device Health** > **Google Play Protect**. It only becomes available when the Play integrity verdict policy in your profile is set to **Check basic integrity** or **Check basic integrity & device integrity**.

Applies to:

- Android Enterprise

For more information, see [Device compliance - Google Play Protect](../protect/compliance-policy-create-android-for-work.md#google-play-protect).

#### New compliance settings for Android work profile, personal devices<!-- 24743927 -->

Now you can add compliance requirements for work profile passwords without impacting device passwords. All new Microsoft Intune settings are available in compliance profiles for Android Enterprise personally owned work profiles under **System Security** > **Work Profile Security**, and include:

- Require a password to unlock work profile
- Number of days until password expires
- Number of previous passwords to prevent reuse
- Maximum minutes of inactivity before password is required
- Password complexity
- Required password type
- Minimum password length

If a work profile password fails to meet requirements, Company Portal marks the device as noncompliant. Intune compliance settings take precedence over the respective settings in an Intune device configuration profile. For example, the password complexity in your compliance profile is set to *medium*. The password complexity in a device configuration profile is set to *high*. Intune prioritizes and enforces the compliance policy.

Applies to:

- Android Enterprise personally owned devices with a work profile

For more information, see [Compliance settings - Android Enterprise](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile).

#### Windows quality updates support for expediting non-security updates<!-- 17614146 -->

Windows quality updates now support expediting non-security updates for those times when a quality fix needs to be deployed faster than the normal quality update settings.

Applies to:

- Windows 11 devices

For more information about installing an expedited update, see [Expedite Windows quality updates in Microsoft Intune](../protect/windows-10-expedite-updates.md#create-and-assign-an-expedited-quality-update).

#### Introducing a remote action to pause the config refresh enforcement interval<!--24249019 -->

In the Windows Settings Catalog, you can configure **Configuration Refresh**. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check in to Intune. The device will replay and re-enforce settings based on previously received policy to minimize the chance for configuration drift.

To support this feature, a remote action is added to allow a pause in action. If an admin needs to make changes or run remediation on a device for troubleshooting or maintenance, they can issue a pause from Intune for a specified period. When the period expires, settings are enforced again.

The remote action **Pause configuration refresh** can be accessed from the device summary page.

For more information, see:

- [Remote actions](../remote-actions/device-management.md)
- [Pause Config Refresh Remote action](../remote-actions/pause-config-refresh.md)

### Device security

#### Updated security baseline for Windows version 23H2<!-- 25021947 -->

You can now deploy the Intune security baseline for Windows version 23H2. This new baseline is based on the **version 23H2** of the Group Policy security baseline found in the [Security Compliance Toolkit and Baselines](https://www.microsoft.com/en-us/download/details.aspx?id=55319) from the Microsoft Download Center, and includes only the settings that are applicable to devices managed through Intune. Use of this updated baseline can help you maintain best-practice configurations for your Windows devices.

This baseline uses the unified settings platform seen in the Settings Catalog. It features an improved user interface and reporting experience, consistency and accuracy improvements related to setting tattooing, and can support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

To view the new baselines included settings with their default configurations, see, [Windows MDM security baseline version 23H2](../protect/security-baseline-settings-mdm-all.md?pivots=mdm-23h2).

#### Use a rootless implementation of Podman to host Microsoft Tunnel<!-- 24836716 -->

When prerequisites are met, you can use a rootless Podman container to host a Microsoft Tunnel server. This capability is available when you use [Podman for Red Hat Enterprise Linux (RHEL)](../protect/microsoft-tunnel-prerequisites.md#linux-server) version 8.8 or later, to host Microsoft Tunnel.

When using a rootless Podman container, the mstunnel services run under a non-privileged service user. This implementation can help limit impact from a container escape. To use a rootless Podman container, you must start the tunnel installation script using a modified command line.

For more information about this Microsoft Tunnel install option, see [Use a rootless Podman container](../protect/microsoft-tunnel-configure.md#use-a-rootless-podman-container).

#### Improvements for Intune deployments of Microsoft Defender for Endpoint<!-- 26314441 -->

We improved and simplified the experience, workflow, and report details for onboarding devices to Microsoft Defender when using Intune's endpoint detection and response (EDR) policy. These changes apply for Windows devices managed by Intune and by the tenant-attach scenario. These improvements include:

- Changes to the EDR node, dashboards, and reports to improve the visibility of your Defender EDR deployment numbers. See [About the endpoint detection and response node](../protect/endpoint-security-edr-policy.md#about-the-endpoint-detection-and-response-node).

- A new tenant-wide option to deploy a preconfigured EDR policy that streamlines the deployment of Defender for Endpoint to applicable Windows devices. See [Use a preconfigured EDR policy](../protect/endpoint-security-edr-policy.md#use-a-preconfigured-edr-policy).

- Changes to Intune's the Overview page of the endpoint security node. These changes provide a consolidated view of reports for the device signals from Defender for Endpoint on your managed devices. See [Use a preconfigured EDR policy](../protect/endpoint-security-edr-policy.md#use-a-preconfigured-edr-policy).

These changes apply to the Endpoint security and endpoint detection and response nodes of the admin center, and the following device platforms:

- Windows 10
- Windows 11

#### Windows quality updates support expediting non-security updates<!-- 17614146 -->

Windows quality updates now support expediting non-security updates for those times when a quality fix needs to be deployed faster than the normal quality update settings.

Applies to:

- Windows 11 devices

For more information about installing an expedited update, see [Expedite Windows quality updates in Microsoft Intune](../protect/windows-10-expedite-updates.md#create-and-assign-an-expedited-quality-update).

### Intune apps

#### Newly available protected apps for Intune<!-- 26677733, 26711918, 26763096, 26763121 -->

The following protected apps are now available for Microsoft Intune:

- Cerby by Cerby, Inc.
- OfficeMail Go by 9Folders, Inc.
- DealCloud by Intapp, Inc.
- Intapp 2.0 by Intapp, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of March 3, 2024

### Device enrollment

#### Role-based access control changes to enrollment settings for Windows Hello for Business<!-- 25661866 -->

We updated Role-based access control (RBAC) in the enrollment area for Windows Hello for Business. Enrollment settings related to Windows Hello for Business are read-only for all roles except the Intune Service Administrator. The Intune Service Administrator can create and edit Windows Hello for Business enrollment settings.

For more information, see [Role-based access control](../protect/windows-hello.md#role-based-access-control) in the *Windows Hello at device enrollment* article.

### Device security

#### New enrollment configuration for Windows Hello for Business<!-- 9601416 -->

A new Windows Hello for Business enrollment setting, **Enable enhanced sign in security** is available in the Intune admin center. Enhanced sign-in security is a Windows Hello feature that prevents malicious users from gaining access to a user's biometrics through external peripherals.

For more information about this setting, see [Create a Windows Hello for Business policy](../protect/windows-hello.md).

#### HTML formatting supported in noncompliance email notifications<!-- 24197255 -->

Intune now supports HTML formatting in noncompliance email notifications for all platforms. You can use supported HTML tags to add formatting such as italics, URL links, and bulleted lists to your organization's messages.

For more information, see [Create a notification message template](../protect/actions-for-noncompliance.md#create-a-notification-message-template).

## Week of February 26, 2024

### Microsoft Intune Suite

#### New Microsoft Cloud PKI service<!-- 17272901 -->

Use the Microsoft Cloud PKI service to simplify and automate certificate lifecycle management for Intune-managed devices. ​Microsoft Cloud PKI is a feature component of the Microsoft Intune Suite and is also available as a standalone [Intune add-on](../fundamentals/intune-add-ons.md). The cloud-based service provides a dedicated PKI infrastructure for your organization, and doesn't require on-premises servers, connectors, or hardware. Microsoft Cloud PKI automatically issues, renews, and revokes certificates for all OS platforms supporting the SCEP certificate device configuration profile. Issued certificates can be used for certificate-based authentication for Wi-Fi, VPN, and other services supporting certificate-based authentication. For more information, see [Overview of Microsoft Cloud PKI](../protect/microsoft-cloud-pki-overview.md).

Applies to:

- Windows
- Android
- iOS/iPadOS
- macOS

### Intune apps

#### Newly available protected app for Intune<!-- 26607121 -->

The following protected app is now available for Microsoft Intune:

- Cinebody by Super 6 LLC

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of February 19, 2024 (Service release 2402)

### App management

#### More app configuration permissions for Android apps<!-- 25115278 -->

There are six new permissions that can be configured for an Android app using an app configuration policy. They are:

- Allow background body sensor data
- Media Video (read)
- Media Images (read)
- Media Audio (read)
- Nearby Wifi Devices
- Nearby Devices

For more information about how to use app config policies for Android apps, see [Add app configuration policies for managed Android Enterprise devices](../apps/app-configuration-policies-use-android.md).

#### Newly available protected apps for Intune<!-- 26607067, 26607087, 26632132 -->

The following protected apps are now available for Microsoft Intune:

- Bob HR by Hi Bob Ltd
- ePRINTit SaaS by ePRINTit USA LLC
- Microsoft Copilot by Microsoft Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

#### Update to Intune Management Extension on Windows<!-- 26472055 -->

To support expanded functionality and bug fixes, use .NET Framework 4.7.2 or higher with the Intune Management Extension on Windows clients. If a Windows client continues to use an earlier version of the .NET Framework, the Intune Management Extension continues to function. The .NET Framework 4.7.2 is available from Windows Update as of July 10, 2018, which is included in Windows 10 1809 (RS5) and newer. Multiple versions of the .NET Framework can coexist on a device.

Applies to:

- Windows 10
- Windows 11

### Device configuration

#### Use assignment filters on Endpoint Privilege Management (EPM) policies<!-- 25230705 -->

You can use assignment filters to assign a policy based on rules you create. A filter allows you to narrow the assignment scope of a policy, like targeting devices with a specific OS version or a specific manufacturer.

You can use filters on Endpoint Privilege Management (EPM) policies.

For more information, see:

- [Use filters when assigning your apps, policies, and profiles in Intune](filters.md)
- [List of platforms, policies, and app types supported by filters in Intune](filters-supported-workloads.md)

Applies to:

- Windows 10
- Windows 11

#### New settings available in the Apple settings catalog<!-- 25280353 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

- **Restrictions**

  - Allow Live Voicemail
  - Force Classroom Unprompted Screen Observation
  - Force Preserve ESIM On Erase

##### macOS

- **Full Disk Encryption > FileVault** > Force Enable In Setup Assistant
- **Restrictions** > Force Classroom Unprompted Screen Observation

For more information, see:

- [Use FileVault disk encryption for macOS with Intune](../protect/encrypt-devices-filevault.md)
- [Create a policy using settings catalog](../configuration/settings-catalog.md)

#### Import up to 20 custom ADMX and ADML administrative templates<!-- 25780608 -->

You can import custom ADMX and ADML administrative templates in Microsoft Intune. Previously, you could import up to 10 files. Now, you can upload up to 20 files.

Applies to:

- Windows 10
- Windows 11

For more information on this feature, see [Import custom ADMX and ADML administrative templates into Microsoft Intune (public preview)](../configuration/administrative-templates-import-custom.md).

#### New setting for updating MAC address randomization on Android Enterprise devices<!-- 24259789 -->

There's a new **MAC address randomization** setting on Android Enterprise devices (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Wi-Fi** for profile type).

Starting with Android 10, when connecting to a network, devices present a randomized MAC address instead of the physical MAC address. Using randomized MAC addresses is recommended for privacy, as it's harder to track a device by its MAC address. However, randomized MAC addresses break functionality that relies on a static MAC address, including network access control (NAC).

Your options:

- **Use device default**: Intune doesn't change or update this setting. By default, when connecting to a network, devices present a randomized MAC address instead of the physical MAC address. Any updates made by the user to the setting persist.

- **Use randomized MAC**: Enables MAC address randomization on devices. When devices connect to a new network, devices present a randomized MAC address, instead of the physical MAC address. If the user changes this value on their device, it resets to **Use randomized MAC** on the next Intune sync.

- **Use device MAC**: Forces devices to present their actual Wi-Fi MAC address instead of a random MAC address. This setting allows devices to be tracked by their MAC address. Only use this value when necessary, such as for network access control (NAC) support. If the user changes this value on their device, it resets to **Use device MAC** on the next Intune sync.

Applies to:

- Android 13 and newer

For more information on the Wi-Fi settings you can configure, see [Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices in Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md).

#### Turn Off Copilot in Windows setting in the Windows settings catalog<!-- 26725574 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There's a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows** for platform > **Settings catalog** for profile type.

- **Windows AI > Turn Off Copilot in Windows (User)**

  - If you enable this policy setting, users can't use Copilot. The Copilot icon won't appear on the taskbar.
  - If you disable or don't configure this policy setting, users can use Copilot when it's available to them.

This setting uses the [Policy CSP - WindowsAI](/windows/client-management/mdm/policy-csp-windowsai).

For more information about configuring Settings Catalog policies in Intune, including user scope vs. device scope, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:

- Windows 10 and later

#### Windows Autopilot self-deploying mode is now generally available<!-- 26780755 -->

Windows Autopilot self-deploying mode is now generally available and out of preview. Windows Autopilot self-deploying mode enables you to deploy Windows devices with little to no user interaction. Once the device connects to network, the device provisioning process starts automatically: the device joins Microsoft Entra ID, enrolls in Intune, and syncs all device-based configurations targeted to the device. Self-deploying mode ensures that the user can't access desktop until all device-based configuration is applied. The Enrollment Status Page (ESP) is displayed during OOBE so users can track the status of the deployment. For more information, see:

- [Windows Autopilot self-deploying mode](/autopilot/self-deploying)
- [Step by step tutorial for Windows Autopilot self-deploying mode in Intune](/autopilot/tutorial/self-deploying/self-deploying-workflow)

This information is also published in [Windows Autopilot: What's new](/autopilot/whats-new).

#### Windows Autopilot for pre-provisioned deployment is now generally available<!-- 26780755 -->

Windows Autopilot for pre-provisioned deployment is now generally available and out of preview. Windows Autopilot for pre-provisioned deployment is used by organizations that want to ensure devices are business-ready before the user accesses them. With pre-provisioning, admins, partners, or OEMs can access a technician flow from the Out-of-box experience (OOBE) and kick off device setup. Next, the device is sent to the user who completes provisioning in the user phase. Pre-provisioning delivers most the configuration in advance so the end user can get to the desktop faster. For more information, see:

- [Windows Autopilot for pre-provisioned deployment](/autopilot/pre-provision).
- [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra join in Intune](/autopilot/tutorial/pre-provisioning/azure-ad-join-workflow)
- [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join in Intune](/autopilot/tutorial/pre-provisioning/hybrid-azure-ad-join-workflow).

This information is also published in [Windows Autopilot: What's new](/autopilot/whats-new).

### Device enrollment

#### ESP setting to install required apps during Windows Autopilot pre-provisioning<!-- 26583413 -->

The setting **Only fail selected blocking apps in technician phase** is now generally available to configure in Enrollment Status Page (ESP) profiles. This setting only appears in ESP profiles that have *blocking apps* selected.

For more information, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md#create-new-profile).

#### New local primary account configuration for macOS automated device enrollment<!-- 5877061 -->

Configure local primary account settings for Macs enrolling in Intune via Apple automated device enrollment. These settings, supported on devices running macOS 10.11 and later, are available in new and existing enrollment profiles under the new **Account Settings** tab. For this feature to work, the enrollment profile must be configured with user-device affinity and one of the following authentication methods:

- Setup Assistant with modern authentication
- Setup Assistant (legacy)

Applies to:

- macOS 10.11 and later

For more information about macOS account settings, see [Create an Apple enrollment profile in Intune](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile).

#### Await final configuration for macOS automated device enrollment now generally available<!-- 24973562 -->

Now generally available, *await final configuration* enables a locked experience at the end of Setup Assistant to ensure that critical device configuration policies are installed on devices. The locked experience works on devices targeted with new and existing enrollment profiles, enrolling via one of these authentication methods:

- Setup Assistant with modern authentication
- Setup Assistant (legacy)
- Without user device affinity

Applies to:

- macOS 10.11 and later

For information about how to enable await final configuration, see [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile).

### Device management

#### AOSP devices check for new tasks and notifications approximately every 15 minutes<!-- 8506468 -->

On devices enrolled with Android (AOSP) management, Intune attempts to check for new tasks and notifications approximately every 15 minutes. To use this feature, devices must be using the Intune app version 24.02.4 or newer.

Applies to:

- Android (AOSP)

For more information, see:

- [How to use Intune in environments without Google Mobile Services](../apps/manage-without-gms.md#some-tasks-can-be-delayed)
- [Policy refresh intervals in Intune](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals)

#### New device management experience for Government clouds in Microsoft Intune<!-- 17585897 23692982 -->

In government clouds, there's a new device management experience in the Intune admin center. The **Devices** area now has a more consistent UI, with more capable controls and an improved navigation structure so you can find what you need faster.

If you want to try the new experience before your tenant is updated, go to **Devices** > **Overview**, select the **Preview upcoming changes to Devices and provide feedback** notification banner, and select **Try it now**.

#### Bulk approval of drivers<!-- 14723288 -->

Bulk actions are now available for Windows Driver update policies. With bulk actions, multiple driver updates can be approved, paused, or declined at the same time, saving time and effort.

When you bulk approve drivers, the date for when the drivers become available to applicable devices can also be set, enabling drivers to be installed together.

Applies to:

- Windows 10
- Windows 11

For more information, see [Bulk driver updates](../protect/windows-driver-updates-policy.md#bulk-driver-updates).

#### App Control for Business policy limitation is resolved<!-- 19548950 -->

A previously documented limitation for App Control for Business policy (WDAC), that limited the number of active policies per device to 32, is resolved by Windows. The issue involves a potential [Boot stop failure when more than 32 policies are active](/windows/security/application-security/application-control/windows-defender-application-control/operations/known-issues#boot-stop-failure-blue-screen-occurs-if-more-than-32-policies-are-active) on a device.

This issue is resolved for devices that run Windows 10 1903 or later with a Windows security update released on or after March 12, 2024. Older versions of Windows can expect to receive this fix in future Windows security updates.

Applies to:

- Windows 10 version 1903 and later

To learn more about App Control for Business policy for Intune, see [Manage approved apps for Windows devices with App Control for Business policy and Managed Installers for Microsoft Intune](../protect/endpoint-security-app-control-policy.md).

### Tenant administration

#### Customization pane support for excluding groups<!-- 17654599 -->

The Customization pane now supports selecting groups to exclude when assigning policies. You can find this setting in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**.

For more information, see [Assign policies in Microsoft Intune](../configuration/device-profile-assign.md).

## Week of January 29, 2024

### Microsoft Intune Suite

#### Microsoft Intune Enterprise Application Management<!-- 10986080 -->

Enterprise Application Management provides an Enterprise App Catalog of Win32 applications that are easily accessible in Intune. You can add these applications to your tenant by selecting them from the Enterprise App Catalog. When you add an Enterprise App Catalog app to your Intune tenant, default installation, requirements, and detection settings are automatically provided. You can modify these settings as well. Intune hosts Enterprise App Catalog apps in Microsoft storage.

For more information, see:

- [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md)
- [Microsoft Intune Enterprise Application Management](../apps/apps-enterprise-app-management.md)
- [Add an Enterprise App Catalog app to Microsoft Intune](../apps/apps-add-enterprise-app.md)

#### Microsoft Intune Advanced Analytics<!--25194145 -->

Intune Advanced Analytics provides comprehensive visibility of the end-user experience in your organization and optimizes it with data driven insights. It includes near real-time data about your devices with Device query, increased visibility with custom device scopes, a battery health report and a detailed device timeline for troubleshooting device issues, and anomaly detection to help identify potential vulnerabilities or risks across your device estate.

- **Battery health report**<!-- 9747162 -->

  The battery health report provides visibility into the health of batteries in your organization's devices and its influence on user experience. The scores and insights in this report are aimed to help IT admins with asset management and purchase decisions that improve user experience while balancing hardware costs.

- **Run on-demand device queries on single devices**<!-- 16719466 -->

  Intune allows you to quickly gain on-demand information about the state of your device. When you enter a query on a selected device, Intune runs a query in real time.

  The data returned can then be used to respond to security threats, troubleshoot the device, or make business decisions.

  Applies to:

  - Windows devices

Intune Advanced Analytics is part of the Microsoft Intune Suite. For added flexibility, this new set of capabilities, together with the existing Advanced Analytics features, is also now available as an individual add-on to Microsoft subscriptions that include Intune.

To use Device query and battery health report in your tenant, or any of the existing Advanced Analytics capabilities, you must have a license for either:

- The Intune Advanced Analytics add-on
- The Microsoft Intune Suite add-on

For more information, see:

- [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md)
- [Microsoft Intune Advanced Analytics](../../analytics/advanced-endpoint-analytics.md)
- [Battery health](../../analytics/battery-health.md)
- [Device query](../../analytics/device-query.md)

## What's new archive
<!-- Past announcements that are older than six months will be moved to the archive -->

For previous months, see the [What's new archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
