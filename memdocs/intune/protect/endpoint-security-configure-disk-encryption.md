---
# required metadata

title: Use Endpoint Security disk encryption policy in Intune | Microsoft Docs
description: Configure the Endpoint Security policy for disk encryption like Windows 10 BitLocker and macOS FileVault in Intune
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha

---

# Configure Endpoint security Disk Encryption policy in Intune

As part of Endpoint security in Intune, Disk Encryption policies make it easy for security admins to focus on managing the discrete group of encryption settings for your managed devices.

Disk encryption profiles contain only the settings that are relevant for encryption methods, like FileVault or BitLocker.

While you can configure the same device settings by using *Endpoint Protection profiles* for device configuration, the device configuration profiles include additional categories of settings that are unrelated to disk encryption, which can complicate the task of configuring only disk encryption.

## FileVault profile for macOS

Use the **FileVault** profile to manage the settings that apply only to FileVault on macOS. FileVault provides built-in Full Disk Encryption for macOS devices.

After you create a policy to encrypt devices with FileVault, the policy applies to devices in two stages. First, the device is prepared to enable Intune to retrieve and back up the recovery key. This action is referred to as escrow. After the key is escrowed, the disk encryption can start.

After you encrypt devices, use the Intune encryption report to view encryption details for those devices.

### Prerequisites for FileVault

- Devices must run macOS 10.13 or later.
- To manage this profile, your account must have the following FileVault permissions, which are part of the **Remote tasks** category, and the built-in RBAC roles that grant the permission:

  - **Get FileVault key**:

    - Help Desk Operator
    - Endpoint security manager

  - **Rotate FileVault key**:
    - Help Desk Operator

### Configure the FileVault profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Disk encryption** > **Create Policy**

3. Select your **Platform**, select the **Profile** you want to configure for that platform, and then select **Create**.

4. On **Basics**, enter the following properties:
   - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. A good policy name might include the *profile type* and *platform*.  
   - **Description**: Enter a description for the policy. This setting is optional, but recommended.

5. Select **Next**.

6. In **Configuration settings**, review and configure the settings you want to apply to devices. For more information about the settings, see the following reference article:

   macOS:
   - **FileVault** – [macOS disk encryption settings](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault)

7. Select **Next**.

8. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as US-NC IT Team or JohnGlenn_ITDepartment. For more information about scope tags, see Use RBAC and scope tags for distributed IT.

   Select **Next**.

9. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see Assign user and device profiles.

   Select **Next**.

10. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

### Manage FileVault

After Intune encrypts a macOS device with FileVault, you can view and manage the FileVault recovery keys when you view the Intune [encryption report](../protect/encryption-monitor.md).

After Intune encrypts a macOS device with FileVault, you can view that device's personal recovery key from the web Company Portal on any device. Once in the web Company Portal, choose the encrypted macOS device, and then choose to "Get recovery key" as a remote device action.

### Retrieve personal recovery key from MEM encrypted macOS devices

End users can retrieve their personal recovery key (FileVault key) using the iOS Company Portal app, the Android Company Portal app, or through the Android Intune app.

The device that has the personal recovery key must be enrolled with Intune and encrypted with FileVault through Intune. Using the iOS Company Portal app, Android Company Portal app, the Android Intune app, or the Company Portal website, the end-user can see the **FileVault** recovery key needed to access their Mac devices. 

End-users can select **Devices** > *the encrypted and enrolled macOS device* > **Get recovery key**. The browser will show the Web Company Portal and display the recovery key.

## BitLocker profile for Windows 10

Use the **BitLocker** profile to manage the settings that apply only to BitLocker drive encryption on devices that run Windows 10. BitLocker is a data protection feature that integrates with the operating system and addresses the threats of data theft or exposure from lost, stolen, or inappropriately decommissioned computers.

After you encrypt devices, use the Intune [encryption report](../protect/encryption-monitor.md) to view encryption details for those devices. You can also access important information for BitLocker from your devices, as found in Azure Active Directory (Azure AD).

### Prerequisites for BitLocker

- BitLocker is available on devices that run Windows 10 or later.
- Some settings for BitLocker can require a TPM.

### Configure the BitLocker profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Disk encryption** > **Create Policy**.

3. Select your **Platform**, select the **Profile** you want to configure for that platform, and then select **Create**. 

4. On **Basics**, enter the following properties:
   - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. A good policy name might include the *profile type* and *platform*.  
   - **Description**: Enter a description for the policy. This setting is optional, but recommended.

5. Select **Next**.

6. In **Configuration settings**, review and configure the settings you want to apply to devices. For more information about the settings, see the following reference article:
Windows 10:
   - **BitLocker** – [Windows 10 disk encryption settings](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker)

7. Select **Next**.

8. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as US-NC IT Team or JohnGlenn_ITDepartment. For more information about scope tags, see Use RBAC and scope tags for distributed IT.
   Select **Next**.

9. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see Assign user and device profiles.

   Select **Next**.

10. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

### Silently enable BitLocker on devices

You can configure a BitLocker policy that automatically and silently enables BitLocker on a device. That means that BitLocker enables successfully without presenting any UI to the end user, even when that user isn't a local Administrator on the device.

**Prerequisites to silently enable BitLocker**  
Devices must meet the following conditions to be eligible for silently enabling BitLocker:

- The device must run Windows 10 version 1809 or later
- The device must be Azure AD Joined

**BitLocker policy configuration**  
The following two settings for BitLocker – Base Settings must be configured in the BitLocker profile:

- **Hide prompt about third-party encryption** = **Yes**

- **Allow standard users to enable encryption during Autopilot** = **Yes**

   Devices must not require use of a *startup PIN* or *startup key.* When a TPM startup PIN or startup key is required, BitLocker cannot silently enable and requires interaction from the end user.

   To meet this requirement, in the BitLocker profile ensure the following three settings under BitLocker OS Drive Settings are not set to Required. They can be set to either Blocked or Allowed.

- **Compatible TPM startup PIN** = *Blocked* or *Allowed*

- **Compatible TPM startup key and PIN** = *Blocked* or *Allowed*

### Manage BitLocker recovery keys

After Intune encrypts a Windows 10 device with BitLocker, you can view and retrieve BitLocker recovery keys when you view the Intune encryption report.
You can use an Intune device action to remotely rotate the BitLocker recovery key of a device that runs Windows 10 version 1909 or later.

#### Prerequisites to rotate BitLocker recovery keys

Devices must meet the following prerequisites to support rotation of the BitLocker recovery key:

- Devices must run Windows 10 version 1909 or later
- Azure AD-joined and Hybrid-joined devices must have support for key rotation enabled:
  - **Enable client-driven recovery password for** 

#### To rotate the BitLocker recovery key

1. Sign in to the Microsoft Endpoint Manager admin center.

2. Select **Endpoint security** > **All devices**.

3. In the list of devices that you manage, select a device.

4. On the **Overview** page of the device, select the **BitLocker key rotation**. If you don’t see this option, select the ellipsis (**…**) to show additional options, and then select the **BitLocker key rotation** device remote action.

   ![Select the ellipsis to view more options](./media/endpoint-security-configure-disk-encryption/select-more.png)

## Next steps

[Endpoint security in Intune](../protect/endpoint-security.md)
Review profile settings for disk encryption](../protect/endpoint-security-disk-encryption-profile-settings.md)
