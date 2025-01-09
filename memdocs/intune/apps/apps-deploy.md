---
# required metadata

title: Assign apps to groups in Microsoft Intune
titleSuffix:
description: Learn how to assign an Intune app to groups of users or devices using Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: dc349e22-9e1c-42ba-9e70-fb2ef980ef7a

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: bryanke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- FocusArea_Apps_Deploy
---

# Assign apps to groups with Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

After you've [added an app](apps-add.md) to Microsoft Intune, you can assign the app to users and devices. It's important to note that you can deploy an app to a device whether or not the device is managed by Intune.

> [!NOTE]
> The **Available for enrolled devices** deployment intent is supported for **user groups** and **device groups** when targeting Android Enterprise fully managed devices (COBO) and Android Enterprise corporate-owned personally enabled (COPE) devices.

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
> To receive app updates on devices that aren't enrolled with Intune, device users must go to their organization's Company Portal and manually install app updates.
> 
> For almost all app types and platforms, *Available assignments* are only valid when assigning to user groups, not device groups. Win32 apps can be assigned to either user or device groups.
> 
> If managed Google Play preproduction track apps are assigned as required on Android Enterprise personally owned work profile devices, they won't install on the device. To work around this, create two identical user groups and assign the preproduction track as "available" to one and "required" to the other. The result will be that the preproduction track successfully deploys to the device. 

