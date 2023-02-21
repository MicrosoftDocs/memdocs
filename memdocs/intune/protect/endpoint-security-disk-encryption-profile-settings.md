---
# required metadata

title: Intune endpoint security disk encryption policy settings | Microsoft Docs
description: Endpoint security disk encryption policy settings for BitLocker and FileVault in Microsoft Intune 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/28/2020
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
ms.collection:
- tier3
- M365-identity-device-management
ms.reviewer: aanavath

---

# Disk encryption policy settings for endpoint security in Intune

View the settings you can configure in profiles for *Disk Encryption* policy in the Endpoint security node of Intune as part of an [Endpoint security policy](../protect/endpoint-security-policy.md).

Applies to:

- macOS
- Windows 10/11

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
      Specify a short message to the user that explains how they can retrieve their personal recovery key. The user sees this message on their sign in screen when prompted to enter their personal recovery key if a password is forgotten.

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

  - **Hide recovery key**  
     Hide the personal recovery key from the user of the macOS device during encryption. After the disk is encrypted, a user can use any device to view their personal recovery key through the Intune Company Portal website, or company portal app on a supported platform.
    - **Not configured** (*default*)
    - **Yes** - Hide the personal recovery key during device encryption.

## BitLocker

### BitLocker – Base Settings

- **Enable full disk encryption for OS and fixed data drives**  
  CSP: [BitLocker - RequireDeviceEncryption](/windows/client-management/mdm/bitlocker-csp#requiredeviceencryption)

  If the drive was encrypted before this policy applied, no extra action is taken. If the encryption method and options match that of this policy, configuration should return success. If an in-place BitLocker configuration option doesn't match this policy, configuration will likely return an error.
  
  To apply this policy to a disk already encrypted, decrypt the drive and reapply the MDM policy. Windows default is to not require BitLocker drive encryption. However, on Azure AD Join and Microsoft Account (MSA) registration/login automatic encryption can apply enabling BitLocker at XTS-AES 128-bit encryption.

  - **Not configured** (*default*) - No BitLocker enforcement takes place.
  - **Yes** - Enforce use of BitLocker.

- **Require storage cards to be encrypted (mobile only)**  
  CSP: [BitLocker - RequireStorageCardEncryption](/windows/client-management/mdm/bitlocker-csp#requirestoragecardencryption)

  This setting only applies to Windows Mobile and Mobile Enterprise SKU devices.
  - **Not configured** (*default*) - The setting returns to the OS default, which is to not require storage card encryption.
  - **Yes** - Encryption on storage cards is required for mobile devices.

  > [!NOTE]
  > Support for [Windows 10 Mobile](https://support.microsoft.com/help/4485197/windows-10-mobile-end-of-support-faq) and [Windows Phone 8.1](https://support.microsoft.com/help/4036480/windows-phone-8-1-end-of-support-faq) ended in August of 2020.

- **Hide prompt about third-party encryption**  
  CSP: [BitLocker - AllowWarningForOtherDiskEncryption](/windows/client-management/mdm/bitlocker-csp#allowwarningforotherdiskencryption)

  If BitLocker is enabled on a system that's already encrypted by a third-party encryption product, it might render the device unusable. Data loss can occur and you might need to reinstall Windows. It's highly suggested to never enable BitLocker on a device that has third-party encryption installed or enabled.

  By default, the BitLocker setup wizard prompts users to confirm that no third-party encryption is in place.

  - **Not configured** (*default*) – The BitLocker setup wizard displays a warning and prompts  users to confirm no third-party encryption is present.
  - **Yes** - Hide the BitLocker setup wizards prompt from users.

  If BitLocker silent enable features are required, the third-party encryption warning must be hidden as any required prompt breaks silent enablement workflows.

  When set to *Yes*, you can then configure the following setting:

  - **Allow standard users to enable encryption during Autopilot**  
    CSP: [BitLocker - AllowStandardUserEncryption](/windows/client-management/mdm/bitlocker-csp)
    - **Not configured** (*default*) – The setting is left as client default, which is to require local admin access to enable BitLocker.
    - **Yes** - During Azure Active Directory Join (AADJ) silent enable scenarios, users don't need to be local administrators to enable BitLocker.

    For non-silent enablement and Autopilot scenarios, the user must be a local admin to complete the BitLocker setup wizard.

- **Configure client-driven recovery password rotation**  
  CSP: [BitLocker - ConfigureRecoveryPasswordRotation](/windows/client-management/mdm/bitlocker-csp)

  Add Work Account (AWA, formally Workplace Joined) devices aren't supported for key rotation.
  - **Not configured** (*default*) – The client won’t rotate BitLocker recovery keys.
  - **Disabled**
  - **Azure AD-joined devices**
  - **Azure AD and Hybrid-joined devices**

### BitLocker - Fixed Drive Settings

- **BitLocker fixed drive policy**  
  CSP: [BitLocker - EncryptionMethodByDriveType](/windows/client-management/mdm/bitlocker-csp#encryptionmethodbydrivetype)

  - **Fixed drive recovery**  
    CSP: [BitLocker - FixedDrivesRecoveryOptions](/windows/client-management/mdm/bitlocker-csp#fixeddrivesrecoveryoptions)

    Control how BitLocker-protected fixed data-drives are recovered in the absence of the required startup key information.

    - **Not configured** (*default*) - The default recovery options are supported including the data recovery agent (DRA). The end user can specify recovery options and recovery information isn't backed up to Azure Active Directory.
    - **Configure** – Enable access to configure various drive recovery techniques.

    When set to *Configure* the following settings are available:

    - **User creation of recovery key**  
      - **Blocked** (*default*)
      - **Required**
      - **Allowed**

    - **Configure BitLocker recovery package**
      - **Password and Key** (*default*) - Include both the BitLocker recovery password that's used by admins and users to unlock protected drives, and recovery key packages that are used by admins for data recovery purposes) in Active Directory.
      - **Password only** - The recovery key packages might not be accessible when needed.

    - **Require device to back up recovery information to Azure Ad**
      - **Not configured** (*default*) - BitLocker enablement will complete even if recovery key backup to Azure AD fails. This can result in no recovery information being stored externally.
      - **Yes** - BitLocker won't complete enablement until recovery keys have been successfully saved to Azure Active Directory.

    - **User creation of recovery password**  
      - **Blocked** (*default*)
      - **Required**
      - **Allowed**

    - **Hide recovery options during BitLocker setup**
      - **Not configured** (*default*) - Allow the user to access extra recovery options.
      - **Yes** - Block the end user from choosing extra recovery options such as printing recovery keys during the BitLocker setup wizard.

    - **Enable BitLocker after recovery information to store**
      - **Not configured** (*default*)  
      - **Yes**

    - **Block the use of certificate-based data recovery agent (DRA)**
      - **Not configured** (*default*) - Allow the use of DRA to be set up. Setting up DRA requires an enterprise PKI and Group Policy Objects to deploy the DRA agent and certificates.
      - **Yes** - Block the ability to use Data Recovery Agent (DRA) to recover BitLocker enabled drives.

  - **Block write access to fixed data-drives not protected by BitLocker**  
    CSP: [BitLocker - FixedDrivesRequireEncryption](/windows/client-management/mdm/bitlocker-csp#fixeddrivesrequireencryption)  
    This setting is available when *BitLocker fixed drive policy* is set to *Configure*.

    - **Not configured** (*default*) - Data can be written to non-encrypted fixed drives.
    - **Yes** - Windows won't allow any data to be written to fixed drives that aren't BitLocker protected. If a fixed drive isn't encrypted, the user will need to complete the BitLocker setup wizard for the drive before write access is granted.

  - **Configure encryption method for fixed data-drives**  
    CSP: [BitLocker - EncryptionMethodByDriveType](/windows/client-management/mdm/bitlocker-csp#encryptionmethodbydrivetype)  

    Configure the encryption method and cipher strength for fixed data-drives disks. *XTS- AES 128-bit* is the Windows default encryption method and the recommended value.

    - **Not configured** (*default*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

### BitLocker - OS Drive Settings

- **BitLocker system drive policy**  
  CSP: [BitLocker - EncryptionMethodByDriveType](/windows/client-management/mdm/bitlocker-csp#encryptionmethodbydrivetype)

  - **Configure** (*default*)  
  - **Not configured**

  When set to *Configure* you can configure the following settings:

  - **Startup authentication required**  
    CSP: [BitLocker - SystemDrivesRequireStartupAuthentication](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)

    - **Not configured** (*default*)
    - **Yes** - Configure the additional authentication requirements at system startup, including the use of Trusted Platform Module (TPM) or startup PIN requirements.

    When set to *Yes* you can configure the following settings:

    - **Compatible TPM startup**  
      CSP: [BitLocker - SystemDrivesRequireStartupAuthentication](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)

      It's recommended to require a TPM for BitLocker. This setting only applies when first enabling BitLocker and has no effect if BitLocker is already enabled.

      - **Blocked** (*default*) - BitLocker doesn’t use the TPM.
      - **Required** - BitLocker enables only if a TPM is present and usable.
      - **Allowed** - BitLocker uses the TPM if it's present.

    - **Compatible TPM startup PIN**  
      CSP: [BitLocker - SystemDrivesRequireStartupAuthentication](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)

      - **Blocked** (*default*) - Block the use of a PIN.
      - **Required** - Require a PIN and TPM be present to enable BitLocker.
      - **Allowed** - BitLocker uses the TPM if it's present and allows a startup PIN to be configured by the user.

      For silent enable scenarios, you must set this to *Blocked*. Silent enable scenarios (including Autopilot) won't be successful when user interaction is required.

    - **Compatible TPM startup key**  
      CSP: [BitLocker - SystemDrivesRequireStartupAuthentication](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)

      - **Blocked** (*default*) - Block the use of startup keys.
      - **Required** - Require a startup key and TPM be present to enable BitLocker.
      - **Allowed** - BitLocker uses the TPM if it's present and allows a startup key (such as a USB drive) be present to unlock the drives.

      For silent enable scenarios, you must set this to *Blocked*. Silent enable scenarios (including Autopilot) won't be successful when user interaction is required.

    - **Compatible TPM startup key and PIN**  
      CSP: [BitLocker - SystemDrivesRequireStartupAuthentication](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)

      - **Blocked** (*default*) - Block the use of a startup key and PIN combination.
      - **Required** - Require BitLocker have a startup key and PIN present to become enabled.
      - **Allowed** - BitLocker uses the TPM if it's present and allows a startup key) and PIN combination.

      For silent enable scenarios, you must set this to *Blocked*. Silent enable scenarios (including Autopilot) won't be successful when user interaction is required.

    - **Disable BitLocker on devices where TPM is incompatible**  
    CSP: [BitLocker - SystemDrivesRequireStartupAuthentication](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)

      If no TPM is present, BitLocker requires a password or USB drive for startup.

      This setting only applies when first enabling BitLocker and has no effect if BitLocker is already enabled.

      - **Not configured** (*default*)
      - **Yes** - Block BitLocker from being configured without a compatible TPM chip.

    - **Enable preboot recovery message and url**  
      CSP: [BitLocker - SystemDrivesRecoveryMessage](/windows/client-management/mdm/bitlocker-csp#systemdrivesrecoverymessage)configure

      - **Not configured** (*default*) – Use the default BitLocker pre-boot recovery information.
      - **Yes** – Enable the configuration of a custom pre-boot recovery message and URL to help your users understand how to find their recovery password. The pre-boot message and URL are seen by users when they're locked out of their PC in recovery mode.

      When set to *Yes* you can configure the following settings:

      - **Preboot recovery message**  
        Specify a custom pre-boot recovery message.

      - **Preboot recovery url**  
        Specify a custom pre-boot recovery URL.

    - **System drive recovery**  
      CSP: [BitLocker - SystemDrivesRecoveryOptions](/windows/client-management/mdm/bitlocker-csp#systemdrivesrecoveryoptions)

      - **Not configured** (*default*)  
      - **Configure** - Enable the configuration of additional settings.

      When set to *Configure* the following settings are available:

      - **User creation of recovery key**  
        - **Blocked** (*default*)
        - **Required**
        - **Allowed**

      - **Configure BitLocker recovery package**
        - **Password and Key** (*default*) - Include both the BitLocker recovery password that's used by admins and users to unlock protected drives, and recovery key packages that are used by admins for data recovery purposes) in Active Directory.
        - **Password only** - The recovery key packages might not be accessible when needed.

      - **Require device to back up recovery information to Azure Ad**
        - **Not configured** (*default*) - BitLocker enablement will complete even if recovery key backup to Azure AD fails. This can result in no recovery information being stored externally.
        - **Yes** - BitLocker won't complete enablement until recovery keys have been successfully saved to Azure Active Directory.

      - **User creation of recovery password**  
        - **Blocked** (*default*)
        - **Required**
        - **Allowed**

      - **Hide recovery options during BitLocker setup**
        - **Not configured** (*default*) - Allow the user to access extra recovery options.
        - **Yes** - Block the end user from choosing extra recovery options such as printing recovery keys during the BitLocker setup wizard.

      - **Enable BitLocker after recovery information to store**
        - **Not configured** (*default*)  
        - **Yes**

      - **Block the use of certificate-based data recovery agent (DRA)**
        - **Not configured** (*default*) - Allow the use of DRA to be set up. Setting up DRA requires an enterprise PKI and Group Policy Objects to deploy the DRA agent and certificates.
        - **Yes** - Block the ability to use Data Recovery Agent (DRA) to recover BitLocker enabled drives.

    - **Minimum PIN length**  
      CSP: [BitLocker - SystemDrivesMinimumPINLength](/windows/client-management/mdm/bitlocker-csp#systemdrivesminimumpinlength)

      Specify the minimum startup PIN length when TPM + PIN is required during BitLocker enablement. The PIN length must be between 4 and 20 digits.

      If you don't configure this setting, users can configure a startup PIN of any length (between 4 and 20 digits)

      This setting only applies when first enabling BitLocker and has no effect if BitLocker is already enabled.

  - **Configure encryption method for Operating System drives**  
   CSP: [BitLocker - EncryptionMethodByDriveType]( https://go.microsoft.com/fwlink/?linkid=872526)

    Configure the encryption method and cipher strength for OS drives. *XTS- AES 128-bit* is the Windows default encryption method and the recommended value.

    - **Not configured** (*default*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

### BitLocker - Removable Drive Settings

- **BitLocker removable drive policy**  
  CSP: [BitLocker - EncryptionMethodByDriveType](/windows/client-management/mdm/bitlocker-csp#encryptionmethodbydrivetype)

  - **Not configured** (*default*)  
  - **Configure**

  When set to *Configure* you can configure the following settings.

  - **Configure encryption method for removable data-drives**  
    CSP: [BitLocker - EncryptionMethodByDriveType](/windows/client-management/mdm/bitlocker-csp#encryptionmethodbydrivetype)

    Select the desired encryption method for removable data-drives disks.

    - **Not configured** (*default*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

  - **Block write access to removable data-drives not protected by BitLocker**  
    CSP: [BitLocker - RemovableDrivesRequireEncryption](/windows/client-management/mdm/bitlocker-csp#removabledrivesrequireencryption)

    - **Not configured** (*default*) - Data can be written to non-encrypted removable drives.
    - **Yes** - Windows doesn’t allow data to be written to removable drives that aren't BitLocker protected. If an inserted removable drive isn't encrypted, the user must complete the BitLocker setup wizard before write access is granted to drive.

    - **Block write access to removable data-drives not protected by BitLocker**  
      CSP: [BitLocker - RemovableDrivesRequireEncryption](/windows/client-management/mdm/bitlocker-csp#removabledrivesrequireencryption)

      - **Not configured** (*default*) - Any BitLocker encrypted drive can be used.
      - **Yes** - Block access to removable drives unless they were encrypted on a computer owned by your organization.

## Next steps

[Endpoint security policy for disk encryption](../protect/endpoint-security-disk-encryption-policy.md)
