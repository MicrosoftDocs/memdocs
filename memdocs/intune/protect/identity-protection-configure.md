---
# required metadata

title: Deploy policy for Windows Hello to groups of Windows 10 and Windows 11 devices in Microsoft Intune
description: Use an Identity protection profile in Microsoft Intune to configure groups of devices to use Windows Hello for Business. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/25/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Use identity protection profiles to manage Windows Hello for Business in Microsoft Intune

Use an Identity protection profile to manage Windows Hello for Business on groups of devices in Microsoft Intune. [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-overview) is a method for signing in to Windows devices by replacing passwords, smart cards, and virtual smart cards. Intune includes built-in settings so Administrators can configure and use Windows Hello for Business. For example, you can use these settings to:

- Enable Windows Hello for Business for devices and users
- Set device PIN requirements, including a minimum or maximum PIN length
- Allow gestures, such as a fingerprint, that users can (or can't use) to sign in to devices

This feature applies to devices running:

- Windows 10
- Windows 11

In addition to use of an Identity protection profile, Intune supports the following options to manage settings for Windows Hello for Business:

- [During device enrollment](../protect/windows-hello.md): Manage Windows Hello when a device enrolls with a tenant-wide policy.
- [Security baselines](../protect/security-baselines.md): Some settings for Windows Hello can be managed by security baselines like the baselines for *Microsoft Defender for Endpoint security* or  *Security Baseline for Windows 10 and later*.
- [Endpoint security Account protection policy](../protect/endpoint-security-account-protection-policy.md): Account protection policies include some of the settings used by Windows Hello.

> [!NOTE]
> For customers looking to configure Windows Holographic for Business, please use [DeviceLock CSP](/windows/client-management/mdm/policy-csp-devicelock)

Intune uses *configuration profiles* to create and customize these settings for your organization's needs. After you add these features in a profile, push or deploy these settings to user and device groups in your organization.

This article shows you how to create a device configuration profile. For a list of all the settings, and what they do, see [Windows device settings to enable Windows Hello for Business](identity-protection-windows-settings.md).

> [!IMPORTANT]
> Due to how Intune determines the scope and applicability of Windows Hello for Business policy, the device may log **Event ID 454** as a result of applying policy. This can be safely ignored when policy is being successful applied (and enforced).

## Create the device profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration profiles** > **Create profile**.

3. Enter the following properties:

   - **Platform**: Select **Windows 10 and later**.
   - **Profile**: Select **Templates** > **Identity protection**.

4. Select **Create**.

5. In **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the new profile. Name your policies so you can easily identify them later.
   - **Description**: Enter a description for the profile. This setting is optional, but recommended.

   Select **Next** to continue.

6. In **Configuration settings**, configure the following settings:

   - **Configure Windows Hello for Business**: Choose how you want to configure Windows Hello for Business:

     - **Not configured** (default): [Provisions Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-how-it-works-provisioning) on the device. When identity protection profiles are assigned to users only, the device context defaults to **Not configured**.

     - **Disabled**: If you don't want to use Windows Hello for Business, select this option. This option disables Windows Hello for Business for all users.

     - **Enabled**: Choose this option to [provision](/windows/security/identity-protection/hello-for-business/hello-how-it-works-provisioning), and configure Windows Hello for Business settings in Intune. Enter the settings you want to configure. For a list of all settings, and what they do, see - [Windows device settings to enable Windows Hello for Business](identity-protection-windows-settings.md).

   - **Use security keys for sign-in**: Enable Windows Hello security key as a sign-in credential for all PCs in the tenant.

     - **Enable**
     - **Not configured**  (default)

   Select **Next** to continue.

7. In **Assignments**, select the user and device groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   > [!IMPORTANT]
   > To allow multiple users to be provisioned to a device, specify that the Windows Hello for Business policy be applied to the devices. If the policy is applied only to users, only one user can be provisioned to a device.

   Select **Next**.

8. In **Applicability Rules**, use the **Rule**, **Property**, and **Value** options to define how this profile applies within assigned groups. Intune applies the profile to devices that meet the rules you enter. For more information about applicability rules, see [Applicability rules](../configuration/device-profile-create.md).

   Select Next.

9. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.



## Next steps

- [Review settings, and what they do](identity-protection-windows-settings.md)
- [Monitor the profile status](../configuration/device-profile-monitor.md)
