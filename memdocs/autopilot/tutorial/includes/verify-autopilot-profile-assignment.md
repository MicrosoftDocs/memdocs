---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 04/24/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-autopilot-profile.md
pre-provisioning/hybrid-azure-ad-join-autopilot-profile.md
self-deploying/self-deploying-autopilot-profile.md
user-driven/azure-ad-join-autopilot-profile.md
user-driven/hybrid-azure-ad-join-autopilot-profile.md


Headings are driven by article context. -->

Before deploying a device, ensure that an Autopilot profile has been assigned to a device group that the device is a member of. Autopilot profile assignment to a device can take some time after the Autopilot profile has been assigned to the device group or after the device has been added to the device group. To verify that the profile has been assigned to a device, follow these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices** in the left pane.

3. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

4. In the **Windows | Windows devices** screen, select **Windows enrollment**.

5. Under **Windows Autopilot Deployment Program**, select **Devices**.

6. In the **Windows Autopilot devices** screen that opens:

   1. Find the desired device that Autopilot deployment profile assignment status needs to be checked.

   2. Once the device is located, its current status is listed under the **Profile status** column. The status has one of the following values:

       - **Not assigned**: The device hasn't been assigned an Autopilot deployment profile.
       - **Assigning**: The device is being assigned an Autopilot deployment profile.
       - **Assigned**: The device has been assigned an Autopilot deployment profile.
       - **Fix pending**:  Intune tries to register the new hardware. If successful, Intune updates the profile status at the next check-in. For more information on this status, see the following articles:
         - [Autopilot profile not applied after reimaging to an older OS version](../../troubleshoot-device-enrollment.md#autopilot-profile-not-applied-after-reimaging-to-an-older-os-version).
         - [Hardware change detection](/mem/intune/enrollment/tutorial-use-autopilot-enroll-devices#hardware-change-detection).
         - [Return of key functionality for Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/return-of-key-functionality-for-windows-autopilot-sign-in-and/ba-p/3583130).
       - **Attention required**: The device can't receive the Autopilot profile until you reset and re-register the device. For more information on this status, see the following articles:
         - [Hardware change detection](/mem/intune/enrollment/tutorial-use-autopilot-enroll-devices#hardware-change-detection).
         - [Return of key functionality for Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/return-of-key-functionality-for-windows-autopilot-sign-in-and/ba-p/3583130).

        Before starting the Autopilot deployment process on a device, make sure that in the **Windows Autopilot devices** page:

        - The device's **Profile status** status is **Assigned**.
        - In the properties of the device, **Date assigned** has a value.

> [!NOTE]
>
> Intune periodically checks for new devices in the assigned device groups, and then begin the process of assigning profiles to those devices. Due to several different factors involved in the process of Autopilot profile assignment, an estimated time for the assignment can vary from scenario to scenario. These factors can include Azure AD groups, membership rules, hash of a device, Intune and Autopilot service, and internet connection. The assignment time varies depending on all the factors and variables involved in a specific scenario.
