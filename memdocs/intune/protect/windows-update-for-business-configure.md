---
# required metadata

title: Learn about using Windows Update for Business in Microsoft Intune
description: Manage Windows 10 and Windows 11 software updates by using Intune policy for Update rings for Windows and Windows feature updates for Windows Update for Business settings in Microsoft Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 11/27/2024
ms.topic: overview
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
- sub-updates
---

# Manage Windows 10 and Windows 11 software updates in Intune

Use Microsoft Intune to manage the install of Windows 10/11 software updates from Windows Update client policies.

By using Windows Update client policies, you simplify the update management experience. You don't need to approve individual updates for groups of devices and can manage risk in your environments by configuring an update rollout strategy. With Intune, you can [configure update settings](windows-update-settings.md) on devices and configure deferral of update installation. You can also prevent devices from installing features from new Windows versions to help keep them stable, while allowing those devices to continue installing updates for quality and security.

Intune stores only the update policy assignments, not the updates themselves. When you save a policy, Intune passes the configuration details to Windows Update, which then determines which of these updates are offered to each device. Devices access Windows Update directly for the updates.

Learn more about Windows [*feature* and *quality* updates](/windows/deployment/update/get-started-updates-channels-tools#types-of-updates) in the Windows documentation.

## Policy types to manage updates

Intune provides the following policy types to manage updates, which you assign to groups of devices:

- **Update rings for Windows 10 and later**: This policy is a collection of settings that configures when devices that run Windows 10 and Windows 11 updates get installed. Update ring policies are supported for devices that run Windows 10 version 1607 or later, and Windows 11. For more information, see [Update rings policy](../protect/windows-10-update-rings.md).

- **Feature updates for Windows 10 and later**: The [Feature updates](../protect/windows-10-feature-updates.md) policy updates devices to the Windows version that you specify, and then freezes the feature set version on those devices. This version freeze remains in place until you choose to update them to a later Windows version. While the feature version remains static, devices can continue to install quality and security updates that are available for their feature version.

  You can also use Feature updates policy to [upgrade your devices that run Windows 10 to Windows 11](../protect/windows-10-feature-updates.md#upgrade-devices-to-windows-11).

- **Quality updates for Windows 10 and later**: With Quality updates for Windows 10 and later, also referred to as Expedited updates, you can expedite the install of the most recent Windows 10 and Windows 11 security updates on devices that you manage with Microsoft Intune. Expedited install is accomplished without the need to pause or edit your existing monthly servicing policies. For more information, see [Expedite updates policy](../protect/windows-10-expedite-updates.md).

- **Driver updates for Windows 10 and later**: With Windows Driver Update Management in Microsoft Intune, you can review, approve for deployment and pause deployments of driver updates for your managed Windows 10 and Windows 11 devices. Your policies can automatically install the newest recommended driver for you, or wait for an admin to manually approve drivers before they're installed. Intune and the Windows Autopatch (DS) take care of the heavy lifting to identify the applicable driver updates for devices that are assigned a driver updates policy. For more information, see [Driver updates policy](../protect/windows-driver-updates-policy.md).

## Policy limitations for Workplace Joined devices

Microsoft introduced a cloud service as part of the Windows Update for Business product family, [Windows Autopatch](/windows/deployment/update/deployment-service-overview#capabilities-of-the-windows-update-for-business-deployment-service). As a cloud service, Windows Update for Business ds supports device update capabilities that require a device to have a Microsoft Entra registration (AADJ devices). These capabilities aren’t supported with Workplace Join (WPJ) devices. Windows update management on WPJ devices remains supported through core [Windows Update client policies](/windows/deployment/update/waas-manage-updates-wufb) capabilities and the Intune *Update rings for Windows 10 and later* policy type.

The following Intune policy types for Windows Updates use Windows Update for Business ds, which prevents their support on WPJ devices:

- Driver Updates for Windows 10 and later
- Feature Updates for Windows 10 and later
- Quality Updates for Windows 10 and later

If you support WPJ devices with Intune, the following information can help you understand the differences in capabilities based on policy type, for both WPJ devices and AADJ devices.

| Capability | Windows Update for Business </br> via Update Ring policy | Windows Update for Business-ds </br> via Driver, Feature, and Quality update policies|
|-|-|-|
| **WPJ device support**      | Yes                  | No                                           |
| **AADJ device support**     | Yes                  | Yes                                          |
| **Scan for Updates and Restart schedules** |  Yes  | Use Update Ring policies to manage schedules |
| **Enforce Update Deadlines**               | Yes   | Use Update Ring policies to enforce deadlines|
| **Control which updates to install** |***Feature***:  Yes </br>  - Defer *all* feature updates by specified days</br></br></br>***Quality***: Yes</br>  - Defer *all* quality updates by specified days</br></br>***Drivers***: Yes</br> - *Allow* or *Block* all *Recommended* drivers</br> - No support for *Other* drivers | ***Feature***:  Yes</br> - Manage *individual* updates</br>  - Specify *Start Date* or *Gradual Rollout* start and end dates. </br></br>  ***Quality***: Use Update Ring policies</br></br></br></br> ***Drivers***: Yes</br> - Manage individual *Recommended* and *Other* drivers. </br></br><!-- </br></br> - Recommended drivers: Per-update  *Allow* or  *Pause* of *Recommended* updates</br>  - Optional drivers: Per-update *Allow* or *Pause* of *Optional* updates</br></br>***Expedited Quality***: Yes    -->                 |
| **Pause Updates** | ***Feature***: </br>  - Pause all updates  </br></br>  ***Quality***: </br>  - Pause all updates </br></br>  ***Drivers***:  </br>  - Block all updates | ***Feature***: </br>  - Pause individual updates</br></br> ***Quality***: </br>  - Pause individual updates</br></br>***Drivers***: </br>  - Pause individual updates                                                                                 |
| **Expedite Quality Update** | No                   | Yes                                         |
| **Reports - Summary count of devices**: </br>  - Feature updates</br>  - Quality updates  | Windows Update for Business reports | Windows Update for Business reports |
| **Reports – Detailed status**:</br>  - Per Update  | Windows Update for Business reports  | Yes, in Intune              |

## Move from update ring deferrals to feature updates policy

When using Intune to manage Windows updates, it's possible to use both *update rings* policy with update deferrals, and *feature updates* policy to manage the updates you want to install on devices. If you're using feature updates, we recommend you end use of deferrals as configured in your update rings policy. Combining update ring deferrals with feature updates policy can create complexity that might delay update installations. You can continue to use the user experience settings from update rings, as they don't create issues when combined with feature updates policy.

While nothing prohibits use of both policy types to control which updates can install on a device, there's typically no advantage to doing so. When both policy types apply to a device, the conditions of both policy types must be met (be true) on the device before it's offered an applicable update. This scenario can lead to updates not installing as expected due to a block by one of the policy types.

### Plan to transition

Plan to manage the change from using update ring deferrals to feature updates so that the Windows Update service can be ready to deploy the updates you expect.

- When Intune policies for Windows updates are created or modified, Intune passes the policy details to Windows Update, which then determines the updates that are applicable for each device that's assigned one or more update policies.

- The process to evaluate updates for devices can take up to 10 minutes to complete, and in some cases might take a bit longer.

- If a device starts a scan for updates *after* a deferral has been set to zero or removed for the device, but *before* Windows Update completes the processing of the feature updates policy, that device can be offered an update you didn't plan for it to install.

Use the following process to ensure Windows Update has processed your feature updates policy before deferrals are removed.

#### Switch to feature updates policy

1. In the Microsoft Intune admin center, create a [feature updates policy](../protect/windows-10-feature-updates.md) that configures your desired Windows version, and assign it to applicable devices.

   After the saved policy is assigned to devices, it will take a few minutes for Windows Update to process the policy.

2. View the [Windows 10 feature updates (Organizational)](../protect/windows-update-reports.md#use-the-windows-10-feature-updates-organizational-report) report for the feature update policy, and verify devices have a state of **OfferReady** before you proceed. Once all devices show **OfferReady**, Windows Update has completed processing the policy.

3. After devices are verified to be in the **OfferReady** state you can safely reconfigure the [Windows 10 and later update ring policy](../protect/windows-10-update-rings.md), for that same set of devices to change the setting **Feature update deferral period (days)** to a value of **0**.

## Reporting on updates

To learn about report options for Update rings policy and Windows feature updates policy, see [Windows update reports](windows-update-reports.md).

## Next steps

- [Use Windows update rings](../protect/windows-10-update-rings.md)
- [Use Windows feature updates](../protect/windows-10-feature-updates.md)
- [Expedite quality updates](../protect/windows-10-expedite-updates.md)
- [Use Windows driver updates policy](../protect/windows-driver-updates-policy.md)
- For more information, see [Manage updates using Windows Update client policies](/windows/deployment/update/waas-manage-updates-wufb) in the Windows documentation.
