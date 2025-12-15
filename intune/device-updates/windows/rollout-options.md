---
title: Configure schedules to gradually roll out Windows Updates in Intune
description: Configure schedules that manage how and when Windows updates roll out to your managed devices with Microsoft Intune.
ms.date: 04/07/2025
ms.topic: how-to
ms.reviewer: davguy; bryanke
#ms.custom:
ms.collection:
- M365-identity-device-management
- sub-updates
---

# Rollout options for Windows Updates in Microsoft Intune

Use rollout options in Microsoft Intune policies for *Feature updates for Windows 10 and later*. With rollout options, you configure schedule options for Windows Update that result in the gradual rollout of updates to devices that receive your policies.

> [!TIP]
> The default behavior for Windows Update is to make an update available to an assigned device right away. However, the update doesn't install right away. Instead, when an update is made available, the device becomes eligible to install it. Before a device can install an available update, the device must connect to Windows Update and scan for updates. When the need for an update is confirmed and the device is eligible, the  Windows Update service then offers the update to that device. After a device completes the update, it's then dependent on user behavior and other settings like Deadline.

You configure rollout options when creating [Feature Updates policy](feature-updates.md) by selecting one of the following options:

- **Make update available as soon as possible** - With this option, there's no delay in making the update available to devices. This selection is the default behavior for Windows Update.

- **Make update available on a specific date** - With this option you can select a day on which the update in the policy is initially available to install. Windows Update doesn't make the update available to devices with this configuration until that day is reached.


## Make updates available gradually

> [!WARNING]
> Gradual rollout will no longer be an available option after October 14, 2025.

With the option **Make update available gradually**, you can direct Windows Update to extend an update offer to different subsets of the devices that the policy targets, at different times. We refer to those subsets as *offer groups*. This behavior distributes the availability of the update across the time you've configured, which can reduce the effect to your network as compared to offering the update to all devices at the same time.

To configure this option, you set the following values. Windows Update uses these values to determine how many offer groups to use based on the number of devices that the policy targets, when to offer the update to the first group, and how long to wait until the update is made available to the next offer group:

- **First group availability** : Configure the first day that Windows Update offers the update to devices that receive this policy.

  This date must be at least two days in the future from when you configure this policy. The delay enables Windows Update time to identify the devices that the policy targets, how many offer groups to use, and to assign devices to those offer groups. If you select a date less than two days in the future, Intune prompts you to reenter the date and shows the first valid date you can use.

- **Final group availability** : Configure the last day that Windows Update makes the update available, which is to the final offer group. The last offer group includes all remaining devices that haven't already received the offer. Depending on the number of days between groups, the last offer might not occur on the last day of the schedule. Devices that are assigned this policy after the *final group availability* date receive the offer immediately.

- **Days between groups** : Windows Update uses this value to determine how many offer groups to use when making the update available to devices.

  For example, you set the first group availability to be January 1, and the final group of availability to be January 10. Then you set three days between groups. The results are that Windows Update creates four groups to use for making the update available. Windows Update then makes the update available to devices in the first group on January 1, available to devices in the next group on January 4, and so on. The update is offered to devices in the last group on the 10th. In this example, each group gets a quarter of the devices, and devices can only get the update after their group becomes eligible.

The following behaviors apply to the management of offer groups:

- Windows Update assigns targeted devices to groups randomly, keeping groups evenly sized, with a minimum unit of 100 devices per group.

- If you edit a policy to change the date for the first or final group availability, or change the number of days between groups for the policy:
  - Windows Update recalculates the number of groups to use, if necessary.
  - For devices that aren't offered the update, Windows Update adjusts group membership. This adjustment can change when a device is offered the update.
  - If the date of the *final group availability* is changed to be in the past, all remaining devices are offered the update as soon as possible.
  - If you change the date of the *first group availability* to the future, devices that were offered the update keep that offer, and new devices don't get an offer until the new start date.

- If the policy assignment changes to add or remove devices from receiving the policy:
  - New devices are distributed to the remaining offer groups.
  - Windows Update attempts to retract the update offer for devices that are no longer targeted by the policy but were offered the update. However, the offer can't be retracted if the device has started processing that offer.

## Intelligent rollouts

To enhance your use of gradual rollouts, you can configure *Intelligent rollouts*.

With intelligent rollouts, Windows Autopatch uses data that it collects from devices to optimize the device members in the offer groups of your gradual rollout deployments. The first offer group includes the fewest number of devices that have the largest pool of variations in your environment. You can think of this first offer group as a *pilot ring* for the deployment.

To enable intelligent rollout, you deploy a [settings catalog](../configuration/settings-catalog.md) profile for device configuration to *Allow Windows Update for Business Cloud Processing*. Then, you assign the profile to the same groups that you use with your Feature update profiles. You only need to deploy this profile to a device a single time. The change then applies to all future deployments for that device.

### Likely issue safeguard holds

The Windows Update client policies that you enable, *Allow WUfB Cloud Processing*, is the same setting that enables Autopatch to create a *likely issue* safeguard hold for a device. To learn more, see [Safeguard holds](/windows/deployment/update/wufb-reports-workbook) in the documentation for Windows Update for Business reports.

As your rollout progresses, Autopatch monitors for unexpected issues. The service uses insights from the Windows ecosystem to create *likely issue* safeguard holds to proactively pause deployments to devices that are likely to encounter an issue. By applying safeguard holds to devices that are likely to have issues with the update, devices and end users are protected from potential productivity affecting issues.

To learn more, see [Manage safeguards using Windows Autopatch](/graph/windowsupdates-manage-safeguards) in the Graph API documentation for device updates.

### Enable intelligent rollouts

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Devices** > **Manage devices** > **Configuration** > **Create**.

3. For Platform, select **Windows 10 and later** and then for Profile type, select **Settings catalog**.

4. On the **Configuration settings** page, select **Add settings**, and then on the *Settings picker* page, search for **Allow WUfB Cloud Processing**.  This setting is in the *System* category. Select the checkbox for this setting and then close the *Settings picker* window to return to the *Configuration settings* page.

5. Set *Allow WUfB Cloud Processing* to **Enabled**.

6. On the **Assignments** page, assign the profile to the same groups you use for your Feature update profiles, and then complete and *Create* this settings catalog profile, to deploy it.

After the profile deploys, devices that use gradual rollouts for Feature update profiles will also have intelligent optimization applied.

## Next steps

Configure [Feature Updates policy](feature-updates.md)
