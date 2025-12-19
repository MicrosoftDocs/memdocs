---
title: Learn about using Windows Update client policies in Microsoft Intune
description: Manage Windows software updates by using Intune policy for Update rings for Windows and Windows feature updates for Windows Update client policies in Microsoft Intune.
ms.date: 02/27/2025
ms.topic: overview
ms.reviewer: davidmeb; bryanke; davguy
---

# Manage Windows software updates in Intune

Use Microsoft Intune to manage the install of Windows software updates from Windows Update client policies.

> [!TIP]
> This feature was formerly known as *Windows Update for Business*.

By using Windows Update client policies, you simplify the update management experience. You don't need to approve individual updates for groups of devices and can manage risk in your environments by configuring an update rollout strategy. With Intune, you can [configure update settings](settings.md) on devices and configure deferral of update installation. You can also prevent devices from installing features from new Windows versions to help keep them stable, while allowing those devices to continue installing updates for quality and security.

Intune stores only the update policy assignments, not the updates themselves. When you save a policy, Intune passes the configuration details to Windows Update, which then determines which of these updates are offered to each device. Devices access Windows Update directly for the updates.

Learn more about Windows [*feature* and *quality* updates](/windows/deployment/update/get-started-updates-channels-tools#types-of-updates) in the Windows documentation.

## Policy types to manage updates

Intune provides the following policy types to manage updates, which you assign to groups of devices:

- **Update rings**: This policy is a collection of settings that configures when Windows updates get installed. For more information, see [Update rings policy](update-rings.md).

- **Feature updates policies**: The [feature updates polcies](feature-updates.md) update devices to the Windows version that you specify, and then freezes the feature set version on those devices. This version freeze remains in place until you choose to update them to a later Windows version. While the feature version remains static, devices can continue to install quality and security updates that are available for their feature version.

  You can also use Feature updates policy to [upgrade your devices that run Windows 10 to Windows 11](feature-updates.md#upgrade-devices-to-windows-11).

- **Quality updates policies**: With Quality updates policies, also referred to as Expedited updates, you can expedite the install of the most recent security updates on devices that you manage with Microsoft Intune. Expedited install is accomplished without the need to pause or edit your existing monthly servicing policies. For more information, see [Expedite updates policy](expedite-updates.md).

- **Driver updates policies**: With Windows Driver Update Management in Microsoft Intune, you can review, approve for deployment and pause deployments of driver updates for your managed Windows devices. Your policies can automatically install the newest recommended driver for you, or wait for an admin to manually approve drivers before they're installed. Intune and the Windows Autopatch take care of the heavy lifting to identify the applicable driver updates for devices that are assigned a driver updates policy. For more information, see [Driver updates policy](driver-updates-policy.md).

## Policy limitations for Workplace Joined devices

Microsoft introduced a cloud service as part of the Windows Update product family, [Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview). As a cloud service, Windows Autopatch supports device update capabilities that require a device to have a Microsoft Entra registration (AADJ devices). These capabilities aren't supported with Workplace Join (WPJ) devices. Windows update management on WPJ devices remains supported through core [Windows Update client policies](/windows/deployment/update/waas-manage-updates-wufb) capabilities and the Intune *Update rings* policy type.

The following Intune policy types for Windows Updates use Windows Autopatch, which prevents their support on WPJ devices:

- Driver Updates
- Feature Updates
- Quality Updates

If you support WPJ devices with Intune, the following information can help you understand the differences in capabilities based on policy type, for both WPJ devices and AADJ devices.

| Capability | Windows Update client policies </br> via Update Ring policy | Windows Autopatch </br> via Driver, Feature, and Quality update policies|
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

## Reporting on updates

To learn about report options for Update rings policy and Windows feature updates policy, see [Windows update reports](reports.md).

## Next steps

- [Use Windows update rings](update-rings.md)
- [Use Windows feature updates](feature-updates.md)
- [Expedite quality updates](expedite-updates.md)
- [Use Windows driver updates policy](driver-updates-policy.md)
- For more information, see [Manage updates using Windows Update client policies](/windows/deployment/update/waas-manage-updates-wufb) in the Windows documentation.
