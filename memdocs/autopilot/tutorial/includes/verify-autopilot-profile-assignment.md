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

       - **Fix pending**:  When a hardware change occurs on a device, this status will display while Intune tries to register the new hardware. When selecting the link for the **Fix pending** status, the following message appears:

          **We've detected a hardware change on this device. We're trying to automatically register the new hardware. You don't need to do anything now; the status will be updated at the next check in with the result.**

          If Intune is able to successfully register the new hardware, Intune updates the profile status when the device next checks into Intune. For more information on this status, see the following articles:

           - [Autopilot profile not applied after reimaging to an older OS version](../../troubleshoot-device-enrollment.md#autopilot-profile-not-applied-after-reimaging-to-an-older-os-version).
           - [Return of key functionality for Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/return-of-key-functionality-for-windows-autopilot-sign-in-and/ba-p/3583130).
           - [Windows Autopilot motherboard replacement scenario guidance](../../autopilot-mbr.md)

       - **Attention required**: After a hardware change occurs on a device, if Intune is unable to register the new hardware, the device can't receive the Autopilot profile until the device is reset and the device re-registers. For more information on this status and how to deregister/re-register a device, see the following articles:

         - [Autopilot profile not applied after reimaging to an older OS version](../../troubleshoot-device-enrollment.md#autopilot-profile-not-applied-after-reimaging-to-an-older-os-version).
         - [Return of key functionality for Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/return-of-key-functionality-for-windows-autopilot-sign-in-and/ba-p/3583130).
         - [Windows Autopilot motherboard replacement scenario guidance](../../autopilot-mbr.md)
         - [Deregister a device](../../registration-overview.md#deregister-a-device)

        Before starting the Autopilot deployment process on a device, make sure that in the **Windows Autopilot devices** page:

        - The device's **Profile status** status is **Assigned**.
        - In the properties of the device, **Date assigned** has a value.
        - In the properties of the device, **Assigned profile** displays the expected Autopilot profile.

> [!NOTE]
>
> Intune periodically checks for new devices in the assigned device groups, and then begins the process of assigning profiles to those devices. Due to several different factors involved in the process of Autopilot profile assignment, an estimated time for the assignment can vary from scenario to scenario. These factors can include Azure AD groups, membership rules, hash of a device, Intune and Autopilot service, and internet connection. The assignment time varies depending on all the factors and variables involved in a specific scenario.
