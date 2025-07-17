---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: laurawi
ms.author: brenduns
manager: laurawi
ms.date: 06/27/2025
ms.topic: article
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
- When a feature enters production, whether it's in preview or generally available, the feature description moves from this article to [What's new](whats-new.md).
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

## Microsoft Intune Suite

###  Endpoint Privilege Management Dashboard for user readiness and elevation trends<!-- 26123334  -->

We’re working on a dashboard for Endpoint Privilege Management (EPM) that will bring you insights to support having your users run as standard users in place of running with local admin permissions. First, the dashboard will report progress towards a Standard User Status to help you understand when your admin users might be ready to be moved to standard users. The dashboard will also help you understand the file elevation trends in your organization.

### Endpoint Privileged Management support on Azure Virtual Desktop<!-- 26079227 -->

We're adding support to deploy Endpoint Privilege Management (EPM) policies to users on Azure Virtual Desktop (AVD) single-session virtual machines. With this support EPM elevation policies will work on AVD single-session environments.

For more information about EPM, which is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md), see [Endpoint Privilege Management overview](../protect/epm-overview.md).


### Endpoint Privilege Management support for wildcards in elevation rules<!-- 30290730 -->

Endpoint Privilege Management (EPM) will soon support the use of wildcards when defining elevation rules. Wildcards allow for more flexible rule creation with broader matching capabilities, enabling file elevations for trusted files that have names that might change with subsequent revisions.
 
For example, you'll be able to create a rule for a Visual Studio setup file called *VSCodeUserSetup-arm64-1.99.2.exe* using wildcards to accommodate future revisions. Several wildcard forms can be used, including `VSCodeUserSetup*`, `VSCodeUserSetup-arm64-*`, or `VSCodeUserSetup-?????-1.??.?.exe`, where an asterisk represents a string, and question marks represent single characters.


<!-- ***********************************************-->

## App management

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies will soon provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### New settings available in the Apple settings catalog <!-- 33064192 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

#### iOS/iPadOS

**Cellular Private Network**:

- Cellular Data Preferred
- CSG Network Identifier
- Data Set Name
- Enable NR Standalone
- Geofences
- Network Identifier
- Version Number

#### macOS

**Authentication > Extensible Single Sign On Kerberos**:

- Allow Platform SSO Auth Fallback

**Microsoft Edge**:

- The Microsoft Edge category is updated with new settings. Learn more about available macOS Edge settings at [Microsoft Edge - Policies](/deployedge/microsoft-edge-policies).


<!-- *********************************************** -->

<!-- ## Device enrollment -->

<!-- *********************************************** -->

## Device management

### New Microsoft Graph permissions for API calls to device management endpoints<!-- 20952394 -->

On July 31, 2025, calls to several Microsoft Graph APIs will require one of two newly added *DeviceManagement* permissions that replace existing permissions. With this change, the older permissions will no longer function and API calls from tools and scripts that use the older permissions will fail.

The following are the Microsoft Graph API calls that are affected:

- ~/deviceManagement/deviceShellScripts
- ~/deviceManagement/deviceHealthScripts
- ~/deviceManagement/deviceComplianceScripts
- ~/deviceManagement/deviceCustomAttributeShellScripts 
- ~/deviceManagement/deviceManagementScripts 

The following are the new permissions that will soon be required, and the old permissions that will no longer function:
- **DeviceManagementScripts.Read.All** - This new permission replaces use of *DeviceManagementConfiguration.Read.All*

- **DeviceManagementScripts.ReadWrite.All** - This new permission replaces use of the *DeviceManagementConfiguration.ReadWrite.All*

Until July 31, 2025, both the *DeviceManagementScripts* and the older *DeviceManagementConfiguration* permissions will work. However, to ensure your tools and scripts continue to function, review and update them to use only the newer permissions before July 31, 2025.

For more information, see [Graph APIs used to configure devices](../developer/graph-apis-used-by-intune-device-configuration-windows.md).

### Remote actions with multiple administrative approval<!-- 27043113  -->

Intune *access policies* help protect against a compromised administrative account by requiring that a second administrative account is used to approve a change before the change is applied. This capability is known as multiple administrative approval (MAA). The remote action **Wipe** will support MAA. Onboarding Remote device actions to MAA will help mitigate the risk of unauthorized or compromised remote actions being taken on devices by a single administrative account thereby enhancing the overall security posture of the environment.

