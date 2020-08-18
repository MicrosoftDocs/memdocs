---
title: Troubleshooting Windows Autopilot
description: Learn how to handle issues as they arise during the Windows Autopilot deployment process.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
---


# Troubleshooting Windows Autopilot

**Applies to: Windows 10**

Windows Autopilot is designed to simplify all parts of the Windows device lifecycle, but there are always situations where issues may arise. Review the following information to assist with troubleshooting efforts.

## Troubleshooting process

Whether you're performing user-driven or self-deploying device deployments, the troubleshooting process is about the same. It's useful to understand the flow for a specific device:

1. A network connection is established. The connection can be a wireless (Wi-fi) or wired (Ethernet) connection.
2. The Windows Autopilot profile is downloaded. When you use a wired connection, or manually establish a wireless connection, the profile downloads from the Autopilot deployment service as soon as the network connection is in place.
3. User authentication occurs. When performing a user-driven deployment, the user will enter their Azure Active Directory credentials, which will be validated.
4. Azure Active Directory join occurs. For user-driven deployments, the device will be joined to Azure AD using the specified user credentials. For self-deploying scenarios, the device will be joined without specifying any user credentials.
5. Automatic MDM enrollment occurs. As part of the Azure AD join process, the device will enroll in the MDM service configured in Azure AD (for example, Microsoft Intune).
6. Settings are applied. If the [enrollment status page](enrollment-status.md) is configured, most settings will be applied while the enrollment status page is displayed. If not configured or available, settings will be applied after the user is signed in.

For troubleshooting, key activities to perform are:

- Configuration: Has Azure Active Directory and Microsoft Intune (or an equivalent MDM service) been configured as specified in [Windows Autopilot configuration requirements](configuration-requirements.md)?
- Network connectivity: Can the device access the services described in [Windows Autopilot networking requirements](networking-requirements.md)?
- Autopilot out-of-box (OOBE) behavior: Were only the expected out-of-box experience screens displayed? Was the Azure AD credentials page customized with organization-specific details as expected?
- Azure AD join issues: Was the device able to join Azure Active Directory?
- MDM enrollment issues: Was the device able to enroll in Microsoft Intune (or an equivalent MDM service)?

## Troubleshooting Autopilot Device Import

### Clicking Import after selecting CSV does nothing, '400' error appears in network trace with error body **"Cannot convert the literal '[DEVICEHASH]' to the expected type 'Edm.Binary'"**

This error points to the device hash being incorrectly formatted. Anything that corrupts the collected hash can cause this error. One possibility is that the hash itself (even if it's valid) fails to be decoded.

The device hash is Base64. At the device level, it's encoded as unpadded Base64, but Autopilot expects padded Base64. Usually, the payload doesn't require padding and the process works. Sometimes, however, the payload doesn't line up cleanly and padding is necessary. In this case, you get the error displayed above. PowerShell's Base64 decoder also expects padded Base64, so we can use this decoder to validate that the hash is properly padded.

The "A" characters at the end of the hash are effectively empty data. Each character in Base64 is 6 bits, A in Base64 is 6 bits equal to 0. Deleting or adding **A**s at the end doesn't change the actual payload data.

To fix this issue, we'll need to modify the hash, then test the new value, until PowerShell succeeds in decoding the hash. The result is mostly illegible, which is fine. We're just looking for it to not throw the error "Invalid length for a Base-64 char array or string". 

To test the base64, you can use the following PowerShell:
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("DEVICE HASH"))
```

So, as an example (this isn't a device hash, but it's misaligned unpadded Base64 so it's good for testing):
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("Q29udG9zbwAAA"))
```

Now for the padding rules. The padding character is "=". The padding character can only be at the end of the hash, and there can only be a maximum of two padding characters. Here's the basic logic.

- Does decoding the hash fail?
 - Yes: Are the last two characters "="?
   - Yes: Replace both "=" with a single "A" character, then try again
   - No: Add another "=" character at the end, then try again
 - No: That hash is valid

