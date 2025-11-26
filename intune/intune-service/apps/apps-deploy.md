---
title: Assign Apps to Groups in Microsoft Intune
description: Learn how to assign an Intune app to groups of users or devices using Microsoft Intune.
ms.date: 11/18/2025
ms.topic: how-to
ms.reviewer: bryanke
ms.collection:
- M365-identity-device-management
- highpri
- FocusArea_Apps_Deploy
---

# Assign Apps to Groups With Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

After you [add an app](apps-add.md) to Microsoft Intune, you can assign the app to users and devices. You can deploy an app to a device whether or not the device is managed by Intune.

> [!NOTE]
> The **Available for enrolled devices** deployment intent is supported for **user groups** and **device groups**. This applies when targeting Android Enterprise fully managed devices (COBO) and Android Enterprise corporate-owned personally enabled (COPE) devices.

## Options when assigning managed apps

The following table lists the various options when *assigning* apps to users and devices:

| Option  | Devices enrolled with Intune | Devices not enrolled with Intune |
|-------------------------------------------------------------------------------------------|------------------------------|----------------------------------|
| Assign to users | Yes | Yes |
| Assign to devices | Yes | No |
| Assign wrapped apps or apps that incorporate the Intune SDK (for app protection policies) | Yes | Yes |
| Assign apps as Available | Yes | Yes |
| Assign apps as Required | Yes | No |
| Uninstall apps | Yes | No |
| Receive app updates from Intune | Yes | No |
| End users install available apps from the Company Portal app | Yes | No |
| End users install available apps from the web-based Company Portal | Yes | Yes |

> [!NOTE]
> Currently, you can assign iOS/iPadOS and Android apps (line-of-business and store-purchased apps) to devices that aren't enrolled with Intune.
>
> Device users with devices that aren’t enrolled in Intune must open their organization’s Company Portal and install app updates manually.
> 
> For almost all app types and platforms, *Available assignments* are only valid when assigning to user groups, not device groups. Win32 apps can be assigned to either user or device groups.
>
> If managed Google Play preproduction track apps are assigned as required on Android Enterprise personally owned work profile devices, they don't install on the device. To work around this issue, create two identical user groups. Assign the preproduction track as "available" to one group and "required" to the other group. The result is that the preproduction track successfully deploys to the device.

