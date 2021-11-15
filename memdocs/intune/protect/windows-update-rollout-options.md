---
# required metadata

title: Configure schedules to gradually roll out Windows Updates in Intune
description: Configure schedules that manage how and when Windows updates roll out to your managed devices with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/16/2021
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

Use rollout options in Microsoft Intune policies for *Feature updates for Windows 10 and later*. With rollout options, you configure schedule options for Windows Update that result in the gradual rollout of updates to to devices that receive your policies.

> [!TIP]  
> The default behavior for Windows Update is to make an update available to an assigned device  right away. This doesn’t mean the update will install right away. Instead, when an update is made available, the device becomes eligible to install it. Before a device can install an available update, the device must connect to Windows Update and scan for updates. When the need for an update is confirmed and the device is eligible, the  Windows Update service then offers the update to that device. After a device completes the update, it is then dependent on user behavior and other settings like Deadline.

You configure rollout options when creating [Feature Updates policy](../protect/windows-10-feature-updates.md) by selecting one of the following options:

- **Make update available as soon as possible** - With this option, there's no delay in making the update available to devices. This selection is the default behavior for Windows Update.

- **Make update available on a specific date** - With this option you can select a day on which the update in the policy will become available to install. Windows Update won’t make the update available to devices with this configuration until that day is reached.

- **Make update available gradually** - This process helps distribute the availability of the update across a range of time that you configure, with Windows Update making an update available to different subsets of the devices targeted by the policy, at different times. This option can reduce the effect to your network when compared to offering the update to all devices at the same time. The following section explains how to use this option in more detail.

In addition to configuring a gradual rollout, you can also configure [gradual rollout protections](#protect-your-gradual-updates). With intelligent optimization, the Windows Update service makes the update available to devices considered most likely to reveal possible issues before other devices. When using optimization, early success builds confidence that the larger population of your devices will receive the update successfully as well.

## Make updates available gradually

With the option **Make update available gradually**, you can direct Windows Update to extend an update offer to different subsets of the devices that are targeted by the policy, at different times. We’ll refer to those subsets as offer groups. This behavior distributes the availability of the update across the time you’ve configured and can reduce the effect to your network as compared to offering the update to all devices at the same time.

To configure this option, you set the following values. Windows Update uses these values to determine how many offer groups to use based on the number of devices that are targeted by the policy, when to offer the update to the first group, and how long to wait until the update is made available to the next offer group:

- **First group availability** – Configure the first day that Windows Update will offer the update to devices that receive this policy.

  This date must be at least two days in the future from when you configure this policy. The delay enables Windows Update time to identify the devices that are targeted by the policy, how many offer groups to use, and to assign devices to those offer groups. If you select a date that isn’t at least two days in the future, Intune prompts you to reenter the date and displays the first valid date you can use.

- **Final group availability** – Configure the last day that Windows Update makes the update available to what will be the final offer group. The last offer group includes all remaining devices that haven’t already received the offer. Depending on the number of days between groups, the last offer might not occur on the last day of the schedule. Devices that are assigned this policy after the *final group availability* date will receive the offer immediately.

- **Days between groups** – Windows Update uses this value to determine how many offer groups to use when making the update available to devices.

  For example, you set the first group availability to be January 1, and the final group of availability to be January 10. Then you set three days between groups. The results are that Windows Update creates four groups to use for making the update available. Windows Update then makes the update available to devices in the first group on the 1st, available to devices in the next group on the 4th, and so on. The update is offered to devices in the last group on the 10th.  In this example, a quarter of the devices that receive the policy are assigned to each group, and devices can only receive the update offer after the group they're assigned to becomes eligible.

The following behaviors apply to the management of offer groups:

- Windows Update assigns targeted devices to the groups randomly, keeping groups evenly-sized.

- If you edit a policy to change the date for the first or final group availability, or change the number of days between groups for the policy:
  - Windows Update recalculates the number of groups to use, if necessary.
  - For devices that haven't been offered the update, Windows Update adjusts group membership. This adjustment can change when a device is offered the update.
  - If the date of the *final group availability* is changed to be in the past, all remaining devices are offered the update as soon as possible.
  - If the date of the *first group availability* is changed to the future, devices that were already offered the update retain that offer, and new devices won’t receive an offer until that new start date.

- If the policy assignment changes to add or remove devices from receiving the policy:
  - New devices are distributed to the remaining offer groups.
  - For devices that are no longer targeted by the policy but were offered the update, Windows Update will attempt to retract the offer. However, the offer can’t be retracted if the device has started processing that offer.

## Protect your gradual updates

You can use a device configuration setting of *AllowWUfBCloudProcessing* for the Windows Update service to protect and optimize your gradual updates and to simplify your deployment processes.

When enabled, the service evaluates the devices that are targeted by the policy to find devices that exhibit or include the greatest range of characteristics that can affect a successful update, and assigns them to earlier groups. Characteristics include drivers, installed applications, hardware components like BIOS/UEFI, RAM, and more.

The intent is to make that update available first to a group of devices most likely to reveal problems with the update in your environment:

- With this optimization, after seeing successful results for that first group, you can have strong confidence that the rollout will go smoothly for later update groups.
- If there are issues with the first group, you can halt the deployment before additional devices receive the offer.

>[!IMPORTANT]  
> To optimize data, the Windows Update service might need to process the data in a different geographical region than where your tenant resides. If your data must remain the same geographical region as your tenant, do not enable optimization.

**To enable optimization**, you must use a device configuration profile with the settings catalog:

1. In the Microsoft Endpoint Manager admin center, create a device configuration profile that uses the settings catalog.
2. For the profile, select **Windows 10 and later**, and then **Settings catalog (preview)**.
3. On the *Configuration settings* page,  select **Add settings**, and then use the *Settings picker* to search for **AllowWUfBCloudProcessing** in the System category.
4. Complete the policy creation, assigning the policy to the devices that you want to be evaluated for optimization.

## Next steps

Configure [Feature Updates policy](../protect/windows-10-feature-updates.md)  
