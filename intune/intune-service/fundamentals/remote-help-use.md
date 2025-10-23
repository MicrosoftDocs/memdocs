---
title: Using Remote Help on Windows to Assist Authenticated Users 
description: Use the Remote Help app to provide remote assistance to authenticated users who also run the Remote Help app, and to troubleshoot for frontline workers (FLW).
author: lenewsad
ms.author: lanewsad
ms.date: 10/16/2025
ms.topic: how-to
ms.localizationpriority: high
ms.reviewer: Karawang
ms.subservice: suite
ms.collection:
- M365-identity-device-management
- highpri
- highseo
---

# Using Remote Help with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

[!INCLUDE [remote-help-overview](includes/remote-help-overview.md)]

The use of Remote Help depends on whether you're requesting help or providing help. In this article, we cover both scenarios.  

## Get help

To get help, you must reach out to your support staff to request assistance. You can reach out by way of call, chat, or email, and you're the sharer during the session.  

### [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

> [!TIP]
> The Remote Help app needs to be installed on your device. If Remote Help isn't installed, you can install Remote Help yourself by following the download instructions in the [Install and update Remote Help](remote-help-deploy.md#install-remote-help-apps) section.  

**Starting the session:**  

1. The helper can initiate a session or you can manually start the Remote Help app and enter a session code provided by the helper.
   > [!NOTE]
   > If the helper initiates the session from Intune, a notification is sent to your device. Select **Open Remote Help** in the notification to open the Remote Help app and continue. If your computer is in *do not disturb* mode, you might not see the notification. In this case, manually open the Remote Help app to continue or check the notifications center.
1. Verify the helper's identity by viewing their information, including their full name, job title, company, profile picture, and verified domain. Then choose to **Allow screen sharing or full control** or **Decline the request**.  
1. The session is established, and the helper can then help in resolving any issues on the device.

**During the session:**

- You can chat with the helper using the chat window in the Remote Help app.
- Helpers that have the elevation permission can enter local admin permissions on your shared device. *Elevation* allows the helper to run executable programs or take similar actions when you lack sufficient permissions.
  > [!IMPORTANT]
  > During a Remote Help session, when a helper has the elevation permission, the helper can perform elevated actions on the sharer's device. When the sharer ends the Remote Help session, a dialog box warns them that if they continue, they're logged off. If the helper ends the session, the sharer isn't logged off.
  
- The helper can request to move from screen sharing to full control if the session started with screen sharing only. You can choose to **Allow full control** or to **Decline the request**.

**When the issues are resolved or you're ready to end the session:**

- Both the sharer and helper can end the session. To end the session, select **Leave** in the upper-right corner of the Remote Help app. 

### [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

This section covers the steps for using the macOS native app to request Remote Help.

> [!TIP]
> If you just want to share your screen and don't need the helper to be able to control your screen or you can't install the native app, you can use the web app.

To request help, you must reach out to your support staff to request assistance, and enter a code they provide to start the session.

**Starting the session:**

1. Open the Remote Help app on the device by going to **Finder** > **Applications** > **Microsoft Remote Help**.  
1. When opening Remote Help for the first time, you must allow Remote Help access to control and share your screen. Select each of the required permissions to open Settings and ensure the permission is allowed for Microsoft Remote Help.
   
   1. **Accessibility** (also available to set in **Settings** > **Privacy & Security** > **Accessibility**).
      
   1. **Screen and System Audio Recording**  (also available to set in **Settings** > **Privacy & Security** > **Screen and System Audio Recording**).
      
1. If prompted, sign in with your work credentials to authenticate to your organization.  
1. Enter the 8-digit security code provided by the helper. After entering the code, select **Share screen** to continue.  
1. When the session connection begins, a trust screen is displayed with the helper's information including their full name, job title, company, profile picture, and verified domain. At this time, the helper requests a session with full control of your device or view only-screen sharing. You can either choose to **Allow** or to **Decline** the request.  
1. You might see a prompt to allow `remotehelp.microsoft.com` to use your microphone. Select **Don't Allow** as this permission isn't needed for screen sharing.
   
     :::image type="content" source="media/remote-help/remote-help-microphone-permission.png" alt-text="An example of the microphone permission prompt highlighting the Don't Allow option":::
   
