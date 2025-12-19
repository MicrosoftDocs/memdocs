---
title: Manage Windows updates with Microsoft Intune
description: Learn how Microsoft Intune helps you manage Windows updates for your organization.
ms.date: 12/16/2025
ms.topic: overview
---

# Manage Windows updates with Microsoft Intune

Keeping Windows devices secure and up to date is one of the most important responsibilities for any organization. Microsoft Intune offers a cloud‑based approach to managing Windows updates so you can deliver updates with control, predictability, and minimal disruption to your users. This overview introduces how Intune manages Windows updates, the policy types you can use, and how these pieces fit together into a complete update strategy.

## Windows update management capabilities

Intune provides a comprehensive set of policies and features to manage how Windows devices receive updates. These capabilities control everything from the underlying Windows Update client behavior to the rollout of feature updates, monthly quality patches, and driver updates. Intune also supports advanced options like expedited delivery of critical security fixes and Hotpatch for eligible editions, available through Windows Autopatch or quality update settings, which applies updates without rebooting. Each policy type serves a specific purpose, giving administrators flexibility to design update strategies that balance security, stability, and user experience. Understanding how these policies and features relate to one another is essential for building a predictable and well‑governed update management process.

:::row:::
:::column:::

#### Windows Update client policies

>**:::image type="icon" source="icons/client-policies.svg" border="false":::** 
>
> Windows Update client policies (formerly known as Windows Update for Business) configure the underlying [Update policy CSP](/windows/client-management/mdm/policy-csp-update). Intune surfaces these settings through update rings and the Settings Catalog, giving administrators flexibility to apply granular update behaviors at the device level.
>
>> [!div class="nextstepaction"]
>> [Learn more](/windows/deployment/update/waas-configure-wufb)

:::column-end:::
:::column:::
#### Update rings policy

>**:::image type="icon" source="icons/update-ring.svg" border="false":::**    
>
> Intune's management object that applies Windows Update client policies to groups of devices. Update rings control deferral periods, deadlines, restart behavior, and user experience settings, enabling phased rollout across your environment.
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
>> [Learn more](quality-updates-policy.md)
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

> A Windows update mechanism that applies security patches without requiring a reboot, reducing downtime. Hotpatch is available for eligible Windows editions and is managed through Windows Autopatch or quality update settings, not as a separate Intune policy.
>
>> [!div class="nextstepaction"]
>> [Learn more](update-rings.md)
:::column-end:::
:::row-end:::

## Windows Autopatch

Windows Autopatch is a cloud service that integrates with Intune to automate update deployment for Windows Enterprise devices. It doesn't introduce new policy types—instead, it orchestrates existing Intune policies and adds advanced capabilities like dynamic device grouping, phased rollout, and compliance reporting. Autopatch also enables features such as Hotpatch for eligible editions and expedited delivery of critical updates.

### Policy types and Autopatch integration

| **Policy type** | **How Autopatch uses it** | **Additional capabilities Autopatch adds** |
| --- | --- | --- |
| **Update rings policy** | Applies Windows Update client settings to device groups. Autopatch organizes devices into rings automatically. | Dynamic ring assignment, phased rollout scheduling, and health monitoring. |
| **Feature updates policy** | Locks devices to a specific Windows version. Autopatch manages feature update deployment and readiness checks. | Automated rollout and reporting for feature updates. |
| **Quality updates policy** | Delivers monthly cumulative updates. Autopatch ensures timely deployment and can expedite critical patches. | Expedited updates for zero-day fixes and Hotpatch support for eligible editions. |
| **Driver updates policy** | Controls delivery of hardware driver updates. Autopatch includes driver and firmware updates in its orchestration. | Approval workflows and staged deployment for drivers and firmware. |

> [!NOTE]
> Autopatch requires Windows Enterprise E3/E5 (or equivalent Microsoft 365 plans). Intune policies work without Autopatch, but Autopatch adds automation, orchestration, and reporting for enrolled devices.


> [!div class="nextstepaction"]
> [Learn more about Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview)

---

|                                                                                | Feature                        | When using Autopatch                                                                             | When NOT using Autopatch                                                                         |
|--------------------------------------------------------------------------------|--------------------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| **:::image type="icon" source="icons/update-ring.svg" border="false":::**      | Update rings                   | Autopatch creates & manages its own rings; you shouldn't assign your own to these devices        | You configure your own update rings in Intune                                                    |
| **:::image type="icon" source="icons/feature-updates.svg" border="false":::**  | Feature update policies        | Autopatch manages version targeting                                                              | You use Intune's Feature updates policy                                                          |
| **:::image type="icon" source="icons/expedite-updates.svg" border="false":::** | Quality expedite updates       | Autopatch handles emergency patching                                                             | You use "Expedite" policy                                                                        |
| **:::image type="icon" source="icons/driver-update.svg" border="false":::**   | Driver updates                 | Autopatch manages this                                                                           | You can allow/deny via settings                                                                  |
| ****                                                                           | Update coordination            | Autopatch orchestrates everything                                                                | You control scheduling & behavior                                                                |
| **:::image type="icon" source="icons/hotpatch-updates.svg" border="false":::** | Hotpatch                       | Devices that support hotpatch continue to use Intune's update policies for timing & coordination | Devices that support hotpatch continue to use Intune's update policies for timing & coordination |
| **:::image type="icon" source="icons/client-policies.svg" border="false":::**  | Windows Update client policies | Intune configures these behind the scenes; you don't assign your own to Autopatch devices        | You configure these directly in Intune                                                           |
| **:::image type="icon" source="icons/quality-updates.svg" border="false":::**  | Quality updates                | Autopatch manages quality updates                                                                | You configure quality updates via update rings and expedite policies                             |


---

<!--from configure.md (deleted)-->

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