---
title: Troubleshooting and monitoring Remote Help for Microsoft Intune.
description: Use the troubleshooting and monitoring information for Remote Help with Microsoft Intune to ensure healthy and successful deployment.
author: lenewsad
ms.author: lanewsad
ms.date: 10/01/2025
ms.topic: how-to
ms.localizationpriority: high
ms.reviewer: Karawang
ms.collection:
- M365-identity-device-management
- highpri
- highseo
---

# Troubleshoot and Monitor Remote Help

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

[!INCLUDE [remote-help-overview](includes/remote-help-overview.md)]

## Monitoring and reports

You can monitor the use of Remote Help from within the Microsoft Intune admin center. For unenrolled devices, reporting on Remote Help sessions is limited.

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant admin** > **Remote Help**.

2. On the Monitor tab, you can see a count of active sessions and historical data about past sessions.

3. On the Remote Help sessions tab, you can see the records of past sessions, including:
   - The helper (Provider ID) and sharer (Recipient ID) of each session.
   - The device that received assistance.
   - The start and end time of the Remote Assistance session.
   - The type of control session.

> [!NOTE]
> The Recipient ID and Recipient name display "--" for Android Enterprise Dedicated devices, as these devices do not have user affinity.

## Monitor

- **Session Reports and Audit Logs**: In the Intune admin center, go to Reports > Endpoint analytics > Remote Help (or under Tenant Administration > Remote Help) to see session reports. Intune records who (helper) connected to which device/user (sharer), the start and end times, and whether the session was view-only or with full control. These logs persist for 30 days on Microsoft's servers. Additionally, you can access the same session reports from the main Intune's Audit Logs (under Tenant Administration). Use these reports for auditing support activities and measuring helpdesk engagement. For privacy, note that session content (screen images or keystrokes) is not recorded by Microsoft – only metadata is stored.

## Log files

Remote Help logs data during installation and during Remote Help sessions, which can be of use when investigating issues with the app.

### [Windows](#tab/windows)

**Installation of Remote Help** - When Remote Help installs or uninstalls, the following two logs are created in the device users' Temp folder, for example, `C:\Users\<username>\AppData\Local\Temp`. The \* in the log file name represents a date and time stamp of when the log was created.

- Remote_help_*_QuickAssist_Win10_x64.msi.log
- Remote_help_*.log

**Operational logs** - During use of Remote Help, operational details are logged in the Windows Event Viewer:

- Event Viewer > Application and Services > Microsoft > Windows > RemoteHelp

### [macOS](#tab/macos)

### [Android](#tab/android)

## Troubleshoot

- If a helper sees a message "Remote Help isn't enabled for this tenant" or cannot start a session, double-check licensing and that the feature was enabled in Tenant Admin. It can take up to 30 minutes (or a few hours in some cases) after assigning licenses for the service to activate.
- If the "New Remote Assistance Session" option is not visible for a helper in Intune, ensure the helper's account is in the Intune role with Remote Help permissions and the "Offer remote assistance" permission (or try re-assigning the role).
- A session failing to connect (after code entry) with a permission error likely indicates the helper's RBAC scope does not cover that user/device. Verify the scope group includes the target user/device and that the helper has the needed permission (e.g., trying to take full control but their role only allows view).
- If Remote Help app on Windows won't install or silently fails, ensure the device meets OS requirements (Windows build, etc.) and has TLS 1.2 network connectivity. Also check that the Intune Win32 app detection rule (if used) is correct (incorrect version detection can cause Intune to think the app is already installed or never installed).
- On Android, if the device is not visible for Remote Help or the app is not functioning, ensure the device is enrolled as Dedicated. COPE/COBO devices are not currently supported by Remote Help – trying to use it on unsupported enrollment types will not work.
- Mac users having trouble should verify they installed the app from Company Portal and approved permissions. If using the web app, note it only allows view access, which might confuse helpers expecting control.
- If the session displays a white screen while attempting to connect, verify that all network requirements are properly configured and that no required endpoints are being blocked.

### Troubleshooting Remote Help on Windows for Edge WebView2

You might see an error code in a dialog box if you're having trouble installing and running Remote Help. The error might be related to Microsoft Edge WebView 2, which is required to use Remote Help. Here are some error codes you might see along with a short description of the problem.

|Error Code |General Problem |
|-----------| ----------------|
|1001|Remote Help failed to initialize one of its internal components.|
|1002|Remote Help failed to load WebView2.|
|1003|Remote Help failed to install WebView2.|

