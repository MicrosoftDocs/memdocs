---
# required metadata

title: Configure schedules to gradually roll out Windows Updates in Intune
description: Configure schedules that manage how and when Windows updates roll out to your managed devices with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/16/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: davguy; bryanke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Rollout options for Windows Updates in Microsoft Intune

Use rollout options in Microsoft Intune policies for *Feature updates for Windows 10 and later*. With rollout options, you configure schedule options for Windows Update that result in the gradual rollout of updates to devices that receive your policies.

> [!TIP]  
> The default behavior for Windows Update is to make an update available to an assigned device  right away. This doesn’t mean the update will install right away. Instead, when an update is made available, the device becomes eligible to install it. Before a device can install an available update, the device must connect to Windows Update and scan for updates. When the need for an update is confirmed and the device is eligible, the  Windows Update service then offers the update to that device. After a device completes the update, it is then dependent on user behavior and other settings like Deadline.

You configure rollout options when creating [Feature Updates policy](../protect/windows-10-feature-updates.md) by selecting one of the following options:

- **Make update available as soon as possible** - With this option, there's no delay in making the update available to devices. This selection is the default behavior for Windows Update.

- **Make update available on a specific date** - With this option you can select a day on which the update in the policy will become available to install. Windows Update won’t make the update available to devices with this configuration until that day is reached.

- **Make update available gradually** - This process helps distribute the availability of the update across a range of time that you configure, with Windows Update making an update available to different subsets of the devices targeted by the policy, at different times. This option can reduce the effect to your network when compared to offering the update to all devices at the same time. The following section explains how to use this option in more detail.

## Make updates available gradually

With the option **Make update available gradually**, you can direct Windows Update to extend an update offer to different subsets of the devices that are targeted by the policy, at different times. We’ll refer to those subsets as offer groups. This behavior distributes the availability of the update across the time you’ve configured and can reduce the effect to your network as compared to offering the update to all devices at the same time.

To configure this option, you set the following values. Windows Update uses these values to determine how many offer groups to use based on the number of devices that are targeted by the policy, when to offer the update to the first group, and how long to wait until the update is made available to the next offer group:

- **First group availability** – Configure the first day that Windows Update will offer the update to devices that receive this policy.

  This date must be at least two days in the future from when you configure this policy. The delay enables Windows Update time to identify the devices that are targeted by the policy, how many offer groups to use, and to assign devices to those offer groups. If you select a date that isn’t at least two days in the future, Intune prompts you to reenter the date and displays the first valid date you can use.

- **Final group availability** – Configure the last day that Windows Update makes the update available to what will be the final offer group. The last offer group includes all remaining devices that haven’t already received the offer. Depending on the number of days between groups, the last offer might not occur on the last day of the schedule. Devices that are assigned this policy after the *final group availability* date will receive the offer immediately.

- **Days between groups** – Windows Update uses this value to determine how many offer groups to use when making the update available to devices.

  For example, you set the first group availability to be January 1, and the final group of availability to be January 10. Then you set three days between groups. The results are that Windows Update creates four groups to use for making the update available. Windows Update then makes the update available to devices in the first group on January 1, available to devices in the next group on January 4, and so on. The update is offered to devices in the last group on the 10th.  In this example, a quarter of the devices that receive the policy are assigned to each group, and devices can only receive the update offer after the group they're assigned to becomes eligible.

The following behaviors apply to the management of offer groups:

- Windows Update assigns targeted devices to the groups randomly, keeping groups evenly sized.

- If you edit a policy to change the date for the first or final group availability, or change the number of days between groups for the policy:
  - Windows Update recalculates the number of groups to use, if necessary.
  - For devices that haven't been offered the update, Windows Update adjusts group membership. This adjustment can change when a device is offered the update.
  - If the date of the *final group availability* is changed to be in the past, all remaining devices are offered the update as soon as possible.
  - If the date of the *first group availability* is changed to the future, devices that were already offered the update retain that offer, and new devices won’t receive an offer until that new start date.

- If the policy assignment changes to add or remove devices from receiving the policy:
  - New devices are distributed to the remaining offer groups.
  - For devices that are no longer targeted by the policy but were offered the update, Windows Update will attempt to retract the offer. However, the offer can’t be retracted if the device has started processing that offer.

## Intelligent rollouts

To enhance your use of gradual rollouts, you can configure *Intelligent rollouts*.

With intelligent rollouts, the Windows Update for Business Deployment Service uses data that it collects from devices to optimize the device members in the offer groups of your gradual rollout deployments. The first offer group will include the fewest number of devices that have the largest pool of variations in your environment. You can think of this as a *pilot ring* for the deployment.

To enable intelligent rollout, you deploy a [settings catalog](../configuration/settings-catalog.md) profile for device configuration to *Allow WUfB Cloud Processing*. Then, you assign the profile to the same groups that you use with your Feature update profiles. You only need to deploy this profile to a device a single time. The change then applies to all future deployments for that device.

### Likely issue safeguard holds

The Windows Update for Business setting that you enable, *Allow WUfB Cloud Processing*, is the same setting that enables the Deployment Service to create a *likely issue* safeguard hold for a device. To learn more, see [Safeguard holds](/windows/deployment/update/update-compliance-feature-update-status#safeguard-holds) in the documentation for Update Compliance monitoring.

As your rollout progresses, the deployment service monitors for unexpected issues. The service leverages insights from the Windows ecosystem and will create *likely issue* safeguard holds and proactively pause deployments to devices that are likely to encounter an issue. By applying safeguard holds to devices that are likely to have issues with the update, devices and end users are protected from potential productivity affecting issues.

To learn more, see [Manage safeguards using the Windows Update for Business deployment service](/graph/windowsupdates-manage-safeguards) in the Graph API documentation for device updates.

### Enable intelligent rollouts

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Devices** > **Configuration profiles** > **Create profile**.

3. For Platform, select **Windows 10 and later** and then for Profile type, select **Settings catalog**.

4. On the **Configuration settings** page, select **Add settings**, and then on the *Settings picker* page, search for **Allow WUfB Cloud Processing**.  You’ll find this setting in the *System* category. Select the checkbox for this setting and then close the *Settings picker* window.

5. Set *Allow WUfB Cloud Processing* to **Enabled**.

6. On the **Assignments** page, assign the profile to the same groups you use for your Feature update profiles, and then complete and *Create* this settings catalog profile, to deploy it.

After the profile deploys, devices that use gradual rollouts for Feature update profiles will also have intelligent optimization applied.

## Next steps

Configure [Feature Updates policy](../protect/windows-10-feature-updates.md)  
