---
# required metadata

title: Using Remote Help on macOS to assist authenticated users.
titleSuffix: Microsoft Intune 
description: Use the Remote Help web app to provide remote assistance to authenticated users and to troubleshoot for frontline workers (FLW).
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 09/12/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
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

Remote Help is a cloud-based solution for secure help desk connections with role-based access controls. With the connection, your support staff can remote connect to the user's device. During the session, the support staff can view the device's display and if permitted by the device user, take full control. Full control enables a helper to directly make configurations or take actions on the device.

In this article, users who provide help are referred to as *helpers*, and users that receive help are referred to as *sharers* as they share their session with the helper. Both helpers and sharers sign in to your organization to use the web app. It's through your Azure Active Directory (Azure AD) that the proper trusts are established for the Remote Help sessions. During the session, the support staff can view the device's display.

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, you determine which users can provide help and the level of help they can provide.

The Remote Help app is available from Microsoft to install on both devices enrolled with Intune and devices that aren't enrolled with Intune. The app can also be deployed through Intune to your managed devices.

## Remote Help capabilities and requirements on macOS

The Remote Help web app supports the following capabilities on macOS:

- **Use Remote Help with unenrolled devices** - Disabled by default, you can choose to allow help to devices that aren't enrolled with Intune.

- **Conditional access**: Administrators can now utilize conditional access capability when setting up policies and conditions for Remote Help. For more information on setting up conditional access, go to [Set up Conditional Access for Remote Help](#set-up-conditional-access-for-remote-help)

- **Compliance Warnings**: Before a helper can connect to a user's device, the helper sees a non-compliance warning about that device if it's not compliant with its assigned policies. This warning doesn't block access but provides transparency about the risk of using sensitive data like administrative credentials during the session.

  - If the user's device isn't enrolled, the helper sees a prompt that the user's device is unenrolled.

- **Chat functionality** - Remote Help includes enhanced chat that maintains a continuous thread of all messages. This chat supports special characters and other languages including Chinese and Arabic. For more information on languages supported, see [Languages Supported](#languages-supported).  

## Prerequisites for Remote Help on macOS

General prerequisites for Remote Help are listed here [Prerequisites for Remote Help](remote-help.md#prerequisites).

The prerequisites for Remote Help on macOS are listed under [Supported devices](#supported-devices).

## Supported devices

### macOS versions

- 11 Big Sur

- 12 Monterey

- 13 Ventura

### Browser versions

- Safari (version 16.4.1+)

- Chrome (version 109+)

- Microsoft Edge (version 109+)

### Network considerations

Remote Help communicates over port 443 (https) and connects to the Remote Assistance Service at `https://remoteassistance.support.services.microsoft.com` by using the Remote Desktop Protocol (RDP). The traffic is encrypted with TLS 1.2.

Both the helper and sharer must be able to reach these endpoints over port 443:

| Domain/Name                       | Description                                           |
|-----------------------------------|-------------------------------------------------------|
|\*.aria.microsoft.com             | Accessible Rich Internet Applications (ARIA) service for providing accessible experiences to users|
|\*.cc.skype.com                   | Required for Azure Communication Service|
|\*.events.data.microsoft.com      | Microsoft Telemetry Service |
|\*.flightproxy.skype.com          | Required for Azure Communication Service|
|\*.registrar.skype.com            | Required for Azure Communication Service|
|\*.support.services.microsoft.com | Primary endpoint used for the Remote Help application|
|\*.trouter.skype.com              | Used for Azure Communication Service for chat and connection between parties|
|\*.aadcdn.msauth.net              | Required for logging in to the application Microsoft Azure Active Directory|
|\*.aadcdn.msftauth.net            | Required for logging in to the application Microsoft Azure Active Directory|
|\*.edge.skype.com                 | Used for Azure Communication Service for chat and connection between parties|
|\*.login.microsoftonline.com      | Required for Microsoft sign in service. Might not be available in preview in all markets or for all localizations|
|\*.remoteassistanceprodacs.communication.azure.com|Used for Azure Communication Service for chat and connection between parties|
|\*.turn.azure.com  | Azure Communication Service |
|\*.remotehelp.microsoft.com  | Primary endpoint for Remote Help Web App |
|\*.trouter.teams.microsoft.com  | Allows for the Remote Help Web App to become directly addressable within the web browser|
|\*.trouter.communication.microsoft.com  | Allows for the Remote Help Web App to become directly addressable within the web browser|
|\*.alcdn.msauth.net|Required to sign-in to the application Microsoft Azure Authentication Library|
|\*.wcpstatic.microsoft.com| Used to confirm cookie compliance in accordance with various laws|
|\*.flightproxy.skype.com | Conversation service URL for Azure Communication Service |
|[Allowlist for Microsoft Edge endpoints](/deployedge/microsoft-edge-security-endpoints) |The app uses Microsoft Edge WebView2 browser control. This article identifies the domain URLs that you need to add to the allowlist to ensure communications through firewalls and other security mechanisms|

## Remote Help modes available for macOS

Remote Help offers screen share session mode on macOS:

**Screen sharing**: View of the remote screen. Remote Help for a web application. The web app allows support teams to view the sharer's device during a connected session. The use of Remote Help depends on whether you're requesting help or providing help.

## Using Remote Help

The use of Remote Help depends on whether you're requesting help or providing help. In this section, we cover both scenarios.

### Request help

To request help, you must reach out to your support staff to request assistance. You can reach out through a call, chat, email, and so on, and you'll be the sharer during the session.

As a sharer, when you've requested help and both you and the helper are ready to start:

1. The helper sends you a Remote Help session link (For example: https://aka.ms/rh?passcode=4060r0gx) and you can navigate in your browser.

2. You may need to sign in to authenticate. After you sign in, you can see information about the helper including the full name, job title, company, profile picture, and verified domain. At this time, the helper can only request a screen sharing session. You can either choose to Allow or to Decline the request.

3. You may see a prompt to allow `remotehelp.microsoft.com` to use your microphone and observe your screen. Select **Allow** to continue.

4. Select the play icon on the upper right-hand corner to finish establishing the session.

5. After the session is established, the helper can then help in resolving any issues on the device.

#### Request help on an unenrolled device

The device might not need to be enrolled to Intune if your administrator allows you to get help on unenrolled devices. If your device is unenrolled and you're trying to receive help, be prepared to enter the security code that get from the individual who is assisting you.

As a sharer, when you've requested help and both you and the helper are ready to start:

1. Navigate to aka.ms/rh on your browser and sign in to authenticate to your organization.  

2. After signing in, get the 8-digit security code from the individual assisting you and enter the code. Then select **Share screen**.

Follow the rest of the steps outlined in [Request help](#request-help) to be in a connected session.

### Provide help

As a helper, after receiving a request from a user who wants assistance by using Remote Help. While the sharer is using a macOS device, you can provide support on either a macOS device or Windows device.

1. Navigate to the device you're trying to help from within the Microsoft Intune admin center:

   1. Sign into [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > **All devices** and select the macOS device on which assistance is needed.

   2. From the remote actions bar across the top of the device view, select **New remote assistance session** and select **Remote Help**, and then **Continue**.

2. Copy and share session link with the sharer that you're trying to help, before selecting Start to launch a new Remote Help session.  

   a. When the sharer navigates to the session link with the passcode embedded, they're 	able to directly get to the specific session.

   b. As an alternative, you can copy and share the 8-digit passcode with the sharer. The sharer can navigate to aka.ms/rh and follow the steps.

2. When Remote Help opens, you must sign in to authenticate to your organization.

3. After the sharer navigates to the Remote Help session, as the helper you'll see information about the sharer, including their full name, job title, company, profile picture, and verified domain. The sharer sees similar information about you.

   At this time, you can only request a screen sharing session of the sharer's device. The sharer can choose *Allow* or *Decline* the request.

4. Remote Help displays a **Compliance Warning* if the sharer's device fails to meet the conditions of its assigned compliance policies.

#### Provide help on an unenrolled device

If the device that you're trying to help isn't enrolled in Intune, you have to follow the process described in this section to give help:

1. Navigate to aka.ms/rhh on your browser and sign in to authenticate to your organization.

2. The helper has to sign in, copy and then share the 8-digit security code with the person they are trying to help.

Remote Help displays a warning if the sharer's device isn't enrolled in Microsoft Intune. This warning doesn't block access but provides transparency about the risk of using sensitive data like administrative credentials during the session.

Follow the steps provided in the section [Provide help](#provide-help) to be in a connected session.

## Set up Conditional Access for Remote Help

This section outlines the steps for provisioning the Remote Help service on the tenant for conditional access.

1. Open PowerShell in admin mode.
    - It may be necessary to install [AzureADPreview](https://www.powershellgallery.com/packages/AzureADPreview/2.0.2.149)  
2. Within PowerShell enter the following commands:

    - Install-Module -Name AzureADPreview
    - Connect-AzureAD
       - Enter in the appropriate credentials for your Azure admin account
    - New-AzureADServicePrincipal -AppId 1dee7b72-b80d-4e56-933d-8b6b04f9a3e2
       - The ID corresponds to the app ID for Remote Assistance Service
       - The display name is **Remote Assistance Service**, which is the backend service for Remote Help  

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

If the sharer exits from a Remote Help session early, the helper may not be notified for 60+ seconds.  

If using Microsoft Edge, it may require the sharer to sign in to the browser before starting a session or the device is reported as "Unenrolled".

## Next steps

[Get support in Microsoft Intune admin center](../../get-support.md)
