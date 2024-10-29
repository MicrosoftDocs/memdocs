---

title: Use Remote Help to assist users authenticated by your organization. 
description: With the Remote Help app, provide remote assistance to authenticated users who also run the Remote Help app.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 07/16/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: karawang
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure, has-azure-ad-ps-ref
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---
 
# Use Remote Help with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

Remote Help is a cloud-based solution for secure help desk connections with role-based access controls. With the connection, your support staff can remote connect to the user's device.

In this article, users who provide help are referred to as *helpers*, and users that receive help are referred to as *sharers* as they share their session with the helper. Both helpers and sharers sign in to your organization to use the app. It's through your Microsoft Entra ID that the proper trusts are established for the Remote Help sessions.

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, you determine which users can provide help and the level of help they can provide.

> [!IMPORTANT]
> This article describes the capabilities and configuration tasks that are applicable in general for Remote Help across supported platforms. For specific capabilities, prerequisites, and other details based on the platform that you are using, go to:
  > - [Remote Help on Windows with Microsoft Intune](remote-help-windows.md)
  > - [Remote Help on Android with Microsoft Intune](remote-help-android.md)
  > - [Remote Help on macOS with Microsoft Intune](remote-help-macOS.md)

## Remote Help capabilities and requirements

The Remote Help app supports the following capabilities in general across the supported platforms.

