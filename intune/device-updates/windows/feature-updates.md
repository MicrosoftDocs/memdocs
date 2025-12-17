---
title: Windows feature update releases
description: Learn about Windows feature update policy settings and how to create feature update releases in Microsoft Intune.
ms.date: 09/10/2024
ms.topic: how-to
ms.reviewer: davidmeb; bryanke; davguy
---

# Configure Windows feature updates releases

With Microsoft Intune, you can create and deploy policy settings that ensure your Windows devices remain on a specific Windows feature update version. These settings help you manage and control the feature set of Windows on your devices, providing stability and predictability for your organization's IT environment.

With these policies, you can:

- Select the Windows [feature update](/windows/deployment/update/get-started-updates-channels-tools#types-of-updates) version that you want devices to remain at. This option supports setting a feature level to any version that remains in support at the time you create the policy.
- [Upgrade devices that run Windows 10 to Windows 11](#upgrade-devices-to-windows-11).

Windows feature updates policies work with update rings policies to prevent a device from receiving a Windows feature version that's later than the value specified in the feature updates policy.

## How feature updates work

When a device receives a policy for Feature updates:

- The device updates to the version of Windows specified in the policy. A device that already runs a later version of Windows remains at its current version. By freezing the version, the devices feature set remains stable during the duration of the policy.

  > [!NOTE]
  > A device won't install an update when it has a *safeguard hold* for that Windows version. When a device evaluates applicability of an update version, Windows creates the temporary safeguard hold if an unresolved known issue exists. Once the issue is resolved, the hold is removed and the device can then update.
  >
  > - Learn more about [safeguard holds](/windows/deployment/update/update-compliance-feature-update-status#safeguard-holds) in the Windows documentation for *Feature Update Status*.
  > - To learn about known issues that can result in a safeguard hold, see the applicable Windows release information and then reference the relevant Windows version from the table of contents for that page:
  >   - [Windows 11 release information](/windows/release-health/windows11-release-information)


- Unlike using the *Pause* option of an update ring, which expires after 35 days, the feature updates policy remains in effect. Devices won't install a new Windows version until you modify or remove the Feature updates policy. If you edit the policy to specify a newer version, devices can then install the features from that Windows version.
- The ability to *Uninstall* the Feature update is still honored by the update rings.
- You can configure policy to manage the schedule by which Windows Update makes the offer available to devices. For more information, see [Rollout options for Windows Updates](rollout-options.md).
- When a Windows feature update is deployed to a device from the cloud service, the latest monthly quality update is automatically included.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [cloud](../../includes/requirements/cloud.md)]

:::column-end:::
:::column span="3":::

> - Public cloud
>
>   > [!IMPORTANT]
>   >
>   > This feature isn't supported on Government Community Cloud (GCC) High and Department of Defense (DoD) cloud environments.
>   > [Enable subscription activation with an existing EA](/windows/deployment/deploy-enterprise-licenses#enable-subscription-activation-with-an-existing-ea) isn't applicable to GCC and GCC High/DoD cloud environments for Windows Autopatch capabilities.

:::column-end:::
:::row-end:::


:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::

> The core functionality of creating and targeting a feature update only requires a license for Intune. The core functionality includes creating the policy and selecting a feature update to update devices, using the **Make updates available as soon as possible** option or specifying a start date, and reporting. Capabilities supported by client policies on Professional SKU devices don't require a license.
>
> Additional cloud-based functionality requires an additional license. To use a cloud-based capability, in addition to a license for Intune, your organization must have one of the following subscriptions that include a license for Windows Autopatch:
> - Windows Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)
> - Windows Education A3 or A5 (included in Microsoft 365 A3 or A5)
> - Windows Virtual Desktop Access E3 or E5
> - Microsoft 365 Business Premium
> 
> The cloud-based capabilities requiring the additional license are indicated in the *Create feature update deployment* > or policy creation page and include the following items and potentially new features:
> - Gradual rollout: The [Gradual Rollout](rollout-options.md#make-updates-available-gradually) capability is a cloud > only feature and includes basic controls for deploying a specified feature update and when to start making the update > available to devices.
> - [Optional feature updates](#create-and-assign-feature-updates-for-windows-10-and-later-policy)
> - Windows 10 (SxS): The Windows 10 (SxS) feature is a cloud-only feature. If you're blocked when creating new policies > for capabilities that require Windows Autopatch and you get your licenses to use Windows Update client policies > through an Enterprise Agreement (EA), contact the source of your licenses such as your Microsoft account team or the > partner who sold you the licenses. The account team or partner can confirm that your tenants licenses meet the Windows > Autopatch license requirements. See [Enable subscription activation with an existing EA](/windows/deployment/deploy-enterprise-licenses#enable-subscription-activation-with-an-existing-ea).

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> The configuration of feature update releases supports the following Windows editions:
> - Pro
> - Pro Education
> - Enterprise
> - Education
>
> > [!IMPORTANT]
> > *Windows Enterprise LTSC*: Windows Update client policies doesn'o't support the *Long Term Service Channel* release. Plan to use alternative patching methods, like WSUS or Configuration Manager.
:::column-end:::
:::row-end:::


:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]

:::column-end:::
:::column span="3":::
> Feature update policies supports devices that are:
> - Enrolled in Intune
> - Microsoft Entra joined
> - Microsoft Entra hybrid joined
>
> Devices must also meet the following requirements:
> - Telemetry must be turned on, with a minimum setting of [*Required*](../../intune-service/configuration/device-restrictions-windows-10.md#reporting-and-telemetry).
>    Devices that receive a feature updates policy and that have Telemetry set to *Not configured* (off), might install a later version of Windows than defined in the feature updates policy.
>
>    Configure Telemetry as part of a [Device Restriction policy](../../intune-service/configuration/device-restrictions-configure.md) for Windows. In the device restriction profile, under *Reporting and Telemetry*, configure the **Share usage data** with a minimum value of **Required**. Values of **Enhanced (1903 and earlier)** or **Optional** are also supported.
> - The *Microsoft Account Sign-In Assistant* (wlidsvc) must be able to run. If the service is blocked or set to *Disabled*, it fails to receive the update. For more information, see [Feature updates aren't being offered while other updates are](/windows/deployment/update/windows-update-troubleshooting#feature-updates-are-not-being-offered-while-other-updates-are). By default, the service is set to *Manual (Trigger Start)*, which allows it to run when needed.
> - Have access to endpoints. To get a detailed list of endpoints required for the associated services listed here, see [Network endpoints](../../intune-service/fundamentals/intune-endpoints.md#access-for-managed-devices).
>    - [Windows Update](/windows/privacy/manage-windows-1809-endpoints#windows-update)
>    - Windows Autopatch
>
> - Enable [data collection](reports.md#configuring-for-client-data-reporting) in Intune for devices that you wish to deploy feature updates.
:::column-end:::
:::row-end:::


### Limitations for Microsoft Entra registered devices

Feature updates policies require the use of Windows Update client policies and [Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview). Where Windows Update client policies supports Microsoft Entra registered devices, Windows Autopatch provides more capabilities that aren't supported by those devices.

For more information about Microsoft Entra registered devices limitations for Windows Update policies, see [Policy limitations for Workplace Joined devices](configure.md).

## Limitations for Feature updates for Windows 10 and later policy

- When you deploy a *Feature updates for Windows 10 and later* policy to a device that also receives an *Update rings for Windows 10 and later* policy, review the update ring for the following configurations:
  - We recommend setting the **Feature update deferral period (days)** to **0**. This configuration ensures your feature updates aren't delayed by update deferrals that might be configured in an update ring policy.
  - Feature updates for the update ring must be *running*. They must not be paused.

  > [!TIP]
  > If you're using feature updates, we recommend you set the Feature update deferral period to *0* in the associated Update Rings policy. Combining update ring deferrals with feature updates policy can create complexity that might delay update installations.
  >
  > For more information, see [Move from update ring deferrals to feature updates policy](configure.md#move-from-update-ring-deferrals-to-feature-updates-policy)

- Feature updates for Windows 10 and later policies can't be applied during the Windows Autopilot out of box experience (OOBE). Instead, the policies apply at the first Windows Update scan after a device has finished provisioning, which is typically a day.

- If you co-manage devices with Configuration Manager, feature updates policies might not immediately take effect on devices when you newly configure the [Windows Update policies workload](../../configmgr/comanage/workloads.md#windows-update-policies) to Intune. This delay is temporary but can initially result in devices updating to a later feature update version than is configured in the policy.

  To prevent this initial delay from impacting your co-managed devices:

  1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2. Go to **Devices** > **By platform** > **Windows** > **Manage updates** > **Windows 10 and later updates** > **Feature updates** tab > **Create profile**.
  3. For **Deployment settings**, enter a meaningful name and a description for the policy. Then, specify the feature update you want devices to be running.
  4. Complete the policy configuration, including assigning the policy to devices. The policy deploys to devices, though any device that already has the version you've selected, or a newer version, won't be offered the update.

     Monitor the report for the policy. To do so, go to **Reports** > **Windows Updates** > **Reports** tab > **Feature Updates report**. Select the policy you created and then generate the report.

  5. Devices that have a state of *OfferReady* or later, are enrolled for feature updates and protected from updating to anything newer than the update you specified in step 3. See [Use the Windows 10 feature updates (Organizational) report](reports.md#use-the-windows-10-feature-updates-organizational-report).
  6. With devices enrolled for updates and protected, you can safely change the *Windows Update policies* workload from Configuration Manager to Intune. See, [Switch workloads to Intune](/configmgr/comanage/how-to-switch-workloads) in the co-management documentation.

- When the device checks in to the Windows Update service, the device's group membership is validated against the security groups assigned to the feature updates policy settings for any feature update holds.

- Managed devices that receive feature update policy are automatically enrolled with the [Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview). The service manages the updates a device receives. Microsoft Intune uses this service and works with your Intune policies for Windows updates to deploy feature updates to devices.

  When a device is no longer assigned to any feature update policies, the device remains enrolled in Autopatch. This change allows time to assign the device to a different policy and ensure that in the meantime the device doesn't receive a feature update that wasn't intended.

 As a result, when a feature updates policy no longer applies to a device, that device isn't offered any feature update until one of the following happens:

  - The device is assigned to a new feature update profile.
  - The device is unenrolled from Intune, which unenrolls the device from feature update management by Autopatch.
  - You use the [Windows Autopatch graph API](/graph/windowsupdates-enroll) to [remove the device](/graph/api/windowsupdates-updatableasset-unenrollassets) from feature update management.

## Create and assign Feature updates for Windows 10 and later policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **By platform** > **Windows** > **Windows 10 and later updates** > **Feature updates** tab > **Create profile**.

3. Under **Deployment settings**:

   a. **Name**, **Description**: Specify a name, and a description (optional).

   b. **Required/Optional updates**: These options are only available when the target version is Windows 11.

     - When the default option **Make available to users as a required update** is selected, the device will automatically install the update based on device settings.
     - When the admin selects the option **Make available to users as an optional update**, then the selected updates are made available to users as an optional update. The rollout settings still control when the update is available to the device but then the user must choose to install the update before it is installed on the device.

     **What the user sees on their device**
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

   c. **Feature update to deploy**: select the specific version of Windows with the feature set you want deployed on your devices. Only versions of Windows that remain in support are available to select.

   d. **Rollout options**: Configure **Rollout options** to manage when Windows Updates makes the update available to devices that receive this policy. For more information about using these options, see [Rollout options for Windows Updates](rollout-options.md), and then select **Next**.

4. Under **Assignments**, choose **+ Select groups to include** and then assign the feature updates deployment to one or more device groups. Select **Next** to continue.

5. Under **Review + create**, review the settings. When ready to save the Feature updates policy, select **Create**.

## Update behavior when multiple policies target a device

Consider the following points when feature update policies target a device with more than one update policy, or target a Windows 10 device with an update for Windows 11:

- Each Windows feature update policy supports a single update. When a device is targeted by more than one policy, it might be targeted with multiple update versions.

- The Windows Update service can only offer a device one feature update at a time, and always offers the latest update version that targets the device.

- Because Windows 11 updates are considered to be later versions than Windows 10, the service always offers the Windows 11 update to a device targeted by both Windows 10 and Windows 11 updates. This is done because deploying a Windows 11 update to a Windows 10 device is a supported upgrade path.

- Using the checkbox **When a device isn't capable of running Windows 11, install the latest Windows 10 feature update** when using multiple policies avoids the problems mentioned in this section and configures the service to detect when the Windows 11 is not eligible for a device and instead offers the latest Windows 10 feature update.

> [!NOTE]
> If you create two policies with the same device/s, where one is set to **Required** and the other set to **Optional** and both policies target the same feature update version, then the update is offered as **Required**.

## Manage Feature updates for Windows 10 and later policy

In the admin center, go to **Devices** > **By platform** > **Windows** > **Manage updates** > **Windows 10 and later updates** > **Feature updates** tab to view your profiles.

For each profile you can view:

- **Feature Update Version** – The feature update version in the profile.

- **Assigned** – If the profile is assigned to one or more groups.

- **Support**: The status of the feature update:
  - **Supported** – The feature update version is in support and can deploy to devices.
  - **Support Ending** - The feature update version is within two months of its support end date.
  - **Not supported** – Support for the feature update has expired and it no longer deploys to devices.

- **Support End Date** – The end of support date for the feature update version.
> [!NOTE]
> The date provided is for the Enterprise and Education editions of Windows.  To find the support dates for other editions supported by Windows Autopatch, see the [Microsoft Product Lifecycle site](https://aka.ms/lifecycle).

Selecting a profile from the list opens the profiles **Overview** pane where you can:

- Select **Delete** to delete the policy from Intune and remove it from devices.
- Select **Properties** to modify the deployment.  On the *Properties* pane, select **Edit** to open the *Deployment settings or Assignments*, where you can then modify the deployment.

> [!NOTE]
> The End user update status Last Scanned Time value will return 'Not scanned yet' until an initial user logs on and Update Session Orchestrator (USO) scan is initiated. For more information on the Unified Update Platform (UUP) architecture and related components, see [Get started with Windows Update](/windows/deployment/update/windows-update-overview).

## Validation and reporting

There are multiple options to get in-depth reporting for Windows 10/11 updates with Intune. Windows update reports show details about your Windows 10 and Windows 11 devices side by side in the same report.

To learn more, see [Intune compliance reports](reports.md).

## Next steps

- Use [Windows update rings in Intune](update-rings.md)
- Use [Windows update compatibility reports](compatibility-reports.md)
- Use [Windows update reports](reports.md) for Windows 10/11 updates
- Also see [Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview) in the Windows deployment content for an alternative solution