## Assign an app

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All Apps**.
3. In the **Apps** pane, select the app you want to assign.
4. In the **Manage** section of the menu, select **Properties**.
5. Scroll down to **Properties** and select **Assignments**.
6. Select **Add Group** to open the **Add group** pane that relates to the app.
7. For the specific app, select an **assignment type**:
   - **Available for enrolled devices**: Assign the app to groups of users who can install the app from the Company Portal app or website.
   - **Available with or without enrollment**: Assign this setting to groups of users whose devices aren't enrolled with Intune. Users must be assigned an Intune license, see [Intune Licenses](../fundamentals/licenses.md).
   - **Required**: The app is installed on devices in the selected groups. Some platforms might have more prompts for the end user to acknowledge before app installation begins.
   - **Uninstall**: The app is uninstalled from devices in the selected groups if Intune previously installed the application. This applies only to apps installed via an "Available for enrolled devices" or "Required" assignment using the same deployment.

     > [!NOTE]
     > **For iOS/iPadOS apps only**:
     > - To configure what happens to managed apps when devices are no longer managed, you can select the intended setting under **Uninstall on device removal**. For more information, see [App uninstall setting for iOS/iPadOS managed apps](apps-deploy.md#app-uninstall-setting-for-ios-managed-apps).
     > - If you create an iOS/iPadOS VPN profile that contains per-app VPN settings, you can select the VPN profile under **VPN**. When the app runs, the VPN connection opens. For more information, see [VPN settings for iOS/iPadOS devices](../configuration/vpn-settings-ios.md).
     > - To configure whether a required iOS/iPadOS app is installed as a removable app by end users, you can select the setting under **Install as removable**.
     > - To prevent the iCloud backup of the managed iOS/iPadOS app, select one of the following settings after adding a group assignment: VPN, Uninstall on device removal, or Install as removable. Then, configure the setting called Prevent iCloud app backup. For more information, see [Prevent iCloud app backup setting for iOS/iPadOS and macOS apps](#prevent-icloud-app-backup-setting-for-iosipados-and-macos-apps).
	  >
     > **For macOS apps only**:
     > - To prevent the iCloud backup of the managed macOS app, select one of the following settings after adding a group assignment: VPN, Uninstall on device removal, or Install as removable. Then, configure the setting called Prevent iCloud app backup. For more information, see [Prevent iCloud app backup setting for iOS/iPadOS and macOS apps](#prevent-icloud-app-backup-setting-for-iosipados-and-macos-apps).
	  >
     > **For Android apps only**:
	  > - If you deploy an Android app as **Available with or without enrollment**, reporting status is only available on enrolled devices.
     >
     > **For Available for enrolled devices**:
	  > - The app is only displayed as available if the user who logs into the Company Portal is the primary user who enrolled the device and the app is applicable to the device.

8. To select the groups of users affected by this app assignment, select **Included Groups**.
9. After you select one or more groups to include, select **Select**.
10. In the **Assign** pane, select **OK** to complete the included groups selection.
11. If you want to exclude any groups of users affected by this app assignment, select **Exclude Groups**.
12. If you choose to exclude any groups, in **Select groups**, select **Select**.
13. In the **Add group** pane, select **OK**.
14. In the app **Assignments** pane, select **Save**.

The app is now assigned to the groups that you selected.

> [!NOTE]
> If Microsoft Entra soft-deletes any of these groups, Intune shows them as soft deleted in the console, and their assignments don’t apply until the groups are restored.

For more information about including and excluding app assignments, see [Include and exclude app assignments](apps-inc-exl-assignments.md).

> [!NOTE]
> You see the status of the selected group in the assignments. The possible status options are: Active, Deleted, or Soft-Deleted.

> [!Tip]
> Intune supports assigning apps to nested groups. For example, if you assign an app to the "Engineering Global" group and have "Engineering APAC", "Engineering EMEA" and "Engineering US" nested as child groups, the assignment also targets members of those child groups.

## Prevent iCloud app backup setting for iOS/iPadOS and macOS apps

Admins have the option to no longer backup managed App Store apps and line-of-business (LOB) apps on iOS/iPadOS and managed App Store apps on macOS devices. This applies to both user and device licensed VPP/non-VPP apps. macOS LOB apps don't support this setting.

This functionality includes both new and existing App Store/LOB apps sent with and without VPP that are added to Intune and targeted to users and devices. Preventing the backup of the specified managed apps ensures proper deployment via Intune when the device is enrolled and restored from backup.

If you configure the new setting for new/existing apps in your tenant, managed apps can be reinstalled for devices, but Intune no longer allows them to be backed up.

> [!NOTE]
> While we don't expect managed apps on devices to backup data to iCloud, data saved locally for managed apps might not be available after a backup and restore.

For existing devices, when **Prevent iCloud app backup** is set to **Yes** for an app or apps, the new behavior is automatically updated for all required App Store/LOB apps (with or without VPP).

Required apps previously installed on devices are automatically reconfigured for all devices once the setting value is saved to **Yes**.

Available apps require the user to redownload the available app from the Company Portal app or the [Company Portal website](https://portal.manage.microsoft.com). Depending on the app's configurations and licensing, a sync between Intune and the device might be needed.

## How conflicts between app intents are resolved

A single group is prevented from being targeted for multiple app assignment intents. However, if a user or device is a member of multiple groups that are each assigned with different intents, a conflict results. Creating assignment conflicts for applications isn't recommended.
The information in the following table can help you understand the resulting intent when a conflict occurs:

> [!NOTE]
> If there are assignment conflicts for applications, the assignment filter might not work as expected because the assignment intent is evaluated before the assignment filter.

| Group 1 intent | Group 2 intent | Resulting intent |
|-----------------------------------|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|User Required|User Available|Required and Available|
|User Required|User Uninstall|Required|
|User Available|User Uninstall|Uninstall|
|User Required|Device Required|Both exist, Intune treats Required
|User Required|Device Uninstall|Both exist, Intune resolves Required
|User Available|Device Required|Both exist, Intune resolves Required (Required and Available)
|User Available|Device Uninstall|Both exist, Intune resolves Available.<br><br>App appears in the Company Portal.<br><br>If the app is already installed (as a required app with previous intent), the app is uninstalled.<br><br>If the user selects **Install from the Company Portal**, the app is installed, and the uninstall intent isn't honored.|
|User Uninstall|Device Required|Both exist, Intune resolves Required|
|User Uninstall|Device Uninstall|Both exist, Intune resolves Uninstall|
|Device Required|Device Uninstall|Required|
|Device Required|Device Available|Required and Available|
|Device Available|Device Uninstall|Uninstall|
|User Required and Available|User Available|Required and Available|
|User Required and Available|User Uninstall|Required and Available|
|User Required and Available|Device Required|Both exist, Required and Available
|User Required and Available|Device Uninstall|Both exist, Intune resolves Required (Required and Available)
|User Available without enrollment|User Required and Available|Required and Available
|User Available without enrollment|User Required|Required
|User Available without enrollment|User Available|Available|
|User Available without enrollment|Device Required|Required and Available without enrollment|
|User Available without enrollment|Device Uninstall|Uninstall and Available without enrollment.<br><br>If the user didn't install the app from the Company Portal, the uninstall is honored.<br><br>If the user installs the app from the Company Portal, the install is prioritized over the uninstall.|

> [!NOTE]
> For managed iOS store apps only, when you add these apps to Microsoft Intune and assign them as **Required**, the apps are automatically created. They receive both **Required** and **Available** intents.<br><br>
> iOS Store apps (not iOS/iPadOS VPP apps) that are targeted with required intent are enforced on the device at the time of the device check-in and also appear in the Company Portal app.<br><br>
> When conflicts occur in **Uninstall on device removal** setting, the app isn't removed from the device when the device is no longer managed.

> [!NOTE]
> Apps deployed as Required to corporate-owned work profile and corporate-owned fully managed devices can't be uninstalled manually by the user.

## Managed Google Play app deployment to unmanaged devices

For unenrolled Android devices, you can use managed Google Play to deploy store apps and line-of-business (LOB) apps to users. Once deployed, you can use [Mobile Application Management (MAM)](../apps/android-deployment-scenarios-app-protection-work-profiles.md#mam) to manage the applications.

Managed Google Play apps targeted as **Available with or without enrollment** appear in the Play Store app on the end user's device, and not in the Company Portal app. End users browse and install apps deployed in this manner from the Play app.

Because the apps are installed from managed Google Play, the end user doesn't need to alter their device settings to allow app installation from unknown sources. This means the devices are more secure. If the app developer publishes a new version of an app to Play that was installed on a user's device, the app is automatically updated by Play.

Steps to assign a Managed Google Play app to unmanaged devices:

1. Connect your Intune tenant to managed Google Play. If you already did this to manage Android Enterprise personally owned, dedicated, fully managed, or corporate-owned work profile devices, you don't need to do it again.
2. Add apps from managed Google Play to your Intune admin center.
3. Target managed Google Play apps as **Available with or without enrollment** to the desired user group. **Required** and **Uninstall** app targeting aren't supported for nonenrolled devices.
4. Assign an App Protection Policy to the user group.
5. User logs in any protected app.
6. The next time the end user opens the Company Portal app and completes the sign in process, they see a message in the Apps section. This message indicates that there are apps available for them. The user can select this notification to navigate to the Play Store.

   > [!NOTE]
   > You can configure [device enrollment setting options](./company-portal-app.md#device-enrollment-setting-options) to be **Available, no prompts** or **Unavailable**. This setting prevents users from unintentionally enrolling their device. It also prevents notifications to enroll after they sign in to the Company Portal.

6. The end user can expand the context menu within the Play Store app and switch between their personal Google account (where they see their personal apps), and their work account (where they see store and LOB apps targeted to them). End users install the apps by tapping Install in the Play Store app.

When an APP selective wipe is issued in the Intune admin center, the work account is automatically removed from the Play Store app. The end user no longer sees work apps in the Play Store app catalog from that point.

When the work account is removed from a device, apps installed from the Play Store remain installed on the device and don't uninstall.

## App uninstall setting for iOS managed apps

For iOS/iPadOS devices, you can choose what happens to managed apps on unenrolling the device from Intune or removing the management profile using **Uninstall on device removal** setting. This setting only applies to apps after the device is enrolled and apps are installed as managed. The setting can't be configured for web apps or web links. Only data protected by Mobile Application Management (MAM) is removed after retirement by an App Selective Wipe.

Default values for the setting are prepopulated for new assignments as follows:

|iOS app type | Default setting for "Uninstall on device removal" |
|--------------------|----------------|
| Line-of-business app | Yes |
| Store app | No |
| VPP app | No |
| Built-in app | No |

>[!NOTE]
>**"Available" assignment types:** If you're updating this setting for "available for enrolled devices" or "available with or without enrollment" groups, users who already have the managed app don't get the updated setting until they sync the device with Intune and reinstall the app.
>
>**Pre-existing assignments:** The App uninstall setting was introduced in May 2019. Assignments that existed before this date are unmodified and all managed apps are removed on device removal from management.
>
> If your assignment was created before May 2019, you might need to explicitly set the App uninstall setting. The default settings might not apply to older assignments.

## Next steps

To learn more about monitoring app assignments, see [How to monitor apps](apps-monitor.md).