> [!NOTE]
> To know more about specific capabilities and requirements based on the platform that you're using, go to:
>  - [Remote Help on Windows with Microsoft Intune](remote-help-windows.md#remote-help-capabilities-and-requirements-on-windows)
>  - [Remote Help on Android with Microsoft Intune](remote-help-android.md#remote-help-capabilities-and-requirements-on-android)
>  - [Remote Help on macOS with Microsoft Intune](remote-help-macos.md#remote-help-capabilities)

- **Enable Remote Help for your tenant**: By default, Intune tenants aren't enabled for Remote Help. If you choose to turn on Remote Help, its use is enabled tenant-wide. Remote Help must be enabled before users can be authenticated through your tenant when using Remote Help.

- **Use Remote Help with unenrolled devices**: Remote Help is supported on enrolled devices that also need to be Entra registered devices. This setting is disabled by default. To allow Remote Help on devices that aren't enrolled in Intune, you must turn on this setting.

- **Requires Organization login**: To use Remote Help, both the helper and the sharer must sign in with a Microsoft Entra account from your organization. You can't use Remote Help to assist users who aren't members of your organization.

- **Compliance Warnings**: Before a helper connects to a user's device, the helper will see a non-compliance warning about that device if it's not compliant with its assigned policies.

- **Role-based access control**: Admins can set RBAC rules that determine the scope of a helper's access, such as:
  - The users who can help others and the range of actions they can do while providing help. For example, who can run elevated privileges while helping.
  - The users who can only view a device, and who can request full control of the session while assisting others.

- **Monitor active Remote Help sessions, and view details about past sessions**: In the Microsoft Intune admin center, you can view reports that include details about who helped who, on what device, and for how long. You can also find details about active sessions. An administrator can also reference audit log sessions created for Remote Help in Intune under **Tenant Administration** > **Audit Logs**.

  For unenrolled devices, auditing the Remote Help sessions is limited.

## Prerequisites

General prerequisites that apply to Remote Help:

  - [Intune subscription](../fundamentals/licenses.md)
  - [Remote Help add on license or an Intune Suite license](intune-add-ons.md#available-add-ons) for all IT support workers (helpers) and users (sharers) that are targeted to use Remote Help and benefit from the service.
  - [Supported platforms and devices](#supported-platforms-and-devices)

For specific prerequisites based on the platform that you're using, go to:

- [Remote Help on Windows with Microsoft Intune](remote-help-windows.md#prerequisites-for-remote-help-on-windows)
- [Remote Help on Android with Microsoft Intune](remote-help-android.md#prerequisites-for-remote-help-on-android)
- [Remote Help on macOS with Microsoft Intune](remote-help-macos.md#remote-help-requirements)

Limitations:  

- Remote Help is supported in Government Community Cloud (GCC) environments on the following platforms:

  - Windows 10/11
  - Windows 10/11 on ARM64 devices
  - Windows 365
  - Samsung and Zebra devices enrolled as Android Enterprise dedicated devices
  - macOS 12, 13, 14, and 15

    Remote Help isn't supported on GCC High or DoD (U.S. Department of Defense) tenants. For more information, go to [Microsoft Intune for US Government GCC High and DoD service description](intune-govt-service-description.md).

  - You cannot establish a Remote Help session from one tenant to a different tenant.
  - Remote Help might not be available in all markets or localizations.

## Supported platforms and devices

This feature applies to:  

- Windows 10/11
- Windows 11 on ARM64 devices
- Windows 10 on ARM64 devices
- Windows 365
- Android Enterprise Dedicated (Samsung and Zebra devices)
- macOS 12, 13, 14, and 15

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

## Configure Remote Help for your tenant

To configure your tenant to support Remote Help, review and complete the following tasks. These tasks are important to configure for all Remote Help platforms that are supported.

### Task 1: Enable Remote Help

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Remote Help**.

2. On the **Settings** tab:
   1. Set **Enable Remote Help** to **Enabled** to allow the use of remote help. By default, this setting is *Disabled*.
   2. Set **Allow Remote Help to unenrolled devices** to **Enabled** if you want to allow this option. By default, this setting is *Disabled*.
   3. Set **Disable chat** to **Yes** to remove the chat functionality in the Remote Help app. By default, chat is enabled and this setting is set to **No**.  

3. Select **Save**.

> [!NOTE]
> When you purchase licenses or start a trial, it could take a while to become active (anywhere between 30 minutes to 8 hours).
> When you try to create a Remote Help session you may continue to see messages indicating that Remote Help isn't enabled for the tenant even if you enabled Remote Help in the tenant after activation.

### Task 2: Configure permissions for Remote Help

Remote Help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, you determine which users can provide help and the level of help they can provide.

To protect the privacy of users who may be using the sharer device, helpers should use the minimum level of privilege required to remotely assist the device. Only request an Unattended session if you know that there's no user at the sharer device to accept the remote help session.  

The following Intune RBAC permissions manage the use of the Remote Help app. Set each to *Yes* to grant the permission:

- Category: **Remote Help app**
- Permissions:
  - **Elevation** : Yes/No
  - **View screen** : Yes/No
  - **Take full control** : Yes/No
  - **Unattended control** : Yes/No
 
> [!NOTE]
> If the **Take full control** permission is set to *Yes*, then by default, the user will have additional permission to **View screen**, even if the user's **View screen** permission is set to *No.*
> If the **Elevation** permission is set to *Yes*, then by default, the user will have additional permission to **View screen** and **Take full control**, even if the user's **View screen** and **Take full control** permission is set to *No.*
> If the **Unattended control** permission is set to *Yes*, then, by default, the user will have additional permission to **View screen**, **Take full control**, and **Elevation**, even if the user's **View screen**, **Take full control**, and **Elevation** permissions is set to *No.*

- Category: **Remote tasks**
- Permissions:
  - **Offer remote assistance** : Yes/No  
  
By default, the built-in **Help Desk Operator** role sets all of these permissions to **Yes**. You can use the built-in role or create custom roles to grant only the remote tasks and Remote Help app permissions that you want different groups of users to have. For more information on using Intune RBAC, see [Role-based access control](../fundamentals/role-based-access-control.md).

### Task 3: Assign user to roles

After creating the custom roles that you can use to provide different users with Remote Help permissions, proceed to assign users to those roles.

1. Sign into [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration**  > **Roles** >  and select a role that grants Remote Help app permissions.

2. Select **Assignments**  > **Assign** to open **Add Role Assignment**.

3. On the *Basics* page, enter an **Assignment name** and optional **Assignment description**, and then choose **Next**.

4. On the **Admin Groups** page, select the group that contains the user you want to give the permissions to. Choose **Next**.

5. On the **Scope (Groups)** page, choose a group containing the users/devices that a member is allowed to manage. You also can choose all users or all devices. Choose **Next** to continue.

   >[!IMPORTANT]
   >If a sharer or a sharer's device isn't in the scope of a helper, that helper cannot provide assistance.

6. On the **Review + Create** page, when you're done, choose **Create**. The new assignment is displayed in the list of assignments.

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

### Try an interactive demo

The [Remote Help]( https://regale.cloud/Microsoft/viewer/1746/remote-help/index.html#/0/0) interactive demo walks you through scenarios step-by-step with interactive annotations and navigation controls.

## Next steps

[Get support in Microsoft Intune admin center](../../get-support.md).
