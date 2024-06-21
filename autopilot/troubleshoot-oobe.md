---
title: Troubleshoot Autopilot OOBE issues
description: How to troubleshoot Autopilot OOBE issues.
ms.subservice: itpro-deploy
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/11/2024
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: troubleshooting
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Troubleshoot Autopilot OOBE issues

When the out-of-box-experience (OOBE) includes unexpected Autopilot behavior, it's useful to check if the device received an Autopilot profile. If so, check the settings that the profile contained. Depending on the Windows client release, there are different mechanisms available to do that.

> [!NOTE]
>
> With Windows 11, additional detailed troubleshooting information about the Autopilot provisioning process can be enabled. The [Windows Autopilot diagnostics page](whats-new.md#windows-autopilot-diagnostics-page) provides IT admins and end users with a user-friendly view to troubleshoot Windows Autopilot failures. This feature can be enabled by going to the [ESP profile](/mem/intune/enrollment/windows-enrollment-status) and selecting **Yes** to **Allow users to collect logs about installation errors**. This feature is currently supported for commercial OOBE, and Autopilot user-driven mode.

## Can't connect to MDM terms of use error

The following messages displayed during OOBE are associated with licensing issues:

> **Something went wrong**.
>
> **Can't connect to the URL of your organization's MDM terms of use. Try again, or contact your system administrator with the problem information from this page.**

Check that the user who is signing into the device has a valid Intune, EMS, or Microsoft 365 license.

## Event log entries

Windows Autopilot logs entries into the event log. The log entries can be used to see details related to the Autopilot profile settings and OOBE flow. These entries can be viewed using Event Viewer. Review the information at **Application and Services Logs** -> **Microsoft** -> **Windows** -> **ModernDeployment-Diagnostics-Provider** -> **Autopilot**. The following events might be recorded, depending on the scenario and profile configuration:

| **Event ID** | **Type** | **Message** |**Description** |
|----------|------|-------------|-------------|
| **100** | Warning | **Autopilot policy [name] not found.** | This error is typically a temporary problem, while the device is waiting for an Autopilot profile to be downloaded. |
| **101** | Info | **AutopilotGetPolicyDwordByName succeeded: policy name = [setting name]; policy value = [value].** | This message shows Autopilot retrieving and processing numeric OOBE settings. |
| **103** | Info | **AutopilotGetPolicyStringByName succeeded: policy name = [name]; value = [value].** | This message shows Autopilot retrieving and processing OOBE setting strings such as the Microsoft Entra tenant name. |
| **109** | Info | **AutopilotGetOobeSettingsOverride succeeded: OOBE setting [setting name]; state = [state].** | This message shows Autopilot retrieving and processing state-related OOBE settings. |
| **111** | Info | **AutopilotRetrieveSettings succeeded.** | This message means that the settings stored in the Autopilot profile that control the OOBE behavior were retrieved successfully. |
| **153** | Info | **AutopilotManager reported the state changed from [original state] to [new state].** | Usually, this message says **ProfileState_Unknown to ProfileState_Available**. This case indicates that a profile was available and downloaded for the device and that the device is ready to deploy using Autopilot. |
| **160** | Info | **AutopilotRetrieveSettings beginning acquisition.** | This message shows that Autopilot is getting ready to download the needed Autopilot profile settings. |
| **161** | Info | **AutopilotManager retrieve settings succeeded.** | The Autopilot profile was successfully downloaded. |
| **163** | Info | **AutopilotManager determined download isn't required and the device is already provisioned. Clean or reset the device to change this.** | This message indicates that an Autopilot profile is resident on the device; it typically would only be removed by the **Sysprep /Generalize** process. |
| **164** | Info | **AutopilotManager determined Internet is available to attempt policy download.** | |
| **171** | Error | **AutopilotManager failed to set TPM identity confirmed. HRESULT=[error code].** | This message indicates an issue performing TPM attestation, needed to complete the self-deploying mode process. |
| **172** | Error | **AutopilotManager failed to set Autopilot profile as available. HRESULT=[error code].** | This error is typically related to event ID 171. |

## Registry

Autopilot profile settings received from the Autopilot deployment service are stored in the device's registry. This information can be found at **HKLM\SOFTWARE\Microsoft\Provisioning\Diagnostics\Autopilot**. Available registry entries include:

| **Value** | **Description** |
|-------|-------------|
| **AadTenantId** | The GUID of the Microsoft Entra tenant the user signed into. The user receives an error if this entry doesn't match the tenant that was used to register the device. |
| **CloudAssignedTenantDomain** | The Microsoft Entra tenant the device is registered with, for example, `contosomn.onmicrosoft.com`. If the device isn't registered with Autopilot, this value is blank. |
| **CloudAssignedTenantId** | The GUID of the Microsoft Entra tenant the device registered with. The GUID corresponds to the tenant domain from the CloudAssignedTenantDomain registry value. If the device isn't registered with Autopilot, this value is blank.|
| **IsAutopilotDisabled** | If set to 1, this registry value indicates that the device isn't registered with Autopilot. This state could also indicate that the Autopilot profile couldn't be downloaded because of network connectivity or firewall issues, or network timeouts. |
| **TenantMatched** | This entry is set to 1 if the user's tenant ID matches the tenant ID that the device was registered with. If this registry value is 0, the user would be shown an error and forced to start over. |
| **CloudAssignedOobeConfig** | A bitmap that shows which Autopilot settings were configured. Values include: **SkipCortanaOptIn** = 1, **OobeUserNotLocalAdmin** = 2, **SkipExpressSettings** = 4, **SkipOemRegistration** = 8, **SkipEula** = 16 |

## ETW trace options

ETW tracing can be used to get detailed information from Autopilot and related components. The ETW trace files can be viewed using the Windows Performance Analyzer or similar tools. For more information, see [the advanced troubleshooting blog](/archive/blogs/mniehaus/troubleshooting-windows-autopilot-level-300400).

## Related content

- [Windows Autopilot - known issues](known-issues.md).
- [Collect MDM logs](/windows/client-management/mdm-collect-logs).
