---
# required metadata

title: Configure Windows 10 update rings policy in Intune - Azure | Microsoft Docs
description: Create and manage Intune policy for Windows 10 update rings. You can configure, deploy, and pause update installation with Windows Update for Business settings using Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/07/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dudeso
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Windows 10 update rings policy in Intune

Create update rings that specify how and when Windows as a Service updates your Windows 10 devices with [*feature* and *quality* updates](/windows/deployment/update/get-started-updates-channels-tools#types-of-updates). With Windows 10, new feature and quality updates include the contents of all previous updates. As long as you've installed the latest update, you know your Windows 10 devices are up to date. Unlike with previous versions of Windows, you now must install the entire update instead of part of an update.

Windows 10 update rings support [scope tags](../fundamentals/scope-tags.md). You can use scope tags with update rings to help you filter and manage sets of configurations that you use.

## Prerequisites

The following prerequisites must be met to use Windows updates for Windows 10 devices in Intune.

- Devices must:  
  - Run Windows 10 version 1607 or later.
  - Have Telemetry turned on, with a minimum setting of [*Basic*](../configuration/device-restrictions-windows-10.md#reporting-and-telemetry).
  
    Configure Telemetry as part of a [Device Restriction policy](../configuration/device-restrictions-configure.md) for Windows 10 or later. In the device restriction profile, under *Reporting and Telemetry*, configure the **Share usage data** with a minimum value of **Basic**. Values of **Enhanced** or **Full** are also supported.

  > [!NOTE]
  > Although not required to configure Windows Update for Business, if the Microsoft Account Sign-In Assistant (wlidsvc) service is disabled, Windows Update doesn't offer feature updates to devices running Windows 10 1709 or later. For more information, see [Feature updates are not being offered while other updates are](/windows/deployment/update/windows-update-troubleshooting#feature-updates-are-not-being-offered-while-other-updates-are).

- Update rings are supported for the following Windows 10 editions:  
  - Windows 10 Pro
  - Windows 10 Enterprise
  - Windows 10 Team - for Surface Hub devices
  - Windows Holographic for Business

    Windows Holographic for Business supports a subset of settings for Windows updates, including:
    - **Automatic update behavior**
    - **Microsoft product updates**
    - **Servicing channel**: Supports **Semi-annual channel** and **Semi-annual channel (Targeted)** options. For more information, see [Manage Windows Holographic](../fundamentals/windows-holographic-for-business.md).

  > [!NOTE]
  > **Unsupported versions and editions**:  
  > *Windows 10 Enterprise LTSC*: Windows Update for Business (WUfB) does not support the *Long Term Service Channel* release. Plan to use alternative patching methods, like WSUS or Configuration Manager.

## Create and assign update rings

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Windows** > **Windows 10 Update Rings** > **Create profile**.

3. Under *Basics*, specify a name, a description (optional), and then select **Next**.
  ![Create an update ring](./media/windows-10-update-rings/basics-tab.png)

4. Under **Update ring settings**, configure settings for your business needs. For information about the available settings, see [Windows update settings](../protect/windows-update-settings.md). After configuring *Update and User experience* settings, select **Next**.

5. Under **Scope tags**, select **+ Select scope tags** to open the *Select tags* pane if you want to apply them to the update ring. Choose one or more tags, and then click **Select** to add them to the update ring and return to the *Scope tag*s page.

   When ready, select **Next** to continue to *Assignments*.

6. Under **Assignments**, choose **+ Select groups to include** and then assign the update ring to one or more groups. Use **+ Select groups to exclude** to fine-tune the assignment. Select **Next** to continue. 

   While update rings can deploy to both device and user groups, consider using only device groups [when you also use feature updates](../protect/windows-10-feature-updates.md#limitations-for-windows-10-feature-updates-policy).

7. Under **Review + create**, review the settings, and then select **Create** when ready to save your Windows 10 update ring. Your new update ring is displayed in the list of update rings.

## Manage your Windows 10 Update rings

In the portal, navigate to **Devices** > **Windows** > **Windows 10 Update Rings** and select the policy that you want to manage.  The policy opens to its **Overview** page.

From this page, you can view the rings assignment status and select the following actions from the top of the Overview pane to manage the update ring:

- [Delete](#delete)
- [Pause](#pause)
- [Resume](#resume)
- [Extend](#extend)
- [Uninstall](#uninstall)

![Available actions](./media/windows-10-update-rings/overview-actions.png)

### Delete

Select **Delete** to stop enforcing the settings of the selected Windows 10 update ring. Deleting a ring removes its configuration from Intune so that Intune no longer applies and enforces those settings.

Deleting a ring from Intune doesn't modify the settings on devices that were assigned the update ring.  Instead, the device keeps its current settings. Devices don't maintain a historical record of what settings they held previously. Devices can also receive settings from additional update rings that remain active.

#### To delete a ring

1. While viewing the overview page for an Update Ring, select **Delete**.
2. Select **OK**.

### Pause

Select **Pause** to prevent assigned devices from receiving feature or quality updates for up to 35 days from the time you pause the ring. After the maximum days have passed, pause functionality automatically expires and the device scans Windows Updates for applicable updates. Following this scan, you can pause the updates again.
If you resume a paused update ring, and then pause that ring again, the pause period resets to 35 days.

#### To pause a ring

1. While viewing the overview page for an Update Ring, select **Pause**.
2. Select either **Feature** or **Quality** to pause that type of update, and then select **OK**.
3. After pausing one update type, you can select Pause again to pause the other update type.

When an update type is paused, the Overview pane for that ring displays how many days remain before that update type resumes.

> [!IMPORTANT]
> After you issue a pause command, devices receive this command the next time they check into the service. It's possible that before they check in, they might install a scheduled update. Additionally, if a targeted device is turned off when you issue the pause command, when you turn it on, it might download and install scheduled updates before it checks in with Intune.

### Resume

While an update ring is paused, you can select **Resume** to restore feature and quality updates for that ring to active operation. After you resume an update ring, you can pause that ring again.

#### To resume a ring

1. While viewing the overview page for a paused Update Ring, select **Resume**.
2. Select from the available options to resume either **Feature** or **Quality** updates, and then select **OK**.
3. After resuming one update type, you can select Resume again to resume the other update type.

### Extend  

While an update ring is paused, you can select **Extend** to reset the pause period for both feature and quality updates for that update ring to 35 days.

#### To Extend the pause period for a ring

1. While viewing the overview page for a paused Update Ring, select **Extend**.
2. Select from the available options to resume either **Feature** or **Quality** updates, and then select **OK**.
3. After extending the pause for one update type, you can select Extend again to extend the other update type.

### Uninstall  

An Intune administrator can use **Uninstall** to uninstall (roll back) the latest *feature* update or the latest *quality* update for an active or paused update ring. After uninstalling one type, you can then uninstall the other type. Intune doesn't support or manage the ability of users to uninstall updates.  

> [!IMPORTANT]
> When you use the *Uninstall* option, Intune passes the uninstall request to devices immediately.
>
> - Windows devices start removal of updates as soon as they receive the change in Intune policy. Update removal isn't limited to maintenance schedules, even when they're configured as part of the update ring.
> - If the update removal requires a device restart, the device  restarts without offering device users an option to delay.

For Uninstall to be successful:

- A device must run the Windows 10 April 2018 update (version 1803) or later.

A device must have installed the latest update. Because updates are cumulative, devices that install the latest update will have the most recent feature and quality update. An example of when you might use this option is to roll back the last update should you discover a breaking issue on your Windows 10 machines.

Consider the following when you use Uninstall:

- Uninstalling a feature or quality update is only available for the servicing channel the device is on.

- Using uninstall for feature or quality updates triggers a policy to restore the previous update on your Windows 10 machines.

- On a Windows 10 device, after a quality update is successfully rolled back, device users continue to see the update listed in **Windows settings** > **Updates** > **Update History**.

- When you initiate an uninstall of feature or quality updates on an Update Ring, Intune also pauses updates of the same type on that Update Ring.

- Once the feature or quality update pause elapses on an Update Ring, devices will reinstall previously uninstalled feature or quality updates if they are still applicable.

- For feature updates specifically, the time you can uninstall the update is limited from 2-60 days. This period is configured by the update rings Update setting **Set feature update uninstall period (2 – 60 days)**. You can't roll back a feature update that's been installed on a device after the update has been installed for longer than the configured uninstall period.

  For example, consider an update ring with a feature update uninstall period of 20 days. After 25 days you decide to roll back the latest feature update and use the Uninstall option.  Devices that installed the feature update over 20 days ago can't uninstall it as they've removed the necessary bits as part of their maintenance. However, devices that only installed the feature update up to 19 days ago can uninstall the update if they successfully check in to receive the uninstall command before exceeding the 20-day uninstall period.

For more information about Windows Update policies, see [Update CSP](/windows/client-management/mdm/update-csp) in the Windows client management documentation.

#### To uninstall the latest Windows 10 update

1. While viewing the overview page for a paused Update Ring, select **Uninstall**.
2. Select from the available options to uninstall either **Feature** or **Quality** updates, and then select **OK**.
3. After you trigger the uninstall for one update type, you can select Uninstall again to uninstall the remaining update type.

## Validation and reporting

There are multiple options to get in-depth reporting for Windows 10 updates with Intune. To learn more, see [Intune compliance reports](../protect/windows-update-compliance-reports.md).

## Next steps

- [Use Windows 10 feature updates in Intune](../protect/windows-10-feature-updates.md)
- Use [Intune compliance reports](../protect/windows-update-compliance-reports.md) for Windows 10 updates  
