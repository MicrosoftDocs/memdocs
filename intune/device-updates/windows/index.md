---
title: Windows update management overview
description: Learn how Microsoft Intune helps you manage Windows updates for your organization.
ms.date: 12/16/2025
ms.topic: overview
---

# Windows update management overview

Keeping Windows devices secure and up to date is one of the most important responsibilities for any organization. Intune provides a **cloud-based approach to Windows update management**, giving you control, predictability, and minimal disruption for users.

This overview explains how Intune manages Windows updates, the policy types available, and how these pieces fit together into a complete update strategy.

## What you can do with Intune

- Configure update settings on devices without managing individual patches.
- Define update rings to control rollout timing and reduce risk.
- Prevent devices from installing new feature versions until you're ready, while still applying security and quality updates.

Intune stores only the policy assignments, not the updates themselves. When you save a policy, Intune sends configuration details to Windows Update, which determines which updates to offer. Devices download updates directly from Windows Update.

## Windows update management capabilities

The following policy types and features help you manage Windows updates in Intune:

:::row:::
:::column:::

#### Windows Update client policy

>**:::image type="icon" source="icons/client-policy.svg" border="false":::** 
>
> Configures the underlying [Update policy CSP](/windows/client-management/mdm/policy-csp-update). Intune surfaces these settings through update rings and the Settings Catalog, giving administrators flexibility to apply granular update behaviors at the device level.
>
>> [!div class="nextstepaction"]
>> [Learn more](/windows/deployment/update/waas-configure-wufb)

:::column-end:::
:::column:::
#### Update rings policy

>**:::image type="icon" source="icons/update-ring.svg" border="false":::**    
>
> Applies Windows Update client policies to groups of devices. Update rings control deferral periods, deadlines, restart behavior, and user experience settings, enabling phased rollout across your environment.
>
>> [!div class="nextstepaction"]
>> [Learn more](update-rings.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::
#### Feature updates policy

>**:::image type="icon" source="icons/feature-updates.svg" border="false":::** 
>
> Locks devices to a specific Windows version (for example, Windows 11 24H2). These policies prevent devices from upgrading beyond the targeted release, ensuring consistency and control over major OS upgrades.
>
>> [!div class="nextstepaction"]
>> [Learn more](feature-updates.md)
:::column-end:::

:::column:::
#### Quality updates policy

>**:::image type="icon" source="icons/quality-updates.svg" border="false":::**
>
> Delivers monthly cumulative updates that include security patches and reliability improvements, keeping devices secure and stable on a regular cadence. This policy also supports expedited updates, which override deferrals and deadlines to push critical security fixes faster than normal rings.
>
>> [!div class="nextstepaction"]
>> [Learn more](quality-updates.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::
#### Driver updates policy

**:::image type="icon" source="icons/driver-update.svg" border="false":::** 

> Manages the delivery of hardware driver updates from Windows Update. Driver update policies help ensure device compatibility and stability by controlling when and how drivers are installed.
>
>> [!div class="nextstepaction"]
>> [Learn more](feature-updates.md)
:::column-end:::
:::column:::

#### Hotpatch updates

**:::image type="icon" source="icons/hotpatch-updates.svg" border="false":::**

> Applies security patches without requiring a reboot, reducing downtime. Hotpatch is available for eligible Windows editions and is managed through Windows Autopatch or quality update settings, not as a separate Intune policy.
>
>> [!div class="nextstepaction"]
>> [Learn more](update-rings.md)
:::column-end:::
:::row-end:::

## Windows Autopatch

Windows Autopatch is a managed cloud service built on the *Windows Update for Business Deployment Service (WUfB DS)* and integrated with Intune. It doesn't introduce new policy types—instead, it automates and orchestrates existing Intune update policies using the same backend service. Autopatch adds advanced capabilities such as dynamic device grouping, phased rollout, health monitoring, and compliance reporting. It also enables cloud-powered features like Hotpatch for eligible Windows 11 Enterprise editions and expedited delivery of critical updates, without requiring manual configuration.

The following table compares how update management differs when you use Autopatch and manual Intune configuration:

| **Feature**             | **When NOT using Autopatch**                                                                | **When using Autopatch**                                                                          |
|-------------------------|---------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **Update coordination** | You control scheduling, deferrals, and rollout manually.                                    | Autopatch orchestrates update rings, feature updates, drivers, and quality updates automatically. |
| **Update rings**        | You configure update rings in Intune to control deferrals, deadlines, and restart behavior. | Autopatch creates and manages its own rings; don't assign custom rings to Autopatch devices.      |
| **Feature updates**     | You use feature updates policies to lock or schedule OS versions.                           | Autopatch manages version targeting and rollout automatically.                                    |
| **Quality updates**     | You configure quality updates policies and expedited update policies.                       | Autopatch expedites critical updates and manages monthly patches.                                 |
| **Driver updates**      | You use driver updates policy for granular control.                                         | Autopatch manages driver approvals and scheduling automatically.                                  |
| **Hotpatch**            | Enabled through quality update settings; timing follows your update ring configuration.     | Applied automatically for eligible devices; Autopatch coordinates timing with its rings.          |


> [!div class="nextstepaction"]
> [Learn more about Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview)

## Prerequisites

Each policy type has its own prerequisites, which the respective documentation details. In general:

- Devices must be enrolled in Intune.
- Devices must be Microsoft Entra joined or hybrid joined.
- Devices must be able to access the Microsoft update endpoints.

Feature updates, quality updates, driver updates, and Hotpatch rely on the same backend service as Autopatch: the Windows Update for Business Deployment Service (WUfB DS). Autopatch simply automates these policies for you, but when you configure them manually in Intune, you're still calling the same service—so the requirements don't change. Because they use the same cloud orchestration layer, the prerequisites are identical:

- Licensing: Windows Enterprise E3/E5 (or equivalent) for access to WUfB DS capabilities.
- Telemetry: Diagnostic data set to Required level.
- Services: Microsoft Account Sign-In Assistant (wlidsvc) enabled.

## Policy limitations for Workplace Joined devices

Microsoft introduced a cloud service as part of the Windows Update product family, [Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview). As a cloud service, Windows Autopatch supports device update capabilities that require a device to be Microsoft Entra joined. These capabilities aren't supported on Microsoft Entra registered devices: Windows update management on such devices remains supported through core [Windows Update client policies](/windows/deployment/update/waas-manage-updates-wufb) capabilities and update rings.

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