---
title: BitLocker settings reference
titleSuffix: Configuration Manager
description: All of the BitLocker management settings available in Configuration Manager
ms.date: 04/12/2022
ms.service: configuration-manager
ms.subservice: protect
ms.topic: reference
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# BitLocker settings reference

*Applies to: Configuration Manager (current branch)*

<!-- 5925683 -->

BitLocker management policies in Configuration Manager contain the following policy groups:

- Setup
- Operating system drive
- Fixed drive
- Removable drive
- Client management

The following sections describe and suggest configurations for the settings in each group.

## Setup

The settings on this page configure global BitLocker encryption options.

### Drive encryption method and cipher strength

*Suggested configuration*: **Enabled** with the default or greater encryption method.

> [!NOTE]
> The **Setup** properties page includes two groups of settings for different versions of Windows. This section describes them both.

#### Windows 8.1 devices

For Windows 8.1 devices, enable the option for **Drive encryption method and cipher strength**, and select one of the following encryption methods:

- AES 128-bit with Diffuser
- AES 256-bit with Diffuser
- AES 128-bit (default)
- AES 256-bit

For more information on how to create this policy with Windows PowerShell, see [New-CMBLEncryptionMethodPolicy](/powershell/module/configurationmanager/new-cmblencryptionmethodpolicy).

#### Windows 10 or later devices

For Windows 10 or later devices, enable the option for **Drive encryption method and cipher strength (Windows 10 or later)**. Then individually select one of the following encryption methods for OS drives, fixed data drives, and removable data drives:

- AES-CBC 128-bit
- AES-CBC 256-bit
- XTS-AES 128-bit (default)
- XTS-AES 256-bit

> [!TIP]
> BitLocker uses Advanced Encryption Standard (AES) as its encryption algorithm with configurable key lengths of 128 or 256 bits. On Windows 10 or later devices, the AES encryption supports cipher block chaining (CBC) or ciphertext stealing (XTS).
>
> If you need to use a removable drive on devices that don't run Windows 10, use AES-CBC.

For more information on how to create this policy with Windows PowerShell, see [New-CMBLEncryptionMethodWithXts](/powershell/module/configurationmanager/new-cmblencryptionmethodwithxts).

#### General usage notes for drive encryption and cipher strength

- If you disable or don't configure these settings, BitLocker uses the default encryption method.

- Configuration Manager applies these settings when you turn on BitLocker.

- If the drive is already encrypted or is in progress, any change to these policy settings doesn't change the drive encryption on the device.

- If you use the default value, the BitLocker Computer Compliance report may display the cipher strength as **unknown**. To work around this issue, enable this setting and set an explicit value for cipher strength.

### Prevent memory overwrite on restart

*Suggested configuration*: **Not configured**

Configure this policy to improve restart performance without overwriting BitLocker secrets in memory on restart.

When you don't configure this policy, BitLocker removes its secrets from memory when the computer restarts.

For more information on how to create this policy with Windows PowerShell, see [New-CMNoOverwritePolicy](/powershell/module/configurationmanager/new-cmnooverwritepolicy).

### Validate smart card certificate usage rule compliance

*Suggested configuration*: **Not configured**

Configure this policy to use smartcard certificate-based BitLocker protection. Then specify the certificate **Object identifier**.

When you don't configure this policy, BitLocker uses the default object identifier `1.3.6.1.4.1.311.67.1.1` to specify a certificate.

For more information on how to create this policy with Windows PowerShell, see [New-CMScCompliancePolicy](/powershell/module/configurationmanager/new-cmsccompliancepolicy).

### Organization unique identifiers

*Suggested configuration*: **Not configured**

Configure this policy to use a certificate-based data recovery agent or the BitLocker To Go reader.

When you don't configure this policy, BitLocker doesn't use the **Identification** field.

If your organization requires higher security measurements, configure the **Identification** field. Set this field on all targeted USB devices, and align it with this setting.

For more information on how to create this policy with Windows PowerShell, see [New-CMUidPolicy](/powershell/module/configurationmanager/new-cmuidpolicy).

## OS drive

The settings on this page configure the encryption settings for the drive on which Windows is installed.

### Operating system drive encryption settings

*Suggested configuration*: **Enabled**

If you enable this setting, the user has to protect the OS drive, and BitLocker encrypts the drive. If you disable it, the user can't protect the drive. If you don't configure this policy, BitLocker protection isn't required on the OS drive.

> [!NOTE]
> If the drive is already encrypted, and you disable this setting, BitLocker decrypts the drive.  

