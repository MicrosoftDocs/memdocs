---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/28/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning\azure-ad-join-autopilot-profile.md
pre-provisioning/hybrid-azure-ad-join-autopilot-profile.md
self-deploying\self-deploying-autopilot-profile.md
user-driven\azure-ad-join-autopilot-profile.md
user-driven\hybrid-azure-ad-join-autopilot-profile.md

Headings are driven by article context. -->

Before deploying a device, ensure that an Autopilot profile is assigned to a device group that the device is a member of. Autopilot profile assignment to a device can take some time after the Autopilot profile is assigned to the device group or after the device is added to the device group. To verify that the profile is assigned to a device, follow these steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Devices**.

1. In the **Windows Autopilot devices** screen that opens:

   1. Find the desired device that Autopilot deployment profile assignment status needs to be checked.

   1. Once the device is located, its current status is listed under the **Profile status** column. The status has one of the following values:

       - **Not assigned**: An Autopilot deployment profile isn't assigned to the device.

       - **Assigning**: An Autopilot deployment profile is being assigned to the device.

       - **Assigned**: An Autopilot deployment profile is assigned to the device.

       - **Fix pending**:  When a hardware change occurs on a device, this status displays while Intune tries to register the new hardware. When the link for the **Fix pending** status is selected, the following message appears:

          **We've detected a hardware change on this device. We're trying to automatically register the new hardware. You don't need to do anything now; the status will be updated at the next check in with the result.**

          If Intune is able to successfully register the new hardware, Intune updates the profile status when the device next checks into Intune. For more information on the **Fix pending** status, see the following articles:

           - [Why is the Windows Autopilot profile not applied after a hardware change occurred on a device?](../../troubleshooting-faq.yml#why-is-the-windows-autopilot-profile-not-applied-after-a-hardware-change-occurred-on-a-device-).
           - [Return of key functionality for Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/return-of-key-functionality-for-windows-autopilot-sign-in-and/ba-p/3583130).
           - [Windows Autopilot motherboard replacement scenario guidance](../../autopilot-motherboard-replacement.md)

       - **Attention required**: If Intune is unable to register the new hardware after a hardware change occurs on a device, the device can't receive the Autopilot profile until the device is reset and the device re-registers. For more information on this status and how to deregister/re-register a device, see the following articles:

         - [Why is the Windows Autopilot profile not applied after a hardware change occurred on a device?](../../troubleshooting-faq.yml#why-is-the-windows-autopilot-profile-not-applied-after-a-hardware-change-occurred-on-a-device-).
         - [Return of key functionality for Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/return-of-key-functionality-for-windows-autopilot-sign-in-and/ba-p/3583130).
         - [Windows Autopilot motherboard replacement scenario guidance](../../autopilot-motherboard-replacement.md)
         - [Deregister a device](../../registration-overview.md#deregister-a-device)

        Before starting the Autopilot deployment process on a device, make sure that in the **Windows Autopilot devices** page:

        - The device's **Profile status** status is **Assigned**.
        - In the properties of the device, **Date assigned** has a value.
        - In the properties of the device, **Assigned profile** displays the expected Autopilot profile.

> [!NOTE]
>
> Intune periodically checks for new devices in the assigned device groups, and then begins the process of assigning profiles to those devices. Due to several different factors involved in the process of Autopilot profile assignment, an estimated time for the assignment can vary from scenario to scenario. These factors can include Microsoft Entra groups, membership rules, hash of a device, Intune and Autopilot services, and internet connection. The assignment time varies depending on all the factors and variables involved in a specific scenario.
