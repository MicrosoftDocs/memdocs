---
# Required metadata
# For more information, see https://learn.microsoft.com/en-us/help/platform/learn-editor-add-metadata
# For valid values of ms.service, ms.prod, and ms.topic, see https://learn.microsoft.com/en-us/help/platform/metadata-taxonomies

title: App Settings Configuration for Apple Devices - Microsoft Intune | Microsoft Learn
description: Learn how to use the Microsoft Intune settings catalog to configure Apple's app settings declaration, including app launch controls and macOS binary execution controls.
author:      beflamm # GitHub alias
ms.author:   beflamm # Microsoft alias
ms.service: microsoft-intune
ms.topic: how-to
ms.date:     08/20/2026
---

# App settings configuration for Apple devices

App settings is a declarative configuration in the Microsoft Intune settings catalog that lets you control which apps and binaries are allowed to launch or run on supervised Apple devices. The settings catalog exposes this configuration directly from Apple's declarative device management (DDM) `App Settings` declaration, so the settings you see in Intune match the keys Apple defines for the platform.

## Prerequisites

**Device platform requirements**

This configuration supports the following platforms:

- iOS/iPadOS 27+ (supervised)

- macOS 27+ (supervised)

## How to configure app settings using the settings catalog

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration** > **Create** > **New policy**.
1. For **Platform**, select **macOS** or **iOS/iPadOS**

4. For **Profile type**, select **Settings catalog**, then select **Create**.
5. On the **Basics** page, enter a name and description, then select **Next**.
1. On the **Configuration settings** page, select **Add settings**

1. In the settings picker, expand **Declarative Device Management (DDM)**, select **App Settings**

1. Expand the **App Settings** category and select the settings you want to configure:
   - **Allowed apps** / **Denied apps** to control which apps can launch (iOS/iPadOS).
      
   - **Allowed binaries** / **Denied binaries** and **Always allow managed apps** to control which binaries can run (macOS).
8. Configure the values for each setting you added. See [Available settings reference](#available-settings-reference) for details on each key.
9. Select **Next**, configure **Scope tags** and **Assignments**, then select **Next** again.
10. Review your settings on the **Review + create** page, then select **Create**.

## Available settings reference

### App launch control (Allowed Apps, Denied Apps)

> [!NOTE]
> The `Allowed app bundle IDs` and `Denied app bundle IDs` settings in the Restrictions profile that was previously used to manage app launch on iOS is deprecated in iOS 27. Migrate existing app launch restrictions to app settings.

| Setting | Description |Example|
| --- | --- | -------- |
| `Allowed Apps` | Enter the bundle IDs of apps you want to allow. If present, the device only shows or launches apps with a listed bundle ID. Use the value `com.apple.webapp` to allow all web clips. Applies to App Store apps, marketplace apps, and locally installed apps. |`com.example.app`|
| `Denied Apps` | Enter the bundle IDs of apps you want to deny. If present, the device prevents showing or launching any listed app. |`com.example.app`|

> [!IMPORTANT]
> Adding an app to the Denied Apps list will not prevent it from being installed on the device. Being a member of the Denied Apps list will only prevent displaying the app on the device, and will prevent it from being launched. 

> [!NOTE]
> If a bundle ID appears in both lists, the device blocks it from launching. Denying system apps can disable other functionality—for example, denying the App Store app can prevent users from accepting Volume Purchase Program (VPP) terms.

### Binary execution control (Allowed Binaries, Denied Binaries, Always Allow Managed Apps)

On macOS, app settings uses the Endpoint Security extension framework to control which binaries—standalone or embedded in an app bundle—are allowed to run. The device always permits system-critical processes signed and sealed as part of the operating system.

| Setting | Description |
| --- | --- |
| `Allowed Binaries` | Enter the binary identifiers that you want to allow on the device. If present, the device only allows binaries matching one of the listed identifiers to run. A binary matches only when all fields in its identifier match. |
| `Denied Binaries` | Enter the binary identifiers you want to prevent on the device. If present, the device blocks binaries matching a listed identifier from running. |
| `Always Allow Managed Apps` | Boolean (default `false`). If `true`, apps deployed as managed apps are automatically included in the effective allow list, reducing ruleset maintenance. This only applies to apps managed through VPP or apps installed using the Line-of-business app type. This doesn't include apps installed using the Line-of-business (PKG) or Line-of-business (DMG) app types which are installed using the Intune agent. |

Each binary identifier can include:

| Field | Description |Example|
| --- | --- | -------- |
| `CDHash` | The 40-character code directory hash of the binary. |90bc96cd95be55c12e7d9b1611cbc677610bb70c|
| `SigningID` | The code signature signing identifier of the binary. |com.example.app|
| `TeamID` | The code signature team identifier. Use `*APPLE*` for Apple binaries with an empty team identifier. |XXXXXXXXXX|
| `PathPrefix` | The file system path prefix used to match binaries. |/Applications/Example.app|
| `SigningState` | One of `All`, `TestFlight`, `DeveloperID`, `Enterprise`, `AppStore`, or `Apple` (default `All`). |All|

> [!IMPORTANT]
> For `Allowed Binaries`, either `CD Hash` or `Team ID` must be present. For `Denied Binaries`, one of `CD Hash`, `Team ID`, or `SigningID` must be present. Use `codesign -dvvv <path_to_binary>` on the binary to generate these values.

## Monitor status

App settings assignment status is reported through Apple's DDM status channel. Review policy status on the **Device status** and **Per-setting status** tabs of the configuration profile in the Intune admin center, and check [audit logs](/intune/intune-service/fundamentals/monitor-audit-logs) for changes to the policy.

## Related Apple documentation

App settings is defined by Apple as a declarative device management configuration. For the authoritative schema and additional examples, see:

- [`app.settings` configuration](https://github.com/apple/device-management/blob/seed_OS_27_0/declarative/declarations/configurations/app.settings.yaml) in Apple's device management GitHub repository—the source schema the settings catalog surfaces.
- [WWDC26 app management updates](https://support.apple.com/en-euro/guide/deployment/depd567c9ffa/1/web/1.0) in Apple's Deployment Guide—background on app launch control, binary execution control, and privacy consent updates.
## Next steps

- [Use the settings catalog to view and configure settings](/intune/intune-service/configuration/settings-catalog)
- [Create a policy using settings catalog](../settings-catalog/index.md#create-the-policy)
- [iOS/iPadOS device settings you can manage with Intune](/intune/intune-service/configuration/device-restrictions-ios)
