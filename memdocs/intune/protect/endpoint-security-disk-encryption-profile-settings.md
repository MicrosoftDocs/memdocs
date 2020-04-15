---
# required metadata

title: Intune endpoint security disk encryption policy settings | Microsoft Docs
description: Endpoint security disk encryption policy settings for Bitlocker and Filevault in Microsoft Intune 
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

# Endpoint security disk encryption policy settings

View the settings you can configure in profiles for *Disk Encryption* policy in the Endpoint security node of Intune.  

Supported platforms and profiles:

- **macOS**:
  - Profile: **FileVault**
- **Windows 10 and later**:
  - Profile: **BitLocker**

## FileVault

### Encryption

**Enable FileVault**  
- **Not configured** (*default*)
- **Yes** - Enable Full Disk Encryption using XTS-AES 128 with FileVault on devices that run macOS 10.13 and later. FileVault is enabled when the user signs off of the device.

  When set to *Yes*, you can configure additional settings for FileVault.

  - **Recovery key type**
    *Personal key* recovery keys are created for devices. Configure the following settings for the personal key:

    - **Personal recovery key rotation**  
      Specify how frequently the personal recovery key for a device will rotate. You can select the default of **Not configured**, or a value of **1** to **12** months.
    - **Escrow location description of personal recovery key**  
      Specify a short message to the user that explains how they can retrieve their personal recovery key. This text is inserted into the message the user sees on their log in screen when prompted to enter their personal recovery key if a password is forgotten.

  - **Number of times allowed to bypass**  
    Set the number of times a user can ignore prompts to enable FileVault before FileVault is required for the user to sign in.
    - **Not configured** (*default*) - Encryption on the device is required before the next sign-in is allowed.
    - **1** to **10** - Allow a user to ignore the prompt from 1 to 10 times before requiring encryption on the device.
    - **No limit, always prompt** - The user is prompted to enable FileVault, but encryption is never required.

  - **Allow deferral until sign out**  
    - **Not configured** (*default*)
    - **Yes** - Defer the prompt to enable FileVault until the user signs out.  

  - **Disable prompt at sign out**  
    Prevent the prompt to the user that requests they enable FileVault when they sign out. When set to Disable, the prompt at sign-out is disabled and instead, the user is prompted when they sign in.
    - **Not configured** (*default*)
    - **Yes** - Disable the prompt to enable FileVault that appears at sign-out.

## BitLocker

### BitLocker – Base Settings

- **Enable full disk encryption for OS and fixed data drives**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  If the drive was encrypted before this policy applied, no extra action is taken. If the encryption method and options match that of this policy, configuration should return success. If an in-place BitLocker configuration option doesn't match this policy, configuration will likely return an error.
  
  To apply this policy to a disk already encrypted, decrypt the drive and reapply the MDM policy. Windows default is to not require BitLocker drive encryption, however on Azure AD Join and Microsoft Account (MSA) registration/login automatic encryption may apply enabling BitLocker at XTS-AES 128-bit encryption.

  - **Not configured** (*default*) - No BitLocker enforcement takes place.
  - **Yes** - Enforce use of BitLocker.

- **Require storage cards to be encrypted (mobile only)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  This setting only applies to Windows Mobile and Mobile Enterprise SKU devices.
  - **Not configured** (*default*) - The setting returns to the OS default, which is to not require storage card encryption.
  - **Yes** - Encryption on storage cards is required for mobile devices.

- **Hide prompt about third-party encryption**  
  CSP: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)

  If BitLocker is enabled on a system that has already been encrypted by a third-party encryption product, it may render the device unusable. Data loss may occur and you may need to reinstall Windows. It is highly suggested to never enable BitLocker on a device that has third-party encryption installed or enabled.

  By default, the BitLocker setup wizard prompts users to confirm that no third-party encryption is in place.

  - **Not configured** (*default*) – The BitLocker setup wizard displays a warning and prompts  users to confirm no third-party encryption is present.
  - **Yes** - Hide the BitLocker setup wizards prompt from users.

  If BitLocker silent enable features are required, the third-party encryption warning must be hidden as any required prompt breaks silent enablement workflows.

- **Enable client-driven recovery password for**  
  CSP: [ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  Add Work Account (AWA, formally Workplace Joined) devices are not supported for key rotation.
  - **Not configured** (*default*) – The client won’t rotate BitLocker recovery keys.
  - **Disabled**
  - **Azure AD-joined devices**
  - **Azure AD and Hybrid-joined devices**

### BitLocker - Fixed Drive Settings

- **BitLocker fixed drive policy**  
  [BitLocker Group Policy settings](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure*, you can then configure the following settings: 