1. Select **Share screen** to continue. You might see a prompt to allow `remotehelp.microsoft.com` share your screen. Select **Allow** to continue.
1. macOS shows a menu with one of two options:  
   - **Green camera icon**: Choose **Screen**, and then move your mouse to select the screen share.

     :::image type="content" source="media/remote-help/remote-help-screen-share.png" alt-text="A screenshot of the macOS screen  sharing dialog to allow screen sharing for Microsoft Remote Help":::
   - **Yellow microphone icon** (if you selected to allow the microphone permission): Select the microphone icon. Select the **grey icon**, and then select **Screen**. Move your cursor to the screen you want to share and select **Share this screen**.  

     :::image type="content" source="media/remote-help/remote-help-screen-share-microphone.png" alt-text="A screenshot of the macOS microphone sharing dialog to allow screen sharing for Microsoft Remote Help":::

1. After the session is established, the helper can help resolve any issues on the device.

**During the session:**

- You can chat with the helper using the chat window in the Remote Help app.

**When the issues are resolved or you're ready to end the session:**

- Both the sharer and helper can end the session. To end the session, select **Leave** in the Remote Help app.

> [!NOTE]
> If Remote Help wasn't installed by your administrator, you can install Remote Help yourself by following the download instructions in the [Install Remote Help apps](remote-help-deploy.md#install-remote-help-apps) section.

### [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

**Starting the session:**
On your device, you see a prompt showing a request to grant screen share or control of the device with the helpers information, including their full name and company.
   
   1. If starting an attended screen sharing or full control session, you must select **Accept** to allow the session to begin. If you don't accept within 5 minutes, the session times out.
   
   1. If starting an unattended control session, the session will begin automatically after 30 seconds if there's no response.  

**During the session:**

- During an attended screen sharing or full control session, the device displays a floating **End Session** button. This button can be repositioned on the screen. Tap the button to end the session from your device.
- During an unattended control session, the screen of the device is blocked due to security and privacy reasons, and you are notified if you interact with it. If you interact with the blocked screen, you receive a notification that a helper connected. When the notification is shown, you and the helper won't be able to take any action for 30 seconds. You won't be able to end the session from your device until the helper ends the session.

### [:::image type="icon" source="../media/icons/webapp.svg"::: **Web App**](#tab/webapp)

During a session, there are two roles: a helper and a sharer. The helper obtains the security code, and then provides it to the sharer. After the session is established, the helper can view the sharer's screen.

**Starting the session:**

1. Go to https://aka.ms/rh in a browser and sign in with their organization's credentials.
1. Enter the code provided by the helper, and review and accept the prompts.

Remote Help displays a warning if the sharer's device isn't enrolled in Microsoft Intune. This warning doesn't block access but provides transparency about the risk of using sensitive data like administrative credentials during the session.

---

## Provide help

To provide help, you must reach out to the user who needs assistance. You can reach out by phone, chat, or email, and you're the helper during the session.

### [**Windows from Windows native app**](#tab/windowsnative)

As a helper, after receiving a request from a user who wants assistance by using the Remote Help app:

1. Launch a session on the remote device from within the Microsoft Intune admin center:
 
   1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > **All devices** and select the device on which assistance is needed.

   2. From the remote actions bar across the top of the device view, select **New remote assistance session** and select **Remote Help**, and then **Continue**.

     > [!NOTE]
     > If you're launching the session from Intune, sign in to the Remote Help app with the same credentials for a successful
     > connection.

1. A notification is sent to the sharer's device, and you see an update that the notification was successfully sent. Select **Launch Remote Help** to join the session.

   1. If the notification is sent but not received by the user, you can resend the notification by selecting **Retry**.

   2. If the sharer's device isn't online or not connected to the internet, an error message is  displayed.

   3. If the device that you're trying to connect to is noncompliant, a warning banner is displayed.

