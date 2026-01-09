---
title: Windows feature update policies
description: Learn about Windows feature update policy settings and how to create feature update releases in Microsoft Intune.
ms.date: 09/10/2024
ms.topic: how-to
ms.reviewer: davidmeb; bryanke; davguy
---

# Manage Windows feature updates policies

When a device receives a feature update policy:

- The device updates to the version of Windows specified in the policy.
    - A device that already runs a later version of Windows remains at its current version. By freezing the version, the devices feature set remains stable during the duration of the policy.

  > [!NOTE]
  > A device won't install an update when it has a [*safeguard hold*](/windows/deployment/update/update-compliance-feature-update-status#safeguard-holds) for that Windows version. When a device evaluates applicability of an update version, Windows creates the temporary safeguard hold if an unresolved known issue exists. Once the issue is resolved, the hold is removed and the device can then update.
  >
  > - To learn about known issues that can result in a safeguard hold, see the applicable Windows release information and then reference the relevant Windows version from the table of contents for that page: [Windows 11 release information](/windows/release-health/windows11-release-information).


- Unlike using the *Pause* option of an update ring, which expires after 35 days, the feature updates policy remains in effect. Devices won't install a new Windows version until you modify or remove the feature updates policy. If you edit the policy to specify a newer version, devices can install that newer version.
- The ability to *Uninstall* the feature update is honored by the update rings.
- You can configure policy to manage the schedule by which Windows Update makes the offer available to devices. For more information, see [Rollout options for Windows Updates](rollout-options.md).
- When a Windows feature update is deployed to a device from the cloud service, the latest monthly quality update is automatically included.

## Create and assign feature update policies

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Windows**
1. Select **Windows updates** > **Feature updates**
1. Select **Create profile**
1. Under **Deployment settings**:
   - Specify a **Name** and an optional **Description** for the feature updates deployment.
   - From the **Feature update to deploy** dropdown, select the Windows version you want to deploy. Only versions of Windows that remain in support are available to select.
   - Select either:
       - **Make available to users as a required update**: the device will automatically install the update based on device settings.
       - **Make available to users as an optional update**: selected updates are made available to users as an optional update. The rollout settings still control when the update is available to the device but then the user must choose to install the update before it is installed on the device. This option requires a license for Windows Autopatch.
1. Under **Rollout options**, configure how and when the update is made available to devices that receive this policy. For more information, see [Rollout options for Windows Updates](rollout-options.md).
1. Select **Next**
1. Under **Assignments**, assign the policy to one or more device groups. Select **Next** to continue.
1. Under **Review + create**, review the settings. When ready to save the policy, select **Create**.

## User experience

When the admin makes the update available as an **Optional** update, the user must navigate to the **Windows update settings** page to see and choose to install the update. It is recommended to communicate to end users through your communication channels that an optional update is available to them.

When the user navigates to the **Windows update settings** page, they can see and choose to install the update when they're willing to take the update.
Users have to click **Download** to install the update. Otherwise it doesn't get installed until the admin makes it a **Required** update.
It's the same optional update experience that users are familiar with in their personal PCs.

When the admin switches from **Optional** to **Required**, the following behavior is observed:

- Updates aren't reinstalled for people who went ahead and opted to install the update back when it was an **Optional** update.
- If a device has not started on an update, the next time the device checks for updates the update is treated and automatically installed as a **Required** update.

When the admin switches from **Required** to **Optional**, the following behavior is observed:

- Devices that have already installed the update are not impacted.
- Devices that are pending restart are likely to continue to install the update as a **Required** update.
- Switching only impacts devices that haven't started the update yet or were early enough in the update process so they could be changed to an **Optional** update.


## Update behavior when multiple policies target a device

Consider the following points when feature update policies target a device with more than one update policy, or target a Windows 10 device with an update for Windows 11:

- Each Windows feature update policy supports a single update. When a device is targeted by more than one policy, it might be targeted with multiple update versions.

- The Windows Update service can only offer a device one feature update at a time, and always offers the latest update version that targets the device.

- Because Windows 11 updates are considered to be later versions than Windows 10, the service always offers the Windows 11 update to a device targeted by both Windows 10 and Windows 11 updates. This is done because deploying a Windows 11 update to a Windows 10 device is a supported upgrade path.

- Using the checkbox **When a device isn't capable of running Windows 11, install the latest Windows 10 feature update** when using multiple policies avoids the problems mentioned in this section and configures the service to detect when the Windows 11 is not eligible for a device and instead offers the latest Windows 10 feature update.

> [!NOTE]
> If you create two policies with the same device/s, where one is set to **Required** and the other set to **Optional** and both policies target the same feature update version, then the update is offered as **Required**.

## Manage Winodws feature update policies

In the admin center, go to **Devices** > **By platform** > **Windows** > **Manage updates** > **Windows updates** > **Feature updates** tab to view your profiles.

