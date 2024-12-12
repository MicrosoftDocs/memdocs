---
# required metadata

title: Using Remote Help on Windows to assist authenticated users.
titleSuffix: Microsoft Intune 
description: Use the Remote Help app to provide remote assistance to authenticated users who also run the Remote Help app, and to troubleshoot for frontline workers (FLW).
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/01/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#CustomerIntent: As an IT admin, I want to use Remote Help on Windows so that we can troubleshoot and assist users such as Frontline Workers.
ms.reviewer: Karawang
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# Remote Help on Windows with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

Remote Help is a cloud-based solution for secure help desk connections with role-based access controls. With the connection, your support staff can remotely connect to the user's device. During the session, the support staff can view the device's display and if permitted by the device user, take full control. Full control enables a helper to directly make configurations or take actions on the device.

In this article, users who provide help are referred to as *helpers*, and users that receive help are referred to as *sharers* as they share their session with the helper. Both helpers and sharers sign in to your organization to use the app. It's through your Microsoft Entra ID that the proper trusts are established for the Remote Help sessions.

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, you determine which users can provide help and the level of help they can provide.

The Remote Help app is available from Microsoft to install on both devices enrolled with Intune and devices that aren't enrolled with Intune. The app can also be deployed through Intune to your managed devices.

## Remote Help capabilities and requirements on Windows

The Remote Help app supports the following capabilities on Windows:

