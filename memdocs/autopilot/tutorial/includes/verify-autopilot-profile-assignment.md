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

Before deploying a device, ensure that an Autopilot profiles has been assigned to it by checking under **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program** where you should see the profile status change from "Unassigned" to "Assigning" and finally to "Assigned."

> [!NOTE]
> Intune will periodically check for new devices in the assigned groups, and then begin the process of assigning profiles to those devices. Due to several different factors involved in the process of Autopilot profile assignment, an estimated time for the assignment can vary from scenario to scenario. These factors can include AAD groups, membership rules, hash of a device, Intune and Autopilot service, and internet connection. The assignment time will vary depending on all the factors and variables involved in a specific scenario.
