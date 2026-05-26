---
title: Windows compliance settings in Microsoft Intune
description: See a list of all the settings you can use when setting compliance for your Windows, Windows Holographic, and Surface Hub devices in Microsoft Intune. Check for compliance on the minimum and maximum operating system, set password restrictions and length, check for partner anti-virus (AV) solutions, enable encryption on data storage, and more.
ms.date: 11/19/2024
ms.topic: reference
ms.reviewer: tycast
ms.collection:
- M365-identity-device-management
- compliance
- sub-device-compliance
---

# Device compliance settings for Windows in Intune

This article lists and describes the different compliance settings you can configure on Windows devices in Intune. As part of your mobile device management (MDM) solution, use these settings to require BitLocker, set a minimum and maximum operating system, set a risk level using Microsoft Defender for Endpoint, and more.

This feature applies to:

- Windows 
- Windows Holographic for Business
- Surface Hub

Settings in this article are organized by the sections that appear in the admin center when you create a compliance policy.

## Before you begin

[Create a compliance policy](./create-policy.md#create-the-policy). For **Platform**, select **Windows 10 and later**.

## Device health
To ensure devices boot to a trusted state, Intune uses Microsoft device attestation services. Devices across Intune commercial, US Government GCC High, and DoD services running Windows 10 use the Device Health Attestation (DHA) service.

For more information, see:

- [Device Health Attestation](/windows-server/security/device-health-attestation)

### Windows Health Attestation Service evaluation rules

- **Require BitLocker**:
   Windows BitLocker Drive Encryption encrypts all data stored on the Windows operating system volume. BitLocker uses the Trusted Platform Module (TPM) to help protect the Windows operating system and user data. It also helps confirm that a computer isn't tampered with, even if its left unattended, lost, or stolen. If the computer is equipped with a compatible TPM, BitLocker uses the TPM to lock the encryption keys that protect the data. As a result, the keys can't be accessed until the TPM verifies the state of the computer.

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - The device can protect data that's stored on the drive from unauthorized access when the system is off, or hibernates.

  [Device HealthAttestation CSP - BitLockerStatus](/windows/client-management/mdm/healthattestation-csp)

  > [!NOTE]
  > If using a device compliance policy in Intune, be aware that the state of this setting is only measured at boot time. Therefore, even though BitLocker encryption may have completed – a reboot will be required in order for the device to detect this and become compliant. For more information, see the following Microsoft support blog on [Device Health Attestation](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-device-health-attestation-settings-as-part-of/ba-p/282643).

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

## Device properties

### Operating system version

To discover build versions for all Windows Feature Updates and Cumulative Updates (to be used in some of the fields below), see [Windows release information](/windows/release-information). Be sure to include the appropriate version prefix before the build numbers, like 11.0 for Windows 11.

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

  When a device has an earlier version than the OS version you enter, it's reported as noncompliant. A link with information on how to upgrade is shown. The end user can choose to upgrade their device. After they upgrade, they can access company resources.

- **Maximum OS required for mobile devices**:  
  Enter the maximum allowed version, in the major.minor.build number.

  When a device is using an OS version later than the version entered, access to organization resources is blocked. The end user is asked to contact their IT administrator. The device can't access organization resources until the rule is changed to allow the OS version.

- **Valid operating system builds**:  
  Specify a list of minimum and maximum OS build ranges. This setting offers more flexibility than **Minimum OS version** and **Maximum OS version**. Use it when you need to enforce specific patch levels across multiple Windows releases.

  Each entry requires a description and a minimum and maximum OS version in **major.minor.build.revision** format. The largest supported value for each field is 65535 (for example, 65535.65535.65535.65535). After you define one or more entries, you can **Export** the list as a CSV file.

  **Example**:

  | Description                    | Minimum OS version | Maximum OS version |
  |--------------------------------|--------------------|--------------------|
  | Windows 11 24H2 (Oct–Dec 2024) | 10.0.26100.1742    | 10.0.26100.2605    |
  | Windows 11 23H2 (Jul–Oct 2024) | 10.0.22631.3880    | 10.0.22631.4317    |
  | Windows 10 22H2 (Jul–Oct 2024) | 10.0.19045.4651    | 10.0.19045.5011    |

  > [!NOTE]
  > If you specify multiple ranges of OS version builds in your policy, and a device has a build outside of the compliant ranges, Company Portal will notify the device user that the device is noncompliant with this setting. However, be aware that due to technical limitations, the compliance remediation message only shows the first OS version range specified in the policy. We recommend that you document the acceptable OS version ranges for managed devices in your organization.

## Configuration Manager Compliance

Applies only to co-managed devices running Windows. Intune-only devices return a not available status.

- **Require device compliance from Configuration Manager**:
  - **Not configured** (*default*) - Intune doesn't check for any of the Configuration Manager settings for compliance.
  - **Require** - Require all settings (configuration items) in Configuration Manager to be compliant.

## System security

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

### Device security

- **Firewall**:
  - **Not configured** (*default*) - Intune doesn't control the Windows Firewall, nor change existing settings.
  - **Require** - Turn on the Windows Firewall, and prevent users from turning it off.

  [Firewall CSP](/windows/client-management/mdm/firewall-csp)

  > [!NOTE]
  > - If the device immediately syncs after a reboot, or immediately syncs waking from sleep, then this setting may report as an **Error**. This scenario might not affect the overall device compliance status. To re-evaluate the compliance status, manually [sync the device](../../user-help/device-actions/sync-device-windows.md).
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

*The following compliance settings are supported with Windows.*  

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

For additional information on Microsoft Defender for Endpoint integration in Conditional Access scenarios, see [Configure Conditional Access in Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/configure-conditional-access).

- **Require the device to be at or under the machine risk score**:  
  Use this setting to take the risk assessment from your defense threat services as a condition for compliance. Choose the maximum allowed threat level:
  - **Not configured** (*default*)
  - **Clear** - This option is the most secure, as the device can't have any threats. If the device is detected as having any level of threats, it's evaluated as noncompliant.
  - **Low** - The device is evaluated as compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.
  - **Medium** - The device is evaluated as compliant if existing threats on the device are low or medium level. If the device is detected to have high-level threats, it's determined to be noncompliant.
  - **High** - This option is the least secure, and allows all threat levels. It may be useful if you're using this solution only for reporting purposes.

  To set up Microsoft Defender for Endpoint as your defense threat service, see [Enable Microsoft Defender for Endpoint with Conditional Access](../microsoft-defender/overview.md).

## Windows Subsystem for Linux

The settings in this section require the Windows Subsystem for Linux (WSL) plug-in. For more information, see [Evaluate compliance for Windows Subsystem for Linux](./configure-wsl.md).

For **Allowed Linux distributions and versions**, enter at least one Linux distribution name. Optionally, enter a minimum or maximum OS version.

  > [!NOTE]
  > The distribution names and versions you enter affect the compliance policy in the following ways:
  > - If no distribution is provided, all distributions are allowed. This is the default behavior.
  > - If only distribution names are provided, all installed versions of that distribution are allowed.
  > - If a distribution name and a minimum OS version are provided, all installed distributions with the provided name and minimum version or later are allowed.
  > - If a distribution name and a maximum OS version are provided, all installed distributions with the provided name and maximum version or earlier are allowed.
  > - If a distribution name, a minimum OS version, and a maximum OS version are provided, all installed distributions and OS versions within the provided range are allowed.


## Windows Holographic for Business

Windows Holographic for Business uses the **Windows 10 and later** platform. Windows Holographic for Business supports the following setting:

- **System Security** > **Encryption** > **Encryption of data storage on device**.

To verify device encryption on the Microsoft HoloLens, see [Verify device encryption](/hololens/security-encryption-data-protection).

## Surface Hub

Surface Hub uses the **Windows 10 and later** platform. Surface Hubs are supported for both compliance and Conditional Access. To enable these features on Surface Hubs, we recommend you [enable Windows automatic enrollment](../../device-enrollment/windows/enable-automatic-mdm.md) in Intune (requires Microsoft Entra ID), and target the Surface Hub devices as device groups. Surface Hubs are required to be Microsoft Entra joined for compliance and Conditional Access to work.

For guidance, see [set up enrollment for Windows devices](../../device-enrollment/windows/enable-automatic-mdm.md).

**Special consideration for Surface Hubs running Windows Team OS**:  
Surface Hubs that run Windows Team OS do not support the Microsoft Defender for Endpoint and Password compliance policies at this time. Therefore, for Surface Hubs that run Windows Team OS set the following two settings to their default of *Not configured*:

- In the category [Password](#password), set **Require a password to unlock mobile devices** to the default of *Not configured*.

- In the category [Microsoft Defender for Endpoint](#microsoft-defender-for-endpoint), set **Require the device to be at or under the machine risk score** to the default of *Not configured*.

## Next steps

- [Add actions for noncompliant devices](./configure-noncompliance-actions.md) and [use scope tags to filter policies](../../fundamentals/role-based-access-control/scope-tags.md).
- [Monitor your compliance policies](./monitor-policy.md).
- See the [compliance policy settings for Windows 8.1](./ref-windows-8-1-settings.md) devices.