## Assign an app

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps**.
3. In the **Apps** pane, select the app you want to assign.
4. In the **Manage** section of the menu, select **Properties**.
5. Scroll down to **Properties** and select **Assignments**.
6. Select **Add Group** to open the **Add group** pane that is related to the app.
7. For the specific app, select an **assignment type**:
   - **Available for enrolled devices**: Assign the app to groups of users who can install the app from the Company Portal app or website.
   - **Available with or without enrollment**: Assign this app to groups of users whose devices aren't enrolled with Intune. Users must be assigned an Intune license, see [Intune Licenses](../fundamentals/licenses.md).
   - **Required**: The app is installed on devices in the selected groups. Some platforms may have additional prompts for the end user to acknowledge before app installation begins.
   - **Uninstall**: The app is uninstalled from devices in the selected groups if Intune has previously installed the application onto the device via an "Available for enrolled devices" or "Required" assignment using the same deployment. 

     > [!NOTE]
     > **For iOS/iPadOS apps only**:
     > - To configure what happens to managed apps when devices are no longer managed, you can select the intended setting under **Uninstall on device removal**. For more information, see [App uninstall setting for iOS/iPadOS managed apps](apps-deploy.md#app-uninstall-setting-for-ios-managed-apps).
     > - If you have created an iOS/iPadOS VPN profile that contains per-app VPN settings, you can select the VPN profile under **VPN**. When the app is run, the VPN connection is opened. For more information, see [VPN settings for iOS/iPadOS devices](../configuration/vpn-settings-ios.md).
     > - To configure whether a required iOS/iPadOS app is installed as a removable app by end users, you can select the setting under **Install as removable**. 
     > - To configure a way to prevent the iCloud backup of the managed iOS/iPadOS app, you can select on one of the following settings after adding a group assignment - VPN, or Uninstall on device removal, or Install as removable. Then, configure the setting called Prevent iCloud app backup. For more information, see [Prevent iCloud app backup setting for iOS/iPadOS and macOS apps](#prevent-icloud-app-backup-setting-for-iosipados-and-macos-apps).
	  >
     > **For macOS apps only**: 
     > - To configure a way to prevent the iCloud backup of the managed macOS app, you can select on one of the following settings after adding a group assignment - VPN, or Uninstall on device removal, or Install as removable. Then, configure the setting called Prevent iCloud app backup. For more information, see [Prevent iCloud app backup setting for iOS/iPadOS and macOS apps](#prevent-icloud-app-backup-setting-for-iosipados-and-macos-apps).
	  >
     > **For Android apps only**: 
	  > - If you deploy an Android app as **Available with or without enrollment**, reporting status will only be available on enrolled devices.
     >
     > **For Available for enrolled devices**: 
	  > - The app is only displayed as available if the user logged into the Company Portal is the primary user who enrolled the device and the app is applicable to the device.

8. To select the groups of users that are affected by this app assignment, select **Included Groups**.
9. After you have selected one or more groups to include, select **Select**.
10. In the **Assign** pane, select **OK** to complete the included groups selection.
11. If you want to exclude any groups of users from being affected by this app assignment, select **Exclude Groups**.
12. If you have chosen to exclude any groups, in **Select groups**, select **Select**.
13. In the **Add group** pane, select **OK**.
14. In the app **Assignments** pane, select **Save**.

The app is now assigned to the groups that you selected. For more information about including and excluding app assignments, see [Include and exclude app assignments](apps-inc-exl-assignments.md).

> [!Tip]
> Intune supports assigning apps to nested groups too. For example, if you assigned an app to the "Engineering Global" group and have "Engineering APAC", "Engineering EMEA" and "Engineering US" nested as child groups, the members of those child groups will also be targeted with the assignment.

## Prevent iCloud app backup setting for iOS/iPadOS and macOS apps

Admins have the option to no longer backup managed App Store apps and line-of-business (LOB) apps on iOS/iPadOS and managed App Store apps on macOS devices, for both user and device licensed VPP/non-VPP apps. macOS LOB apps won’t support this setting. This functionality includes both new and existing App Store/LOB apps sent with and without VPP that are being added to Intune and targeted to users and devices. Preventing the backup of the specified managed apps ensure that these apps can be properly deployed via Intune when the device is enrolled and restored from backup. If you configure the new setting for new/existing apps in your tenant, managed apps can and will be reinstalled for devices, but Intune will no longer allow them to be backed up.

> [!NOTE]
> While we don't expect managed apps on devices to backup data to iCloud, note that data saved locally for managed apps may not be available after a backup and restore.

For existing devices, when **Prevent iCloud app backup** is set to **Yes** for an app/apps, the new behavior is automatically updated for all required App Store/LOB apps (with or without VPP). Required apps previously installed on devices are automatically reconfigured for all devices once the setting value is saved to **Yes**. Available apps require the user to redownload the available app from the Company Portal app or the [Company Portal website](https://portal.manage.microsoft.com). Additionally, depending on the app’s configurations and licensing, a sync between Intune and the device may be needed. 

## How conflicts between app intents are resolved

A single group is prevented from being targeted for multiple app assignment intents, however if a user or a device is a member of multiple groups that are each assigned with different intents it will result in a conflict. Creating assignment conflicts for applications isn't recommended.
The information in the following table can help you understand the resulting intent when a conflict occurs:

| Group 1 intent | Group 2 intent | Resulting intent |
|-----------------------------------|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|User Required|User Available|Required and Available|
|User Required|User Uninstall|Required|
|User Available|User Uninstall|Uninstall|
|User Required|Device Required|Both exist, Intune treats Required
|User Required|Device Uninstall|Both exist, Intune resolves Required
|User Available|Device Required|Both exist, Intune resolves Required (Required and Available)
|User Available|Device Uninstall|Both exist, Intune resolves Available.<br><br>App shows up in the Company Portal.<br><br>If the app is already installed (as a required app with previous intent), the app is uninstalled.<br><br>If the user selects **Install from the Company Portal**, the app is installed, and the uninstall intent isn't honored.|
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
> For managed iOS store apps only, when you add these apps to Microsoft Intune and assign them as **Required**, the apps are automatically created with both **Required** and **Available** intents.<br><br>
> iOS Store apps (not iOS/iPadOS VPP apps) that are targeted with required intent will be enforced on the device at the time of the device check-in and will also show in the Company Portal app.<br><br>
> When conflicts occur in **Uninstall on device removal** setting, the app isn't removed from the device when the device is no longer managed.

> [!NOTE]
> Apps deployed as Required to corporate-owned work profile and corporate-owned fully managed devices can't be uninstalled manually by the user.

## Managed Google Play app deployment to unmanaged devices

For unenrolled Android devices, you can use managed Google Play to deploy store apps and line-of-business (LOB) apps to users. Once deployed, you can use [Mobile Application Management (MAM)](../apps/android-deployment-scenarios-app-protection-work-profiles.md#mam) to manage the applications. Managed Google Play apps targeted as **Available with or without enrollment** will appear in the Play Store app on the end user's device, and not in the Company Portal app. End user will browse and install apps deployed in this manner from the Play app. Because the apps are being installed from managed Google Play, the end user won't need to alter their device settings to allow app installation from unknown sources, which means the devices will be more secure. If the app developer publishes a new version of an app to Play that was installed on a user's device, the app will be automatically updated by Play. 

Steps to assign a Managed Google Play app to unmanaged devices:

1. Connect your Intune tenant to managed Google Play. If you have already done this in order to manage Android Enterprise personally owned, dedicated, fully managed, or corporate-owned work profile devices, you don't need to do it again.
2. Add apps from managed Google Play to your Intune admin center.
3. Target managed Google Play apps as **Available with or without enrollment** to the desired user group. **Required** and **Uninstall** app targeting aren't supported for nonenrolled devices.
4. Assign an App Protection Policy to the user group.
5. User logs in any protected app.
6. The next time the end user opens the Company Portal app and completes the log in process, they'll see a message indicating in the Apps section that there are apps available for them. The user can select this notification to navigate to the Play Store.

   > [!NOTE]
   > You can configure [device enrollment setting options](./company-portal-app.md#device-enrollment-setting-options) to be **Available, no prompts** or **Unavailable**. This setting will prevent user from unintentionally enrolling their device or receiving notifications to enroll their device after they logged in to the Company Portal.

6. The end user can expand the context menu within the Play Store app and switch between their personal Google account (where they see their personal apps), and their work account (where they'll see store and LOB apps targeted to them). End users install the apps by tapping Install in the Play Store app.

When an APP selective wipe is issued in the Intune admin center, the work account will be automatically removed from the Play Store app and the end user will from that point no longer see work apps in the Play Store app catalog. When the work account is removed from a device, apps installed from the Play Store will remain installed on the device and won't uninstall. 

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
>**"Available" assignment types:** If you're updating this setting for "available for enrolled devices" or "available with or without enrollment" groups, users who already have the managed app won't get the updated setting until they sync the device with Intune and re-install the app. 
>
>**Pre-existing assignments:** The App uninstall setting was introduced in May 2019. Assignments that existed prior to this date are unmodified and all managed apps will be removed on device removal from management. If your assignment was created before May 2019, you may need to explicitly set the App uninstall setting, as the default settings above may not apply. 

## Next steps

To learn more about monitoring app assignments, see [How to monitor apps](apps-monitor.md).
