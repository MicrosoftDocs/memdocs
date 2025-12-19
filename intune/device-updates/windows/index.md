---
title: Manage Windows updates with Microsoft Intune
description: Learn how Microsoft Intune helps you manage Windows updates for your organization.
ms.date: 12/16/2025
ms.topic: overview
---

# Manage Windows updates with Microsoft Intune

Keeping Windows devices secure and up to date is one of the most important responsibilities for any organization. Microsoft Intune offers a modern, cloud‑based approach to managing Windows Update client policies so you can deliver updates with control, predictability, and minimal disruption to your users.
This overview introduces how Intune manages Windows updates, the policy types you can use, and how these pieces fit together into a complete update strategy.

How Intune manages Windows updates
Intune integrates with Windows Update for Business to configure how and when Windows 10 and Windows 11 devices receive updates. Rather than downloading and approving individual patches (as you would in WSUS), Intune defines update behavior through policy. Devices then communicate directly with the Windows Update service to retrieve the correct updates.
With Intune, you can manage:

All Windows updates flow from Microsoft's global update service; Intune provides the policy layer that governs timing, user experience, and safeguards.

## Windows update management in Intune

Intune provides a comprehensive set of policies to manage how Windows devices receive updates. These policies control everything from the underlying Windows Update client behavior to the rollout of feature updates, monthly quality patches, and driver updates. Intune also supports advanced capabilities like expedited delivery of critical security fixes and Hotpatch for eligible editions, which applies updates without rebooting. Each policy type serves a specific purpose, giving administrators flexibility to design update strategies that balance security, stability, and user experience. Understanding how these policies and features relate to one another is essential for building a predictable and well‑governed update management process.

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
> Delivers monthly cumulative updates that include security patches and reliability improvements, keeping devices secure and stable on a regular cadence. This policy also supports expedited updates, which override deferrals and deadlines to push critical security fixes (such as zero-day patches) faster than normal rings.
>
>> [!div class="nextstepaction"]
>> [Learn more](quality-updates-policy.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::

:::column:::
#### Driver updates policy

**:::image type="icon" source="icons/driver-update.svg" border="false":::** 

> Manages the delivery of hardware driver updates from Windows Update. Driver update policies help ensure device compatibility and stability by controlling when and how drivers are installed.
>
>> [!div class="nextstepaction"]
>> [Learn more](feature-updates.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::

#### Hotpatch updates

**:::image type="icon" source="icons/hotpatch-updates.svg" border="false":::**

> A Windows update mechanism that applies security patches without requiring a reboot, reducing downtime. Hotpatch is available for eligible Windows editions and is managed through Windows Autopatch or quality update settings, not as a separate Intune policy.
>
>> [!div class="nextstepaction"]
>> [Learn more](update-rings.md)
:::column-end:::
:::column:::

:::column-end:::
:::row-end:::

## Windows Autopatch

Windows Autopatch is a cloud service that automates the management of Windows updates using Intune. Instead of manually configuring update rings, feature update policies, quality updates, driver updates, and hotpatching, Autopatch orchestrates these policies on your behalf. The service applies Microsoft-recommended deployment rings, monitors update health, and automatically adjusts rollout based on device readiness and reliability signals. Autopatch reduces administrative overhead while maintaining a secure and up‑to‑date device fleet.

> [!div class="nextstepaction"]
> [Learn more about Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview)

---

Intune provides several policy types, each designed for a specific purpose. Understanding these helps you choose the right tool for each scenario.
Update rings
Update rings control the cadence and experience of updates, including:

Deferral periods for quality and feature updates
Deadlines and grace periods
Restart behavior and active hours

Use update rings to set your baseline update behavior and to create staged deployment groups (for example: Pilot → Broad).
Feature updates policy
Feature updates policies let you lock devices to a specific Windows version (for example, stay on 22H2) until you choose to upgrade.
Use this when you want predictable OS version targeting, regardless of ring deferrals.
Quality updates (expedite) policy
Expedite policies push a specific quality update as soon as possible to remediate critical vulnerabilities. These settings override deferrals and deadlines in update rings.
Use this only for urgent or zero‑day scenarios.
Driver and firmware updates
Intune can manage whether devices receive driver and firmware updates from Windows Update. You can choose to enable, disable, or selectively allow drivers depending on your device ecosystem.
Windows Autopatch
Windows Autopatch is a managed service that automates the update rollout process. Autopatch uses update rings behind the scenes, creates its own deployment groups, and orchestrates updates for you.
Use Autopatch when you prefer Microsoft to manage update sequencing, validation, and rollout, instead of maintaining your own rings and schedules.
Hotpatch
Hotpatch is a servicing mechanism that delivers certain security updates without requiring a reboot. Intune does not configure hotpatch directly, but devices that support hotpatch continue to use Intune's update policies for timing and coordination.

How the pieces fit together
Intune's Windows update management is designed as a layered system, where each policy type handles a specific need:

Update rings → set the baseline scheduling and user experience
Feature updates → control the Windows version
Expedite updates → override schedules for urgent patches
Driver policies → manage hardware‑level updates
Autopatch → optional automation layer that manages the above for you

These policies are complementary. For example, you can assign update rings for routine monthly updates while using a feature updates policy to pin devices to 23H2 until you approve an upgrade.

What you can do with Intune
With Intune, organizations can:

Standardize Windows update behavior across all devices
Stage updates using rings or Autopatch deployment groups
Control when devices move to a new Windows version
Push emergency patches during high‑risk situations
Reduce user disruption with controlled reboot experiences
Monitor update compliance across the fleet
Troubleshoot devices that fall behind or fail to apply updates

Intune gives you the flexibility to adopt a simple, fully automated model or a highly controlled, staged approach — whichever fits your operational needs.

Next steps
Use the rest of the articles in this section to explore each policy type in more depth:

Plan your update strategy
Configure update rings
Deploy feature update targeting
Expedite critical updates
Manage driver and firmware updates
Use Windows Autopatch
Understand hotpatching scenarios
Monitor and troubleshoot update compliance


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