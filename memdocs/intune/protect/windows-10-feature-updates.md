---
# required metadata

title: Configure feature updates policy for Windows 10 Windows 11 devices in Intune
description: Create and manage Intune policy for Windows feature updates. Configure and deploy policy to maintain the Windows feature version of Windows 10/11 devices you manage with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/09/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: davidmeb; bryanke; davguy
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Feature updates for Windows 10 and later policy in Intune

With *Feature updates for Windows 10 and later* in Intune, you can select the Windows [feature update](/windows/deployment/update/get-started-updates-channels-tools#types-of-updates) version that you want devices to remain at, like Windows 10 version 1909 or a version of Windows 11. Intune supports setting a feature level to any version that remains in support at the time you create the policy.

You can also use feature updates policy to [upgrade devices that run Windows 10 to Windows 11](#upgrade-devices-to-windows-11).

Windows feature updates policies work with your *Update rings for Windows 10 and later* policies to prevent a device from receiving a Windows feature version that's later than the value specified in the feature updates policy.

When a device receives a policy for Feature updates:

- The device updates to the version of Windows specified in the policy. A device that already runs a later version of Windows remains at its current version. By freezing the version, the devices feature set remains stable during the duration of the policy.

  > [!NOTE]
  > A device won't install an update when it has a *safeguard hold* for that Windows version. When a device evaluates applicability of an update version, Windows creates the temporary safeguard hold if an unresolved known issue exists. Once the issue is resolved, the hold is removed and the device can then update.
  >
  > - Learn more about [safeguard holds](/windows/deployment/update/update-compliance-feature-update-status#safeguard-holds) in the Windows documentation for *Feature Update Status*.
  > - To learn about known issues that can result in a safeguard hold, see the applicable Windows release information and then reference the relevant Windows version from the table of contents for that page:
  >   - [Windows 11 release information](/windows/release-health/windows11-release-information)
  >   - [Windows 10 release information](/windows/release-health/release-information)
  >
  >   For example, for Windows 11 version 21H2, go to the Windows 11 release information and then from the left-hand pane, select *Version 21H2* and then *Known issues and notifications*. The [resultant page](/windows/release-health/status-windows-11-21h2) includes details for known issues for that Windows version that might result in safeguard hold.

- Unlike using *Pause* with an update ring, which expires after 35 days, the Feature updates policy remains in effect. Devices won't install a new Windows version until you modify or remove the Feature updates policy. If you edit the policy to specify a newer version, devices can then install the features from that Windows version.

- The ability to *Uninstall* the Feature update is still honored by the Update Rings.

- You can configure policy to manage the schedule by which Windows Update makes the offer available to devices. For more information, see [Rollout options for Windows Updates](../protect/windows-update-rollout-options.md).

## Prerequisites

> [!IMPORTANT]
> This feature is not supported on GCC and GCC High/DoD cloud environments.

The following are prerequisites for Intune's Feature updates for Windows 10 and later:

- In addition to a license for Intune, your organization must have one of the following subscriptions that include a license for Windows Update for Business deployment service:
  - Windows 10/11 Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)
  - Windows 10/11 Education A3 or A5 (included in Microsoft 365 A3 or A5)
  - Windows Virtual Desktop Access E3 or E5
  - Microsoft 365 Business Premium

  *Review your subscription details for applicability to Windows 11.*

   Beginning in November of 2022, the Windows Update for Business deployment service (WUfB DS) license will be checked and enforced.
  
   Capabilities supported by client policies on Professional SKU devices will not require a license.  That includes basic controls for deploying a specified feature update and when to start making the update available to devices. The [Gradual Rollout](/mem/intune/protect/windows-update-rollout-options#make-updates-available-gradually) capability is a cloud only feature, requiring a license that includes the Windows Update for Business deployment service.
  
  If you’re blocked when creating new policies for capabilities that require WUfB DS and you get your licenses to use WUfB through an Enterprise Agreement (EA), contact the source of your licenses such as your Microsoft account team or the partner who sold you the licenses. The account team or partner can confirm that your tenants licenses meet the WUfB DS license requirements. See [Enable subscription activation with an existing EA](/windows/deployment/deploy-enterprise-licenses#enable-subscription-activation-with-an-existing-ea).

- Devices must:  
  - Run a version of Windows 10/11 that remains in support.
  - Be enrolled in Intune MDM and be Hybrid AD joined or Azure AD joined.
  - Have Telemetry turned on, with a minimum setting of [*Required*](../configuration/device-restrictions-windows-10.md#reporting-and-telemetry).

    Devices that receive a feature updates policy and that have Telemetry set to *Not configured* (off), might install a later version of Windows than defined in the feature updates policy. The prerequisite to require Telemetry is under review as this feature moves towards general availability.
  
    Configure Telemetry as part of a [Device Restriction policy](../configuration/device-restrictions-configure.md) for Windows 10/11. In the device restriction profile, under *Reporting and Telemetry*, configure the **Share usage data** with a minimum value of **Required**. Values of **Enhanced (1903 and earlier)** or **Optional** are also supported.

  - The *Microsoft Account Sign-In Assistant* (wlidsvc) must be able to run. If the service is blocked or set to *Disabled*, it fails to receive the update. For more information, see [Feature updates aren't being offered while other updates are](/windows/deployment/update/windows-update-troubleshooting#feature-updates-are-not-being-offered-while-other-updates-are). By default, the service is set to *Manual (Trigger Start)*, which allows it to run when needed.

  - Have access to endpoints. To get a detailed list of endpoints required for the associated service listed here, go to [Network endpoints](../fundamentals/intune-endpoints.md#access-for-managed-devices).

    - [Windows Update](/windows/privacy/manage-windows-1809-endpoints#windows-update)
    - Windows Update for Business -deployment service

- Feature updates are supported for the following Windows 10/11 editions:  
  - Pro
  - Enterprise
  - Education
  - Education
  - Pro for Workstations

  > [!NOTE]
  > **Unsupported versions and editions**:  
  > *Windows 10/11 Enterprise LTSC*: Windows Update for Business (WUfB) does not support the *Long Term Service Channel* release. Plan to use alternative patching methods, like WSUS or Configuration Manager.

## Limitations for Feature updates for Windows 10 and later policy

- When you deploy a *Feature updates for Windows 10 and later* policy to a device that also receives an *Update rings for Windows 10 and later* policy, review the update ring for the following configurations:
  - We recommend setting the **Feature update deferral period (days)** to **0**. This configuration ensures your feature updates are not delayed by update deferrals that might be configured in an update ring policy.
  - Feature updates for the update ring must be *running*. They must not be paused.

  > [!TIP]
  > If you're using feature updates, we recommend you end use of deferrals as configured in your update rings policy. Combining update ring deferrals with feature updates policy can create complexity that might delay update installations.  
  >
  > For more information, see [Move from update ring deferrals to feature updates policy](../protect/windows-update-for-business-configure.md#move-from-update-ring-deferrals-to-feature-updates-policy)

- Feature updates for Windows 10 and later policies cannot be applied during the Autopilot out of box experience (OOBE). Instead, the policies apply at the first Windows Update scan after a device has finished provisioning, which is typically a day.

- If you co-manage devices with Configuration Manager, feature updates policies might not immediately take effect on devices when you newly configure the [Windows Update policies workload](../../configmgr/comanage/workloads.md#windows-update-policies) to Intune. This delay is temporary but can initially result in devices updating to a later feature update version than is configured in the policy.

  To prevent this initial delay from impacting your co-managed devices:
  
  1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2. Go to **Devices** > **Windows** > **Feature updates for Windows 10 and later** > **Create profile**.
  3. For **Deployment settings**, enter a meaningful name and a description for the policy.  Then, Specify the feature update you want devices to be running.  
  4. Complete the policy configuration, including assigning the policy to devices. The policy deploys to devices, though any device that already has the version you’ve selected, or a newer version, won’t be offered the update.

     Monitor the report for the policy. To do so, go to **Reports** > **Windows Updates** > **Reports** Tab > **Feature Updates report**. Select the policy you created and then generate the report.

  5. Devices that have a state of *OfferReady* or later, are enrolled for feature updates and protected from updating to anything newer than the update you specified in step 3. See, [Use the Windows 10 feature updates (Organizational) report](../protect/windows-update-compliance-reports.md#use-the-windows-10-feature-updates-organizational-report).
  6. With devices enrolled for updates and protected, you can safely change the *Windows Update policies* workload from Configuration Manager to Intune. See, [Switch workloads to Intune](/configmgr/comanage/how-to-switch-workloads) in the co-management documentation.

- When the device checks in to the Windows Update service, the device's group membership is validated against the security groups assigned to the feature updates policy settings for any feature update holds.

- Managed devices that receive feature update policy are automatically enrolled with the [Windows Update for Business deployment service](/windows/deployment/update/deployment-service-overview). The deployment service manages the updates a device receives. The service is utilized by Microsoft Intune and works with your Intune policies for Windows updates to deploy feature updates to devices.

  When a device is no longer assigned to any feature update policies, Intune waits 90 days to unenroll that device from feature update management and to unenroll that device from the deployment service. This delay allows time to assign the device to a different policy and ensure that in the meantime the device doesn’t receive a feature update that wasn't intended.

  This means that when a feature updates policy no longer applies to a device, that device won’t be offered any feature updates until one of the following happens:

  - 90 days elapse.
  - The device is assigned to a new feature update profile.
  - The device is unenrolled from Intune, which unenrolls the device from feature update management by the Deployment Service.
  - You use the Windows Update for [Business deployment service graph API](/graph/windowsupdates-enroll) to [remove the device](/graph/api/windowsupdates-updatableasset-unenrollassets) from feature update management.

  To keep a device at its current feature update version and prevent it from being unenrolled and updated to the most recent feature update version, ensure the device remains assigned to a feature update policy that specifies the devices current Windows version.

## Create and assign Feature updates for Windows 10 and later policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Windows** > **Feature updates for Windows 10 and later** > **Create profile**.

3. Under **Deployment settings**:

   - Specify a name, a description (optional), and for **Feature update to deploy**, select the version of Windows with the feature set you want, and then select **Next**. Only versions of Windows that remain in support are available to select.

   - Configure **Rollout options** to manage when Windows Updates makes the update available to devices that receive this policy. For information about using these options, see [Rollout options for Windows Updates](../protect/windows-update-rollout-options.md).

4. Under **Assignments**, choose **+ Select groups to include** and then assign the feature updates deployment to one or more device groups. Select **Next** to continue.

5. Under **Review + create**, review the settings. When ready to save the Feature updates policy, select **Create**.  

## Upgrade devices to Windows 11

You can use policy for *Feature updates for Windows 10 and later* to upgrade devices that run Windows 10 to Windows 11.

When you use feature updates policy to deploy Windows 11, you can target the policy to Windows 10 devices that meet the Windows 11 minimum requirements to upgrade them to Windows 11. Devices that don’t meet the requirements for Windows 11 won’t install the update and remain at their current Windows 10 version.

However, if a Windows 10 device that can’t run Windows 11 is targeted with a Windows 11 update, future Windows 10 updates will not be offered to that device automatically. In this case, remove the not eligible device from the Windows 11 policy and assign the device to a Windows 10 feature update policy. See [Update behavior when multiple policies target a device](#update-behavior-when-multiple-policies-target-a-device).

When there are multiple versions of Windows 11 available, you can choose to deploy the latest build. When you deploy the latest build to a group of devices, those devices that already run Windows 11 will update while devices that still run Windows 10 will upgrade to that version of Windows 11 if they meet the upgrade requirements. In this way, you can always upgrade supported Windows 10 devices to the latest Windows 11 version  even if you choose to delay the upgrade of some devices until a future time.

### Prepare to upgrade to Windows 11

The first step in preparing for a Windows 11 upgrade is to ensure your devices meet the [minimum system requirements for Windows 11](/windows/whats-new/windows-11-requirements#hardware-requirements).

You can use [Endpoint analytics in Microsoft Intune](../../analytics/overview.md) to determine which of your devices meet the hardware requirements. If some of your devices don't meet all the requirements, you can see exactly which ones aren't met. To use Endpoint analytics, your devices must be managed by Intune, co-managed, or have the Configuration Manager client version 2107 or newer with tenant attach enabled.

If you’re already using Endpoint analytics, navigate to the [Work from anywhere report](../../analytics/work-from-anywhere.md), and select the Windows score category in the middle to open a flyout with aggregate Windows 11 readiness information. For more granular details, go to the Windows tab at the top of the report. On the Windows tab, you’ll see device-by-device readiness information.

### Licensing for Windows 11 versions

Windows 11 includes a new license agreement, which can be viewed at [https://www.microsoft.com/useterms/](https://www.microsoft.com/useterms/). This license agreement is automatically accepted by an organization that submits a policy to deploy Windows 11.

When you use configure a policy in the Microsoft Intune admin center to deploy any Windows 11 version, the Microsoft Intune admin center displays a notice to remind you that by submitting the policy you are accepting the Windows 11 License Agreement terms on behalf of the devices, and your device users. After submitting the feature updates policy, end users won’t see or need to accept the license agreement, making the update process seamless.

This license reminder appears each time you select a Windows 11 build, even if all your Windows devices already run Windows 11. This prompt is provided because Intune doesn’t track which devices will receive the policy, and its possible new devices that run Windows 10 might later enroll and be targeted by the policy.

For more information including general licensing details, see the [Windows 11 documentation](/windows/whats-new/windows-11).

### Create policy for Windows 11

To deploy Windows 11, you’ll create and deploy a feature updates policy just as you might have done previously for a Windows 10 device. It’s the [same process](#create-and-assign-feature-updates-for-windows-10-and-later-policy) though instead of selecting a Windows 10 version, you’ll select a Windows 11 version from the *Feature update to deploy* dropdown list. The dropdown list displays both Windows 10 and Windows 11 version updates that are in support.

- Policies for Windows 11 and Windows 10 can exist side by side in Microsoft Intune.
- Deploying an older Windows version to a device won’t downgrade the device. Devices only install an update when it's newer than the devices current version.
- Deploying a Windows 11 update to a Windows 10 device that supports Windows 11, [upgrades that device](#upgrade-devices-to-windows-11).
- Avoid deploying a Windows 11 policy to a Windows 10 device that doesn't support Windows 11.  

## Update behavior when multiple policies target a device:

Consider the following points when feature update policies target a device with more than one update policy, or target a Windows 10 device with an update for Windows 11:

- Each Windows feature update policy supports a single update. When a device is targeted by more than one policy, it might be targeted with multiple update versions.  

- The Windows Update service can only offer a device one feature update at a time, and always offers the latest update version that targets the device.

- Because Windows 11 updates are considered to be later versions than Windows 10, the service always offers the Windows 11 update to a device targeted by both Windows 10 and Windows 11 updates. This is done because deploying a Windows 11 update to a Windows 10 device is a supported upgrade path.

- The Windows Update for Business deployment service can’t determine that a device can’t run Windows 11. Therefore, if a Windows 10 device that can’t run Windows 11 is targeted with a Windows 11 update, Windows 10 updates will not be offered automatically. In this case, remove the not eligible device from the Windows 11 policy and assign the device to a Windows 10 feature update policy.

## Manage Feature updates for Windows 10 and later policy

In the admin center, go to **Devices** > **Windows** > **Feature updates for Windows 10 and later** to view your profiles.

For each profile you can view:

- **Feature Update Version** – The feature update version in the profile.

- **Assigned** – If the profile is assigned to one or more groups.

- **Support**: The status of the feature update:
  - **Supported** – The feature update version is in support and can deploy to devices.
  - **Support Ending** - The feature update version is within two months of its support end date.
  - **Not supported** – Support for the feature update has expired and it no longer deploys to devices.

- **Support End Date** – The end of support date for the feature update version.

Selecting a profile from the list opens the profiles **Overview** pane where you can:

- Select **Delete** to delete the policy from Intune and remove it from devices.
- Select **Properties** to modify the deployment.  On the *Properties* pane, select **Edit** to open the *Deployment settings or Assignments*, where you can then modify the deployment.
- Select **End user update status** to view information about the policy.

> [!NOTE]
> The End user update status Last Scanned Time value will return 'Not scanned yet' until an initial user logs on and Update Session Orchestrator (USO) scan is initiated. For more information on the Unified Update Platform (UUP) architecture and related components, see [Get started with Windows Update](/windows/deployment/update/windows-update-overview).

## Validation and reporting

There are multiple options to get in-depth reporting for Windows 10/11 updates with Intune. Windows update reports show details about your Windows 10 and Windows 11 devices side by side in the same report.

To learn more, see [Intune compliance reports](../protect/windows-update-compliance-reports.md).

## Next steps

- Use [Windows update rings in Intune](../protect/windows-10-update-rings.md)
- Use [Windows update compatibility reports](../protect/windows-update-compatibility-reports.md)
- Use [Intune compliance reports](../protect/windows-update-compliance-reports.md) for Windows 10/11 updates
- Also see [Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview) in the Windows deployment content for an alternative solution