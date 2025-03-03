---
# required metadata
title: What's new in previous months in the Microsoft Intune
titleSuffix: 
description: Review older announcements from the Intune what's new page
keywords:
author: dougeby  
ms.author: dougeby
manager: dougeby
ms.date: 02/05/2025
ms.topic: whats-new
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 9ba01d60-4a03-4e3e-9aba-8be905c0054c

# optional metadata

ROBOTS: NOINDEX,NOFOLLOW
#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# What's new in the Microsoft Intune - previous months

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

<!-- Maintenance plan:

     Maintain ~2 years of archived content -->

## Week of July 22, 2024 (Service release 2407)

### Microsoft Intune Suite

#### New actions for Microsoft Cloud PKI<!-- 24231040 -->

The following actions have been added for Microsoft Cloud PKI issuing and root certification authorities (CA):

- Delete: Delete a CA.
- Pause: Temporarily suspend use of a CA.
- Revoke: Revoke a CA certificate.

You can access all new actions in the Microsoft Intune admin center and Graph API. For more information, see [Delete Microsoft Cloud PKI certification authority](../protect/microsoft-cloud-pki-delete.md).

### App management

#### Intune support for additional macOS app types from the Company Portal<!-- 26133163 -->

Intune supports the capability to deploy DMG and PKG apps as **Available** in the Intune macOS Company Portal. This capability enables end users to browse and install agent-deployed applications using Company Portal for macOS. This capability requires a minimum version of the Intune agent for macOS v2407.005 and Intune Company Portal for macOS v5.2406.2.

#### Newly available Enterprise App Catalog apps for Intune<!-- 28691663 -->