1. When Remote Help opens, you must sign in to authenticate to your organization.

1. After the sharer opens the Remote Help app through the notification, as the helper you see information about the sharer, including their full name, job title, company, profile picture, and verified domain. The sharer sees similar information about you.

   At this time, you can request a session with full control of the sharer's device or choose only screen sharing. If you request full control, the sharer can choose to **Allow full control** or to **Decline the request**.

1. After establishing that the session uses a shared display or full control, Remote Help displays a *compliance warning* if the sharer's device fails to meet the conditions of its assigned compliance policies.

   During assistance, helpers that have the elevation permission can enter local admin permissions on your shared device. *Elevation* allows the helper to run executable programs or take similar actions when you lack sufficient permissions.

   > [!NOTE]
   > When the `EnableSecureCredentialPrompting` policy is enabled, it blocks the elevation process during Remote Help sessions. To allow elevation, disable this policy.  For more information, see [Enable secure credential prompting](/windows/client-management/mdm/policy-csp-admx-credui#enablesecurecredentialprompting).   

1. After the issues are resolved, or at any time during the session, both the sharer and helper can end the session. To end the session, select **Leave** in the upper right corner of the Remote Help app. If a helper performs elevated actions on a user's device and the sharer ends the session, at the end of the session the sharer is automatically signed out.

#### Provide help on an AVD

If you're trying to help an Azure Virtual Desktop (AVD) that could have multiple users on the device, you must follow the process described in this section to give help:

1. Locate the Remote Help app on your device and manually start it. After the Remote Help app opens, you need to sign in to authenticate your organization.

1. After signing into the app, under **Give help** select **Get a security code**. Remote Help generates a security code that you need to share with the person who has requested assistance active on the AVD. The sharer enters the code in their instance of the Remote Help app to establish a connection to your Remote Help instance.

>[!NOTE]
> If you initiate the Remote Help request from Intune, then the notification is delivered to all active users on the Azure Virtual Desktop.

>[!NOTE]
> The restart option isn't available for helpdesk agents remotely helping AVD.

### [:::image type="icon" source="../media/icons/intune.svg"::: **macOS from the Intune admin center**](#tab/macosintune)

1. Navigate to the device you're trying to help from the Microsoft Intune admin center:

   1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > **All devices**. Select the macOS device on which assistance is needed.

   1. From the remote action bar across the top of the device view, select **New remote assistance session** and select **Remote Help**. 

   1. Select **Continue**.  

1. Copy and share the eight-digit session code with the sharer that you're trying to help. Then select **Start** to launch a new Remote Help session.

1. When Remote Help opens in a new tab for the first time, you must sign in to authenticate to your organization.

1. After the sharer navigates to the Remote Help session, as the helper you'll see information about the sharer, including their full name, job title, company, profile picture, and verified domain. The sharer sees similar information about you.

1. At this time, you can request a session with full control of the sharer's device or choose only screen sharing. The sharer can choose to **Allow** or to **Decline** the request.

### Enrolled macOS device

1. The helper navigates to the device to connect to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  

  1. Sign in to the Microsoft Intune admin center and go to **Devices** > **All devices** and select the macOS device on which assistance is needed.

  1. From the remote action bar across the top of the device view, select **New remote assistance session** and select **Remote Help**. 
  
  1. Select **Continue**.  

1. To invite a user to a session, provide the user with the security code.

   - If the sharer is also using the web app:
     - Copy and share the session link with the user (the link is limited to View Only) (For example: https://aka.ms/rh?passcode=4060r0gx). The link opens in the user's web browser. You can only request a screen sharing session of the device.

   - If the sharer is using the macOS application:
     - Share the eight-character security code with the user. You can request a screen sharing session. View only and full control are supported.  

1. After the sharer either selects the link or enters the code into Remote Help for macOS, they're joined to the session. If the user isn't already signed in to the app, they're prompted to do so.

1. At the start of the session, the trust screen is displayed, which shows the other person's full name, job title, company, profile picture, and verified domain.

   - Helpers can see information about the sharer.

   - The sharer can see information about the helper.

1. The sharer can choose to **Allow** or to **Decline** the request after viewing the trust screen.

1. If the sharer's device isn't compliant with your organization's policies, Remote Help displays a compliance warning that encourages the helper to be cautious.  

#### macOS unenrolled device  

If the device that you're trying to help isn't enrolled in Microsoft Intune, follow the process described in this section to provide help.  

1. The helper navigates to https://aka.ms/rhh in their web browser, and then signs in to authenticate with their organization.

1. After authenticating, a security code is shown.  

1. Copy and share the eight-digit security code with the person to be helped.

1. The sharer then goes to https://aka.ms/rh and logs in with their organization's credentials.

1. After the sharer enters the code, and both users accept the prompts, the sessions begin.

Remote Help displays a warning if the sharer's device isn't enrolled in Microsoft Intune. This warning doesn't block access but provides transparency about the risk of using sensitive data, like administrative credentials, during the session.

### [:::image type="icon" source="../media/icons/intune.svg"::: **Android from Intune admin center**](#tab/androidadmin)

1. Navigate to the device you're trying to help from the Microsoft Intune admin center:

   a. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > **All devices**. Select the Android device on which assistance is needed.

   b. From the remote action bar across the top of the device view, select **New remote assistance session**. Select **Remote Help**, and then select **Continue**.

   c. Select the session type from the options for which you have permission: screen sharing, full control, unattended control. Then select **Launch Remote Help**.

1. On the device, the user sees a prompt showing a request to grant screen share or control of the device.

    a. If starting an attended screen sharing or full control session, the user must select **Accept** to allow the session to begin. If the user doesn't accept within five minutes, the session times out.

    b. If starting an unattended control session, the session begins automatically after 30 seconds if there's no response from the user.  

1. When the session is ongoing:   

    a. During an attended screen sharing or full control session, the sharer device displays a floating **End Session** button. You can reposition this button on the screen. Tap the button to end the session from the sharer device.

    b. During an attended full control session, use the buttons on the menu bar, keyboard, or mouse input to interact with the sharer device. You can also long-press on the Power button in the menu bar to simulate a long press. For example, to open the power options menu on some devices.

    c. During an unattended control session, the screen of the device you're connected to is blocked due to security and privacy reasons, and the user is notified if they interact with it. If the user interacts with the blocked screen, they'll receive a notification letting them know that you're currently accessing the device. When the notification is shown, you and the end user won't be able to take any action for 30 seconds when this screen will close.

      > [!TIP]
      > We recommend limiting your activities to nonsensitive operations during an unattended control session, even with the screen of the device you're connected to blocked to the end user.  

1. At the end of the session, select **Leave** to end the session from the admin console.

> [!NOTE]
> On Android 13 devices, the device unlock UI (the PIN entry pad, or the pattern dot grid) can't be shown remotely. To unlock the device, you can still use keyboard input to enter a passcode. Android added this feature as a security measure to protect the end user from a passcode or unlock pattern being captured if the device is unlocked while screen sharing.  

### [:::image type="icon" source="../media/icons/webapp.svg"::: **Windows or macOS from the web app**](#tab/helperwebapp)

1. Sign in to <a href="https://aka.ms/rhh" target="_blank"><u>https://aka.ms/rhh</u></a>.
1. Copy and share the eight-digit session code with the sharer that you're trying to help.
1. After the sharer enters the session code, as the helper you'll see information about the sharer, including their full name, job title, company, profile picture, and verified domain. The sharer sees similar information about you.
1. At this time, you can request a session with full control of the sharer's device or choose only screen sharing. The sharer can choose to **Allow** or to **Decline** the request.

---

> [!NOTE]
> - Remote Help displays a compliance warning if the sharer's device fails to meet the conditions of its assigned compliance policies.
> - If the tenant is configured to allow Remote Help on unenrolled devices, you receive a warning when connecting to unenrolled devices. This warning doesn't block access but provides transparency about the risk of using sensitive data, like administrative credentials, during the session.

---

## Next steps

[Get support in the Microsoft Intune admin center.](../../get-support.md)
