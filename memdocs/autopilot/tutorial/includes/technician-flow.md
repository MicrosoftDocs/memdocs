---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 04/07/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-technician-flow.md
pre-provisioning/hybrid-azure-ad-join-technician-flow.md

Headings are driven by article context. -->

Once all of the configurations for Windows Autopilot for pre-provisioned deployment have been completed on the Intune and Azure AD side, the next step is to start the Autopilot process. This step is known as the technician flow.

[!INCLUDE [Assignment tip](../includes/assignment-tip.md)]

To start the technician flow, follow these steps:

1. Select a device that is part of the device group created in the previous **Create a device group** step.

1. If a wired network connection is available, connect the device to the wired network connection.

1. Power on the device.

1. Once the device boots up, one of two things occurs depending on the state of network connectivity:

   - If the device is connected to a wired network and has network connectivity, the device may reboot one time followed by the Azure AD sign-in page appearing.

   - If the device isn't connected to a wired network or if it doesn't have network connectivity, it prompts to connect to a network. Connectivity to the Internet is required during the technician flow phase:

     1. OOBE (out of box experience) begins and a screen asking for a country or region appears. Select the appropriate country or region, and then select **Yes**.

     1. The keyboard screen appears to select a keyboard layout. Select the appropriate keyboard layout, and then select **Yes**.

     1. An additional keyboard layouts screen appears. If needed, select additional keyboard layouts via **Add layout**, or select **Skip** if no additional keyboard layouts are needed.

         > [!NOTE]
         >
         > When there's no network connectivity, the country/region and keyboard screens appear even if these screens have been set to hidden in the Autopilot profile. Because there was no network connectivity at this point, the device hasn't downloaded the Autopilot profile to know that these screens should have been hidden.

     1. The **Let's connect you to a network** screen appears. At this screen, either plug the device into a wired network (if available), or select and connect to a wireless Wi-Fi network.

     1. Once network connectivity is established, the **Next** button should become available. Select **Next**.

     1. At this point, the device may reboot. After it reboots, the Azure AD sign-in page should appear.

    > [!NOTE]
    >
    > Additional screens such as License Terms, Privacy, Language, and Keyboard may appear before the Azure AD sign-in page depending on how the Autopilot profile was configured at the **Create and assign Autopilot profile** step.

1. At the Azure AD sign-in page, **DON'T** sign in or select **Next**/**Sign in**. Instead, press the <kbd>WIN</kbd> key on the keyboard five times. Pressing the <kbd>WIN</kbd> key five times should display a **What would you like to do?** options screen instead.

1. From the **What would you like to do?** options screen:

   - For Windows 10, select the **Windows Autopilot provisioning** option, and then select **Continue**.
   - For Windows 11, select the **Pre-provision with Windows Autopilot** option, and then select **Next**.

1. In the **Windows Autopilot Configuration** screen (Windows 10) or the **Pre-provision with Windows Autopilot** screen (Windows 11), it displays the following information about the deployment:

   - The name of the organization for the device.

   - The name of the Autopilot deployment profile assigned to the device during the **Create and assign Autopilot profile** step.

   - The user assigned to the device if a user was assigned to the device in the **Assign Autopilot device to a user (optional)** step (if applicable).

   - A QR code containing a unique identifier for the device. This code can be used to look up the device in Intune to perform actions such as verifying configurations, make any necessary changes, etc.

      > [!NOTE]
      >
      > The QR codes can be scanned using a companion app. The app also configures the device to specify who it belongs to. The Autopilot team has published to GitHub an [open-source sample of the companion app](https://github.com/Microsoft/WindowsAutopilotCompanion) that integrates with Intune using the Graph API.

1. Validate that the information in the **Windows Autopilot Configuration** screen is correct. Once all information has been confirmed as correct, select **Provision** (Windows 10) or **Next** (Windows 11) to begin the provisioning process.

1. The device may reboot, followed by the Enrollment Status Page (ESP) appearing. The Enrollment Status Page (ESP) displays progress during the provisioning process across three phases:

   - **Device preparation** (Device ESP)
   - **Device setup** (Device ESP)
   - **Account setup** (User ESP)

   The first two phases of **Device preparation** and **Device setup** are part of the Device ESP while the final phase of **Account setup** is part of the User ESP.

   For technician flow of the Windows Autopilot for pre-provisioned deployment, only the first two Device ESP phases of **Device preparation** and **Device setup** run. The last User ESP phase of **Account setup** will run during the next step of **User flow**.

   > [!NOTE]
   >
   > To view and hide detailed progress information in the ESP during the provisioning process:
   >
   > - Windows 10: To show details, next to the appropriate phase select **Show details**. To hide the details, next to the appropriate phase select **Hide details**.
   > - Windows 11: To show details, next to the appropriate phase select **∨**. To hide the details, next to the appropriate phase select **∧**.

1. Once **Device setup** and the device ESP process completes, a status screen is displayed showing whether the provisioning process either succeeded of failed:

    - If the pre-provisioning process completes successfully, a success status screen appears with information about the deployment. Information presented includes the previously presented information of organization name, Autopilot deployment profile name, QR code (Windows 10 only), and if applicable, assigned user. The elapsed time of the provisioning process is also provided.

      Select **Reseal** to shut down the device. At that point, the device can be delivered to the end-user.

      > [!IMPORTANT]
      >
      > Outside of testing scenarios, if the intention is to deliver the device to an end-user, **DON'T** turn the device back on at this point. Instead, deliver the device to the end-user where they perform the last step of **User flow**.

      > [!NOTE]
      >
      > The technician flow inherits behavior from [self-deploying mode](../self-deploying/self-deploying-workflow.md). Self-deploying mode uses the Enrollment Status Page (ESP) to hold the device in a provisioning state and prevent the user from proceeding to the desktop after enrollment but before applications and configurations are done applying. If the Enrollment Status Page (ESP) is disabled, the **Reseal** button may appear before applications and configurations are done applying. Disabling the ESP may advertently allow proceeding to the user flow before technician flow provisioning is complete. The success status screen validates that enrollment was successful, not that the technician flow is necessarily complete. For this reason, it's recommended not to disable the Enrollment Status Page (ESP). Instead enable the Enrollment Status Page (ESP) as suggested in the **Configure and assign Autopilot Enrollment Status Page (ESP)** step.

    - If the pre-provisioning process fails, an error status screen appears with information about why the deployment failed including an error. The error screen also displays the previously presented information of organization name, Autopilot deployment profile name, QR code (Windows 10 only), and if applicable, assigned user. The elapsed time of the provisioning process is also provided.

      From this screen, diagnostic logs can be gathered from the device to troubleshoot the issue by using the following methods:

    - In Windows 10, select **View diagnostics**.

    - In Windows 11, press the <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>D</kbd> keys and then select **Export Logs**.

      If the issue can be easily fixed, for example resolving network connectivity, then select the **Retry** button to retry provisioning the device. Otherwise if the issue can't be immediately fixed or can't be fixed without a reset, then select the **Reset** button so that the process starts over again.