- **Conditional Access**: Administrators can now utilize Conditional Access capability when setting up policies and conditions for Remote Help. For example, multi-factor authentication, installing security updates, and locking access to Remote Help for a specific region or IP addresses. For more information on setting up Conditional Access, go to [Setup Conditional Access for Remote Help](#setup-conditional-access-for-remote-help)

- **Compliance Warnings**: Before a helper can connect to a user's device, the helper sees a non-compliance warning about that device if it's not compliant with its assigned policies. This warning doesn't block access but provides transparency about the risk of using sensitive data like administrative credentials during the session.

  - Helpers who have access to device views in Intune will see a link in the warning to the device properties page in the Microsoft Intune admin center. The link allows a helper to learn more about why the device isn't compliant.

  - If the user's device isn't enrolled, the helper sees a prompt that the user's device is unenrolled.

- **Elevation of privilege** - When needed, a helper with the correct RBAC permissions can interact with the  UAC prompt on the sharer's machine to enter credentials. For example, your Help Desk employees might enter their administrative credentials to complete an action on the sharer's device that requires administrative permissions.

- **Enhanced chat** - Remote Help includes enhanced chat that maintains a continuous thread of all messages. This chat supports special characters and other languages including Chinese and Arabic. For more information on languages supported, see [Languages Supported](#languages-supported).

- **Remotely start session** - The helper is able to launch Remote Help seamlessly on the helper and user's device from Intune by sending a notification to the user's device. The notification allows helpdesk and the sharer to be connected to a session quickly without exchanging session codes.  

## Prerequisites for Remote Help on Windows

General prerequisites for Remote Help are listed [here](remote-help.md#prerequisites).

The prerequisites for Remote Help on Windows are:

- Set up the Remote Help app for Windows. See [Install and update Remote Help](#install-and-update-remote-help)
- The helper and sharer can be on an enrolled or unenrolled device.

To remotely start a session:
- The helper can be on an enrolled or unenrolled device.
- The sharer's device needs to be enrolled device with Intune management extension.
  - Intune management extension is required for the remote launch feature and that is supported on Windows 10 and 11. Specifically for Windows 10 the OS builds need to be greater than or equal to version 19042 and have KB5018410 patch installed. The OS version should be greater than or equal to 10.0.19042.2075 or 10.0.19043.2075 or 10.0.19044.2075. For more information on the Intune management extension, see [Intune management extension](../apps/intune-management-extension.md)

- Optional Windows updates for higher notification reliability:
   - Win 11: [July 25, 2023—KB5028245 (OS Build 22000.2245) Preview - Microsoft Support](https://support.microsoft.com/topic/july-25-2023-kb5028245-os-build-22000-2245-preview-bbe6f09f-6cec-4777-a548-d237f5d849d2)
   - Win 10: [August 22, 2023—KB5029331 (OS Build 19045.3393) Preview - Microsoft Support](https://support.microsoft.com/topic/august-22-2023-kb5029331-os-build-19045-3393-preview-9f6c1dbd-0ee6-469b-af24-f9d0bf35ca18)

### Network considerations

Remote Help communicates over port 443 (https) and connects to the Remote Assistance Service at `https://remotehelp.microsoft.com` by using the Remote Desktop Protocol (RDP). The traffic is encrypted with TLS 1.2.

Both the helper and sharer must be able to reach these endpoints over port 443. Go to [Network endpoints for Remote Help](intune-endpoints.md#remote-help) for a list of endpoints needed for Remote Help.

## Remote Help modes available for Windows

Remote Help offers three different session modes for Windows:

- **Request screen sharing**: Request view of the remote screen. To minimize effect on end user privacy, this option is recommended unless full control is necessary.

- **Request full control**: Request full control of the remote device.

- **Elevation**: Allows helpers to enter UAC credentials when prompted on the sharer's device. Enabling elevation also allows the helper to view and control the sharer's device when the sharer grants the helper access.

## Install and update Remote Help

Remote Help is available as download from Microsoft and must be installed on each device before that device can be used to participate in a Remote Help session. By default, Remote Help opts users into automatic updates and updates itself when an update is available.

Some users may choose to opt out of automatic updates. However, when a new version of Remote Help is necessary, the app prompts users to install that version upon opening. You can use the same process to download and install Remote Help to install an updated version. There's no need to uninstall the previous version before installing the updated version.

- Intune admins can download and deploy the app to enrolled devices. For more information about app deployments, see [Install apps on Windows devices](../apps/apps-windows-10-app-deploy.md#install-apps-on-windows-devices).
- Individual users who have permissions to install apps on their devices can also download and install Remote Help.

> [!NOTE]
>
> - On May 2022, existing users of Remote Help will see a recommended upgrade screen when they open the Remote Help app. Users will be able to continue using Remote Help without upgrading.
> - On May 23, 2022, existing users of Remote Help will see a mandatory upgrade screen when they open the Remote Help app. They will not be able to proceed until they upgrade to the latest version of Remote Help.
> - Remote Help will now require Microsoft Edge WebView2 Runtime. During the Remote Help installation process, if Microsoft Edge WebView2 Runtime is not installed on the device, then Remote Help installation will install it. When uninstalling Remote Help, Microsoft Edge WebView2 Runtime will not be uninstalled.

### Download Remote Help

Download the latest version of Remote Help direct from Microsoft at [aka.ms/downloadremotehelp](https://aka.ms/downloadremotehelp).

The most recent version of Remote Help is **5.1.1419.0**

### Deploy Remote Help as a Win32 app

To deploy Remote Help with Intune, you can add the app as a Windows Win32 app, and define a detection rule to identify devices that don't have the most current version of Remote Help installed. Before you can add Remote Help as a Win32 app, you must repackage *remotehelpinstaller.exe* as a *.intunewin* file, which is a Win32 app file you can deploy with Intune. For information on how to repackage a file as a Win32 app, see [Prepare the Win32 app content for upload](../apps/apps-win32-prepare.md).

After you repackage Remote Help as a *.intunewin* file, use the procedures in [Add a Win32 app](../apps/apps-win32-add.md) with the following details to upload and deploy Remote Help. In the following, the repackaged remotehelpinstaller.exe file is named *remotehelp.intunewin*.

   > [!IMPORTANT]
   > Make sure the file you dowloaded is renamed to **remotehelpinstaller.exe**. 

1. On the App information page, select **Select app package file**, and locate the *remotehelp.intunewin* file you've previously prepared, and then select **OK**.

   Add a *Publisher* and then select **Next**. The other details on the App Information page are optional.

2. On the Program page, configure the following options:

   - For *Install command line*, specify **remotehelpinstaller.exe /quiet acceptTerms=1**
   - For *Uninstall command line*, specify **remotehelpinstaller.exe /uninstall /quiet acceptTerms=1**

    To opt out of automatic updates, specify enableAutoUpdates=0 as part of the install command **remotehelpinstaller.exe /quiet acceptTerms=1 enableAutoUpdates=0**

   > [!IMPORTANT]
   > The command line options *acceptTerms* and *enableAutoUpdates* are always case sensitive.

   You can leave the rest of the options at their default values and select **Next** to continue.

3. On the Requirements page, configure the following options to meet your environment, and then select **Next**:

   - *Operating system architecture*
   - *Minimum operating system*

4. On the Detection rules page, for *Rules format*, select **Manually configure detection rules**, and then select **Add** to open the *Detection rule* pane. Configure the following options:

   - For *Rule type*, select **File**
   - For *Path*, specify **C:\Program Files\Remote Help**
   - For *File or folder*, specify **RemoteHelp.exe**
   - For *Detection method*, select **String (version)**
   - For *Operator*, select **Greater than or equal to**
   - For *Value*, specify the Remote Help version that you're deploying. For example, **10.0.22467.1000**. See the following note for details on how to get the Remote Help version.
   - Leave *Associated with a 32-bit app on 64-bit clients* set to **No**
     
> [!NOTE]
> To get the version of the **RemoteHelp.exe**, install RemoteHelp manually to a machine and run the following Powershell command **(Get-Item "$env:ProgramFiles\Remote Help\RemoteHelp.exe").VersionInfo**. From the output make a note of the FileVersion and use it to specify the *Value* in the detection rule.

5. Proceed to the Assignments page, and then select an applicable device group or device groups that should install the Remote Help app. Remote Help is applicable when targeting group(s) of devices and not for User groups.

6. Complete creation of the Windows app to have Intune deploy and install Remote Help on applicable devices.

## How to use Remote Help

The use of Remote Help depends on whether you're requesting help or providing help. In this section, both scenarios are covered.

### Request help

To request help, you must reach out to your support staff to request assistance. You can reach out through a call, chat, email, and so on, and you'll be the sharer during the session.

As a sharer, when you've requested help and both you and the helper are ready to start:

1. The helper locates the device in the Microsoft Intune admin center and selects **New remote assistance session**. A notification is sent to the sharer's device.

2. The sharer must select **Launch Remote Help** to join the session. The sharer may need to sign in to authenticate. As an alternative, both the helper and sharer can manually launch the app and exchange a session code.

3. After opening the Remote Help app, the sharer has to wait for the helper to set up the session. The helper sees information about the sharer including the full name, job title, company, profile picture, and verified domain. As the sharer, your app displays similar information about the helper.

   At this time, the helper might request a session with full control of your device or choose only screen sharing. If they request full control, you can select the option to *Allow full control* or choose to *Decline the request*.

4. After the helper establishes the type of session (full control or screen sharing), the session is established, and the helper can then help in resolving any issues on the device.

   During assistance, helpers that have the *Elevation* permission can enter local admin permissions on your shared device. *Elevation* allows the helper to run executable programs or take similar actions when you lack sufficient permissions.

5. After the issues are resolved, or at any time during the session, both the sharer and helper can end the session. To end the session, select **Leave** in the upper right corner of the Remote Help app. 
#### Request help on an unenrolled device

The device might not need to be enrolled to Intune if your administrator allows you to get help on unenrolled devices. If your device is unenrolled and you're trying to receive help, be prepared to enter a security code that you'll get from the individual who is assisting you. You'll enter the code in your Remote Help instance to establish a connection to the helper's instance of Remote Help.

As a sharer, when you've requested help and both you and the helper are ready to start:

1. Start the Remote Help app on the device and sign in to authenticate to your organization.  

2. After signing into the app, get the security code from the individual assisting you and enter the code. Then select **Submit**.

3. After submitting the security code from the helper, the helper sees information about you including your full name, job title, company, profile picture, and verified domain. As the sharer, your app displays similar information about the helper.

4. At this time, the helper might request a session with full control of your device or choose only screen sharing. If they request full control, you can select the option to **Allow full control** or choose to **Decline the request**. Full control must be established before the help session starts.

5. After establishing the type of session (full control or screen sharing), the session is established, and the helper can now help resolving any issues on the device.  

### Provide help

As a helper, after receiving a request from a user who wants assistance by using the Remote Help app:

1. Launch a session on the remote device from within the Microsoft Intune admin center:

   1. Sign into [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > **All devices** and select the device on which assistance is needed.

   2. From the remote actions bar across the top of the device view, select **New remote assistance session** and select **Remote Help**, and then **Continue**.

> [!NOTE]
> If you are launching the session from the Intune, login with the same credentials to the Remote Help app for a successful
> connection.

2. A notification is sent to the sharer's device, and you'll see an update that the notification was successfully sent. Select **Launch Remote Help** to join the session.  

   a. If the notification is sent but not received by the user, you can resend the notification by selecting **Retry**.

   b. If the sharer's device isn't online or not connected to the internet, an error message is  displayed.

   c. If the device that you're trying to connect to is noncompliant, a warning banner is displayed.

2. When Remote Help opens, you must sign in to authenticate to your organization.

3. After the sharer opens the Remote Help app through the notification, as the helper you'll see information about the sharer, including their full name, job title, company, profile picture, and verified domain. The sharer sees similar information about you.

   At this time, you can request a session with full control of the sharer's device or choose only screen sharing. If you request full control, the sharer can choose to *Allow full control* or to *Decline the request*.

4. After establishing that the session uses a shared display or full control, Remote Help will display a **Compliance Warning* if the sharer's device fails to meet the conditions of its assigned compliance policies.

   During assistance, helpers that have the *Elevation* permission can enter local admin permissions on your shared device. *Elevation* allows the helper to run executable programs or take similar actions when you lack sufficient permissions.

5. After the issues are resolved, or at any time during the session, both the sharer and helper can end the session. To end the session, select **Leave** in the upper right corner of the Remote Help app. If a helper performs elevated actions on a user's device and the sharer ends the session, at the end of the session the sharer is automatically signed out.

#### Provide help on an unenrolled device

If the device that you're trying to help isn't enrolled in Intune, you must follow the process described in this section to give help:

1. Locate the Remote Help app on your device and manually start it. After the Remote Help app opens, you'll need to sign in to authenticate your organization.

2. After signing into the app, under **Give help** select **Get a security code**. Remote Help generates a security code that you'll share with the person who has requested assistance. The sharer enters the code in their instance of the Remote Help app to establish a connection to your Remote Help instance.

After the sharer enters the security code, as the helper you'll see information about the sharer, including their full name, job title, company, profile picture, and verified domain. The sharer sees similar information about you. At this time, you can request a session with full control of the sharer's device or choose only screen sharing. If you request full control, the sharer can choose to **Allow full control** or to **Decline the request**.  

Now you'll be in a session with the user with the same experience and procedure outlined in the section [Provide help](#provide-help).

> [!IMPORTANT]
> During a Remote Help session, when a helper has the Elevation permission, the helper will not automatically be able to view the sharer's UAC prompt. Instead, for a non-admin sharer, a button will appear on the helper's Remote Help toolbar that will allow them to request access to the UAC prompt on the sharer's device. Once requested and accepted, the helper will be able to perform elevated actions on the sharer's device. When the sharer ends the Remote Help session, they will be shown a dialog box that will warn them that if they continue, they will be logged off. If the helper ends the session, the sharer will not be logged off.

## Log files

Remote Help logs data during installation and during Remote Help sessions, which can be of use when investigating issues with the app.

**Installation of Remote Help** - When Remote Help installs or uninstalls, the following two logs are created in the device users' Temp folder, for example, `C:\Users\<username>\AppData\Local\Temp`. The \* in the log file name represents a date and time stamp of when the log was created.

- Remote_help_*_QuickAssist_Win10_x64.msi.log
- Remote_help_*.log

**Operational logs** - During use of Remote Help, operational details are logged in the Windows Event Viewer:

- Event Viewer > Application and Services > Microsoft > Windows > RemoteHelp

## Installation details

Automatic firewall rule creation from the Remote Help installer has been removed. However, if needed, System administrators can create firewall rules.

Depending on the environment that Remote Help is utilized in, it may be necessary to create firewall rules to allow Remote Help through the Windows Firewall. In some situations when it's necessary, the following Remote Help executables should be allowed through the firewall:

- C:\Program Files\Remote help\RemoteHelp.exe
- C:\Program Files\Remote help\RHService.exe
- C:\Program Files\Remote help\RemoteHelpRDP.exe

## Setup Conditional Access for Remote Help

This section outlines the steps for provisioning the Remote Help service on the tenant for Conditional Access.

1. Open PowerShell in admin mode.
    - It may be necessary to install [Microsoft Graph PowerShell](/powershell/microsoftgraph/installation)  
2. Within PowerShell enter the following commands:

### Installation

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```

### Sign in

Use the `Connect-MgGraph` command to sign in with the required scopes. You'll need to sign in with an admin account to consent to the required scopes.
```powershell

Connect-MgGraph -Scopes "Application.ReadWrite.All"
```

### Create the service principal

Create a Service Principal using the `Remote Assistance Service` AppId "1dee7b72-b80d-4e56-933d-8b6b04f9a3e2".

```powershell
New-MgServicePrincipal -AppId "1dee7b72-b80d-4e56-933d-8b6b04f9a3e2"
```

```Output
DisplayName                                     Id AppId                                   ServicePrincipalType
----                                         ------- -----------                                   ---------------
RemoteAssistanceService                      3d5ff82b-a5f2-483a-xxxx-9514ed66f7c5        1dee7b72-b80d-4e56-933d-8b6b04f9a3e2
```

This output has been shortened for readability.

The ID corresponds to the app ID for the Remote Assistance Service.

The display name is **Remote Assistance Service**, which is the backend service for Remote Help.  

### Sign out

Use the `Disconnect-MgGraph` command to sign out.

```powershell
Disconnect-MgGraph
```


## Languages Supported

Remote Help is supported in the following languages:

- Arabic
- Bulgarian
- Chinese (Simplified)
- Chinese (Traditional)
- Croatian
- Czech
- Danish
- Dutch
- English
- Estonian
- Finnish
- French
- German
- Greek
- Hebrew
- Hungarian
- Italian
- Japanese
- Korean
- Latvian
- Lithuanian
- Norwegian
- Polish
- Portuguese
- Romanian
- Russian
- Serbian
- Slovak
- Slovenian
- Spanish
- Swedish
- Thai
- Turkish
- Ukrainian

## Troubleshooting Remote Help on Windows for Edge WebView2

You might see an error code in a dialog box if you're having trouble installing and running Remote Help. The error might be related to Microsoft Edge WebView 2, which is required to use Remote Help. Here are some error codes you might see along with a short description of the problem.

|Error Code |General Problem |
|-----------| ----------------|
|1001|Remote Help failed to initialize one of its internal components.|
|1002|Remote Help failed to load WebView2.|
|1003|Remote Help failed to install WebView2.|

### Solutions

1. Ensure that Microsoft Edge is installed properly and is up to date.
   
Remote Help uses the Microsoft Edge browser control. If your device has Microsoft Edge installed, then it's likely that Remote Help will run properly. If you have problems, the common troubleshooting tips here may help get Remote Help working. Learn more about [Troubleshooting tips for installing and updating Microsoft Edge.](https://support.microsoft.com/microsoft-edge/troubleshooting-tips-for-installing-and-updating-microsoft-edge-a5eceb94-c2b1-dfab-6569-e79d0250317b)
After installing or updating Microsoft Edge, try opening Remote Help again. If Remote Help doesn't run or you get an error message that Microsoft Edge WebView2 isn't installed, go to the next step.

2. Install Microsoft Edge WebView 2
   
Microsoft Edge WebView2 is required to use Remote Help. If you get an error message that WebView2 isn't installed when you try to open Remote Help, then [download and install Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/consumer/?form=MA13LH) from the Microsoft website. After you've downloaded WebView2, try opening Remote Help again.

> [!NOTE]
> WebView2 should already be installed if your device is running Windows 11 or has Microsoft Edge.

## Known Issues
For remotely starting a session on the user's device, notifications that are sent to the sharer's device when a helper launches a Remote Help session fails if the Microsoft Intune Management Service isn't running.
After the user's device is restarted, there's a delay for the service to start. You can either manually wait for the service to start (30 minutes after restart), or manually start the service through services.msc.
For newly enrolled devices, there's a 1 hour delay before the user's device begins receiving notifications when a helper initiates a session.

## What's New for Remote Help

Updates for Remote Help are released periodically. When we update Remote Help, you can read about the changes here.

### June 25, 2024

Version 5.1.1419.0

- Resolve issue where the screen may be blank on first launch. 

### March 13, 2024

Version: 5.1.1214.0

- Changed the primary endpoint for Remote Help from https://remoteassistance.support.services.microsoft.com to https://remotehelp.microsoft.com.
  > [!NOTE]
  > This could cause a breaking change for some organizations that have not yet allowed remotehelp.microsoft.com through their firewall after 5/30/2024.
- Resolved various bugs including an issue with Conditional Access. If a tenant had a **Terms of Use** policy enabled for Office 365, Remote Help wouldn't know how to respond and would instead present an authentication error message to the user.
- Enabled a shortcut to open context menus with the keyboard shortcut 'Alt + Space'

### October 25, 2023

Version: 5.0.1311.0

- Disabled the relaying of system audio from the Sharer device to the Helper device, which caused an echo when both users were using another app to communicate (such as Teams).
- Added the capability for Helpers that have elevation permissions to also be able to elevate apps on devices where the Sharer is an Administrator.

### September 7, 2023

Version: 5.0.1045.0

With Remote Launch, the helper can launch Remote Help seamlessly on the helper and sharer's device from Intune by sending a notification to the sharer's device.

### July 13, 2023

Version: 5.0.1045.0
This version of Remote Help provides support for ARM64 devices including the Microsoft Surface Pro X and Parallels Desktop on macOS.

### June 20, 2023

Version: 4.2.1424.0
With Remote Help 4.2.1424.0, a new in-session connection mode feature provides users with a way to seamlessly switch between full control and view-only modes during a remote assistance session.

### May 1, 2023

Version: 4.2.1270.0

This version includes a minor update that enables future functionality.

- Added support for slashes within the Remote Help URI (to enable future functionality)

### March 27, 2023

Version: 4.2.1167.0 - Changes in this release:

This release addresses a bug in the Laser Pointer and includes some updates to prepare for future releases.

- Updated product name from **Remote help** to **Remote Help**
- Updated application description to better localize it for non-US locales
- Resolved a bug where the app would flash a white screen when launched in dark mode
- Fixed a bug with the Laser pointer color change

### February 6, 2023

Version: 4.1.1.0 - Changes in this release:

A new Laser Pointer feature has been added to better assist a helper guide a sharer during a session. A helper can use the Laser Pointer in both Full Control and View Only sessions. Other updates include improvements to localization, and error handling.

Various bug fixes included in this release:

- Fixed an issue where in some cases a helper is unable to interact with elevated applications

- Resolved an accessibility issue where a helper was unable to use some keyboard navigation hotkeys

- Reliability fixes and improved logging for WebView2 integration

### September 6, 2022

Version: 4.0.1.13 - Changes in this release:

Fixes were introduced to address an issue that prevented people from having multiple sessions open at the same time. The fixes also addressed an issue where the app was launching without focus, and prevented keyboard navigation and screen readers from working on launch.

For more information, go to [Use Remote Help with Intune](remote-help.md).

### July 26, 2022

Version: 4.0.1.12 - Changes in this release:

Various fixes were introduced to address the 'Try again later' message that appears when not authenticated. The fixes also include an improved auto-update capability.

### May 11, 2022

Version 4.0.1.7 - Webview 2 release

### April 5, 2022

Version 4.0.0.0 - GA release

## Next steps

[Get support in Microsoft Intune admin center.](../../get-support.md)
