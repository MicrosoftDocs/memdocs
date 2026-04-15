---
title: App inventory for Windows devices
description: Use app inventory in Microsoft Intune to collect detailed application data from Windows devices with faster refresh cycles and richer metadata than Discovered apps.
ms.date: 04/15/2026
ms.topic: how-to
ai-usage: ai-generated
ms.collection:
- M365-identity-device-management
---

# App inventory for Windows devices in Microsoft Intune

App inventory provides faster, more detailed visibility into the applications installed on your Intune-managed Windows devices. It collects richer app metadata than [Discovered apps](app-discovered-apps.md), including install paths, uninstall commands, and app sizes. App inventory is the intended long-term replacement for Discovered apps, but both features currently operate in parallel. More guidance on the transition will be provided as details become available.

## How app inventory works

App inventory expands the existing device inventory agent on Windows devices to also collect application data and upload it to the Intune service. The device inventory agent:

- Collects Win32 apps from the Windows registry uninstall keys (`HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall` and per-user keys), including 32-bit apps on 64-bit systems
- Collects Windows Store apps using the package manager API
- Uploads delta changes to reduce bandwidth and processing time
- Reports data to the **All apps** page in the Intune admin center

> [!IMPORTANT]
> Unlike Discovered apps, which collect inventory automatically, app inventory requires you to create and assign a device configuration policy to enable collection. Devices don't report app inventory data until a policy is assigned.

## Prerequisites

- Devices must be enrolled in Intune and Microsoft Entra joined
- Windows 10/11

## Create an app inventory policy

To collect app inventory data, create a device configuration policy that specifies which application properties to collect and assign it to your device or user groups.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Select the following settings:
   - **Platform**: Windows 10 and later
   - **Profile type**: Properties catalog
4. Select **Create**.
5. In **Basics**, enter a name and description for the policy. For example, *App inventory - all properties*.
6. In **Configuration settings**, select **Add settings**, then expand **Application Inventory**.
7. Select the application properties you want to collect. The following properties are required and selected by default:
   - App Name
   - App Version
   - Publisher
   - Architectures
   - Install Scope
   - Install Scope Platform User Id
   - Install Scope User Id

   You can also collect the following optional properties:

   | Properties catalog setting | Report column name | Description |
   |----------|-------------|-------------|
   | **Install location** | Install location | The path where the application is installed on the device. |
   | **Install date** | Install date | The date the application was installed. |
   | **Estimated size** | Estimated size | The estimated size of the application, in bytes. |
   | **Platform-specific app ID** | Package Name | An identifier specific to the platform. For Win32 apps, this value is the MSI product code. For Store apps, this value is the package full name. |
   | **Platform Specific App ID Type** | Platform Specific App ID Type | The type of platform-specific identifier (for example, MSI product code or package name). |
   | **Uninstall command** | Uninstall command | The command used to uninstall the application. |
   | **Modify command** | Modify command | The command used to modify the application. |
   | **Languages** | Languages | The languages the application supports. |
   | **Install Scope User Name** | User Name | The user name associated with the app installation. Best-effort resolution for non-Entra users on the device. |

   The following properties also appear in the app inventory report but aren't configurable in the Properties catalog:

   | Report column | Description |
   |----------|-------------|
   | **MSI Product Code** | The MSI product code for Win32 apps, when available. |
   | **Installed For** | Indicates whether the app is installed at the device level or for a specific user. |
   | **Last updated** | The date the app record was last updated. |
   | **Last checked** | The date the device last reported app inventory data. |

   > [!NOTE]
   > Not all properties are guaranteed to have data for every application. Data availability depends on whether the information exists in the data source (the uninstall registry key or package manager API) on the device.

8. Select **Next**.
9. In **Assignments**, select the device or user groups that should have application inventory collected.
10. Complete the remaining wizard steps and select **Create**.

After the policy is assigned, inventory data collection begins at the next device check-in and repeats multiple times per day for active devices. Collection is triggered with the MMPC sync/check-in cycle.

### Combine app and device inventory policies

The Properties catalog also includes device inventory properties, so you have flexibility in how you organize your policies. For example, you can:

- Create separate policies for app inventory and device inventory settings, then assign both to the same device groups.
- Combine app and device inventory settings into a single policy.
- Create multiple policies with different property selections for different device groups.

If more than one policy targets the same device, the device merges the settings. When there's a conflict, "collect" wins over "don't collect" for a given property.

## View app inventory data

After devices check in with the inventory policy, you can view the collected app data.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **Monitor** > **All apps**.
3. Select the **App Inventory** tab.

The **All apps** page brings both managed apps and inventoried apps into the same location, making it easier to explore and navigate between these related data sets. The **App Inventory** tab displays the list of applications detected across your devices, including all the properties you selected in the inventory policy.

### Required properties and report column mapping

Some properties in the Properties catalog appear under different column names in the app inventory report. The following table maps the required Properties catalog settings to their report column names:

| Properties catalog setting | Report column name |
|----------|-------------|
| Install Scope Platform User Id | SID |
| Install Scope User Id | User Entra ID |
| Install Scope User Name | User Name |
| Platform Specific App Id | Package Name |

## Data collection details

### Refresh cycle

App inventory collects data more frequently than Discovered apps. For active devices, collection runs multiple times per day, triggered by the MMPC sync/check-in cycle.

### App collection sources

The device inventory agent collects applications from two sources on Windows devices:

- **Win32 apps**: Read from the Windows registry uninstall keys at both the system level (`HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`) and per-user level (`HKU\{SID}\Software\Microsoft\Windows\CurrentVersion\Uninstall`), including 32-bit apps on 64-bit systems.
- **Store apps**: Read from the Windows package manager at both the system level and per-user level.

### Install scope

Each application record includes an install scope that indicates whether the app is installed for:

- **Device**: The app is installed at the system level for all users.
- **User**: The app is installed for a specific user.

For user-scoped apps, the inventory record includes the Microsoft Entra user ID associated with the installation. The agent also makes a best-effort attempt to resolve the user name for non-Entra users on the device.

### Delta sync

After the initial full sync, the device inventory agent sends only the changes (new, updated, or deleted apps) since the last collection. Delta sync reduces the amount of data transferred and minimizes processing overhead.

### Policy deletion behavior

If the app inventory policy is removed from a device, the device inventory agent stops collecting application data. Existing app inventory data is retained in the service until it ages out after 28 days.

## Differences between Discovered apps and app inventory

| Capability | Discovered apps | App inventory |
|------------|----------------|----------------------|
| Admin configuration | No configuration available | Requires a device configuration policy |
| Refresh cycle | Seven days (24 hours for Win32 via IME) | Multiple times per day |
| Properties collected | App name, platform, version, publisher, device count | App name, version, publisher + install location, install date, size, architecture, uninstall command, modify command, platform-specific ID, languages, install scope, and more |
| Supported platforms | Windows, iOS/iPadOS, macOS, Android, AOSP | Windows (macOS, iOS/iPadOS, and Android support planned) |
| Admin center location | **Apps** > **Monitor** > **Discovered apps** | **Apps** > **Monitor** > **All apps** > **App Inventory** tab |
| Install scope tracking | No | Yes (Device or User) |

Both features can run simultaneously. App inventory doesn't disable Discovered apps.

## Known limitations

- App inventory is currently available for Windows 10/11 devices that are Microsoft Entra joined.
- Sovereign cloud availability: Supported in GCC High. Not supported in Microsoft Azure operated by 21Vianet.

## Related content

- [Discovered apps](app-discovered-apps.md)
- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
- [App types in Microsoft Intune](apps-add.md#app-types-in-microsoft-intune)
