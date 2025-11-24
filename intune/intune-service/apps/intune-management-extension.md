---
title: Understand Microsoft Intune Management Extension
description: Understand Microsoft Intune management extension for Windows.
ms.date: 10/02/2025
ms.topic: how-to
ms.reviewer: bryanke
ms.collection:
- M365-identity-device-management
- Windows
- highpri
- FocusArea_Apps_Win32
---

# Intune Management Extension for Windows

[!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

The Intune Management Extension (IME) is an installer agent that enhances Windows device management (MDM). It supplements the standard Windows MDM feature by enabling advanced device management capabilities.

> [!NOTE]
> For details about PowerShell scripts, see [Use PowerShell scripts on Windows devices in Intune](../apps/powershell-scripts.md).

> [!IMPORTANT]
> To support expanded functionality and bug fixes, use .NET Framework 4.7.2 or later with the Intune Management Extension on Windows clients. If a Windows client uses an earlier version of the .NET Framework, the Intune Management Extension still functions. The .NET Framework 4.7.2 is available from Windows Update as of July 10, 2018, and is included in Windows 10 version 1809 (RS5) and later. Multiple versions of the .NET Framework can coexist on a device.

This feature applies to:

- Windows 10 and later (excluding Windows Home and Windows devices running in S mode).

> [!NOTE]
> After the Intune management extension prerequisites are met, the extension installs automatically when you assign any of the following to the user or device:
>
> - A PowerShell script
> - A Win32 app
> - A Microsoft Store app
> - A custom compliance policy setting
> - A proactive remediation
>
> For more information, see Intune Management Extension [prerequisites](../apps/intune-management-extension.md#prerequisites).

## Prerequisites

The Intune management extension has the following prerequisites. When the prerequisites are met, the Intune management extension installs automatically when a PowerShell script or Win32 app is assigned to the user or device.

- Devices running Windows 10 version 1607 or later. If the device is enrolled using [automatic enrollment](../enrollment/windows-bulk-enroll.md), it must run Windows 10 version 1709 or later. The Intune management extension doesn't support Windows in S mode because S mode doesn't allow running nonstore apps.

- Devices joined to Microsoft Entra ID, including:

  - Microsoft Entra hybrid joined: Devices joined to Microsoft Entra ID and on-premises Active Directory (AD). See [Plan your Microsoft Entra hybrid join implementation](/azure/active-directory/devices/hybrid-azuread-join-plan) for guidance.

  - Microsoft Entra registered/Workplace joined (WPJ): Devices [registered](/azure/active-directory/user-help/user-help-register-device-on-network) in Microsoft Entra ID. For more information, see [Workplace Join as a seamless second factor authentication](/windows-server/identity/ad-fs/operations/join-to-workplace-from-any-device-for-sso-and-seamless-second-factor-authentication-across-company-applications#BKMK_DRS). These are Bring Your Own Device (BYOD) devices with a work or school account added via **Settings** > **Accounts** > **Access work or school**.

- Devices enrolled in Intune, including:

  - Devices enrolled using group policy (GPO). For more information, see [Enroll a Windows device automatically using Group Policy](/windows/client-management/enroll-a-windows-10-device-automatically-using-group-policy).

  - Devices manually enrolled in Intune, which occurs when:

    - [Automatic enrollment to Intune](../enrollment/quickstart-setup-auto-enrollment.md) is enabled in Microsoft Entra ID. Users sign in to devices using a local user account and manually join the device to Microsoft Entra ID. Then, they sign in to the device using their Microsoft Entra account.

    OR

    - Users sign in to the device using their Microsoft Entra account and then enroll in Intune.

  - Co-managed devices using Configuration Manager and Intune. When installing Win32 apps, set the **Apps** workload to **Pilot Intune** or **Intune**. PowerShell scripts run even if the **Apps** workload is set to **Configuration Manager**. The Intune management extension deploys to a device when you target a PowerShell script to the device. The device must be Microsoft Entra ID or Microsoft Entra hybrid joined and run Windows 10 version 1607 or later. See the following articles for guidance:

    - [What is co-management](/configmgr/comanage/overview)
    - [Client apps workload](/configmgr/comanage/workloads#client-apps)
    - [How to switch Configuration Manager workloads to Intune](/configmgr/comanage/how-to-switch-workloads)

- For devices behind firewalls and proxy servers, enable communication for Intune. For more information, see [Network requirements for PowerShell scripts and Win32 apps](../fundamentals/intune-endpoints.md).

> [!NOTE]
> For details about using Windows 10 or Windows 11 virtual machines, see [Using Windows 10 virtual machines with Microsoft Intune](../fundamentals/windows-10-virtual-machines.md).

## Understand Intune management extension agent installation

For devices meeting the prerequisites, the Intune management extension installs automatically when certain features are assigned to a user or device. Installation occurs when the following features are assigned:

- [PowerShell scripts](../apps/powershell-scripts.md)
- [Remediations](../fundamentals/remediations.md)
- [Discovery scripts for custom compliance](../protect/compliance-custom-script.md)
- [Win32 apps](../apps/apps-win32-add.md)
- [Endpoint analytics](../../endpoint-analytics/settings.md)
- [Remote Help](../fundamentals/remote-help-windows.md)
- [Managed Installers in Intune](../protect/endpoint-security-app-control-policy.md)
- [Update Windows BIOS using configuration MDM policy](../configuration/bios-configuration.md)

> [!NOTE]
> For details about how the IME is rolled out and updated, see [Service information for Microsoft Intune release updates](../fundamentals/intune-service-servicing-information.md).

The agent installs at `C:\ProgramData\Microsoft\IntuneManagementExtension\Logs` when applicable and doesn't appear in the start menu on Windows devices. The agent appears as **IntuneManagementExtension** under **Services** in **Task Manager** when running on Windows devices.

### Intune management extension functionality

- The IME silently authenticates with Intune services before checking in to receive assigned installations for the Windows device.
- The IME checks for new or updated installations with Intune services every 8 hours. This check-in process is independent of the MDM check-in.
- The IME might periodically perform health checks to validate connectivity to Intune services.

### Manually initiate an Intune management IME check-in from a Windows device

On a Windows device with the IME installed, open **Company Portal**, select **Settings** > **Sync**. This initiates an MDM check-in and an IME check-in.

Alternatively, open **Task Manager**, find the service **IntuneManagementExtension**, right-click, and select **Restart**. The `IntuneManagementExtension` service restarts immediately, initiating a check-in with Intune.

> [!NOTE]
> The **Sync** actions from either the **Settings** app (Windows 10 or later) or **Devices** in Microsoft Intune admin center initiate an MDM check-in but don't force an IME check-in.

### Intune management extension removal

The IME is removed from the device under the following conditions:

- PowerShell scripts are no longer assigned to the device.
- The Windows device is no longer managed.
- The IME is in an irrecoverable state for over 24 hours (device-awake time).

## Common issues and resolutions

### Issue: Intune management extension doesn't download

**Possible resolutions**:

- The device isn't joined to Microsoft Entra ID. Make sure the devices meet the [prerequisites](#prerequisites) in this article.
- No PowerShell scripts or Win32 apps are assigned to the groups the user or device belongs to.
- The device can't check in with the Intune service. For example, there's no internet access or no access to Windows Push Notification Services (WNS).
- The device is in S mode. The Intune management extension doesn't support devices running in S mode.
- On Windows devices, if the proxy is configured only at the user level (and not machine-wide), make sure a user is signed into the device. Alternatively, use `bitsadmin /util /setieproxy` to manually configure the proxy for the BITS (Background Intelligent Transfer Service). For more information, see [bitsadmin util and setieproxy](/windows-server/administration/windows-commands/bitsadmin-util-and-setieproxy).

To check if the device is automatically enrolled:

1. Go to **Settings** > **Accounts** > **Access work or school**.
2. Select the joined account > **Info**.
3. Under **Advanced Diagnostic Report**, select **Create Report**.
4. Open the `MDMDiagReport` in a web browser.
5. Search for the **MDMDeviceWithAAD** property. If the property exists, the device is automatically enrolled. If this property doesn't exist, the device isn't automatically enrolled.

[Enable Windows automatic enrollment](../enrollment/windows-enroll.md#enable-windows-automatic-enrollment) includes the steps to configure automatic enrollment in Intune.

## Intune management extension logs

IME logs on the client machine are typically in `C:\ProgramData\Microsoft\IntuneManagementExtension\Logs`. Use [CMTrace.exe](/configmgr/core/support/cmtrace) to view these log files.

:::image type="content" source="media/intune-management-extension/image.png" alt-text="Screenshot showing Intune Management Extension log files in CMTrace.":::

Also, use the log file *AppWorkload.log* to troubleshoot and analyze Win32 app management events on the client. This log file contains all logging information related to app deployment activities conducted by the IME.

### IME log files

| Log file | Description |
|---|---|
| IntuneManagementExtension.log | The main log file. It contains all the IME check-ins, policy requests, policy processing, and reporting activities. |
| AgentExecutor.log | Tracks PowerShell script executions (deployed by Intune). |
| AppActionProcessor.log | Tracks detection and applicability check actions for assigned apps. |
| AppWorkload.log | Helps troubleshoot and analyze Win32 app deployment activities. |
| ClientCertCheck.log | Tracks device client certificate checks. |
| ClientHealth.log | Tracks the health of the Intune management extension. |
| DeviceHealthMonitoring.log | Tracks the health of hardware readiness, device inventory, and other data collectors. |
| HealthScripts.log | Tracks the health of remediations that run on a regular schedule. |
| Sensor.log | Tracks the health of the Endpoint analytics data collector, including boot performance, app reliability, and more. |
| Win32AppInventory.log | Tracks the health of the app inventory collector. |

## Next steps

- The app you create appears in the apps list. Assign it to the groups you choose. For more information, see [Assign apps to groups with Microsoft Intune](../apps/apps-deploy.md).
- Learn more about monitoring app properties and assignments. For more information, see [Monitor app information and assignments with Microsoft Intune](../apps/apps-monitor.md).
- Learn more about the context of your app in Intune. For more information, see [Overview of the Microsoft Intune mobile device management (MDM) lifecycle](../fundamentals/device-lifecycle.md).