If you have devices without a [Trusted Platform Module (TPM)](/windows/security/information-protection/tpm/trusted-platform-module-top-node), use the option to **Allow BitLocker without a compatible TPM (requires a password)**. This setting allows BitLocker to encrypt the OS drive, even if the device doesn't have a TPM. If you allow this option, Windows prompts the user to specify a BitLocker password.

On devices with a compatible TPM, two types of authentication methods can be used at startup to provide added protection for encrypted data. When the computer starts, it can use only the TPM for authentication, or it can also require the entry of a personal identification number (PIN). Configure the following settings:

- **Select protector for operating system drive**: Configure it to use a TPM and PIN, or just the TPM.

- **Configure minimum PIN length for startup**: If you require a PIN, this value is the shortest length the user can specify. The user enters this PIN when the computer boots to unlock the drive. By default, the minimum PIN length is `4`.

> [!TIP]
> For higher security, when you enable devices with TPM + PIN protector, consider *disabling* the following group policy settings in **System** > **Power Management** > **Sleep Settings**:
>
> - Allow Standby States (S1-S3) When Sleeping (Plugged In)
>
> - Allow Standby States (S1-S3) When Sleeping (On Battery)

For more information on how to create this policy with Windows PowerShell, see [New-CMBMSOSDEncryptionPolicy](/powershell/module/configurationmanager/new-cmbmsosdencryptionpolicy).

### Allow enhanced PINs for startup

*Suggested configuration*: **Not configured**

Configure BitLocker to use enhanced startup PINs. These PINs permit the use of more characters such as uppercase and lowercase letters, symbols, numbers, and spaces. This setting applies when you turn on BitLocker.

> [!IMPORTANT]
> Not all computers can support enhanced PINs in the pre-boot environment. Before you enable its use, evaluate whether your devices are compatible with this feature.

If you enable this setting, all new BitLocker startup PINs allow the user to create enhanced PINs.

- **Require ASCII-only PINs**: Help make enhanced PINs more compatible with computers that limit the type or number of characters that you can enter in the pre-boot environment.

If you disable or don't configure this policy setting, BitLocker doesn't use enhanced PINs.

For more information on how to create this policy with Windows PowerShell, see [New-CMEnhancedPIN](/powershell/module/configurationmanager/new-cmenhancedpin).

### Operating system drive password policy

*Suggested configuration*: **Not configured**

Use these settings to set the constraints for passwords to unlock BitLocker-protected OS drives. If you allow non-TPM protectors on OS drives, configure the following settings:

- **Configure password complexity for operating system drives**: To enforce complexity requirements on the password, select **Require password complexity**.

- **Minimum password length for operating system drive**: By default, the minimum length is `8`.

- **Require ASCII-only passwords for removable OS drives**

If you enable this policy setting, users can configure a password that meets the requirements that you define.

For more information on how to create this policy with Windows PowerShell, see [New-CMOSPassphrase](/powershell/module/configurationmanager/new-cmospassphrase).

#### General usage notes for OS drive password policy

- For these complexity requirement settings to be effective, also enable the group policy setting **Password must meet complexity requirements** in **Computer Configuration** > **Windows Settings** > **Security Settings** > **Account Policies** > **Password Policy**.

- BitLocker enforces these settings when you turn it on, not when you unlock a volume. BitLocker lets you unlock a drive with any of the protectors that are available on the drive.

- If you use group policy to enable FIPS-compliant algorithms for encryption, hashing, and signing, you can't allow passwords as a BitLocker protector.

### Reset platform validation data after BitLocker recovery

*Suggested configuration*: **Not configured**

Control whether Windows refreshes platform validation data when it starts after BitLocker recovery.

If you enable or don't configure this setting, Windows refreshes platform validation data in this situation.

If you disable this policy setting, Windows doesn't refresh platform validation data in this situation.

For more information on how to create this policy with Windows PowerShell, see [New-CMTpmAutoResealPolicy](/powershell/module/configurationmanager/new-cmtpmautoresealpolicy).

### Pre-boot recovery message and URL

*Suggested configuration*: **Not configured**

When BitLocker locks the OS drive, use this setting to display a custom recovery message or a URL on the pre-boot BitLocker recovery screen. This setting only applies to Windows 10 or later devices.

When you enable this setting, select one of the following options for the pre-boot recovery message:

- **Use default recovery message and URL**: Display the default BitLocker recovery message and URL in the pre-boot BitLocker recovery screen. If you previously configured a custom recovery message or URL, use this option to revert to the default message.

