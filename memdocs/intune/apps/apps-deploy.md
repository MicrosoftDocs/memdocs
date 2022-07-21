---
# required metadata

title: Assign apps to groups in Microsoft Intune
titleSuffix:
description: Learn how to assign an Intune app to groups of users or devices using Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/29/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: dc349e22-9e1c-42ba-9e70-fb2ef980ef7a

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Assign apps to groups with Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

After you've [added an app](apps-add.md) to Microsoft Intune, you can assign the app to users and devices. It is important to note that you can deploy an app to a device whether or not the device is managed by Intune.

> [!NOTE]
> The **Available for enrolled devices** deployment intent is supported for **user groups** and **device groups** when targeting Android Enterprise fully managed devices (COBO) and Android Enterprise corporate-owned personally-enabled (COPE) devices.

The following table lists the various options for *assigning* apps to users and devices:

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
> *Available assignments* are only valid for user groups, not device groups.
> 
> If Managed Google Play Pre-Production track apps are assigned as required on Android Enterprise personally-owned work profile devices, they will not install on the device. To work around this, create two identical user groups and assign the pre-production track as "available" to one and "required" to the other. The result will be that the pre-production track successfully deploys to the device. 

## Assign an app

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps**.
3. In the **Apps** pane, select the app you want to assign.
4. In the **Manage** section of the menu, select **Assignments**.
5. Select **Add Group** to open the **Add group** pane that is related to the app.
6. For the specific app, select an **assignment type**:
   - **Available for enrolled devices**: Assign the app to groups of users who can install the app from the Company Portal app or website.
   - **Available with or without enrollment**: Assign this app to groups of users whose devices are not enrolled with Intune. Users must be assigned an Intune license, see [Intune Licenses](../fundamentals/licenses.md).
   - **Required**: The app is installed on devices in the selected groups. Some platforms may have additional prompts for the end user to acknowledge before app installation begins.
   - **Uninstall**: The app is uninstalled from devices in the selected groups if Intune has previously installed the application onto the device via an "Available for enrolled devices" or "Required" assignment using the same deployment. 

     > [!NOTE]
     > **For iOS/iPadOS apps only**:
     > - To configure what happens to managed apps when devices are no longer managed, you can select the intended setting under **Uninstall on device removal**. For more information, see [App uninstall setting for iOS/iPadOS managed apps](apps-deploy.md#app-uninstall-setting-for-ios-managed-apps).
     > - If you have created an iOS/iPadOS VPN profile that contains per-app VPN settings, you can select the VPN profile under **VPN**. When the app is run, the VPN connection is opened. For more information, see [VPN settings for iOS/iPadOS devices](../configuration/vpn-settings-ios.md).
     > - To configure whether a required iOS/iPadOS app is installed as a removable app by end users, you can select the setting under **Install as removable**. 
	 >
     > **For Android apps only**: 
	 > - If you deploy an Android app as **Available with or without enrollment**, reporting status will only be available on enrolled devices.
     >
     > **For Available for enrolled devices**: 
	 > - The app is only displayed as available if the user logged into the Company Portal is the primary user who enrolled the device and the app is applicable to the device.

7. To select the groups of users that are affected by this app assignment, select **Included Groups**.
8. After you have selected one or more groups to include, select **Select**.
9. In the **Assign** pane, select **OK** to complete the included groups selection.
10. If you want to exclude any groups of users from being affected by this app assignment, select **Exclude Groups**.
11. If you have chosen to exclude any groups, in **Select groups**, select **Select**.
12. In the **Add group** pane, select **OK**.
13. In the app **Assignments** pane, select **Save**.

The app is now assigned to the groups that you selected. For more information about including and excluding app assignments, see [Include and exclude app assignments](apps-inc-exl-assignments.md).

> [!Tip]
> Intune supports assigning apps to nested groups too. For example, if you assigned an app to the "Engineering Global" group and have "Engineering APAC", "Engineering EMEA" and "Engineering US" nested as child groups, the members of those child groups will also be targeted with the assignment.

## How conflicts between app intents are resolved

A single group is prevented from being targeted for multiple app assignment intents, however if a user or a device is a member of multiple groups that are each assigned with different intents it will result in a conflict. Creating assignment conflicts for applications is not recommended.
The information in the following table can help you understand the resulting intent when a conflict occurs:

| Group 1 intent | Group 2 intent | Resulting intent |
|-----------------------------------|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|User Required|User Available|Required and Available|
|User Required|User Uninstall|Required|
|User Available|User Uninstall|Uninstall|
|User Required|Device Required|Both exist, Intune treats Required
|User Required|Device Uninstall|Both exist, Intune resolves Required
|User Available|Device Required|Both exist, Intune resolves Required (Required and Available)
|User Available|Device Uninstall|Both exist, Intune resolves Available.<br><br>App shows up in the Company Portal.<br><br>If the app is already installed (as a required app with previous intent), the app is uninstalled.<br><br>If the user selects **Install from the Company Portal**, the app is installed, and the uninstall intent is not honored.|
|User Uninstall|Device Required|Both exist, Intune resolves Required|
|User Uninstall|Device Uninstall|Both exist, Intune resolves Uninstall|
|Device Required|Device Uninstall|Required|
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
> When conflicts occur in **Uninstall on device removal** setting, the app is not removed from the device when the device is no longer managed.

> [!NOTE]
> Apps deployed as Required to corporate-owned work profile devices cannot be uninstalled manually by the user.

## Managed Google Play app deployment to unmanaged devices

For unenrolled Android devices, you can use Managed Google Play to deploy store apps and line-of-business (LOB) apps to users. Once deployed, you can use [Mobile Application Management (MAM)](../apps/android-deployment-scenarios-app-protection-work-profiles.md#mam) to manage the applications. Managed Google Play apps targeted as **Available with or without enrollment** will appear in the Play Store app on the end user's device, and not in the Company Portal app. End user will browse and install apps deployed in this manner from the Play app. Because the apps are being installed from managed Google Play, the end user will not need to alter their device settings to allow app installation from unknown sources, which means the devices will be more secure. If the app developer publishes a new version of an app to Play that was installed on a user's device, the app will be automatically updated by Play. 

Steps to assign a Managed Google Play app to unmanaged devices:

1. Connect your Intune tenant to managed Google Play. If you have already done this in order to manage Android Enterprise personally-owned, dedicated, fully managed, or corporate-owned work profile devices, you do not need to do it again.
2. Add apps from managed Google Play to your Intune console.
3. Target managed Google Play apps as **Available with or without enrollment** to the desired user group. **Required** and **Uninstall** app targeting are not supported for non-enrolled devices.
4. Assign an App Protection Policy to the user group.
5. User logs in any protected app.
6. The next time the end user opens the Company Portal app and completes the log in process, they will see a message indicating in the Apps section that there are apps available for them. The user can select this notification to navigate to the Play Store.

   > [!NOTE]
   > You can configure [device enrollment setting options](./company-portal-app.md#device-enrollment-setting-options) to be **Available, no prompts** or **Unavailable**. This setting will prevent user from unintentionally enrolling their device or receiving notifications to enroll their device after they logged in to the Company Portal.

6. The end user can expand the context menu within the Play Store app and switch between their personal Google account (where they see their personal apps), and their work account (where they will see store and LOB apps targeted to them). End users install the apps by tapping Install in the Play Store app.

When an APP selective wipe is issued in the Intune console, the work account will be automatically removed from the Play Store app and the end user will from that point no longer see work apps in the Play Store app catalog. When the work account is removed from a device, apps installed from the Play Store will remain installed on the device and will not uninstall. 

## App uninstall setting for iOS managed apps
For iOS/iPadOS devices, you can choose what happens to managed apps on unenrolling the device from Intune or removing the management profile using **Uninstall on device removal** setting. This setting only applies to apps after the device is enrolled and apps are installed as managed. The setting cannot be configured for web apps or web links. Only data protected by Mobile Application Management (MAM) is removed after retirement by an App Selective Wipe.

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
