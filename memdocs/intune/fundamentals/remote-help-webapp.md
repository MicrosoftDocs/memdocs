---
# required metadata
title: Using Remote Help Web App.
titleSuffix: Microsoft Intune 
description: Use the Remote Help web app to provide remote assistance to authenticated users and to troubleshoot for frontline workers (FLW).
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
#CustomerIntent: As an IT admin, I want to use Remote Help Web App so that we can troubleshoot and assist users such as Frontline Workers.
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
 
# Remote Help Web App

Remote Help is a cloud-based solution for secure help desk connections with role-based access controls (RBAC). With this connection, your support staff can remotely connect to the user's device and view their display.  

In this article, users who provide help are referred to as Helpers, and users that receive help are referred to as Sharers as they share their session with the helper.

In situations where the sharer needs assistance but is unable to install the Remote Help native application on a device, the sharer can share their screen to a helper by using the Remote Help Web App. This web app provides View Only capabilities to the helper, which allows them to guide the user through support scenarios.

## Remote Help Web App Capabilities

The Remote Help web app supports the following capabilities:

Use Remote Help with unenrolled devices: Disabled by default, you can choose to allow help to devices that aren't enrolled with Intune.  

- **Conditional access**: Administrators can now utilize conditional access capability when setting up policies and conditions for Remote Help. For more information on setting up conditional access, go to [Setup Conditional Access for Remote Help](remote-help-windows.md#setup-conditional-access-for-remote-help).

- **Compliance Warnings**: Before connecting to a user's device, a helper will see a non-compliance warning about that device if it's not compliant with its assigned policies. This warning doesn’t block access but provides transparency about the risk of using sensitive data like administrative credentials during the session.  

If the user’s device that they're trying to connect to isn't enrolled, the helper sees a prompt that the user’s device is unenrolled.

- **Chat functionality**: Remote Help includes enhanced chat that maintains a continuous thread of all messages. This chat supports special characters and other languages including Chinese and Arabic. For more information on languages supported, see [Languages Supported](remote-help-windows.md#languages-supported).

## Authentication and Permissions

Both Helpers and Sharers sign in to your organization using Microsoft Entra ID, which ensures that proper trusts are established for the Remote Help sessions.  

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, tenant administrators determine which users can provide help and the level of help they can provide.

## Prerequisites and supported devices for Remote Help Web App

In addition to the [general prerequisites for Remote Help](remote-help.md#prerequisites), there are other prerequisites for the Remote Help web app.

- [SSO(Single-Sign-On)](../configuration/use-enterprise-sso-plug-in-ios-ipados-with-intune.md#prerequisites)

- For sessions with unenrolled devices

  - Allow Remote Help to unenrolled devices (**Tenant Administration** > **Remote Help** > **Settings**)

## Supported Devices

Device support is dependent on both the users operating system, and their web browser.  

### macOS Versions

- 11 Big Sur (Web app only)

- 12 Monterey

- 13 Ventura

- 14 Sonoma

### Windows Versions

- Windows 10

- Windows 11

### Linux Versions

Linux isn't officially supported by Remote Help. However, the Remote Help Web App might function for most Linux devices that are using a supported browser.

## Browser Versions

- Safari (version 16.4.1+)

- Chrome (version 109+)

- Edge (version 109+)

- Firefox (version 122+)

## Network Considerations  

Both the helper and sharer must be able to reach Remote Help endpoints over port 443. Go to Network endpoints for Remote Help for a complete list of Remote Help endpoints.
 
## Using Remote Help web app

The web app allows support teams to view the sharer’s device during a connected session. The use of Remote Help depends on whether you’re requesting help or providing help. In this section, we cover both scenarios.

## Establishing a session

During a session there are two roles, a helper, and a sharer. The helper obtains the security code, and then provides it to the sharer. After the session is established, the helper can view the Sharer’s screen.

### Enrolled macOS device

1. The helper navigates to the device to connect to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

- Sign into Microsoft Intune admin center and go to **Devices** > **All devices** and select the macOS device on which assistance is needed.

- From the remote action bar across the top of the device view, select **New remote assistance session** and select **Remote Help**, and then **Continue**.

2. To invite a user to a session, provide the user with the security code.

- If the sharer is also using the web app:  

 - Copy and share the session link with the user (the link is limited to View Only) (For example: https://aka.ms/rh?passcode=4060r0gx). The link opens in the user's web browser. You can only request a screen sharing session of the device.

- If the sharer is using the macOS application:

 - Share the 8-character security code with the user. You can request a screen sharing session (view only, and full control are supported)

3. After the sharer either selects the link or enters the code into Remote Help for macOS, they're joined to the session.  

- If the user isn't already logged in to the application, they're prompted to do so.

4. At the start of the session, the trust screen is displayed which shows the other person’s full name, job title, company, profile picture, and verified domain.

- Helpers can see information about the sharer.

- Sharer can see information about the helper.

5. The sharer can choose to *Allow* or to *Decline* the request, after viewing the trust screen.

6. If the Sharers device isn't compliant with your organizations policies, Remote Help displays a *Compliance Warning* that encourages the helper to be cautious.

### Unenrolled device

If the device that you're trying to help isn't enrolled in Intune, follow the process described in this section to provide help:  

1. The helper navigates to https://aka.ms/rhh in their web browser, then signs in to authenticate with their organization.

2. After authenticating, a security code is displayed.

3. Copy and share the 8-digit security code with the person to be helped.

4. The sharer then navigates to https://aka.ms/rh and logs in with their organization’s credentials.

5. After the sharer enters the code, and both users accept the prompts, the sessions begin.

Remote Help displays a warning if the sharer’s device isn't enrolled in Microsoft Intune. This warning doesn’t block access but provides transparency about the risk of using sensitive data like administrative credentials during the session.

More details are outlined in [Provide help](#establishing-a-session).

## Known Issues

- If the sharer exits from a Remote Help session early, the helper may not be notified for 60+ seconds.  

- If using Edge, it may require the sharer to sign in to Edge before starting a session or the device is reported as Unenrolled.

- SSO must be enabled for the tenant to use the Remote Help web app.
