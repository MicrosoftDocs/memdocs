---
title: Move from update ring deferrals to feature updates policy
description: TBD
ms.date: 09/10/2024
ms.topic: how-to
ms.reviewer: 
---

# Move from update ring deferrals to feature updates policy

When using Intune to manage Windows updates, it's possible to use both *update rings* policy with update deferrals, and *feature updates* policy to manage the updates you want to install on devices. If you're using feature updates, we recommend you end use of deferrals as configured in your update rings policy. Combining update ring deferrals with feature updates policy can create complexity that might delay update installations. You can continue to use the user experience settings from update rings, as they don't create issues when combined with feature updates policy.

While nothing prohibits use of both policy types to control which updates can install on a device, there's typically no advantage to doing so. When both policy types apply to a device, the conditions of both policy types must be met (be true) on the device before it's offered an applicable update. This scenario can lead to updates not installing as expected due to a block by one of the policy types.

## Plan to transition

Plan to manage the change from using update ring deferrals to feature updates so that the Windows Update service can be ready to deploy the updates you expect.

- When Intune policies for Windows updates are created or modified, Intune passes the policy details to Windows Update, which then determines the updates that are applicable for each device that's assigned one or more update policies.
- The process to evaluate updates for devices can take up to 10 minutes to complete, and in some cases might take a bit longer.
- If a device starts a scan for updates *after* a deferral has been set to zero or removed for the device, but *before* Windows Update completes the processing of the feature updates policy, that device can be offered an update you didn't plan for it to install.

Use the following process to ensure Windows Update has processed your feature updates policy before deferrals are removed.

### Switch to feature updates policy

1. In the Microsoft Intune admin center, create a [feature updates policy](feature-updates.md) that configures your desired Windows version, and assign it to applicable devices.
   After the saved policy is assigned to devices, it will take a few minutes for Windows Update to process the policy.
1. View the [Windows feature updates (Organizational)](reports.md#use-the-windows-10-feature-updates-organizational-report) report for the feature update policy, and verify devices have a state of **OfferReady** before you proceed. Once all devices show **OfferReady**, Windows Update has completed processing the policy.
1. After devices are verified to be in the **OfferReady** state you can safely reconfigure the [Update ring policy](update-rings.md), for that same set of devices to change the setting **Feature update deferral period (days)** to a value of **0**.