The Enterprise App Catalog has updated to include additional apps. For a complete list of supported apps, see [Apps available in the Enterprise App Catalog](../apps/apps-enterprise-app-management.md#apps-available-in-the-enterprise-app-catalog).

#### The Intune App SDK and Intune App Wrapping Tool are now in a different GitHub repo<!-- 27264674, 27264632 -->

The Intune App SDK and Intune App Wrapping Tool have moved to a different GitHub repository and a new account. There are redirects in place for all existing repositories. In addition, the Intune sample applications are also included in this move. This change relates to both Android and iOS platforms.

### Device configuration

#### New clipboard transfer direction settings available in the Windows settings catalog <!-- 28748086 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

**Administrative Templates > Windows Components > Remote Desktop Services > Remote Desktop Session Host > Device and Resource Redirection**:

- Restrict clipboard transfer from server to client
- Restrict clipboard transfer from server to client (User)
- Restrict clipboard transfer from client to server
- Restrict clipboard transfer from client to server (User)

For more information on configuring the clipboard transfer direction in Azure Virtual Desktop, see [Configure the clipboard transfer direction and types of data that can be copied in Azure Virtual Desktop](/azure/virtual-desktop/clipboard-transfer-direction-data-types).

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

In an Intune device restrictions configuration policy, you can configure the **Allow access to all apps in Google Play store** setting using the **Allow** and **Not configured** options (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully managed, dedicated and corporate-owned work profile > Device restrictions** for profile type > **Applications**).

The available options are updated to **Allow**, **Block**, and **Not configured**.

There's no impact to existing profiles using this setting.

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

#### Just-in-time registration and compliance remediation available for all iOS/iPadOS enrollments<!-- 27759589 -->

You can now configure just-in-time (JIT) registration and JIT compliance remediation for all Apple iOS and iPadOS enrollments. These Intune-supported features improve the enrollment experience because they can take the place of the Intune Company Portal app for device registration and compliance checks. We recommend setting up JIT registration and compliance remediation for new enrollments, and to improve the experience for existing enrolled devices. For more information, see [Set up just in time registration in Microsoft Intune](../enrollment/set-up-just-in-time-registration.md).

### Device management

#### Consolidation of Intune profiles for identity protection and account protection <!-- 24810271 -->

We have consolidated the Intune profiles that were related to identity and account protection, into a single new profile named *Account protection*. This new profile is found in the [account protection policy node of endpoint security](../protect/endpoint-security-account-protection-policy.md), and is now the only profile template that remains available when creating new policy instances for identity and account protection. The new profile includes Windows Hello for Business settings for both users and devices, and settings for Windows Credential Guard.

Because this new profile uses Intune’s unified settings format for device management, the profiles settings are also available through the [settings catalog](../configuration/settings-catalog.md), and help to improve the reporting experience in the Intune admin center.

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

#### Newly available protected apps for Intune<!-- 28334000, 28157519, 28311088, 28156655, 28246919, 28246936, 28100886 -->

The following protected apps are now available for Microsoft Intune:

- Asana: Work in one place (Android) by Asana, Inc.
- Goodnotes 6 (iOS) by Time Base Technology Limited
- Riskonnect Resilience by Riskonnect, Inc.
- Beakon Mobile App by Beakon Mobile Team
- HCSS Plans: Revision control (iOS) by Heavy Construction Systems Specialists, Inc.
- HCSS Field: Time, cost, safety (iOS) by Heavy Construction Systems Specialists, Inc.
- Synchrotab for Intune (iOS) by Synchrotab, LLC

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of July 15, 2024

### Device management

#### New setting in the Device Control profile for Attack surface reduction policy<!-- 28761508 -->

We've added a new category and setting to the Device Control profile for the *Windows 10, Windows 11, and Windows Server* platform of Intune [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

The new setting is **Allow Storage Card**, and found in the new **System** category of the profile. This setting is also available from the Intune [settings catalog](../configuration/settings-catalog.md) for the Windows devices.

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

Existing enrolled devices aren't affected by this change. For new user or device enrollments that utilize Company Portal, users must return to Company Portal to complete registration:

- For iOS users: Users with notifications enabled are prompted to return to the Company Portal app for iOS. If they disable notifications, they aren't alerted, but still need to return to Company Portal to complete registration.

- For macOS devices: The Company Portal app for macOS detects the installation of the management profile and automatically register the device, unless the user closes the app. If they close the app, they must reopen it to complete registration.

If you're using dynamic groups, which rely on device registration to work, it's important for users to complete device registration. Update your user guidance and admin documentation as needed. If you're using Conditional Access (CA) policies, no action is required. When users attempt to sign in to a CA-protected app, they are prompted to return to Company Portal to complete registration.

These changes are currently rolling out and will be made available to all Microsoft Intune tenants by the end of July. There's no change to the Company Portal user interface. For more information about device enrollment for Apple devices, see:

- [Enrollment guide: Enroll macOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-macos.md#device-enrollment-end-user-tasks)
- [Enrollment guide: Enroll iOS and iPadOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-ios-ipados.md)

## Week of June 24, 2024

### Device enrollment

#### Add corporate device identifiers for Windows<!-- 25873757 -->

Microsoft Intune now supports corporate device identifiers for devices running Windows 11, version 22H2 and later so that you can identify corporate machines ahead of enrollment. When a device that matches the model, manufacturer, and serial number criteria enrolls, Microsoft Intune marks it as a corporate device and enable the appropriate management capabilities. For more information, see [Add corporate identifiers](../enrollment/corporate-identifiers-add.md).

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

We've completed a rebrand in the Microsoft Intune admin center to support replacing Wandera with Jamf. This includes updates to the name of the Mobile Threat Defense connector, which is now *Jamf*, and changes to the minimum required platforms to use the Jamf connector:

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

Each time we add a new granular permission for an endpoint security policy to Intune, those same rights are removed from the *Security baselines* permission. If you use custom roles with the *Security baselines* permission, the new RBAC permission is assigned automatically to your custom roles with the same rights that were granted through the *Security baseline* permission. This autoassignment ensures your admins continue to have the same permissions they have today.

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

Enrollment time grouping is a new, faster way to group devices during enrollment. When configured, Intune adds devices to the appropriate group without requiring inventory discovery and dynamic membership evaluations. To set up enrollment time grouping, you must configure a static Microsoft Entra security group in each enrollment profile. After a device enrolls, Intune adds it to the static security group and delivers assigned apps and policies.

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

You can prevent end users within your organization from accessing BitLocker recovery keys by configuring the Microsoft Entra toggle **Restrict non-admin users from recovering the BitLocker key(s) for their owned device**.

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

Feature updates can now be made available to end users as **Optional** updates, with the introduction of **Optional** Feature updates. End users see the update in the **Windows Update** settings page in the same way that it's shown for consumer devices.

End users can easily opt in to try out the next Feature update and provide feedback. When it's time to roll out the feature as a **Required** update, admins can change the setting on the policy and update the rollout settings so that the update is deployed as a **Required** update to devices that don't yet have it installed.

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

We recently released and improved the Managed Home Screen experience, which is now Generally Available. The app is redesigned to improve the core workflows throughout the application. The updated design offers a more usable and supportable experience.

With the release, we stop investing in previous Managed Home Screen workflows. New features and fixes for Managed Home Screen are only added to the new experience. During August 2024, the new experience is automatically enabled for all devices.

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

#### New elevation type for Endpoint Privilege Management<!-- 25230692 -->

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

## Week of January 22, 2024 (Service release 2401)

### App management

#### Install DMG and PKG apps up to 8 GB in size on managed Macs<!-- 25766031 -->

The size-limit of DMG and PKG apps that can be installed using Intune on managed Macs has been increased. The new limit is 8 GB and is applicable to apps (DMG and unmanaged PKG) that are installed using the Microsoft Intune management agent for macOS.

For more information about DMG and PKG apps, see [Add a macOS DMG app to Microsoft Intune](../apps/lob-apps-macos-dmg.md) and [Add an unmanaged macOS PKG app to Microsoft Intune](../apps/macos-unmanaged-pkg.md).

#### Intune support of store-signed LOB apps for Surface Hub devices<!-- 25865620 -->

Intune now supports the deployment of store-signed LOB apps (single file `.appx`, `.msix`, `.appxbundle`, and `.msixbundle`) to Surface Hub devices. The support for store-signed LOB apps enables offline store apps to be deployed to Surface Hub devices following the retirement of the Microsoft Store for Business.

#### Route SMS/MMS messages to specific app<!-- 24594466 -->

You can configure an app protection policy to determine which SMS/MMS app must be used when the end user intends to send a SMS/MMS message after getting redirected from a policy managed app. When the end user selects on a number with the intent of sending an SMS/MMS message, the app protection settings are used to redirect to the configured SMS/MMS app. This capability relates to the **Transfer messaging data to** setting and applies to both iOS/iPadOS and Android platforms.

For more information, see [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md) and [Android app protection policy settings](../apps/app-protection-policy-settings-android.md).

#### End user app PIN reset<!-- 24605159 -->

For managed apps that require a PIN to access, allowed end users can now reset the app PIN at any time. You can require an app PIN in Intune by selecting the **PIN for access** setting in iOS/iPadOS and Android app protection policies.

For more information about app protection policies, see [App protection policies overview](../apps/app-protection-policy.md).

#### Maximum app package size<!-- 17546826 -->

The maximum package size for uploading apps to Intune is changed from 8 GB to 30 GB for paid customers. Trial tenants are still restricted to 8 GB.

For more information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md#prerequisites).

### Device configuration

#### New setting that disables location on Android Enterprise devices<!-- 21060837 -->

On Android Enterprise devices, there's a new setting that allows admins to control the location (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile > Device Restrictions** for profile type > **General**):

- **Location**: **Block** disables the **Location** setting on the device and prevents users from turning it on. When this setting is disabled, then any other setting that depends on the device location is affected, including the **Locate device** remote action. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using location on the device.

Applies to:

- Android Enterprise

For more information on the settings you can configure, see [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

#### Date and time picker for managed software updates in the settings catalog on iOS/iPadOS and macOS devices<!-- 26015175 -->

Using the settings catalog, you can enforce managed updates on iOS/iPadOS and macOS devices by entering a date and time (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type > **Declarative Device Management > Software Update**).

Previously, you had to manually type the date and time. Now, there's a date and time picker for the **Target Local Date Time** setting:

**Declarative Device Management (DDM) > Software Update**:

- Target Local Date Time

> [!IMPORTANT]
> If you create a policy using this setting before the January 2024 release, then this setting shows `Invalid Date` for the value. The updates are still scheduled correctly and use the values you originally configured, even though it shows `Invalid Date`.
>
> To configure a new date and time, you can delete the `Invalid Date` values, and select a new date and time using the date time picker. Or, you can create a new policy.

Applies to:

- iOS/iPadOS
- macOS

For more information about configuring Managed software updates in Intune, see [Use the settings catalog to configure managed software updates](../protect/managed-software-updates-ios-macos.md).

### Device management

#### New device management experience in Microsoft Intune<!-- 17585897 23692982 -->

We're rolling out an update to the device management experience in the Intune admin center. The **Devices** area now has a more consistent UI, with more capable controls and an improved navigation structure so you can find what you need faster. The new experience, previously in public preview, will gradually roll out for general availability over the coming weeks. The public preview experience continues to be available until your tenant receives the update.

The availability of this new admin center experience varies tenant by tenant. While a few will see this update immediately, many might not see the new experience for several weeks. For Government clouds, the availability of this experience is estimated around late February 2024.

Due to the rollout timelines, we're updating our documentation to the new experience as soon as possible to help ease the transition to the new admin center layout. We're unable to provide a side-by-side content experience during this transition and believe providing documentation that aligns to the newer experience brings more value to more customers. If you want to try the new experience and align with doc procedures before your tenant is updated, go to **Devices** > **Overview**, select the notification banner that reads **Preview upcoming changes to Devices and provide feedback**, and select **Try it now**.

#### BlackBerry Protect Mobile now supports app protection policies<!-- 13357196  -->

You can now use Intune app protection policies with *BlackBerry Protect Mobile* (powered by Cylance AI). With this change, Intune supports BlackBerry Protect Mobile for mobile application management (MAM) scenarios for [unenrolled devices](../protect/mtd-add-apps-unenrolled-devices.md). This support includes the use of risk assessment with Conditional Access and configuration of Conditional Launch settings for unenrolled devices.

While configuring the CylancePROTECT Mobile connector (formerly BlackBerry Mobile), you now can select options to turn on *App protection policy evaluation* for both Android and iOS/iPadOS devices.

For more information, see [Set up BlackBerry Protect Mobile](../protect/blackberry-mobile-threat-defense-connector.md), and [Create Mobile Threat Defense app protection policy with Intune](../protect/mtd-app-protection-policy.md).

### Device security

#### Support for Intune Defender Update control policies for devices managed by Microsoft Defender for Endpoint<!--25470154 -->

You can now use the endpoint security policy for *Defender Update control* (Antivirus policy) from the Microsoft Intune admin center with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Defender Update control** policies are part of endpoint security [Antivirus policy](../protect/endpoint-security-antivirus-policy.md).

Applies to the following when you use the *Windows 10, Windows 11, and Windows Server* platform:

- Windows 10
- Windows 11

With this support available, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive the policy will get it.

### Intune apps

#### Newly available protected apps for Intune<!-- 25765585, 26137219 -->

The following protected apps are now available for Microsoft Intune:

- PrinterOn Print by PrinterOn, Inc. (iOS/iPadOS)
- Align for Intune by MFB Technologies, Inc. (iOS/iPadOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Monitoring reports for devices<!-- 17744651 -->

In Intune, you can view a new list of all device monitoring reports. You can find these reports in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Monitor**. The **Monitor** pane provides reports related to configuration, compliance, enrollment, and software updates. Additionally, there are other reports that you can view, such as **Device actions**.

For more information, see [Intune reports](reports.md).

#### Exported report data maintains search results<!-- 17723620 -->

Intune can now maintain your report search and filter results when exporting report data. For example, when you use the [Noncompliant devices and settings](reports.md#noncompliant-devices-report-organizational) report, set the OS filter to "Windows", and search for "PC", the exported data will only contain Windows devices with "PC" in their name. This capability is also available when calling the `ExportJobs` API directly.

#### Easy upload of diagnostic logs for Microsoft Tunnel servers<!-- 15728481 -->

You can now use a single click within the Intune admin center to have Intune enable, collect, and submit eight hours of verbose logs for a Tunnel Gateway Server to Microsoft. The verbose logs can then be referenced while working with Microsoft to identify or resolve issues with a Tunnel server.

In contrast, the collection of verbose logs previously required you to sign on to the server, run manual tasks and scripts to enable and collect verbose logs, and then copy them to a location from which you can transfer them to Microsoft.

To find this new capability, in the admin center go to **Tenant administration** > **Microsoft Tunnel Gateway** > select a server > select the **Logs** tab. On this tab, is a new section named **Send verbose server logs** with button labeled **Send logs**, and a list view that displays the various log sets that have been collected and submitted to Microsoft.

When you select the **Send logs** button:

- Intune captures and submits the current server logs as a baseline, prior to collecting verbose logs.
- Verbose logging is automatically enabled at level 4, and runs for eight hours to provide time to reproduce an issue for capture in those logs.
- After eight hours, Intune submits the verbose logs and then restores the server to its default verbosity level of zero (0), for normal operations. If you previously set logs to run at a higher verbosity level, you can restore your custom verbosity level after log collection and upload is complete.
- Each time Intune collects and submits logs, it updates the list view below the button.
- Below the button is a list of past log submissions, displaying their verbosity level and an Incident ID that you can use when working with Microsoft to reference a specific set of logs.

For more information about this capability, see [Easy upload of diagnostic logs for Tunnel servers](../protect/microsoft-tunnel-monitor.md#easy-upload-of-diagnostic-logs-for-tunnel-servers).

## Week of December 11, 2023 (Service release 2312)

### App management

#### Support to add unmanaged PKG-type applications to managed macOS devices is now generally available<!-- 17296091   -->

You can now upload and deploy unmanaged PKG-type applications to managed macOS devices using the Intune MDM agent for macOS devices. This feature enables you to deploy custom PKG installers, such as unsigned apps and component packages. You can add a PKG app in the Intune admin center by selecting **Apps** > **macOS** > **Add** > **macOS app (PKG)** for app type.

Applies to:

- macOS

For more information, see [Add an unmanaged macOS PKG app to Microsoft Intune](../apps/macos-unmanaged-pkg.md). To deploy managed PKG-type app, you can continue to [add macOS line-of-business (LOB) apps to Microsoft Intune](../apps/lob-apps-macos.md). For more information about the Intune MDM agent for macOS devices, see [Microsoft Intune management agent for macOS](../apps/lob-apps-macos-agent.md).

#### Windows MAM supported in government cloud environments and in 21 Vianet in China<!-- 25273622  -->

Customer tenants in US Government Community (GCC), US Government Community (GCC) High, and Department of Defense (DoD) environments are now able to use Windows MAM. For related information, see [Deploying apps using Intune on the GCC High and DoD Environments](../apps/apps-deploy-gcc-dod.md) and [Data protection for Windows MAM](../apps/protect-mam-windows.md).

In addition, Windows MAM is available for Intune operated by 21Vianet in China. For more information, see [Intune operated by 21Vianet in China](china.md).

### Device configuration

#### Updated security baseline for Microsoft Edge v117<!-- 25021903 -->

We released a new version of the Intune security baseline for **Microsoft Edge**, version [**v117**](../protect/security-baselines.md#available-security-baselines). This update brings support for recent settings so you can continue to maintain best-practice configurations for Microsoft Edge.

We also updated our [reference article](../protect/security-baseline-v2-edge-settings.md?pivots=edge-v117) for this baseline where you can view the default configuration of the settings this baseline version includes.

### Device management

#### Support for variables in noncompliant email notifications<!-- 6111965  -->

Use variables to personalize email notifications that are sent when a user's device becomes noncompliant. The variables included in the template, such as `{{username}}` and `{{devicename}}`, are replaced by the actual username or device name in the email that users receive. Variables are supported with all platforms.

For more information and a list of supported variables, see [Create a notification message template](../protect/actions-for-noncompliance.md#create-a-notification-message-template).

#### Updated report visualization for Microsoft Defender for Endpoint connector<!--  24762035  -->

We updated the reporting visualization for the Microsoft Defender for Endpoint connector. This [report visualization](../protect/advanced-threat-protection-configure.md#view-the-count-of-devices-that-are-onboarded-to-microsoft-defender-for-endpoint) displays the count of devices that are onboarded to Defender for Endpoint based on status from the Defender CSP, and visually aligns to other recent report views that use a bar to represent the percentage of devices with different status values.

### Device security

#### New settings for scheduling Antivirus scans added to Antivirus policy for Windows devices<!-- 26013546  -->

We added two settings to the *Microsoft Defender Antivirus* profile for [endpoint security Antivirus policy](../protect/endpoint-security-antivirus-policy.md#antivirus-profiles) that applies to Windows 10 and Windows 11 devices. These two settings work together to first enable support for a random start time of a device's antivirus scan, and to then define a range of time during which the randomized scan start can begin. These settings are supported with devices managed by Intune and devices managed through the [Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.

- [**RandomizeScheduleTaskTimes**](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#admx-microsoftdefenderantivirus-randomizescheduletasktimes) – This setting enables randomization of the scan start time on devices.
- [**SchedulerRandomizationTime**](/windows/client-management/mdm/defender-csp?WT.mc_id=Portal-fx#configurationschedulerrandomizationtime) – With this setting, you can set boundaries for the random start time.

In addition to being added to the Microsoft Defender Antivirus profile, both settings are now available from the [settings catalog](../configuration/settings-catalog.md).

Applies to:

- Windows 10
- Windows 11

#### Microsoft Tunnel support for direct proxy exclusion list in VPN profiles for Android Enterprise<!-- 24139621 -->

Intune now supports configuration of a *Proxy exclusion list* when you [configure a VPN profile for Microsoft Tunnel](../protect/microsoft-tunnel-configure.md#create-a-vpn-profile) for Android devices. With an exclusion list, you can exclude specific domains from your proxy setup without requiring the use of a Proxy Auto-Configuration (PAC) file. The proxy exclusion list is available with both Microsoft Tunnel and Microsoft Tunnel for MAM.

The proxy exclusion list is supported in environments that use a single proxy. The exclusion list isn't suitable or supported when you use multiple proxy servers, for which you should continue to use a `.PAC` file.

Applies to:

- Android Enterprise

#### Microsoft Tunnel server health metric to report on TLS certificate revocation<!-- 25853648  -->

We added a new health metric for Microsoft Tunnel named **TLS certificate revocation**. This new health metric report on the status of the Tunnel Servers TLS certificate by accessing the Online Certificate Status Protocol (OCSP) or CRL address as defined in the TLS certificate. You can view the status of this new check with all the health checks in the Microsoft Intune admin center by navigating to **Tenant administration** > **Microsoft Tunnel Gateway** > **Health status**, selecting a server, and then selecting that servers **Health check** tab.

This metric runs as part of the existing Tunnel Health checks, and supports the following status:

- *Healthy*: The TLs certificate isn't revoked
- *Warning*: Unable to check if the TLS certificate is revoked
- *Unhealthy*: The TLS certificate is revoked, and should be updated

For more information about the TLS certificate revocation check, see [Monitor Microsoft Tunnel](../protect/microsoft-tunnel-monitor.md).

### Intune apps

#### Newly available protected app for Intune<!-- 25636619  -->

The following protected app is now available for Microsoft Intune:

- Akumina EXP by Akumina Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of November 27, 2023

### App management

#### Configure offline caching in Microsoft 365 (Office) for Android devices<!-- 25008682 -->

When the **Save As to Local Storage** setting is set to **blocked** in an [app protection policy](../apps/app-protection-policies.md), you can use a configuration key in an app configuration policy to enable or disable offline caching. This setting is only applicable to the Microsoft 365 (Office) app on Android.

For more information, see [Data protection settings in Microsoft 365 (Office)](../apps/manage-microsoft-office.md#data-protection-settings-in-microsoft-365-office).

#### Win32 app grace period settings on a device<!-- 17644728 -->

On a device where a Win32 app with grace period settings is deployed, low-rights users without administrative privileges can now interact with the grace period UX. Admins on the device continue to be able to interact with the grace period UX on the device.

For more information about grace period behavior, see [Set Win32 app availability and notifications](../apps/apps-win32-app-management.md#set-win32-app-availability-and-notifications).

#### Managed Home Screen app configuration additions<!-- 25374056 -->

Now in public preview, Microsoft Managed Home Screen (MHS) is updated to improve the core workflows and user experience. In addition to some user interface changes, there's a new top bar navigation where admins can configure device identifying attributes to be displayed. Additionally, users can access settings, sign in/out, and view notifications when permissions are requested on the top bar.

You can add more settings to configure the Managed Home Screen app for Android Enterprise. Intune now supports the following settings in your Android Enterprise app configuration policy:

- Enable updated user experience
- Top Bar Primary Element
- Top Bar Secondary Element
- Top Bar User Name Style

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Intune APP SDK for .NET MAUI<!-- 17696301 -->

Using the Intune APP SDK for .NET MAUI, you can develop Android or iOS apps for Intune that incorporate the [.NET Multi-platform App UI](https://dotnet.microsoft.com/apps/maui). Apps developed using this framework allow you to enforce [Intune mobile application management](../apps/app-management.md). For .NET MAUI support on Android, see [Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android). For .NET MAUI support on iOS, see [Intune App SDK for .NET MAUI - iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).

## Week of November 13, 2023 (Service release 2311)

### App management

#### New grace period status added in apps for Android, Android AOSP<!-- 13498172 13498291  -->

The Intune Company Portal app for Android and Microsoft Intune app for Android AOSP now show a grace period status for devices that don't meet compliance requirements but are still within their given grace period. Users can see the date by which devices must be compliant, and the instructions for how to become compliant. If users don't update their device by the given date, the device is marked as noncompliant.

For more information, see the following articles:

- [Configure compliance policies with actions for noncompliance](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance)
- [Check compliance in Intune app for AOSP](../user-help/check-compliance-aosp.md)
- [Check compliance in Company Portal for Android](../user-help/check-compliance-on-your-device-android.md)

### Device configuration

#### New settings available in the Apple settings catalog<!-- 25189345  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Managed Settings**:

- Data roaming
- Personal hotspot
- Voice roaming (deprecated): This setting is deprecated in iOS 16.0. Data roaming is the replacement setting.

##### Shared iPad

**Managed Settings**:

- Diagnostic submission

##### macOS

**Microsoft Defender > Antivirus engine**:

- Enable passive mode (deprecated): This setting is deprecated. Enforcement level is the replacement setting.
- Enable real-time protection (deprecated): This setting is deprecated. Enforcement level is the replacement setting.
- Enforcement level

#### Settings to manage Windows Subsystem for Linux are now available in the Windows settings catalog<!-- 17757930  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings to the Windows settings catalog for *Windows Subsystem for Linux* (WSL). These settings enable Intune integration with WSL so admins can manage deployments of WSL and controls into Linux instances themselves.

To find these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Devices** > **Configuration** > **Create** > **New Policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

**Windows Subsystem for Linux**:

- Allow kernel debugging
- Allow custom networking configuration
- Allow custom system distribution configuration
- Allow kernel command line configuration
- Allow custom kernel configuration
- Allow WSL1
- Allow the Windows Subsystem for Linux
- Allow the Inbox version of the Windows Subsystem For Linux
- Allow user setting firewall configuration
- Allow nested virtualization
- Allow passthrough disk mount
- Allow the debug shell

Applies to:

- Windows 10
- Windows 11

### Device enrollment

#### Enrollment for iOS/iPadOS devices in shared device mode now generally available<!-- 25199565   -->

Now generally available to configure in the Microsoft Intune admin center, set up automated device enrollment for iOS/iPadOS devices that are in shared device mode. Shared device mode is a feature of Microsoft Entra that enables your frontline workers to share a single device throughout the day, signing in and out as needed.

For more information, see [Set up enrollment for devices in shared device mode](../enrollment/automated-device-enrollment-shared-device-mode.md).

### Device management

#### Improvements to new device experience in admin center (public preview)<!-- 24155098, 25103808, 17705028   -->

We made the following changes to the new Devices experience in the Microsoft Intune admin center:

- More entry points to platform-specific options: Access the platform pages from the **Devices** navigation menu.
- Quick entry to monitoring reports: Select the titles of the metrics cards to go to the corresponding monitoring report.
- Improved navigation menu: We added icons back in to provide more color and context as you navigate.

Flip the toggle in the Microsoft Intune admin center to try out the new experience while it's in public preview and share your feedback. 

For more information, see:

- [New Microsoft Intune Devices experience - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/intune-customer-success/new-microsoft-intune-devices-experience/ba-p/3777342)
- [Try new Devices experience - Microsoft Learn](public-preview.md)

### Device security

#### Additional settings for the Linux Antivirus policy template<!-- 24191424 -->

We expanded support for Linux by adding the following settings to the *Microsoft Defender Antivirus* template for Linux devices:

- cloudblocklevel
- scanarhives
- scanafterdefinitionupdate
- maximumondemandscanthreads
- behaviormonitoring
- enablefilehashcomputation
- networkprotection
- enforcementlevel
- nonexecmountpolicy
- unmonitoredfilesystems

The Microsoft Defender Antivirus template for Linux is supported for devices [managed by Intune](../protect/endpoint-security-antivirus-policy.md), and devices managed only by Defender through the [Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.

#### Updated security baseline for Microsoft 365 Apps for Enterprise<!-- 25021846   -->

We released a new version of the Intune security baseline for **Microsoft 365 Apps for Enterprise**, version [**2306**](../protect/security-baselines.md#available-security-baselines).

The Microsoft 365 Office Apps baseline can help you rapidly deploy configurations to your Office Apps that meet the security recommendations of the Office and security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations. You can modify the default baseline to meet the requirements of your organization.

We also updated our [reference article](../protect/security-baseline-v2-office-settings.md?pivots=v2306) for this baseline where you can view the default configuration of the settings this baseline version includes.

#### Deprecation and replacement of two settings found in the Linux and macOS endpoint security Antivirus policies<!-- 25234740  -->

There are two deprecated settings that in the *Antivirus engine* category of [Microsoft Defender Antivirus](../protect/endpoint-security-antivirus-policy.md) profiles of both macOS and Linux. These profiles are available as part of Intune's endpoint security Antivirus policies.

For each platform, a single setting replaces the two deprecated settings. This new setting aligns with how Microsoft Defender for Endpoint manages the device configurations.

The following are the two deprecated settings:

- *Enable real-time protection* now appears as *Enable real-time protection (deprecated)*
- *Enable passive mode* now appears as *Enable passive mode (deprecated)*

The new setting that replaces the two deprecated settings:

- *Enforcement level* - By default, Enforcement level is set to *Passive* and supports options of *Real time* and *On demand*.

These settings are also available from the Intune [settings catalog](../configuration/settings-catalog.md) for each platform, where the old settings are also marked as deprecated and replaced by the new setting.

With this change, a device that has either of the *deprecated* settings configured will continue to apply that configuration until the device is targeted by the new setting *Enforcement level*. Once targeted by Enforcement Level, the deprecated settings no longer are applied to the device.

The *deprecated* settings will be removed from the Antivirus profiles and the settings catalog in a future update to Intune.

> [!NOTE]
> The changes for Linux are now available. The macOS settings are marked as deprecated, but the *Enforcement level* setting will not be available until December.

Applies to:

- Linux
- macOS

#### Microsoft Defender Firewall profiles are renamed to Windows Firewall<!-- 25171457 -->

To align to Firewall branding changes in Windows, we are updating the names of Intune profiles for endpoint security Firewall policies. In profiles that have *Microsoft Defender Firewall* in the name we're replacing that with *Windows Firewall*.

The following platforms have profiles that are affected, with only the profile names being affected by this change:

- Windows 10 and later (ConfigMgr)
- Windows 10, Windows 11, and Windows Server

#### Endpoint security Firewall policy for Windows Firewall to manage firewall settings for Windows Hyper-V<!--  25767542  -->

We added new settings to the *Windows Firewall* profile (formerly *Microsoft Defender Firewall*) for endpoint security [Firewall policy](../protect/endpoint-security-firewall-policy.md). The new settings can be used to manage Windows Hyper-V settings. To configure the new settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Endpoint security** > **Firewall** > Platform: **Windows 10, Windows 11, and Windows Server** > Profile: **Windows Firewall**.

The following settings are added to the *Firewall* category:

- **Target** - When *Target* is set to **Windows Subsystem for Linux**, the following child settings are applicable:
  - Enable Public Network Firewall
  - Enable Private Network Firewall
  - Allow Host Policy Merge
  - Enable Domain Network Firewall
  - Enable Loopback

Applies to:

- Windows 10
- Windows 11

For more information about these settings, see [Windows Firewall with Advanced Security](/windows/security/operating-system-security/network-security/windows-firewall/windows-firewall-with-advanced-security).

#### New Endpoint Security Firewall policy profile for Windows Hyper-V Firewall Rules<!-- 10946486  -->

We released a new profile named *Windows Hyper-V Firewall Rules* that you can find through the *Windows 10, Windows 11, and Windows Server* platform path for endpoint security [Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune). Use this profile to manage the firewall settings and rules that apply to specific Hyper-V containers on Windows, including applications like the Windows Subsystem for Linux (WSL) and the Windows Subsystem for Android (WSA).

Applies to:

- Windows 10
- Windows 11

### Intune apps

#### Newly available protected apps for Intune<!-- 25417889, 25161990, 25174019  -->

The following protected apps are now available for Microsoft Intune:

- Hey DAN for Intune by Civicom, Inc.
- Microsoft Azure by Microsoft Corporation (iOS)
- KeePassium for Intune by KeePassium Labs (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of November 6, 2023

### App management

#### Minimum version update for iOS Company Portal<!-- 17964541 -->

Users are required to update to v5.2311.1 of the iOS Company Portal. If you enabled the **[Block installing apps using App Store](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised)** device restriction setting, you'll likely need to push an update to the related devices that use this setting. Otherwise, no action is needed.

If you have a helpdesk, you might want to make them aware of the prompt to update the Company Portal app. In most cases, users have app updates set to automatic, so they receive the updated Company Portal app without taking any action. Users that have an earlier app version are prompted to update to the latest Company Portal app.

### Device security

#### Defender for Endpoint security settings management enhancements and support for Linux and macOS are generally available<!-- 24190967 -->

The improvements that were introduced in the Defender for Endpoint security settings management [opt-in public preview](#defender-for-endpoint-security-settings-management-enhancements-and-support-for-linux-and-macos-in-public-preview) are now generally available.

With this change, the default behavior for security settings management includes all the behavior added for the opt-in preview – without having to enable support for preview features in Microsoft Defender for Endpoint. This includes the general availability and support for the following endpoint security profiles for Linux and macOS:

**Linux**:

- Microsoft Defender Antivirus
- Microsoft Defender Antivirus exclusions
- Endpoint detection and response

**MacOS**:

- Microsoft Defender Antivirus
- Microsoft Defender Antivirus exclusions
- Endpoint detection and response

For more information, see [Microsoft Defender for Endpoint Security settings management](../protect/mde-security-integration.md) in the Intune documentation.

### Device management

### Feature updates and reports support Windows 11 policies<!--17614166 -->

The new setting on Feature update policies enables an organization to deploy Windows 11 to those devices that are eligible for the upgrade, while ensuring devices not eligible for the upgrade are on the latest Windows 10 feature update with a single policy. As a result, admins don't need to create or manage groups of eligible and non-eligible devices.

For more information on feature updates, see [Feature updates for Windows 10 and later](../protect/windows-10-feature-updates.md).

## Week of October 30, 2023

### Device security

#### Strict Tunnel Mode in Microsoft Edge available for Microsoft Tunnel for MAM on Android and iOS/iPadOS devices<!--24045412-->

In Intune, you can use the Microsoft Tunnel for mobile application management (MAM) on Android and iOS/iPadOS devices. With the MAM tunnel, unmanaged devices (devices not enrolled in Intune) can access on-premises apps and resources.

There's a new **Strict Tunnel Mode** feature you can configure for Microsoft Edge. When users sign into Microsoft Edge with an organization account, if the VPN isn't connected, then **Strict Tunnel Mode** blocks internet traffic. When the VPN reconnects, internet browsing is available again.

To configure this feature, create a Microsoft Edge app configuration policy, and add the following setting:

- **Key**: `com.microsoft.intune.mam.managedbrowser.StrictTunnelMode`
- **Value**: `True`

Applies to:

- Android Enterprise version 10 and later
- iOS/iPadOS version 14 and later

For more information, see:

- [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-mam.md)
- [Microsoft Tunnel for MAM - Android](../protect/microsoft-tunnel-mam-android.md)
- [Microsoft Tunnel for MAM - iOS/iPadOS](../protect/microsoft-tunnel-mam-ios.md)

## Week of October 23, 2023 (Service release 2310)

### App management

#### Update for users of Android Company Portal app<!-- 25109006   -->

If users launch a version of the Android Company Portal app below version 5.0.5333.0 (released November 2021), they'll see a prompt encouraging them to update their Android Company Portal app. If a user with an older Android Company Portal version attempts a new device registration using a recent version of the Authenticator app, the process will likely fail. To resolve this behavior, update the Android Company Portal app.

#### Minimum SDK version warning for iOS devices<!-- 9410239  -->

The **Min SDK version** for the iOS Conditional Launch setting on iOS devices now includes a **warn** action. This action warns end users if the min SDK version requirement isn't met.

For more information, see [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md).

#### Minimum OS for Apple LOB and store apps<!-- 24623225  -->

You can configure the minimum operating system to be the latest Apple OS releases for both Apple line-of-business apps and iOS/iPadOS store apps. You can set the minimum operating system for Apple apps as follows:

- iOS/iPadOS 17.0 for iOS/iPadOS line-of-business apps
- macOS 14.0 for macOS line-of-business apps
- iOS/iPadOS 17.0 for iOS/iPadOS store apps

Applies to:

- iOS/iPadOS
- macOS

#### Android (AOSP) supports line-of-business (LOB) apps<!-- 24823138   -->

You can install and uninstall mandatory LOB apps on AOSP devices by using the **Required** and **Uninstall** group assignments.

Applies to:

- Android

To learn more about managing LOB apps, see [Add an Android line-of-business app to Microsoft Intune](../apps/lob-apps-android.md).

#### Configuration scripts for unmanaged macOS PKG apps<!-- 17745891  -->

You can now configure pre-install and post-install scripts in unmanaged macOS PKG apps. This feature gives you greater flexibility over custom PKG installers. Configuring these scripts is optional and requires the Intune agent for macOS devices v2309.007 or higher.

For more information about adding scripts to unmanaged macOS PKG apps, see [Add an unmanaged macOS PKG app](../apps/macos-unmanaged-pkg.md).

### Device configuration

#### FSLogix settings are available in the Settings Catalog and Administrative Templates<!-- 10946920  -->

The [FSLogix settings](/fslogix/reference-configuration-settings) are available in the Settings Catalog and in Administrative Templates (ADMX) for you to configure.

Previously, to configure FSLogix settings on Windows devices, you imported them using the ADMX import feature in Intune.

Applies to:

- Windows 10
- Windows 11

For more information on these features, see:

- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Use Windows 10/11 templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md)
- [What is FSLogix?](/fslogix/overview-what-is-fslogix)

#### Use delegated scopes in your Managed Google Play apps that configure enhanced permissions on Android Enterprise devices<!-- 14029609  -->

In your Managed Google Play apps, you can give apps enhanced permissions using delegated scopes.

When your apps include delegated scopes, you can configure the following settings in a device configuration profile (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Device Restrictions** for profile type > **Applications**):

- **Allow other apps to install and manage certificates**: Admins can select multiple apps for this permission. The selected apps are granted access to certificate installation and management.
- **Allow this app to access Android security logs**: Admins can select one app for this permission. The selected app is granted access to security logs.
- **Allow this app to access Android network activity logs**: Admins can select one app for this permission. The selected app is granted access to network activity logs.

To use these settings, your Managed Google Play app must use delegated scopes.

Applies to:

- Android Enterprise fully managed devices
- Android Enterprise dedicated devices
- Android Enterprise corporate-owned devices with a work profile

For more information on this feature, see:

- [Android's built-in app configurations](../developer/app-sdk-android-phase6.md#androids-built-in-app-configurations)
- [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune > Applications](../configuration/device-restrictions-android-for-work.md#applications)

#### Samsung ended support for kiosk mode on Android device administrator (DA) devices<!-- 24810356  -->

Samsung marked the Samsung Knox kiosk APIs used on Android device administrator as deprecated in Knox 3.7 (Android 11).

Though the functionality might continue to work, there's no guarantee that it will continue working. Samsung won't fix bugs that might arise. For more information on Samsung support for deprecated APIs, see [What kind of support is offered after an API is deprecated?](https://docs.samsungknox.com/dev/knox-sdk/faqs/general/deprecated-api-support-change.htm) (opens Samsung's web site).

Instead, you can manage kiosk devices with Intune using [dedicated device management](../enrollment/android-kiosk-enroll.md).

Applies to:

- Android device administrator (DA)

#### Import and export settings catalog policies<!-- 3470151  -->

The Intune [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure, and all in one place (**Devices** > **Manage devices** > **Configuration** > **Create** > **New Policy** > Select your **platform** > For **Profile type**, select **Settings catalog**).

The settings catalog policies can be imported and exported:

- To export an existing policy, select the profile > select the ellipsis > **Export JSON**.
- To import a previously exported settings catalog policy, select **Create** > **Import policy** > select the previously exported JSON file.

For more information about the settings catalog, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

> [!NOTE]
>
> This feature is continuing to roll out. It may be a couple of weeks before it's available in your tenant.

#### New setting to block users from using the same password to unlock the device and access the work profile on Android Enterprise personally owned devices with a work profile<!-- 6167371  -->

On Android Enterprise personally owned devices with a work profile, users can use the same password to unlock the device and access the work profile.

There's a new setting that can enforce different passwords to unlock the device and access the work profile (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** > **Personally Owned Work Profile** for platform > **Device Restrictions** for profile type):

- **One lock for device and work profile**: **Block** prevents users from using the same password for the lock screen on the device and work profile. End users are required to enter the device password to unlock the device and enter their work profile password to access their work profile. When set to **Not Configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to access their work profile using a single password.

This setting is optional and doesn't impact existing configuration profiles.

Currently, if the work profile password doesn't meet the policy requirements, then device users see a notification. The device isn't marked as non-compliant. A separate compliance policy for the work profile is being created and will be available in a future release.

Applies to:

- Android Enterprise personally owned devices with a work profile (BYOD)

For a list of settings you can configure on personally owned devices with a work profile, see [Android Enterprise device settings list to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-enterprise-personal.md).

#### New settings available in the macOS settings catalog<!-- 24950434  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** > **Settings catalog** for profile type.

**Privacy > Privacy Preferences Policy Control**:

- System Policy App Data

**Restrictions**:

- Force On Device Only Dictation

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Device enrollment

#### Web based device enrollment with JIT registration for personal iOS/iPadOS devices<!-- 15412485  -->

Intune supports web-based device enrollment with just in time (JIT) registration for personal devices set up via Apple device enrollment. JIT registration reduces the number of authentication prompts shown to users throughout the enrollment experience and establishes SSO across the device. Enrollment takes place on the web version of Intune Company Portal, eliminating need for the Company Portal app. Also, this enrollment method enables employees and students without managed Apple IDs to enroll devices and access volume-purchased apps.

For more information, see [Set up web based device enrollment for iOS](../enrollment/web-based-device-enrollment-ios.md).

### Device management

#### Updates to the Intune add-ons page<!--17395941 -->

The Intune add-ons page under **Tenant administration** includes **Your add-ons**, **All add-ons**, and **Capabilities**. It provides an enhanced view into your trial or purchased licenses, the add-on capabilities you're licensed to use in your tenant, and support for new billing experiences in Microsoft admin center.

For more information, see [Use Intune Suite add-ons capabilities](intune-add-ons.md).

#### Remote Help for Android is now Generally available<!--17675897 -->

Remote Help is generally available for Android Enterprise Dedicated devices from Zebra and Samsung.

With Remote Help, IT Pros can remotely view the device screen and take full control in both attended and unattended scenarios, to diagnose and resolve issues quickly and efficiently.

Applies to:

- Android Enterprise Dedicated devices, manufactured by Zebra or Samsung

For more information, see [Remote Help on Android](remote-help-android.md).

### Device security

#### Configure declarative software updates and passcode policies for Apple devices in the Settings Catalog<!-- 24989083  -->

You can manage software updates and passcode using Apple's declarative device management (DDM) configuration using the settings catalog (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type > **Declarative device management**).

For more information about DDM, see [Apple's declarative device management (DDM)](https://developer.apple.com/documentation/devicemanagement/leveraging_the_declarative_management_data_model_to_scale_devices) (opens Apple's website).

DDM allows you to install a specific update by an enforced deadline. The autonomous nature of DDM provides an improved user experience as the device handles the entire software update lifecycle. It prompts users that an update is available and also downloads, prepares the device for the installation, & installs the update.

In the settings catalog, the following declarative software update settings are available at **Declarative device management > Software Update**:

- **Details URL**: The web page URL that shows the update details. Typically, this URL is a web page hosted by your organization that users can select if they need organization-specific help with the update.
- **Target Build Version**: The target build version to update the device to, like `20A242`. The build version can include a supplemental version identifier, like `20A242a`. If the build version you enter isn't consistent with the **Target OS Version** value you enter, then the **Target OS Version** value takes precedence.
- **Target Local Date Time**: The local date time value that specifies when to force install the software update. If the user doesn't trigger the software update before this time, then the device force installs it.
- **Target OS Version**: The target OS version to update the device to. This value is the OS version number, like `16.1`. You can also include a supplemental version identifier, like `16.1.1`.

For more information on this feature, see [Manage software updates with the settings catalog](../protect/managed-software-updates-ios-macos.md).

In the settings catalog, the following declarative passcode settings are available at **Declarative device management > Passcode**:

- **Automatic Device Lock**: Enter the maximum time period that a user can be idle before the system automatically locks the device.
- **Maximum Grace Period**: Enter the maximum time period that a user can unlock the device without a passcode.
- **Maximum Number of Failed Attempts**: Enter the maximum number of wrong passcode attempts before:
  - iOS/iPadOS wipes the device
  - macOS locks the device
- **Minimum Passcode Length**: Enter the minimum number of characters a passcode must have.
- **Passcode Reuse Limit**: Enter the number of previously used passcodes that can't be used.
- **Require Complex Passcode**: When set to **True**, a complex passcode is required. A complex passcode doesn't have repeated characters, and doesn't have increasing or decreasing characters, like `123` or `CBA`.
- **Require Passcode on Device**: When set to **True**, the user must set a passcode to access the device. If you don't set other passcode restrictions, then there aren't any requirements about the length or quality of the passcode.

Applies to:

- iOS/iPadOS 17.0 and later
- macOS 14.0 and later

For information about the settings catalog, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

#### Mvision Mobile is now Trellix Mobile Security<!-- 16208061 -->

The Intune [Mobile Threat Defense partner](../protect/mobile-threat-defense.md) **Mvision Mobile** has transitioned to **Trellix Mobile Security**. With this change, we've updated our documentation and the Intune admin center UI. For example, the *Mvision Mobile connector* is now *Trellix Mobile Security*. Existing installs of the Mvision Mobile connector also update to Trellix Mobile Security.

If you have questions about this change, reach out to your Trellix Mobile Security representative.

### Intune apps

#### Newly available protected app for Intune<!-- 24920511, 24950232  -->

The following protected app is now available for Microsoft Intune:

- BuddyBoard by Brother Industries, LTD
- Microsoft Loop by Microsoft Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Updated reports for Policy compliance and Setting compliance are now generally available<!-- 24299948, 24299945  -->

The following device compliance reports are out of public preview and are now generally available:

- [Policy compliance](reports.md#policy-compliance-report-organizational)
- [Setting compliance](reports.md#settings-compliance--organizational)

With this move to general availability, the older versions of both reports have been retired from the Intune admin center and are no longer available.

For more information about these changes, see the Intune Support Team blog at [https://aka.ms/Intune/device_compl_report](https://aka.ms/Intune/device_compl_report).

### Tenant administration

#### Intune admin center home page update<!-- 16950040  -->

The Intune admin center home page has been redesigned with a fresh new look and more dynamic content. The **Status** section has been simplified. You can explore Intune related capabilities in the **Spotlight** section. The **Get more out of Intune** section provides links to the Intune community and blog, and Intune customer success. Also, the **Documentation and training** section provides links to **What's New in Intune**, **Feature in development**, and more training. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Home**.

## Week of October 16, 2023

### Tenant administration

#### `endpoint.microsoft.com` URL redirects to `intune.microsoft.com`<!-- 25169925 -->

Previously, it was announced that the Microsoft Intune admin center has a new URL (`https://intune.microsoft.com`).

The `https://endpoint.microsoft.com` URL now redirects to `https://intune.microsoft.com`.

## Week of September 18, 2023 (Service release 2309)

### App management

#### MAM for Windows general availability<!-- 12394345, 12394352 -->

You can now enable protected MAM access to org data via Microsoft Edge on personal Windows devices. This capability uses the following functionality:
- Intune Application Configuration Policies (ACP) to customize the org user experience in Microsoft Edge
- Intune Application Protection Policies (APP) to secure org data and ensure the client device is healthy when using Microsoft Edge
- Windows Security Center threat defense integrated with Intune APP to detect local health threats on personal Windows devices
- Application Protection Conditional Access to ensure the device is protected and healthy before granting protected service access via Microsoft Entra ID.

Intune Mobile Application Management (MAM) for Windows is available for Windows 11, build 10.0.22621 (22H2) or later. This feature includes the supporting changes for Microsoft Intune (2309 release), Microsoft Edge (v117 stable branch and later) and Windows Security Center (v 1.0.2309.xxxxx and later). App Protection Conditional Access is in Public Preview.

Sovereign cloud support is expected in the future. For more information, see [App protection policy settings for Windows](../apps/app-protection-policy-settings-windows.md).

### Device configuration

#### OEMConfig profiles that don't deploy successfully aren't shown as "pending"<!-- 24284049 -->

For Android Enterprise devices, you can create a configuration policy that configures the OEMConfig app (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **OEMConfig** for profile type).

Previously, OEMConfig profiles that exceed 350 KB show a "pending" state. This behavior changed. An OEMConfig profile that exceeds 350 KB isn't deployed to the device. Profiles in a pending state or profiles larger that 350 KB aren't shown. Only profiles that successfully deploy are shown.

This change is a UI change only. No changes are made to the corresponding Microsoft Graph APIs.

To monitor the profile pending status in the Intune admin center, go to **Devices** > **Manage devices** > **Configuration** > Select the profile > **Device status**.

Applies to:

- Android Enterprise

For more information on OEM Configuration, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

#### Config Refresh settings are in the settings catalog for Windows Insiders<!-- 15060174  -->

In the Windows Settings Catalog, you can configure **Config Refresh**. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check in to Intune.

Config Refresh:

- Enable config refresh
- Refresh cadence (minutes)

Applies to:

- Windows 11

For more information on the Settings Catalog, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

#### Managed Settings now available in the Apple settings catalog<!-- 21083384  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

The settings within the Managed Settings command are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** > **Settings catalog** for profile type.

**Managed Settings > App Analytics**:

- Enabled: If true, enable sharing app analytics with app developers. If false, disable sharing app analytics.

Applies to:

- Shared iPad

**Managed Settings > Accessibility Settings**:

- Bold Text Enabled
- Grayscale Enabled
- Increase Contrast Enabled
- Reduce Motion Enabled
- Reduce Transparency Enabled
- Text Size
- Touch Accommodations Enabled
- Voice Over Enabled
- Zoom Enabled

**Managed Settings > Software Update Settings**:

- Recommendation Cadence: This value defines how the system presents software updates to the user.

**Managed Settings > Time Zone**:

- Time Zone: The Internet Assigned Numbers Authority (IANA) time zone database name.

Applies to:

- iOS/iPadOS

**Managed Settings > Bluetooth**:

- Enabled: If true, enable the Bluetooth setting. If false, disable the Bluetooth setting.

**Managed Settings > MDM Options**:

- Activation Lock Allowed While Supervised: If true, a supervised device registers itself with Activation Lock when the user enables Find My.

Applies to:

- iOS/iPadOS
- macOS

For more information on these settings, see [Apple's developer website](https://developer.apple.com/documentation/devicemanagement/settingscommand/command/settings). For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### New settings available in the macOS settings catalog<!-- 24809885  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There's a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** > **Settings catalog** for profile type.

**Microsoft Defender > Cloud delivered protection preferences**:

- Cloud Block Level

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Intune integration with the Zebra Lifeguard Over-the-Air service is generally available<!-- 16238201  -->

Microsoft Intune supports integration with Zebra Lifeguard Over-the-Air service, which allows you to deliver OS updates and security patches over-the-air to eligible Zebra devices that are enrolled with Intune. You can select the firmware version you want to deploy, set a schedule, and stagger update downloads and installs. You can also set minimum battery, charging status, and network conditions requirements for when the update can happen.

This integration is now generally available for Android Enterprise Dedicated and Fully Managed Zebra devices that are running Android 8 or later. It also requires a Zebra account and Intune Plan 2 or Microsoft Intune Suite.

Previously, this feature was in public preview and free for use. With this release as generally available, this solution now requires an add-on license for its use.

For licensing details, see [Intune add-ons](intune-add-ons.md).

### Device enrollment

#### SSO support during enrollment for Android Enterprise fully managed and corporate-owned devices with a work profile<!-- 8080357 -->

Intune supports single sign-on (SSO) on Android Enterprise devices that are fully managed or corporate-owned with a work profile.  With the addition of SSO during enrollment, end users enrolling their devices only need to sign in once with their work or school account.


Applies to:

- Android Enterprise corporate owned devices with a work profile
- Android Enterprise fully managed

For more information on these enrollment methods, see:

- [Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile](../enrollment/android-corporate-owned-work-profile-enroll.md)
- [Set up enrollment for Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md)

### Device management

#### Introducing Remote Help on macOS<!--12454029 -->

The Remote Help web app allows users to connect to macOS devices and join a view-only remote assistance session.

Applies to:

- 11 Big Sur
- 12 Monterey
- 13 Ventura

For more information on Remote Help on macOS, see [Remote Help](remote-help-macos.md).

#### Management certificate expiration date<!-- 17648747  -->

Management certificate expiration date is available as a column in the **Devices** workload. You can filter on a range of expiration dates for the management certificate and also export a list of devices with an expiration date matching the filter.

This information is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **All devices**.

#### Windows Defender Application Control (WDAC) references are updated to App Control for Business<!-- 24863807  -->

Windows renamed *Windows Defender Application Control* (WDAC) as *App Control for Business*. With this change, the references in Intune docs and the Intune admin center are updated to reflect this new name.

#### Intune supports iOS/iPadOS 15.x as the minimum version<!-- 24161619 -->

Apple released iOS/iPadOS version 17. Now, the minimum version supported by Intune is iOS/iPadOS 15.x.

Applies to:

- iOS/iPadOS

> [!NOTE]
>
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

#### Government tenant support for endpoint security Application Control policy and managed installer<!-- 24850055   -->

We've added support to use endpoint security [Application Control policies](../protect/endpoint-security-app-control-policy.md), and to configure a managed installer, to the following sovereign cloud environments:

- US Government clouds
- 21Vianet in China

Support for Application Control policy and managed installers was originally [released in preview in June 2023](#new-endpoint-security-application-control-policy-in-preview). Application Control policies in Intune are an implementation of Defender Application Control (WDAC).

### Device security

#### Endpoint Privilege Management support for Windows 365 devices<!-- 17016794  -->

You can now use [Endpoint Privilege Management](../protect/epm-overview.md) to manage application elevations on Windows 365 devices (also known as Cloud PCs).

This support doesn't include Azure Virtual Desktop.

#### Elevation report by Publisher for Endpoint Privilege Management<!--  24593400  -->

We've released a new report named **Elevation report by Publisher** for Endpoint Privilege Management (EPM). With [this new report](../protect/epm-reports.md#elevation-report-by-publisher) you can view all managed and unmanaged elevations, which are aggregated by the publisher of the app that is elevated.

You'll find the report in the Report node for EPM in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Navigate to **Endpoint security** > **Endpoint Privilege Management** and then select the **Reports** tab.

#### macOS support with Intune Endpoint security policies for Endpoint detection and response<!--  17757981 -->

Intune Endpoint security policies for *Endpoint detection and response* (EDR) now support macOS. To enable this support, we've added a new [EDR template profile for macOS](../protect/endpoint-security-edr-policy.md#devices-managed-by-microsoft-intune). Use this profile with macOS devices enrolled with Intune and macOS devices managed through the opt-in public preview of the [Defender for Endpoint security settings management](../protect/mde-security-integration.md?pivots=mdssc-preview) scenario.

The EDR template for macOS includes the following settings for the *Device tags* category from Defender for Endpoint:

- **Type of  tag** – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.
- **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn't be repeated in the same profile.

To learn more about Defender for Endpoint settings that are available for macOS, see [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences#device-tags) in the Defender documentation.

#### Linux support with Intune Endpoint security policies for Endpoint detection and response<!--  17757972  -->

Intune Endpoint security policies for *Endpoint detection and response* (EDR) now support Linux. To enable this support, we've added a new [EDR template profile for Linux](../protect/endpoint-security-edr-policy.md#devices-managed-by-microsoft-intune). Use this profile with Linux devices enrolled with Intune and Linux devices managed through the opt-in public preview of the [Defender for Endpoint security settings management](../protect/mde-security-integration.md?pivots=mdssc-preview) scenario.

The EDR template for Linux includes the following settings for the *Device tags* category from Defender for Endpoint:

- **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn't be repeated in the same profile.
- **Type of tag** – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.

You can learn more about Defender for Endpoint settings that are available for Linux in [Set preferences for Microsoft Defender for Endpoint on Linux](/microsoft-365/security/defender-endpoint/linux-preferences#device-tags) in the Defender documentation.

### Monitor and troubleshoot 

#### Updated reports for Update rings for Windows 10 and later<!-- 10159960 -->

Reporting for [Update rings for Windows 10 and later](../protect/windows-10-update-rings.md) has been updated to use Intune's improved reporting infrastructure. These changes align to similar improvements introduced for other Intune features.

With this change for reports for Update rings for Windows 10 and later, when you select an update rings policy in the Intune admin center, there isn't a left-pane navigation for *Overview*, *Manage*, or *Monitor* options. Instead, the policy view opens to a single pane that includes the following policy details:

- **Essentials** – including the policy name, created and modified dates, and more details.
- **Device and user check-in status** – This view is the default report view and includes:
  - A high-level overview of device status for this policy, and a *View report* button to open a more comprehensive report view.
  - A streamlined representation and count of the different device status values returned by devices assigned to the policy. The simplified bar and chart replace former doughnut charts seen in the prior reporting representation.
- Two other report tiles to open more reports. These tiles include:
  - **Device assignment status** – This report combines the same information as the previous Device status and User status reports, which are no longer available. However, with this change, pivots and drill-in through based on the user name is no longer available.
  - **Per setting status** – This new report provides success metrics for each setting configured differently than the defaults, allowing for new insight to which settings might not be successfully deploying to your organization.
- **Properties** – View details for each configuration page of the policy, including an option to **Edit** each areas profile details.

For more information about reports for update rings for Windows 10 and later, see [Reports for Update rings for Windows 10 and later policy](../protect/windows-update-reports.md#reports-for-update-rings-for-windows-10-and-later-policy) in the Windows Update reports for Microsoft Intune article.

### Role-based access

#### Updating the scope of UpdateEnrollment<!--25077072 -->

With the introduction of a new role **UpdateEnrollment**, the scope of **UpdateOnboarding** is getting updated.

The **UpdateOnboarding** setting for custom and built-in roles is modified to only manage or change the Android Enterprise binding to Managed Google Play and other account-wide configurations. Any built-in roles that used **UpdateOnboarding** will now have **UpdateEnrollmentProfiles** included.

The resource name is being updated from **Android for work** to **Android Enterprise**.

For more information, see [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md).

## Week of September 11, 2023

### Device configuration

#### Introducing Remote Launch on Remote Help<!--9843475 -->

With Remote Launch, the helper can launch Remote Help seamlessly on the helper and user's device from Intune by sending a notification to the user's device. This feature allows both helpdesk and the sharer to be connected to a session quickly without exchanging session codes.

Applies to:

- Windows 10/11

For more information, see [Remote Help](remote-help-windows.md).

## Week of September 4, 2023

### Device management

#### Microsoft Intune ending support for Android device administrator on devices with GMS access in August 2024<!--13891824 -->

Microsoft Intune is ending support for [Android device administrator management](../enrollment/android-enroll-device-administrator.md) on devices with access to Google Mobile Services (GMS) on August 30, 2024. After that date, device enrollment, technical support, bug fixes, and security fixes will be unavailable.

If you currently use device administrator management, we recommend switching to another Android management option in Intune before support ends.

For more information, see [Ending support for Android device administrator on GMS devices](https://aka.ms/Intune-Android-DA-blog).

## Week of August 28, 2023

### Device configuration

#### Windows and Android support for 4096-bit key size for SCEP and PFX certificate profiles<!--16314561  -->

Intune [SCEP certificate profiles](../protect/certificates-profile-scep.md) and [PKCS certificate profiles](../protect/certificates-pfx-configure.md) for Windows and Android devices now support a **Key size (bits)** of **4096**. This key size is available for new profiles and existing profiles you choose to edit.

- SCEP profiles have always included the *Key size (bits)* setting and now support 4096 as an available configuration option.
- PKCS profiles don't include the *Key size (bits)* setting directly. Instead, an admin must [modify the certificate template on the Certification Authority](../protect/certificates-pfx-configure.md#configure-certificate-templates-on-the-ca) to set the *Minimum key size* to 4096.

If you use a third-party Certificate Authority (CA), you might need to contact your vendor for assistance with implementing the 4096-bit key size.

When updating or deploying new certificate profiles to take advantage of this new key size, we recommend using a staggered deployment approach. This approach can help avoid creating excessive demand for new certificates across a large number of devices at the same time.

With this update, be aware of the following limitations on Windows devices:

- 4096-bit key storage is supported only in the *Software Key Storage Provider* (KSP). The following don't support storing keys of this size:
  - The hardware TPM (Trusted Platform Module). As a workaround you can use the Software KSP for key storage.
  - Windows Hello for Business. There isn't a workaround at this time.

### Tenant administration

#### Access policies for multiple Administrator Approval are now generally available<!-- 24936423   -->

Access policies for multiple Administrator Approval are out of public preview and are now generally available. With these policies, you can protect a resource, like App deployments, by requiring any change to the deployment to be approved by one of a group of users who are *approvers* for the resource, before that change is applied.

For more information, see [Use Access policies to require multiple administrative approval](multi-admin-approval.md).

## Week of August 21, 2023 (Service release 2308)

### App management

#### Managed Home Screen end-users prompted to grant exact alarm permission<!-- 19804494 -->  
Managed Home Screen uses the exact alarm permission to do the following actions:

- Automatically sign out users after a set time of inactivity on the device
- Launch a screen saver after a set period of inactivity
- Automatically relaunch MHS after a certain period of time when a user exits kiosk mode

For devices running Android 14 and higher, by default, the exact alarm permission will be denied. To make sure critical user functionality isn't impacted, end-users are prompted to grant exact alarm permission upon first launch of Managed Home Screen. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](..\apps\app-configuration-managed-home-screen-app.md) and [Android's developer documentation]( https://developer.android.com/about/versions/14/changes/schedule-exact-alarms).

#### Managed Home Screen notifications<!-- 19805777  -->  
For Android devices running Android 13 or higher that target API level 33, by default, applications don't have permission to send notifications. In previous versions of Managed Home Screen, when an admin had enabled automatic relaunch of Managed Home Screen, a notification was displayed to alert users of the relaunch. To accommodate change to notification permission, in the scenario when an admin has enabled auto-relaunch of Managed Home Screen, the application will now display a toast message alerting users of the relaunch. Managed Home Screen is able to auto-grant permission for this notification, so no change is required for admins configuring Managed Home Screen to accommodate the change in notification permission with API level 33. For more information about Android 13 (API level 33) notification messages, see the [Android developer documentation](https://developer.android.com/develop/ui/views/notifications/notification-permission). For more information about Managed Home Screen, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### New macOS web clip app type<!-- 24128407  -->  
In Intune, end users can pin web apps to the dock on your macOS devices (**Apps** > **macOS** > **Add** > **macOS web clip**).

Applies to:

- macOS

For related information about the settings you can configure, see [Add web apps to Microsoft Intune](../apps/web-app.md).

#### Win32 app configurable installation time<!-- 17644704  -->  
In Intune, you can set a configurable installation time to deploy Win32 apps. This time is expressed in minutes. If the app takes longer to install than the set installation time, the system will fail the app install. Max timeout value is 1440 minutes (1 day). For more information about Win32 apps, see [Win32 app management in Microsoft Intune](../apps/apps-win32-add.md#step-2-program).

#### Samsung Knox conditional launch check<!-- 8610063   -->  
You can add more detection of device health compromises on Samsung Knox devices. Using a conditional launch check within a new Intune App Protection Policy, you can require that hardware-level device tamper detection and device attestation be performed on compatible Samsung devices. For more information, see the **Samsung Knox device attestation** setting in the **Conditional launch** section of [Android app protection policy settings in Microsoft Intune](../apps/app-protection-policy-settings-android.md#device-conditions).

### Device configuration

#### Remote Help for Android in public preview<!-- 16238217 -->  
Remote Help is available in public preview for Android Enterprise Dedicated devices from Zebra and Samsung. With Remote Help, IT Pros can remotely view the device screen and take full control in both attended and unattended scenarios, to diagnose and resolve issues quickly and efficiently.

Applies to:

- Android Enterprise Dedicated devices, manufactured by Zebra or Samsung

For more information, see [Remote Help on Android](remote-help-android.md).

#### Group Policy analytics is generally available<!-- 24249203  -->  
Group Policy analytics is generally available (GA). Use Group Policy analytics to analyze your on-premises group policy objects (GPOs) for their migration to Intune policy settings.

Applies to:

- Windows 11
- Windows 10

For more information about Group Policy analytics, see [Analyze your on-premises GPOs using Group Policy analytics in Microsoft Intune](../configuration/group-policy-analytics.md).

#### New SSO, login, restrictions, passcode, and tamper protection settings available in the Apple settings catalog<!-- 24335541  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** > **Settings catalog** for profile type.

##### iOS/iPadOS 17.0 and later

**Restrictions**:

- Allow iPhone Widgets On Mac

##### macOS

**Microsoft Defender > Tamper protection**:

- Process's arguments
- Process path
- Process's Signing Identifier
- Process's Team Identifier
- Process exclusions

##### macOS 13.0 and later

**Authentication > Extensible Single Sign On (SSO)**:

- Account Display Name
- Additional Groups
- Administrator Groups
- Authentication Method
- Authorization Right
- Group
- Authorization Group
- Enable Authorization
- Enable Create User At Login
- Login Frequency
- New User Authorization Mode
- Account Name
- Full Name
- Token To User Mapping
- User Authorization Mode
- Use Shared Device Keys

##### macOS 14.0 and later

**Login > Login Window Behavior**:

- Autologin Password
- Autologin Username

**Restrictions**:

- Allow ARD Remote Management Modification
- Allow Bluetooth Sharing Modification
- Allow Cloud Freeform
- Allow File Sharing Modification
- Allow Internet Sharing Modification
- Allow Local User Creation
- Allow Printer Sharing Modification
- Allow Remote Apple Events Modification
- Allow Startup Disk Modification
- Allow Time Machine Backup

**Security > Passcode**:

- Password Content Description
- Password Content Regex

### Device enrollment

#### Just-in-time registration and compliance remediation for iOS/iPadOS Setup Assistant with modern authentication now generally available<!-- 16276610 -->

Just in time (JIT) registration and compliance remediation for Setup Assistant with modern authentication are now out of preview and generally available. With just in time registration, the device user doesn't need to use the Company Portal app for Microsoft Entra registration and compliance checking. JIT registration and compliance remediation are embedded into the user's provisioning experience, so they can view their compliance status and take action within the work app they're trying to access. Also, this establishes single-sign on across the device. For more information about how to set up JIT registration, see [Set up Just in Time Registration](../enrollment/automated-device-enrollment-authentication.md).

#### Awaiting final configuration for iOS/iPadOS automated device enrollment now generally available<!-- 17473384  -->  
Now generally available, *awaiting final configuration* enables a locked experience at the end of Setup Assistant to ensure that critical device configuration policies install on devices. The locked experience works on devices targeted with new and existing enrollment profiles. Supported devices include:

- iOS/iPadOS 13+ devices enrolling with Setup Assistant with modern authentication
- iOS/iPadOS 13+ devices enrolling without user affinity  
- iOS/iPadOS 13+ devices enrolling with Microsoft Entra ID shared mode  

This setting is applied once during the out-of-box automated device enrollment experience in Setup Assistant. The device user doesn't experience it again unless they re-enroll their device.  Awaiting final configuration is enabled by default for new enrollment profiles. For information about how to enable awaiting final configuration, see [Create an Apple enrollment profile](..//enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

### Device management

#### Changes to Android notification permission prompt behavior<!-- 19783177  -->  
We've updated how our Android apps handle notification permissions to align with recent changes made by Google to the Android platform.  As a result of Google changes, notification permissions are granted to apps as follows:

- **On devices running Android 12 and earlier**: Apps are permitted to send notifications to users by default.
- **On devices running Android 13 and later**: Notification permissions vary depending on the API the app targets.
  - *Apps targeting API 32 and lower*: Google has added a notification permission prompt that appears when the user opens the app. Management apps can still configure apps so that they're automatically granted notification permissions.
  - *Apps targeting API 33 and higher*: App developers define when the notification permission prompts appear. Management apps can still configure apps so that they're automatically granted notification permissions.

You and your device users can expect to see the following changes now that our apps target API 33:

- **Company Portal used for work profile management**: Users see a notification permission prompt in the personal instance of the Company Portal when they first open it. Users don't see a notification permission prompt in the work profile instance of Company Portal because notification permissions are automatically permitted for Company Portal in the work profile. Users can silence app notifications in the Settings app.
- **Company Portal used for device administrator management**: Users see a notification permission prompt when they first open the Company Portal app.  Users can adjust app notification settings in the Settings app.
- **Microsoft Intune app**: No changes to existing behavior. Users don't see a prompt because notifications are automatically permitted for the Microsoft Intune app.  Users can adjust some app notification settings in the Settings app.
- **Microsoft Intune app for AOSP**: No changes to existing behavior. Users don't see a prompt because notifications are automatically permitted for the Microsoft Intune app.  Users can't adjust app notification settings in the Settings app.

### Device security

#### Defender Update controls to deploy updates for Defender is now generally available<!-- 24666660 -->  
The profile **Defender Update controls** for Intune Endpoint security Antivirus policy, which manages update settings for Microsoft Defender, is now generally available. This profile is available for the *Windows 10, Windows 11, and Windows Server* platform. While in public preview, this profile was available for the *Windows 10 and later* platform.

The profile includes settings for the rollout release channel by which devices and users receive Defender Updates that are related to daily security intelligence updates, monthly platform updates, and monthly engine updates.

This profile includes the following settings, which are all directly taken from [Defender CSP - Windows Client Management](/windows/client-management/mdm/policy-csp-Defender).

- Engine Updates Channel
- Platform Updates Channel
- Security Intelligence Updates Channel

These settings are also available from the [settings catalog](../configuration/settings-catalog.md) for the *Windows 10 and later* profile.

#### Elevation report by applications for Endpoint Privilege Management<!-- 24593324 -->  
We've released a new report named **Elevation report by applications** for Endpoint Privilege Management (EPM). With [this new report](../protect/epm-reports.md#elevation-report-by-applications) you can view all managed and unmanaged elevations, which are aggregated by the application that elevated. This report can aid you in identifying applications that might require elevation rules to function properly, including rules for child processes.

You'll find the report in the Report node for EPM in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Navigate to **Endpoint security** > **Endpoint Privilege Management** and then select the **Reports** tab.

#### New settings available for macOS Antivirus policy<!-- 24191427 -->  
The [Microsoft Defender Antivirus](../protect/endpoint-security-antivirus-policy.md) profile for macOS devices has been updated with nine more settings, and three new settings categories:

**Antivirus engine** – The following settings are new in this category:

- **Degree of parallelism for on-demand scans** – Specifies the degree of parallelism for on-demand scans. This setting corresponds to the number of threads used to perform the scan and impacts the CPU usage, and the duration of the on-demand scan.
- **Enable file hash computation** – Enables or disables file hash computation feature. When this feature is enabled, Windows Defender computes hashes for files it scans. This setting helps improve the accuracy of Custom Indicator matches. However, enabling Enable file hash computation can impact device performance.
- **Run a scan after definitions are updated** – Specifies whether to start a process scan after new security intelligence updates are downloaded on the device. Enabling this setting triggers an antivirus scan on the running processes of the device.
- **Scanning inside archive files** – If true, Defender unpacks archives and scan files inside them. Otherwise archive content is skipped, which improves scanning performance.

**Network protection** – A new category that includes the following setting:

- **Enforcement level** – Configure this setting to specify if network protection is *disabled*, *in audit mode*, or *enforced*.

**Tamper  protection** - A new category that includes the following setting:

- **Enforcement level** - Specify whether tamper protection is *disabled*, in *audit mode*, or *enforced*.

**User interface preferences** – A new category that includes the following settings:

- **Control sign-in to consumer version** - Specify whether users can sign into the consumer version of Microsoft Defender.
- **Show / hide status menu icon** – Specify whether the status menu icon (shown in the top-right corner of the screen) is hidden or not.
- **User initiated feedback** – Specify whether users can submit feedback to Microsoft by going to *Help* > *Send Feedback*.

New profiles that you create include the original settings and the new settings. Your existing profiles automatically update to include the new settings, with each new setting set to *Not configured* until you choose to edit that profile to change it.

For more information about how to set preferences for Microsoft Defender for Endpoint on macOS in enterprise organizations, see [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences?view=o365-worldwide&preserve-view=true).

### Intune apps

#### Newly available protected app for Intune<!-- 24400497  -->  
The following protected app is now available for Microsoft Intune:

- VerityRMS by Mackey LLC (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### CloudDesktop log now collected with Windows diagnostics data<!-- 24541366 -->
The Intune remote action to [collect diagnostics](../remote-actions/collect-diagnostics.md) from a Windows device now includes data in a log file.

Log file:
- %temp%\CloudDesktop\*.log

#### Anomaly detection device cohorts in Intune Endpoint analytics is generally available<!-- 24577118  -->  
Anomaly detection device cohorts in Intune Endpoint analytics is now generally available.

Device cohorts are identified in devices associated with a high or medium severity anomaly. Devices are correlated into groups based on one or more factors they have in common like an app version, driver update, OS version, device model. A correlation group will contain a detailed view with key information about the common factors between all affected devices in that group. You can also view a breakdown of devices currently affected by the anomaly and 'at risk' devices. "At risk" devices haven't yet shown symptoms of the anomaly.

For more information, see [Anomaly detection in Endpoint analytics](../../analytics/anomaly-detection.md#anomalies-tab).

#### Improved user experience for device timeline in Endpoint Analytics<!-- 24604944 -->  
The user interface (UI) for device timeline in Endpoint analytics is improved and includes more advanced capabilities (support for sorting, searching, filtering, and exports). When viewing a specific device timeline in Endpoint analytics, you can search by event name or details. You can also filter the events and choose the source and level of events that appear on the device timeline and select a time range of interest.

For more information, see [Enhanced device timeline](../../analytics/enhanced-device-timeline.md).

#### Updates for compliance policies and reports<!--15425771  -->  
We've made several improvements to the Intune compliance policies and reports. With these changes, the reports more closely align to the experience in use for device configuration profiles and reports. We've updated our [compliance report documentation](../protect/compliance-policy-monitor.md) to reflect the available compliance report improvements.

Compliance report improvements include:

- Compliance details for Linux devices.
- Redesigned reports that are up-to-date and simplified, with newer report versions beginning to replace older report versions, which will remain available for some time.
- When viewing a policy for compliance, there isn't a left-pane navigation. Instead, the policy view opens to a single pane that defaults to the Monitor tab and its Device status view.
  - This view provides a high-level overview of device status for this policy, supports drilling in to review the full report, and a per-setting status view of the same policy.
  - The doughnut chart is replaced by a streamlined representation and count of the different device status values returned by devices assigned the policy.
  - You can select the Properties tab to view the policy details, and review and edit its configuration and assignments.
  - The *Essentials* section is removed with those details appearing in the policy's *Properties* tab.
- The updated status reports support sorting by columns, the use of filters, and search. Combined, these enhancements enable you to pivot the report to display specific subsets of details you want to view at that time. With these enhancements, we have removed the *User status* report as it has become redundant. Now, while viewing the default *Device status* report you can focus the report to display the same information that was available from *User status* by sorting on the *User Principal Name* column, or searching for a specific username in the search box.
- When viewing status reports, the count of devices that Intune displays now remains consistent between different report views as you drill in for deeper insights or details.

For more information about these changes, see the Intune Support Team blog at [https://aka.ms/Intune/device_compl_report](https://aka.ms/Intune/device_compl_report).

## Week of August 14, 2023

### App management

#### Use the Turn off the Store application setting to disable end user access to Store apps, and allow managed Intune Store apps<!-- 16544362 -->  
In Intune, you can use the new **Store app** type to deploy Store apps to your devices.

Now, you can use the **Turn off the Store application** policy to disable end users' direct access to Store apps. When it's disabled, end users can still access and install Store apps from the Windows Company Portal app and through Intune app management. If you want to allow random store app installs outside of Intune, then don't configure this policy.

The previous **Only display the private store within the Microsoft Store app** policy doesn't prevent end users from directly accessing the store using the Windows Package Manager `winget` APIs. So, if your goal is to block random unmanaged Store application installs on client devices, then it's recommended to use the **Turn off the Store application** policy. Don't use the **Only display the private store within the Microsoft Store app** policy.
Applies to:

- Windows 10 and later

For more information, see [Add Microsoft Store Apps to Microsoft Intune](../apps/store-apps-microsoft.md).

## Week of August 7, 2023

### Role-based access control

#### Introducing a new role-based access control (RBAC) permission under the resource Android for work<!--11298214 -->  
Introducing a new RBAC **Permission** for creating a custom role in Intune, under the resource **Android for work**. The permission **Update Enrollment Profile** allows the admin to manage or change both AOSP and Android Enterprise Device Owner enrollment profiles that are used to enroll devices.

For more information, see [Create custom role](create-custom-role.md).

## Week of July 31, 2023

### Device security

### New BitLocker profile for Intune's endpoint security Disk encryption policy<!-- 24631986   -->  
We have released a new experience creating new *BitLocker* profiles for endpoint security Disk Encryption policy. The experience for editing your previously created BitLocker policy remains the same, and you can continue to use them. This update applies only for the new [BitLocker](../protect/endpoint-security-disk-encryption-policy.md) policies you create for the *Windows 10 and later* platform.

This update is part of the continuing rollout of new profiles for endpoint security policies, which began in April 2022.

### App management

#### Uninstall Win32 and Microsoft store apps using the Windows Company Portal<!-- 4664389 -->  
End-users can uninstall Win32 apps and Microsoft store apps using the Windows Company Portal if the apps were assigned as available and were installed on-demand by the end-users. For Win32 apps, you have the option to enable or disable this feature (off by default). For Microsoft store apps, this feature is always on and available for your end-users. If an app can be uninstalled by the end-user, the end-user will be able to select **Uninstall** for the app in the Windows Company Portal. For related information, see [Add apps to Microsoft Intune](../apps/apps-add.md).

## Week of July 24, 2023 (Service release 2307)

### App management

#### Intune supports new Google Play Android Management API<!-- 10982449 -->  
Changes have been made to how Managed Google Play public apps are managed in Intune. These changes are to support [Google's Android Management APIs](https://developers.google.com/android/management) (opens Google's web site).

Applies to:

- Android Enterprise

To learn more about changes to the admin and user experience, see [Support Tip: Intune moving to support new Google Play Android Management API](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-intune-moving-to-support-new-google-play-android/ba-p/3849875).



#### App report for Android Enterprise corporate-owned devices<!-- 2055436  -->  
You can now view a report containing all apps found on a device for Android Enterprise corporate-owned scenarios, including system apps. This report is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Monitor** > **Discovered apps**. You'll see **Application Name** and **Version** for all apps detected as installed on the device. It can take up to 24 hours for app information to populate the report.

For related information, see [Intune discovered apps](../apps/app-discovered-apps.md).

#### Add unmanaged PKG-type applications to managed macOS devices [Public Preview]<!-- 17296091  -->  
You can now upload and deploy unmanaged PKG-type applications to managed macOS devices using the Intune MDM agent for macOS devices. This feature enables you to deploy custom PKG installers, such as unsigned apps and component packages. You can add a PKG app in the Intune admin center by selecting **Apps** > **macOS** > **Add** > **macOS app (PKG)** for app type.

Applies to:

- macOS

For more information, see [Add an unmanaged macOS PKG app to Microsoft Intune](../apps/macos-unmanaged-pkg.md). To deploy managed PKG-type app, you can continue to [add macOS line-of-business (LOB) apps to Microsoft Intune](../apps/lob-apps-macos.md). For more information about the Intune MDM agent for macOS devices, see [Microsoft Intune management agent for macOS](../apps/lob-apps-macos-agent.md).

#### New settings available for the iOS/iPadOS web clip app type<!-- 21084128   -->  
In Intune, you can pin web apps to your iOS/iPadOS devices (**Apps** > **iOS/iPadOS** > **Add** > **iOS/iPadOS web clip**). When you add web clips, there are new settings available:

- **Full screen**: If configured to **Yes**, launches the web clip as a full-screen web app without a browser. There isn't a URL nor search bar, and no bookmarks.
- **Ignore manifest scope**: If configured to **Yes**, a full screen web clip can navigate to an external web site without showing Safari UI. Otherwise, Safari UI appears when navigating away from the web clip's URL. This setting has no effect when **Full screen** is set to **No**. Available in iOS 14 and later.
- **Precomposed**: If configured to **Yes**, prevents Apple's application launcher (SpringBoard) from adding "shine" to the icon.
- **Target application bundle identifier**: Enter the application bundle identifier that specifies the application that opens the URL. Available in iOS 14 and later.

Applies to:

- iOS/iPadOS

For more information, see [Add web apps to Microsoft Intune](../apps/web-app.md).

#### Change to default settings when adding Windows PowerShell scripts<!-- 20986905  -->  
In Intune, you can use policies to deploy Windows PowerShell scripts to your Windows devices (**Devices** > **Scripts** > **Add** > **Windows 10 and later**). When you add a Windows PowerShell script, there are settings you configure. To increase secure-by-default behavior of Intune, the default behavior of the following settings has changed:

- The **Run this script using the logged on credentials** setting defaults to **Yes**. Previously, the default was **No**.
- The **Enforce script signature check** setting defaults to **Yes**. Previously, the default was **No**.

This behavior applies to new scripts you add, not existing scripts.

Applies to:

- Windows 10 and later (excluding Windows 10 Home)

For more information about using Windows PowerShell scripts in Intune, see [Use PowerShell scripts on Windows 10/11 devices in Intune](../apps/intune-management-extension.md).

### Device configuration

#### Added Support for Scope tags<!-- 16485280  -->  
You can now add scope tags when creating deployments using Zebra LifeGuard Over-the-Air integration (in public preview).

#### New settings available in the macOS settings catalog<!-- 24167142  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

**Microsoft AutoUpdate (MAU)**:

- Current Channel (Monthly)

**Microsoft Defender > User interface preferences**:

- Control sign-in to consumer version

**Microsoft Office > Microsoft Outlook**:

- Disable `Do not send response`

**User Experience > Dock**:

- MCX Dock Special Folders

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Compliance Retrieval service support for MAC address endpoints<!--  24332824  -->  
We've now added MAC address support to the Compliance Retrieval service.

The initial release of the CR service included support for using only the Intune device ID with the intent to eliminate the need to manage internal identifiers like serial numbers and MAC addresses. With this update, organizations that prefer to use MAC addresses over certificate authentication can continue to do so while implementing the CR service.

While this update adds MAC address support to the CR service, our recommendation is to use certificate-based authentication with the Intune device ID included in the certificate.

For information about the CR service as a replacement for the Intune Network Access Control (NAC) service, see the Intune blog at [https://techcommunity.microsoft.com/t5/intune-customer-success/new-microsoft-intune-service-for-network-access-control/ba-p/2544696](https://techcommunity.microsoft.com/t5/intune-customer-success/new-microsoft-intune-service-for-network-access-control/ba-p/2544696).

#### Settings insight within Intune security baselines is generally available<!-- 24507891   -->  
Announcing the general availability of Settings insight in Microsoft Intune.

The [Settings insight](settings-insight.md) feature adds insight to settings giving you confidence in configurations that have been successfully adopted by similar organizations. Settings insight is currently available for security baselines.

Navigate to **Endpoint security** > **Security baselines**. While creating and editing a workflow, these insights are available for all settings with light bulbs.

### Device security

#### Tamper protection support for Windows on Azure Virtual Desktop<!--15135590  -->  
Intune now supports use of endpoint security [Antivirus policy](../protect/endpoint-security-antivirus-policy.md#prerequisites-for-tamper-protection) to manage *Tamper protection* for Windows on Azure Virtual Desktop multi-session devices. Support for Tamper protection requires devices to onboard to Microsoft Defender for Endpoint before the policy that enables Tamper protection is applied.

#### EpmTools PowerShell module for Endpoint Privilege Management<!-- 22800379  -->  
The EpmTools PowerShell module is now available for use with Intune Endpoint Privilege Management (EPM). EpmTools includes the cmdlets like **Get-FileAttributes** that you can use to retrieve file details to help build accurate elevation rules, and other cmdlets you can use to troubleshoot or diagnose EPM policy deployments.

For more information, see [EpmTools PowerShell module](../protect/epm-overview.md#epmtools-powershell-module).

#### Endpoint Privilege Management support to manage elevation rules for child processes<!-- 15931887 -->  
With Intune Endpoint Privilege Management (EPM) you can manage which files and processes are allowed to *Run as Administrator* on your Windows devices.  Now, EPM [elevation rules](../protect/epm-policies.md#windows-elevation-rules-policy) support a new setting, **Child process behavior**.

With *Child process behavior*, your rules can manage the elevation context for any child processes created by the managed process. Options include:

- Allowing all child processes created by the managed process to always run as elevated.
- Allow a child process to run as elevated only when it matches the rule that manages its parent process.
- Deny all child processes from running in an elevated context, in which case they run as standard users.

Endpoint Privilege Management is available as an Intune add-on. For more information, see [Use Intune Suite add-on capabilities](intune-add-ons.md).

### Intune apps

#### Newly available protected app for Intune<!-- 24323519  -->  
The following protected app is now available for Microsoft Intune:

- Dooray! for Intune

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Updated reports for Setting compliance and Policy compliance are in public preview<!-- 15425624, 15425656  -->  
We've released two new reports as a public preview for Intune device compliance. You can find these new preview reports in the Intune admin center at **Reports** > **Device compliance** > *Reports* tab:

- [Setting compliance (preview)](reports.md)
- [Policy compliance (preview)](reports.md)

Both reports are new instances of existing reports, and deliver improvements over the older versions, including:  

- Details for Linux settings and devices
- Support for sorting, searching, filtering, exports, and paging views
- Drill-down reports for deeper details, which are filtered based on the column you select.
- Devices are represented a single time. This behavior is in contrast to the original reports, which could count a device more than once if multiple users used that device.

Eventually, the [older report versions](../protect/compliance-policy-monitor.md#other-compliance-reports) that are still available in the admin center at *Devices > Monitor* will be retired.

## Week of July 10, 2023

### App management

#### Updates to app configuration policy reporting<!-- 18098046  -->  
As part of our continuing efforts to improve the Intune reporting infrastructure, there have been several user interface (UI) changes for app configuration policy reporting. The UI has been updated with the following changes:

- There isn't a **User status** tile or a **Not applicable device** tile on the **Overview** section of the **App configuration policies** workload.
- There isn't a **User install status** report on the **Monitor** section of the **App configuration policies** workload.
- The **Device install status** report under the **Monitor** section of the **App configuration policies** workload no longer shows the **Pending state** in the **Status** column.

You can configure policy reporting in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Configuration**.

## Week of July 3, 2023

### Device management

#### Intune support for Zebra devices on Android 13<!-- 17192763 -->  
Zebra will be releasing support for Android 13 on their devices. You can read more at [Migrating to Android 13](https://techdocs.zebra.com/lifeguard/a13/) (opens Zebra's web site).

- **Temporary issues on Android 13**

  The Intune team thoroughly tested Android 13 on Zebra devices. Everything continues working as normal, except for the following two temporary issues for device administrator (DA) devices.

  For Zebra devices running Android 13 and enrolled with DA management:

  1. App installations don't happen silently. Instead, users get a notification from the Company Portal app (if they allow notifications) that asks for permission to allow the app installation. If a user doesn't accept the app installation when prompted, then the app doesn't install. Users will have a persistent notification in the notification drawer until they allow the installation.

  2. New MX profiles don't apply to Android 13 devices. Newly enrolled Android 13 devices don't receive configuration from MX profiles. MX profiles that previously applied to enrolled devices continue to apply.

  In an update coming later in July, these issues will be resolved and the behavior will return to how it was before.

- **Update devices to Android 13**

  You'll soon be able to use Intune's Zebra LifeGuard Over-the-Air integration to update Android Enterprise dedicated and fully managed devices to Android 13. For more information, see [Zebra LifeGuard Over-the-Air Integration with Microsoft Intune](../protect/zebra-lifeguard-ota-integration.md).

  Before you migrate to Android 13, review [Migrating to Android 13](https://techdocs.zebra.com/lifeguard/a13/) (opens Zebra's web site).

- **OEMConfig for Zebra devices on Android 13**

  OEMConfig for Zebra devices on Android 13 requires using Zebra's new [Zebra OEMConfig Powered by MX OEMConfig app](https://play.google.com/store/apps/details?id=com.zebra.oemconfig.release) (opens the Google Play store). This new app can also be used on Zebra devices running Android 11, but not earlier versions.

  For more information on this app, go to the [New Zebra OEMConfig app for Android 11 and later](https://techcommunity.microsoft.com/t5/intune-customer-success/new-zebra-oemconfig-app-for-android-11-and-later/ba-p/3846730) blog post.

  The [Legacy Zebra OEMConfig app](https://play.google.com/store/apps/details?id=com.zebra.oemconfig.common) (opens the Google Play store) can only be used on Zebra devices running Android 11 and earlier.

For more general information about Intune Android 13 support, go to the [Day Zero support for Android 13 with Microsoft Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/day-zero-support-for-android-13-with-microsoft-intune/ba-p/3601760) blog post.

### Device security

#### Defender for Endpoint security settings management enhancements and support for Linux and macOS in public preview<!-- 14743017, 15319901, 18713045, 18713050, 17757959 17757967, 17758270  -->  
With [Defender for Endpoint security settings management](../protect/mde-security-integration.md), you can use Intune's endpoint security policies to manage Defender security settings on devices that onboard to Defender for Endpoint but aren't enrolled with Intune.

Now, you can opt in to a public preview from within the Microsoft Defender portal to gain access to several enhancements for this scenario:

- Intune's endpoint security policies become visible in and can be managed from within the Microsoft Defender portal. This enables security admins to remain in the Defender portal to manage Defender and the Intune endpoint security policies for Defender security settings management.

- Security settings management supports deploying Intune endpoint security Antivirus policies to devices that run Linux and macOS.

- For Windows devices, the Windows Security Experience profile is now supported with security settings management.

- A new onboarding workflow removes the Microsoft Entra hybrid join prerequisite. Microsoft Entra hybrid join requirements prevented many Windows devices from successfully onboarding to Defender for Endpoint security settings management. With this change, those devices can now complete enrollment and start processing policies for security settings management.

- Intune creates a synthetic registration in Microsoft Entra ID for devices that can't fully register with Microsoft Entra ID. Synthetic registrations are device objects created in Microsoft Entra ID that enable devices to receive and report back on Intune policies for security settings management. In addition, should a device with a synthetic registration become fully registered, the synthetic registration is removed from Microsoft Entra ID in deference to the full registration.

If you don't opt in to the Defender for Endpoint Public Preview, the previous behaviors remain in place. In this case, while you can view the Antivirus profiles for Linux, you can't deploy it as its supported only for devices managed by Defender. Similarly, the macOS profile that's currently available for devices enrolled with Intune can't be deployed to devices managed by Defender.

Applies to:

- Linux
- macOS
- Windows

## Week of June 26, 2023

### Device configuration

#### Android (AOSP) supports assignment filters<!-- 7591220 -->  
Android (AOSP) supports assignment filters. When you create a filter for Android (AOSP), you can use the following properties:

- DeviceName
- Manufacturer
- Model
- DeviceCategory
- oSVersion
- IsRooted
- DeviceOwnership
- EnrollmentProfileName

For more information on filters, see [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md).

Applies to:

- Android

#### On-demand remediation for a Windows device<!-- 14783338 -->  
A new device action that is in public preview allows you to run a remediation on-demand on a single Windows device. The **Run remediation** device action allows you to resolve issues without having to wait for a remediation to run on its assigned schedule. You'll also be able to view the status of remediations under **Remediations** in the **Monitor** section of a device.

The **Run remediation** device action is rolling-out and can take a few weeks to reach all customers.

For more information, see [Remediations](remediations.md).

### Device management

#### Windows Driver update management in Intune is generally available<!-- 5584639  -->  
Announcing the general availability of **Windows Driver update management** in Microsoft Intune. With driver update policies, you can view a list of driver updates that are recommended and applicable to your Windows 10 and Windows 11 device that are assigned to the policy. Applicable driver updates are those that can update a device's driver version. Driver update policies update automatically to add new updates as they're published by the driver manufacturer and remove older drivers that no longer apply to any device with the policy.

Update policies can be configured for one of two approval methods:

- With *Automatic approval*, each new *recommended* driver that's published by the driver manufacturer and added to the policy is automatically approved for deployment to applicable devices. Policies set for automatic approvals can be configured with a deferral period before the automatically approved updates are installed on devices. This deferral gives you time to review the driver and to pause its deployment if necessary.

- With *manual approval*, all new driver updates are automatically added to the policy, but an admin must explicitly approve each update before Windows Update deploys it to a device. When you manually approve an update, you choose the date when Windows Update will begin to deploy it to your devices.

To help you manage driver updates, you review a policy and decline an update you don't want to install. You can also indefinitely pause any approved update, and reapprove a paused update to restart its deployment.

This release also includes [driver update reports](../protect/windows-update-reports.md#reports-for-windows-driver-updates-policy) that provide a success summary, per-device update status for each approved driver, and error and troubleshooting information. You can also select an individual driver update and view details about it across all the policies that include that driver version.

To learn about using Windows Driver update policies, see [Manage policy for Windows Driver updates with Microsoft Intune](../protect/windows-driver-updates-overview.md).

Applies to:

- Windows 10
- Windows 11

## Week of June 19, 2023 (Service release 2306)

### App management

#### MAM for Microsoft Edge for Business [Preview]<!-- 12394345 -->  
You can now enable protected MAM access to org data via Microsoft Edge on personal Windows devices. This capability uses the following functionality:

- Intune Application Configuration Policies (ACP) to customize the org user experience in Microsoft Edge
- Intune Application Protection Policies (APP) to secure org data and ensure the client device is healthy when using Microsoft Edge
- Windows Defender client threat defense integrated with Intune APP to detect local health threats on personal Windows devices
- Application Protection Conditional Access to ensure the device is protected and healthy before granting protected service access via Microsoft Entra ID

For more information, see [Preview: App protection policy settings for Windows](../apps/app-protection-policy-settings-windows.md).

To participate in the public preview, [complete the opt-in form](https://aka.ms/MAMforWindowsPublic).

### Device configuration

#### New settings available in the Apple settings catalog<!-- 19951554  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Networking > Network Usage Rules**:

- SIM Rules

##### macOS

**Authentication > Extensible Single Sign On (SSO)**:

- Authentication Method
- Denied Bundle Identifiers
- Registration Token

**Full Disk Encryption > FileVault**:

- Output path
- Username
- Password
- UseKeyChain

#### Device Firmware Configuration Interface (DFCI) supports Asus devices <!-- 10249874 -->  
For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type.

Some Asus devices running Windows 10/11 are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, see:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](/autopilot/dfci-management)

Applies to:

- Windows 10
- Windows 11

#### Saaswedo Datalert telecom expense management is removed in Intune <!-- 23616707  -->  
In Intune, you could manage telecom expenses using Saaswedo's Datalert telecom expense management. This feature is removed from Intune. This removal includes:

- The **Telecom Expense Management** connector

- **Telecom expenses** RBAC category
  - **Read** permission
  - **Update** permission

For more information from Saaswedo, see [The datalert service is unavailable](https://www.saaswedo.com/datalert-service-unavailable) (opens Saaswedo's web site).

Applies to:

- Android
- iOS/iPadOS

#### Settings insight within Intune security baseline<!-- 11127203  -->  
The [Settings insight](settings-insight.md) feature adds insights to security baselines giving you confidence in configurations that are successfully adopted by similar organizations.

Navigate to **Endpoint security** > **Security baselines**. When you create and edit the workflow, these insights are available for you in the form of a light bulb.

### Device management

#### New endpoint security Application Control policy in preview<!-- 15711976 -->  
As a public preview, you can use a new endpoint security policy category, Application Control. Endpoint security Application Control policy includes:

- Policy to set the Intune Management Extension as a tenant-wide managed installer. When enabled as a managed installer, apps you deploy through Intune (after enablement of Managed Installer) to Windows devices are tagged as installed by Intune. This tag becomes useful when you use Application Control policies to manage which apps you want to allow or block from running on your managed devices.

- Application Control policies that are an implementation of Defender Application Control (WDAC). With Endpoint security Application Control policies, it's easy to configure policy that allows trusted apps to run on your managed devices. Trusted apps are installed by a managed installer or from the App store. In addition to built-in trust settings, these policies also support custom XML for application control so you can allow other apps from other sources to run to meet your organizations requirements.

To get started with using this new policy type, see [Manage approved apps for Windows devices with Application Control policy and Managed Installers for Microsoft Intune](../protect/endpoint-security-app-control-policy.md)

Applies to:

- Windows 10
- Windows 11

#### Endpoint analytics is available to tenants in Government cloud<!-- 8527244  -->  
With this release, Endpoint analytics is available to tenants in Government cloud.

Learn more about [Endpoint analytics](../../analytics/overview.md).

#### Introducing in-session connection mode switch in Remote Help<!-- 10602971  -->  
In Remote Help, you can now take advantage of the in-session connection mode switch feature. This feature can help effortlessly transition between full control and view-only modes, granting flexibility and convenience.

For more information on Remote Help, see [Remote Help](remote-help.md).

Applies to:

- Windows 10/11

### Device security

#### Update to Endpoint Privilege Management reports<!-- 17727222 -->  
Intune's Endpoint Privilege Management (EPM) reports now support exporting the full reporting payload to a CSV file. With this change, you can now export all events from an elevation report in Intune.

#### Endpoint Privilege Managements run with elevated access option now available on the top-level menu for Windows 11<!-- 17749664  -->  
The Endpoint Privilege Management option to *Run with elevated access* is now available as a top-level right-click option on Windows 11 devices. Previous to this change, standard users were required to select *Show more options* to view the *Run with elevated access* prompt on Windows 11 devices.

[Endpoint Privilege Management](../protect/epm-overview.md) is available as an Intune add-on. For more information, see [Use Intune Suite add-on capabilities](intune-add-ons.md).

Applies to:

- Windows 11

### Intune apps

#### Newly available protected apps for Intune<!-- 23027634, 21159364, 21234187, 21237641, 20771088  -->  
The following protected apps are now available for Microsoft Intune:

- Idenprotect Go by Apply Mobile Ltd (Android)
- LiquidText by LiquidText, Inc. (iOS)
- MyQ Roger: OCR scanner PDF by MyQ spol. s r.o.
- CiiMS GO by Online Intelligence (Pty) Ltd
- Vbrick Mobile by Vbrick Systems

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Microsoft Intune troubleshooting pane is now generally available<!-- 18099474 -->  
The Intune troubleshooting pane is now generally available.  It provides details about user's devices, policies, applications, and status. The troubleshooting pane includes the following information:

- A summary of policy, compliance, and application deployment status.
- Support for exporting, filtering, and sorting all reports.
- Support to filter by excluding policies and applications.
- Support to filter to a user's single device.
- Details about available device diagnostics and disabled devices.
- Details about offline devices that haven't checked-in to the service for three or more days.

You can find the troubleshooting pane in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot**.

#### Updated troubleshoot + support pane in Intune<!-- 16240430  -->  
The **Troubleshooting + support** pane in the Intune admin center has been updated by consolidating the **Roles and Scopes** report into a single report. This report now includes all relevant role and scope data from both Intune and Microsoft Entra ID, providing a more streamlined and efficient experience. For related information, see [Use the troubleshooting dashboard to help users at your company](help-desk-operators.md).

#### Download mobile app diagnostics<!-- 22139638  -->  
Now generally available, access user-submitted mobile app diagnostics in the Intune admin center, including app logs sent through Company Portal apps, which include Windows, iOS, Android, Android AOSP, and macOS. In addition, you can retrieve app protection logs via Microsoft Edge. For more information, see [Company Portal app logs](../apps/company-portal-app.md#app-logs) and [Use Microsoft Edge for iOS and Android to access managed app logs](../apps/manage-microsoft-edge.md#use-microsoft-edge-for-ios-and-android-to-access-managed-app-logs).

## Week of June 12, 2023

### Device management

#### New Devices from HTC and Pico supported on Microsoft Intune for Android Open Source Devices<!-- 24271568 -->  
Microsoft Intune for Android open source project devices (AOSP) now supports the following devices:

- HTC Vive XR Elite
- Pico Neo 3 Pro
- Pico 4

For more information, see:

- [Operating systems and browsers supported by Microsoft Intune](supported-devices-browsers.md)

- [Android Open Source Project Supported Devices](android-os-project-supported-devices.md)

Applies to:

- Android (AOSP)

### App management

#### Microsoft Store for Business or Microsoft Store for Education<!-- 24250535 -->  
Apps added from the Microsoft Store for Business or Microsoft Store for Education won't deploy to devices and users. Apps show as "not applicable" in reporting. Apps already deployed are unaffected. Use the [new Microsoft Store app](../apps/store-apps-microsoft.md) to deploy Microsoft Store apps to devices or users. For related information, see [Adding your Microsoft Store for Business and Education apps to the Microsoft Store in Intune](https://aka.ms/Intune/MSfB-support) for upcoming dates when Microsoft Store for Business apps will no longer deploy and Microsoft Store for Business apps will be removed.

For more information, see the following resources:

- [Update to Intune integration with the Microsoft Store on Windows](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/update-to-intune-integration-with-the-microsoft-store-on-windows/ba-p/3585077)
- [Embracing the Future of Microsoft Store with Intune: A Step-by-Step Guide](https://www.youtube.com/watch?v=c534X9yMvDo)
- [Embracing the Future of Microsoft Store with Intune for Education: A Step-by-Step Guide](https://www.youtube.com/watch?v=Heoi0RuClQM)

## Week of June 5, 2023

### Device configuration

### Android Enterprise 11+ devices can use Zebra's latest OEMConfig app version<!-- 8675347 -->  

On Android Enterprise devices, you can use OEMConfig to add, create, and customize OEM-specific settings in Microsoft Intune (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **OEMConfig**).

There's a new **Zebra OEMConfig Powered by MX** OEMConfig app that aligns more closely to Google's standards. This app supports Android Enterprise 11.0 and newer devices.

The older **Legacy Zebra OEMConfig** app continues to support devices with Android 11 and earlier.

In your Managed Google Play, there are two versions of Zebra OEMConfig app. Be sure to select the correct app that applies to your Android device versions.

For more information on OEMConfig and Intune, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:

- Android Enterprise 11.0 and newer

## Week of May 29, 2023

### Device management

#### Intune UI displays Windows Server devices as distinct from Windows clients for the Security Management for Microsoft Defender for Endpoint scenario<!-- 16882836 -->  
To support the [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md) (MDE security configuration) scenario, Intune now differentiates Windows devices in Microsoft Entra ID as either *Windows Server* for devices that run Windows Server, or as *Windows* for devices that run Windows 10 or Windows 11.

With this change, you can improve policy targeting for MDE security configuration. For example, you can use dynamic groups that consist of only Windows Server devices, or only Windows client devices (Windows 10/11).

For more information about this change, see the Intune Customer Success blog [Windows Server devices now recognized as a new OS in Microsoft Intune, Microsoft Entra ID, and Defender for Endpoint
](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-windows-server-devices-will-now-be-identified-as-a/ba-p/3767773).

### Tenant administration

#### Organizational messages for Windows 11 now generally available<!-- 15272978 -->  
Use organizational messages to deliver branded, personalized call-to-actions to employees. Select from more than 25 messages that support employees through device onboarding and lifecycle management, in 15 different languages. Messages can be assigned to Microsoft Entra user groups. They're shown just above the taskbar, in the notifications area, or in the Get started app on devices running Windows 11. Messages continue to appear or reappear based on the frequency you configure in Intune, and until the user has visited the customized URL.

Other features and functionality added in this release include:

- Confirm licensing requirements prior to first message.
- Choose from eight new themes for taskbar messages.
- Give messages a custom name.
- Add scope groups and scope tags.
- Edit the details of a scheduled message.

Scope tags were previously unavailable for organizational messages. With the addition of scope tag support, Intune adds the default scope tag to every message created before June 2023. Admins that want access to those messages must be associated with a role that has the same tag. For more information about available features and how to set up organizational messages, see
[Overview of organizational messages](/microsoft-365/admin/misc/organizational-messages-microsoft-365).

## Week of May 22, 2023 (Service release 2305)

### App management

#### Update to macOS shell scripts maximum running time limit<!-- 23187517 -->
Based on customer feedback, we're updating the Intune agent for macOS (version 2305.019) to extend the maximum script run time to 60 minutes. Previously, the Intune agent for macOS only allowed shell scripts to run for up to 15 minutes before reporting the script as a failure. The Intune agent for macOS 2206.014 and higher supports the 60-minute timeout.

#### Assignment filters support app protection policies and app configuration policies<!-- 7476247 -->  
Assignment filters support MAM app protection policies and app configuration policies. When you create a new filter, you can fine tune MAM policy targeting using the following properties:

- Device Management Type
- Device Manufacturer
- Device Model
- OS Version
- Application Version
- MAM Client Version

> [!IMPORTANT]
> All new and edited app protection policies that use **Device Type** targeting are replaced with assignment filters.

For more information on filters, see [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md).

#### Update to MAM reporting in Intune<!-- 10100428  -->  
MAM reporting has been simplified and overhauled, and now uses Intune's newest reporting infrastructure. Benefits of this include improved data accuracy and instantaneous updating. You can find these streamlined MAM reports in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Monitor**. All MAM data available to you is contained within the new **App protection status** report and **App configuration status** report.

#### Global quiet time app policy settings<!-- 15424417   -->  
The global quiet time settings allow you to create policies to schedule quiet time for your end users. These settings automatically mute Microsoft Outlook email and Teams notifications on iOS/iPadOS and Android platforms. These policies can be used to limit end user notifications received after work hours. For more information, see [Quiet time notification policies](../apps/app-office-policies.md#quiet-time-notification-policies).

### Device configuration

#### Introducing enhanced chat in Remote Help<!-- 10602997 -->  
Introducing enhanced chat with Remote Help. With the new and enhanced chat you can maintain a continuous thread of all messages. This chat provides support for special characters and other languages including Chinese and Arabic.

For more information on Remote Help, see [Remote Help](remote-help.md).

Applies to:

- Windows 10/11

#### Remote Help administrators can reference audit log sessions<!-- 9052185  -->  
For Remote Help, in addition to existing session reports, administrators can now reference audit logs sessions created in Intune. This feature enables administrators to reference past events for troubleshooting and analyzing log activities.

For more information on Remote Help, see [Remote Help](remote-help.md).

Applies to:

- Windows 10
- Windows 11

#### Turn on/off Personal data encryption on Windows 11 devices using the settings catalog<!-- 10346018  -->  
The settings catalog includes hundreds of settings that you can configure and deploy to your devices.

In the settings catalog, you can turn on/off **Personal data encryption** (PDE). PDE is a security feature introduced in Windows 11 version 22H2 that provides more encryption features for Windows.

PDE is different than BitLocker. PDE encrypts individual files and content, instead of whole volumes and disks. You can use PDE with other encryption methods, such as BitLocker.

For more information on the settings catalog, see:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md)
- [Common Tasks you can complete using the Settings Catalog in Intune](../configuration/settings-catalog-common-features.md)

This feature applies to:

- Windows 11

#### Visual Studio ADMX settings are in the Settings Catalog and Administrative Templates <!-- 10875730 -->  
Visual Studio settings are included in the Settings Catalog and Administrative Templates (ADMX). Previously, to configure Visual Studio settings on Windows devices, you imported them with ADMX import.

For more information on these policy types, see:

- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Use Windows 10/11 templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md)
- [Visual Studio Administrative Templates (ADMX)](/visualstudio/install/administrative-templates)

Applies to:

- Windows 10
- Windows 11

#### Group policy analytics supports scope tags<!-- 12714882  -->  
In Group Policy analytics, you import your on-premises GPO. The tool analyzes your GPOs and shows the settings that can (and can't) be used in Intune.

When you import your GPO XML file in Intune, you can select an existing scope tag. If you don't select a scope tag, then the **Default** scope tag is automatically selected. Previously, when you imported a GPO, the scope tags assigned to you were automatically applied to the GPO.

Only admins within that scope tag can see the imported policies. Admins not in that scope tag can't see the imported policies.

Also, admins within their scope tag can migrate the imported policies that they have permissions to see. To migrate an imported GPO into a Settings Catalog policy, a scope tag must be associated with the imported GPO. If a scope tag isn't associated, then it can't migrate to a Settings Catalog policy. If no scope tag is selected, then a default scope tag is automatically applied.

For more information on scope tags and Group Policy analytics, see:

- [Analyze your on-premises GPOs using Group Policy analytics in Microsoft Intune](../configuration/group-policy-analytics.md)
- [Create a Settings Catalog policy using your imported GPOs](../configuration/group-policy-analytics-migrate.md)
- [Use role-based access control (RBAC) and scope tags for distributed IT](scope-tags.md)

#### Introducing Intune integration with the Zebra Lifeguard Over-the-Air service (public preview)<!-- 14340034  -->  
Now available in public preview, Microsoft Intune supports integration with Zebra Lifeguard Over-the-Air service, which allows you to deliver OS updates and security patches over-the-air to eligible Zebra devices that are enrolled with Intune. You can select the firmware version you want to deploy, set a schedule, and stagger update downloads and installs. You can also set minimum battery, charging status, and network conditions requirements for when the update can happen.

Available for Android Enterprise Dedicated and Fully Managed Zebra devices that are running Android 8 or later, and requires an account with Zebra.

#### New Google domain allowlist settings for Android Enterprise personally owned devices with a work profile<!-- 14711684 -->  
On Android Enterprise personally owned devices with a work profile, you can configure settings that restrict device features and settings.

Currently, there's an **Add and remove accounts** setting that can allow Google accounts be added to the work profile. For this setting, when you select **Allow all accounts types**, you can also configure:

- **Google domain allow-list**:  Restricts users to add only certain Google account domains in the work profile. You can import a list of allowed domains or add them in the admin center using the `contoso.com` format. When left blank, by default, the OS might allow adding all Google domains in the work profile.

For more information on the settings you can configure, see [Android Enterprise device settings list to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-enterprise-personal.md).

Applies to:

- Android Enterprise personally owned devices with a work profile

#### Renaming Proactive remediation to Remediations and moving to a new location<!-- 16526263  -->  
Proactive remediations are now Remediations and are available from **Devices** > **Remediations**. You can still find Remediations in both the new location and the existing **Reports** > **Endpoint Analytics** location until the next Intune service update.

Remediations are currently not available in the new [Devices experience preview](public-preview.md).

Applies to:

- Windows 10
- Windows 11

#### Remediations are now available in Intune for US Government GCC High and DoD<!-- 16526300 -->  
Remediations (previously known as proactive remediations) are now available in [Microsoft Intune for US Government GCC High and DoD](intune-govt-service-description.md).

Applies to:

- Windows 10
- Windows 11

#### Create inbound and outbound network traffic rules for VPN profiles on Windows devices<!-- 17943658 -->  
> [!NOTE]
> This setting is coming in a future release, possibly the 2308 Intune release.

You can create a device configuration profile that deploys a VPN connection to devices (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **VPN** for profile type).

In this VPN connection, you can use the **Apps and Traffic rules** settings to create network traffic rules.

There's a new **Direction** setting you can configure. Use this setting to allow Inbound and Outbound traffic from the VPN connection:

- **Outbound** (default): Allows only traffic to external networks/destinations to flow using the VPN. Inbound traffic is blocked from entering the VPN.
- **Inbound**: Allows only traffic coming from external networks/ sources to flow using the VPN. Outbound traffic is blocked from entering the VPN.

For more information on the VPN settings you can configure, including the network traffic rule settings, see [Windows device settings to add VPN connections using Intune](../configuration/vpn-settings-windows-10.md).

Applies to:

- Windows 10 and later

#### New settings available in the macOS settings catalog <!-- 18430228  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

**Microsoft Defender > Antivirus engine**:

- Scanning inside archive files
- Enable file hash computation

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Wipe device action and new obliteration behavior setting available for macOS<!-- 16647226 -->  
You can now use the **Wipe** device action instead of Erase for macOS devices. You can also configure the **Obliteration Behavior** setting as part of the **Wipe** action.

This new key allows you to control the wipe fallback behavior on Macs that have Apple Silicon or the T2 Security Chip. To find this setting, navigate to **Devices** > **By platform** > **macOS** > [Select a device] > **Overview** > **Wipe** in the **Device action** area.

For more information on the Obliteration Behavior setting, go to Apple's Platform Deployment site [Erase Apple devices - Apple Support](https://support.apple.com/guide/deployment/erase-devices-dep0a819891e/web).

Applies to:

- macOS

### Device enrollment

#### Account driven Apple User Enrollment available for iOS/iPadOS 15+ devices (public preview)<!-- 14161683  -->  
Intune supports account driven user enrollment, a new and improved variation of Apple User Enrollment for iOS/iPadOS 15+ devices. Now available for public preview, the new option utilizes just-in-time registration, which eliminates the need for the Company Portal app during enrollment. Device users can initiate enrollment directly in the Settings app, resulting in a shorter and more efficient onboarding experience. You can continue to target iOS/iPadOS devices using the existing profile-based user enrollment method that uses Company Portal. Devices running iOS/iPadOS, version 14.8.1 and earlier remain unaffected by this update and can continue to use the existing method. For more information, see [Set up account driven Apple User Enrollment](../enrollment/apple-account-driven-user-enrollment.md).  

### Device security

#### New security baseline for Microsoft 365 Office Apps<!-- 9587103  -->  
We've released a new security baseline to help you manage security configurations for **M365 Office Apps**. This new baseline uses an updated template and experience that uses the unified settings platform seen in the Intune settings catalog. You can view the list of settings in the new baseline at [Microsoft 365 Apps for Enterprise baseline settings (Office)](../protect/security-baseline-v2-office-settings.md).

The new Intune security baseline format aligns the presentation of settings that are available to the settings found in the Intune settings catalog. This alignment helps resolve past issues for setting names and implementations for settings that could create conflicts. The new format also improves the reporting experience for baselines in the Intune admin center.

The Microsoft 365 Office Apps baseline can help you rapidly deploy configurations to your Office Apps that meet the security recommendations of the Office and security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations. You can modify the default baseline to meet the requirements of your organization.

To learn more, see [Security baselines overview](../protect/security-baselines.md).

Applies to:

- Windows 10
- Windows 11

#### Security baseline update for Microsoft Edge version 112<!-- 3408610  -->  
We've released a new version of the Intune security baseline for Microsoft Edge, version 112. In addition to releasing this new version for Microsoft Edge, the new baseline uses an updated template experience that uses the unified settings platform seen in the Intune settings catalog. You can view the list of settings in the new baseline at [Microsoft Edge baseline settings (version 112 and higher)](../protect/security-baseline-v2-edge-settings.md).

The new Intune security baseline format aligns the presentation of settings that are available to the settings found in the Intune settings catalog. This alignment helps resolve past issues for setting names and implementations for settings that could create conflicts. The new format also improves the reporting experience for baselines in the Intune admin center.

Now that the new baseline version is available, all new profiles you create for Microsoft Edge use the new baseline format and version. While the new version becomes the default baseline version, you can continue to use the profiles you've previously created for older versions of Microsoft Edge. But, you can't create new profiles for those older versions of Microsoft Edge.

To learn more, see [Security baselines overview](../protect/security-baselines.md).

Applies to:

- Windows 10
- Windows 11

### Intune apps

#### Newly available protected apps for Intune<!-- 17782795, 17782816, 17851777, 17644967, 17948005, 17971727 -->  
The following protected apps are now available for Microsoft Intune:

- Achievers by Achievers Inc.
- Board.Vision for iPad by Trusted Services PTE. LTD.
- Global Relay by Global Relay Communications Inc.
- Incorta (BestBuy) by Incorta, Inc. (iOS)
- Island Enterprise Browser by Island (iOS)
- Klaxoon for Intune by Klaxoon (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of May 8, 2023

### Device configuration

#### Device Firmware Configuration Interface (DFCI) supports Dynabook devices<!-- 10249859 -->  
For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type.

Some Dynabook devices running Windows 10/11 are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, see:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](/autopilot/dfci-management)

Applies to:

- Windows 10
- Windows 11

#### eSIM bulk activation for Windows PCs via download server is now available on the Settings Catalog<!-- 19809114 -->  
You can now perform at-scale configuration of Windows eSIM PCs using the Settings Catalog. A download server (SM-DP+) is configured using a configuration profile.

Once the devices receive the configuration, they automatically download the eSIM profile. For more information, see [eSIM configuration of a download server](../configuration/esim-device-configuration-download-server.md).

Applies to:

- Windows 11
- eSIM capable devices

## Week of May 1, 2023

### App management

#### macOS shell scripts maximum running time limit<!-- 19396575 -->  
We have fixed an issue that caused Intune tenants with long-running shell scripts to not report back on the script run status. The macOS Intune agent stops any macOS shell scripts that run longer than 15 minutes. These scripts report as failed. The new behavior is enforced from macOS Intune agent version 2305.019.

#### DMG app installation for macOS<!-- 13911806 -->  
The DMG app installation feature for macOS is now generally available. Intune supports **required** and **uninstall** assignment types for DMG apps. The Intune agent for macOS is used to deploy DMG apps.

#### Deprecation of Microsoft Store for Business and Education<!-- 19677954 -->  
The Microsoft Store for Business connector is no longer available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Apps added from the Microsoft Store for Business or Microsoft Store for Education won't sync with Intune. Apps that have previously synced continue to be available and deploy to devices and users.

It's now also possible to delete Microsoft Store for Business apps from the **Apps** pane in the Microsoft Intune admin center so that you can clean up your environment as you move to the new Microsoft Store app type.

For related information, see [Adding your Microsoft Store for Business and Education apps to the Microsoft Store in Intune](https://aka.ms/Intune/MSfB-support) for upcoming dates when Microsoft Store for Business apps won't deploy and Microsoft Store for Business apps are removed.

### Device configuration

#### Remote Help now supports Conditional Access capability<!--16108299 -->  
Administrators can now utilize Conditional Access capability when setting up policies and conditions for Remote Help. For example, multifactor authentication, installing security updates, and locking access to Remote Help for a specific region or IP addresses.

For more information, see:

- [Conditional Access](../protect/conditional-access.md)
- [Remote Help](remote-help-windows.md#setup-conditional-access-for-remote-help)

### Device security

#### Updated settings for Microsoft Defender in endpoint security Antivirus policy<!-- 19991301  -->  
We've updated the available settings in the *Microsoft Defender Antivirus* profile for endpoint security Antivirus policy.  You can find this profile in the Intune admin center at **Endpoint security** > **Antivirus** > *Platform:* **Windows 10, Windows 11, and Windows Server**  > *Profile:* **Microsoft Defender Antivirus**.

- **The following settings have been added**:

  - Metered Connection Updates
  - Disable Tls Parsing
  - Disable Http Parsing
  - Disable Dns Parsing
  - Disable Dns Over Tcp Parsing
  - Disable Ssh Parsing
  - Platform Updates Channel
  - Engine Updates Channel
  - Security Intelligence Updates Channel
  - Allow Network Protection Down Level
  - Allow Datagram Processing On Win Server
  - Enable Dns Sinkhole

  For more information about these settings, see the [Defender CSP]( /windows/client-management/mdm/Defender-csp?WT.mc_id=Portal-fx).
The new settings are also available through the Intune [Settings Catalog](../configuration/settings-catalog.md).

- **The following setting has been deprecated**:

  - Allow Intrusion Prevention System

  This setting now appears with the *Deprecated* tag. If this deprecated setting was previously applied on a device, the setting value is updated to *NotApplicable* and has no effect on the device. If this setting is configured on a device, there's no effect on the device.

Applies to:

- Windows 10
- Windows 11

## Week of April 17, 2023 (Service release 2304)

### App management

#### Changes to iCloud app backup and restore behavior on iOS/iPadOS and macOS devices<!-- 16261392  -->  
As an app setting, you can select to **Prevent iCloud app backup** for iOS/iPadOS and macOS devices. You can *not* backup managed App Store apps and line-of-business (LOB) apps on iOS/iPadOS, as well as managed App Store apps on macOS devices (macOS LOB apps don't support this feature), for both user and device licensed VPP/non-VPP apps. This update includes both new and existing App Store/LOB apps sent with and without VPP that are being added to Intune and targeted to users and devices.

Preventing the backup of the specified managed apps ensures that these apps can be properly deployed via Intune when the device is enrolled and restored from backup. If the admin configures this new setting for new or existing apps in their tenant, then managed apps can and will be reinstalled for devices. But, Intune doesn't allow them to be backed up.

This new setting appears in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by modifying the properties of an app. For an existing app, you can select **Apps** > **iOS/iPadOS** or **macOS** > *select the app* > **Properties** > Assignment **Edit**. If no group assignment has been set, select **Add group** to add a group. Modify either the setting under **VPN**, **Uninstall on device removal**, or **Install as removable**. Then, select **Prevent iCloud app backup**. The **Prevent iCloud app backup** setting is used to prevent backup of app data for the application. Set to **No** to allow the app to be backed up by iCloud.

For more information, see [Changes to applications' backup and restore behavior on iOS/iPadOS and macOS devices](https://techcommunity.microsoft.com/t5/intune-customer-success/changes-to-applications-backup-and-restore-behavior-on-ios/ba-p/3692064) and [Assign apps to groups with Microsoft Intune](../apps/apps-deploy.md).

#### Prevent automatic updates for Apple VPP apps<!-- 16876430   -->  
You can control the automatic update behavior for Apple VPP at the per-app assignment level using the **Prevent automatic updates** setting. This setting is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** or **macOS** > *Select a volume purchase program app* > **Properties** > **Assignments** > *Select a Microsoft Entra group* > **App settings**.

Applies to:

- iOS/iPadOS
- macOS

### Device configuration

#### Updates to the macOS Settings Catalog <!-- 17673709  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

The new setting is located under:

**Microsoft AutoUpdate (MAU) > [targeted app]**:

- Update channel override

The following settings have been deprecated:

**Microsoft AutoUpdate (MAU) > [targeted app]**:

- Channel Name (Deprecated)

**Privacy > Privacy Preferences Policy Control > Services > Listen Event or Screen Capture**:

- Allowed

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### The Microsoft Enterprise SSO plug-in for Apple devices is now generally available<!-- 17826329  -->  
In Microsoft Intune, there's a Microsoft Enterprise SSO plug-in. This plug-in provides single sign-on (SSO) to iOS/iPadOS and macOS apps and websites that use Microsoft Entra ID for authentication.

This plug-in is now generally available (GA).

For more information about configuring the Microsoft Enterprise SSO plug-in for Apple devices in Intune, go to [Microsoft Enterprise SSO plug-in in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md).

Applies to:

- iOS/iPadOS
- macOS

#### Disable Activation Lock device action for supervised macOS devices<!-- 16813146  -->  
You can now use the **Disable Activation Lock** device action in Intune to bypass Activation Lock on Mac devices without requiring the current username or password. This new action is available in **Devices** > **By platform** > **macOS** > select one of your listed devices > **Disable Activation Lock**.

More information on managing Activation Lock is available at [Bypass iOS/iPadOS Activation Lock with Intune](../remote-actions/device-activation-lock-disable.md) or on Apple's website at [Activation Lock for iPhone, iPad, and iPod touch - Apple Support](https://support.apple.com/en-us/HT201365).

Applies to:

- macOS 10.15 or later

#### ServiceNow Integration is now Generally Available (GA)<!-- 18163832  -->  
Now generally available, you can view a list of ServiceNow incidents associated with the user you've selected in the Intune Troubleshooting workspace. This new feature is available under **Troubleshooting + Support** > select a user > **ServiceNow Incidents**. The incidents shown have a direct link back to the source incident and show key information from the incident. All incidents listed link the "Caller" identified in the incident with the user selected for Troubleshooting.

For more information, go to [Use the troubleshooting portal to help users at your company](service-now-integration.md).

#### More permissions to support administrators in controlling delivery of organization messages<!-- 16982298  -->  
With more permissions administrators can control delivery of content created and deployed from Organizational messages and the delivery of content from Microsoft to users.

The **Update organizational message control** RBAC permission for organizational messages determines who can change the Organizational Messages toggle to allow or block Microsoft direct messages. This permission is also added to the **Organizational Messages Manager** built-in role.

Existing custom roles for managing Organizational Messages must be modified to add this permission for users to modify this setting.

- For more information, about role-based access control (RBAC), see [RBAC with Microsoft Intune](role-based-access-control.md).
- For more information, about prerequisites for organization messages, see [Organizational messages prerequisites](/microsoft-365/admin/misc/organizational-messages-microsoft-365#role-based-access-control-requirements).

### Device management

#### Endpoint security firewall rules support for ICMP type<!-- 5653356  -->  
You can now use the **IcmpTypesAndCodes** setting to configure inbound and outbound rules for [Internet Control Message Protocol](/windows/security/threat-protection/windows-firewall/create-an-inbound-icmp-rule) (ICMP) as part of a firewall rule. This setting is available in the [*Microsoft Defender Firewall rules*](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune) profile for the *Windows 10, Windows 11, and Windows Server* platform.

Applies to:

- Windows 11 and later

#### Manage Windows LAPS with Intune policies (public preview)<!-- 11890571  -->  
Now available in a public preview, manage Windows Local Administrator Password Solution (Windows LAPS) with Microsoft Intune [Account protection policies](../protect/endpoint-security-account-protection-policy.md). To get started, see [Intune support for Windows LAPS](../protect/windows-laps-overview.md).

[Windows LAPS](/windows-server/identity/laps/laps-overview) is a Windows feature that allows you to manage and backs up the password of a local administrator account on your Microsoft Entra joined or Windows Server Active Directory-joined devices.

To manage LAPS, Intune configures the Windows [LAPS configuration service provider](/windows/client-management/mdm/LAPS-csp) (CSP) that is built in to Windows devices. It takes precedence over other sources of Windows LAPS configurations, like GPOs or the Microsoft Legacy LAPS tool. Some of the capabilities you can use when Intune manages Windows LAPS include:

- Define password requirements like complexity and length that apply to the local administrator accounts on a device.
- Configure devices to rotate their local admin account passwords on a schedule. And, back up the account and password in your Microsoft Entra ID or on-premises Active Directory.
- Use an Intune device action from the admin center to manually rotate the password for an account on your own schedule.
- View account details from within the Intune admin center, like the account name and password. This information can help you recover devices that are otherwise inaccessible.
- Use Intune reports to monitor your LAPS policies, and when devices last rotated passwords manually or by schedule.  

Applies to:

- Windows 10
- Windows 11

#### New settings available for macOS software update policies<!-- 16646756  -->  
macOS software update policies now include the following settings to help manage when updates install on a device. These settings are available when the *All other updates* update type is configured to *Install later*:

- **Max User Deferrals**:  When the *All other updates* update type is configured to *Install later*, this setting allows you to specify the maximum number of times a user can postpone a minor OS update before it's installed. The system prompts the user once a day. Available for devices running macOS 12 and later.

- **Priority**: When the *All other updates* update type is configured to *Install later*, this setting allows you to specify values of *Low* or *High* for the scheduling priority for downloading and preparing minor OS updates. Available for devices running macOS 12.3 and later.

For more information, see [Use Microsoft Intune policies to manage macOS software updates](../protect/software-updates-macos.md).

Applies to:

- macOS

#### Introducing the new partner portals page<!-- 17829024  -->  
You can now manage hardware specific information on your HP or Surface devices from our partner portals page.

The HP link takes you to HP Connect where you can update, configure, and secure the BIOS on your HP devices.
The Microsoft Surface link takes you to the Surface Management Portal where you can get insights into device compliance, support activity, and warranty coverage.

To access the Partner portals page, you must enable the Devices pane preview and then navigate to **Devices** > **Partner Portals**.

#### Windows Update compatibility reports for Apps and Drivers are now generally available<!-- 17917026  -->  
The following Microsoft Intune reports for [Windows Update compatibility](../protect/windows-update-compatibility-reports.md) are out of preview and now generally available:

- **Windows feature update device readiness report** - This report provides per-device information about compatibility risks that are associated with an upgrade or update to a chosen version of Windows.

- **Windows feature update compatibility risks report** - This report provides a summary view of the top compatibility risks across your organization for a chosen version of Windows. You can use this report to understand which compatibility risks impact the greatest number of devices in your organization.

These reports can help you plan an upgrade from Windows 10 to 11, or for installing the latest Windows feature update.

### Device security

#### Microsoft Intune Endpoint Privilege Management is generally available<!--1564177  -->  
Microsoft Endpoint Privilege Management (EPM) is now generally available and no longer in preview.

With [Endpoint Privilege Management](../protect/epm-overview.md), admins can set policies that allow standard users to perform tasks normally reserved for an administrator. To do so, you configure policies for *automatic* and *user-confirmed* workflows that elevate the run-time permissions for apps or processes you select. You then assign these policies to users or devices that have end users running without Administrator privileges. After the device receives a policy, EPM brokers the elevation on behalf of the user, allowing them to elevate approved applications without needing full administrator privileges. EPM also includes built-in insights and reporting.

Now that EPM is out of preview, it requires another license to use. You can choose between a stand-alone license that adds only EPM, or license EPM as part of the Microsoft Intune Suite. For more information, see [Use Intune Suite add-on capabilities](intune-add-ons.md).

While Endpoint Privilege Management is now generally available, the [reports for EPM](../protect/epm-reports.md) will transition to a feature in *preview*, and will receive some more enhancements before being removed from preview.

#### Support for WDAC Application ID tagging with Intune Firewall Rules policy<!-- 17224780  -->  
Intune's *Microsoft Defender Firewall Rules* profiles, which are available as part of [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md), now include the Policy App ID setting. This setting is described in the [*MdmStore/FirewallRules/{FirewallRuleName}/PolicyAppId*](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx#mdmstorefirewallrulesfirewallrulenamepolicyappid) CSP and supports specifying a Windows Defender Application Control (WDAC) Application ID tag.

With this capability, you can scope your firewall rules to an application or a group of applications and rely on your WDAC policies to define those applications. By using tags to link to and rely on WDAC policies, your Firewall Rules policy won't need to rely on the firewall rules option of an absolute file path, or use of a variable file path that can reduce security of the rule.

Use of this capability requires you to have WDAC policies in place that include *AppId* tags that you can then specify in your Intune Microsoft Defender Firewall Rules.

For more information, see the following articles in the Windows Defender Application Control documentation:

- [About application control for Windows](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)
- [WDAC Application ID (AppId) Tagging guide](/windows/security/threat-protection/windows-defender-application-control/appidtagging/windows-defender-application-control-appid-tagging-guide)

Applies to:

- Windows 10/11

#### New App and browser isolation profile for Intune's endpoint security Attack Surface Reduction policy<!-- 17392386  -->  
We have released a new experience creating new *App and Browser Isolation* profiles for endpoint security Attack Surface Reduction policy. The experience for editing your previously created App and Browser isolation policies remains the same, and you can continue to use them. This update applies only for the new [App and Browser Isolation](../protect/endpoint-security-asr-policy.md#attack-surface-reduction-profiles) policies you create for the *Windows 10 and later* platform.

This update is part of the continuing rollout of new profiles for endpoint security policies, which began in April 2022.

Additionally, the new profile includes the following changes for the settings it includes:

- **Block external content from non-enterprise approved sites** - This setting is removed from the updated profile as it was supported only by Microsoft Edge Legacy. Microsoft Edge Legacy support ended in March 2021. [Microsoft 365 apps say farewell to Internet Explorer 11 and Windows 10 sunsets Microsoft Edge Legacy - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/microsoft-365-blog/microsoft-365-apps-say-farewell-to-internet-explorer-11-and/ba-p/1591666).

- **Clipboard file type** – This setting is added to the updated profile and determines the type of content that can be copied from the host to Application Guard environment and vice versa. You can view the CSP for this new setting at [Settings/ClipboardFileType](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#settingsclipboardfiletype) in the WindowsDefenderApplicationGuard CSP documentation.

### Intune apps

#### Newly available protected apps for Intune<!-- 17318943, 17319737, 17457189, 17624650  -->
The following protected apps are now available for Microsoft Intune:

- ixArma by INAX-APPS (iOS)
- myBLDNG by Bldng.ai (iOS)
- RICOH Spaces V2 by Ricoh Digital Services
- Firstup - Intune by Firstup, Inc. (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Role-based access control

#### New Assign (RBAC) permissions for organizational messages<!-- 16872833  -->  
The **Assign** RBAC permissions for organizational messages determines who can assign target Microsoft Entra groups to an organizational message. To access RBAC permissions, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Roles**.

This permission is also added to the **Organizational Messages Manager** built-in role.  Existing custom roles for managing Organizational Messages must be modified to add this permission for users to modify this setting.

- For more information, about role-based access control (RBAC), see [RBAC with Microsoft Intune](role-based-access-control.md).
- For more information, about prerequisites for organization messages, see [Organizational messages prerequisites](/microsoft-365/admin/misc/organizational-messages-microsoft-365#role-based-access-control-requirements).

### Tenant administration

#### Delete organizational messages<!-- 15273028  -->  
You can now delete organizational messages from Microsoft Intune.  After you delete a message, it's removed from Intune, and no longer appears in the admin center. You can delete a message anytime, regardless of its status. Intune automatically cancels active messages after you delete them. For more information, see [Delete organizational messages](/microsoft-365/admin/misc/organizational-messages-microsoft-365#delete-message).  

#### Review audit logs for organizational messages<!-- 16576073 -->  
Use audit logs to track and monitor organizational message events in Microsoft Intune. To access the logs, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Audit logs**. For more information, see [Audit logs for Intune activities](monitor-audit-logs.md#view-the-audit-logs).  

## Week of April 10, 2023

### Device configuration

#### User configuration support for Windows 10 multi-session VMs is now GA<!-- 17060455 -->  
You can now:

- Configure user scope policies using **Settings catalog** and assign to groups of users.
- Configure user certificates and assign to users.
- Configure PowerShell scripts to install in the user context and assign to users.

Applies to:

- **Windows 10**
- Virtual machines created in [Azure Public and Azure Government clouds](intune-govt-service-description.md)

## Week of April 3, 2023

### Device configuration

#### Add Google accounts to Android Enterprise personally owned devices with a work profile<!-- 9113561 -->  
On Android Enterprise personally owned devices with a work profile, you can configure settings that restrict device features and settings. Currently, there's an **Add and remove accounts** setting. This setting prevents accounts from being added in the work profile, including preventing Google accounts.

This setting changed. You can now add Google accounts. The **Add and remove accounts** setting options are:

- **Block all accounts types**: Prevents users from manually adding or removing accounts in the work profile. For example, when you deploy the Gmail app into the work profile, you can prevent users from adding or removing accounts in this work profile.
- **Allow all accounts types**: Allows all accounts, including Google accounts. These Google accounts are blocked from installing apps from the **Managed Google Play Store**.

  This setting requires:

  - Google Play app version 80970100 or higher

- **Allow all accounts types, except Google accounts** (default): Intune doesn't change or update this setting. By default, the OS might allow adding accounts in the work profile.

For more information on the settings you can configure, go to [Android Enterprise device settings list to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-enterprise-personal.md).

Applies to:

- Android Enterprise personally owned devices with a work profile

## Week of March 27, 2023

### App management

#### Update macOS DMG apps<!-- 13155074 -->
You can now update apps of type **macOS apps (DMG)** deployed using Intune. To edit a DMG app that's already created in Intune, upload the app update with the same bundle identifier as the original DMG app. For related information, see [Add a macOS DMG app to Microsoft Intune](../apps/lob-apps-macos-dmg.md).

#### Install required apps during pre-provisioning<!-- 12716381 -->
A new toggle is available in the Enrollment Status Page (ESP) profile that allows you to select whether you want to attempt to install required applications during the Windows Autopilot pre-provisioning technician phase. We understand that installing as many applications as possible during pre-provisioning is desired to reduce the end user setup time. If there's an app install failure, ESP continues except for the apps specified in the ESP profile. To enable this function, you need to edit your Enrollment Status Page profile by selecting **Yes** on the new setting entitled **Only fail selected apps in technician phase**. This setting only appears if you have blocking apps selected. For information about ESP, go to [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

## Week of March 20, 2023 (Service release 2303)

### App management

### More minimum OS versions for Win32 apps<!-- 16842404  -->  
Intune supports more minimum operating system versions for Windows 10 and 11 when installing Win32 apps. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **Windows** > **Add** > **Windows app (Win32)**. In the **Requirements** tab next to **Minimum operating system**, select one of the available operating systems. Other OS options include:

- Windows 10 21H2
- Windows 10 22H2
- Windows 11 21H2
- Windows 11 22H2

#### Managed apps permission is no longer required to manage VPP apps<!-- 17205644  -->  
You can view and manage VPP apps with only the **Mobile apps** permission assigned. Previously, the **Managed apps** permission was required to view and manage VPP apps. This change doesn't apply to Intune for Education tenants who still need to assign the **Managed apps** permission. More information about permissions in Intune is available at [Custom role permissions](create-custom-role.md#custom-role-permissions).

### Device configuration

#### New settings and setting options available in the macOS Settings Catalog <!-- 16813395  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Microsoft Defender > Tamper protection**:

- Enforcement level

**Microsoft Office > Microsoft OneDrive**:

- Automatic upload bandwidth percentage
- Automatically and silently enable the Folder Backup feature (aka Known Folder Move)
- Block apps from downloading online-only files
- Block external sync
- Disable automatic sign in
- Disable download toasts
- Disable personal accounts
- Disable tutorial
- Display a notification to users once their folders have been redirected
- Enable Files On-Demand
- Enable simultaneous edits for Office apps
- Force users to use the Folder Backup feature (aka Known Folder Move)
- Hide dock icon
- Ignore named files
- Include ~/Desktop in Folder Backup (aka Known Folder Move)
- Include ~/Documents in Folder Backup (aka Known Folder Move)
- Open at login
- Prevent users from using the Folder Backup feature (aka Known Folder Move)
- Prompt users to enable the Folder Backup feature (aka Known Folder Move)
- Set maximum download throughput
- Set maximum upload throughput
- SharePoint Prioritization
- SharePoint Server Front Door URL
- SharePoint Server Tenant Name

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Add custom Bash scripts to configure Linux devices<!-- 12508999  -->  
In Intune, you can add existing Bash scripts to configure Linux devices (**Devices** > **By platform** > **Linux** > **Scripts**).

When you create this script policy, you can set the context that the script runs in (user or root), how frequently the script runs, and how many times execution should retry.

For more information on this feature, go to [Use custom Bash scripts to configure Linux devices in Microsoft Intune](../configuration/custom-settings-linux.md).

Applies to:

- Linux Ubuntu Desktops

### Device enrollment

#### Support for the await final configuration setting for iOS/iPadOS Automated device enrollment (public preview)<!-- 13156553  -->  
Now in public preview, Intune supports a new setting called **Await final configuration** in eligible new and existing iOS/iPadOS automated device enrollment profiles. This setting enables an out-of-the-box locked experience in Setup Assistant. It prevents device users from accessing restricted content or changing settings on the device until most Intune device configuration policies are installed. You can configure the setting in an existing automated device enrollment profile, or in a new profile (**Devices** > **By platform** > **iOS/iPadOS** > **Device onboarding** > **Enrollment** > **Enrollment program tokens** > **Create profile**). For more information, see [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

#### New setting gives Intune admins control over device-to-category mapping<!-- 15029839 -->  
Control visibility of the device category prompt in Intune Company Portal. You can now hide the prompt from end users and leave the device-to-category mapping up to Intune admins. The new setting is available in the admin center under **Tenant Administration** > **Customization** > **Device Categories**. For more information, see [Device categories](../apps/company-portal-app.md#device-categories).

#### Support for multiple enrollment profiles and tokens for fully managed devices <!-- 14205233  -->  
Create and manage multiple enrollment profiles and tokens for Android Enterprise fully managed devices. With this new functionality, you can now use the *EnrollmentProfileName* dynamic device property to automatically assign enrollment profiles to fully managed devices. The enrollment token that came with your tenant remains in a default profile. For more information, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md).

<a name='new-azure-ad-frontline-worker-experience-for-ipad-public-preview---6367427----'></a>

#### New Microsoft Entra frontline worker experience for iPad (public preview)<!-- 6367427  -->  
*This capability begins to roll out to tenants in mid-April.*

Intune now supports a frontline worker experience for iPhones and iPads using Apple automated device enrollment. You can now enroll devices that are enabled in Microsoft Entra ID shared mode via zero-touch. For more information about how to configure automated device enrollment for shared device mode, see [Set up enrollment for devices in Microsoft Entra shared device mode](../enrollment/automated-device-enrollment-shared-device-mode.md).  

Applies to:

- iOS/iPadOS

### Device management

#### Endpoint security firewall policy support for log configurations<!-- 16730565   -->  
You can now configure settings in [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune) that configure firewall logging options. These settings can be found in the *Microsoft Defender Firewall* profile template for the *Windows 10 and later* platform, and are available for the *Domain*, *Private*, and *Public* profiles in that template.

Following are the new settings, all found in the [Firewall configuration service provider (CSP)](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx):

- Enable Log Success Connections
- Log File Path
- Enable Log Dropped Packets
- Enable Log Ignored Rules

Applies to:

- Windows 11

#### Endpoint security firewall rules support for Mobile Broadband (MBB)<!-- 16730577  -->  
The **Interface Types** setting in [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune) now include the option for **Mobile Broadband**. Interface Types is available in the **Microsoft Defender Firewall Rules** profile for all platforms that support Windows. For information about the use of this setting and option, see [Firewall configuration service provider (CSP)](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx).

Applies to:  

- Windows 10
- Windows 11

#### Endpoint security firewall policy support for network list manager settings<!-- 9803477  -->  
We've added a pair of network list manager settings to [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune). To help determine when a Microsoft Entra device is or isn't on your on-premises domain subnets, you can use the network list manager settings. This information can help firewall rules apply correctly.

The following settings are found in a new category named *Network List Manager*, that's available in the *Microsoft Defender Firewall* profile template for the *Windows 10, Windows 11, and Windows Server* platform:

- Allowed Tls Authentication Endpoints
- Configured Tls Authentication Network Name

For information about Network Categorization settings, see [NetworkListManager CSP](/windows/client-management/mdm/policy-csp-networklistmanager).

Applies to:

- Windows 10
- Windows 11

#### Improvements to Devices area in admin center (public preview) <!-- 12775837 -->  
The Devices area in the admin center now has a more consistent UI, with more capable controls and an improved navigation structure so you can find the information you need faster. To opt in to the public preview and try out the new experience, go to **Devices** and flip the toggle at the top of the page. Improvements include:

* A new scenario-focused navigation structure.
* New location for platform pivots to create a more consistent navigation model.
* A reduction in journey, helping you get to your destination faster.
* Monitoring and reports are within the management workflows, giving you easy access to key metrics and reports without having to leave the workflow.
* A consistent way across list views to search, sort, and filter data.

For more information about the updated UI, see [Try new Devices experience in Microsoft Intune](public-preview.md).

### Device security

#### Microsoft Intune Endpoint Privilege Management (public preview)<!-- 15654169   -->  
As a public preview, you can now use Microsoft Intune Endpoint Privilege Management. With Endpoint Privilege Management, admins can set policies that allow standard users to perform tasks normally reserved for an administrator. Endpoint Privilege Management can be configured in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) at **Endpoint security** > **Endpoint Privilege Management**.

With the public preview, you can configure policies for *automatic* and *user-confirmed* workflows that elevate the run-time permissions for apps or processes you select. You then assign these policies to users or devices that have end users running without Administrator privileges. Once policy is received, Endpoint Privilege Management will broker the elevation on behalf of the user, allowing them to elevate approved applications without needing full administrator privileges. The preview also includes built-in insights and reporting for Endpoint Privilege Management.

To learn how to activate the public preview and use Endpoint Privilege Management policies, start with [Use Endpoint Privilege Management with Microsoft Intune](../protect/epm-overview.md). Endpoint Privilege Management is part of the [Intune Suite](intune-add-ons.md) offering, and free to try while it remains in public preview.

### Intune apps

#### Newly available protected apps for Intune<!-- 16927438, 17030201, 17074872 17103353 -->  
The following protected apps are now available for Microsoft Intune:

- EVALARM by GroupKom GmbH (iOS)
- ixArma by INAX-APPS (Android)
- Seismic | Intune by Seismic Software, Inc.
- Microsoft Viva Engage by Microsoft (formally Microsoft Yammer)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Diagnostic data collection for Endpoint Privilege Management<!-- 17392824   -->  
To support the release of Endpoint Privilege Management, we've updated [Collect diagnostics from a Windows device](../remote-actions/collect-diagnostics.md) to include the following data, which is collected from devices enabled for Endpoint Privilege Management:

- Registry keys:

  - HKLM\SOFTWARE\Microsoft\EPMAgent

- Commands:

  - %windir%\system32\pnputil.exe /enum-drivers

- Log files:

  - %ProgramFiles%\Microsoft EPM Agent\Logs\\\*.*
  - %windir%\system32\config\systemprofile\AppData\Local\mdm\\\*.log

#### View status for pending and failed organizational messages<!-- 17017707  -->  
We've added two more states to organizational message reporting details to make it easier to track pending and failed messages in the admin center.

- **Pending**: The message hasn't been scheduled yet and is currently in progress.
- **Failed**: The message failed to schedule due to a service error.

For information about reporting details, see [View reporting details for organizational messages](/microsoft-365/admin/misc/organizational-messages-microsoft-365).  


#### More reporting information related to tenant attach devices<!-- 9220597  -->  
You can now view information for tenant attach devices in the existing antivirus reports under the Endpoint Security workload. A new column differentiates between devices managed by Intune and devices managed by Configuration Manager. This reporting information is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Endpoint security** > **Antivirus**.

## Week of March 13, 2023

### Device management

#### Meta Quest 2 and Quest Pro are now in Open Beta (US only) on Microsoft Intune for Android Open Source Devices  
Microsoft Intune for Android open source project devices (AOSP) has welcomed Meta Quest 2 and Quest Pro into Open Beta for the US market.

For more information, go to [Operating systems and browsers supported by Microsoft Intune](supported-devices-browsers.md)

Applies to:

- Android (AOSP)

### App management

#### Trusted Root Certificates Management for Intune App SDK for Android<!-- 15135752 -->  
If your Android application requires SSL/TLS certificates issued by an on-premises or private certificate authority to provide secure access to internal websites and applications, the Intune App SDK for Android now has support for certificate trust management. For more information and examples, see [Trusted Root Certificates Management](../developer/app-sdk-android-phase7.md#trusted-root-certificates-management).

#### System context support for UWP apps<!-- 16544103 -->  
In addition to user context, you can deploy Universal Windows Platform (UWP) apps from the **Microsoft Store app (new)** in system context. If a provisioned *.appx* app is deployed in system context, the app auto-installs for each user that logs in. If an individual end user uninstalls the user context app, the app still shows as installed because it's still provisioned. In addition, the app must not already be installed for any users on the device. Our general recommendation is to not mix install contexts when deploying apps. Win32 apps from the **Microsoft Store app (new)** already support system context.

## Week of March 6, 2023

### App management

#### Deploy Win32 apps to device groups<!-- 7359954 -->  
You can now deploy Win32 apps with **Available** intent to device groups. For more information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

### Device management

#### New URL for Microsoft Intune admin center<!-- 17441426 -->  
The Microsoft Intune admin center has a new URL: [https://intune.microsoft.com](https://intune.microsoft.com). The previously used URL, [https://endpoint.microsoft.com](https://endpoint.microsoft.com), continues to work but will redirect to the new URL in late 2023. We recommend taking the following actions to avoid issues with Intune access and automated scripts:

* Update login or automation to point to `https://intune.microsoft.com`.
* Update your firewalls, as needed, to allow access to the new URL.
* Add the new URL to your favorites and bookmarks.
* Notify your helpdesk and update IT administrator documentation.

### Tenant administration

#### Add CMPivot queries to Favorites folder<!-- 16702226 -->
You can add your frequently used queries to a **Favorites** folder in CMPivot. CMPivot allows you to quickly assess the state of a device managed by Configuration Manager via Tenant Attach and take action. The functionality is similar to one already present in the Configuration Manager console. This addition helps you keep all your most used queries in one place. You can also add tags to your queries to help search and find queries. The queries saved in the Configuration Manager console aren't automatically added to your **Favorites** folder. You need to create new queries and add them to this folder. For more information about CMPivot, see [Tenant attach: CMPivot usage overview](../../configmgr/tenant-attach/cmpivot-start.md).

### Device enrollment

#### New Microsoft Store apps now supported with the Enrollment Status Page<!-- 16280325 -->
The Enrollment Status Page (ESP) now supports the new Microsoft store applications during Windows Autopilot. This update enables better support for the new Microsoft Store experience and should be rolling out to all tenants starting with Intune 2303. For related information, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

## Week of February 27, 2023

### Device configuration

#### Support for Locate device on Android Enterprise corporate owned fully managed and Android Enterprise corporate owned work profile devices<!--12391424 -->

You can now use "Locate device" on Android Enterprise corporate owned fully managed and Android Enterprise corporate owned work profile devices. With this feature, admins are able to locate lost or stolen corporate devices on-demand.

In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you need to turn the feature on using a device configuration profiles (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Device Restrictions** for profile type).

Select **Allow** on the **Locate device** toggle for fully managed and corporate owned work profile devices and select applicable groups. **Locate device** is available when you select **Devices**, and then select **All devices**. From the list of devices you manage, select a supported device, and choose the **Locate device** remote action.

For information on locating lost or stolen devices with Intune, go to:

- [Locate lost or stolen devices with Intune](../remote-actions/device-locate.md)

Applies to:

- Android Enterprise corporate owned fully managed
- Android Enterprise corporate owned dedicated devices
- Android Enterprise corporate owned work profile

#### Intune add-ons <!-- 13817801 -->

Microsoft Intune Suite provides mission-critical advanced endpoint management and security capabilities into Microsoft Intune. 

You can find add-ons to Intune in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Tenant administration** > **Intune add-ons**.

For detailed information, see [Use Intune Suite add-on capabilities](intune-add-ons.md).

#### View ServiceNow Incidents in the Intune Troubleshooting workspace (Preview)<!-- 12508062 -->

In public preview, you can view a list of ServiceNow incidents associated with the user you've selected in the Intune Troubleshooting workspace. This new feature is available under **Troubleshooting + Support** > select a user > **ServiceNow Incidents**. The list of incidents shown have a direct link back to the source incident and show key information from the incident. All incidents listed link the "Caller" identified in the incident with the user selected for Troubleshooting.

For more information, go to [Use the troubleshooting portal to help users at your company](service-now-integration.md).

### Device security

#### Microsoft Tunnel for MAM is now generally available<!-- 16883728  -->

Now out of preview and generally available, you can add [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-overview.md) to your tenant. Tunnel for MAM supports connections from unenrolled [Android](../protect/microsoft-tunnel-mam-android.md) and [iOS](../protect/microsoft-tunnel-mam-ios.md) devices. This solution provides your tenant with a lightweight VPN solution that allows mobile devices access to corporate resources while adhering to your security policies.

In addition, MAM Tunnel for iOS now supports Microsoft Edge.

Previously, Tunnel for MAM for Android and iOS was in public preview and free for use. With this release as generally available, this solution now requires an add-on license for its use.

For licensing details, see [Intune add-ons](intune-add-ons.md).

Applies to:

- Android
- iOS

### Tenant administration

#### Organizational messages now support custom destination URLs <!-- 16576068  -->

You can now add any custom destination URL to organizational messages in the taskbar, notifications area, and Get Started app. This feature applies to Windows 11. Messages created with Microsoft Entra registered domains that are in a scheduled or active state are still supported. For more information, see [Create organizational messages](/microsoft-365/admin/misc/organizational-messages-microsoft-365?tabs=taskbar#step-1-create-a-message). 

## Week of February 20, 2023 (Service release 2302)

### App management

#### Latest iOS/iPadOS version available as minimum OS requirement for LOB and store apps<!-- 16433620  -->  
You can specify iOS/iPadOS 16.0 as the minimum operating system for line-of-business and store app deployments. This setting option is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** > *iOS store app or Line-of-business app*. For more information about managing apps, see [Add apps to Microsoft Intune](../apps/apps-add.md).

#### Newly available protected app for Intune<!-- 16655639  -->  
The following protected app is now available for Microsoft Intune:

- Egnyte for Intune by Egnyte

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Device configuration

#### Endpoint Manager admin center is renamed to Intune admin center<!-- 15560662   -->  
The Microsoft Endpoint Manager admin center is now called the **Microsoft Intune admin center**.

#### A new Associated Assignments tab for your filters<!-- 7538503  -->  
When you assign an app or policy, you can filter the assignment using different device properties, such as device manufacturer, model, and ownership. You can create and associate a filter with the assignment.

After you create a filter, there's a new **Associated Assignments tab**. This tab shows all the policy assignments, the groups that receive the filter assignments, and if the filter is using **Exclude** or **Include**:

1. Sign in to the Microsoft Intune admin center.
2. Go to **Devices** > **Organize devices** > **Filters** > Select an existing filter > **Associated Assignments tab**.
 
For more information on filters, go to:

- [Use filters when assigning your apps, policies, and profiles in Intune](filters.md)
- [Device properties, operators, and rule editing when creating filters in Intune](filters-device-properties.md)

#### Size and generation included in iOS/iPadOS model information<!-- 16406692  -->  
You can view the size and generation for enrolled iOS/iPadOS devices as part of the **Model** attribute in **Hardware device details**.

Go to **Devices > All devices** > select one of your listed devices and select **Hardware** to open its details. For example, iPad Pro 11 inch (third generation) displays for the device model instead of iPad Pro 3. For more information, go to: [See device details in Intune](../remote-actions/device-inventory.md#hardware-device-details)

Applies to:  
- **iOS/iPadOS**

#### Disable Activation Lock device action for supervised iOS/iPadOS devices<!-- 15571509 -->  
You can use the **Disable Activation Lock** device action in Intune to bypass Activation Lock on iOS/iPadOS devices without requiring the current username or password.

This new action is available under  **Devices > iOS/iPadOS >** *select one of your listed devices* **> Disable Activation Lock**.

More information on managing Activation Lock is available at [Bypass iOS/iPadOS Activation Lock with Intune](../remote-actions/device-activation-lock-disable.md) or on Apple's website at [Activation Lock for iPhone, iPad, and iPod touch - Apple Support.](https://support.apple.com/en-us/HT201365)

Applies to:  
- **iOS/iPadOS**

#### Allow Temporary Enterprise Feature Control is available in the Settings Catalog<!-- 15752120  -->  
In on-premises group policy, there's an **Enable features introduced via servicing that are off by default** setting.

In Intune, this setting is known as **Allow Temporary Enterprise Feature Control** and is available in the Settings Catalog. This servicing adds features that off by default. When set to **Allowed**, these features are enabled and turned on.

For more information on this feature, go to:

- [AllowTemporaryEnterpriseFeatureControl](/windows/client-management/mdm/policy-csp-Update#allowtemporaryenterprisefeaturecontrol) policy CSP
- [Blog: Commercial control for continuous innovation](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/commercial-control-for-continuous-innovation/ba-p/3737575)

The Windows features that enabled by this policy setting should release later in 2023. Intune is releasing this policy setting now for your awareness and preparation, which is before any need to use the setting with future Windows 11 releases.

For more information on the settings catalog, go to [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

Applies to:

- Windows 11

### Device management

#### Device Control support for Printer Protection (Preview)<!-- 12355154  -->  
In public preview, Device Control profiles for Attack Surface Reduction policy now support [reusable settings groups for Printer Protection](../protect/reusable-settings-groups.md#add-reusable-groups-to-a-device-control-profile).

Microsoft Defender for Endpoint Device Control [Printer Protection](/microsoft-365/security/defender-endpoint/printer-protection-overview) enables you to audit, allow, or prevent printer with or without exclusions within Intune. It allows you to block users from printing via a non-corporate network printer or non-approved USB printer. This feature adds another layer of security and data protection for work from home and remote work scenarios.

Applies to:  
- Windows 10
- Windows 11

#### Support to delete stale devices that are managed through Security Management for Microsoft Defender for Endpoint<!--14729617  -->   
You can now **Delete** a device that's managed through the [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md) solution from within the Microsoft Intune admin center. The delete option appears along with other device management options when you view the device's Overview details. To locate a device managed by this solution, in the admin center go to **Devices** > **All devices**, and then select a device that displays either *MDEJoined* or *MDEManaged* in the *Managed by* column.

#### New settings and setting options available in the Apple Settings Catalog<!-- 16813380  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Login > Service Management - Managed Login Items**:

- Team Identifier

**Microsoft Office > Microsoft Office**:

- Office Activation Email Address

Applies to:  
- macOS

**Networking > Domains**:

- Cross Site Tracking Prevention Relaxed Domains

Applies to:  
- iOS/iPadOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Device security
 
#### Use Endpoint security Antivirus policy to manage Microsoft Defender update behavior (Preview)<!-- 11890335 -->  
As part of a public preview for Endpoint security [Antivirus policy](../protect/endpoint-security-antivirus-policy.md), you can use the new profile **Defender Update controls** for the *Windows 10 and later* platform to manage update settings for Microsoft Defender. The new profile includes settings for the rollout release channel. With the rollout channel, devices and users receive Defender Updates that are related to daily security intelligence updates, monthly platform updates, and monthly engine updates.

This profile includes the following settings, which are all directly taken from [Defender CSP - Windows Client Management](/windows/client-management/mdm/policy-csp-Defender).

- Engine Updates Channel
- Platform Updates Channel
- Security Intelligence Updates Channel

These settings are also available from the [settings catalog](../configuration/settings-catalog.md) for the *Windows 10 and later* profile.

Applies to:  
- Windows 10
- Windows 11

## Week of February 6, 2023

### Tenant administration

#### Apply recommendations and insights to enrich the Configuration Manager site health and device management experience<!--16957774 -->

You can now use the Microsoft Intune admin center to view recommendations and insights for your Configuration Manager sites. These recommendations can help you improve the site health and infrastructure and enrich the device management experience.

Recommendations include:  

- How to simplify your infrastructure
- Enhance device management
- Provide device insights
- Improve the health of the site

To view recommendations, open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Connectors and tokens** > **Microsoft Endpoint Configuration Manager**,  and select a *site* to view recommendations for that site.  Once selected, the *Recommendations* tab displays each insight along with a *Learn more* link. This link opens details on how to apply that recommendation.

For more information, see [Enable Microsoft Intune tenant attach - Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md).

## Week of January 30, 2023

### Device management

#### HTC Vive Focus 3 supported on Microsoft Intune for Android Open Source Devices<!--15670082--> 

Microsoft Intune for Android open source project devices (AOSP) now supports HTC Vive Focus 3. 

For more information, go to [Operating systems and browsers supported by Microsoft Intune](supported-devices-browsers.md)

Applies to:

- Android (AOSP)

#### Introducing support for laser pointers in Remote Help<!-- 16108312 -->

In Remote Help, you can now use a laser pointer when you're providing assistance on Windows.

For more information on Remote Help, go to [Remote Help](remote-help.md).

Applies to:

- Windows 10/11

## Week of January 23, 2023 (Service release 2301)

### App management

#### Configure whether to show Configuration Manager apps in Windows Company Portal<!-- 9135109 -->  
In Intune, you can choose whether to show or hide Configuration Manager apps from appearing in the Windows Company Portal. This option is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**. Next to **Settings**, select **Edit**. The option to **Show** or **Hide** the Configuration Manager applications are located in the **App Sources** section of the pane. For related information about configuring the Company Portal app, see [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

#### Block pinning web pages to Managed Home Screen app<!-- 15593458 -->  
On Android Enterprise dedicated devices using Managed Home Screen, you can now use app configuration to configure the Managed Home Screen app to block pinning browser web pages to Managed Home Screen. The new `key` value is `block_pinning_browser_web_pages_to_MHS`. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

### Device management

#### Grace period status visible in Microsoft Intune app for Android<!-- 13498225 -->  
The Microsoft Intune app for Android now shows a grace period status to account for devices that don't meet compliance requirements but are still within their given grace period. Users can see the date by which devices must be compliant, and the instructions for how to become compliant. If they don't update their device by the given date, the device is marked as noncompliant. For more information, see the following docs:

- [Configure compliance policies with actions for noncompliance](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance)
- [Check compliance status](../user-help/check-compliance-microsoft-intune-app-android.md)


#### Software update policies for macOS are now generally available<!-- 12393100 -->  
Software update policies for macOS devices are now generally available. This general availability applies to supervised devices running macOS 12 (Monterey) and later. Improvements are being made to this feature.

For more information, see [Use Microsoft Intune policies to manage macOS software updates](../protect/software-updates-macos.md).

#### Windows Autopilot device diagnostics<!-- 16697347 -->  
Windows Autopilot diagnostics is available to download in Microsoft Intune admin center from either in the Autopilot deployments monitor or Device Diagnostics monitor for an individual device.

### Device enrollment

#### Enrollment notifications now generally available<!-- 16545401 -->  
Enrollment notifications are now generally available, and are supported on Windows, Apple, and Android devices. This feature is only supported with user-driven enrollment methods. For more information, see [Set up enrollment notifications](../enrollment/enrollment-notifications.md).  

#### Skip or show Terms of Address pane in Setup Assistant<!-- 14661838 -->  
Configure Microsoft Intune to skip or show a new Setup Assistant pane called **Terms of Address** during Apple Automated Device Enrollment. The **Terms of Address** lets users on iOS/iPadOS and macOS devices personalize their device by selecting how the system addresses them: feminine, neutral, or masculine.  The pane is visible during enrollment by default, and is available for select languages.  You can hide it on devices running iOS/iPadOS 16 and later, and macOS 13 and later. For more information about the Setup Assistant screens supported in Intune, see:

- [Setup Assistant screens for Macs](../enrollment/device-enrollment-program-enroll-macos.md#setup-assistant-screen-reference)
- [Setup Assistant screens for iOS/iPadOS](../enrollment/device-enrollment-program-enroll-ios.md#setup-assistant-screen-reference)

### Device security

#### Microsoft Tunnel for Mobile Application Management for iOS/iPadOS (Preview)<!-- 15769204, 9851288 -->  
As a public preview, you can use the Mobile Application Management (MAM) to the Microsoft Tunnel VPN gateway for iOS/iPadOS. With this preview for iOS devices that haven't enrolled with Intune, supported apps on those unenrolled devices can use Microsoft Tunnel to connect to your organization when working with corporate data and resources. This feature includes VPN gateway support for:

- Secure access to on-premises apps and resources using modern authentication
- Single Sign On and Conditional Access

For more information, go to:

- [Microsoft Tunnel for Mobile Application Management for iOS/iPadOS admin guide (public preview)](../protect/microsoft-tunnel-mam-ios.md)
- [Microsoft Tunnel for MAM iOS SDK developer guide](../developer/tunnel-mam-ios-sdk.md)

Applies to:

- iOS/iPadOS

####  Attack surface reduction policy support for Security settings management for Microsoft Defender for Endpoint <!-- 13816760 -->  
Devices managed through the [MDE Security configuration](../protect/mde-security-integration.md#which-solution-should-i-use) scenario support attack surface reduction policy. To use this policy with devices that use Microsoft Defender for Endpoint but aren't enrolled with Intune:

1. In the Endpoint Security node, create a new *Attack surface reduction* policy.
2. Select **Windows 10, Windows 11, and Windows Server** as the *Platform*.
3. Select **Attack Surface Reduction Rules** for the *Profile*.

Applies to:

- Windows 10
- Windows 11

#### SentinelOne – New mobile threat defense partner<!-- 13911932 -->  
You can now use [SentinelOne](../protect/sentinelone-mobile-threat-defense-connector.md) as an integrated Mobile Threat Defense (MTD) partner with Intune. By configuring the SentinelOne connector in Intune, you can control mobile device access to corporate resources using Conditional Access that's based on risk assessment in your compliance policy. The SentinelOne connector can also send risk levels to app protection policies.

### Device configuration

#### Device Firmware Configuration Interface (DFCI) supports Fujitsu devices<!--10249866 -->  
For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type).

Some Fujitsu devices running Windows 10/11 are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, go to:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](../../autopilot/dfci-management.md)

Applies to:

- Windows 10
- Windows 11

#### Support for Bulk Device Actions on devices running Android (AOSP)<!--15397458 -->  
You can now complete "Bulk Device Actions" for devices running Android (AOSP). The bulk device actions supported on devices running Android (AOSP) are Delete, Wipe and Restart.

Applies to:

- Android (AOSP)

#### Updated descriptions for iOS/iPadOS and macOS settings in the settings catalog<!-- 16360170 -->  
The settings catalog lists all the settings you can configure, and all in one place. For the iOS/iPadOS and macOS settings, for each setting category, the descriptions are updated to include more detailed information.

For more information on the settings catalog, go to:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md)
- [Common tasks you can complete using the Settings Catalog in Intune](../configuration/settings-catalog-common-features.md)

Applies to:

- iOS/iPadOS
- macOS

#### New settings available in the Apple Settings Catalog<!--16237513  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Accounts > Subscribed Calendars**:

- Account Description
- Account Host Name
- Account Password
- Account Use SSL
- Account Username

Applies to:

- iOS/iPadOS

**Networking > Domains**:

- Cross Site Tracking Prevention Relaxed Domains

Applies to:

- macOS

The following settings are also in Settings Catalog. Previously, they were only available in Templates:

**File Vault**:
- User Enters Missing Info 

Applies to:

- macOS

**Restrictions**:
- Rating Region

Applies to:

- iOS/iPadOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).


<a name='filter-app-and-policy-assignments-by-the-devices-azure-ad-join-type-devicetrusttype---8110331---'></a>

#### Filter app and policy assignments by the device's Microsoft Entra join type (`deviceTrustType`)<!-- 8110331 -->  
When you assign an app or policy, you can filter the assignment using different device properties, such as device manufacturer, operating system SKU, and more.

A new device filter property `deviceTrustType` is available for Windows 10 and later devices. With this property, you can filter app and policy assignments depending on the Microsoft Entra join type. The values include **Microsoft Entra joined**, **Microsoft Entra hybrid joined**, and **Microsoft Entra registered**.

For more information on filters and the device properties you can use, go to:

- [Use filters when assigning your apps, policies, and profiles in Intune](filters.md)
- [Device properties, operators, and rule editing when creating filters in Intune](filters-device-properties.md)

Applies to:

- Windows 10 and later

### Monitor and troubleshoot

#### Download mobile app diagnostics in the Microsoft Intune admin center (public preview)<!-- 9353471 -->  
Now in public preview, access user-submitted mobile app diagnostics in the admin center, including app logs sent through Company Portal app for Android, Android (AOSP), or Windows, with support for iOS, macOS, and Microsoft Edge for iOS coming at a later date. For more information about accessing mobile app diagnostics for Company Portal, see [Configure Company Portal](../apps/company-portal-app.md#app-logs).

#### WinGet troubleshooting using diagnostic files<!-- 16724699 -->  
[WinGet](/windows/package-manager/winget/) is a command line tool that enables you to discover, install, upgrade, remove, and configure applications on Windows 10 and Windows 11 devices. When working with [Win32 app management in Intune](../apps/apps-win32-app-management.md), you can now use the following file locations to help troubleshoot WinGet:

- *%TEMP%\winget\defaultstate\*.log*
- *Microsoft-Windows-AppXDeployment/Operational*
- *Microsoft-Windows-AppXDeploymentServer/Operational*

#### Intune troubleshooting pane update<!-- 4442647 -->  
A new experience for the Intune Troubleshooting pane provides details about user's devices, policies, applications, and status. The troubleshooting pane includes the following information:

- A summary of policy, compliance, and application deployment status.
- Support for exporting, filtering, and sorting all reports.
- Support to filter by excluding policies and applications.
- Support to filter to a user's single device.
- Details about available device diagnostics and disabled devices.
- Details about offline devices that haven't checked-in to the service for three or more days.

You can find the troubleshooting pane in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot**. To view the new experience during preview, select **Preview upcoming changes to Troubleshooting and provide feedback** to display the **Troubleshooting preview** pane, then select **Try it now**.

#### New report for devices without compliance policy (preview)<!--14911124 -->  
We've added a new report named **Devices without compliance policy** to the Device compliance reports you can access through the *Reports* node of the Microsoft Intune admin center.  This report, which is in preview, uses a  newer reporting format that provides for more capabilities.

To learn about this new organizational report, see [Devices without compliance policy (Organizational)](reports.md#devices-without-compliance-policy-organizational).

An older version of this report remains available through the *Devices > Monitor* page of the admin center. Eventually, that older report version will retire, though it remains available for now.

#### Service health messages for tenant issues that require administrative attention<!-- 14791676 -->  
The *Service health and message center page* in the Microsoft Intune admin center can now display messages for **Issues in your environment that require action**. These messages are important communications that are sent to a tenant to alert administrators about issues in their environment that might require action to resolve.

You can view messages for *Issues in your environment that require action* in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by going to **Tenant administration** > **Tenant status** and then selecting the **Service health and message center** tab.

For more information about this page of the admin center, see [View details about your Tenant on the Intune tenant status page](tenant-status.md).

### Tenant administration

#### Improved UI experience for multiple certificate connectors<!-- 16263248 -->  
We've added pagination controls to the *Certificate connectors* view to help improve the experience when you have more than 25 certificate connectors configured. With the new controls, you can see the total number of connector records and easily navigate to a specific page when viewing your certificate connectors.

To view certificate connectors, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Tenant administration** > **Connectors and tokens** > **Certificate connectors**.

### Intune apps

#### Newly available protected app for Intune<!-- 16620158 -->  
The following protected app is now available for Microsoft Intune:

- Voltage SecureMail by Voltage Security

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Scripts

#### Preview PowerShell script package content in Endpoint Analytics<!-- 12930245 -->  
Admins can now see a preview of a PowerShell script's content for proactive remediations. The content is displayed in a grayed-out box with scrolling capability. Admins can't edit the content of the script in the preview. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Endpoint analytics** > **Proactive remediations**. For more information, see [PowerShell scripts for Proactive remediations](../../intune-service/fundamentals/powershell-scripts-remediation.md).

## Week of January 16, 2023

### App management

#### Win32 app supersedence GA<!-- 9318154 -->  

The feature set for Win32 app supersedence GA is available. It adds support for apps with supersedence during ESP, and also allows supersedence & dependency relationships to be added in the same app subgraph. For more information, see [Win32 app supersedence improvements](https://aka.ms/Intune/Win32-Supersedence). For information about Win32 app supersedence, see [Add Win32 app supersedence](../apps/apps-win32-supersedence.md).

## Week of January 9, 2023

### Device configuration

#### The Company Portal app enforces Password Complexity setting on Android Enterprise 12+ personally owned devices with a work profile<!-- 16211313  -->  
On Android Enterprise 12+ personally owned devices with a work profile, you can create a compliance policy and/or device configuration profile that sets the password complexity. Starting with the 2211 release, this setting is available in the Intune admin center:

- **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > Personally owned with a work profile > **Device restrictions** for profile type > **Password**
- **Devices** > **Compliance policies** > **Create policy** > **Android Enterprise** for platform > Personally owned with a work profile

The Company Portal app enforces the **Password complexity** setting.

For more information on this setting and the other settings you can configure on personally owned devices with a work profile, go to:

- [Device compliance settings for Android Enterprise in Intune](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile)
- [Device restriction settings list for Android Enterprise in Intune](../configuration/device-restrictions-android-enterprise-personal.md)

Applies to:

- Android Enterprise 12+ personally owned devices with a work profile

## Week of December 19, 2022

### Intune apps

#### Newly available protected app for Intune<!-- 15448654 -->  
The following protected app is now available for Microsoft Intune:

- Appian for Intune by Appian Corporation (Android)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of December 12, 2022 (Service release 2212)

### Device configuration

#### Remote Help client app includes a new option to disable chat functionality in the Tenant level setting<!-- 14685052 -->  
In the Remote Help app, admins can disable chat functionality from the new tenant level setting. Turning on the disable chat feature removes the chat button in the Remote Help app. This setting can be found in the Remote Help **Settings** tab under **Tenant Administration** in Microsoft Intune.

For more information, see [Configure Remote Help for your tenant](remote-help.md#configure-remote-help-for-your-tenant).

**Applies to**: Windows 10/11

#### New settings available in the macOS Settings Catalog<!-- 16069006 -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**File Vault > File Vault Options**:

- Block FV From Being Disabled
- Block FV From Being Enabled

**Restrictions**:

- Allow Bluetooth Modification

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### There are default settings for SSO extension requests on iOS, iPadOS, and macOS devices<!-- 15082414-15084030 -->
When you create a single sign-on app extension configuration profile, there are some settings that you configure. The following settings use the following default values for all SSO extension requests:

- **AppPrefixAllowList** key
  - macOS default value: `com.microsoft.,com.apple.`
  - iOS/iPadOS default value: `com.apple.`

- **browser_sso_interaction_enabled** key
  - macOS default value: `1`
  - iOS/iPadOS default value: `1`

- **disable_explicit_app_prompt** key
  - macOS default value: `1`
  - iOS/iPadOS default value: `1`

If you configure a value other than the default value, then the configured value overwrites the default value.

For example, you don't configure the `AppPrefixAllowList` key. By default, all Microsoft apps (`com.microsoft.`) and all Apple apps (`com.apple.`) are enabled for SSO on macOS devices. You can overwrite this behavior by adding a different prefix to the list, such as `com.contoso.`.

For more information on the Enterprise SSO plug-in, go to [Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS and macOS devices in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md).

Applies to:

- iOS/iPadOS
- macOS

### Device enrollment

#### Enrollment token lifetime increases to 65 years for Android Enterprise dedicated devices<!-- 15094454  -->  
Now you can create an enrollment profile for Android Enterprise dedicated devices that's valid for up to 65 years.  If you have an existing profile, the enrollment token still expires at whatever date you chose when you created the profile, but during renewal you can extend the lifetime. For more information about creating an enrollment profile, see [Set up Intune enrollment for Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md#create-an-enrollment-profile).

### Device management

#### Update policies for macOS now available for all supervised devices<!-- 16141990  -->  
Software update policies for macOS devices now apply to all macOS supervised devices. Previously, only those devices that enrolled through Automated Device Enrollment (ADE) would qualify to receive updates. For more information on configuring update policies for macOS, see [Use Microsoft Intune policies to manage macOS software updates](../protect/software-updates-macos.md).

Applies to:  
- macOS

#### Policy and reports for Windows feature updates and expedited quality updates are now Generally Available<!-- 15738456 -->  
Both the policies and reports for managing feature updates and quality updates (expedited updates) for Windows 10 and later, are out of preview and now generally available.

For more information about these policies and reports, see:

- [Feature updates policy](../protect/windows-10-feature-updates.md)
- [Expedite quality updates policy](../protect/windows-10-expedite-updates.md)
- [Windows Update compliance reports](../protect/windows-update-reports.md)

Applies to:

- Windows 10/11

## Week of November 28, 2022

### App management

#### Microsoft Store apps in Intune<!-- 12708346 -->  
You can now search, browse, configure, and deploy Microsoft Store apps within Intune. The new Microsoft Store app type is implemented using the Windows Package Manager. This app type features an expanded catalog of apps, which includes both UWP apps and Win32 apps. Roll out of this feature is expected to complete by December 2, 2022. For more information, see [Add Microsoft Store apps to Microsoft Intune](../apps/store-apps-microsoft.md).

### Tenant administration

#### Access policies for multiple Administrator Approval (public preview)<!-- 9348867  -->  
In public preview, you can use Intune *access policies* to require that a second Administrator Approval account approve a change before the change is applied. This capability is known as multiple Administrator Approval (MAA).

You create an access policy to protect a type of resource, like App deployments. Each access policy also includes a group of users who are *approvers* for the changes protected by the policy. When a resource, like an app deployment configuration, is protected by an access policy, any changes that made to the deployment, including creating, deleting, or modifying an existing deployment, won't apply until a member of the approvers group for that access policy reviews and approves that change.

Approvers can also reject requests. The individual requesting a change and the approver can provide notes about the change, or why it was approved or rejected.

Access policies are supported for the following resources:

- **Apps** – Applies to [app deployments](../apps/apps-add.md), but doesn't apply to app protection policies.
- **Scripts** – Applies to deploying scripts to devices that run [macOS](../apps/macos-shell-scripts.md) or [Windows](../apps/intune-management-extension.md).

For more information, see [Use Access policies to require multiple administrative approval](multi-admin-approval.md).

### Device security

#### Microsoft Tunnel for Mobile Application Management for Android (Preview)<!-- 15769204 -->  
As a public preview, you can now use Microsoft Tunnel with unenrolled devices. This capability is called [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-mam.md) (MAM). This preview supports Android, and without any changes to your existing Tunnel infrastructure, supports the Tunnel VPN gateway for:

- Secure access to on-premises apps and resources using modern authentication
- Single Sign On and Conditional Access

To use Tunnel MAM, unenrolled devices must install Microsoft Edge, Microsoft Defender for Endpoint, and the Company Portal. You can then use the Microsoft Intune admin center to configure the following profiles for the unenrolled devices:

- An App configuration profile for managed apps, to configure Microsoft Defender on devices for use as the Tunnel client app.
- A second App configuration profile for managed apps, to configure Microsoft Edge to connect to Tunnel.
- An App protection profile to enable automatic start of the Microsoft Tunnel connection.

Applies to:

- Android Enterprise

## Week of November 14, 2022 (Service release 2211)

### App management

#### Control the display of Managed Google Play apps<!-- 621615   -->  
You can group Managed Google Play apps into collections and control the order that collections are displayed when selecting apps in Intune. You can also make apps visible via search only. This capability is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **All Apps** > **Create** > **Managed Google Play app**. For more information, see [Add a Managed Google Play store app directly in the Intune admin center](../apps/apps-add-android-for-work.md#add-a-managed-google-play-store-app-directly-in-the-microsoft-intune-admin-center).

### Device configuration

#### New password complexity setting for Android Enterprise 12+ personally owned devices with a work profile<!-- 12436068  -->  
On Android Enterprise 11 and older personally owned devices with a work profile, you can set the following password settings:

- **Devices** > **Compliance** > **Android Enterprise** for platform > **Personally owned work profile** > **System security** > **Required password type**, **Minimum password length**
- **Devices** > **Manage devices** > **Configuration** > **Android Enterprise** for platform > **Personally owned work profile** > **Device restrictions** > **Work profile settings** > **Required password type**, **Minimum password length**
- **Devices** > **Manage devices** > **Configuration** > **Android Enterprise** for platform > **Personally owned work profile** > **Device restrictions** > **Password** > **Required password type**, **Minimum password length**

Google is deprecating the **Required password type** and **Minimum password length** settings for Android 12+ personally owned devices with a work profile and replacing them with new password complexity requirements. For more information about this change, go to [Day zero support for Android 13](https://aka.ms/Intune/Android13).

The new **Password complexity** setting has the following options:

- **None**: Intune doesn't change or update this setting. By default, the OS might not require a password.
- **Low**: Pattern or PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked.
- **Medium**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length, alphabetic length, or alphanumeric length must be at least four characters.
- **High**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length must be at least eight characters. The alphabetic or alphanumeric length must be at least six characters.

On Android 12+, if you currently use the **Required password type** and **Minimum password length** settings in a compliance policy or device configuration profile, then we recommend using the new **Password complexity** setting instead.

If you continue to use the **Required password type** and **Minimum password length** settings, and don't configure the **Password complexity** setting, then new devices running Android 12+ might default to the **High** password complexity.

For more information on these settings and what happens to existing devices with the deprecated settings configured, go to:

- [Android Enterprise personally owned devices with a work profile - configuration profile settings list](../configuration/device-restrictions-android-enterprise-personal.md)
- [Android Enterprise personally owned devices with a work profile - compliance policy settings list](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile)

Applies to:

- Android Enterprise 12.0 and newer personally owned devices with a work profile

#### New settings available in the iOS/iPadOS and macOS Settings Catalog<!-- 16068756 -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Networking > DNS Settings**:

- DNS Protocol
- Server Addresses
- Server Name
- Server URL
- Supplemental Match Domains
- On Demand Rules
- Action
- Action Parameters
- DNS Domain Match
- DNS Server Address Match
- Interface Type Match
- SSID Match
- URL String Probe
- Prohibit Disablement

**File Vault**:

- Defer
- Defer Don't Ask At User Logout
- Defer Force At User Login Max Bypass Attempts
- Enable
- Show Recovery Key
- Use Recovery Key

**File Vault > File Vault Recovery Key Escrow**:

- Device Key
- Location

**Restrictions**:

- Allow Air Play Incoming Requests

Applies to:

- macOS

**Web > Web Content Filter**:

- Allow List Bookmarks
- Auto Filter Enabled
- Deny List URLs
- Filter Browsers
- Filter Data Provider Bundle Identifier
- Filter Data Provider Designated Requirement
- Filter Grade
- Filter Packet Provider Bundle Identifier
- Filter Packet Provider Designated Requirement
- Filter Packets
- Filter Sockets
- Filter Type
- Organization
- Password
- Permitted URLs
- Plugin Bundle ID
- Server Address
- User Defined Name
- User Name
- Vendor Config

Applies to:

- iOS/iPadOS
- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Device Firmware Configuration Interface (DFCI) supports Panasonic devices<!-- 15729353 -->  
For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type).

New Panasonic devices running Windows 10/11 are being enabled for DFCI starting Fall 2022. So, admins can create DFCI profiles to manage the BIOS and then deploy the profiles to these Panasonic devices.

Contact your device vendor or device manufacturer to ensure you get eligible devices.

For more information about DFCI profiles, go to:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](/autopilot/dfci-management)

Applies to:

- Windows 10
- Windows 11

#### Sign in and background item management support on macOS devices using the settings catalog<!-- 15751007  -->  
On macOS devices, you can create a policy that automatically opens items when users sign in to their macOS devices. For example, you can open apps, documents, and folders.

In Intune, the settings catalog includes new Service Management settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type > **Login** > **Service Management**. These settings can prevent users from disabling the managed login and background items on their devices.

For more information on the settings catalog, go to:

- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Common tasks you can complete using the Settings Catalog](../configuration/settings-catalog-common-features.md)

Applies to:

- macOS 13 and newer

### Intune apps

#### Newly available protected apps for Intune<!-- 16118715, 16118848, 16135107, 16027039, 15658466, 15658598  -->  
The following protected apps are now available for Microsoft Intune:

- Varicent by Varicent US OpCo Corporation
- myBLDNG by Bldng.ai
- Enterprise Files for Intune by Stratospherix Ltd
- ArcGIS Indoors for Intune by ESRI
- Meetings by Decisions by Decisions AS
- Idenprotect Go by Apply Mobile Ltd

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Review Cloud PC connectivity health checks and errors in Microsoft Intune admin center<!-- 13811774 -->  
You can now review connectivity health checks and errors in the Microsoft Intune admin center to help you understand if your users are experiencing connectivity issues. There's also a troubleshooting tool to help resolve connectivity issues. To see the checks, select **Devices** > **Windows 365** > **Azure network connections** > *select a connection in the list* > **Overview**.  

### Tenant administration

#### Deliver organizational messages for Windows 11 (public preview)<!-- 15314747  -->  
Use Microsoft Intune to deliver important messages and call-to-actions to employees on their devices.  Organizational messages are preconfigured messages intended to improve employee communication in remote and hybrid-work scenarios. They can be used to help employees adapt to new roles, learn more about their organization, and stay informed of new updates and trainings. You can deliver messages  just above the taskbar, in the notifications area, or in the Get Started app on Windows 11 devices.

During public preview, you can:

* Select from various preconfigured, common messages to assign to Microsoft Entra user groups.
* Add your organization's logo. 
* Include a custom destination URL in the message that redirects device users to a specific place.
* Preview messages in 15 supported languages, in dark and light theme.
* Schedule a delivery window and message frequency.
* Track the status of messages and the number of views and clicks they receive. Views and clicks are aggregated by messages.
* Cancel scheduled or active messages.  
* Configure a new built-in role in Intune called *Organizational Messages Manager*, which allows assigned admins to view and configure messages.  

All configurations need to be done in the Microsoft Intune admin center. The Microsoft Graph API isn't available to use with organizational messages. For more information, see [Overview of organizational messages](/microsoft-365/admin/misc/organizational-messages-microsoft-365).

## Week of November 7, 2022

### App management

#### Ending support for Windows Information Protection<!-- 15991481 -->
Windows Information Protection (WIP) policies without enrollment are being deprecated. You can no longer create new WIP policies without enrollment. Until December of 2022, you can modify existing policies until the deprecation of the *without enrollment* scenario is complete. For more information, go to [Support tip: End of support guidance for Windows Information Protection](https://aka.ms/Intune-WIP-support).

### Device Configuration

#### User configuration support for Windows 11 multi-session VMs is now generally available

You can now:
 - Configure user scope policies using **Settings catalog** and assign to groups of users, including ADMX-ingested policies
 - Configure user certificates and assign to users
 - Configure PowerShell scripts to install in the user context and assign to users

Applies to:
 - **Windows 11**
 - **Virtual machines** created in [Azure Public and Azure Government clouds](/enterprise-mobility-security/solutions/ems-intune-govt-service-description)
## Week of October 31, 2022

### App management

#### Primary MTD service app protection policy setting for Intune<!-- 13222514 -->
Intune now supports both Microsoft Defender for Endpoint and one non-Mobile Threat Defense (MTD) connector to be turned "On" for App Protection Policy evaluation per platform. This feature enables scenarios where a customer might want to migrate between Microsoft Defender for Endpoint and non-Microsoft MTD service. And, they don't want a pause in protection via risk scores in App Protection Policy. A new setting has been introduced under Conditional Launch health checks titled "Primary MTD service" to specify which service should be enforced for the end user. For more information, see [Android app protection policy settings](../apps/app-protection-policy-settings-android.md) and [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md).

## Week of October 24, 2022 (Service release 2210)

### App management

#### Use filters with app configuration policies for managed devices<!-- 7423842  -->  
You can use filters to refine the assignment scope when deploying app configuration policies for managed devices. You must first [create a filter](filters.md#create-a-filter) using any of the available properties for iOS and Android. Then, in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) you can assign your managed app configuration policy by selecting **Apps** > **Configuration** > **Create** > **Managed devices** and go to the assignment page. After selecting a group, you can refine the applicability of the policy by choosing a filter and deciding to use it in **Include** or **Exclude** mode. For related information about filters, see [Use filters when assigning your apps, policies, and profiles in Microsoft Intune admin center](filters.md).

### Device configuration

#### Group Policy analytics automatically applies scope tags assigned to admins when they import Group Policy objects<!-- 16017499 -->  
In Group Policy analytics, you can import your on-premises GPOs to see the policy settings that support cloud-based MDM providers, including Microsoft Intune. You can also see any deprecated settings or settings not available.

Now, scope tags assigned to admins are automatically applied when these admins import GPOs into Group Policy analytics.

For example, admins have **Charlotte**, **London**, or **Boston** scope tags assigned to their role:

- An admin with the **Charlotte** scope tag imports a GPO. 
- The **Charlotte** scope tag is automatically applied to the imported GPO.
- All admins with the **Charlotte** scope tag can see the imported object.
- Admins with only the **London** or only the **Boston** scope tags can't see the imported object from the **Charlotte** admin.

For admins to see the analytics or migrate the imported GPO to an Intune policy, these admins must have one of the same scope tags as the admin that did the import.

For more information on these features, go to:

- [Analyze your on-premises GPOs using Group Policy analytics in Microsoft Intune](../configuration/group-policy-analytics.md)
- [Use role-based access control (RBAC) and scope tags for distributed IT](scope-tags.md)

Applies to:

- Windows 11
- Windows 10

#### New network endpoints for Microsoft Intune<!--15847055 -->

New network endpoints have been added to our documentation to accommodate new Azure Scale Units (ASU) that are added to the Intune service. We recommend updating your firewall rules with the latest list of IP addresses to ensure that all network endpoints for Microsoft Intune are up-to-date.

For the full list, go to  [Network endpoints for Microsoft Intune](intune-endpoints.md).

#### Filter app and group policy assignments using Windows 11 SE operating system SKUs<!-- 10588651  -->  
When you assign an app or policy, you can filter the assignment using different device properties, such as device manufacturer, operating system SKU, and more.

Two new Windows 11 SE operating system SKUs are available. You can use these SKUs in your assignment filters to include or exclude Windows 11 SE devices from applying group-targeted policies and applications. 

For more information on filters and the device properties you can use, go to:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Device properties, operators, and rule editing when creating filters in Microsoft Intune](filters-device-properties.md)

Applies to:

- Windows 11 SE

#### New settings available in the iOS/iPadOS and macOS settings catalog <!-- 15514929  -->  
The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the settings catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Networking > Cellular**:

- Enable XLAT464

Applies to:

- iOS/iPadOS

**Privacy > Privacy Preferences Policy Control**:

- System Policy App Bundles

Applies to:

- macOS

**Restrictions**:

- Allow Rapid Security Response Installation
- Allow Rapid Security Response Removal

Applies to:

- iOS/iPadOS
- macOS

For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### New settings for Device Firmware Configuration Interface (DFCI) profiles on Windows devices<!-- 15511597  -->  
You can create a DFCI profile that enables the Windows OS to pass management commands from Intune to UEFI (Unified Extensible Firmware Interface) (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates > Device Firmware Configuration Interface**)

You can use this feature to control BIOS settings. There are new settings you can configure in the DFCI policy:

- Cameras:
  - Front camera
  - Infrared camera
  - Rear camera

- Radios:
  - WWAN
  - NFC

- Ports
  - SD Card

For more information on DFCI profiles, go to:

- [Use Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [DFCI profile settings list](../configuration/device-firmware-configuration-interface-windows-settings.md)

Applies to:

- Windows 11 on supported UEFI
- Windows 10 RS5 (1809) and later on supported UEFI

### Device enrollment

#### iOS/iPadOS Setup Assistant with modern authentication supports Just in Time Registration (public preview)<!-- 15515188 -->  
Intune supports just in time (JIT) Registration for iOS/iPadOS enrollment scenarios that use Setup Assistant with modern authentication. JIT Registration reduces the number of authentication prompts shown to users throughout the provisioning experience, giving them a more seamless onboarding experience. It eliminates the need to have the Company Portal app for Microsoft Entra registration and compliance checks, and establishes single sign-on across the device. JIT Registration is available in public preview for devices enrolling through Apple automated device enrollment and running iOS/iPadOS 13.0 or later. For more information, see [Authentication methods for automated device enrollment](../enrollment/automated-device-enrollment-authentication.md). 

### Device management

#### Connect Chrome OS devices in Intune (public preview)<!-- 14273312 -->  
View company or school-owned devices that run on Chrome OS in the Microsoft Intune admin center.  Now in public preview, you can establish a connection between the Google Admin console and Microsoft Intune admin center.  Device information about your Chrome OS endpoints is synced into Intune and viewable in your device inventory list. Basic remote actions, such as restart, wipe, and lost mode are also available in the admin center. For more information about how to set up a connection, see [Configure Chrome Enterprise connector](../enrollment/chrome-enterprise-connector-configure.md).  

#### Manage macOS software updates with Intune<!-- 9801186 -->  
You can now use Intune policies to manage macOS software updates for devices that enrolled using Automated Device Enrollment (ADE).  See [Manage macOS software update policies in Intune](../protect/software-updates-macos.md).

Intune supports the following macOS update types:

- Critical updates
- Firmware updates
- Configuration file updates
- All other updates (OS, built-in apps)

In addition to scheduling when a device updates, you can manage behaviors, like:

- Download and install: Download or install the update, depending on the current state.
- Download only: Download the software update without installing it.
- Install immediately: Download the software update and trigger the restart countdown notification.
- Notify only:  Download the software update and notify the user through the App Store.
- Install later: Download the software update and install it at a later time.
- Not configured: No action taken on the software update.

For information from Apple about managing macOS software updates, see [Manage software updates for Apple devices - Apple Support](https://support.apple.com/guide/deployment/manage-software-updates-depc4c80847a/web) in the Apple's Platform Deployment documentation.
Apple maintains a list of security updates at [Apple security updates - Apple Support](https://support.apple.com/en-us/HT201222).

#### Deprovision Jamf Pro from within the Microsoft Intune admin center<!-- 3485465  -->  
You can now [deprovision your Jamf Pro to Intune integration](../protect/conditional-access-jamf-cloud-connector.md#deprovision-jamf-pro-from-within-the-microsoft-intune-admin-center) from within the Microsoft Intune admin center. This feature can be useful should you no longer have access to the Jamf Pro console, through which you can also deprovision integration.

This capability functions similarly to disconnecting Jamf Pro from within the Jamf Pro console. So, after you remove the integration, your organization's Mac devices are removed from Intune after 90 days.

#### New hardware details available for individual devices running on iOS/iPadOS<!-- 15038076  -->  
Select **Devices** > **All devices** > *select one of your listed devices* and open it's **Hardware** details. The following new details are available in the **Hardware** pane of individual devices:

- **Battery level**: Shows the battery level of the device anywhere between 0 and 100, or defaults to null if the battery level can't be determined. This feature is available for devices running iOS/iPadOS 5.0 and later.
- **Resident users**: Shows the number of users currently on the shared iPad device, or defaults to null if the number of users can't be determined. This feature is available for devices running iOS/iPadOS 13.4 and later.

For more information, go to [View device details with Microsoft Intune](../remote-actions/device-inventory.md).

Applies to

- iOS/iPadOS

#### Use the `$null` value in filters<!-- 11030128  -->  
When you assign apps and policies to groups, you can use filters to assign a policy based on rules you create (**Tenant administration** > **Filters** > **Create**). These rules use different device properties, such as category or the enrollment profile.

Now, you can use the `$null` value with the `-Equals` and `-NotEquals` operators.

For example, use the `$null` value in the following scenarios:

- You want to target all devices that don't have a category assigned to the device.
- You want to target devices that don't have an enrollment profile property assigned to the device.

For more information on filters and the rules you can create, go to:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Device properties, operators, and rule editing when creating filters in Microsoft Intune](filters-device-properties.md)

Applies to:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10/11

### Device security

#### Reusable groups of settings for removable storage in Device Control profiles (preview) <!-- 7351534 -->  
In public preview, you can use [reusable groups of settings](../protect/reusable-settings-groups.md) with [device control profiles](../protect/endpoint-security-asr-policy.md#reusable-settings-groups-for-device-control-profiles) in your attack surface reduction policies.

The reusable groups for device control profiles include a collection of settings that support managing *read*, *write*, and *execute* access for removable storage. Examples of common scenarios include:

- Prevent write and execute access to all but allow specific approved USBs
- Audit write and execute access to all but block specific unapproved USBs
- Only allow specific user groups to access specific removable storage on a shared PC

Applies to:  
- Windows 10 or later

#### Reusable groups of settings for Microsoft Defender Firewall Rules (preview) <!-- 5653346, 6009541 -->  
In public preview, you can use [reusable groups of settings](../protect/reusable-settings-groups.md) that you can use with [profiles for Microsoft Defender Firewall Rules](../protect/endpoint-security-firewall-policy.md#add-reusable-settings-groups-to-profiles-for-firewall-rules). The reusable groups are collections of remote IP addresses and FQDNs that you define one time and can then use with one or more firewall rule profiles. You don't need to reconfigure the same group of IP addresses in each individual profile that might require them.

Features of the reusable settings groups include:

- Add one or more remote IP addresses.

- Add one or more FQDNs that can auto resolve to the remote IP address, or for one or more simple keywords when auto resolve for the group is off.

- Use each settings group with one or more firewall rule profiles and the different  profiles can support different access configurations for the group.

  For example, you can create two firewall rule profiles that reference the same reusable settings group and assign each profile to a different group of devices. The first profile can block access to all the remote IP addresses in the reusable settings group, while the second profile can be configured to allow access.

- Edits to a settings group that's in use are automatically applied to all Firewall Rules profiles that use that group.  

#### Attack surface reduction rule exclusions on a per-rule basis<!-- 13385644   -->  
You can now [configure per-rule exclusions for Attack surface reduction rules policies](../protect/endpoint-security-asr-policy.md#exclusions-for-attack-surface-reduction-rules). Per-rule exclusions are enabled through a new per-rule setting **ASR Only Per Rule Exclusions**.

When you create or edit attack surface reduction rule policies and change a setting that supports exclusions from the default of *Not configured* to any of the other available options, the new per-setting exclusion option becomes available. Any configurations for that setting instance of *ASR Only Per Rule Exclusions* apply to only that setting.

You can continue to configure global exclusions that apply to all attack surface reduction rules on the device
by using the setting **Attack Surface Reduction Only Exclusions**.

Applies to:

- Windows 10/11

> [!NOTE]  
> ASR policies don't support merge functionality for *ASR Only Per Rule Exclusions* and a policy conflict can result when multiple policies that configure *ASR Only Per Rule Exclusions* for the same device conflict. To avoid conflicts, combine the configurations for *ASR Only Per Rule Exclusions* into a single ASR policy. We are investigating adding policy merge for *ASR Only Per Rule Exclusions* in a future update.

#### Grant apps permission to silently use certificates on Android Enterprise devices<!-- 12441244    -->  
You can now configure silent use of certificates by apps on Android Enterprise devices that enrolled as **Fully Managed, Dedicated, and Corporate-Owned work Profile**.

This capability is available on a new **Apps** page in the certificate profile configuration workflow by setting **Certificate access** to  **Grant silently for specific apps (require user approval for other apps)**.  With this configuration, the apps you then select silently use the certificate. All other apps continue to use the default behavior, which is to require user approval.

This capability supports the following certificate profiles for only Android Enterprise Fully Managed, Dedicated, and Corporate-Owned work Profiles:

- [Derived credentials](../protect/derived-credentials.md#use-derived-credentials-for-app-authentication)
- [Imported PKCS](../protect/certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
- [PKCS](../protect/certificates-pfx-configure.md#create-a-pkcs-certificate-profile)
- [SCEP](../protect/certificates-profile-scep.md#create-a-scep-certificate-profile)

#### In-app notifications for Microsoft Intune app<!-- 13110609  -->  
Android Open Source Project(AOSP) device users can now receive compliance notifications in the Microsoft Intune app. This capability is only available on AOSP user-based devices. For more information, see [AOSP compliance notifications](../user-help/check-compliance-aosp.md#compliance-notifications).

### Intune apps

#### Newly available protected apps for Intune<!-- 15287512, 15448552   -->  
The following protected apps are now available for Microsoft Intune:

- MyITOps for Intune by MyITOps, Ltd
- MURAL - Visual Collaboration by Tactivos, Inc

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of October 17, 2022

### App management

#### Enhanced app picker for managed apps on Android devices<!-- 14531483 -->

Android device users can select, view, and remove their default app selections in the Intune Company Portal app. Company Portal securely stores the device user's default choices for managed apps. Users can view and remove their selections in the Company Portal app by going to **Settings** > **Default Apps** > **See defaults**. This feature is an enhancement to the Android custom app picker for managed apps, which is a part of the Android MAM SDK. For more information about how to view default apps, see [View and edit default apps](../user-help/use-managed-apps-on-your-device-android.md#view-and-edit-default-apps). 

## Week of October 10, 2022

### Device management

#### Microsoft Endpoint Manager branding change<!-- 15812021 -->  
As of October 12, 2022, the name Microsoft Endpoint Manager will no longer be used. Going forward, we refer to cloud-based unified endpoint management as Microsoft Intune and on-premises management as Microsoft Configuration Manager. With the launch of advanced management, Microsoft Intune is the name of our growing product family for endpoint management solutions at Microsoft.  For details, see [the official announcement](https://aka.ms/itsintune) on the endpoint management Tech Community blog. Documentation changes are ongoing to remove Microsoft Endpoint Manager.

For more information, see [Intune documentation]( ../../index.yml).

#### Grace period status visible in Windows Company Portal<!-- 14746606 -->  
Windows Company Portal now displays a grace period status to account for devices that don't meet compliance requirements but are still within their given grace period. Users are shown the date by which they need to become compliant and the instructions for how to become compliant. If users don't update their device by the given date, their device status changes to noncompliant. For more information about setting grace periods, see [Configure compliance policies with actions for noncompliance](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) and [Check access from Device details page](../user-help/check-device-access-windows-cpapp.md).

#### Linux device management available in Microsoft Intune<!-- 14616038 -->  
Microsoft Intune now supports Linux device management for devices running Ubuntu Desktop 22.04 or 20.04 LTS. Intune admins don't need to do anything to enable Linux enrollment in the Microsoft Intune admin center.  Linux users can [enroll supported Linux devices](../user-help/enroll-device-linux.md) on their own and use the Microsoft Edge browser to access corporate resources online.

In the admin center, you can:

- Enforce Conditional Access policies in Microsoft Edge.  
- [Create a Linux device compliance policy](../protect/device-compliance-get-started.md#device-compliance-policies) with rules about:  
  - Allowed distributions
  - Custom compliance
  - Device encryption
  - Password policy
- [Apply custom compliance settings](../protect/compliance-use-custom-settings.md) using POSIX-compliant shell scripts for discovery, and JSON files to define the custom settings you want to use.

## Week of October 03, 2022

### Device Security

#### Non-compliance warning message includes a link<!--13694184  -->  
In Remote Help, a link has been added to the non-compliance warning notification **View device compliance information** and it allows a helper to learn more about why the device isn't compliant in Microsoft Intune.

For more information, go to:

- [Microsoft Intune Remote Help](remote-help.md)

- [Monitor Device compliance](../protect/compliance-policy-monitor.md)

Applies to:
**Windows 10/11**

## Week of September 26, 2022

### Monitor and troubleshoot

#### Open Help and Support without losing your context in the Microsoft Intune admin center<!-- 12469338 -->  
You can now use the `?` icon in the Microsoft Intune admin center to open a [help and support](../../get-support.md) session without losing your current node of focus in the admin center. The `?` icon is always available in the upper right of the title bar of the admin center. This change adds another way to access *Help and support*.

When you select `?`, the admin center opens the help and support view in a new and separate side-by-side pane. By opening this separate pane, you're free to navigate the support experience without affecting your original location and focus on the admin center.

## Week of September 19, 2022 (Service release 2209)

### App management

#### New app types for Microsoft Intune<!-- 7210233 -->
As an admin, you can create and assign two new types of Intune apps:
- **iOS/iPadOS web clip** 
- **Windows web link**

These new app types work in a similar way to the existing **web link** application type, however they apply only for their specific platform, whereas web link applications apply across all platforms. With these new app types, you can assign to groups and also use assignment filters to limit the scope of assignment. This functionality is in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apps** > **All Apps** > **Create**.

### Device management

#### Microsoft Intune is ending support for Windows 8.1<!-- 14740233 -->
Microsoft Intune is ending support on October 21, 2022 for devices running Windows 8.1. After that date, technical assistance and automatic updates that help protect your devices running Windows 8.1 will no longer be available. Also, because the sideloading scenario for line-of-business apps is only applicable to Windows 8.1 devices, Intune no longer supports Windows 8.1 sideloading. Sideloading is installing, and then running or testing an app that isn't cerified by the Microsoft Store. In Windows 10/11, "sideloading" is simply setting a device config policy to include "Trusted app installation". 

#### Group member count visible in assignments<!-- 13434676 -->
When assigning policies in the admin center, you can now see the number of users and devices in a group. Having both counts help you pinpoint the right group and understand the impact the assignment has before you apply it.

### Device configuration

#### New lock screen message when adding custom support information to Android Enterprise devices<!-- 13158348 -->
On Android Enterprise devices, you can create a device restrictions configuration profile that shows a custom support message on the devices (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** > **Fully managed, dedicated, and corporate-owned work profile** for platform > **Device restrictions** for profile type > **Custom support information**).

There's a new setting you can configure:
- **Lock screen message**: Add a message that's shown on the device lock screen. 

When you configure the **Lock screen message**, you can also use the following device tokens to show device-specific information:
- `{{AADDeviceId}}`: Microsoft Entra device ID
- `{{AccountId}}`: Intune tenant ID or account ID
- `{{DeviceId}}`: Intune device ID
- `{{DeviceName}}`: Intune device name
- `{{domain}}`: Domain name
- `{{EASID}}`: Exchange Active Sync ID
- `{{IMEI}}`: IMEI of the device
- `{{mail}}`: Email address of the user
- `{{MEID}}`: MEID of the device
- `{{partialUPN}}`: UPN prefix before the `@` symbol
- `{{SerialNumber}}`: Device serial number
- `{{SerialNumberLast4Digits}}`: Last four digits of the device serial number
- `{{UserId}}`: Intune user ID
- `{{UserName}}`: User name
- `{{userPrincipalName}}`: UPN of the user

> [!NOTE]
> Variables aren't validated in the UI and are case sensitive. As a result, you might see profiles saved with incorrect input. For example, if you enter `{{DeviceID}}`, instead of `{{deviceid}}` or `{{DEVICEID}}`, then the literal string is shown instead of the device's unique ID. Be sure to enter the correct information. All lowercase or all uppercase variables are supported, but not a mix.

For more information on this setting, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md#custom-support-information).

Applies to:
- Android 7.0 and newer
- Android Enterprise corporate owned fully managed
- Android Enterprise corporate owned dedicated devices
- Android Enterprise corporate owned work profile

#### Filter on the user scope or device scope in the settings catalog for Windows devices<!-- 13949975 -->
When you create a settings catalog policy, you can use **Add settings** > **Add filter** to filter settings based on the Windows OS edition (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type).

When you **Add filter**, you can also filter on the settings by user scope or device scope.

For more information on the settings catalog, go to [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

Applies to:
- Windows 10
- Windows 11

#### Android Open Source Project (AOSP) platform is generally available<!-- 15027949 -->
Microsoft Intune management of corporate-owned devices that run on the Android Open Source Project (AOSP) platform is now generally available (GA). This feature includes the full suite of capabilities that are available as part of the public preview.

Currently, Microsoft Intune only supports the new Android (AOSP) management option for RealWear devices.
- [Deployment guide: Manage Android devices in Microsoft Intune](deployment-guide-platform-android.md)
- [Deployment guide: Enroll Android devices in Microsoft Intune](deployment-guide-enrollment-android.md)

Applies to:
- Android Open Source Project (AOSP)

#### Device Firmware Configuration Interface (DFCI) now supports Acer devices<!-- 15240661 -->
For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type).

New Acer devices running Windows 10/11 will be enabled for DFCI in later 2022. So, admins can create DFCI profiles to manage the BIOS and then deploy the profiles to these Acer devices.

Contact your device vendor or device manufacturer to ensure you get eligible devices.

For more information about DFCI profiles in Intune, go to [Use Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md).

Applies to:
- Windows 10
- Windows 11

#### New settings available in the iOS/iPadOS and macOS settings catalog<!-- 15349701 -->
The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. 

There are new settings available in the settings catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Accounts > LDAP**:

- LDAP Account Description
- LDAP Account Host Name
- LDAP Account Password
- LDAP Account Use SSL
- LDAP Account User Name
- LDAP Search Settings

Applies to:
- iOS/iPadOS
- macOS

The following settings are also in settings catalog. Previously, they were only available in Templates:

**Privacy > Privacy Preferences Policy Control**:

- Accessibility
- Address Book
- Apple Events
- Calendar
- Camera
- File Provider Presence
- Listen Event
- Media Library
- Microphone
- Photos
- Post Event
- Reminders
- Screen Capture
- Speech Recognition
- System Policy All Files
- System Policy Desktop Folder
- System Policy Documents Folder
- System Policy Downloads Folder
- System Policy Network Volumes
- System Policy Removable Volumes
- System Policy Sys Admin Files

Applies to:

- macOS

For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Device enrollment

#### Set up enrollment notifications (public preview)<!-- 9283605 -->
Enrollment notifications inform device users, via email or push notification, when a new device has been enrolled in Microsoft Intune. You can use enrollment notifications for security purposes. They can notify users and help them report devices enrolled in error, or for communicating to employees during the hiring or onboarding process. Enrollment notifications are available to try now in public preview for Windows, Apple, and Android devices. This feature is only supported with user-driven enrollment methods.

### Device security

#### Assign compliance policies to the All devices group<!-- 2213410 -->
The **All devices** option is now available for [compliance policy](../protect/create-compliance-policy.md) assignments. With this option, you can assign a compliance policy to all enrolled devices in your organization that match the policy's platform. You don't need to create a Microsoft Entra group that contains all devices.

When you include the *All devices* group, you can then exclude individual groups of devices to further refine the assignment scope.

#### Trend Micro – New mobile threat defense partner<!-- 11017779 -->
You can now use [Trend Micro Mobile Security as a Service](../protect/trend-micro-mobile-threat-defense-connector.md) as an integrated mobile threat defense (MTD) partner with Intune. By configuring the Trend MTD connector in Intune, you can control mobile device access to corporate resources using Conditional Access that's based on risk assessment.
 
For more information, see:
- [Mobile threat defense integration with Intune](../protect/mobile-threat-defense.md)

<!-- - [Trend Micro Mobile Security documentation](https://docs.trendmicro.com/en-us/enterprise/trend-micro-vision-one/mobile-security/getting-started-with_003.aspx) -->

#### Grace period status visible on Intune Company Portal website<!-- 15025900 -->
The Intune Company Portal website now shows a grace period status to account for devices that don't meet compliance requirements but are still within their given grace period. Users are shown the date by which they need to become compliant and the instructions for how to become compliant. If they don't update their device by the given date, their status changes to noncompliant. For more information about setting grace periods, see [Configure compliance policies with actions for noncompliance](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance).

### Intune apps

#### Newly available protected apps for Intune<!-- 15007580, 15235927 -->
The following protected apps are now available for Microsoft Intune:
- RingCentral for Intune by RingCentral, Inc.
- MangoApps, Work from Anywhere by MangoSpring, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of September 12, 2022

### Device management

#### Intune now requires iOS/iPadOS 14 and higher<!-- 14778947 -->
With Apple's release of iOS/iPadOS 16, Microsoft Intune and the Intune Company Portal will now require iOS/iPadOS 14 and higher. For more information, see [Supported operating systems and browsers in Intune](supported-devices-browsers.md).

#### Intune now requires macOS 11.6 and higher<!-- 14766663 -->
With Apple's release of macOS 13 Ventura, Microsoft Intune, the Company Portal app, and the Intune MDM agent will now require macOS 11.6 (Big Sur) and later. For more information, see [Supported operating systems and browsers in Intune](supported-devices-browsers.md).

## Week of September 05, 2022

### Device management

#### Remote Help version: 4.0.1.13 release<!-- 15329690 -->

With Remote Help 4.0.1.13, fixes were introduced to address an issue that prevented people from having multiple sessions open at the same time. The fixes also addressed an issue where the app was launching without focus, and prevented keyboard navigation and screen readers from working on launch.

For more information, go to [Use Remote Help with Intune and Microsoft Intune](remote-help.md).

## Week of August 29, 2022

### App management

#### Updated Microsoft Intune App SDK for Android<!-- 15363982 -->
The developer guide for the Intune App SDK for Android has been updated. The updated guide provides the following stages:
- Planning the integration
- MSAL prerequisite
- Getting started with MAM
- MAM integration essentials
- Multi-Identity
- App configuration
- App participation features

For more information, see [Intune App SDK for Android](../developer/app-sdk-android-phase1.md).

## Week of August 22, 2022

### Device management

#### Use Intune role-based access control (RBAC) for tenant attached devices <!-- 14996522 -->

You can now use Intune role-based access control (RBAC) when interacting with tenant attached devices from the Microsoft Intune admin center. For example, when using Intune as the role-based access control authority, a user with Intune's [Help Desk Operator role](role-based-access-control.md#built-in-roles) doesn't need an assigned security role or other permissions from Configuration Manager. For more information, see [Intune role-based access control for tenant attached clients](../../configmgr/cloud-attach/use-intune-rbac.md).

## Week of August 15, 2022 (Service release 2208)

### App management

#### Android strong biometric change detection<!-- 9740832 -->
The Android **Fingerprint instead of PIN for access** setting in Intune, which allows the end-user to use [fingerprint authentication](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication) instead of a PIN, is being modified. This change allows you to require end-users to set strong biometrics. And, if a change in strong biometrics is detected, you can require end-users to confirm their app protection policy (APP) PIN. You can find Android app protection policies in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **App protection policies** > **Create policy** > **Android**. For more information, see [Android app protection policy settings in Microsoft Intune](../apps/app-protection-policy-settings-android.md#access-requirements).

#### Noncompliance details available for Android (AOSP) in Microsoft Intune app<!-- 12645770 -->
Android (AOSP) users can view noncompliance reasons in the Microsoft Intune app. These details describe why a device is marked noncompliant. This information is available on the Device details page for devices enrolled as user-associated Android (AOSP) devices.

### Intune apps

#### Newly available protected apps for Intune<!-- 14709109, 14955442, 14981985 -->
The following protected apps are now available for Microsoft Intune:
- Nexis Newsdesk Mobile by LexisNexis
- My Portal by MangoApps (Android)
- Re:Work Enterprise by 9Folders, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Device enrollment

#### Configure zero-touch enrollment from Microsoft Intune admin center<!-- 1872357 -->
Now you can configure Android zero-touch enrollment from the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). This feature lets you link your zero-touch account to Intune, add support information, configure zero-touch enabled devices, and customize provisioning extras. For more information about how to enable zero-touch from the admin center, see [Enroll by using Google Zero Touch](../enrollment/android-dedicated-devices-fully-managed-enroll.md#enroll-by-using-google-zero-touch).  

### Device management

#### Custom settings for Windows 10/11 device compliance is now generally available<!-- 12862904 -->

Support for the following custom features is generally available:

- [Create custom compliance policy settings](../protect/compliance-use-custom-settings.md) for Windows devices using PowerShell scripts.
- Create custom compliance rules and remediation messages that appear in the Company Portal app.

Applies to:  
- Windows 10/11

#### View contents of macOS shell scripts and custom attributes<!-- 14757037 -->
You can view the contents of macOS shell scripts and custom attributes after you upload the scripts to Intune. You can view Shell scripts and custom attributes in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **By platform** > **macOS**. For more information, see [Use shell scripts on macOS devices in Intune](../apps/macos-shell-scripts.md).

#### Reset passcode remote action available for Android (AOSP) Corporate devices<!-- 10247332 -->
You can use Reset passcode remote action from the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) for Android Open Source Project (AOSP) Corporate devices.

For information on remote actions, see:
- [Reset or remove a device passcode in Intune](../remote-actions/device-passcode-reset.md)
- [Remotely restart devices with Intune](../remote-actions/device-restart.md)
- [Remotely lock devices with Intune](../remote-actions/device-remote-lock.md)

Applies to:
- Android Open Source Project (AOSP)

### Device configuration

#### Certificate profiles support for Android (AOSP) devices<!-- 8506336 -->
You can now use Simple Certificate Enrollment Protocol (SCEP) [certificate profiles](../protect/certificates-configure.md) with corporate-owned and userless devices that run the Android Open Source Project (AOSP) platform.

#### Import, create, and manage custom ADMX and ADML administrative templates<!-- 4970862 -->
You can create a device configuration policy that uses built-in ADMX templates. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Administrative templates**.

You can also import custom and third party/partner ADMX and ADML templates into the Intune admin center. Once imported, you can create a device configuration policy, assign the policy to your devices, and manage the settings in the policy.

For information, go to:
- [Import custom ADMX and ADML administrative templates into Intune](../configuration/administrative-templates-import-custom.md)
- [Overview: Use Windows 10/11 templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md).

Applies to:
- Windows 11
- Windows 10

#### Add an HTTP proxy to Wi-Fi device configuration profiles on Android Enterprise<!-- 13975609 -->
On Android Enterprise devices, you can create a Wi-Fi device configuration profile with basic and enterprise settings. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** for platform > **Wi-Fi**.

When you create the profile, you can configure an HTTP proxy using a PAC file or configure the settings manually. You can configure an HTTP proxy for each Wi-Fi network in your organization.

When the profile is ready, you can deploy this profile to your Fully Managed, Dedicated, and Corporate-Owned Work Profile devices. 

For more information on the Wi-Fi settings you can configure, go to [Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices in Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md).

Applies to:
- Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile

#### iOS/iPadOS settings catalog supports declarative device management (DDM)<!-- 15016105 -->
On iOS/iPadOS 15+ devices enrolled using [User Enrollment](../enrollment/apple-user-enrollment-with-company-portal.md), the settings catalog automatically uses Apple's declarative device management (DDM) when configuring settings.
- No action is required to use DDM. The feature is built into the settings catalog.
- There's no impact to existing policies in the settings catalog.
- iOS/iPadOS devices that aren't enabled for DDM continue to use Apple's standard MDM protocol.

For more information, go to:
- [Meet declarative device management](https://aka.ms/DDM2021) (opens Apple's web site)
- [Microsoft simplifies Intune enrollment for Apple updates](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/microsoft-simplifies-endpoint-manager-enrollment-for-apple/ba-p/3570319)
- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md)

Applies to:
-  iOS/iPadOS 15 or later devices enrolled using Apple User Enrollment

#### New macOS settings available in the settings catalog <!-- 15020250 -->
The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. New settings are available in the settings catalog. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Microsoft Auto Update**:

- Current Channel
- Number of minutes for the final countdown timer

**Restrictions**:

- Allow Universal Control

The following settings are also in settings catalog. Previously, they were only available in Templates:

**Authentication > Extensible Single Sign On**:

- Extension Data
- Extension Identifier
- Hosts
- Realm
- Screen Locked Behavior
- Team Identifier
- Type
- URLs

**Authentication > Extensible Single Sign On > Extensible Single Sign On Kerberos**:

- Extension Data
- Allow Automatic Login
- Allow Password Change
- Credential Bundle ID ACL
- Credential Use Mode
- Custom Username Label
- Delay User Setup
- Domain Realm Mapping
- Help Text
- Include Kerberos Apps In Bundle ID ACL
- Include Managed Apps In Bundle ID ACL
- Is Default Realm
- Monitor Credentials Cache
- Perform Kerberos Only
- Preferred KDCs
- Principal Name
- Password Change URL
- Password Notification Days
- Password Req Complexity
- Password Req History
- Password Req Length
- Password Req Min Age
- Password Req Text
- Require TLS For LDAP
- Require User Presence
- Site Code
- Sync Local Password
- Use Site Auto Discovery
- Extension Identifier
- Hosts
- Realm
- Team Identifier
- Type

For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:
- macOS

#### New iOS/iPadOS settings in the settings catalog<!-- 15020319 -->
The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. There are new iOS/iPadOS settings available in the settings catalog. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** for platform > **Settings catalog** for profile type. Previously, these settings were only available in Templates:

**Authentication > Extensible Single Sign On**:

- Extension Data
- Extension Identifier
- Hosts
- Realm
- Screen Locked Behavior
- Team Identifier
- Type
- URLs

**Authentication > Extensible Single Sign On > Extensible Single Sign On Kerberos**:

- Extension Data
- Allow Automatic Login
- Credential Bundle ID ACL
- Domain Realm Mapping
- Help Text
- Include Managed Apps In Bundle ID ACL
- Is Default Realm
- Preferred KDCs
- Principal Name
- Require User Presence
- Site Code
- Use Site Auto Discovery
- Extension Identifier
- Hosts
- Realm
- Team Identifier
- Type

**System Configuration > Lock Screen Message**:
- Asset Tag Information
- Lock Screen Footnote

For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:
- iOS/iPadOS

### Monitor and troubleshoot

#### New noncompliant devices and settings report<!-- 13532817 -->
In **Reports** > **Device Compliance** > **Reports**, there's a new **Noncompliant devices and settings** organization report. This report:
- Lists each noncompliant device.
- For each noncompliant device, it shows the compliance policy settings that the devices aren't compliant with.

For more information on this report, go to [Noncompliant devices and settings report (Organizational)](reports.md#noncompliant-devices-report-organizational).

## Week of August 1, 2022

### Device security

#### Disable use of UDP connections on your Microsoft Tunnel Gateway servers<!-- 9295335 -->

You can now disable the use of UDP by your Microsoft Tunnel Servers. When you disable use of UDP, the VPN server supports only TCP connections from tunnel clients. To support use of only TCP connections, your devices must use the generally available version of [Microsoft Defender for Endpoint as the Microsoft Tunnel client app](../protect/microsoft-tunnel-configure.md) as the tunnel client app.

To disable UDP, [create or edit a *Server configuration* for Microsoft Tunnel Gateway](../protect/microsoft-tunnel-configure.md#create-a-server-configuration) and select the checkbox for the new option named **Disable UDP Connections**.

### App management

#### Company Portal for Windows bulk app install<!-- 6401437 -->
The Company Portal for Windows now allows users to select multiple apps and install in bulk. From the **Apps** tab of the Company Portal for Windows, select the multi-select view button on the top right corner of the page. Then, select the checkbox next to each app that you need to install. Next, select the **Install Selected** button to start installation. All selected apps install at the same time without requiring users to right-click each app or navigate to each app's page. For more information, see [Install and share apps on your device](../user-help/install-apps-cpapp-windows.md) and [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

## Week of July 25, 2022 (Service release 2207)

### Device management

#### Initiate compliance checks for your AOSP devices from the Microsoft Intune app<!--12645739 -->
You can now initiate a compliance check for your AOSP devices from the Microsoft Intune app. Go to **Device details**. This feature is available on devices that are enrolled via the Microsoft Intune app as user-associated (Android) AOSP devices.

#### Monitor bootstrap escrow status on a Mac<!-- 12404441 -->  
Monitor the bootstrap token escrow status for an enrolled Mac in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). A new hardware property in Intune, called *Bootstrap token escrowed*, reports whether or not a bootstrap token has been escrowed in Intune. For more information about bootstrap token support for macOS, see [Bootstrap tokens](../enrollment/macos-enroll.md#bootstrap-tokens).

#### Enable Common Criteria mode for Android Enterprise devices<!-- 13158881 -->
For Android Enterprise devices, you can use a new setting, **Common Criteria mode**, to enable an elevated set of security standards that are typically used by only highly sensitive organizations, such as government establishments.

Applies to:
- Android 5.0 and newer
- Android Enterprise corporate owned fully managed
- Android Enterprise corporate owned dedicated devices
- Android Enterprise corporate owned work profile

The new setting, *Common Criteria mode*, is found in the *System security* category when you configure a [Device restrictions](../configuration/device-restrictions-configure.md) template for the *Android Enterprise - Fully Managed, Dedicated, and Corporate-Owned Work Profile*.
 
Devices that receive a policy with *Common Criteria mode* set to **Require**, elevate security components that include but are not limited to:  
- AES-GCM encryption of Bluetooth Long Term Keys
- Wi-Fi configuration stores
- Blocks bootloader download mode, the manual method for software updates
- Mandates additional key zeroization on key deletion
- Prevents non-authenticated Bluetooth connections
- Requires that FOTA updates have 2048-bit RSA-PSS signature

Learn more about Common Criteria:
- [Common Criteria for Information Technology Security Evaluation](https://www.commoncriteriaportal.org) at commoncriteriaportal.org
- [CommonCriteriaMode](https://developers.google.com/android/management/reference/rest/v1/enterprises.policies#commoncriteriamode) in the Android Management API documentation
- [Knox Deep Dive: Common Criteria Mode](https://www.samsungknox.com/blog/knox-deep-dive-common-criteria-mode) at samsungknox.com

#### New hardware detail available for individual devices running on iOS/iPadOS and macOS<!-- 9598434 -->
In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **All devices** > *select one of your listed devices* and open it's **Hardware** details. The following new detail is available in the **Hardware** pane of individual devices:
 - **Product name**: Shows the product name of the device, such as `iPad8,12`. Available for iOS/iPadOS and macOS devices. 

For more information, see [View device details with Microsoft Intune](../remote-actions/device-inventory.md).

Applies to:
- iOS/iPadOS, macOS

#### Remote Help Version: 4.0.1.12 release<!-- 14999203 -->
With Remote Help 4.0.1.12, various fixes were introduced to address the 'Try again later' message that appears when not authenticated. The fixes also include an improved auto-update capability. 

For more information, see [Use Remote Help with Intune](remote-help.md).

### Device enrollment

#### Intune supports sign-in from another device during iOS/iPadOS and macOS Setup Assistant with modern authentication<!-- 12377183 -->  
Users going through automated device enrollment (ADE) can now authenticate by signing in from another device. This option is available for iOS/iPadOS and macOS devices enrolling via Setup Assistant with modern authentication. The screen that prompts device users to sign in from another device is embedded into Setup Assistant and shown to them during enrollment. For more information about the sign-in process for users, see [Get the Intune Company Portal app (../user-help/sign-in-to-the-company-portal.md#sign-in-via-another-device).  

#### Detect and manage hardware changes on Windows Autopilot devices<!-- 12795465 --> 
Microsoft Intune will now alert you when it detects a hardware change on an Autopilot-registered device. You can view and manage all affected devices in the admin center. Also, you can remove the affected device from Windows Autopilot and register it again so that the hardware change is accounted for.

### Device configuration

#### New macOS Microsoft AutoUpdate (MAU) settings in the settings catalog<!-- 14873468 -->
The settings catalog supports settings for Microsoft AutoUpdate (MAU) (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type).

The following settings are now available:

**Microsoft Auto Update**:

- Automatically acknowledge data collection policy
- Days before forced updates
- Deferred updates
- Disable Office Insider membership
- Enable AutoUpdate
- Enable check for updates
- Enable extended logging
- Register app on launch
- Update cache server
- Update channel
- Update check frequency (mins)
- Updater optimization technique

The settings can be used to configure preferences for the following applications:

- Company Portal
- Microsoft Auto Update
- Microsoft Defender
- Microsoft Defender ATP
- Microsoft Edge
- Microsoft Edge Beta
- Microsoft Edge Canary
- Microsoft Edge Dev
- Microsoft Excel
- Microsoft OneNote
- Microsoft Outlook
- Microsoft PowerPoint
- Microsoft Remote Desktop
- Microsoft Teams
- Microsoft Word
- OneDrive
- Skype for Business

For more information about the settings catalog, go to:
- [Tasks you can complete using the Settings Catalog in Intune](../configuration/settings-catalog-common-features.md)
- [Create a policy using settings catalog in Microsoft Intune](../configuration/settings-catalog.md)

For more information about Microsoft AutoUpdate settings you can configure, go to:
- [Use preferences to manage privacy controls for Office for Mac - Deploy Office](/deployoffice/privacy/mac-privacy-preferences#preference-setting-for-connected-experiences-that-download-online-content).
- [Set a deadline for updates from Microsoft AutoUpdate](/deployoffice/mac/mau-deadline)

Applies to:
- macOS

#### New iOS/iPadOS settings in the settings catalog<!-- 14875716 -->
The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. There are new iOS/iPadOS settings available in the settings catalog (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** for platform > **Settings catalog** for profile type).

New settings include:

**Networking > Cellular**:
- Allowed Protocol Mask
- Allowed Protocol Mask In Domestic Roaming
- Allowed Protocol Mask In Roaming
- Authentication Type
- Name
- Password
- Proxy Port
- Proxy Server
- Username

The following settings are also in settings catalog. Previously, they were only available in Templates:

**User experience > Notifications**:
- Grouping type
- Preview type
- Show In Car Play

**Printing > Air Print**:
- Force TLS
- Port

**App Management > App Lock**:
- Disable Auto Lock
- Disable Device Rotation
- Disable Ringer Switch
- Disable Sleep Wake Button
- Disable Touch
- Disable Volume Buttons
- Enable Assistive Touch
- Enable Invert Colors
- Enable Mono Audio
- Enable Speak Selection
- Enable Voice Control
- Enable Voice Over
- Enable Zoom
- Assistive Touch
- Invert Colors
- Voice Control
- Voice Over
- Zoom

**Networking > Domains**:
- Safari Password Auto Fill Domain

**Networking > Network Usage Rules**:
- Application Rules
- Allow Cellular Data
- Allow Roaming Cellular Data
- App Identifier Matches

**Restrictions**:
- Allow Account Modification
- Allow Activity Continuation
- Allow Adding Game Center Friends
- Allow Air Drop
- Allow Air Print
- Allow Air Print Credentials Storage
- Allow Air Print iBeacon Discovery
- Allow App Cellular Data Modification
- Allow App Clips
- Allow App Installation
- Allow App Removal
- Allow Apple Personalized Advertising
- Allow Assistant
- Allow Assistant User Generated Content
- Allow Assistant While Locked
- Allow Auto Correction
- Allow Auto Unlock
- Allow Automatic App Downloads
- Allow Bluetooth Modification
- Allow Bookstore
- Allow Bookstore Erotica
- Allow Camera
- Allow Cellular Plan Modification
- Allow Chat
- Allow Cloud Backup
- Allow Cloud Document Sync
- Allow Cloud Keychain Sync
- Allow Cloud Photo Library
- Allow Cloud Private Relay
- Allow Continuous Path Keyboard
- Allow Definition Lookup
- Allow Device Name Modification
- Allow Diagnostic Submission
- Allow Diagnostic Submission Modification
- Allow Dictation
- Allow Enabling Restrictions
- Allow Enterprise App Trust
- Allow Enterprise Book Backup
- Allow Enterprise Book Metadata Sync
- Allow Erase Content And Settings
- Allow ESIM Modification
- Allow Explicit Content
- Allow Files Network Drive Access
- Allow Files USB Drive Access
- Allow Find My Device
- Allow Find My Friends
- Allow Find My Friends Modification
- Allow Fingerprint For Unlock
- Allow Fingerprint Modification
- Allow Game Center
- Allow Global Background Fetch When Roaming
- Allow Host Pairing
- Allow In App Purchases
- Allow iTunes
- Allow Keyboard Shortcuts
- Allow Listed App Bundle IDs
- Allow Lock Screen Control Center
- Allow Lock Screen Notifications View
- Allow Lock Screen Today View
- Allow Mail Privacy Protection
- Allow Managed Apps Cloud Sync
- Allow Managed To Write Unmanaged Contacts
- Allow Multiplayer Gaming
- Allow Music Service
- Allow News
- Allow NFC
- Allow Notifications Modification
- Allow Open From Managed To Unmanaged
- Allow Open From Unmanaged To Managed
- Allow OTAPKI Updates
- Allow Paired Watch
- Allow Passbook While Locked
- Allow Passcode Modification
- Allow Password Auto Fill
- Allow Password Proximity Requests
- Allow Password Sharing
- Allow Personal Hotspot Modification
- Allow Photo Stream
- Allow Podcasts
- Allow Predictive Keyboard
- Allow Proximity Setup To New Device
- Allow Radio Service
- Allow Remote Screen Observation
- Allow Safari
- Allow Screenshot
- Allow Shared Device Temporary Session
- Allow Shared Stream
- Allow Spell Check
- Allow Spotlight Internet Results
- Allow System App Removal
- Allow UI App Installation
- Allow UI Configuration Profile Installation
- Allow Unmanaged To Read Managed Contacts
- Allow Unpaired External Boot To Recovery
- Allow Untrusted TLS Prompt
- Allow USB Restricted Mode
- Allow Video Conferencing
- Allow Voice Dialing
- Allow VPN Creation
- Allow Wallpaper Modification
- Autonomous Single App Mode Permitted App IDs
- Blocked App Bundle IDs
- Enforced Software Update Delay
- Force Air Drop Unmanaged
- Force Air Play Outgoing Requests Pairing Password
- Force Air Print Trusted TLS Requirement
- Force Assistant Profanity Filter
- Force Authentication Before Auto Fill
- Force Automatic Date And Time
- Force Classroom Automatically Join Classes
- Force Classroom Request Permission To Leave Classes
- Force Classroom Unprompted App And Device Lock
- Force Delayed Software Updates
- Force Encrypted Backup
- Force iTunes Store Password Entry
- Force Limit Ad Tracking
- Force On Device Only Dictation
- Force On Device Only Translation
- Force Watch Wrist Detection
- Force WiFi Power On
- Force WiFi To Allowed Networks Only
- Require Managed Pasteboard
- Safari Accept Cookies
- Safari Allow Autofill
- Safari Allow JavaScript
- Safari Allow Popups
- Safari Force Fraud Warning

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:
- iOS/iPadOS

#### New macOS settings available in the settings catalog<!-- 14875745 -->
The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. New settings are available in the settings catalog (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type).

New settings include:

**System configuration > System extensions**:

- Removable System Extensions

The following settings are also in settings catalog. Previously, they were only available in Templates:

**System configuration > System extensions**:
- Allow User Overrides
- Allowed System Extension Types
- Allowed System Extensions
- Allowed Team Identifiers

For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:
- macOS

#### New search feature in Preview devices when creating a filter<!-- 14921046 -->
In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can create filters, and then use these filters when assigning apps and policies (**Devices** > **Organize devices** > **Filters** > **Create**).

When you create a filter, you can select **Preview devices** to see a list of enrolled devices that match your filter criteria. In **Preview devices**, you can also search through the list using the device name, OS version, device model, device manufacturer, user principal name of the primary user, and device ID.

For more information on filters, go to [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md).

## Week of July 18, 2022

### Device management

#### New event viewers to help debug WMI issues<!-- 14712854  -->
Intune's remote action to [collect diagnostics](../remote-actions/collect-diagnostics.md#collect-diagnostics) has been expanded to collect details about Windows Management Instrumentation (WMI) app issues.

The new event viewers include:

- Microsoft-Windows-WMI-Activity/Operational
- Microsoft-Windows-WinRM/Operational

For more information about Windows device diagnostics, see [Collect diagnostics from a Windows device](../remote-actions/collect-diagnostics.md).

## Week of July 4, 2022

### Device management

#### Endpoint analytics scores per device model<!-- 14439211 -->

Endpoint analytics now displays [scores by device model](../../analytics/scores.md#bkmk_model). These scores help admins contextualize the user experience across device models in the environment. Scores per model and per device are available in all Endpoint analytics reports, including the [Work from anywhere](../../analytics/work-from-anywhere.md) report.

### Monitor and troubleshoot

#### Use Collect diagnostics to collect details about Windows expedited updates<!--  14337387 -->

Intune's remote action to [Collect diagnostics](../remote-actions/collect-diagnostics.md) now collects more details about [Windows expedited updates](../protect/windows-10-expedite-updates.md) that you deploy to devices. This information can be of use when troubleshooting problems with expedited updates.

The new details that are collected include:  
- Files: `C:\Program Files\Microsoft Update Health Tools\Logs\*.etl`
- Registry Keys: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CloudManagedUpdate`