For each profile you can view:

- **Feature Update Version**: The feature update version in the profile.

- **Assigned**: If the profile is assigned to one or more groups.

- **Support**: The status of the feature update:
  - **Supported**: The feature update version is in support and can deploy to devices.
  - **Support Ending** - The feature update version is within two months of its support end date.
  - **Not supported**: Support for the feature update has expired and it no longer deploys to devices.

- **Support End Date**: The end of support date for the feature update version.
> [!NOTE]
> The date provided is for the Enterprise and Education editions of Windows.  To find the support dates for other editions supported by Windows Autopatch, see the [Microsoft Product Lifecycle site](https://aka.ms/lifecycle).

Selecting a profile from the list opens the profiles **Overview** pane where you can:

- Select **Delete** to delete the policy from Intune and remove it from devices.
- Select **Properties** to modify the deployment.  On the *Properties* pane, select **Edit** to open the *Deployment settings or Assignments*, where you can then modify the deployment.

> [!NOTE]
> The End user update status Last Scanned Time value will return *Not scanned yet* until a user logs on and Update Session Orchestrator (USO) scan is initiated. For more information on the Unified Update Platform (UUP) architecture and related components, see [Get started with Windows Update](/windows/deployment/update/windows-update-overview).

## Validation and reporting

There are multiple options to get in-depth reporting for Windows updates with Intune. Windows update reports show details about your Windows devices side by side in the same report.

To learn more, see [reports for feature updates policies](feature-updates-reports.md).

## Feature updates policies limitations and considerations

- When you deploy a feature updates policy to a device that is also targeted by an update ring policy, review the update ring for the following configurations:
  - We recommend setting the **Feature update deferral period (days)** to **0**. This configuration ensures your feature updates aren't delayed by update deferrals that might be configured in an update ring policy.
  - Feature updates for the update ring must be *running*. They must not be paused.

  > [!TIP]
  > If you're using feature updates, we recommend you set the Feature update deferral period to *0* in the associated Update Rings policy. Combining update ring deferrals with feature updates policy can create complexity that might delay update installations.
  >
  > For more information, see [Move from update ring deferrals to feature updates policy](ring-deferrals-to-feature-updates-policy.md).

- Windows feature updates policies can't be applied during the Windows Autopilot out of box experience (OOBE). Instead, the policies apply at the first Windows Update scan after a device has finished provisioning, which is typically a day.

- If you co-manage devices with Configuration Manager, feature updates policies might not immediately take effect on devices when you newly configure the [Windows Update policies workload](../../configmgr/comanage/workloads.md#windows-update-policies) to Intune. This delay is temporary but can initially result in devices updating to a later feature update version than is configured in the policy.

  To prevent this initial delay from impacting your co-managed devices:

  1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  1. Go to **Devices** > **By platform** > **Windows** > **Manage updates** > **Windows updates** > **Feature updates** tab > **Create profile**.
  1. For **Deployment settings**, enter a meaningful name and a description for the policy. Then, specify the feature update you want devices to be running.
  1. Complete the policy configuration, including assigning the policy to devices. The policy deploys to devices, though any device that already has the version you've selected, or a newer version, won't be offered the update.

     Monitor the report for the policy. To do so, go to **Reports** > **Windows Updates** > **Reports** tab > **Feature Updates report**. Select the policy you created and then generate the report.

  1. Devices that have a state of *OfferReady* or later, are enrolled for feature updates and protected from updating to anything newer than the update you specified in step 3. See [Use the Windows feature updates (Organizational) report](feature-updates-reports.md#use-the-windows-feature-updates-organizational-report).
  1. With devices enrolled for updates and protected, you can safely change the *Windows Update policies* workload from Configuration Manager to Intune. See, [Switch workloads to Intune](/configmgr/comanage/how-to-switch-workloads) in the co-management documentation.

- When the device checks in to the Windows Update service, the device's group membership is validated against the security groups assigned to the feature updates policy settings for any feature update holds.

- Managed devices that receive feature update policy are automatically enrolled with the [Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview). The service manages the updates a device receives. Microsoft Intune uses this service and works with your Intune policies for Windows updates to deploy feature updates to devices.

  When a device is no longer assigned to any feature update policies, the device remains enrolled in Autopatch. This change allows time to assign the device to a different policy and ensure that in the meantime the device doesn't receive a feature update that wasn't intended.

 As a result, when a feature updates policy no longer applies to a device, that device isn't offered any feature update until one of the following happens:

  - The device is assigned to a new feature update profile.
  - The device is unenrolled from Intune, which unenrolls the device from feature update management by Autopatch.
  - You use the [Windows Autopatch graph API](/graph/windowsupdates-enroll) to [remove the device](/graph/api/windowsupdates-updatableasset-unenrollassets) from feature update management.

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431