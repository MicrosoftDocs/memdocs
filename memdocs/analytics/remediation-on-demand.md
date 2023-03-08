---
# required metadata

title: Run remediation on-demand (preview)
titleSuffix: Microsoft Endpoint Manager
description: Learn how you can run a proactive remediation script on-demand to a single Windows device with advanced features in Endpoint analytics.
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 07/03/2023 
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.localizationpriority: high
---

# Run a proactive remediation script on-demand (preview)

> [!NOTE]
> While in public preview, run remediation is available at no additional cost. When run remediation becomes generally available, it will be available as [Intune add-ons](../intune/fundamentals/intune-add-ons.md) and require an additional cost to the licensing options that include Microsoft Endpoint Manager or Intune.

You can use the **Run remediation** device action to run a [proactive remediation](proactive-remediations.md) script on-demand to a single Windows device.

## Prerequisites

- [Proactive remediations](proactive-remediations.md#bkmk_prereq) must already be configured before a remediation script can be used on-demand.
- The built-in or custom script packages must be available for users to run a remediation on-demand, however they do not need to be assigned to a user or device. You can use **Scope tags** to limit which remediation script packages a user can see.
- Users must be Global Admins, Intune Admins, or have a role with the **Run remediation** permission (available under  **Remote tasks**).
- Devices are online and able to communicate with Intune and [Windows Push Notification Service (WNS)](../intune/fundamentals/intune-endpoints.md#windows-push-notification-services-wns) during the remote action.
- The [Intune Management Extension](../intune/apps/intune-management-extension.md) must be installed on devices. The installation is done automatically when a Win32 app, PowerShell script, or Proactive Remediation is assigned to a user or device.

## How to run a proactive remediation script on-demand

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Navigate to  **Devices** >  **Windows** > select a supported device.
3. On the device's  **Overview**  page, select  **…** > **Run remediation (preview).**
4. In the **Run remediation (preview)** pane, select the **Script package** you want to run from the list. Select **View details** to see properties of the script package like detection and remediation script contents, description, and configured settings.
5. To run the remediation on-demand, select **Run remediation**.

> [!NOTE]
> Only a single **Run remediation** device action can be issued at a time for the same device. If you run multiple **Run remediation** device actions in a short period of time to a device, they may overwrite each other.

> [!NOTE]
> The device might not receive the **Run remediation** device action if it is not online or able to successfully communicate with Intune or Windows Push Notification Service (WNS) when the device action is sent.

## Monitor remediation status for a device

You can view the status of proactive remediations that have been assigned or run on-demand to a device.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Navigate to  **Devices** >  **Windows** > select a supported device.
3. Select **Remediations** in the **Monitor** section.