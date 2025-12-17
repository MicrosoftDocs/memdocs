---
title: Configure Windows Update rings policy
description: Create and manage Intune policy for Windows update rings. You can configure, deploy, and pause update installation with Windows Update client policies using Microsoft Intune.
ms.date: 04/18/2024
ms.topic: how-to
ms.reviewer: davguy; davidmeb; bryanke
---

# Windows Update rings policy

Create update rings that specify how and when Windows as a Service updates your Windows devices with [*feature* and *quality* updates](/windows/deployment/update/get-started-updates-channels-tools#types-of-updates). With Windows, new feature and quality updates include the contents of all previous updates. As long as you've installed the latest update, you know your Windows devices are up to date. Unlike with previous versions of Windows, you now must install the entire update instead of part of an update.

Update rings can also be used to upgrade your eligible Windows 10 devices to Windows 11. To do so, when creating a policy you use the setting named *Upgrade Windows 10 devices to Latest Windows 11 release* by configuring it as *Yes*. When you use update rings to upgrade to Windows 11, devices install the most current version of Windows 11. If you later set the upgrade setting back to *No*, devices that haven't started the upgrade won't start while devices that are in the process of upgrading will continue to do so. Devices that have completed the upgrade will remain with Windows 11. For more information on eligibility, see [Windows 11 Specs and System Requirements | Microsoft](https://www.microsoft.com/windows/windows-11-specifications).

Windows update rings support [scope tags](../../intune-service/fundamentals/scope-tags.md). You can use scope tags with update rings to help you filter and manage sets of configurations that you use.

## Prerequisites

The following prerequisites must be met to use Windows Update Rings for Windows devices in Intune.

- Devices must have access to endpoints. To get a detailed list of endpoints required for the associated service listed here, see [Network endpoints](../../intune-service/fundamentals/intune-endpoints.md#access-for-managed-devices).
  - [Windows Update](/windows/privacy/manage-windows-1809-endpoints#windows-update)

  > [!NOTE]
  > Although not required to configure Windows Update client policies, if the Microsoft Account Sign-In Assistant (wlidsvc) service is disabled, Windows Update doesn't offer feature updates. For more information, see [Feature updates are not being offered while other updates are](/windows/deployment/update/windows-update-troubleshooting#feature-updates-are-not-being-offered-while-other-updates-are).

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> Windows update ring policies support the following Windows editions:
> - Pro
> - Pro Education
> - Enterprise
> - Education
> - Windows IoT Enterprise
> - Windows Team - for Surface Hub devices
> - Windows Holographic for Business - Windows Holographic for Business supports a subset of settings for Windows updates, including:
>    - **Automatic update behavior**
>    - **Microsoft product updates**
>    - **Servicing channel**: Any update build that is generally available.
> For more information, see [Manage Windows Holographic](../../intune-service/fundamentals/windows-holographic-for-business.md).
>
> Windows Enterprise LTSC and IoT Enterprise LTSC- LTSC is supported for Quality updates, but not for Feature updates. As a result, the following ring controls aren't supported for LTSC:
>   - [Pause](update-rings.md#pause) of *Feature* updates
>   - [Feature Update Deferral period (days)](settings.md#update-settings)
>   - [Set feature update uninstall period (2 - 60 days)](settings.md#update-settings)
>   - [Enable pre-release builds](settings.md#update-settings), which includes the following build options:
>     - Windows Insider Release Preview
>     - Beta Channel
>     - Dev Channel
>   - [Use deadline settings](settings.md#user-experience-settings) for *Feature* updates.
:::column-end:::
:::row-end:::

### Limitations for Microsoft Entra registered devices

Intune Update rings for Windows require the use of Windows Update client policies, which supports devices that are Workplace Joined (WPJ). However, the following Intune Windows Update policy types use Windows Update client policies and [Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview), which provides for additional capabilities that are not supported for WPJ devices.

- Driver updates
- Feature updates
- Quality updates (also known as *Expedited* updates)

For more information about Microsoft Entra registered devices limitations for Windows Update policies, see [Policy limitations for Workplace Joined devices](configure.md).

## Create and assign update rings

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** > **By platform** > **Windows** > **Manage updates** > **Windows 10 and later updates** > **Update rings** tab > **Create profile**.
1. Under *Basics*, specify a name, a description (optional), and then select **Next**.
  ![Create an update ring](./images/update-rings/basics-tab.png)
1. Under **Update ring settings**, configure settings for your business needs. For information about the available settings, see [Windows update settings](settings.md). After configuring *Update and User experience* settings, select **Next**.
1. Under **Scope tags**, select **+ Select scope tags** to open the *Select tags* pane if you want to apply them to the update ring. Choose one or more tags, and then click **Select** to add them to the update ring and return to the *Scope tag*s page.

   When ready, select **Next** to continue to *Assignments*.

   > [!NOTE]
   > When configuring or editing Intune policies, some policy types might not display the Scope Tags configuration page if there are no custom defined scope tags for the tenant.
   > If you don't see the Scope Tag option, ensure that at least one tag in addition to the default scope tag has been defined.

1. Under **Assignments**, choose **+ Select groups to include** and then assign the update ring to one or more groups. Use **+ Select groups to exclude** to fine-tune the assignment. Select **Next** to continue.

   In most cases, we recommend deploying update rings to device groups. Use of device groups aligns to our guidance for deploying [feature updates](feature-updates.md) and removes the need for a user to sign-on to a device before the policy can apply.

1. Under **Review + create**, review the settings, and then select **Create** when ready to save your Windows update ring. Your new update ring is displayed in the list of update rings.

## Manage your Windows Update rings

In the portal, navigate to **Devices** > **By platform** > **Windows** > **Manage updates** > **Windows 10 and later updates** > **Update rings** tab and select the ring policy that you want to manage. Intune displays details similar to the following for the selected policy:

:::image type="content" source="./images/update-rings/default-policy-view.png" alt-text="Screen capture of the default view for Update rings policy." lightbox="./images/update-rings/default-policy-view.png":::

This view includes:

- **Policy actions**: use the available actions to manage the selected update ring policy. For more information about each action, see the [Policy actions](#policy-actions) section.

:::image type="content" source="./images/update-rings/overview-actions.png" alt-text="Available actions.":::

This view also includes:

- **Essentials**: A list of details about the policy, including when it was created, last modified, and a count of groups that are assigned to the policy.

- **Device and user check-in status**: The default report view for this policy. In addition to this default view, the following report details and options are available:
  - **View report**: A button opens a more detailed report view for *Device and user check-in status*.

  - **Two additional report tiles**: You can select the tiles for the following reports to view additional details:
    - **Device assignment status**: This report shows all the devices that are targeted by the policy, including devices in a pending policy assignment state.
    - **Per setting status**: View the configuration status of each setting for this policy across all devices and users.

  For details about this report view, see [Reports for Update rings for Windows 10 and later policy](reports.md#reports-for-update-rings-for-windows-10-and-later-policy).

- **Properties**: View details for each configuration page of the policy, including an option to **Edit** each area of the policy.

### Policy actions

Select a tab to learn more about its purpose and available options.

# :::image type="icon" source="icons/delete.svg" border="false"::: [**Delete**](#tab/delete)

Select **Delete** to stop enforcing the settings of the selected Windows update ring. Deleting a ring removes its configuration from Intune so that Intune no longer applies and enforces those settings.

Deleting a ring from Intune doesn't modify the settings on devices that were assigned the update ring.  Instead, the device keeps its current settings. Devices don't maintain a historical record of what settings they held previously. Devices can also receive settings from other update rings that remain active.

To delete a ring:

1. While viewing the overview page for an Update Ring, select **Delete**.
1. Select **OK**.

# :::image type="icon" source="icons/pause.svg" border="false"::: [**Pause**](#tab/pause)
Select **Pause** to prevent assigned devices from receiving feature or quality updates for up to 35 days from the time you pause the ring. After the maximum days have passed, pause functionality automatically expires and the device scans Windows Updates for applicable updates. Following this scan, you can pause the updates again.
If you resume a paused update ring, and then pause that ring again, the pause period resets to 35 days.

To pause a ring:

1. While viewing the overview page for an Update Ring, select **Pause**.
1. Select either **Feature** or **Quality** to pause that type of update, and then select **OK**.
1. After pausing one update type, you can select Pause again to pause the other update type.

When an update type is paused, the Overview pane for that ring displays how many days remain before that update type resumes.

> [!IMPORTANT]
> After you issue a pause command, devices receive this command the next time they check into the service. It's possible that before they check in, they might install a scheduled update. Additionally, if a targeted device is turned off when you issue the pause command, when you turn it on, it might download and install scheduled updates before it checks in with Intune.

# :::image type="icon" source="icons/resume.svg" border="false"::: [**Resume**](#tab/resume)
While an update ring is paused, you can select **Resume** to restore feature and quality updates for that ring to active operation. After you resume an update ring, you can pause that ring again.

To resume a ring:

1. While viewing the overview page for a paused Update Ring, select **Resume**.
1. Select from the available options to resume either **Feature** or **Quality** updates, and then select **OK**.
1. After resuming one update type, you can select Resume again to resume the other update type.

# :::image type="icon" source="icons/extend.svg" border="false"::: [**Extend**](#tab/extend)
While an update ring is paused, you can select **Extend** to reset the pause period for both feature and quality updates for that update ring to 35 days.

To Extend the pause period for a ring:

1. While viewing the overview page for a paused Update Ring, select **Extend**.
1. Select from the available options to resume either **Feature** or **Quality** updates, and then select **OK**.
1. After extending the pause for one update type, you can select Extend again to extend the other update type.

# :::image type="icon" source="icons/uninstall.svg" border="false"::: [**Uninstall**](#tab/uninstall)

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


## Validation and reporting

There are multiple options to get in-depth reporting for Windows 10/11 updates with Intune. To learn more about the reports for update rings, including details for the default  view and the additional report tiles, see [Windows update reports](reports.md#reports-for-update-rings-for-windows-10-and-later-policy).

## Next steps

- Use [Windows feature updates in Intune](feature-updates.md)
- Use [Windows update compatibility reports](compatibility-reports.md)
- Use [Windows update reports](reports.md) for Windows updates
- Also see [Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview) in the Windows deployment content for an alternative solution
