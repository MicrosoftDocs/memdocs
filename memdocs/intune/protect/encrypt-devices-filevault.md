---
# required metadata
title: Encrypt macOS devices with FileVault disk encryption with Intune 
titleSuffix: Microsoft Intune
description: Encrypt macOS devices with the built-in encryption method FileVault, and manage the recovery keys for encrypted devices from within the Microsoft Endpoint Manager admin center. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/15/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid:  

# optional metadata

#audience:

ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure

---

# Use FileVault disk encryption for  macOS with Intune

Intune supports macOS FileVault disk encryption. FileVault is a whole-disk encryption program that is included with macOS. You can use Intune to configure FileVault on devices that run **macOS 10.13 or later**.

Use one of the following policy types to configure FileVault on your managed devices:

- **[Endpoint security policy for macOS FileVault](#create-endpoint-security-policy-for-filevault)**. The FileVault profile in *Endpoint security* is a focused group of settings that is dedicated to configuring FileVault.

  View the [FileVault settings that are available in profiles for disk encryption policy](../protect/endpoint-security-disk-encryption-profile-settings.md).

- **[Device configuration profile for endpoint protection for macOS FileVault](#create-endpoint-security-policy-for-filevault)**. FileVault settings are one of the available settings categories for macOS endpoint protection. For more information about using a device configuration profile, see [Create a device profile in Inunte](../configuration/device-profile-create.md).

  View the [FileVault settings that are available in endpoint protection profiles for device configuration policy](../protect/endpoint-protection-macos.md#filevault).

To manage BitLocker for Windows 10, see [Manage BitLocker policy](../protect/encrypt-devices.md).

> [!TIP]
> Intune provides a built-in [encryption report](encryption-monitor.md) that presents details about the encryption status of devices, across all your managed devices.

After you create a policy to encrypt devices with FileVault, the policy is applied to devices in two stages. First, the device is prepared to enable Intune to retrieve and back up the recovery key. This action is referred to as escrow. After the key is escrowed, the disk encryption can start.

In addition to using Intune policy to encrypt a device with FileVault, you can deploy policy to a managed device to enable Intune to [assume management of FileVault when the device was encrypted by the user](#assume-management-of-filevault-on-previously-encrypted-devices). This scenario requires the device to receive FileVault policy from Intune, followed by the user uploading their personal recovery key to Intune.

User-approved device enrollment is required for FileVault to work on a device. The user must manually approve of the management profile from system preferences for enrollment to be considered user-approved.

## Permissions to manage FileVault

To manage FileVault in Intune, your account must have the applicable Intune [role-based access control](../fundamentals/role-based-access-control.md) (RBAC) permissions.

Following are the FileVault permissions, which are part of the **Remote tasks** category, and the built-in RBAC roles that grant the permission:

- **Get FileVault key**:
  - Help Desk Operator
  - Endpoint security manager

- **Rotate FileVault key**
  - Help Desk Operator

## Create device configuration policy for FileVault

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration profiles** > **Create profile**.

3. On the **Create a profile** page, set the following options, and then click **Create**:
   - **Platform**: macOS
   - **Profile**: Endpoint protection

   ![Select the Endpoint protection profile](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. On the **Basics** page, enter the following properties:

   - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name might include the profile type and platform.

   - **Description**: Enter a description for the policy. This setting is optional, but recommended.

5. On the **Configuration settings** page, select **FileVault** to expand the available settings:

   > [!div class="mx-imgBorder"]
   > ![FileVault settings](./media/encrypt-devices-filevault/filevault-settings.png)

6. Configure the following settings:
  
   - For *Enable FileVault*, select **Yes**.

   - For *Recovery key type*, select **Personal key**.

   - For *Escrow location description of personal recovery key*, add a message to help guide users on [how to retrieve the recovery key](#retrieve-a-personal-recovery-key) for their device. This information can be useful for your users when you use the setting for Personal recovery key rotation, which can automatically generate a new recovery key for a device periodically.

     For example: To retrieve a lost or recently rotated recovery key, sign in to the Intune Company Portal website from any device. In the portal, go to *Devices* and select the device that has FileVault enabled, and then select *Get recovery key*. The current recovery key is displayed.

   Configure the remaining [FileVault settings](endpoint-protection-macos.md#filevault) to meet your business needs, and then select **Next**.

7. On the **Scope (Tags)** page, choose **Select scope tags** to open the Select tags pane to assign scope tags to the profile.

   Select **Next** to continue.

8. On the **Assignments** page, select the groups that will receive this profile. For more information on assigning profiles, see Assign user and device profiles.
Select **Next**.

9. On the **Review + create** page, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

## Create endpoint security policy for FileVault

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Disk encryption** > **Create Policy**.

3. On the **Basics** page, enter the following properties, and then choose **Next**.
   - **Platform**: macOS
   - **Profile**: FileVault

   ![Select the FileVault profile](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. On the **Configuration settings** page:
   1. Set *Enable FileVault* to **Yes**.
   2. For *Recovery key type*, only **Personal Recovery Key** is supported.
   3. Configure additional settings to meet your requirements.

   Consider adding a message to help guide users on [how to retrieve the recovery key](#retrieve-a-personal-recovery-key) for their device. This information can be useful for your users when you use the setting for Personal recovery key rotation, which can automatically generate a new recovery key for a device periodically.

   For example: To retrieve a lost or recently rotated recovery key, sign in to the Intune Company Portal website from any device. In the portal, go to Devices and select the device that has FileVault enabled, and then select *Get recovery key*. The current recovery key is displayed.

5. When your done configuring settings, select **Next**.

6. On the **Scope (Tags)** page, choose **Select scope tags** to open the Select tags pane to assign scope tags to the profile.

   Select **Next** to continue.

7. On the **Assignments** page, select the groups that will receive this profile. For more information on assigning profiles, see Assign user and device profiles.
Select **Next**.

8. On the **Review + create** page, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

## Manage FileVault

To view information about devices that receive FileVault policy, see [Monitor disk encryption](../protect/encryption-monitor.md).

When Intune first encrypts a macOS device with FileVault, a personal recovery key is created. Upon encryption, the device displays the personal key a single time to the device user.

For managed devices, Intune can escrow a copy of the personal recovery key. Escrow of keys enables Intune administrators to rotate keys to help protect devices, and users to recover a lost or rotated personal recovery key.

Intune escrows a recovery key when Intune policy encrypts a device, or after a user uploads their recovery key for device that they manually encrypted.

After Intune escrows the personal recovery key:

- Admins can manage and rotate the FileVault recovery keys for any managed macOS device, by using the Intune encryption report.
- Admins can view the personal recovery key for only managed macOS devices that are marked as *corporate*. They can’t view the recovery key for personal devices.
- Users can view and [retrieve their personal recovery key from a supported location](#retrieve-a-personal-recovery-key). For example, from the Company Portal website, the user can choose to *Get recovery key* as a remote device action.

### Assume management of FileVault on previously encrypted devices

Intune can manage FileVault disk encryption on macOS devices that are encrypted through use of Intune policies. Intune can also take over management of FileVault on devices that were encrypted by device users, and not through Intune policy.

#### Prerequisites to assume management of FileVault

To assume management of previously encrypted device, the following conditions must be met:

1. **Deploy a FileVault policy to the device**. The previously encrypted device must receive a policy from Intune that turns on FileVault disk encryption.

   In this scenario, the policy doesn’t decrypt or re-encrypt the device. Instead, the policy enables Intune to assume management of the FileVault encryption that’s already enabled on the device.  You can use either endpoint security disk encryption policy, or a device configuration endpoint protection policy to encrypt devices with FileVault.

   See [Create and deploy policy](#create-device-configuration-policy-for-filevault).

2. **Users upload their personal recovery key to Intune**.  After the device receives the FileVault policy, direct the device user that encrypted the device to upload their personal recovery key to Intune. If the key is entered successfully, Intune assumes management of the FileVault encryption, and a new personal recovery key is created for the device and user.

   > [!IMPORTANT]
   > Intune doesn’t alert users that they must upload their personal recovery key to complete encryption. Instead, use your normal IT communication channels to alert users who have previously encrypted their macOS device with FileVault that they must upload their personal recovery key to Intune.  
   >
   > Based on your compliance policy, devices might be blocked from accessing corporate resources until Intune successfully assumes management of FileVault encryption on the device.

#### Upload a personal recovery key

To enable Intune to manage FileVault on a previously encrypted device, the device user must use the Company Portal website to upload their current personal recovery key for the device to Intune.  Upon upload, Intune rotates the key to create a new personal recovery key, which is then stored by Intune for future recovery, if needed.

In the Company Portal website, the user locates their encrypted macOS device and selects the option **Store recovery key**. As soon as the personal recovery key is entered, Intune attempts to rotate the key to generate a new key. Rotation is done to validate that the entered key was accurate for that device. This new key is then stored and managed by Intune for future use, should the user need to recover their device.

If the key rotation fails, then either the device hasn’t processed the FileVault policy, or the key that was entered is not accurate for the device.

After successful rotation, a user can [retrieve their new personal recovery key from a supported location](#retrieve-a-personal-recovery-key).

 View the [end-user content for upload of the personal recovery key](../user-help/store-recovery-key.md).

> [!IMPORTANT]
> For a device that is encrypted by a user and not by Intune, Intune can’t manage the devices FileVault encryption until that device receives a FileVault policy and the device user successfully uploads their personal recovery key.

### Retrieve a personal recovery key

For a macOS device that has its FileVault encryption managed by Intune, end users can retrieve their personal recovery key (FileVault key) from the following locations, using any device:

- Company Portal website
- iOS/iPadOS Company Portal app
- Android Company Portal app
- Intune app

Administrators can view personal recovery keys for encrypted macOS devices that are marked as a *corporate* device. They can’t view the recovery key for a personal device.

The device that has the personal recovery key must be enrolled with Intune and encrypted with FileVault through Intune. Using the iOS Company Portal app, Android Company Portal app, the Android Intune app, or the Company Portal website, the user can see the **FileVault** recovery key needed to access their Mac devices.

Device users can select **Devices** > *the encrypted and enrolled macOS device* > **Get recovery key**. The browser will show the Web Company Portal and display the recovery key.

### Rotate recovery keys

Intune supports multiple options to rotate and recover personal recovery keys. One reason to rotate a key is if the current personal key is lost or thought to be at risk.

- **Automatic rotation**: As an admin, you can configure the FileVault setting Personal recovery key rotation to automatically generate new recovery key's periodically. When a new key is generated for a device, the key isn't displayed to the user. Instead, the user must get the key either from an admin, or by using the company portal app.

- **Manual rotation**: As an admin, you can view information for a device that you manage with Intune and that's encrypted with FileVault. You can then choose to manually rotate the recovery key for corporate devices. You can't rotate recovery keys for personal devices.

  To rotate a recovery key:

  1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

  2. Select **Devices** > **All devices**.

  3. From the list of devices, select the device that is encrypted and for which you want to rotate its key. Then under Monitor, select **Recovery keys**.
  
  4. On the Recovery keys pane, select **Rotate FileVault recovery key**.

     The next time the device checks in with Intune, the personal key is rotated. When needed, the new key can be obtained by the user through the company portal.

### Recover recovery keys

- **Administrator**: Administrators can't view personal recovery keys for devices that are encrypted with FileVault.

- **End-user**: End-users use the Company Portal website from any device to view the current personal recovery key for any of their managed devices. You can't view recovery keys from the Company Portal app.

  To view a recovery key:
  
  1. Sign in to the *Intune Company Portal* website from any device.

  2. In the portal, go to **Devices** and select the macOS device that is encrypted with FileVault.

  3. Select **Get recovery key**. The current recovery key is displayed.

## Next steps

[Manage BitLocker policy](../protect/encrypt-devices.md)

[Monitor disk encryption](../protect/encryption-monitor.md)
