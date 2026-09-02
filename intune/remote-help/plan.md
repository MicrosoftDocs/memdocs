---
title: Plan for Remote Help with Microsoft Intune
description: Learn about the requirements and capabilities of Remote Help with Microsoft Intune on Windows, macOS, and Android Enterprise.
ms.date: 08/13/2026
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1023
ms.reviewer: karawang
#customer intent: As an IT administrator, I want to understand Remote Help requirements, permissions, and limitations so that I can plan a secure deployment.
---

# Planning for Remote Help with Microsoft Intune

In this article, users who provide help are referred to as *helpers*, and users that receive help are referred to as *sharers*, as they share their session with the helper. Both helpers and sharers sign in to your organization to use the app. It's through your Microsoft Entra ID that the proper trusts are established for the Remote Help sessions.

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, you determine which users can provide help and the level of help they can provide.

> [!TIP]
> For a customized experience based on your environment, you can access the [Intune Suite add-ons guide](https://go.microsoft.com/fwlink/?linkid=2314706) in the Microsoft 365 admin center.

## Planning checklist  
Follow this checklist to streamline your planning process.  

- Support for platforms and devices  
- Language support  
- Tenant configuration  
- Conditional access  
- Role-based access control (RBAC)  
- Network considerations  
- Prerequisites  
- Limitations  
- Known issues  
- Enrolled or unenrolled devices  

## Planning considerations  

Use these considerations to prepare your organization for Remote Help.    

- Enforce least privilege: Only grant the minimum Remote Help permissions needed for each support role. Use custom Intune roles if necessary to limit who can take full control or perform unattended sessions. For example, level-1 support might get view-only rights, while tier-2 gets full control rights. This principle helps protect user privacy and device integrity.

- Scope unattended control narrowly: Unattended control allows a helper to troubleshoot to a device without an end user present. Create a dedicated custom Intune role that includes the Windows unattended control remote sign-in and Android unattended control permissions, and assign it only to authorized support personnel, such as Tier 3 helpdesk staff or senior administrators. Scope the role to only the device groups that require unattended support.

- Use Conditional Access for helpers: Since helpers have elevated access to user devices, add an extra layer of security. Requiring MFA or compliant device status for helper accounts through Conditional Access is highly recommended. These measures help prevent a compromised helper account from being used to access devices. Microsoft Entra Conditional Access policies for Remote Help are supported only on Windows and macOS.
  
- Enable unenrolled device support only if needed: Allowing Remote Help on unenrolled devices (Microsoft Entra registered only) is convenient for supporting personal devices, but it comes with reduced oversight, such as no device compliance information or limited audit data. Enable this feature thoughtfully, and consider limiting which support staff can help unenrolled devices by using separate roles.
  
- Network and firewall: Verify that corporate network policies don't interfere with Remote Help. The app communicates over port 443 to Azure cloud endpoints. If your users are on a corporate network, ensure proxy or SSL inspection doesn't break the connection. If your proxy servers are using SSL inspection, the domains listed for Remote Help should be excluded to avoid issues. For more information, see [Network endpoints for Remote Help](../fundamentals/endpoints.md#remote-help).
  
- Support for Government Cloud is reduced: Remote Help is supported in Government Community Cloud (GCC) environments except in Azure Virtual Desktop (AVD). Remote Help isn't supported on GCC High or DoD (U.S. Department of Defense) tenants. For more information, go to [Microsoft Intune for US Government GCC High and DoD service description](../fundamentals/government-service.md).
  
- Remote Help sharers, helpers, and devices must be in the same tenant: Remote Help's integration with compliance policies and role-based access control (RBAC) requires all participants to be in the same tenant.
  
  > [!NOTE]
  > This can affect outsourced helpdesk scenarios where helpdesk admins are working across tenants. Consider a scenario where your user's (sharers) device belongs to tenant A, but the helper's device belongs to tenant B (in the case where they're using a device issued by their outsourcing organization). As a workaround, consider supplying devices joined to your tenant A to the helpdesk, or consider providing them with access to Windows 365 or AVD devices joined to tenant A.
  
- Combine with Endpoint Analytics: Use data from Remote Help sessions to identify common issues. For example, if many sessions show compliance warnings, consider improving your device compliance policies. Remote Help audit logs combined with Intune Endpoint Analytics might provide insights into support trends, such as frequently problematic apps or policies.
  
- Keep the Remote Help apps up to date: New versions of Windows and macOS bring improvements and required fixes. Microsoft might enforce upgrades for older versions. Use automatic updates on both platforms, or regularly deploy the latest package through Intune after testing. For Android, updates are available through Google Play. Monitor devices during regular maintenance windows to ensure that they receive the latest version.
  
- Plan for privacy and compliance: Remote Help may raise privacy concerns. To help address these concerns, communicate that Remote Help requires user consent for attended sessions. For unattended access on Windows and Android devices, users can't observe the actions performed by support personnel but they're notified when an unattended session is active. All Remote Help sessions are clearly indicated to users, and no session recordings are stored by the service. Consider documenting these behaviors in your organization's IT policies and user guidance. Because unattended access allows support without an active user present, use it only for appropriate administrative and support scenarios.
  
- Rollout in phases: If possible, deploy Remote Help in a pilot phase. Start with IT or a small department to work out any issues. Gather feedback from both helpers and users. Once you are confident, expand to the whole organization. A phased approach can prevent overwhelming the helpdesk with unexpected technical issues.  

### Helper and client modes  

Remote Help clients support different modes based on the combination of the helper app and the sharer app. Windows, macOS, and Android have Remote Help apps that can be installed that enhance functionality. Remote Help apps are sometimes referred to as a *native app*. Remote Help also supports sharing from devices with reduced capabilities from a web app. 

These are the different modes: 

- **Attended**: Support session in which an end user participates and grants access to the helper. Attended sessions support view-only access, full control, and optional UAC elevation.

  **View only**: Request view of the remote screen. To minimize effect on end user privacy, this option is recommended unless full control is necessary.
  
  **Request full control**: Request full control of the remote device.
  
  **Elevation**: Allows helpers to enter User Account Control (UAC) credentials when prompted on the sharer's device. Enabling elevation also allows the helper to view and control the sharer's device when the sharer grants the helper access.
  
- **Unattended**: A support session that allows authorized helpers to access and control an Intune-managed device without an active participant in the session. This capability is supported on Windows and Android devices.

This table shows the mode support by helper app and sharer app.  

| |Helping from:</br>Windows native|Helping from:</br>Windows web|Helping from:</br>macOS web|
|---|---|---|---|
|**Sharing from:</br>Windows native**|✅ View only</br>✅ Full control</br>✅ Elevation|✅ Unattended|Unsupported|
|**Sharing from:</br>macOS native**|Unsupported|✅ View only</br>✅ Full control|✅ View only</br>✅ Full control|
|**Sharing from:</br>Android native**|Unsupported|✅ View only</br>✅ Full control</br>✅ Unattended|✅ View only</br>✅ Full control</br>✅ Unattended|
|**Sharing from:</br>macOS webapp**|Unsupported|✅ View only|✅ View only</br>|
|**Sharing from:</br>Windows webapp**|Unsupported|✅ View only|✅ View only</br>|

> [!NOTE]
> For Windows devices receiving support, attended and unattended sessions are provided through separate Remote Help applications. View only, full control, and elevation apply to the attended experience, while unattended control applies to the unattended experience.

For information about deploying the Remote Help apps, see [Deploy Remote Help](deploy.md).

## Authentication and permissions  

Both helpers and sharers sign in to your organization using Microsoft Entra ID, which ensures that proper trusts are established for the Remote Help sessions.

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, tenant administrators determine which users can provide help and the level of help they can provide.

### Role based access control (RBAC)

To use Remote Help, helpers must have the appropriate role based access control (RBAC) permissions assigned to their user account. The following table lists the available permissions for Remote Help and their descriptions.

|Permission|Description|
|---|---|
|Remote Help app - View screen|Allows the helper to view the sharer's screen without taking control.|
|Remote Help app - Take full control|Allows the helper to take full control of the sharer's device.|
|Remote Help app - Elevation|Allows the helper to interact with the user account control prompts on Windows.|
|Remote Help app - Android unattended control| Allows the helper to connect to Android devices without requiring the sharer to accept the connection each time. This capability requires the Android device to be enrolled in Intune as a dedicated device. Assign this permission explicitly and scope it to the specific devices that can receive unattended support.|
|Remote Help app - Windows unattended control remote sign-in| Allows the helper to start an unattended remote sign-in session to a targeted, physical, corporate-owned Windows device without requiring the sharer to accept the connection each time. Assign this permission explicitly and scope it to the specific devices that can receive unattended support.|
|Remote Tasks - Offer remote assistance| Allows the helper to offer remote assistance to users.|
|Remote Assistance Connector - Read|Required to allow the user to see if Remote Help is configured for the tenant when starting a session.|

The following Intune built-in roles include Remote Help permissions:

- Help Desk Operator (View screen, take full control, elevation, Android unattended control, Remote Tasks - Offer remote assistance, Remote Assistance Connector - Read)
- School Administrator (View screen, take full control, elevation, Remote Tasks - Offer remote assistance, Remote Assistance Connector - Read)

> [!NOTE]
> A person needs a combination of the *Remote Tasks - Offer Remote Assistance* permission, the *Remote Assistance Connector - read* permission, and at least one of the Remote Help permissions to provide help. The permissions are granted to users in the admin group of a role assignment for the users or devices in the defined scope groups. For more information about Intune role-based access control, see [About role-based access control (RBAC) for Microsoft Intune](../fundamentals/role-based-access-control/overview.md).

> [!IMPORTANT]
> If a sharer or a sharer's device isn't in the scope of a helper, that helper can't provide assistance. The *All Devices* scope group doesn't include unenrolled devices. Instead, use a user scope group during the assignment process.
>
> If you select a group to exclude from assignment such as a policy or app assignment, it needs to either be nested in one of the RBAC assignment [scope groups](../fundamentals/role-based-access-control/overview.md#about-intune-role-assignments), or it needs to be separately listed as a scope group in the RBAC role assignment.

## Prerequisites

Remote Help has the following requirements: 

- A Remote Help license for everyone targeted to use the service — both helpers (IT support workers) and sharers (users).
- A [supported platform or device](#supported-platforms).  
- Intune-enrolled devices must be registered with Microsoft Entra.  

[!INCLUDE [additional-licensing](../includes/licensing/additional-licensing.md)]

## Limitations
Remote Help has the following limitations:  

- You can't establish a Remote Help session from one tenant to a different tenant.
- Remote Help might not be available in all markets or localizations.
- Remote Help is supported in Government Community Cloud (GCC) environments on the following platforms:
  - Windows
  - Windows on ARM64 devices
  - Windows 365
  - Samsung and Zebra devices enrolled as Android Enterprise dedicated devices
  - macOS 13, 14, and 15
- Remote Help isn't supported on GCC High or DoD (U.S. Department of Defense) tenants. For more information, go to [Microsoft Intune for US Government GCC High and DoD service description](../fundamentals/government-service.md).

## Supported platforms

Each platform has specific prerequisites and capabilities.

### [:::image type="icon" source="../media/icons/16/windows.svg"::: **Windows**](#tab/windows)

For attended control, Remote Help supports:
- Windows x86, x64, and ARM64
- Windows 365
- Azure Virtual Desktop (desktop and RemoteApp sessions)  

For unattended control, additional requirements apply. The target device must be a physical, Intune-managed, corporate-owned Windows device running an x64-based operating system and be Microsoft Entra joined or Microsoft Entra hybrid joined. Virtual devices, including Windows 365 and Azure Virtual Desktop, as well as unenrolled and personally owned (BYOD) devices, aren't supported for unattended control. Devices that don't meet these requirements can still receive attended support.

To receive Remote Help notifications and unattended support requests, ensure that the target device has the Intune Management Extension (IME) installed. We also recommend keeping Windows and the Intune Management Extension up to date to ensure the most reliable experience. For more information, see [Intune management extension](../device-management/tools/management-extension-windows.md).

We don't recommend remotely starting a session to users on Azure virtual desktops. For more information, see [Provide help in Azure Virtual Desktop desktop and RemoteApp sessions](start-session.md#provide-help-in-azure-virtual-desktop-desktop-and-remoteapp-sessions). 

### [:::image type="icon" source="../media/icons/16/macos.svg"::: **macOS**](#tab/macos)

- macOS 13 (Ventura)
- macOS 14 (Sonoma)
- macOS 15 (Sequoia)
- macOS 26.0 (from version 1.0.2509231 of Remote Help and later)

### [:::image type="icon" source="../media/icons/16/android.svg"::: **Android**](#tab/android)

Remote Help is supported on the following Android Enterprise devices enrolled in dedicated mode:

- Samsung Knox devices
  - The device must have Samsung Knox. For a list of Knox compatible devices, see [Device Compatibility Knox Solutions](https://www.samsungknox.com/knox-platform/supported-devices) (opens Samsung website). Samsung devices without Knox work for screen share, but don't work in full control or unattended mode.  
- Zebra devices
  - Running MX version 8.3 or later.    
  - Unattended control is only supported on MX version 9.3 and later.   
  - Set up Zebra OEMConfig for your tenant. For more information, see [Use OEMConfig on Android Enterprise devices in Microsoft Intune](../device-configuration/templates/configure-oemconfig-android.md).  

- Set up Managed Google Play for your tenant. For more information, see [Connect your Intune account to your Managed Google Play account](../device-enrollment/android/connect-managed-google-play.md).  
- Install the Intune app on devices with a version later than 5.0.5541.0.  
- Devices must not have device configuration policy set to block screen capture.  

### [:::image type="icon" source="../media/icons/16/globe.svg"::: **Web App**](#tab/webapp)

Device support is dependent on both the users operating system, and their web browser.  

- Safari, version 16.4.1 and later
- Chrome, version 109 and later
- Microsoft Edge, version 109 and later
- Firefox, version 122 and later  

> [!NOTE]
> Virtual machines (VMs) aren't supported.

#### macOS versions

- macOS 11 Big Sur (web app only)
- macOS 12 Monterey
- macOS 13 Ventura
- macOS 14 Sonoma

#### Windows versions  

- Windows 11

 > [!IMPORTANT]
 > [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]


#### Linux versions

Remote Help isn't supported on Linux. However, the Remote Help web app might function for most Linux devices that are using a supported browser.

---

## Network considerations

Both the helper and sharer must be able to reach specific endpoints over port 443. For more information, see [Network endpoints for Remote Help](../fundamentals/endpoints.md#remote-help).

Remote Help communicates over port 443 (https) and connects to the Remote Assistance Service at `https://remotehelp.microsoft.com` by using the Remote Desktop Protocol (RDP). The traffic is encrypted with TLS 1.2.

## Requirements and prerequisites

### [:::image type="icon" source="../media/icons/16/windows.svg"::: **Windows**](#tab/windows)

#### Attended control

If your organization restricts Remote Help to enrolled devices only, the sharer's Windows device must be enrolled into the same tenant where the Remote Help session is starting from.

#### Unattended control

Remote Help for unattended control is supported only on enrolled devices. The following requirements also apply to the target device:

- The Azure Virtual Desktop agent and Azure Virtual Desktop agent bootloader must be installed. Install the agent first, and then install the bootloader. No further configuration is required after installation. You can deploy both as Win32 apps. For more information, see [Deploy Remote Help](deploy.md).
- The Intune Management Extension must be installed. It's required to orchestrate the unattended session.
- Remote Desktop must be enabled on the device. You can enable this setting through an Intune settings catalog configuration profile.
- The device must be powered on and connected to the internet. Devices that are asleep, hibernating, or shut down can't receive unattended support.
- The helper must be assigned the **Remote Help app - Windows unattended control remote sign-in** permission scoped to the target devices.

### [:::image type="icon" source="../media/icons/16/macos.svg"::: **macOS**](#tab/macos)

If your organization restricts Remote Help to enrolled devices, the following requirements ensure Remote Help can authenticate the user and recognize the device as enrolled:

1. Configure the Microsoft Enterprise SSO plug-in. For more information, see [Use Enterprise SSO Plug-in on macOS](../device-configuration/templates/configure-enterprise-sso-plugin-macos.md?tabs=prereq-intune%2Ccreate-profile-intune).
1. Open and sign in to Company Portal. The user must open and sign in to Company Portal for Remote Help to recognize the device is enrolled.

> [!NOTE]
> Company Portal isn't supported on devices enrolled without user affinity. To use Remote Help on these devices, you need to change your tenant settings to set **Remote Help to unenrolled devices** to **Allowed**.

### [:::image type="icon" source="../media/icons/16/android.svg"::: **Android**](#tab/android)

- Remote Help only supports enrolled Android devices.

- Supported Zebra and Samsung devices in Android Dedicated Device (COSU) mode do not require a Sharer license because no user is signed in. Only the Helper requires a Remote Help license.

### [:::image type="icon" source="../media/icons/16/globe.svg"::: **Web App**](#tab/webapp)

The web app has the same requirements as the platform of the sharer.

---

## Supported languages for chat

Remote Help with chat *on* is supported in the following languages:

### [:::image type="icon" source="../media/icons/16/windows.svg"::: **Windows**](#tab/windows)

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

### [:::image type="icon" source="../media/icons/16/macos.svg"::: **macOS**](#tab/macos)

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

### [:::image type="icon" source="../media/icons/16/android.svg"::: **Android**](#tab/android)

The Remote Help app for Android uses the language set on the device. The Remote Help app for Android supports all languages that are supported by Android.

### [:::image type="icon" source="../media/icons/16/globe.svg"::: **Web App**](#tab/webapp)

The Remote Help web app supports all of the languages supported by the browser being used.

---

## Data and privacy

Microsoft logs a small amount of session data to monitor the health of the Remote Help system. This data includes the following information:

- Start and end time of the session. This information is stored on Microsoft servers for 30 days.
- Who helped whom and on what device. This information is stored on Microsoft servers for 30 days.
- Errors arising from Remote Help itself, such as unexpected disconnections. This information is stored on the sharer's device in the event viewer.  
- Features used inside the app, such as view only and elevation. This information is stored on Microsoft servers for 30 days.

Remote Help logs session details to the Windows Event Logs on the device of both the helper and sharer. Microsoft can't access a session or view any actions or keystrokes that occur in the session.

The helper and sharer see the following information about the other individual, taken from their organizational profiles:

- Their organization profile picture (if present)
- Company name
- Verified domain
- First and last name
- Job title

Microsoft doesn't store any data about the sharer or the helper for longer than 30 days.

---

## Next Steps

> [!div class="nextstepaction"]
> [Next: Deploy Remote Help >](deploy.md)
