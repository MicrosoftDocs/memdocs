---
title: Plan for Remote Help with Microsoft Intune
description: Learn about the requirements and capabilities of Remote Help with Microsoft Intune on Windows, macOS, and Android Enterprise.
author: lenewsad
ms.author: lanewsad
ms.date: 10/01/2025
ms.topic: how-to
ms.localizationpriority: high
ms.reviewer: karawang
ms.collection:
- M365-identity-device-management
- highpri
- highseo
---

 # Planning for Remote Help with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

[!INCLUDE [remote-help-overview](includes/remote-help-overview.md)]

In this article, users who provide help are referred to as *helpers*, and users that receive help are referred to as *sharers* as they share their session with the helper. Both helpers and sharers sign in to your organization to use the app. It's through your Microsoft Entra ID that the proper trusts are established for the Remote Help sessions.

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, you determine which users can provide help and the level of help they can provide.

> [!TIP]
> As a companion to this article, see our [Intune Suite‎ add-ons guide](https://go.microsoft.com/fwlink/?linkid=2314425) to review the step-by-step process to assign licenses, configure settings, and enable add-ons across your organization's devices. For a customized experience based on your environment, you can access the [Intune Suite‎ add-ons guide](https://go.microsoft.com/fwlink/?linkid=2314706) in the Microsoft 365 admin center.  

## Planning checklist

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

When planning for Remote Help, consider:

- **Enforce Least Privilege**: Only grant the minimum Remote Help permissions needed for each support role. Use custom Intune roles if necessary to limit who can take full control or perform unattended sessions 2. For example, level-1 support might get view-only rights, while tier-2 gets full control rights. This principle helps protect user privacy and device integrity.
- **Use Conditional Access for Helpers**: Since helpers have elevated access into user devices, add an extra layer of security. Requiring MFA or compliant device status for helper accounts via Conditional Access is highly recommended. These additional measures ensure that a compromised helper account can't easily be used maliciously to access devices. Entra ID Conditional Access policies for Remote Help are only supported on Windows and macOS.
- **Enable Unenrolled Device Support Only If Needed**: Allowing Remote Help on unenrolled devices (Entra registered only) is convenient for supporting personal devices, but it comes with reduced oversight (no device compliance info or limited audit data). Enable that feature thoughtfully and consider limiting which support staff can help unenrolled devices (perhaps via separate roles).
- **Network and Firewall**: Verify that corporate network policies don't interfere with Remote Help. The app communicates over port 443 to Azure cloud endpoints. If your users are on a corporate network, ensure proxy or SSL inspection doesn't break the connection. If your proxy servers are using SSL inspection, the domains listed for Remote Help should be excluded to avoid issues).
- **Support for Government Cloud is reduced**: Remote Help is supported in Government Community Cloud (GCC) environments on except in Azure Virtual Desktop (AVD). Remote Help isn't supported on GCC High or DoD (U.S. Department of Defense) tenants. For more information, go to [Microsoft Intune for US Government GCC High and DoD service description](intune-govt-service-description.md).
- **Cross-Tenant support is not available**: Remember, you can't use Remote Help across different Microsoft Entra tenants. If your organization has multiple tenants or you support external clients, Remote Help won't function for those scenarios yet.
  > [!NOTE]
  > Lack of cross tenant support can affect outsourced helpdesk scenarios. Consider a scenario where your user's (sharers) device belongs to tenant A, but the helper's device belongs to tenant B (in the case where they're using a device issued by their outsourcing organization)  As a workaround, consider supplying devices joined to your tenant A to the helpdesk, or consider providing them with access to Windows 365 or AVD devices joined to tenant A.
- **Combine with Endpoint Analytics**: Use the data from Remote Help sessions to identify common issues. For example, if many sessions show compliance warnings, perhaps improve your device compliance policies. Remote Help's audit logs combined with Intune's Endpoint Analytics might give insights into support trends (like frequently problematic apps or policies).
- **Keep the Remote Help apps up to date**: On Windows and Mac, new versions bring improvements and required fixes. Microsoft might enforce upgrades for older versions. Use autoupdate on both platforms (Windows Update, Mac via Microsoft AutoUpdate) or regularly push the latest package via Intune after testing. For Android, updates come through the Play Store automatically if you approved the app – monitor that devices are getting the latest version during your regular maintenance windows.
- **Plan for Privacy and Compliance**: Remote Help can raise privacy questions. Assure stakeholders that Remote Help requires user consent and doesn't give IT silent access by default. All sessions are consensual and visibly indicated on the user's screen. No session recordings are stored in the service. These points can be included in your internal IT policies or user guides to address concerns. Unattended access on Android should be used sparingly.
- **Rollout in Phases**: If possible, deploy Remote Help in a pilot phase. Start with IT or a small department to work out any issues. Gather feedback from both helpers and users. Once confident, expand to the whole organization. A phased approach can prevent overwhelming the helpdesk with unexpected technical issues.

## Remote Help capabilities

The Remote Help app supports the following capabilities in general across the supported platforms.

- **Enable Remote Help for your tenant**: By default, Remote Help isn't enabled for Intune tenants. If you choose to turn on Remote Help, its use is enabled tenant-wide. Remote Help must be enabled before users can be authenticated through your tenant when using Remote Help.

- **Chat functionality**: Remote Help includes enhanced chat that maintains a continuous thread of all messages. This chat supports special characters and other languages including Chinese and Arabic. For more information on languages supported, see [Languages Supported](remote-help-plan.md#supported-languages).

- **Use Remote Help with unenrolled devices**: This setting is turned off by default. For Windows and macOS devices, enabling this option allows help to be provided to devices that aren't enrolled in Intune. This setting doesn't apply to devices used by helpers.

- **Requires Organization login**: To use Remote Help, both the helper and the sharer must sign in with a Microsoft Entra account from your organization. You can't use Remote Help to assist users who aren't members of your organization.

- **Compliance Warnings**: Before a helper connects to a user's non-compliant device, the helper will be shown a warning. This warning doesn't block access but provides transparency about the risk of using sensitive data like administrative credentials during the session.

If the user's device that they're trying to connect to isn't enrolled, the helper sees a prompt that the user's device is unenrolled.

- **Conditional Access**: Administrators can now utilize Conditional Access capability when setting up policies and conditions for Remote Help. For more information on setting up Conditional Access, go to [Setup Conditional Access for Remote Help](remote-help-windows.md#setup-conditional-access-for-remote-help).

- **Role-based access control**: Admins can set RBAC rules that determine the scope of a helper's access, such as:
  - The users who can help others and the range of actions they can do while providing help. For example, who can run elevated privileges while helping.
  - The users who can only view a device, and who can request full control of the session while assisting others.

- **Monitor active Remote Help sessions, and view details about past sessions**: In the Microsoft Intune admin center, you can view reports that include details about who helped who, on what device, and for how long. You can also find details about active sessions. An administrator can also reference audit log sessions created for Remote Help in Intune under **Tenant Administration** > **Audit Logs**.

  For unenrolled devices, auditing the Remote Help sessions is limited.

- **Web app for sharers** - In situations where the Sharer needs assistance but is unable to install the native application for macOS, the Sharer can use the Web App to share their screen to a helper. This web app provides view only capabilities to the helper, allowing them to guide the user through resolving issues.

### Helper and client modes

Remote Help clients support different modes based on the combination of the helper app and the sharer app. Windows, macOS, and Android have Remote Help apps that can be installed that enhance functionality. These Remote Help apps are sometimes referred to as a native app. Remote Help also supports sharing from devices with reduced capabilities from a web app.

These are the different modes:

- **View only**: Request view of the remote screen. To minimize effect on end user privacy, this option is recommended unless full control is necessary.
- **Request full control**: Request full control of the remote device.
- **Elevation**: Allows helpers to enter UAC credentials when prompted on the sharer's device. Enabling elevation also allows the helper to view and control the sharer's device when the sharer grants the helper access.
- **Unattended**: Full control of the device without the presence of an end user.

This table shows the mode support by helper app and sharer app.

|Sharer app|Windows native|Windows web|macOS web|
|---|---|---|---|
|Windows native|✅ View only</br>✅ Full Control</br>✅ Elevation|Unsupported|Unsupported|
|macOS native|Unsupported|✅ View only</br>✅ Full Control|✅ View only</br>✅ Full Control|
|Android native|Unsupported|✅ View only</br>✅ Full Control</br>✅ Unattended|✅ View only</br>✅ Full Control</br>✅ Unattended|
|macOS webapp|Unsupported|✅ View only|✅ View only</br>|
|Windows webapp|Unsupported|✅ View only|✅ View only</br>|

For information on deploying the Remote Help apps, see [Deploy Remote Help](remote-help-deploy.md).

## Authentication and Permissions

Both Helpers and Sharers sign in to your organization using Microsoft Entra ID, which ensures that proper trusts are established for the Remote Help sessions.

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, tenant administrators determine which users can provide help and the level of help they can provide.

### Role based access control (RBAC)

To use Remote Help, helpers must have the appropriate Role based access control (RBAC) permissions assigned to their user account. The following table lists the available permissions for Remote Help and their descriptions.

|Permission|Description|
|---|---|
|Remote Help - View screen|Allows the helper to view the sharer's screen without taking control.|
|Remote Help - Take full control|Allows the helper to take full control of the sharer's device.|
|Remote Help - Elevation|Allows the helper to interact with the user account control prompts on Windows.|
|Remote Help - Unattended| Allows the helper to connect to Android devices without requiring the sharer to accept the connection each time. This capability requires the Android device to be enrolled in Intune as a fully managed device or as a dedicated device.|

The following Intune built-in roles include Remote Help permissions:

- School Administrator (View screen, take full control, elevation)
- Help Desk Operator (View screen, take full control, elevation, unattended)

## Prerequisites

General prerequisites that apply to Remote Help:

- [Intune subscription](../fundamentals/licenses.md)
- [Remote Help add on license or an Intune Suite license](intune-add-ons.md#available-add-ons) for all IT support workers (helpers) and users (sharers) that are targeted to use Remote Help and benefit from the service.
- [Supported platforms and devices](#supported-platforms)
- To support Remote Help Intune-enrolled devices must be registered with Microsoft Entra.

## Limitations

- You can't establish a Remote Help session from one tenant to a different tenant.
- Remote Help might not be available in all markets or localizations.
- Remote Help is supported in Government Community Cloud (GCC) environments on the following platforms:

  - Windows 10/11
  - Windows 10/11 on ARM64 devices
  - Windows 365
  - Samsung and Zebra devices enrolled as Android Enterprise dedicated devices
  - macOS 13, 14, and 15

- Remote Help isn't supported on GCC High or DoD (U.S. Department of Defense) tenants. For more information, go to [Microsoft Intune for US Government GCC High and DoD service description](intune-govt-service-description.md).

## Supported platforms

Each platform has specific prerequisites and capabilities.

### [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

- Windows 10/11 x86, x64 and ARM64
- Windows 365
- Azure Virtual Desktop

In addition, there are optional Windows updates for higher notification reliability:

- Windows 11: [July 25, 2023—KB5028245 (OS Build 22000.2245) Preview - Microsoft Support](https://support.microsoft.com/topic/july-25-2023-kb5028245-os-build-22000-2245-preview-bbe6f09f-6cec-4777-a548-d237f5d849d2)
- Windows 10: [August 22, 2023—KB5029331 (OS Build 19045.3393) Preview - Microsoft Support](https://support.microsoft.com/topic/august-22-2023-kb5029331-os-build-19045-3393-preview-9f6c1dbd-0ee6-469b-af24-f9d0bf35ca18)

The Intune management extension is required on the sharer's device for the remote launch feature. Specifically for Windows 10 the OS builds need to be greater than or equal to version 19042 and have KB5018410 patch installed. The OS version should be greater than or equal to 10.0.19042.2075 or 10.0.19043.2075 or 10.0.19044.2075. For more information on the Intune management extension, see [Intune management extension](../apps/intune-management-extension.md).

We don't recommend remotely starting a session to users on Azure virtual desktops. For more information, see [How to provide help on an AVD](remote-help-use.md#provide-help-on-an-avd).

### [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

- macOS 13 (Ventura)
- macOS 14 (Sonoma)
- macOS 15 (Sequoia)
- macOS 26.0 (from version 1.0.2509231 of Remote Help and later)

### [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

Remote Help is supported on the following Android Enterprise devices enrolled in dedicated mode:

- Samsung Knox devices
- Zebra devices
  - Running MX version 8.3 or higher
  - Unattended control is only supported on MX version 9.3 and higher

- Set up Managed Google Play for your tenant. For more information, go to [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md)
- Install the Intune app on devices with a version higher than 5.0.5541.0
- Devices must NOT have device configuration policy set to block Screen capture
- Samsung devices only: The device must have Knox. For a list of Knox compatible devices, see [Device Compatibility Knox Solutions](https://www.samsungknox.com/knox-platform/supported-devices) (opens Samsung's website). Samsung devices without Knox work for screen share, but don't work in full control or unattended mode.
- Zebra devices only: Set up Zebra OEMConfig for your tenant. For more details, go to [Use OEMConfig on Android Enterprise devices in Microsoft Intune](../configuration/android-oem-configuration-overview.md)

### [:::image type="icon" source="../media/icons/webapp.svg"::: **Web App**](#tab/webapp)

Device support is dependent on both the users operating system, and their web browser.

- Safari (version 16.4.1+)
- Chrome (version 109+)
- Microsoft Edge (version 109+)
- Firefox (version 122+)

> [!NOTE]
> Virtual Machines (VMs) aren't supported.

#### macOS Versions

- 11 Big Sur (Web app only)
- 12 Monterey
- 13 Ventura
- 14 Sonoma

#### Windows Versions

- Windows 10
- Windows 11

#### Linux Versions

Linux isn't supported by Remote Help. However, the Remote Help Web App might function for most Linux devices that are using a supported browser.

---

## Network considerations

Both the helper and sharer must be able to reach specific endpoints over port 443. For more information, see [Network endpoints for Remote Help](intune-endpoints.md#remote-help).

Remote Help communicates over port 443 (https) and connects to the Remote Assistance Service at `https://remotehelp.microsoft.com` by using the Remote Desktop Protocol (RDP). The traffic is encrypted with TLS 1.2.

## Requirements if Remote Help is restricted to enrolled devices

If your organization restricts Remote Help to enrolled devices only, there are extra requirements:

### [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

The sharer's Windows device must be enrolled into the same tenant where the Remote Help session is starting from.

### [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

1. **Single sign-on (SSO)**. For more information, see [Use Enterprise SSO Plug-in on macOS](../configuration/use-enterprise-sso-plug-in-macos-with-intune.md?tabs=prereq-intune%2Ccreate-profile-intune).
1. **Open and sign in to Company Portal**. The user must open and sign into Company Portal for Remote Help to recognize the device is enrolled.

> [!NOTE]
> Company Portal isn't supported on devices enrolled without user affinity. To use Remote Help on these devices, you need to change your tenant settings to set **Remote Help to unenrolled devices** to **Allowed**.

### [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

Remote Help doesn't support unenrolled devices on Android.

### [:::image type="icon" source="../media/icons/webapp.svg"::: **Web App**](#tab/webapp)

The web app has the same requirements as the platform of the sharer.

---

## Supported Languages

Remote Help is supported in the following languages:

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
- Features used inside the app such as view only and elevation. This information is stored on Microsoft servers for 30 days.

Remote Help logs session details to the Windows Event Logs on the device of both the helper and sharer. Microsoft can't access a session or view any actions or keystrokes that occur in the session.

The helper and sharer both see the following information about the other individual, taken from their organizational profiles:

- Their organization profile picture (if present)
- Company name
- Verified domain
- First and Last name
- Job title

Microsoft doesn't store any data about either the sharer or the helper for longer than 30 days.

---

## Next Steps

> [!div class="nextstepaction"]
> [Next: Deploy Remote Help >](remote-help-deploy.md)