Use these steps to resolve these issues:

1. Ensure that Microsoft Edge is installed properly and is up to date.

Remote Help uses the Microsoft Edge browser control. If your device has Microsoft Edge installed, then it's likely that Remote Help will run properly. If you have problems, the common troubleshooting tips here may help get Remote Help working. Learn more about [Troubleshooting tips for installing and updating Microsoft Edge.](https://support.microsoft.com/microsoft-edge/troubleshooting-tips-for-installing-and-updating-microsoft-edge-a5eceb94-c2b1-dfab-6569-e79d0250317b)
After installing or updating Microsoft Edge, try opening Remote Help again. If Remote Help doesn't run or you get an error message that Microsoft Edge WebView2 isn't installed, go to the next step.

1. Install Microsoft Edge WebView 2

Microsoft Edge WebView2 is required to use Remote Help. If you get an error message that WebView2 isn't installed when you try to open Remote Help, then [download and install Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/consumer/?form=MA13LH) from the Microsoft website. After you've downloaded WebView2, try opening Remote Help again.

> [!NOTE]
> WebView2 should already be installed if your device is running Windows 11 or has Microsoft Edge.

## Known Issues

- For remotely starting a session on the user's device, notifications that are sent to the sharer's device when a helper launches a Remote Help session fails if the Microsoft Intune Management Service isn't running.
- After the user's device is restarted, there's a delay for the service to start. You can either manually wait for the service to start (30 minutes after restart), or manually start the service through services.msc.
 For newly enrolled devices, there's a 1 hour delay before the user's device begins receiving notifications when a helper initiates a session.


## Troubleshooting Remote Help on Android

If a Remote Help session for Android is unable to connect, check for the following possibilities:

  | Check if                      | Solution                                           |
  |-----------------------------------|-----------------------------------------------|
  | The device has been newly enrolled with Intune. | On newly enrolled devices, push notifications (needed for Remote Help to receive session initiation requests) may take a while to start working. Wait for 15 minutes and try again later.|
  | The Remote Help app isn't installed. | Install the app, see [Remote Help on Android](remote-help-android.md#deploy-remote-help-app) for details. |
  | All the required permissions have been granted to the Remote Help app. | Review and ensure that all required permissions are granted. See [Remote Help on Android](remote-help-android.md#prerequisites-for-remote-help-on-android) for details. |
  | The Intune app version isn't updated. | Update the Intune app to the latest version. |
  | The device doesn't have access to Google services. | Remote Help requires access to Google Mobile Services to function, so make sure the device has Google services. You can do this by verifying that the Play Store is present on the device. See [Android: Google Mobile Services](https://www.android.com/gms/). |
  | There's no response from the end user. | Screen Sharing and Full Control Sessions time out automatically after 5 minutes if there's no response from [Android: Google Mobile Services](https://www.android.com/gms/) on the end user device. Make sure the user accepts the prompt to start the session. |
  | The device manufacturer or OS/Zebra MX/Samsung Knox version isn't supported | Make sure the device is supported. See [Remote Help on Android](remote-help-android.md#supported-devices) |
  | (On Samsung devices only) The Knox license on the device is expired/invalid or has network issues.  | Make sure that all Knox permissions have been granted, and that the device has an active Knox license; see [License activation errors](https://configure.samsungknox.com/files/knox-configure-getting-started/Content/license-activation-errors.htm) for troubleshooting Knox activation errors. |
  | (On Samsung devices only) Other apps are actively using the Samsung Knox remote desktop APIs (you're using another remote assistance app on the device). | Close or uninstall any other apps that may be using remote viewing/control capabilities on the device. |


## Known Issues macOS

- If the sharer exits from a Remote Help session early, the helper might not be notified for 60+ seconds.

- If using Edge, the sharer might have to sign in to Edge before starting a session or the device reports as Unenrolled.

- Verify that your browser is up to date.

- If you're screen sharing using another application like Teams or recording during the session, it might take longer for the session to connect.


## Known Issues web app

- If the sharer exits from a Remote Help session early, the helper may not be notified for 60+ seconds.

- If using Edge, it may require the sharer to sign in to Edge before starting a session or the device is reported as Unenrolled.

- SSO must be enabled for the tenant to use the Remote Help web app.


## Next steps

[Get support in Microsoft Intune admin center.](../../get-support.md)