- **Use custom recovery message**: Include a custom message in the pre-boot BitLocker recovery screen.

  - **Custom recovery message option**: Type the custom message to display. If you also want to specify a recovery URL, include it as part of this custom recovery message. The maximum string length is 32,768 characters.

- **Use custom recovery URL**: Replace the default URL displayed in the pre-boot BitLocker recovery screen.

  - **Custom recovery URL option**: Type the URL to display. The maximum string length is 32,768 characters.

> [!NOTE]
> Not all characters and languages are supported in pre-boot. First test your custom message or URL to make sure it appears correctly on the pre-boot BitLocker recovery screen.

For more information on how to create this policy with Windows PowerShell, see [New-CMPrebootRecoveryInfo](/powershell/module/configurationmanager/new-cmprebootrecoveryinfo).

### Encryption policy enforcement settings (OS drive)

*Suggested configuration*: **Enabled**

Configure the number of days that users can postpone BitLocker compliance for the OS drive. The **Noncompliance grace period** begins when Configuration Manager first detects it as noncompliant. After this grace period expires, users can't postpone the required action or request an exemption.

If the encryption process requires user input, a dialog box appears in Windows that the user can't close until they provide the required information. Future notifications for errors or status won't have this restriction.

If BitLocker doesn't require user interaction to add a protector, after the grace period expires, BitLocker starts encryption in the background.

If you disable or don't configure this setting, Configuration Manager doesn't require users to comply with BitLocker policies.

To enforce the policy immediately, set a grace period of `0`.

For more information on how to create this policy with Windows PowerShell, see [New-CMUseOsEnforcePolicy](/powershell/module/configurationmanager/new-cmuseosenforcepolicy).

## Fixed drive

The settings on this page configure encryption for other data drives in a device.

### Fixed data drive encryption

*Suggested configuration*: **Enabled**

Manage your requirement for encryption of fixed data drives. If you enable this setting, BitLocker requires users to put all fixed data drives under protection. It then encrypts the data drives.

When you enable this policy, either enable auto-unlock or the settings for **Fixed data drive password policy**.

