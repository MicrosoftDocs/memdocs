---
title: Plan for Remote Help with Microsoft Intune
description: Learn about the requirements and capabilities of Remote Help with Microsoft Intune on Windows, macOS, and Android Enterprise.
author: lenewsad
ms.author: lanewsad
ms.date: 10/16/2025
ms.topic: how-to
ms.localizationpriority: high
ms.reviewer: karawang
ms.subservice: suite
ms.collection:
- M365-identity-device-management
- highpri
- highseo
---

 # Planning for Remote Help with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

[!INCLUDE [remote-help-overview](includes/remote-help-overview.md)]

In this article, users who provide help are referred to as *helpers*, and users that receive help are referred to as *sharers*, as they share their session with the helper. Both helpers and sharers sign in to your organization to use the app. It's through your Microsoft Entra ID that the proper trusts are established for the Remote Help sessions.

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, you determine which users can provide help and the level of help they can provide.

> [!TIP]
> As a companion to this article, see our [Intune Suite‎ add-ons guide](https://go.microsoft.com/fwlink/?linkid=2314425) to review the step-by-step process to assign licenses, configure settings, and enable add-ons across your organization's devices. For a customized experience based on your environment, you can access the [Intune Suite‎ add-ons guide](https://go.microsoft.com/fwlink/?linkid=2314706) in the Microsoft 365 admin center.  

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
- Enrolled and or unenrolled devices  

## Planning considerations  

Use these considerations to prepare your organization for Remote Help.    

- Enforce least privilege: Only grant the minimum Remote Help permissions needed for each support role. Use custom Intune roles if necessary to limit who can take full control or perform unattended sessions. For example, level-1 support might get view-only rights, while tier-2 gets full control rights. This principle helps protect user privacy and device integrity.
  
- Use Conditional Access for helpers: Since helpers have elevated access into user devices, add an extra layer of security. Requiring MFA or compliant device status for helper accounts via Conditional Access is highly recommended. These measures ensure that a compromised helper account can't easily be used maliciously to access devices. Entra ID Conditional Access policies for Remote Help are only supported on Windows and macOS.
  
- Enable unenrolled device support only if needed: Allowing Remote Help on unenrolled devices (Entra registered only) is convenient for supporting personal devices, but it comes with reduced oversight (no device compliance info or limited audit data). Enable that feature thoughtfully and consider limiting which support staff can help unenrolled devices (perhaps via separate roles).
  
- Network and firewall: Verify that corporate network policies don't interfere with Remote Help. The app communicates over port 443 to Azure cloud endpoints. If your users are on a corporate network, ensure proxy or SSL inspection doesn't break the connection. If your proxy servers are using SSL inspection, the domains listed for Remote Help should be excluded to avoid issues. For more information, see [Network endpoints for Remote Help](intune-endpoints.md#remote-help).
  
- Support for Government Cloud is reduced: Remote Help is supported in Government Community Cloud (GCC) environments except in Azure Virtual Desktop (AVD). Remote Help isn't supported on GCC High or DoD (U.S. Department of Defense) tenants. For more information, go to [Microsoft Intune for US Government GCC High and DoD service description](intune-govt-service-description.md).
  
- Remote Help sharers, helpers, and devices must be in the same tenant: Remote Help's integration with compliance policies and role-based access control (RBAC) requires all participants to be in the same tenant.
  
  > [!NOTE]
  > This can affect outsourced helpdesk scenarios where helpdesk admins are working across tenants. Consider a scenario where your user's (sharers) device belongs to tenant A, but the helper's device belongs to tenant B (in the case where they're using a device issued by their outsourcing organization). As a workaround, consider supplying devices joined to your tenant A to the helpdesk, or consider providing them with access to Windows 365 or AVD devices joined to tenant A.
  
- Combine with Endpoint Analytics: Use the data from Remote Help sessions to identify common issues. For example, if many sessions show compliance warnings, perhaps improve your device compliance policies. Remote Help's audit logs combined with Intune's Endpoint Analytics might give insights into support trends (like frequently problematic apps or policies).
  
- Keep the Remote Help apps up to date: New versions of Windows and Mac bring improvements and required fixes. Microsoft might enforce upgrades for older versions. Use autoupdate on both platforms (Windows Update, Mac via Microsoft AutoUpdate) or regularly push the latest package via Intune after testing. For Android, updates come through the Play Store automatically if you approved the app – monitor that devices are getting the latest version during your regular maintenance windows.
  
- Plan for privacy and compliance: Remote Help can raise privacy questions. Assure stakeholders that Remote Help requires user consent or in the case of Android unattended Remote Help, clearly indicates a remote session is active. All sessions are consensual and visibly indicated on the user's screen. No session recordings are stored in the service. These points can be included in your internal IT policies or user guides to address concerns. Unattended access on Android should be used sparingly.
  
- Rollout in phases: If possible, deploy Remote Help in a pilot phase. Start with IT or a small department to work out any issues. Gather feedback from both helpers and users. Once you are confident, expand to the whole organization. A phased approach can prevent overwhelming the helpdesk with unexpected technical issues.  

### Helper and client modes  

Remote Help clients support different modes based on the combination of the helper app and the sharer app. Windows, macOS, and Android have Remote Help apps that can be installed that enhance functionality. Remote Help apps are sometimes referred to as a *native app*. Remote Help also supports sharing from devices with reduced capabilities from a web app. 

These are the different modes: 

- **View only**: Request view of the remote screen. To minimize effect on end user privacy, this option is recommended unless full control is necessary.
  
- **Request full control**: Request full control of the remote device.
  
- **Elevation**: Allows helpers to enter User Account Control (UAC) credentials when prompted on the sharer's device. Enabling elevation also allows the helper to view and control the sharer's device when the sharer grants the helper access.
  
- **Unattended**: Full control of the device without the presence of an end user.  

This table shows the mode support by helper app and sharer app.  

| |Helping from:</br>Windows native|Helping from:</br>Windows web|Helping from:</br>macOS web|
|---|---|---|---|
|**Sharing from:</br>Windows native**|✅ View only</br>✅ Full control</br>✅ Elevation|Unsupported|Unsupported|
|**Sharing from:</br>macOS native**|Unsupported|✅ View only</br>✅ Full control|✅ View only</br>✅ Full control|
|**Sharing from:</br>Android native**|Unsupported|✅ View only</br>✅ Full control</br>✅ Unattended|✅ View only</br>✅ Full control</br>✅ Unattended|
|**Sharing from:</br>macOS webapp**|Unsupported|✅ View only|✅ View only</br>|
|**Sharing from:</br>Windows webapp**|Unsupported|✅ View only|✅ View only</br>|

For information about deploying the Remote Help apps, see [Deploy Remote Help](remote-help-deploy.md).

## Authentication and permissions  

Both helpers and sharers sign in to your organization using Microsoft Entra ID, which ensures that proper trusts are established for the Remote Help sessions.

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, tenant administrators determine which users can provide help and the level of help they can provide.

### Role based access control (RBAC)

To use Remote Help, helpers must have the appropriate role based access control (RBAC) permissions assigned to their user account. The following table lists the available permissions for Remote Help and their descriptions.

|Permission|Description|
|---|---|
|Remote Help - View screen|Allows the helper to view the sharer's screen without taking control.|
|Remote Help - Take full control|Allows the helper to take full control of the sharer's device.|
|Remote Help - Elevation|Allows the helper to interact with the user account control prompts on Windows.|
|Remote Help - Unattended| Allows the helper to connect to Android devices without requiring the sharer to accept the connection each time. This capability requires the Android device to be enrolled in Intune as a fully managed device or as a dedicated device.|
|Remote Tasks - Offer remote assistance| Allows the helper to offer remote assistance to users.|
|Remote Assistance Connector - Read|Required to allow the user to see if Remote Help is configured for the tenant when starting a session.|

The following Intune built-in roles include Remote Help permissions:

- Help Desk Operator (View screen, take full control, elevation, unattended, Remote Tasks - Offer remote assistance, Remote Assistance Connector - Read)
- School Administrator (View screen, take full control, elevation, Remote Tasks - Offer remote assistance, Remote Assistance Connector - Read)

> [!NOTE]
> A person needs a combination of the *Remote Tasks - Offer Remote Assistance* permission, the *Remote Assistance Connector - read* permission, and at least one of the Remote Help permissions to provide help. The permissions are granted to users in the admin group of a role assignment for the users or devices in the defined scope groups. For more information about Intune role-based access control, see [About role-based access control (RBAC) for Microsoft Intune](../fundamentals/role-based-access-control.md).

> [!IMPORTANT]
> If a sharer or a sharer's device isn't in the scope of a helper, that helper can't provide assistance. The *All Devices* scope group doesn't include unenrolled devices. Instead, use a user scope group during the assignment process.
>
> If you select a group to exclude from assignment such as a policy or app assignment, it needs to either be nested in one of the RBAC assignment [scope groups](role-based-access-control.md#about-intune-role-assignments), or it needs to be separately listed as a scope group in the RBAC role assignment.

## Prerequisites

Remote Help has the following requirements: 

- [Intune subscription](../fundamentals/licenses.md).  
- [Remote Help add on license or an Intune Suite license](intune-add-ons.md#available-add-ons) for all IT support workers (helpers) and users (sharers) that are targeted to use Remote Help and benefit from the service.  
- [Supported platforms and devices](#supported-platforms).  
- Intune-enrolled devices must be registered with Microsoft Entra.  

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
- Remote Help isn't supported on GCC High or DoD (U.S. Department of Defense) tenants. For more information, go to [Microsoft Intune for US Government GCC High and DoD service description](intune-govt-service-description.md).

## Supported platforms

Each platform has specific prerequisites and capabilities.

### [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

- Windows x86, x64, and ARM64
- Windows 365
- Azure Virtual Desktop

There are optional Windows updates for higher notification reliability:

- Windows 11: [July 25, 2023—KB5028245 (OS Build 22000.2245) Preview - Microsoft Support](https://support.microsoft.com/topic/july-25-2023-kb5028245-os-build-22000-2245-preview-bbe6f09f-6cec-4777-a548-d237f5d849d2)
- Windows 10: [August 22, 2023—KB5029331 (OS Build 19045.3393) Preview - Microsoft Support](https://support.microsoft.com/topic/august-22-2023-kb5029331-os-build-19045-3393-preview-9f6c1dbd-0ee6-469b-af24-f9d0bf35ca18)

 > [!IMPORTANT]
 > [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

The Intune management extension is required on the sharer's device for the remote launch feature. Specifically for Windows 10 the OS builds need to be greater than or equal to version 19042 and have KB5018410 patch installed. The OS version should be greater than or equal to 10.0.19042.2075 or 10.0.19043.2075 or 10.0.19044.2075. For more information about the Intune management extension, see [Intune management extension](../apps/intune-management-extension.md).  

We don't recommend remotely starting a session to users on Azure virtual desktops. For more information, see [How to provide help on an AVD](remote-help-use.md#provide-help-on-an-avd). 

### [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

- macOS 13 (Ventura)
- macOS 14 (Sonoma)
- macOS 15 (Sequoia)
- macOS 26.0 (from version 1.0.2509231 of Remote Help and later)

### [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

Remote Help is supported on the following Android Enterprise devices enrolled in dedicated mode:

- Samsung Knox devices
  - The device must have Samsung Knox. For a list of Knox compatible devices, see [Device Compatibility Knox Solutions](https://www.samsungknox.com/knox-platform/supported-devices) (opens Samsung website). Samsung devices without Knox work for screen share, but don't work in full control or unattended mode.  
- Zebra devices
  - Running MX version 8.3 or later.    
  - Unattended control is only supported on MX version 9.3 and later.   
  - Set up Zebra OEMConfig for your tenant. For more information, see [Use OEMConfig on Android Enterprise devices in Microsoft Intune](../configuration/android-oem-configuration-overview.md).  

- Set up Managed Google Play for your tenant. For more information, see [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md).  
- Install the Intune app on devices with a version later than 5.0.5541.0.  
- Devices must not have device configuration policy set to block screen capture.  

### [:::image type="icon" source="../media/icons/webapp.svg"::: **Web App**](#tab/webapp)

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

Both the helper and sharer must be able to reach specific endpoints over port 443. For more information, see [Network endpoints for Remote Help](intune-endpoints.md#remote-help).

Remote Help communicates over port 443 (https) and connects to the Remote Assistance Service at `https://remotehelp.microsoft.com` by using the Remote Desktop Protocol (RDP). The traffic is encrypted with TLS 1.2.

## Requirements if Remote Help is restricted to enrolled devices  

If your organization restricts Remote Help to enrolled devices only, there are extra requirements.  

### [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

The sharer's Windows device must be enrolled into the same tenant where the Remote Help session is starting from.

### [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

1. **Single sign-on (SSO)**. For more information, see [Use Enterprise SSO Plug-in on macOS](../configuration/use-enterprise-sso-plug-in-macos-with-intune.md?tabs=prereq-intune%2Ccreate-profile-intune).
1. Open and sign in to Company Portal. The user must open and sign into Company Portal for Remote Help to recognize the device is enrolled.

> [!NOTE]
> Company Portal isn't supported on devices enrolled without user affinity. To use Remote Help on these devices, you need to change your tenant settings to set **Remote Help to unenrolled devices** to **Allowed**.

### [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

Remote Help doesn't support unenrolled devices on Android.

### [:::image type="icon" source="../media/icons/webapp.svg"::: **Web App**](#tab/webapp)

The web app has the same requirements as the platform of the sharer.

---

## Supported languages for chat

Remote Help with chat *on* is supported in the following languages:

### [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

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

### [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

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

### [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

The Remote Help app for Android uses the language set on the device. The Remote Help app for Android supports all languages that are supported by Android.

### [:::image type="icon" source="../media/icons/webapp.svg"::: **Web App**](#tab/webapp)

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
> [Next: Deploy Remote Help >](remote-help-deploy.md)
