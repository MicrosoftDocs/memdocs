---
title: Manage Windows Update Ring Policies
description: Learn about Windows Update ring policies for Windows devices, how to create and manage them, and improve update deployment.
ms.date: 01/12/2026
ms.topic: how-to
ms.reviewer: davguy; davidmeb; bryanke
---

# Manage Windows Update ring policies

Windows update rings define how and when Windows updates are installed on devices. They control client‑side update behavior such as deferral periods, restart settings, deadlines, active hours, and user notifications. Update rings apply broadly to Windows updates and are commonly used to create deployment stages—for example, test, pilot, and production—by assigning different settings to different device groups.

In Microsoft Intune, update rings are configured through **update ring policies**, which provide a general policy surface for managing Windows Update behavior on devices. These policies use Windows Update client settings and can be used on their own or alongside other Windows update policies, such as feature updates, quality updates, and driver updates.

> [!NOTE]
> When devices are managed through Windows Autopatch, update rings may be created and maintained by the service to implement rollout cadence and restart behavior. In these scenarios, admins typically shouldn't assign custom update rings to Autopatch‑managed devices. Instead, update rings work in combination with service‑managed policies that control update targeting and sequencing.

## Prerequisites

[!INCLUDE [prerequisites-network](includes/prerequisites-network.md)]

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::
> - [Microsoft Intune Plan 1](../../intune-service/fundamentals/licenses.md)
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> Windows Update ring policies support the following Windows editions:
> - Pro
> - Pro Education
> - Enterprise
> - Education
> - Windows IoT Enterprise
> - Windows Team - for Surface Hub devices
> - Windows Holographic for Business - Supports a suset of settings for Windows updates, including:
>    - **Automatic update behavior**
>    - **Microsoft product updates**
>    - **Servicing channel**: Any update build that is generally available.
> For more information, see [Manage Windows Holographic](../../intune-service/fundamentals/windows-holographic-for-business.md).
>
> Windows Enterprise LTSC and IoT Enterprise LTSC- LTSC is supported for Quality updates, but not for Feature updates. As a result, the following ring controls aren't supported for LTSC:
>   - Pause of feature updates
>   - Feature Update Deferral period
>   - Set feature update uninstall period
>   - Enable pre-release builds
>   - Use deadline settings for feature updates
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]

:::column-end:::
:::column span="3":::
> The *Microsoft Account Sign-In Assistant* service (`wlidsvc`) must be enabled and running.
>
> If the Microsoft Account Sign-In Assistant service is disabled, Windows Update doesn't offer feature updates. For more information, see [Feature updates are not being offered while other updates are](/windows/deployment/update/windows-update-troubleshooting#feature-updates-are-not-being-offered-while-other-updates-are).
:::column-end:::
:::row-end:::

## Create and assign update rings

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **By platform** > **Windows** > **Manage updates** > **Windows updates**
1. Select the **Update rings** tab > **Create profile**.
1. Under *Basics*, specify a name, a description (optional), and then select **Next**.
1. Under **Update ring settings**, configure settings aligned with your organization's update deployment strategy
   - For information about the available settings, see [Windows update settings](update-ring-policy-settings.md).
   - After configuring *Update and User experience* settings, select **Next**.
1. Under **Scope tags**, select **+ Select scope tags** to open the *Select tags* pane if you want to apply them to the update ring. Choose one or more tags, and then click **Select** to add them to the update ring and return to the *Scope tag*s page.
1. Select **Next** to continue to *Assignments*.
1. Under **Assignments**, choose **+ Select groups to include** and then assign the update ring to one or more groups. Use **+ Select groups to exclude** to fine-tune the assignment. Select **Next** to continue.

   > [!TIP]
   > Assign update rings to device groups. The use of device groups removes the need for a user to sign-on to a device before the policy can apply.

1. Under **Review + create**, review the settings, and then select **Create** when ready to save your Windows update ring. Your new update ring is displayed in the list of update rings.

## Manage update rings

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **By platform** > **Windows** > **Manage updates** > **Windows updates**
1. Select the **Update rings** tab and select the ring policy that you want to manage. Intune displays details similar to the following for the selected policy:

   :::image type="content" source="./images/update-rings.png" alt-text="Screen capture of the default view for Update ring policy." lightbox="./images/update-rings.png":::

This view includes:

