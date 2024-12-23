---
# required metadata
title: Encrypt macOS FileVault disk encryption with Intune policy
titleSuffix: Microsoft Intune
description: Use Microsoft Intune policy to configure FileVault on macOS devices, and use the admin center to manage their recovery keys.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/25/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid:

# optional metadata

#audience:

ms.reviewer: beflamm; aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- highpri
- sub-secure-endpoints

---

# Use FileVault disk encryption for macOS with Intune

Use Microsoft Intune to configure and manage macOS FileVault disk encryption. FileVault is a whole-disk encryption program that is included with macOS. With Intune you can deploy policies that configure FileVault, and then manage recovery keys on devices that run **macOS 10.13 or later**.

Use one of the following policy types to configure FileVault on your managed devices:

- **[Endpoint security policy for macOS FileVault](#create-endpoint-security-policy-for-filevault)**. The FileVault profile in *Endpoint security* is a focused group of settings that is dedicated to configuring FileVault.

  View the [FileVault settings that are available in profiles for disk encryption policy](../protect/endpoint-security-disk-encryption-profile-settings.md).

- **[Device configuration profile for endpoint protection for macOS FileVault](#create-endpoint-security-policy-for-filevault)**. FileVault settings are one of the available settings categories for macOS endpoint protection. For more information about using a device configuration profile, see [Create a device profile in Intune](../configuration/device-profile-create.md).

  View the [FileVault settings that are available in endpoint protection profiles for device configuration policy](../protect/endpoint-protection-macos.md#filevault).

- **[Settings catalog profile for macOS FileVault](#create-settings-catalog-policy-for-filevault)**. FileVault can be configured through the Intune [settings catalog](../configuration/settings-catalog.md), which includes some settings that aren't available in the *endpoint security* and *endpoint protection* templates.

To manage BitLocker for Windows 10/11, see [Manage BitLocker policy](../protect/encrypt-devices.md).

> [!TIP]
> Intune provides a built-in [encryption report](encryption-monitor.md) that presents details about the encryption status of devices, across all your managed devices.

After you create a policy to encrypt devices with FileVault, the policy is applied to devices in two stages. First, the device is prepared to enable Intune to retrieve and back up the recovery key. This action is referred to as escrow. After the key is escrowed, the disk encryption can start.

In addition to using Intune policy to encrypt a device with FileVault, you can deploy policy to a managed device to enable Intune to [assume management of FileVault when the device the user has encrypted it](#assume-management-of-filevault-on-previously-encrypted-devices). This scenario requires the device to receive FileVault policy from Intune, followed by the user uploading their personal recovery key to Intune.

User-approved device enrollment is required for FileVault to work on a device. The user must manually approve of the management profile from system preferences for enrollment to be considered user-approved.

## Role-based access controls to manage FileVault

To manage FileVault in Intune, an account must be assigned an Intune [role-based access control](../fundamentals/role-based-access-control.md) (RBAC) role that includes the **Remote tasks** permission with the **Rotate FileVault key** right set to **Yes**:

You can add this permission and right to your own [custom RBAC roles](../fundamentals/create-custom-role.md) or use one of the following [built-in RBAC roles](../fundamentals/role-based-access-control-reference.md) that include this right:

- Help Desk Operator
- Endpoint Security Administrator

## Create endpoint security policy for FileVault

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Disk encryption** > **Create Policy**.

3. On the **Basics** page, enter the following properties, and then choose **Next**.
   - **Platform**: macOS
   - **Profile**: FileVault

   ![Select the FileVault profile](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. On the **Configuration settings** page:
   1. Set *Enable FileVault* to **Yes**.
   2. For *Recovery key type*, only **Personal Recovery Key** is supported.
   3. Configure other settings to meet your requirements.

   Consider adding a message to help guide users on [how to retrieve the recovery key](#retrieve-a-personal-recovery-key) for their device. This information can be useful for your users when you use the setting for Personal recovery key rotation, which can automatically generate a new recovery key for a device periodically.

   For example: To retrieve a lost or recently rotated recovery key, sign in to the Intune Company Portal website from any device. In the portal, go to Devices and select the device that has FileVault enabled, and then select *Get recovery key*. The current recovery key is displayed.

5. When your done configuring settings, select **Next**.

6. On the **Scope (Tags)** page, choose **Select scope tags** to open the Select tags pane to assign scope tags to the profile.

   Select **Next** to continue.

7. On the **Assignments** page, select the groups that will receive this profile. For more information on assigning profiles, see Assign user and device profiles. Select **Next**.

8. On the **Review + create** page, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

## Create settings catalog policy for FileVault

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **By platform** > **macOS** > **Manage devices** > **Configuration** > **Create** > **New policy**.

3. On the **Create a profile** page, select **Settings catalog** for the **Profile type**.

4. On the **Basics** page, enter the following properties:

   - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name might include the profile type and platform.

   - **Description**: Enter a description for the policy. This setting is optional, but recommended.

5. On the **Configuration settings** page, select **+ Add settings** to open the settings picker. The FileVault settings are located under the *Full Disk Encryption* category:

   :::image type="content" source="./media/encrypt-devices-filevault/filevault-settings-picker.png" alt-text="Image of the FileVault options in the Full Disk Encryption category of the Settings picker.":::

   To enable FileVault, select and configure the following settings from the *Full Disk Encryption* category:

   - FileVault > **Enable** - Set to **On**
   - FileVault Recovery Key Escrow > **Location** - Specify a description of the location where the recovery key is escrowed. This text is inserted into the message the user sees when enabling FileVault.

   > [!TIP]
   >
   > When configuring encryption for devices that run macOS 14 or later, you can use the macOS Setup Assistant to enforce FileVault encryption before a user arrives at the home screen. See [Enable FileVault through the Setup Assistant](#enable-filevault-through-the-setup-assistant) later in this article.

6. Configure extra [FileVault settings](https://support.apple.com/en-md/guide/deployment/dep32bf53500/web) *(opens Apple’s website)* to meet your business needs, and then select **Next**.

7. If applicable, on the **Scope (Tags)** page, choose **Select scope tags** to open the *Select tags* pane to assign scope tags to the profile. Select **Next** to continue.

8. On the **Assignments** page, select the groups that receive this profile. For more information on assigning profiles, see Assign user and device profiles. Select **Next**.

9. On the **Review + create** page, when you're done, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

### Enable FileVault through the Setup Assistant

For devices that run macOS 14 and later, your settings catalog policy can also enforce FileVault encryption through the macOS Setup Assistant, before a user arrives at the home screen. This goal requires extra configurations:

- The **Await final configuration** feature for the device must be set to **Yes**. This configuration prevents end users from accessing restricted content or changing settings until applicable Intune device configuration policies apply. For information on this configuration, see [Automatically enroll Macs with Apple Business Manager or Apple School Manager](../../intune/enrollment/device-enrollment-program-enroll-macos.md).

- Create a filter using the *EnrollmentProfileName* attribute that will be assigned to the settings catalog policy. This ensures that the FileVault policy will be assigned when the device first enrolls with Intune. For more information on configuring filters, see [Create filters in Microsoft Intune](../fundamentals/filters.md). 

- When *Await final Configuration* set to *Yes* for a device, you can then add the following Full Disk Encryption setting for FileVault in your settings catalog profile

- FileVault > **Force Enable in Setup Assistant** – Set to **Enabled**.

   The following image shows the settings catalog profile configured with the core settings to enable FileVault and use the Setup Assistant to enforce encryption. In this example, the Location setting uses the simple name of our domain, *Contoso*:

  > [!IMPORTANT]
  > The **Defer** setting must be configured to **Enabled** to successfully enable FileVault in Setup Assistant for devices running macOS 14.4. 

  :::image type="content" source="./media/encrypt-devices-filevault/filevault-setup-assistant-configuration.png" alt-text="Screenshot of the settings needed to enable File Vault in Setup Assistant.":::

## Create device configuration policy for FileVault (Deprecated)

> [!NOTE]
> The macOS template for Endpoint Protection is deprecated and no longer supports creating new profiles. Instead, use the [Endpoint security](#create-endpoint-security-policy-for-filevault) or the [settings catalog](#create-settings-catalog-policy-for-filevault) to configure and manage new FileVault profiles.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage devices** > **Configuration** > On the *Policies* tab, select **+ Create**.

3. On the **Create a profile** page, set the following options, and then select **Create** > **New policy**:
   - **Platform**: macOS
   - **Profile type**: Templates
   - **Template name**: Endpoint protection (Deprecated)

   :::image type="content" source="./media/encrypt-devices-filevault/select-macos-filevault-dc.png" alt-text="Screen shot that displays the the Endpoint protection profile.":::

4. On the **Basics** page, enter the following properties:

   - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name might include the profile type and platform.

   - **Description**: Enter a description for the policy. This setting is optional, but recommended.

5. On the **Configuration settings** page, select **FileVault** to expand the available settings:

   :::image type="content" source="./media/encrypt-devices-filevault/filevault-settings.png" alt-text="Screen shot that displays FileVault settings.":::

6. Configure the following settings:
  
   - For *Enable FileVault*, select **Yes**.

   - For *Recovery key type*, select **Personal key**.

   - For *Escrow location description of personal recovery key*, add a message to help guide users on [how to retrieve the recovery key](#retrieve-a-personal-recovery-key) for their device. This information can be useful for your users when you use the setting for Personal recovery key rotation, which can automatically generate a new recovery key for a device periodically.

     For example: To retrieve a lost or recently rotated recovery key, sign in to the Intune Company Portal website from any device. In the portal, go to *Devices* and select the device that has FileVault enabled, and then select *Get recovery key*. The current recovery key is displayed.

   Configure the remaining [FileVault settings](endpoint-protection-macos.md#filevault) to meet your business needs, and then select **Next**.

7. If applicable, on the **Scope (Tags)** page, choose **Select scope tags** to open the Select tags pane to assign scope tags to the profile.

   Select **Next** to continue.

8. On the **Assignments** page, select groups to receive this profile. For more information on assigning profiles, see Assign user and device profiles.
Select **Next**.

9. On the **Review + create** page, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

## Manage FileVault

To view information about devices that receive FileVault policy, see [Monitor disk encryption](../protect/encryption-monitor.md).

When Intune first encrypts a macOS device with FileVault, a personal recovery key is created. Upon encryption, the device displays the personal key a single time to the device user.

> [!NOTE]
>
> A device that reports error code -2016341107 / 0x87d1138d generally means the end user has not accepted the FileVault prompt to begin encryption.

For managed devices, Intune can escrow a copy of the personal recovery key. Escrow of keys enables Intune administrators to rotate keys to help protect devices, and users to recover a lost or rotated personal recovery key.

Intune escrows a recovery key when Intune policy encrypts a device, or after a user uploads their recovery key for device that they manually encrypted.

After Intune escrows the personal recovery key:

- Admins can manage and rotate the FileVault recovery keys for any managed macOS device, by using the Intune encryption report.
- Admins can view the personal recovery key for only managed macOS devices that are marked as *corporate*. They can’t view the recovery key for personal devices.
- Users can view and [retrieve their personal recovery key from a supported location](#retrieve-a-personal-recovery-key). For example, from the Company Portal website, the user can choose to *Get recovery key* as a remote device action.

### Assume management of FileVault on previously encrypted devices

Intune can’t manage FileVault disk encryption on a macOS device that is encrypted by a device user unless you apply FileVault policy through Intune. There are two methods you can use that enable Intune to take-over management of FileVault in this scenario:

- [Upload a personal recovery key to Intune](#upload-a-personal-recovery-key) – Use this method when the user knows their personal recovery key.
- [The user generates a new recovery key on the device](#generate-a-new-recovery-key-on-the-device) – Use this method if the personal recovery key isn’t known by the user.

Both methods require that the device has active policy from Intune that manages FileVault encryption. To deliver this policy, use an [endpoint security disk encryption profile](#create-endpoint-security-policy-for-filevault).

#### Upload a personal recovery key

To enable Intune to manage FileVault on a previously encrypted device, the user who encrypted the device can use the Company Portal website to upload their personal recovery key for the device to Intune. Upload of the key enables Intune to assume management of the encryption.

Upon upload, Intune rotates the key to create a new personal recovery key. Intune stores the new key for future recovery needs and makes it available to the device user.

**Prerequisites**:

- **The encrypted device must have an Intune FileVault policy for disk encryption.**

  Before Intune can assume management of encryption of a user-encrypted device, that device must receive an Intune FileVault policy for disk encryption.  

  Use an [endpoint security disk encryption profile](#create-endpoint-security-policy-for-filevault), to encrypt devices with FileVault.

- **The user who encrypted the device must have access to their personal recovery key for the device and be directed to upload it to Intune.**

  Intune doesn’t alert users that they must upload their personal recovery key to complete encryption. Instead, use your normal IT communication channels to alert users who have previously encrypted their macOS device with FileVault that they must upload their personal recovery key to Intune.

  > [!NOTE]
  > Based on your compliance policy, devices might be blocked from accessing corporate resources until Intune successfully assumes management of FileVault encryption on the device

**Upload a personal recovery key to Intune**:

1. After the device receives the FileVault profile, direct the user to use the [Company Portal website](https://portal.manage.microsoft.com/).

2. In the Company Portal website, the user locates their encrypted macOS device and selects the option **Store recovery key**.

3. The user must enter their personal recovery key, and Intune then attempts to rotate the key to generate a new key.
   - If the key rotation is successful, Intune stores the new key for future use, and makes the key available to the user should the user need to recover their device.
   - If the key rotation fails, then either the device hasn’t processed the FileVault policy, or the key that is entered isn't accurate for the device.

4. After successful rotation, a user can [retrieve their new personal recovery key from a supported location](#retrieve-a-personal-recovery-key).

For more information, see [end-user content for upload of the personal recovery key](../user-help/store-recovery-key.md).

#### Generate a new recovery key on the device

To enable Intune to manage FileVault on a previously encrypted device, the user who encrypted the device can use the Terminal app on the device to rotate their personal recovery key. If the device has an active FileVault policy from Intune when the key is rotated, Intune then assumes management of the encryption.

**Prerequisites**:

- **The encrypted device must have an Intune FileVault policy for disk encryption.**

  Before Intune can assume management of encryption of a user-encrypted device, that device must receive an Intune FileVault policy for disk encryption.  

  Use an [endpoint security disk encryption profile](#create-endpoint-security-policy-for-filevault) to encrypt devices with FileVault.

- **The device user must have access to the Terminal app on the encrypted device.**

**Use Terminal to generate a new personal recovery key**:

1. After the device receives the FileVault profile, the user who encrypted the device must sign-in to the device, open Terminal, and run the following two commands, in order:
   1. `cd /Applications/Utilities`
   2. `sudo fdesetup changerecovery -personal`

      When this command runs, the user is prompted to provide their device password. After the password is provided, the device rotates the personal recovery key and presents the new personal recovery key to the user.

      After recording the new recovery key, complete the remaining prompts from the command.

2. After the command prompts are completed, the personal recovery key on the device has been rotated. If the device successfully received the FileVault policy, Intune assumes management of the device’s encryption the next time the device checks-in with Intune.

   By default, the device checks in about every eight hours. To expedite device check-in, use one of the following options:

   - An Intune admin can sign-in to Microsoft Intune admin center, go to **Devices**, select the device, and then select **Sync**. This notifies the device to immediately check in with Intune.
   - The device user can open the Company Portal app and go to **Settings** > **Sync**. This directs the device to immediately check for policy or profile updates.

3. After Intune assumes management of the encryption, a user can [retrieve their new personal recovery key from a supported location](#retrieve-a-personal-recovery-key).

For more information, see [end-user content for upload of the personal recovery key](../user-help/store-recovery-key.md).

### Retrieve a personal recovery key

For a macOS device that has its FileVault encryption managed by Intune, end users can retrieve their personal recovery key (FileVault key) from the following locations, using any device:

- Company Portal website (https://portal.manage.microsoft.com/)
- iOS/iPadOS Company Portal app
- Android Company Portal app
- Intune app

Administrators can view personal recovery keys for encrypted macOS devices that are marked as a *corporate* device. They can’t view the recovery key for a personal device.

The device that has the personal recovery key must be enrolled with Intune and encrypted with FileVault through Intune. When a device user uses the iOS Company Portal app, Android Company Portal app, the Android Intune app, or the Company Portal website, the user can see the **FileVault** recovery key needed to access their Mac devices.

Device users can select **Devices** > *the encrypted and enrolled macOS device* > **Get recovery key**. The browser shows the Web Company Portal and displays the recovery key.

### Rotate recovery keys

Intune supports multiple options to rotate and recover personal recovery keys. One reason to rotate a key is if the current personal key is lost or thought to be at risk.

- **Automatic rotation**: As an admin, you can configure the FileVault setting Personal recovery key rotation to automatically generate new recovery key's periodically. When a new key is generated for a device, the key isn't displayed to the user. Instead, the user must get the key either from an admin, or by using the company portal app.

- **Manual rotation**: As an admin, you can view information for a device that you manage with Intune and that's encrypted with FileVault. You can then choose to manually rotate the recovery key for corporate devices. You can't rotate recovery keys for personal devices.

  To rotate a recovery key:

  1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

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