For more information on multiple administrative approval, see [Use multiple administrative approvals in Intune](../fundamentals/multi-admin-approval.md).

### Introducing platform level targeting of Device Cleanup rule<!-- 13835920 -->

We're adding a feature that allows a customer to:

- Configure one device cleanup rule per platform (Windows, iOS/macOS, iPadOS, Android, Linux)
- Configure a different RBAC permission and assign the permission to different RBAC roles

Platform level targeting of the Device Cleanup rule helps administrators to remove stale and inactive devices from their tenant based on the active days rule specified by the admin. Scoped and targeted Device cleanup rules add an intermediate stage where an admin will be able to target removing stale devices by having a rule configured at the platform or OS level.

For more information, see [device cleanup rules](../remote-actions/devices-wipe.md#automatically-hide-devices-with-cleanup-rules).

<!-- *********************************************** -->

## Device security

### macOS support for local administrator account configuration LAPS and password solution<!-- 25385731 -->

We’re working on adding Intune support for macOS local administrator account configuration during ADE (automated device enrollment) enrollment, and macOS support for Microsoft Local Admin Password Solution (LAPS).

With the local admin account configuration support:  
- You’ll be able to use macOS automated device enrollment (ADE) profiles to configure the local and standard administrator accounts for a device. When configured, this capability applies to all new macOS device enrollments as well as device re-enrollments.
- Intune automatically creates a randomized, unique, and secure password for the device’s admin account. That password is then automatically rotated every six months.
- Previously enrolled devices won’t be affected unless or until they re-enroll with Intune if these settings are configured.
- The following variables will be supported for the fullname and username account settings:  
  - {{username}}
  - {{serialNumber}}
  - {{partialupn}}
  - {{managedDeviceName}}

With the LAPS support:  
- For custom RBAC roles: Permissions to view and manage the admin password will require an admin be assigned new Intune role-based access control permissions for Enrollment program.
- Admins with sufficient permissions will be able to view and manually rotate the password of devices that enrolled with the local admin account configuration through macOS ADE.

Applies to:

- macOS

For more information about this support for macOS, see the following in the Apple developer documentation:
- [Account Configuration | Apple Developer Documentation](https://developer.apple.com/documentation/devicemanagement/account_configuration)
- [Set the Local Administrator Password | Apple Developer Documentation](https://developer.apple.com/documentation/devicemanagement/set_the_local_administrator_password)

### Support for Intune Device control policy for devices managed by Microsoft Defender for Endpoint<!-- 15466620 -->

You'll be able to use the endpoint security policy for *Device control* (Attack surface reduction policy) from the Microsoft Intune with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Device control** policies are part of endpoint security [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

Applies to the following when you use the *Windows* platform:

- Windows 10
- Windows 11

When this change takes effect, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive this policy will get it.

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

## Monitor and troubleshoot

### Declarative Apple software update operational report<!-- 25207078 -->

You'll soon be able to view near real time, rich reporting for operating system updates on Apple devices using the new per-device Apple software updates report:

- Pending OS update information such as OS and build version, and its status on the device
- Current OS information for a device, including Rapid Security Responses
- Install reasons that describe how an update was triggered, for example, by the user or enforced through DDM
- Information about the latest public update made available by Apple
 
This new report will be available through the *Devices* > Select a device > *Monitor* node of the admin center.
 
Applies to:
 
- iOS/iPadOS
- macOS

### Declarative Apple software update reports<!-- 31557946 -->

You'll soon be able to view near real time, rich reporting for operating system updates on Apple devices using new Apple software update reports:

 - *Apple software update failures report* - With this report you’ll be able to view details about update failures including why the update failed, how many times it has failed, and the timestamp of the last failure.
- *Apple software updates report* - View details about pending and current software update information across your entire device fleet.
- *Apple software update summary report* - View a summary of the update installation status for each OS.

The Apple software update failure report will be available through the *Devices* > *Monitor* node of the admin center. The Apple software updates report and summary report will be available through the *Reports* > *Apple updates* node of the admin center.

Applies to:

- iOS/iPadOS
- macOS

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
