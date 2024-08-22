---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/19/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-technician-flow.md
pre-provisioning/hybrid-azure-ad-join-technician-flow.md

Headings are driven by article context. -->

Once all of the configurations for Windows Autopilot for pre-provisioned deployment are completed in Intune and in Microsoft Entra ID, the next step is to start the Windows Autopilot deployment process on the device. For Windows Autopilot for pre-provisioned deployment, the Autopilot process is split into two different phases that run at two different points in time by two different sets of individuals:

- The first phase is known as the **technician flow** and is normally run by the IT department, OEM, or reseller.
- The second phase is known as the **user flow** and is normally run by the end-user.

To start the technician flow, select a device that is part of the device group created in the previous **Create a device group** step, and then follow these steps:

[!INCLUDE [Network connectivity](../includes/network-connectivity.md)]

4. At the Microsoft Entra sign-in page, **DON'T** sign in or select the **Next**/**Sign in** button. Instead, press the <kbd>WIN</kbd> key on the keyboard five times. Pressing the <kbd>WIN</kbd> key five times should display a **What would you like to do?** options screen instead.

5. From the **What would you like to do?** options screen:

   - For Windows 10, select the **Windows Autopilot provisioning** option, and then select **Continue**.
   - For Windows 11, select the **Pre-provision with Windows Autopilot** option, and then select **Next**.

6. In the **Windows Autopilot Configuration** screen (Windows 10) or the **Pre-provision with Windows Autopilot** screen (Windows 11), it displays the following information about the deployment:

   - The name of the organization for the device.

   - The name of the Autopilot deployment profile assigned to the device during the **Create and assign Autopilot profile** step.

   - The user assigned to the device if a user was assigned to the device in the **Assign Autopilot device to a user (optional)** step (if applicable).

   - A QR code containing a unique identifier for the device. This code can be used to look up the device in Intune to perform actions such as verifying configurations, make any necessary changes, etc.

7. Validate that the information in the **Windows Autopilot Configuration** screen is correct. Once all information is confirmed as correct, select **Provision** (Windows 10) or **Next** (Windows 11) to begin the provisioning process.

8. The device might reboot, followed by the Enrollment Status Page (ESP) appearing. The Enrollment Status Page (ESP) displays progress during the provisioning process across three phases:

   - **Device preparation** (Device ESP)
   - **Device setup** (Device ESP)
   - **Account setup** (User ESP)

   The first two phases of **Device preparation** and **Device setup** are part of the Device ESP while the final phase of **Account setup** is part of the User ESP.

   For technician flow of the Windows Autopilot for pre-provisioned deployment, only the first two Device ESP phases of **Device preparation** and **Device setup** run. The last User ESP phase of **Account setup** will run during the next step of **User flow**.

9. Once **Device setup** and the device ESP process completes, a status screen is displayed showing whether the provisioning process either succeeded of failed:

    - If the pre-provisioning process completes successfully, a success status screen appears with information about the deployment. Information presented includes the previously presented information of organization name, Autopilot deployment profile name, QR code (Windows 10 only), and if applicable, assigned user. The elapsed time of the provisioning process is also provided.

      Select **Reseal** to shut down the device. At that point, the device can be delivered to the end-user.

      > [!IMPORTANT]
      >
      > Outside of testing scenarios, if the intention is to deliver the device to an end-user, **DON'T** turn the device back on at this point. Instead, deliver the device to the end-user where they perform the last step of **User flow**.

    - If the pre-provisioning process fails, an error status screen appears with information about why the deployment failed including an error. The error screen also displays the previously presented information of organization name, Autopilot deployment profile name, QR code (Windows 10 only), and if applicable, assigned user. The elapsed time of the provisioning process is also provided.

      From this screen, diagnostic logs can be gathered from the device to troubleshoot the issue by using the following methods:

      - In Windows 10, select **View diagnostics**.

      - In Windows 11, enter the keystroke <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>D</kbd> and then select **Export Logs**.

      If the issue can be easily fixed, for example resolving network connectivity, then select the **Retry** button to retry provisioning the device. Otherwise if the issue can't be immediately fixed or can't be fixed without a reset, then select the **Reset** button so that the process starts over again.
