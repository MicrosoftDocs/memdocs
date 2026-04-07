---
title: Enhanced app inventory for Windows devices
description: Use enhanced app inventory in Microsoft Intune to collect detailed application data from Windows devices with faster refresh cycles and richer metadata.
ms.date: 04/07/2026
ms.topic: how-to
ai-usage: ai-generated
ms.collection:
- M365-identity-device-management
---

# Enhanced app inventory for Windows devices in Microsoft Intune

Enhanced app inventory provides faster, more detailed visibility into the applications installed on your Intune-managed Windows devices. It replaces the seven-day refresh cycle used by [Discovered apps](app-discovered-apps.md) with a configurable collection interval and collects richer app metadata, including install paths, uninstall commands, and app sizes.

## How enhanced app inventory works

Enhanced app inventory uses a dedicated inventory agent on Windows devices to collect application data and upload it to the Intune service. The inventory agent:

- Collects Win32 apps from the Windows registry (system-level and per-user)
- Collects Windows Store apps using the package manager API
- Uploads delta changes to reduce bandwidth and processing time
- Reports data to a new **Application Inventory** in the Intune admin center

Unlike Discovered apps, which collect inventory automatically, enhanced app inventory requires you to create and assign a device configuration policy to enable collection.

## Prerequisites

- Devices must be enrolled in Intune and Microsoft Entra joined
- Devices must be corporate-owned
- Windows 11

## Create an app inventory policy

To collect enhanced app inventory data, create a device configuration policy that specifies which application properties to collect and assign it to your device or user groups.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Select the following settings:
   - **Platform**: Windows 11
   - **Profile type**: Properties catalog
4. Select **Create**.
5. In **Basics**, enter a name and description for the policy. For example, *Enhanced app inventory - all properties*.
6. In **Configuration settings**, select **Add settings**, then expand **Application Inventory**.
7. Select the application properties you want to collect. The key properties (App Name, Version, and Publisher) are selected by default and can't be removed.

   You can collect the following properties:

   | Property | Description |
   |----------|-------------|
   | **App name** | The display name of the application. |
   | **App version** | The version of the application. |
   | **Publisher** | The publisher of the application. |
   | **Architecture** | The processor architecture of the application (x86, x64, ARM, ARM64). |
   | **Install location** | The path where the application is installed on the device. |
   | **Install date** | The date the application was installed. |
   | **Estimated size** | The estimated size of the application, in bytes. |
   | **Platform-specific app ID** | An identifier specific to the platform. For Win32 apps, this value is the MSI product code. For Store apps, this value is the package full name. |
   | **Uninstall command** | The command used to uninstall the application. |
   | **Modify command** | The command used to modify the application. |
   | **Languages** | The languages the application supports. |

8. Select **Next**.
9. In **Assignments**, select the device or user groups that should have application inventory collected.
10. Complete the remaining wizard steps and select **Create**.

After the policy is assigned, inventory data collection begins at the next device check-in and repeats on a regular schedule.

## View app inventory data

After devices check in with the inventory policy, you can view the collected app data.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices**.
3. Select a device.
4. Select **Application Inventory** in the **Monitor** section.

**Application Inventory** displays the list of applications detected on the selected device, including all the properties you selected in the inventory policy.

## Data collection details

### Refresh cycle

Enhanced app inventory collects data more frequently than Discovered apps:

| Feature | Refresh cycle |
|---------|---------------|
| Discovered apps (Win32 via IME) | Every 24 hours |
| Discovered apps (all other apps) | Every seven days |
| Enhanced app inventory | Every 4-8 hours (configurable) |

The inventory agent runs on a configurable schedule. The collection frequency can be adjusted without requiring an agent update.

### App collection limits

A maximum of 1,000 applications can be collected per device. If a device has more than 1,000 installed applications, the inventory agent uses a deterministic selection to collect a consistent set of apps. Apps that exceed the limit are logged for monitoring.

The 1,000-app limit is configurable through the settings framework.

### App collection sources

The inventory agent collects applications from two sources on Windows devices:

- **Win32 apps**: Read from the Windows registry uninstall keys at both the system level (`HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`) and per-user level (`HKU\{SID}\Software\Microsoft\Windows\CurrentVersion\Uninstall`), including 32-bit apps on 64-bit systems.
- **Store apps**: Read from the Windows package manager at both the system level and per-user level.

### Install scope

Each application record includes an install scope that indicates whether the app is installed for:

- **Device**: The app is installed at the system level for all users.
- **User**: The app is installed for a specific user.

For user-scoped apps, the inventory record includes the Microsoft Entra user ID associated with the installation.

### Delta sync

After the initial full sync, the inventory agent sends only the changes (new, updated, or deleted apps) since the last collection. Delta sync reduces the amount of data transferred and minimizes processing overhead.

### Policy deletion behavior

If the app inventory policy is removed from a device, the inventory agent stops collecting application data and deletes existing app inventory records from the device. The service marks the records as deleted.

## Differences between Discovered apps and enhanced app inventory

| Capability | Discovered apps | Enhanced app inventory |
|------------|----------------|----------------------|
| Admin configuration | Automatic, no policy required | Requires a device configuration policy |
| Refresh cycle | Seven days (24 hours for Win32 via IME) | 4-8 hours (configurable) |
| Properties collected | App name, platform, version, publisher, device count | App name, version, publisher + install location, install date, size, architecture, uninstall command, modify command, platform-specific ID, languages |
| Supported platforms | Windows, iOS/iPadOS, macOS, Android, AOSP | Windows (corporate-owned, Entra joined) |
| Device ownership | Corporate and personal | Corporate only |
| Admin center location | **Apps** > **Monitor** > **Discovered apps** | **Devices** > device > **Application Inventory** |
| App limit per device | No documented limit | 1,000 apps (configurable) |
| Install scope tracking | No | Yes (Device or User) |

Both features can run simultaneously. Enhanced app inventory doesn't replace or disable Discovered apps.

## Known limitations

- Enhanced app inventory is available only for Windows 10/11 devices that are corporate-owned and Microsoft Entra joined.
- Personal devices aren't supported.
- The maximum number of apps collected per device is 1,000.
- Sovereign cloud availability: Supported in GCC High. Not supported in Microsoft Azure operated by 21Vianet.

## Related content

- [Discovered apps](app-discovered-apps.md)
- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
- [App types in Microsoft Intune](apps-add.md#app-types-in-microsoft-intune)
