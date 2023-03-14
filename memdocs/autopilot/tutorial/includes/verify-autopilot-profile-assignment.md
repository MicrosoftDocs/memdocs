---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 02/23/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the azure-ad-join-autopilot-profile.md and the hybrid-azure-ad-join-autopilot-profile.md articles. Headings are driven by article context. -->

Before deploying a device, ensure that an Autopilot profile has been assigned to a device group that the device is a member of. Autopilot profile assignment to a device can take some time after the Autopilot profile has been assigned to the device group or after the device has been added to the device group. To verify that the profile has been assigned to a device, follow these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, select **Windows enrollment**.

1. Under **Windows Autopilot Deployment Program**, select **Devices**.

1. In the **Windows Autopilot devices** screen that opens:

   1. Find the desired device that Autopilot deployment profile assignment status needs to be checked.

   2. Once the device is located, its current status will be listed under the **Profile status** column. The status will be one of the following values:

       - **Not assigned**: The device hasn't been assigned an Autopilot deployment profile.
       - **Assigning**: The device is being assigned an Autopilot deployment profile.
       - **Assigned**: The device has been assigned an Autopilot deployment profile.

        Before starting the Autopilot deployment process on a device, make sure that its **Profile status** status is **Assigned**.

> [!NOTE]
>
> Intune will periodically check for new devices in the assigned device groups, and then begin the process of assigning profiles to those devices. Due to several different factors involved in the process of Autopilot profile assignment, an estimated time for the assignment can vary from scenario to scenario. These factors can include AAD groups, membership rules, hash of a device, Intune and Autopilot service, and internet connection. The assignment time will vary depending on all the factors and variables involved in a specific scenario.