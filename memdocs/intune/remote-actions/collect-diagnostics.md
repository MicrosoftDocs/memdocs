---
# required metadata

title: Collect diagnostics from a Windows device
titleSuffix: Microsoft Intune
description: Learn how to collect diagnostics from a Windows device.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/26/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jlynn
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Collect diagnostics from a Windows device

The **Collect diagnostics** remote action lets you collect and download Windows device logs without interrupting the user. Only non-user locations and file types can be accessed, so no personal information is collected.

The diagnostic collection is stored for 28 days and then deleted. Each device can have up to 10 collections stored at one time.

## Requirements

The **Collect diagnostics** remote action is supported for:
- Windows 10 version 1909 and later.
- Microsoft HoloLens 2 2004 and later.
- Global Admins, Intune Admins, or a role with **Collect diagnostics** permissions (under **Remote tasks**).
- Corporate-owned devices.
- Devices that are online and able to communicate with the service during diagnostics.

## Collect diagnostics

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows** > select a supported device.
2. On the device’s **Overview** page, select **…** >  **Collect diagnostics** > **Yes**. A pending notification appears on the device’s **Overview** page.
3. To see the status of the action, select **Device diagnostics monitor**.
4. After the  action completes, select **Download** in the row for the action > **Yes**.
5. The data zip file is added to your download tray and you can save it to your computer.

## Data collected

No personal information is collected. Each collection contains the following data:
- MDM logs (including Autopilot).
- Some event viewer logs.
- WMI and MDM ETLs.
- HKLM policy registry keys.
- ipconfig information and firewall rules.
- Ping testing of local network adapter.
- Windows Update logs.
- Windows data from MSINFO32, DSREGCMD, GPRESULT, and CertUtil.
- Config Manager client logs.
- mpcmdrun (Windows Defender ATP diagnostics).

## Disable device diagnostics
You can disable the **Collect diagnostics** remote action for all devices by following these steps:
1.	Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Device diagnostics**.
2.	Change the control to **Disabled**.