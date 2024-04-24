---
# required metadata

title: Using Remote Help on macOS to assist authenticated users.
titleSuffix: Microsoft Intune 
description: Use Remote Help to provide remote assistance to authenticated users and to troubleshoot for frontline workers (FLW).
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/19/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#CustomerIntent: As an IT admin, I want to use Remote Help on macOS so that we can troubleshoot and assist users such as Frontline Workers.
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
 
# Remote Help on macOS with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

Remote Help is a cloud-based solution for secure help desk connections with role-based access controls. With this connection, your support staff can remotely connect to a user's device and view their display.

In this article, users who provide help are referred to as *helpers*, and users that receive help are referred to as *sharers* as they share their session with the helper.
Remote Help is available for macOS as both a native application that can be downloaded and installed on the user’s device, and as a Web App that runs within the user’s web browser.

## Remote Help Native macOS App

Most organizations install the Remote Help application for macOS on their users’ devices. This makes the application readily available to users when they need to initiate a support session. Remote Help for macOS provides the helper with view only and full control capabilities where they can control the Sharer’s mouse and keyboard.

## Remote Help Web App

In situations where the Sharer needs assistance but is unable to install the native application for macOS, the Sharer can use the Web App to share their screen to a helper. This web app provides view only capabilities to the helper, which allows them to guide the user through resolving whichever issue they have encountered.
Helpers always use the Remote Help Web App to provide support to a Sharer that is on macOS. This provides them with a consistent and friendly experience accessible through the Intune portal. For more details, go to [Remote Help Web app](remote-help-webapp.md).

## Authentication and Permissions

Both helpers and sharers sign in to your organization using Microsoft Entra ID, which ensures that proper trusts are established for the Remote Help sessions.

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, you determine which users can provide help and the level of help they can provide.