Looping the logic above on the previous example hash, we get the following permutations:
- Q29udG9zbwAAA
- Q29udG9zbwAAA=
- Q29udG9zbwAAA==
- Q29udG9zbwAAAA
- Q29udG9zbwAAAA=
- **Q29udG9zbwAAAA==** (This one has valid padding)

Replace the collected hash with this new padded hash then try to import again.

## Troubleshooting Autopilot OOBE issues

When OOBE includes unexpected Autopilot behavior, it's useful to check if the device received an Autopilot profile. If so, check the settings that the profile contained. Depending on the Windows 10 release, there are different mechanisms available to do that.

### Windows 10 version 1803 and above

Windows 10 version 1803 and above adds event log entries. You can use the og entries to see details related to the Autopilot profile settings and OOBE flow. These entries can be viewed using Event Viewer. Review the information at **Application and Services Logs –> Microsoft –> Windows –> Provisioning-Diagnostics-Provider –> Autopilot** for versions before 1903. For version 1903 and later, see **Application and Services Logs –> Microsoft –> Windows –> ModernDeployment-Diagnostics-Provider –> Autopilot**. The following events may be recorded, depending on the scenario and profile configuration:

| Event ID | Type | Description |
|----------|------|-------------| 
| 100 | Warning | “Autopilot policy [name] not found.” This error is typically a temporary problem, while the device is waiting for an Autopilot profile to be downloaded. |
| 101 | Info | “AutopilotGetPolicyDwordByName succeeded: policy name = [setting name]; policy value = [value].” This message shows Autopilot retrieving and processing numeric OOBE settings. |
| 103 | Info | “AutopilotGetPolicyStringByName succeeded: policy name = [name]; value = [value].” This message shows Autopilot retrieving and processing OOBE setting strings such as the Azure AD tenant name. |
| 109 | Info | “AutopilotGetOobeSettingsOverride succeeded: OOBE setting [setting name]; state = [state].” This message shows Autopilot retrieving and processing state-related OOBE settings. |
| 111 | Info | “AutopilotRetrieveSettings succeeded.” This message means that the settings stored in the Autopilot profile that control the OOBE behavior have been retrieved successfully. |
| 153 | Info | “AutopilotManager reported the state changed from [original state] to [new state].” Usually, this message should say “ProfileState_Unknown” to “ProfileState_Available”. This case indicates that a profile was available and downloaded for the device. So, the device is ready to deploy using Autopilot. |
| 160 | Info | “AutopilotRetrieveSettings beginning acquisition.” This message shows that Autopilot is getting ready to download the needed Autopilot profile settings. |
| 161 | Info | “AutopilotManager retrieve settings succeeded.” The Autopilot profile was successfully downloaded. |
| 163 | Info | “AutopilotManager determined download isn't required and the device is already provisioned. Clean or reset the device to change this.” This message indicates that an Autopilot profile is resident on the device; it typically would only be removed by the **Sysprep /Generalize** process. |
| 164 | Info | “AutopilotManager determined Internet is available to attempt policy download.” |
| 171 | Error | “AutopilotManager failed to set TPM identity confirmed. HRESULT=[error code].” This message indicates an issue performing TPM attestation, needed to complete the self-deploying mode process. | 
| 172 | Error | “AutopilotManager failed to set Autopilot profile as available. HRESULT=[error code].” This error is typically related to event ID 171. |

In addition to the event log entries, the registry and ETW trace options below work with Windows 10 version 1803 and above.

### Windows 10 version 1709 and above

Autopilot profile settings received from the Autopilot deployment service are stored in the device's registry. This information can be found at **HKLM\SOFTWARE\Microsoft\Provisioning\Diagnostics\Autopilot**. Available registry entries include:

| Value | Description |
|-------|-------------|
| AadTenantId | The GUID of the Azure AD tenant the user signed into. The user receives an error if this entry doesn't match the tenant that was used to register the device. |
| CloudAssignedTenantDomain | The Azure AD tenant the device has been registered with, for example, “contosomn.onmicrosoft.com.” If the device isn't registered with Autopilot, this value will be blank. |
| CloudAssignedTenantId | The GUID of the Azure AD tenant the device registered with. The GUID corresponds to the tenant domain from the CloudAssignedTenantDomain registry value. If the device isn’t registered with Autopilot, this value will be blank.|
| IsAutopilotDisabled | If set to 1, this registry value indicates that the device isn't registered with Autopilot. This state could also indicate that the Autopilot profile couldn't be downloaded because of network connectivity or firewall issues, or network timeouts. |
| TenantMatched | This entry is set to 1 if the user's tenant ID matches the tenant ID that the device was registered with. If this registry value is 0, the user would be shown an error and forced to start over. |
| CloudAssignedOobeConfig | A bitmap that shows which Autopilot settings were configured. Values include: SkipCortanaOptIn = 1, OobeUserNotLocalAdmin = 2, SkipExpressSettings = 4, SkipOemRegistration = 8, SkipEula = 16 |

### Windows 10 semi-annual channel supported versions

On devices running a [supported version](https://docs.microsoft.com/windows/release-information/) of Windows 10 semi-annual channel, you can use ETW tracing to get detailed information from Autopilot and related components. The ETW trace files can be viewed using the Windows Performance Analyzer or similar tools. For more information, see [the advanced troubleshooting blog](https://blogs.technet.microsoft.com/mniehaus/2017/12/13/troubleshooting-windows-autopilot-level-300400/).

## Troubleshooting Azure AD Join issues

The most common issue joining a device to Azure AD is related to Azure AD permissions. Make sure that [the correct configuration is in place](configuration-requirements.md) to allow users to join devices to Azure AD. Errors can also happen if the user exceeds the number of devices that they're allowed to join. This limit is configured in Azure AD.

An Azure AD device is created upon import. It's important this object isn't deleted. The object acts as Autopilot's anchor in Azure AD for group membership and targeting (including the profile). Deleting it may lead to join errors. If this object is deleted, you can fix the issue by deleting and reimporting this autopilot hash so it can recreate the associated object.

Error code 801C0003 will typically be reported on an error page titled "Something went wrong". This error means that the Azure AD join failed.

## Troubleshooting Intune enrollment issues

See [this knowledge base article](https://support.microsoft.com/help/4089533/troubleshooting-windows-device-enrollment-problems-in-microsoft-intune) for assistance with Intune enrollment issues. Common issues can include"
- incorrect or missing licenses assigned to the user.
- too many devices enrolled for the user.

Error code 80180018 will typically be reported on an error page titled "Something went wrong". This error means that the MDM enrollment failed.

If Autopilot Reset fails immediately with the error **Ran into trouble. Please sign in with an administrator account to see why and reset manually**, see [Troubleshoot Autopilot Reset](https://docs.microsoft.com/education/windows/autopilot-reset#troubleshoot-autopilot-reset) for more help.

## Profile download

When an Internet-connected Windows 10 device boots up, it will attempt to connect to the Autopilot service and download an Autopilot profile. Note: It's important that a profile exists at this stage so that a blank profile isn't cached locally on the PC. To remove the currently cached local profile in Windows 10 version 1803 and earlier, it's necessary to re-generalize the OS using **sysprep /generalize /oobe**, reinstall the OS, or re-image the PC. In Windows 10 version 1809 and later, you can retrieve a new profile by rebooting the PC.

When a profile is downloaded depends upon the version of Windows 10 that is running on the PC. See the following table.

| Windows 10 version | Profile download behavior |
| --- | --- |
| 1709 | The profile is downloaded after the OOBE network connection page. This page isn't displayed when using a wired connection. In this case, the profile is downloaded before the EULA screen. |
| 1803 | The profile is downloaded as soon as possible. If wired, it's downloaded at the start of OOBE. If wireless, it's downloaded after the network connection page. |
| 1809 | The profile is downloaded as soon as possible (same as 1803), and again after each reboot. |

If you need to reboot a computer during OOBE:
- Press Shift-F10 to open a command prompt.
- Enter **shutdown /r /t 0** to restart immediately, or **shutdown /s /t 0** to shut down immediately.

For more information, see [Windows Setup Command-Line Options](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

## Related topics

[Windows Autopilot - known issues](known-issues.md)<br>
[Diagnose MDM failures in Windows 10](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
