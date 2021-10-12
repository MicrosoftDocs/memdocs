---
# required metadata

title: Remotely assist users that are authenticated by your organization. 
description: With the remote help app, provide remote assistance to authenticated users who also run the remote help app.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/29/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.reviewer: nehashah
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---
 
# Use remote help with Intune and Microsoft Endpoint Manager

In public preview, *remote help* is an application that works with Intune and enables your information and front-line workers to get assistance when needed over a remote connection. With this connection, your support staff can remote connect to the shared device. During the session they can view the devices display and if permitted by the shared device user, take full control. Full control enables a helper to directly make configurations or take actions on the shared device. Remote help works with both devices that have enrolled with Intune and with devices that aren't enrolled.

In this article, we'll refer to the users who provide help as *helpers*, and users that receive help as *sharers* as they share their session with the helper. Both helpers and sharers sign in to your organization to use the app. It's through your Azure Active Directory (Azure AD) that the proper trusts are established for the remote help sessions.

Remote help uses Intune role-based access controls (RBAC) to set the level of access a helper is allowed. Through RBAC, you can determine which users can provide help and the level of help they can provide.

The remote help app is available from the Microsoft Store for Windows to install on both devices enrolled with Intune devices that aren’t enrolled. The app can also be deployed through Intune to your managed devices.

## Remote help capabilities and requirements

The Remote help app supports the following capabilities:

- **Enable remote help for your tenant** – By default, Intune tenants aren't enabled for remote help. If you choose to turn on remote help, its use is enabled tenant-wide.

- **Use remote help with unenrolled devices** – Disabled by default, you can choose to allow help to devices that aren't enrolled with Intune.

- **Requires Organization login** - To use remote help, both the helper and the sharer must sign in with an Azure Active Directory (Azure AD) account from your organization. You can’t use remote help to assist users who aren’t members of your organization.

- **Compliance Warnings** - Before connecting to device, a helper will see a non-compliance warning about that device if it’s not compliant to its assigned policies. This warning doesn’t block access but provides transparency about the risk of using sensitive data like administrative credentials during the session.

  Unenrolled devices always report as non-compliant. This is because until a device enrolls with Intune it can’t receive policies from Intune and therefore is unable to establish is compliance status.

- **Role-based access control** – Admins can set RBAC rules that determine the scope of a helper’s access, like:
  - The users who can help others and the range of actions they can do while providing help, like who can run elevated privileges while helping.
  - The users that can only view a device, and which can request full control of the session while assisting others.

- **Elevation of privilege** - When needed, a helper with the correct RBAC permissions can interact with the  UAC prompt on the sharer's machine to enter credentials. For example, your Help Desk employees might enter administrative credentials to complete an action on the sharer’s device that requires administrative permissions.

- **Monitor active remote help sessions, and view details about past sessions** – In the Microsoft Endpoint Manager admin center you can view reports that include details about who helped who, on what device, and for how long. You’ll also find details about active sessions.

  For unenrolled devices, auditing and reporting about the remote help sessions is limited.

## Prerequisites

