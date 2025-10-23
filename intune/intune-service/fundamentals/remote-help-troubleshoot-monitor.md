---
title: Troubleshoot and monitor Remote Help for Microsoft Intune.
description: Use the troubleshooting and monitoring information for Remote Help with Microsoft Intune to ensure healthy and successful deployment.
author: lenewsad
ms.author: lanewsad
ms.date: 10/01/2025
ms.topic: how-to
ms.localizationpriority: high
ms.reviewer: Karawang
ms.subservice: suite
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
> - The Recipient ID and Recipient name display "--" for Android Enterprise Dedicated devices, as these devices don't have user affinity.
> - The use of the Windows "elevation" capability isn't reported in the Remote Help sessions report.

These logs persist for 30 days on Microsoft's servers. The content of a session, like screen images or keystrokes, aren't recorded – only metadata is stored.

## Log files

Remote Help logs data during installation and during Remote Help sessions, which can be of use when investigating issues with the app.

**Installation of Remote Help** - When Remote Help installs or uninstalls, the following two logs are created in the device users' Temp folder, for example, `C:\Users\<username>\AppData\Local\Temp`. The `*` in the log file name represents a date and time stamp of when the log was created.

- Remote_help_*_QuickAssist_Win10_x64.msi.log
- Remote_help_*.log

**Operational logs** - During use of Remote Help, operational details are logged in the Windows Event Viewer:

- Event Viewer > Application and Services > Microsoft > Windows > RemoteHelp

## Troubleshoot