- **Policy actions**: use the available actions to manage the selected update ring policy. For more information about each action, see the [Policy actions](#policy-actions) section.
- **Essentials**: A list of details about the policy, including when it was created, last modified, and a count of groups that are assigned to the policy.
- **Device and user check-in status**: The default report view for this policy. In addition to this default view, the following report details and options are available:
  - **View report**: A button opens a more detailed report view for *Device and user check-in status*.
  - **Two additional report tiles**: You can select the tiles for the following reports to view additional details:
    - **Device assignment status**: This report shows all the devices that are targeted by the policy, including devices in a pending policy assignment state.
    - **Per setting status**: View the configuration status of each setting for this policy across all devices and users.

  For details about this report view, see [Reports for update ring policies](update-rings-reports.md).

- **Properties**: View details for each configuration page of the policy, including an option to **Edit** each area of the policy.

### Policy actions

Select a tab to learn more about its purpose and available options.

# [:::image type="icon" source="icons/delete.svg" border="false"::: **Delete**](#tab/delete)

Select **Delete** to stop enforcing the settings of the selected Windows update ring. Deleting a ring removes its configuration from Intune so that Intune no longer applies and enforces those settings.

Deleting a ring from Intune doesn't modify the settings on devices that were assigned the update ring.  Instead, the device keeps its current settings. Devices don't maintain a historical record of what settings they held previously. Devices can also receive settings from other update rings that remain active.

To delete a ring:

1. While viewing the overview page for an Update Ring, select **Delete**.
1. Select **OK**.

# [:::image type="icon" source="icons/pause.svg" border="false"::: **Pause**](#tab/pause)
Select **Pause** to prevent assigned devices from receiving feature or quality updates for up to 35 days from the time you pause the ring. After the maximum days have passed, pause functionality automatically expires and the device scans Windows Updates for applicable updates. Following this scan, you can pause the updates again.
If you resume a paused update ring, and then pause that ring again, the pause period resets to 35 days.

To pause a ring:

1. While viewing the overview page for an Update Ring, select **Pause**.
1. Select either **Feature** or **Quality** to pause that type of update, and then select **OK**.
1. After pausing one update type, you can select Pause again to pause the other update type.

When an update type is paused, the Overview pane for that ring displays how many days remain before that update type resumes.

> [!IMPORTANT]
> After you issue a pause command, devices receive this command the next time they check into the service. It's possible that before they check in, they might install a scheduled update. Additionally, if a targeted device is turned off when you issue the pause command, when you turn it on, it might download and install scheduled updates before it checks in with Intune.

# [:::image type="icon" source="icons/resume.svg" border="false"::: **Resume**](#tab/resume)
While an update ring is paused, you can select **Resume** to restore feature and quality updates for that ring to active operation. After you resume an update ring, you can pause that ring again.

To resume a ring:

1. While viewing the overview page for a paused Update Ring, select **Resume**.
1. Select from the available options to resume either **Feature** or **Quality** updates, and then select **OK**.
1. After resuming one update type, you can select Resume again to resume the other update type.

# [:::image type="icon" source="icons/extend.svg" border="false"::: **Extend**](#tab/extend)
While an update ring is paused, you can select **Extend** to reset the pause period for both feature and quality updates for that update ring to 35 days.

To Extend the pause period for a ring:

1. While viewing the overview page for a paused Update Ring, select **Extend**.
1. Select from the available options to resume either **Feature** or **Quality** updates, and then select **OK**.
1. After extending the pause for one update type, you can select Extend again to extend the other update type.

# [:::image type="icon" source="icons/uninstall.svg" border="false"::: **Uninstall**](#tab/uninstall)

An Intune administrator can use **Uninstall** to uninstall (roll back) the latest *feature* update or the latest *quality* update for an active or paused update ring. After uninstalling one type, you can then uninstall the other type. Intune doesn't support or manage the ability of users to uninstall updates.

> [!IMPORTANT]
> When you use the *Uninstall* option, Intune passes the uninstall request to devices immediately.
>
> - Windows devices start removal of updates as soon as they receive the change in Intune policy. Update removal isn't limited to maintenance schedules, even when they're configured as part of the update ring.
> - If the update removal requires a device restart, the device  restarts without offering device users an option to delay.

For Uninstall to be successful:

A device must have installed the latest update. Because updates are cumulative, devices that install the latest update will have the most recent feature and quality update. An example of when you might use this option is to roll back the last update should you discover a breaking issue on your Windows machines.

Consider the following when you use Uninstall:

- Uninstalling a feature or quality update is only available for the servicing channel the device is on.
- Using uninstall for feature or quality updates triggers a policy to restore the previous update on your Windows machines.
- After a quality update is successfully rolled back, device users continue to see the update listed in **Windows settings** > **Updates** > **Update History**.
- When you initiate an uninstall of feature or quality updates on an Update Ring, Intune also pauses updates of the same type on that Update Ring.
- Once the feature or quality update pause elapses on an Update Ring, devices will reinstall previously uninstalled feature or quality updates if they're still applicable.
- Uninstallation will not be successful when the feature update was applied using an Enablement Package. To learn more about Enablement Packages, see [KB5015684](https://support.microsoft.com/topic/kb5015684-featured-update-to-version-22h2-by-using-an-enablement-package-09d43632-f438-47b5-985e-d6fd704eee61).
- For feature updates specifically, the time you can uninstall the update is limited from 2-60 days. This period is configured by the update rings Update setting **Set feature update uninstall period (2 – 60 days)**. You can't roll back a feature update that's been installed on a device after the update has been installed for longer than the configured uninstall period.

  For example, consider an update ring with a feature update uninstall period of 20 days. After 25 days you decide to roll back the latest feature update and use the Uninstall option.  Devices that installed the feature update over 20 days ago can't uninstall it as they've removed the necessary bits as part of their maintenance. However, devices that only installed the feature update up to 19 days ago can uninstall the update if they successfully check in to receive the uninstall command before exceeding the 20-day uninstall period.

For more information about Windows Update policies, see [Update CSP](/windows/client-management/mdm/update-csp) in the Windows client management documentation.

To uninstall the latest Windows update:

1. While viewing the overview page for a paused Update Ring, select **Uninstall**.
1. Select from the available options to uninstall either **Feature** or **Quality** updates, and then select **OK**.
1. After you trigger the uninstall for one update type, you can select Uninstall again to uninstall the remaining update type.
---

## Next steps

- [Windows feature update policies](feature-update-policy.md)
- [Windows feature updates reports](feature-updates-reports.md)
- [Windows update compatibility reports](compatibility-reports.md)

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431