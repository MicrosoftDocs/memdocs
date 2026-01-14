---
title: Upgrade Devices to Windows 11 Using Feature Updates
description: Learn how to upgrade Windows 10 devices to Windows 11 using feature updates in Microsoft Intune.
ms.date: 01/14/2026
ms.topic: how-to
ms.reviewer: 
---

# Upgrade devices to Windows 11 using feature updates

You can use feature updates policies to upgrade devices that run Windows 10 to Windows 11.

When you use feature updates policy to deploy Windows 11, you can target the policy to Windows 10 devices that meet the Windows 11 minimum requirements to upgrade them to Windows 11. Devices that don't meet the requirements for Windows 11 won't install the update and remain at their current Windows 10 version.

Another option is to select the checkbox **When a device isn't capable of running Windows 11, install the latest Windows 10 feature update**, then devices that don't meet the requirements for Windows 11 will get the latest Windows 10 feature update instead.

However, if a Windows 10 device that can't run Windows 11 is targeted with a Windows 11 update, future Windows 10 updates won't be offered to that device automatically. In this case, remove the not eligible device from the Windows 11 policy and assign the device to a Windows 10 feature update policy. See [Update behavior when multiple policies target a device](feature-updates-policy.md#update-behavior-when-multiple-policies-target-a-device).

## Prepare to upgrade to Windows 11

The first step in preparing for a Windows 11 upgrade is to ensure your devices meet the [minimum system requirements for Windows 11](/windows/whats-new/windows-11-requirements#hardware-requirements).

You can use [endpoint analytics](../../endpoint-analytics/index.md) to determine which of your devices meet the hardware requirements. If some of your devices don't meet all the requirements, you can see exactly which ones aren't met. To use Endpoint analytics, your devices must be managed by Intune, co-managed, or have the Configuration Manager client with tenant attach enabled.

If you're already using Endpoint analytics, navigate to the [Work from anywhere report](../../endpoint-analytics/work-from-anywhere.md), and select the Windows score category in the middle to open a flyout with aggregate Windows 11 readiness information. For more granular details, go to the Windows tab at the top of the report. On the Windows tab, you'll see device-by-device readiness information.

## Licensing for Windows 11 versions

Windows 11 includes a license agreement that can be viewed at [https://www.microsoft.com/useterms/](https://www.microsoft.com/useterms/). This license agreement is automatically accepted by an organization that submits a policy to deploy Windows 11.

When you configure a policy in the Microsoft Intune admin center to deploy any Windows 11 version, the Microsoft Intune admin center displays a notice to remind you that by submitting the policy you are accepting the Windows 11 License Agreement terms on behalf of the devices, and your device users. After submitting the feature updates policy, end users won't see or need to accept the license agreement, making the update process seamless.

This license reminder appears each time you select a Windows 11 build, even if all your Windows devices already run Windows 11. This prompt is provided because Intune doesn't track which devices will receive the policy, and its possible new devices that run Windows 10 might later enroll and be targeted by the policy.

For more information including general licensing details, see the [Windows 11 documentation](/windows/whats-new/windows-11).

## Create policy for Windows 11

To deploy Windows 11, you'll create and deploy a feature updates policy just as you might have done previously for a Windows 10 device. It's the [same process](feature-updates.md) though instead of selecting a Windows 10 version, you'll select a Windows 11 version from the *Feature update to deploy* dropdown list. The dropdown list displays both Windows 10 and Windows 11 version updates that are in support.

Also, the admin can choose to deploy the latest Windows 10 update to devices that are not eligible for Windows 11. To enable this feature, the admin must select the checkbox **When a device isn't capable of running Windows 11, install the latest Windows 10 feature update** in the deployment policy. This capability is only available if you choose a Windows 11 version from the *Feature update to deploy* dropdown list, and if the tenant meets the [licensing requirements](feature-updates.md#prerequisites) defined at the beginning of this document.

With this capability, you do not need to create two different deployment policies or two different feature updates. With a single policy, you can get your Windows 10 devices that can't go to Windows 11 to upgrade to the latest Windows 10 version and all the devices that can go to Windows 11 to upgrade to a Windows 11 version that you choose.

You cannot set the checkbox for an existing policy because changing the checkbox value ends the current deployment and starts two new deployments. To change your deployment settings, delete the current feature update policy and create a new policy with the checkbox selected.

- Deploying an older Windows version to a device won't downgrade the device. Devices only install an update when it's newer than the devices current version.
- Deploying a Windows 11 update to a Windows 10 device that supports Windows 11, upgrades that device.