Use the table in this section to troubleshoot common issues with Remote Help.

  | Check if                      | Solution                                           |
  |-----------------------------------|-----------------------------------------------|
  | Remote Help is enabled for the tenant | In the Intune admin center, go to **Tenant administration** > **Remote Help** and ensure that Remote Help is enabled. It can take up to 30 minutes (or a few hours in some cases) after assigning licenses for the service to activate. |
  | The helper and sharer are using supported platforms and versions | See [Plan Remote Help](remote-help-plan.md#supported-platforms) for details. |
  | The helper has the required permissions | The helper must be assigned to an Intune role with Remote Help permissions and have the "Offer remote assistance" permission. See [Assign Remote Help permissions to helpers](remote-help-plan.md#role-based-access-control-rbac) for details. |
  | The helper and sharer are signing in with organizational accounts from the same tenant | Both the helper and sharer must sign in with a Microsoft Entra account from your organization. You can't use Remote Help to assist users who aren't members of your organization. |
  | The helper and sharer have network access to the required endpoints | See [Network endpoints for Remote Help](remote-help-plan.md#network-considerations) for details. |

### [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

Use the table in this section to troubleshoot common issues with Remote Help on Windows devices.

  | Check if                      | Solution                                           |
  |-----------------------------------|-----------------------------------------------|
  | The device meets the requirements for Remote Help | See [Plan Remote Help](remote-help-plan.md#supported-platforms) for details. |
  | The device has network access to the required endpoints | See [Network endpoints for Remote Help](remote-help-plan.md#network-considerations) for details. |
  | The Intune Win32 app detection rule (if used) is correct | Incorrect version detection can cause Intune to think the app is already installed or never installed. See [Deploy Remote Help](remote-help-deploy.md) for details. |
  | The device is in *do not disturb* mode | If the device is in *do not disturb* mode, notifications for Remote Help session requests won't be shown. Disable *don't disturb* mode and try again or ask the sharer to check their notifications pane. |

#### Troubleshooting Remote Help on Windows for Microsoft Edge WebView2

You might see an error code in a dialog box if you're having trouble installing and running Remote Help. The error might be related to Microsoft Edge WebView 2, which is required to use Remote Help. Here are some error codes you might see along with a short description of the problem.

|Error Code |General Problem |
|-----------| ----------------|
|1001|Remote Help failed to initialize one of its internal components.|
|1002|Remote Help failed to load WebView2.|
|1003|Remote Help failed to install WebView2.|

Use these steps to resolve these issues:

1. Ensure that Microsoft Edge is installed properly and is up to date.
  
  Remote Help uses the Microsoft Edge browser control. If you have problems, the common troubleshooting tips here may help get Remote Help working. Learn more about [Troubleshooting tips for installing and updating Microsoft Edge.](https://support.microsoft.com/microsoft-edge/troubleshooting-tips-for-installing-and-updating-microsoft-edge-a5eceb94-c2b1-dfab-6569-e79d0250317b)
  
  After installing or updating Microsoft Edge, try opening Remote Help again. If Remote Help doesn't run or you get an error message that Microsoft Edge WebView2 isn't installed, go to the next step.

1. Install Microsoft Edge WebView 2
  
  Microsoft Edge WebView2 is required to use Remote Help. If you get an error message that WebView2 isn't installed when you try to open Remote Help, then [download and install Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/consumer/?form=MA13LH) from the Microsoft website. When WebView2 is installed, try opening Remote Help again.

  > [!NOTE]
  > WebView2 should already be installed if your device is running Windows 11 or has Microsoft Edge.

### [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

Use the table in this section to troubleshoot common issues with Remote Help on macOS devices.

  | Check if                      | Solution                                           |
  |-----------------------------------|-----------------------------------------------|
  | Single sign-on is configured and active | If unenrolled devices support isn't enabled, the Entra Enterprise single sign-on extension must be configured and registered for Intune to be able to confirm the device is enrolled. See [Plan Remote Help](remote-help-plan.md#prerequisites) for details. |
  | The required operating system permissions for *Accessibility* and *Screen sharing* are allowed | See [Plan Remote Help](remote-help-deploy.md?tabs=macos#configure-remote-help-apps) for details. |
  | Whether the sharer is using the native Remote Help app or the web app | The web app only allows view access, which might confuse helpers expecting control. |

### [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

Use the table in this section to troubleshoot common issues with Remote Help on Android devices.

  | Check if                      | Solution                                           |
  |-----------------------------------|-----------------------------------------------|
  | The device is enrolled in Dedicated mode. | Remote Help doesn't support other Android enrollment types. |
  | The device has been newly enrolled with Intune. | On newly enrolled devices, push notifications, needed for Remote Help to receive session initiation requests, can take a while to start working. Wait for 15 minutes and try again later.|
  | The Remote Help app isn't installed. | Install the app, see [Deploy Remote Help](remote-help-deploy.md) for details. |
  | All the required permissions are configured and granted for the Remote Help app. | Review and ensure that all required permissions are granted. See [Plan Remote Help](remote-help-plan.md#prerequisites) for details. |
  | The Intune app version isn't updated. | Update the Intune app to the latest version. |
  | The device doesn't have access to Google services. | Remote Help requires access to Google Mobile Services to function, so make sure the device has Google services. You can do this by verifying that the Play Store is present on the device. See [Android: Google Mobile Services](https://www.android.com/gms/). |
  | There's no response from the end user. | Screen Sharing and Full Control Sessions time out automatically after 5 minutes if there's no response from [Android: Google Mobile Services](https://www.android.com/gms/) on the end user device. Make sure the user accepts the prompt to start the session. |
  | The device manufacturer or OS/Zebra MX/Samsung Knox version isn't supported | Make sure the device is supported. See [Plan Remote Help](remote-help-plan.md#supported-platforms) |
  | (On Samsung devices only) The Knox license on the device is expired/invalid or has network issues.  | Make sure that all Knox permissions have been granted, and that the device has an active Knox license; see [License activation errors](https://configure.samsungknox.com/files/knox-configure-getting-started/Content/license-activation-errors.htm) for troubleshooting Knox activation errors. |
  | (On Samsung devices only) Other apps are actively using the Samsung Knox remote desktop APIs (you're using another remote assistance app on the device). | Close or uninstall any other apps using remote viewing/control capabilities on the device. |

---

## Known Issues

### [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

For Windows devices, the following are known issues with Remote Help when using the remote launch feature:
- Notifications for remotely triggering a Remote Help session fail if the *Microsoft Intune Management Service* isn't running.
- After the user's device is restarted, there's a short delay for the *Microsoft Intune Management Service* to start. Either wait for the *Microsoft Intune Management Service* to start or ask the sharer to open the app and share the code.
- For newly enrolled devices, there's a 1 hour delay before the user's device begins receiving notifications when a helper initiates a session.

### [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

- If the sharer exits from a Remote Help session early, the helper might not be notified for 60+ seconds.
- If using Microsoft Edge, the sharer might have to sign in to Microsoft Edge before starting a session or the device reports as Unenrolled.
- Verify that your browser is up to date.
- If you're screen sharing using another application like Teams or recording during the session, it might take longer for the session to connect.

### [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

- On newly enrolled devices, push notifications, needed for Remote Help to receive session initiation requests, can take a while to start working. Wait for 15 minutes and try again later.

---

### Web app known issues

- If the sharer exits from a Remote Help session early, the helper may not be notified for 60+ seconds.
- If using Microsoft Edge, it may require the sharer to sign in to Microsoft Edge before starting a session or the device is reported as Unenrolled.
- SSO must be enabled for the tenant to use the Remote Help web app.

## Next steps

[Get support in Microsoft Intune admin center.](../../get-support.md)
