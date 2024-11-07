---
# required metadata

title: Windows compliance settings in Microsoft Intune
description: See a list of all the settings you can use when setting compliance for your Windows 10, Windows 11, Windows Holographic, and Surface Hub devices in Microsoft Intune. Check for compliance on the minimum and maximum operating system, set password restrictions and length, check for partner anti-virus (AV) solutions, enable encryption on data storage, and more.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 6/18/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
- compliance
- sub-device-compliance
---

# Device Compliance settings for Windows 10/11 in Intune

This article lists and describes the different compliance settings you can configure on Windows devices in Intune. As part of your mobile device management (MDM) solution, use these settings to require BitLocker, set a minimum and maximum operating system, set a risk level using Microsoft Defender for Endpoint, and more.

This feature applies to:

- Windows 10/11
- Windows Holographic for Business
- Surface Hub

As an Intune administrator, use these compliance settings to help protect your organizational resources. To learn more about compliance policies, and what they do, see [get started with device compliance](device-compliance-get-started.md).

## Before you begin

[Create a compliance policy](create-compliance-policy.md#create-the-policy). For **Platform**, select **Windows 10 and later**.

## Device health
To ensure devices boot to a trusted state, Intune utilizes Microsoft device attestation services.  Devices across Intune commercial, US Government GCC High, and DoD services running Windows 10 use the Device Health Attestation (DHA) service. 

For more information, see:  

- [Device Health Attestation](/windows-server/security/device-health-attestation)  
  
### Windows Health Attestation Service evaluation rules

- **Require BitLocker**:  
   Windows BitLocker Drive Encryption encrypts all data stored on the Windows operating system volume. BitLocker uses the Trusted Platform Module (TPM) to help protect the Windows operating system and user data. It also helps confirm that a computer isn't tampered with, even if its left unattended, lost, or stolen. If the computer is equipped with a compatible TPM, BitLocker uses the TPM to lock the encryption keys that protect the data. As a result, the keys can't be accessed until the TPM verifies the state of the computer.  

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - The device can protect data that's stored on the drive from unauthorized access when the system is off, or hibernates.
  
  [Device HealthAttestation CSP - BitLockerStatus](/windows/client-management/mdm/healthattestation-csp)
  
  > [!NOTE]
  > If using a device compliance policy in Intune, be aware that the state of this setting is only measured at boot time. Therefore, even although BitLocker encryption may have completed - a reboot will be required in order for the device detect this and become compliant. For more information, see the following Microsoft support blog on [Device Health Attestation](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-device-health-attestation-settings-as-part-of/ba-p/282643).
  
- **Require Secure Boot to be enabled on the device**:  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - The system is forced to boot to a factory trusted state. The core components that are used to boot the machine must have correct cryptographic signatures that are trusted by the organization that manufactured the device. The UEFI firmware verifies the signature before it lets the machine start. If any files are tampered with, which breaks their signature, the system doesn't boot.

  > [!NOTE]
  > The **Require Secure Boot to be enabled on the device** setting is supported on some TPM 1.2 and 2.0 devices. For devices that don't support TPM 2.0 or later, the policy status in Intune shows as **Not Compliant**. For more information on supported versions, see  [Device Health Attestation](/windows/security/information-protection/tpm/trusted-platform-module-overview#device-health-attestation).

- **Require code integrity**:  
  Code integrity is a feature that validates the integrity of a driver or system file each time it's loaded into memory.
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Require code integrity, which detects if an unsigned driver or system file is being loaded into the kernel. It also detects if a system file is changed by malicious software or run by a user account with administrator privileges.

For more information, see:  

- For details about how the Health Attestation service works, see [Health Attestation CSP](/windows/client-management/mdm/healthattestation-csp).  
- [Support Tip: Using Device Health Attestation Settings as Part of Your Intune Compliance Policy](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Using-Device-Health-Attestation-Settings-as-Part-of/ba-p/282643).  

## Device Properties

### Operating System Version

To discover build versions for all Windows 10/11 Feature Updates and Cumulative Updates (to be used in some of the fields below), see [Windows release information](/windows/release-information). Be sure to include the appropriate version prefix before the build numbers, like 10.0 for Windows 10 as the following examples illustrate.

- **Minimum OS version**:  
  Enter the minimum allowed version in the **major.minor.build.revision number** format. To get the correct value, open a command prompt, and type `ver`. The `ver` command returns the version in the following format:

  `Microsoft Windows [Version 10.0.17134.1]`

  When a device has an earlier version than the OS version you enter, it's reported as noncompliant. A link with information on how to upgrade is shown. The end user can choose to upgrade their device. After they upgrade, they can access company resources.

- **Maximum OS version**:  
  Enter the maximum allowed version, in the **major.minor.build.revision number** format. To get the correct value, open a command prompt, and type `ver`. The `ver` command returns the version in the following format:

  `Microsoft Windows [Version 10.0.17134.1]`

  When a device is using an OS version later than the version entered, access to organization resources is blocked. The end user is asked to contact their IT administrator. The device can't access organization resources until the rule is changed to allow the OS version.

- **Minimum OS required for mobile devices**:  
  Enter the minimum allowed version, in the major.minor.build number format.

  When a device has an earlier version that the OS version you enter, it's reported as noncompliant. A link with information on how to upgrade is shown. The end user can choose to upgrade their device. After they upgrade, they can access company resources.

- **Maximum OS required for mobile devices**:  
  Enter the maximum allowed version, in the major.minor.build number.

  When a device is using an OS version later than the version entered, access to organization resources is blocked. The end user is asked to contact their IT administrator. The device can't access organization resources until the rule is changed to allow the OS version.

- **Valid operating system builds**:  
  Specify a list of minimum and maximum operating system builds. Valid operating system builds provides additional flexibility when compared against minimum and maximum OS versions. Consider a scenario where minimum OS version is set to 10.0.18362.xxx (Windows 10 1903) and maximum OS version is set to 10.0.18363.xxx (Windows 10 1909). This configuration can allow a Windows 10 1903 device that doesn't have recent cumulative updates installed to be identified as compliant. Minimum and maximum OS versions might be suitable if you have standardized on a single Windows 10 release, but might not address your requirements if you need to use multiple builds, each with specific patch levels. In such a case, consider leveraging valid operating system builds instead, which allows multiple builds to be specified as per the following example.

  The largest supported value for each of the version, major, minor, and build fields is 65535. For example, the largest value you can enter is 65535.65535.65535.65535.

  **Example**:  
  The following table is an example of a range for the acceptable operating systems versions for different Windows 10 releases. In this example, three different Feature Updates have been allowed (1809, 1909 and 2004). Specifically, only those versions of Windows and which have applied cumulative updates from June to September 2020 will be considered to be compliant. This is sample data only. The table includes a first column that includes any text you want to describe the entry, followed by the minimum and maximum OS version for that entry. The second and third columns must adhere to valid OS build versions in the **major.minor.build.revision number** format. After you define one or more entries, you can **Export** the list as a comma-separated values (CSV) file.  

  | Description                 | Minimum OS version | Maximum OS version |
  |-----------------------------|--------------------|--------------------|
  | Win 10 2004 (Jun-Sept 2020) | 10.0.19041.329     | 10.0.19041.508     |
  | Win 10 1909 (Jun-Sept 2020) | 10.0.18363.900     | 10.0.18363.1110    |
  | Win 10 1809 (Jun-Sept 2020) | 10.0.17763.1282    | 10.0.17763.1490    |

  > [!NOTE]
  > If you specify multiple ranges of OS version builds in your policy, and a device has a build outside of the compliant ranges, Company Portal will notify the device user that the device is noncompliant with this setting. However, be aware that due to technical limitations, the compliance remediation message only shows the first OS version range specified in the policy. We recommend that you document the acceptable OS version ranges for managed devices in your organization.  
  
## Configuration Manager Compliance

Applies only to co-managed devices running Windows 10/11. Intune-only devices return a not available status.

- **Require device compliance from Configuration Manager**:  
  - **Not configured** (*default*) - Intune doesn't check for any of the Configuration Manager settings for compliance.
  - **Require** - Require all settings (configuration items) in Configuration Manager to be compliant.

## System Security

### Password

- **Require a password to unlock mobile devices**:  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Users must enter a password before they can access their device. 

- **Simple passwords**:  
  - **Not configured** (*default*) - Users can create simple passwords, such as **1234** or **1111**.
  - **Block** - Users can't create simple passwords, such as **1234** or **1111**.

- **Password type**:  
  Choose the type of password or PIN required. Your options:
  - **Device default** (*default*) - Require a password, numeric PIN, or alphanumeric PIN
  - **Numeric** - Require a password or numeric PIN
  - **Alphanumeric** - Require a password, or alphanumeric PIN.  
  
  When set to *Alphanumeric*, the following settings are available:  
  - **Password complexity**:  
    Your options:
    - **Require digits and lowercase letters** (*default*)
    - **Require digits, lowercase letters, and uppercase letters**
    - **Require digits, lowercase letters, uppercase letters, and special characters**

    > [!TIP]
    > The Alphanumeric password policies can be complex. We encourage administrators to read the CSPs for more information:
    >
    > - [DeviceLock/AlphanumericDevicePasswordRequired CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)
    > - [DeviceLock/MinDevicePasswordComplexCharacters CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordcomplexcharacters)

- **Minimum password length**:  
  Enter the minimum number of digits or characters that the password must have.

- **Maximum minutes of inactivity before password is required**:  
  Enter the idle time before the user must reenter their password.

- **Password expiration (days)**:  
  Enter the number of days before the password expires, and they must create a new one, from 1-730.

- **Number of previous passwords to prevent reuse**:  
  Enter the number of previously used passwords that can't be used.

- **Require password when device returns from idle state (Mobile and Holographic)**:  
  - **Not configured** (*default*)
  - **Require** - Require device users to enter the password every time the device returns from an idle state.

  > [!IMPORTANT]
  > When the password requirement is changed on a Windows desktop, users are impacted the next time they sign in, as that's when the device goes from idle to active. Users with passwords that meet the requirement are still prompted to change their passwords.

### Encryption

- **Encryption of data storage on a device**:  
  This setting applies to all drives on a device.
  - **Not configured** (*default*)
  - **Require** - Use *Require* to encrypt data storage on your devices.
  
   [DeviceStatus CSP - DeviceStatus/Compliance/EncryptionCompliance](/windows/client-management/mdm/devicestatus-csp)

  > [!NOTE]
  > The **Encryption of data storage on a device** setting generically checks for the presence of encryption on the device, more specifically at the OS drive level. Currently, Intune supports only the encryption check with BitLocker. For a more robust encryption setting, consider using **Require BitLocker**, which leverages Windows Device Health Attestation to validate BitLocker status at the TPM level. However, when leveraging this setting, be aware that a reboot may be required before the device will reflect as compliant.

### Device Security  

- **Firewall**:  
  - **Not configured** (*default*) - Intune doesn't control the Windows Firewall, nor change existing settings.
  - **Require** - Turn on the Windows Firewall, and prevent users from turning it off.

  [Firewall CSP](/windows/client-management/mdm/firewall-csp)

  > [!NOTE]
  > - If the device immediately syncs after a reboot, or immediately syncs waking from sleep, then this setting may report as an **Error**. This scenario might not affect the overall device compliance status. To re-evaluate the compliance status, manually [sync the device](../user-help/sync-your-device-manually-windows.md).
  >
  > - If a configuration is applied (for example, via a group policy) to a device that configures Windows Firewall to allow all inbound traffic, or turns off the firewall, setting **Firewall** to **Require** will return **Not compliant**, even if Intune device configuration policy turns Firewall on. This is because the group policy object overrides the Intune policy. To fix this issue, we recommend that you remove any conflicting group policy settings, or that you migrate your Firewall-related group policy settings to Intune device configuration policy. In general, we recommend that you [keep default settings](/windows/security/threat-protection/windows-firewall/best-practices-configuring#keep-default-settings), including blocking inbound connections. For more information, see [Best practices for configuring Windows Firewall](/windows/security/threat-protection/windows-firewall/best-practices-configuring).

- **Trusted Platform Module (TPM)**:  
  - **Not configured** (*default*) -  Intune doesn't check the device for a TPM chip version.
  - **Require** - Intune checks the TPM chip version for compliance. The device is compliant if the TPM chip version is greater than **0** (zero). The device isn't compliant if there isn't a TPM version on the device.

  [DeviceStatus CSP - DeviceStatus/TPM/SpecificationVersion](/windows/client-management/mdm/devicestatus-csp)
  
- **Antivirus**:  
  - **Not configured** (*default*) - Intune doesn't check for any antivirus solutions installed on the device.
  - **Require** - Check compliance using antivirus solutions that are registered with [Windows Security Center](https://blogs.windows.com/windowsexperience/2017/01/23/introducing-windows-defender-security-center/), such as Symantec and Microsoft Defender.
    When set to Require, a device that has its Antivirus software disabled or out of date is noncompliant.

  [DeviceStatus CSP - DeviceStatus/Antivirus/Status](/windows/client-management/mdm/devicestatus-csp)

- **Antispyware**:  
  - **Not configured** (*default*) - Intune doesn't check for any antispyware solutions installed on the device.
  - **Require** - Check compliance using antispyware solutions that are registered with [Windows Security Center](https://blogs.windows.com/windowsexperience/2017/01/23/introducing-windows-defender-security-center/), such as Symantec and Microsoft Defender.
    When set to Require, a device that has its antimalware software disabled or out of date is noncompliant.

  [DeviceStatus CSP - DeviceStatus/Antispyware/Status](/windows/client-management/mdm/devicestatus-csp)

### Defender

*The following compliance settings are supported with Windows 10/11 Desktop.*

- **Microsoft Defender Antimalware**:  
  - **Not configured** (*default*) - Intune doesn't control the service, nor change existing settings.
  - **Require** - Turn on the Microsoft Defender anti-malware service, and prevent users from turning it off.

- **Microsoft Defender Antimalware minimum version**:  
  Enter the minimum allowed version of Microsoft Defender anti-malware service. For example, enter `4.11.0.0`. When left blank, any version of the Microsoft Defender anti-malware service can be used.

  *By default, no version is configured*.

- **Microsoft Defender Antimalware security intelligence up-to-date**:  
  Controls the Windows Security virus and threat protection updates on the devices.
  - **Not configured** (*default*) - Intune doesn't enforce any requirements.
  - **Require** - Force the Microsoft Defender security intelligence be up-to-date.

  [Defender CSP - Defender/Health/SignatureOutOfDate CSP](/windows/client-management/mdm/defender-csp)
  
  For more information, see [Security intelligence updates for Microsoft Defender Antivirus and other Microsoft antimalware](https://www.microsoft.com/en-us/wdsi/defenderupdates).

- **Real-time protection**:  
  - **Not configured** (*default*) - Intune doesn't control this feature, nor change existing settings.
  - **Require** - Turn on real-time protection, which scans for malware, spyware, and other unwanted software.  

  [Policy CSP - Defender/AllowRealtimeMonitoring CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

## Microsoft Defender for Endpoint

### Microsoft Defender for Endpoint rules

For additional information on Microsoft Defender for Endpoint integration in conditional access scenarios, see [Configure Conditional Access in Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/configure-conditional-access).

- **Require the device to be at or under the machine risk score**:  
  Use this setting to take the risk assessment from your defense threat services as a condition for compliance. Choose the maximum allowed threat level:
  - **Not configured** (*default*)  
  - **Clear** -This option is the most secure, as the device can't have any threats. If the device is detected as having any level of threats, it's evaluated as non-compliant.
  - **Low** - The device is evaluated as compliant if only low-level threats are present. Anything higher puts the device in a non-compliant status.
  - **Medium** - The device is evaluated as compliant if existing threats on the device are low or medium level. If the device is detected to have high-level threats, it's determined to be non-compliant.
  - **High** - This option is the least secure, and allows all threat levels. It may be useful if you're using this solution only for reporting purposes.
  
  To set up Microsoft Defender for Endpoint as your defense threat service, see [Enable Microsoft Defender for Endpoint with Conditional Access](advanced-threat-protection.md).

## Windows Subsystem for Linux (WSL)

These settings require the Intune WSL plug-in. For additional information, see [Evaluate compliance for Windows Subsystem for Linux](compliance-wsl.md). 

- **Allowed Linux distributions and versions** - Specify at least one Linux distribution name and optionally, a minimum or maximum OS version.
  > [!NOTE]
  > The provided distribution names and versions affect the compliance policy as follows:
  > - If no distribution is listed, all distributions are allowed (default).
  > - If only distribution names are provided, any installed version of that distribution are allowed. 
  > - If a distribution name and a minimum OS version are provided, installed distributions with the provided name and at least the  provided version number or higher are allowed.
  > - If a distribution name and a maximum OS version are provided, installed distributions with the provided name and up to the provided version number are allowed.
  > - If a distribution name, a minimum OS version and a maximum OS version are provided, installed distributions and OS version numbers within the provided range are allowed. 


## Windows Holographic for Business

Windows Holographic for Business uses the **Windows 10 and later** platform. Windows Holographic for Business supports the following setting:

- **System Security** > **Encryption** > **Encryption of data storage on device**.

To verify device encryption on the Microsoft HoloLens, see [Verify device encryption](/hololens/security-encryption-data-protection).

## Surface Hub

Surface Hub uses the **Windows 10 and later** platform. Surface Hubs are supported for both compliance and Conditional Access. To enable these features on Surface Hubs, we recommend you [enable Windows automatic enrollment](../enrollment/windows-enroll.md) in Intune (requires Microsoft Entra ID), and target the Surface Hub devices as device groups. Surface Hubs are required to be Microsoft Entra joined for compliance and Conditional Access to work.

For guidance, see [set up enrollment for Windows devices](../enrollment/windows-enroll.md).

**Special consideration for Surface Hubs running Windows 10/11 Team OS**:  
Surface Hubs that run Windows 10/11 Team OS do not support the Microsoft Defender for Endpoint and Password compliance policies at this time. Therefore, for Surface Hubs that run Windows 10/11 Team OS set the following two settings to their default of *Not configured*:

- In the category [Password](#password), set **Require a password to unlock mobile devices** to the default of *Not configured*.

- In the category [Microsoft Defender for Endpoint](#microsoft-defender-for-endpoint), set **Require the device to be at or under the machine risk score** to the default of *Not configured*.

## Next steps

- [Add actions for noncompliant devices](actions-for-noncompliance.md) and [use scope tags to filter policies](../fundamentals/scope-tags.md).
- [Monitor your compliance policies](compliance-policy-monitor.md).
- See the [compliance policy settings for Windows 8.1](compliance-policy-create-windows-8-1.md) devices.