- Windows 10/11
- Devices must install the remote help app. Device users can download the app from the Microsoft Store for Windows.
  <!-- Pending app details including official name/publisher, and download or store link -->

  Intune admins can download and deploy the app to enrolled devices. For more information about app deployments, see [Install apps on Windows devices](../apps/apps-windows-10-app-deploy.md#install-apps-on-windows-10-devices).

## Configure remote help for your tenant

To configure your tenant to support remote help, review and complete the following tasks.

### Task 1 – Enable remote help

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Connectors and tokens** > **Remote help (preview)**.

2. On the **Settings** tab:
   1. Set **Enable remote help** to **Enabled** to allow use of remote help.  By default, this setting is *Enabled*.
   2. Set **Allow remote help to unenrolled devices** to **Enabled** if you want to allow this option. By default, this setting *Not allowed*.

3. Select **Save**.

### Task 2 – Configure permissions for remote help

The following Intune RBAC permissions manage use of the remote help app:

- Category: **Remote help app**
- Permissions:
  - **Take full control** – Yes/No
  - **Elevation** – Yes/No
  - **View screen** – Yes/No

By default, the built-in **Help Desk Operator** role sets all three permissions to **Yes**. You can use the built-in role or create custom roles to grant only the remote help app permissions that you want different groups of users to have. For more information on using Intune RBAC, see [Role-based access control](../fundamentals/role-based-access-control.md).

> [!IMPORTANT]  
> When a remote help session ends between a sharer and a helper that has the *Elevation* permission set to *Yes*,  both the helper and the sharer are signed out of their devices. Therefore, it is important for helpers who are granted this permission to understand the impact this action can have to a sharer. The sharer should plan to save any active work prior seeking support as any session might end early or unexpectedly, which can cause a loss of active work hasn’t been saved.  

### Task 3 – Assign user to roles

After creating the custom roles that you'll use to provide different users with remote help permissions, assign users to those roles.

1. Sign into [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration**  > **Roles** >  and select a role that grants remote help app permissions.

2. Select **Assignments**  > **Assign** to open **Add Role Assignment**.

3. On the *Basics* page, enter an **Assignment name** and optional **Assignment description**, and then choose **Next**.

4. On the **Admin Groups** page, select the group that contains the user you want to give the permissions to. Choose **Next**.

5. On the **Scope (Groups)** page, choose a group containing the users/devices that the member above will be allowed to manage. You also can choose all users, or all devices. Choose **Next** to continue.

   >[!IMPORTANT]
   >If a sharer’s device isn’t in the scope of a helper, that helper cannot provide assistance.

6. On the **Review + Create** page, when you're done, choose **Create**. The new assignment is displayed in the list of assignments.

## How to use remote help

The use of remote help depends on whether you're requesting help or providing help.

### Request help

To request help, you must reach out to your support staff to request assistance. You can reach out through a call, chat, email, and so on. While the remote help app can respond to an offer to help, it doesn’t support submitting a request for assistance from others. To aid in starting the session, be prepared to provide your username and device name on which assistance is needed. You're the sharer during the session.

> [!TIP]  
> Plan to save your active work before a remote help session to avoid an unexpected loss of work. This is because both you and the helper are signed out of your devices when a session ends, and the helper has the *Elevation* permission.

1. When assistance is ready to help, start the remote help app on the device. The app will then be ready to respond to the helper when their remote help app attempts to make a device-to-device connection.

2. After the connection is made, you and the helper see a sign-in screen. You must both sign in with your organization credentials.

3. After signing in, a company branded remote help app opens on both the helper and sharer’s devices. To establish a trusted connection:
   - The helper will see a security code that they must provide to the sharer.
   - The sharer must enter the security code before the helper can assist.

   After the code is entered, both apps display information about the other individual. The information can include usernames, user profile pictures, job title, and the verified domain. This is the same as you might see in Teams or Outlook:
   - As the sharer, your app displays the organizational details of the helper. If the helper requests full control, you can select the option to *Allow full control* or choose to *Decline the request*.
   - The helper’s app displays the organization details about you, the sharer. The helper can request *Full control* of your device or select *Screen sharing* to view your device but not control it.

4. After establishing assistance through a shared display or full control session, the helper can now assist resolving any issues on the device.

   During assistance, helpers that have the *Elevation* permission can enter local admin permissions on your shared device. *Elevation* allows the helper to run executable programs or take similar actions when you lack sufficient permissions.

5. After the issues are resolved, or at any time during the session, both the sharer or helper can end the session. To end the session, select **Leave** in the upper right corner of the remote help app.

### Provide help  

> [!TIP]  
> Plan to save your active work before a remote help session begins to avoid an unexpected loss of work. This is because both you and the sharer are signed out of your devices when a session ends, and the helper has the *Elevation* permission.

As a helper, after receiving a request from a user who wants assistance through the remote help app:

1. Sign into Microsoft Endpoint Manager admin center and go to **Devices** > **All devices** and select the device on which assistance is needed.

2. From the remote actions bar across the top of the device view, select **New remote help session**.

   As the session connects to the device, you can view details about the device, and monitor the status of the connection to it.

   After a connection is made to a device that is enrolled with Intune and that has an authenticated user signed in,  both the helper and the sharer see a sign-in screen. You must both sign in with your organization credentials. When connecting to a device without a user, only the helper sign’s in.

3. After signing in, a company branded Remote help app opens on both the helper and sharer’s devices. To establish a trusted connection:
   1. The helper will see a security code that they must provide to the sharer.
   2. The sharer must enter that security code before the helper can provide help.

   After the code is entered, both apps display information about the other individual. The information can include usernames, user profile pictures, job title, and the verified domain. This is the same information you might see in Teams or Outlook:
   1. The helper’s app displays the organization details for the sharer. As the helper you can request *Full control* of the sharer’s device or select *Screen sharing* to view their device but not control it.
   2. The sharer’s app displays the organizational details of the helper. They can select the option to *Allow full* control if you request it, or they can *Decline the request*.

4. After establishing assistance through a shared display or full control session, the helper can now assist resolving any issues on the device.

   During assistance, helpers that have the *Elevation* permission can enter local admin permissions for the shares device to run executable programs or take similar actions that require the elevated permissions.

5. After the issues are resolved, or at any time during the session, both the sharer or helper can end the session. To end the session, select **Leave** in the upper right corner of the remote help app.

## Data and privacy

Intune logs a small amount of session data to monitor the health of the remote help system. This data includes the following information:

- Start and end time of the session
- Errors arising from remote help itself, such as unexpected disconnections
- Features used inside the app such as view only, annotation, and session pause

Remote help logs session details to the Windows Event Logs on the device of both the helper and sharer. Microsoft can't access a session or view any actions or keystrokes that occur in the session.

Both helper and the sharer see details about the other, taken from their organizational profiles.

In some scenarios, the helper does require the sharer to respond to application permission prompts (User Account Control), but otherwise the helper has the same permissions as the sharer on the device.

## Monitoring and reports

You can monitor the use of remote help from within Microsoft Endpoint Manager.

1. Sign into Microsoft Endpoint Manager admin center and go to Tenant admin > Connectors and tokens > Remote help (preview).

2. On the Monitor tab, you’ll see a count of active sessions and historical data about past sessions.

3. On the Remote help sessions tab, you’ll see the records of past sessions, including:
   - The helper (Provider ID) and sharer (Recipient ID) of each session.
   - The device that received assistance.
   - The start and end time of the Remote Assistance session.

## Next steps

[Get support in Microsoft Endpoint Manager admin center](../../get-support.md)
