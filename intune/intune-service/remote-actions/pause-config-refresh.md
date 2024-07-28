---
# required metadata

title: Pause Config Refresh
titleSuffix: Microsoft Intune
description: Learn how Config Refresh can be paused for a configurable period of time, after which it's automatically re-enabled, or can be turned back on manually at any time by an IT administrator.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 03/12/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#customerIntent: As an IT admin, I want to pause Config Refresh so that I can make changes or run remediation on a device for troubleshooting or maintenance.
ms.reviewer: Mike Danoski
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Pause Config Refresh in Intune

With Config Refresh, you can ensure that your settings are retained the way you configured them. Use the Windows [settings catalog](../configuration/settings-catalog.md) to set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check in to Intune every 90 minutes by default, or every 30 minutes if desired.

To support this feature, there's a remote action that allows for a pause. If an admin needs to make changes or run remediation on a device for troubleshooting or maintenance, they can issue the Pause action from Intune for a specified period. When the period expires, the settings are enforced again.  

## Supported platforms for Pause Config Refresh

- Windows 11

## How to use Pause Config Refresh?

Complete the following steps to Pause Config Refresh for a configurable period of time.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as an administrator.

2. Select **Devices**, and then select **All devices**.

3. From the list of devices you manage, select a device, and choose **Pause Config Refresh**.

4. Specify the number of minutes to pause Config Refresh in the **Time period to Pause Config Refresh**. The maximum is 1440 minutes (24 hours).

5. Select **Pause**.

> [!Note]
> If you pause a device that does not have Config Refresh enabled it has no effect.
> If Config Refresh is paused and you want to resume, then select Pause again for 0 minutes to resume Config Refresh enforcement.

## Next steps

To see the status of the action you just took, in **Devices**, select **Device actions**.