For details about configuring and setting up of permissions, go to [Using Remote Help](remote-help.md#task-2-configure-permissions-for-remote-help).

## Remote Help capabilities and requirements on macOS

The Remote Help web app supports the following capabilities on macOS:

- **Use Remote Help with unenrolled devices**: Disabled by default, you can choose to allow help to devices that aren't enrolled with Intune.

- **Conditional access**: Administrators can now utilize conditional access capability when setting up policies and conditions for Remote Help. For more information on setting up conditional access, go to [Setup Conditional Access for Remote Help](#setup-conditional-access-for-remote-help)

- **Compliance Warnings**: Before connecting to a user's device, a helper will see a non-compliance warning about that device if it's not compliant with its assigned policies. This warning doesn't block access but provides transparency about the risk of using sensitive data like administrative credentials during the session.

- **Enrollment status**: If the user's device that the helper is trying to connect to isn't enrolled, the helper sees a prompt notifying them of the device status.

- **Chat functionality**: Remote Help includes enhanced chat that maintains a continuous thread of all messages. This chat supports special characters and other languages including Chinese and Arabic. For more information on languages supported, see [Languages supported](#languages-supported).  

## Prerequisites for Remote Help on macOS

General prerequisites for Remote Help are listed here [Prerequisites for Remote Help](remote-help.md#prerequisites).

The prerequisites for Remote Help on macOS are listed under [Supported devices](#supported-devices).

If your organization, by default, restricts remote assistance to enrolled devices only, single sign-on (SSO) is a prerequisite for accessing Remote Help. You can learn more about this prerequisite [here.](../configuration/use-enterprise-sso-plug-in-macos-with-intune.md?tabs=prereq-intune%2Ccreate-profile-intune)

## Supported devices

### macOS versions

- 12 Monterey

- 13 Ventura

- 14 Sonoma 

### Browser versions

- Safari (version 16.4.1+)

- Chrome (version 109+)

- Edge (version 109+)

- Firefox (version 122+)

> [!NOTE]
> Virtual Machines (VMs) are currently not supported.

## Network considerations

Both the helper and sharer must be able to reach specific endpoints over port 443. Go to [Network endpoints for Remote Help](intune-endpoints.md#remote-help) for a list of endpoints needed for Remote Help.

## Remote Help modes available on macOS

Remote Help offers different session modes for macOS.

- **Screen sharing**: View the remote screen.
- **Full control**: View the display and control the devices mouse and keyboard.

## Install and update Remote Help

Remote Help is available to download from Microsoft and must be installed on the device you're trying to help before that device can be used to participate in a Remote Help session. Remote Help receives the latest versions through the [Microsoft AutoUpdate (MAU) application](https://learn.microsoft.com/en-us/DeployOffice/mac/update-office-for-mac-using-msupdate#application-identifiers). Users can opt in for automatic updates to ensure Remote Help is up to date.

## Download Remote Help

Download the latest version of Remote Help directly from Microsoft at https://aka.ms/downloadremotehelpmacos 
The most recent version of Remote Help is 1.0.2404171.

## Add Remote Help as a LOB application

You can add Remote Help as a line-of-business (LOB) app to Microsoft Intune.

To include LOB apps in your managed environment, you upload the app installation file to Intune and assign the app to devices or groups from Intune. For more information on adding a macOS LOB app to Microsoft Intune, go to [How to add macOS line-of-business apps to Microsoft Intune](../apps/lob-apps-macos.md).

## Using Remote Help

The web app allows support teams to view the sharer's device during a connected session. The use of Remote Help depends on whether you're requesting help or providing help. In this section, we cover both scenarios.

### Request help

To request help, you must reach out to your support staff to request assistance. You can reach out through a call, chat, email, and so on, and you'll be the sharer during the session.

When you as the sharer and your helper are ready to begin the session:

1. Open Remote Help app on the device **Finder** > **Applications** > **Microsoft Remote Help**.

2. If prompted, sign in with your organization credentials to authenticate. to your organization.

3. Your helper will provide you with an 8-digit security code. After entering the code, select **Share screen** to continue.

4. When the session connection begins, a trust screen is displayed with the Helpers information including their full name, job title, company, profile picture and verified domain. At this time, the helper requests a session with Full control of your device or View Only screen sharing. You can either choose to *Allow* or to *Decline* the request.

5. You might see a prompt to allow `remotehelp.microsoft.com` to use your microphone. Select **Don't Allow** as this permission isn't needed for screen sharing.

6. Select **Share screen** to continue.

7. You might see a prompt to allow `remotehelp.microsoft.com` share your screen. Select **Allow** to continue.

8. macOS displays a dialogue menu in the top right corner as one of two options:

  - Green camera icon: Choose **Screen**, and then move your mouse to select the screen share.
  - Yellow microphone icon: Select the microphone icon, then to the right of the application name Microsoft Remote Help, select the grey icon, and then Screen. Move your cursor to the screen you want to share and select **Share this screen**.

9. After the session is established, the helper can then help in resolving any issues on the device.

#### Request help on an unenrolled device

Your device might not need to be enrolled to Intune if your administrator allows you to get help on unenrolled devices. If your device is unenrolled and you're trying to receive help, follow the rest of the steps outlined in [Request help](#request-help) to be in a connected session.

### Provide help

As a helper, after receiving a request from a user who wants assistance by using Remote Help. While the sharer is using a macOS device, you can provide support on either a macOS device or Windows device.

1. Navigate to the device you're trying to help from the Microsoft Intune admin center:

   1. Sign into [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > **All devices** and select the macOS device on which assistance is needed.

   2. From the remote action bar across the top of the device view, select **New remote assistance session** and select **Remote Help**, and then **Continue**.

2. Copy and share the 8-digit session code with the sharer that you're trying to help, before selecting **Start** to launch a new Remote Help session. this allows you to navigate to the session link with the embedded passcode.  

3. When Remote Help opens in a new tab, you must sign in to authenticate to your organization.

4. After the sharer navigates to the Remote Help session, as the helper you'll see information about the sharer, including their full name, job title, company, profile picture, and verified domain. The sharer sees similar information about you.

5. At this time, you can request a session with full control of the sharer's device or choose only screen sharing. The sharer can choose to *Allow* or to *Decline* the request. Remote Help displays a *Compliance Warning* if the sharer's device fails to meet the conditions of its assigned compliance policies.

#### Provide help on an unenrolled device

If the device that you're trying to help isn't enrolled in Intune, you must follow the process described in this section to give help:

1. Navigate to https://aka.ms/rhh on your browser and sign in to authenticate to your organization.

2. The helper must sign in, copy and then share the 8-digit security code with the person you're trying to help.

Remote Help displays a warning if the sharer's device isn't enrolled in Microsoft Intune. This warning doesn't block access but provides transparency about the risk of using sensitive data like administrative credentials during the session.

Follow the rest of the steps outlined in [Provide help](#provide-help) to be in a connected session.

## Setup Conditional Access for Remote Help

Remote Help for macOS supports conditional access. For more details, go to [Setup Conditional Access for Remote Help](remote-help-windows.md#setup-conditional-access-for-remote-help).

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

## Known Issues

- If the sharer exits from a Remote Help session early, the helper might not be notified for 60+ seconds.  

- If using Edge, the sharer might have to sign in to Edge before starting a session or the device reports as Unenrolled.

- Verify that your browser is up to date.

- If you're screen sharing using another application like Teams or recording during the session, it might take longer for the session to connect.
