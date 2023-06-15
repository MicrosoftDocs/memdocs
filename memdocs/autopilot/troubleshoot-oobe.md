---
title: Troubleshoot Autopilot OOBE issues
description: How to troubleshoot Autopilot OOBE issues.
ms.technology: itpro-deploy
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/17/2022
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: troubleshooting
---

# Troubleshoot Autopilot OOBE issues

*Applies to:*

- Windows 11
- Windows 10

When the out-of-box-experience (OOBE) includes unexpected Autopilot behavior, it's useful to check if the device received an Autopilot profile. If so, check the settings that the profile contained. Depending on the Windows client release, there are different mechanisms available to do that.

> [!NOTE]
> With Windows 11, you can enable users to view additional detailed troubleshooting information about the Autopilot provisioning process. The [Windows Autopilot diagnostics page](windows-autopilot-whats-new.md#windows-autopilot-diagnostics-page) provides IT admins and end users with a user-friendly view to troubleshoot Windows Autopilot failures. This feature can be enabled by going to the [ESP profile](../intune/enrollment/windows-enrollment-status.md) and selecting **Yes** to **Allow users to collect logs about installation errors**. This feature is currently supported for commercial OOBE, and Autopilot user-driven mode.

## Can't connect to MDM terms of use error

If you receive an error during OOBE that **Something went wrong** and **Can't connect to the URL of your organization's MDM terms of use. Try again, or contact your system administrator with the problem information from this page.** This is often due to a licensing issue. Check that the user who is signing into the device has a valid Intune, EMS, or Microsoft 365 license.

## Windows 10 version 1803 and above

Windows 10 version 1803 and above adds event log entries. You can use the log entries to see details related to the Autopilot profile settings and OOBE flow. These entries can be viewed using Event Viewer. Review the information at **Application and Services Logs -> Microsoft -> Windows -> Provisioning-Diagnostics-Provider -> Autopilot** for versions before 1903. For version 1903 and later, see **Application and Services Logs -> Microsoft -> Windows -> ModernDeployment-Diagnostics-Provider -> Autopilot**. The following events may be recorded, depending on the scenario and profile configuration:

| Event ID | Type | Description |
|----------|------|-------------|
| 100 | Warning | "Autopilot policy [name] not found." This error is typically a temporary problem, while the device is waiting for an Autopilot profile to be downloaded. |
| 101 | Info | "AutopilotGetPolicyDwordByName succeeded: policy name = [setting name]; policy value = [value]." This message shows Autopilot retrieving and processing numeric OOBE settings. |
| 103 | Info | "AutopilotGetPolicyStringByName succeeded: policy name = [name]; value = [value]." This message shows Autopilot retrieving and processing OOBE setting strings such as the Azure AD tenant name. |
| 109 | Info | "AutopilotGetOobeSettingsOverride succeeded: OOBE setting [setting name]; state = [state]." This message shows Autopilot retrieving and processing state-related OOBE settings. |
| 111 | Info | "AutopilotRetrieveSettings succeeded." This message means that the settings stored in the Autopilot profile that control the OOBE behavior have been retrieved successfully. |
| 153 | Info | "AutopilotManager reported the state changed from [original state] to [new state]." Usually, this message should say "ProfileState_Unknown" to "ProfileState_Available". This case indicates that a profile was available and downloaded for the device. So, the device is ready to deploy using Autopilot. |
| 160 | Info | "AutopilotRetrieveSettings beginning acquisition." This message shows that Autopilot is getting ready to download the needed Autopilot profile settings. |
| 161 | Info | "AutopilotManager retrieve settings succeeded." The Autopilot profile was successfully downloaded. |
| 163 | Info | "AutopilotManager determined download isn't required and the device is already provisioned. Clean or reset the device to change this." This message indicates that an Autopilot profile is resident on the device; it typically would only be removed by the **Sysprep /Generalize** process. |
| 164 | Info | "AutopilotManager determined Internet is available to attempt policy download." |
| 171 | Error | "AutopilotManager failed to set TPM identity confirmed. HRESULT=[error code]." This message indicates an issue performing TPM attestation, needed to complete the self-deploying mode process. | 
| 172 | Error | "AutopilotManager failed to set Autopilot profile as available. HRESULT=[error code]." This error is typically related to event ID 171. |

In addition to the event log entries, the registry and ETW trace options below work with Windows 10 version 1803 and above.

## Windows 10 version 1709 and above

Autopilot profile settings received from the Autopilot deployment service are stored in the device's registry. This information can be found at **HKLM\SOFTWARE\Microsoft\Provisioning\Diagnostics\Autopilot**. Available registry entries include:

| Value | Description |
|-------|-------------|
| AadTenantId | The GUID of the Azure AD tenant the user signed into. The user receives an error if this entry doesn't match the tenant that was used to register the device. |
| CloudAssignedTenantDomain | The Azure AD tenant the device has been registered with, for example, "contosomn.onmicrosoft.com." If the device isn't registered with Autopilot, this value will be blank. |
| CloudAssignedTenantId | The GUID of the Azure AD tenant the device registered with. The GUID corresponds to the tenant domain from the CloudAssignedTenantDomain registry value. If the device isn't registered with Autopilot, this value will be blank.|
| IsAutopilotDisabled | If set to 1, this registry value indicates that the device isn't registered with Autopilot. This state could also indicate that the Autopilot profile couldn't be downloaded because of network connectivity or firewall issues, or network timeouts. |
| TenantMatched | This entry is set to 1 if the user's tenant ID matches the tenant ID that the device was registered with. If this registry value is 0, the user would be shown an error and forced to start over. |
| CloudAssignedOobeConfig | A bitmap that shows which Autopilot settings were configured. Values include: SkipCortanaOptIn = 1, OobeUserNotLocalAdmin = 2, SkipExpressSettings = 4, SkipOemRegistration = 8, SkipEula = 16 |

## Windows 10 semi-annual channel supported versions

On devices running a [supported version](/windows/release-information/) of Windows 10 semi-annual channel, you can use ETW tracing to get detailed information from Autopilot and related components. The ETW trace files can be viewed using the Windows Performance Analyzer or similar tools. For more information, see [the advanced troubleshooting blog](/archive/blogs/mniehaus/troubleshooting-windows-autopilot-level-300400).

## Related topics

[Windows Autopilot - known issues](known-issues.md)

[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)
