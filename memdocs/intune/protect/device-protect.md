---
# required metadata

title: Protect devices with Microsoft Intune 
titleSuffix: Microsoft Intune
description: Learn about the Intune capabilities that can help you protect your devices and data against unauthorized access and other threats.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/23/2024
ms.topic: overview
ms.subservice: protect
ms.service: microsoft-intune
ms.localizationpriority: high
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier2
- M365-identity-device-management
- sub-secure-endpoints
---

# Protect data and devices with Microsoft Intune

Microsoft Intune can help you keep your managed devices secure and up to date while helping you to protect your organization's data from compromised devices. Data protection includes controlling what users do with an organization's data on both managed and unmanaged devices. Data protection also extends to blocking access to data from devices that might be compromised.

This article highlights many of Intune's built-in capabilities and partner technologies you can integrate with Intune. As you learn more about them, you can bring several together for more comprehensive solutions on your journey towards a zero-trust environment.

From the Microsoft Intune admin center, Intune [supports managed devices](../fundamentals/supported-devices-browsers.md#intune-supported-operating-systems) that run Android, iOS/iPad, Linux, macOS, and Windows.

When you use Configuration Manager to manage on-premises devices, you can extend Intune policies to those devices by configuring [tenant attach](../protect/tenant-attach-intune.md) or [co-management](../../configmgr/comanage/overview.md).

Intune can also work with information from devices that you manage with third-party products that provide device compliance and mobile threat protection.

## Protect devices through policies

Deploy Intune's *endpoint security*, *device configuration*, and *device compliance* policies to configure devices to meet your organizations security goals. Policies support one or more profiles, which are the discrete sets of platform-specific rules you deploy to groups of enrolled devices.

- With [endpoint security policies](../protect/endpoint-security.md), deploy security focused policies that are designed to help you focus on the security of your devices and mitigate risk. The available tasks can help you identify at-risk devices, to remediate those devices, and restore them to a compliant or more secure state.

- With [device configuration policies](../configuration/device-profiles.md), manage profiles that define the settings and features that devices use in your organization. Configure devices for endpoint protection, provision certificates for authentication, set software update behaviors, and more.

- With [device compliance policies](../protect/device-compliance-get-started.md), you create profiles for different device platforms that establish device requirements. Requirements can include operating system versions, the use of disk encryption, or being at or under specific *threat levels* as defined by threat management software.

  Intune can safeguard devices that aren't compliant with your policies and alert the device user so they can bring the device into compliance.

  When you add [Conditional Access](../protect/conditional-access.md) to the mix, configure policies that allow only compliant devices to access your network and organization's resources. Access restrictions can include file shares and company email. Conditional Access policies also work with the device state data reported by third-party [device compliance partners](../protect/device-compliance-partners.md) you integrate with Intune.

Following are a few of the security settings and tasks you can manage through available policies:

- **Authentication methods** – Configure how your devices authenticate to your organization's resources, email, and applications.

  - [Use certificates for authentication](../protect/certificates-configure.md) to applications, your organization's resources, and for signing and encryption of email using S/MIME. You can also set up [derived credentials](../protect/derived-credentials.md) when your environment requires the use of smartcards.

  - Configure settings that help limit risk, like:
    - Require multi-factor-authentication (MFA) to add an extra layer of authentication for users.
    - Set PIN and password requirements that must be met before gaining access to resources.
    - Enable [Windows Hello for Business](../protect/windows-hello.md) for Windows devices.

- **Device encryption** – Manage [BitLocker](../protect/encrypt-devices.md) on Windows devices, and [FileVault](../protect/encrypt-devices-filevault.md) on macOS.

- **Software updates** – Manage how and when devices get software updates. The following are supported:

  - Android *firmware* updates:
    - [Firmware Over-the-Air (FOTA)](../protect/fota-updates-android.md) - Supported by some OEMs, you can use FOTA to remotely update firmware of devices.
    - [Zebra LifeGuard Over-the-Air (LG OTA)](../protect/zebra-lifeguard-ota-integration.md) - Manage firmware updates for supported Zebra devices through the Intune admin center.
  - [iOS](../protect/software-updates-ios.md) - Manage device operating system versions, and when devices check for and install updates.
  - [macOS](../protect/software-updates-macos.md) - Manage software updates for macOS devices that enrolled as supervised devices.
  - [Windows](../protect/windows-update-for-business-configure.md)- To manage the Windows Update experience for devices, you can configure when devices scan or install updates, hold a set of your managed devices at specific feature versions, and more.

- **Security baselines** – Deploy [security baselines](../protect/security-baselines.md) to establish a core security posture on your Windows devices. Security baselines are preconfigured groups of Windows settings that come recommended by the relevant product teams. You can use baselines as provided or edit instances of them to meet your security goals for targeted groups of devices.

- **Virtual private networks (VPNs)** – With VPN profiles, assign VPN settings to devices so they can easily connect to your organization's network. Intune supports several [VPN connection types](../configuration/vpn-settings-configure.md#vpn-connection-types) and apps that include both built-in capabilities for some platforms and both first and third-party VPN apps for devices.

- **Windows Local Administrator Password Solution (LAPS)** - With [Windows LAPS policy](../protect/windows-laps-overview.md), you can:
  - Enforce password requirements for local admin accounts
  - Back up a local admin account from devices to your Active Directory (AD) or Microsoft Entra
  - Schedule rotation of those account passwords to help keep them safe.

## Protect data through policies

Intune-managed apps and Intune's [app protection policies](../apps/app-protection-policy.md) can help stop data leaks and keep your organization's data safe. These protections can apply to devices that are enrolled with Intune and to devices that aren't.

- **Intune-managed apps** (or *managed apps* for short), are apps that integrate the [Intune App SDK](../developer/app-sdk.md) or are wrapped by the [Intune App Wrapping Tool](../developer/apps-prepare-mobile-application-management.md). These apps can be managed using Intune app protection policies. To view a list of publicly available managed apps, see [Intune protected apps](../apps/apps-supported-intune-apps.md).

  Users can use managed apps to work with both your organization's data, and their own personal data. However, when app protection policies require the use of a managed app, the managed app is the only app that can be used to access your organization's data. App protection rules don't apply to a user's personal data.

- **App protection policies** are rules that ensure an organization's data remains safe or contained in a managed app. The rules identify the managed app that must be used, and define what can be done with the data while the app is in use.

The following are examples of protections and restrictions you can set with app protection policies and managed apps:

- Configure app-layer protections, like requiring a PIN to open an app in a work context.
- Control the sharing of an organization's data between apps on a device, like blocking copy and paste, or screen captures.
- Prevent the saving of your organization's data to personal storage locations.

## Use device actions to protect devices and data

From the Microsoft Intune admin center, you can run [device actions](../remote-actions/device-management.md#available-remote-actions) that help keep a selected device protected. You can run a subset of these actions as [bulk device actions](../remote-actions/bulk-device-actions.md) to affect multiple devices at the same time. And several [remote actions from Intune](../../configmgr/comanage/quickstart-remote-actions.md) can also be used with co-managed devices.

Device actions aren't policy and take effect a single time when invoked. They apply either immediately if the device is accessible on-line, or when the device next boots up or checks in with Intune. Considered these actions as supplemental to the use of policies that configure and maintain security configurations for a population of devices.

Following are examples of actions you can run that help secure devices and data:

**Devices managed by Intune**:

- BitLocker key rotation (Windows only)
- Disable Activation Lock (iOS only)
- Full or Quick scan (Windows only)
- Remote lock
- Retire (which removes your organization's data from the device while leaving personal data intact)
- Update Microsoft Defender Security Intelligence
- Wipe (factory reset the device, removing all data, apps, and settings)

**Devices managed by Configuration Manager**:

- Retire
- Wipe
- Sync (force a device to immediately check in with Intune to find new policies or pending actions)

## Integrate with other products and partner technologies

Intune supports integration with partner apps from both first-party and third-party sources, which expand on its built-in capabilities. You can also integrate Intune with several Microsoft technologies.

### Compliance partners

Learn about using [device compliance partners](../protect/device-compliance-partners.md) with Intune. When you manage a device with a mobile device management partner other than Intune, you can integrate that compliance data with Microsoft Entra ID. When integrated, Conditional Access policies can use the partner data alongside compliance data from Intune.

### Configuration Manager

You can use many Intune policies and device actions to [protect the devices you manage with Configuration Manager](../protect/endpoint-security-manage-devices.md). To support those devices, configure [co-management](../../configmgr/comanage/overview.md) or [tenant attach](../../configmgr/tenant-attach/device-sync-actions.md). You can also [use both together](../../configmgr/comanage/faq.yml#should-i-use-co-management-or-tenant-attach-) with Intune.

- With *Co-management*, you can concurrently manage a Windows device with both Configuration Manager and Intune. You install the Configuration Manager client and enroll the device to Intune. The device communicates with both services.

- With *Tenant attach*, you set up synchronization between your Configuration Manager site and your Intune tenant. This synchronization provides you with a single view for all devices that you manage with Microsoft Intune.

After a connection between Intune and Configuration Manager is established, devices from Configuration Manager are available in the Microsoft Intune admin center. You can then deploy Intune policies to those devices or use device actions to protect them.

Some of the protections you can apply include:

- Deploy certificates to devices by using Intune *Simple Certificate Enrollment Protocol* (SCEP) or *private and public key pair* (PKCS) certificate profiles.
- Use compliance policy.
- Use endpoint security policies, like *Antivirus*, *Endpoint detection and response*, and *Firewall* rules.
- Apply security baselines.
- Manage Windows Updates.

### Mobile threat defense apps

Mobile Threat Defense (MTD) apps actively scan and analyze devices for threats. When you integrate (connect) [Mobile Threat Defense](../protect/mobile-threat-defense.md) apps with Intune, you gain the apps assessment of a devices threat level. Evaluation of a device threat or risk level is an important tool for protecting your organization's resources from compromised mobile devices. You can then use that threat level in various policies, like Conditional Access policies, to help gate access to those resources.

Use threat-level data with policies for device compliance, app protection, and Conditional Access. These policies use the data to help block noncompliant devices from accessing your organization's resources.

With an integrated MTD app:

- For [enrolled devices](../protect/mtd-device-compliance-policy-create.md):
  - Use Intune to deploy and then manage the MTD app on devices.
  - Deploy device compliance policies that use the devices reported threat level to evaluate compliance.
  - Define Conditional Access policies that consider a devices threat level.
  - Define app protection policies to determine when to block or allow access to data, based on the threat level of the device.

- For [devices that don't enroll with Intune](../protect/mtd-app-protection-policy.md) but run an MTD app that integrates with Intune, use their threat level data with your app protection policies to help block access to your organization's data.

Intune supports integration with:

- Several [third-party MTD partners](../protect/mobile-threat-defense.md#mobile-threat-defense-partners).
- [Microsoft Defender for Endpoint](../protect/advanced-threat-protection.md), which supports extra capabilities with Intune.

### Microsoft Defender for Endpoint

On its own, Microsoft Defender for Endpoint provides several security focused benefits. Microsoft Defender for Endpoint also [integrates with Intune](../protect/advanced-threat-protection.md) and is supported on several device platforms. With integration, you gain a mobile threat defense app and add capabilities to Intune for keeping data and devices safe. These capabilities include:

- **Support for Microsoft Tunnel** - On Android devices, Microsoft Defender for Endpoint is the client application you use with [Microsoft Tunnel](../protect/microsoft-tunnel-overview.md), a VPN gateway solution for Intune. When used as the Microsoft Tunnel client app, you don't need a subscription for Microsoft Defender for Endpoint.

- **Security tasks** – With [security tasks](../protect/atp-manage-vulnerabilities.md), Intune admins can take advantage of Microsoft Defender for Endpoint's [threat and vulnerability management](/windows/security/threat-protection/windows-defender-atp/next-gen-threat-and-vuln-mgt) capabilities. How it works:

  - Your Defender for Endpoint team identifies at-risk-devices and create the security tasks for Intune in the Defender for Endpoint security center.
  - Those tasks show up in Intune with mitigation advice that Intune admins can use to mitigate the risk.
  - When a task is resolved in Intune, that status passes back to the Defender for Endpoint security center where the results of the mitigation can be evaluated.

- **Endpoint security policies** – The following Intune endpoint security policies require integration with Microsoft Defender for Endpoint. When you use [tenant attach](../protect/tenant-attach-intune.md), you can deploy these policies to devices you manage with either Intune or Configuration Manager.

  - [Antivirus policy](../protect/endpoint-security-antivirus-policy.md) - Manage the settings for *Microsoft Defender Antivirus* and the *Windows Security experience* on supported devices, like Windows and macOS.

  - [Endpoint detection and response policy](../protect/endpoint-security-edr-policy.md) – Use this policy to configure endpoint detection and response (EDR), which is a capability of Microsoft Defender for Endpoint.

### Conditional Access

Conditional Access is a Microsoft Entra capability that [works with Intune](../protect/conditional-access.md) to help protect devices. For devices that register with Microsoft Entra ID, Conditional Access policies can use device and compliance details from Intune to enforce access decisions for users and devices.

Combine Conditional Access policy with:

- [Device compliance policies](../protect/create-conditional-access-intune.md) can require a device be marked as compliant before that device can be used to access your organization's resources. The Conditional Access policies specify apps services you want to protect, conditions under which the apps or services can be accessed, and the users the policy applies to.

- [App protection policies](../protect/app-based-conditional-access-intune.md) can add a security layer that ensures only client apps that support Intune app protection policies can access your online resources, like Exchange or other Microsoft 365 services.

Conditional Access also works with the following to help you keep devices secure:

- Microsoft Defender for Endpoint and third-party MTD apps
- Device compliance partner apps
- Microsoft Tunnel

## Add Endpoint Privilege Management

Endpoint Privilege Management (EPM) allows you to run your Windows users as standard users while elevating privileges only when needed, as designed by organizational rules and parameters set by your organization. This design supports the enforcement of least privilege access, a core tenant of a Zero Trust security architecture. EPM enables IT teams to manage standard users more efficiently and limit their attack surface by only allowing employees to run as administrators for specific, approved applications or tasks.

Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

By deploying EPM *elevation rules* that you define, you can allow only the applications you trust to run in the elevated context. For example, your rules can require a *file hash* match or the presence of a *certificate* to validate the files integrity before it runs on a device.

> [!TIP]
>
> Endpoint Privilege Management is available as an [Intune add-on](../fundamentals/intune-add-ons.md) which requires an additional license to use, and supports Windows 10 and Windows 11 devices.

For more information, see [Endpoint Privilege Management](../protect/epm-overview.md).

## Next steps

Plan to use Intune's capabilities to support your journey towards a zero-trust environment by protecting your data and securing devices. Beyond the previous in-line links to learn more about those capabilities, learn about [data security and sharing in Intune](../protect/privacy-data-secure-share.md).