- **Configure auto-unlock for fixed data drive**: Allow or require BitLocker to automatically unlock any encrypted data drive. To use auto-unlock, also require BitLocker to encrypt the [OS drive](#os-drive).

If you don't configure this setting, BitLocker doesn't require users to put fixed data drives under protection.

If you disable this setting, users can't put their fixed data drives under BitLocker protection. If you disable this policy after BitLocker encrypts fixed data drives, BitLocker decrypts the fixed data drives.

For more information on how to create this policy with Windows PowerShell, see [New-CMBMSFDVEncryptionPolicy](/powershell/module/configurationmanager/new-cmbmsfdvencryptionpolicy).

### Deny write access to fixed drives not protected by BitLocker

*Suggested configuration*: **Not configured**

Require BitLocker protection for Windows to write data to fixed drives on the device. BitLocker applies this policy when you turn it on.

When you enable this setting:

- If BitLocker protects a fixed data drive, Windows mounts it with read and write access.

- For any fixed data drive that BitLocker doesn't protect, Windows mounts it as read-only.

When you don't configure this setting, Windows mounts all fixed data drives with read and write access.

For more information on how to create this policy with Windows PowerShell, see [New-CMFDVDenyWriteAccessPolicy](/powershell/module/configurationmanager/new-cmfdvdenywriteaccesspolicy).

### Fixed data drive password policy

*Suggested configuration*: **Not configured**

Use these settings to set the constraints for passwords to unlock BitLocker-protected fixed data drives.

If you enable this setting, users can configure a password that meets your defined requirements.

For higher security, enable this setting, and then configure the following settings:

- **Require password for fixed data drive**: Users have to specify a password to unlock a BitLocker-protected fixed data drive.

- **Configure password complexity for fixed data drives**: To enforce complexity requirements on the password, select **Require password complexity**.

- **Minimum password length for fixed data drive**: By default, the minimum length is `8`.

If you disable this setting, users can't configure a password.

When the policy isn't configured, BitLocker supports passwords with the default settings. The default settings don't include password complexity requirements, and require only eight characters.

For more information on how to create this policy with Windows PowerShell, see [New-CMFDVPassPhrasePolicy](/powershell/module/configurationmanager/new-cmfdvpassphrasepolicy).

#### General usage notes for fixed data drive password policy

- For these complexity requirement settings to be effective, also enable the group policy setting **Password must meet complexity requirements** in **Computer Configuration** > **Windows Settings** > **Security Settings** > **Account Policies** > **Password Policy**.

- BitLocker enforces these settings when you turn it on, not when you unlock a volume. BitLocker lets you unlock a drive with any of the protectors that are available on the drive.

- If you use group policy to enable FIPS-compliant algorithms for encryption, hashing, and signing, you can't allow passwords as a BitLocker protector.

### Encryption policy enforcement settings (fixed data drive)

*Suggested configuration*: **Enabled**

Configure the number of days that users can postpone BitLocker compliance for fixed data drives. The **Noncompliance grace period** begins when Configuration Manager first detects the fixed data drive as noncompliant. It doesn't enforce the fixed data drive policy until the OS drive is compliant. After the grace period expires, users can't postpone the required action or request an exemption.

If the encryption process requires user input, a dialog box appears in Windows that the user can't close until they provide the required information. Future notifications for errors or status won't have this restriction.

If BitLocker doesn't require user interaction to add a protector, after the grace period expires, BitLocker starts encryption in the background.

If you disable or don't configure this setting, Configuration Manager doesn't require users to comply with BitLocker policies.

To enforce the policy immediately, set a grace period of `0`.

For more information on how to create this policy with Windows PowerShell, see [New-CMUseFddEnforcePolicy](/powershell/module/configurationmanager/new-cmusefddenforcepolicy).

## Removable drive

The settings on this page configure encryption for removable drives, such as USB keys.

### Removable data drive encryption

*Suggested configuration*: **Enabled**

This setting controls the use of BitLocker on removable drives.

- **Allow users to apply BitLocker protection on removable data drives**: Users can turn on BitLocker protection for a removable drive.

- **Allow users to suspend and decrypt BitLocker on removable data drives**: Users can remove or temporarily suspend BitLocker drive encryption from a removable drive.

When you enable this setting, and allow users to apply BitLocker protection, the Configuration Manager client saves recovery information about removable drives to the recovery service on the management point. This behavior allows users to recover the drive if they forget or lose the protector (password).

When you enable this setting:

- Enable the settings for **Removable data drive password policy**

- *Disable* the following group policy settings in **System** > **Removable Storage Access** for both user & computer configurations:

  - **All removable storage classes: Deny all access**
  - **Removable disks: Deny write access**
  - **Removable disks: Deny read access**

If you disable this setting, users can't use BitLocker on removable drives.

For more information on how to create this policy with Windows PowerShell, see [New-CMRDVConfigureBDEPolicy](/powershell/module/configurationmanager/new-cmrdvconfigurebdepolicy).

### Deny write access to removable drives not protected by BitLocker

*Suggested configuration*: **Not configured**

Require BitLocker protection for Windows to write data to removable drives on the device. BitLocker applies this policy when you turn it on.

When you enable this setting:

- If BitLocker protects a removable drive, Windows mounts it with read and write access.

- For any removable drive that BitLocker doesn't protect, Windows mounts it as read-only.

- If you enable the option to **Deny write access to devices configured in another organization**, BitLocker only gives write access to removable drives with identification fields that match the allowed identification fields. Define these fields with the **Organization unique identifiers** global settings on the [Setup](#setup) page.

When you disable or don't configure this setting, Windows mounts all removable drives with read and write access.

> [!NOTE]
> You can override this setting with the group policy settings in **System** > **Removable Storage Access**. If you enable the group policy setting **Removable disks: Deny write access**, then BitLocker ignores this Configuration Manager setting.

For more information on how to create this policy with Windows PowerShell, see [New-CMRDVDenyWriteAccessPolicy](/powershell/module/configurationmanager/new-cmrdvdenywriteaccesspolicy).

### Removable data drive password policy

*Suggested configuration*: **Enabled**

Use these settings to set the constraints for passwords to unlock BitLocker-protected removable drives.

If you enable this setting, users can configure a password that meets your defined requirements.

For higher security, enable this setting, and then configure the following settings:

- **Require password for removable data drive**: Users have to specify a password to unlock a BitLocker-protected removable drive.

- **Configure password complexity for removable data drives**: To enforce complexity requirements on the password, select **Require password complexity**.

- **Minimum password length for removable data drive**: By default, the minimum length is `8`.

If you disable this setting, users can't configure a password.

When the policy isn't configured, BitLocker supports passwords with the default settings. The default settings don't include password complexity requirements, and require only eight characters.

For more information on how to create this policy with Windows PowerShell, see [New-CMRDVPassPhrasePolicy](/powershell/module/configurationmanager/new-cmrdvpassphrasepolicy).

#### General usage notes for removable data drive password policy

- For these complexity requirement settings to be effective, also enable the group policy setting **Password must meet complexity requirements** in **Computer Configuration** > **Windows Settings** > **Security Settings** > **Account Policies** > **Password Policy**.

- BitLocker enforces these settings when you turn it on, not when you unlock a volume. BitLocker lets you unlock a drive with any of the protectors that are available on the drive.

- If you use group policy to enable FIPS-compliant algorithms for encryption, hashing, and signing, you can't allow passwords as a BitLocker protector.

## Client management

The settings on this page configure BitLocker management services and clients.

### BitLocker Management Services

*Suggested configuration*: **Enabled**

When you enable this setting, Configuration Manager automatically and silently backs up key recovery information in the site database. If you disable or don't configure this setting, Configuration Manager doesn't save key recovery information.

- **Select BitLocker recovery information to store**: Configure the key recovery service to back up BitLocker recovery information. It provides an administrative method of recovering data encrypted by BitLocker, which helps prevent data loss because of the lack of key information.

- **Allow recovery information to be stored in plain text**: Without a BitLocker management encryption certificate for SQL Server, Configuration Manager stores the key recovery information in plain text. For more information, see [Encrypt recovery data in the database](../../deploy-use/bitlocker/encrypt-recovery-data.md).

- **Client checking status frequency (minutes)**: At the configured frequency, the client checks the BitLocker protection policies and status on the computer and also backs up the client recovery key. By default, the Configuration Manager client checks BitLocker status every 90 minutes.

    > [!IMPORTANT]
    > Don't set this value to less than 60. A smaller frequency value may cause the client to briefly report inaccurate compliance states.<!-- 13901360 -->

For more information on how to create these policies with Windows PowerShell, see:

- [Set-CMBlmPlaintextStorage](/powershell/module/configurationmanager/set-cmblmplaintextstorage)
- [New-CMBMSClientConfigureCheckIntervalPolicy](/powershell/module/configurationmanager/new-cmbmsclientconfigurecheckintervalpolicy)

### User exemption policy

*Suggested configuration*: **Not configured**

Configure a contact method for users to request an exemption from BitLocker encryption.

If you enable this policy setting, provide the following information:

- **Maximum days to postpone**: How many days the user can postpone an enforced policy. By default, this value is `7` days (one week).

- **Contact method**: Specify how users can request an exemption: URL, email address, or phone number.

- **Contact**: Specify the URL, email address, or phone number. When a user requests an exemption from BitLocker protection, they see a Windows dialog box with instructions on how to apply. Configuration Manager doesn't validate the information you enter.

  - **URL**: Use the standard URL format, `https://website.domain.tld`. Windows displays the URL as a hyperlink.

  - **Email address**: Use the standard email address format, `user@domain.tld`. Windows displays the address as the following hyperlink: `mailto:user@domain.tld?subject=Request exemption from BitLocker protection`.

  - **Phone number**: Specify the number you want your users to call. Windows displays the number with the following description: `Please call <your number> for applying exemption`.

If you disable or don't configure this setting, Windows doesn't display the exemption request instructions to users.

> [!NOTE]
> BitLocker manages exemptions per user, not per computer. If multiple users sign in to the same computer, and any one user isn't exempt, BitLocker encrypts the computer.

For more information on how to create this policy with Windows PowerShell, see [New-CMBMSUserExemptionPolicy](/powershell/module/configurationmanager/new-cmbmsuserexemptionpolicy).

### URL for the security policy link

*Suggested configuration*: **Enabled**

Specify a URL to display to users as the **Company Security Policy** in Windows. Use this link to provide users with information about encryption requirements. It shows when BitLocker prompts the user to encrypt a drive.

If you enable this setting, configure the **security policy link URL**.

If you disable or don't configure this setting, BitLocker doesn't show the security policy link.

For more information on how to create this policy with Windows PowerShell, see [New-CMMoreInfoUrlPolicy](/powershell/module/configurationmanager/new-cmmoreinfourlpolicy).

## Next steps

If you use Windows PowerShell to create these policy objects, then use the [New-CMBlmSetting](/powershell/module/configurationmanager/new-cmblmsetting) cmdlet. This cmdlet creates a BitLocker management policy settings object that contains all of the specified policies. To deploy the policy settings to a collection, use the [New-CMSettingDeployment](/powershell/module/configurationmanager/new-cmsettingdeployment) cmdlet.
