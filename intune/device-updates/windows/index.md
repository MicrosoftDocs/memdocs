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

The following policy types help you manage Windows updates in Intune:

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
>Delivers monthly cumulative updates for security and reliability. Supports:
>- Expedited updates: Push critical fixes immediately by overriding deferrals and deadlines.
>- Hotpatch: Apply eligible security patches without reboot to reduce downtime.
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
:::column-end:::
:::row-end:::

## Windows Autopatch

Windows Autopatch is a managed cloud service integrated with Intune. It doesn't introduce new policy types—instead, it automates and orchestrates existing Intune update policies using the same backend service. Autopatch adds advanced capabilities such as dynamic device grouping, phased rollout, health monitoring, and compliance reporting. It also enables cloud-powered features like Hotpatch for eligible Windows 11 Enterprise editions and expedited delivery of critical updates, without requiring manual configuration.

The following table compares how update management differs when you use Autopatch and manual Intune configuration:

| **Feature** | **When NOT using Autopatch** | **When using Autopatch** |
|--|--|--|
| **Update coordination** | You control scheduling, deferrals, and rollout manually. | Autopatch orchestrates update rings, feature updates, drivers, and quality updates automatically. |
| **Update rings** | You configure update rings in Intune to control deferrals, deadlines, and restart behavior. | Autopatch creates and manages its own rings; don't assign custom rings to Autopatch devices. |
| **Feature updates** | You use feature updates policies to lock or schedule OS versions. | Autopatch manages version targeting and rollout automatically. |
| **Quality updates** | You configure quality updates policies, expedited updates, and optionally enable Hotpatch through quality update settings. | Autopatch manages monthly patches, expedites critical updates, and applies Hotpatch automatically for eligible devices. |
| **Driver updates** | You use driver updates policy for granular control. | Autopatch manages driver approvals and scheduling automatically. |

> [!div class="nextstepaction"]
> [Learn more about Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview)

## Prerequisites

Each policy type has specific prerequisites, detailed in their respective documentation. In general:

- Devices must be enrolled in Intune.
- Devices must be Microsoft Entra joined or hybrid joined.\
  Microsoft Entra registered devices aren't supported for any policy type that uses the same backend service as Windows Autopatch—including Feature updates, Quality updates, and Driver updates.\
  For Entra registered devices, update management remains limited to Windows Update client policies and update rings policies.
- Devices must have access to Microsoft update endpoints.

Feature update policies, quality update policies, and driver update policies use the same cloud orchestration layer as Windows Autopatch. Autopatch automates these policies, but when you configure them manually in Intune, you're still calling the same backend service—so the requirements don't change. Because they share this service, the prerequisites are the same across these three policy types:

- Licensing: A Windows license that includes the [Autopatch entitlement](/windows/deployment/windows-autopatch/prepare/windows-autopatch-prerequisites#licenses-and-entitlements).
- Telemetry: Diagnostic data set to *Required* level.
- Services: Microsoft Account Sign-In Assistant enabled.\
  If the service is blocked or set to *Disabled*, it fails to receive the update. For more information, see [Feature updates aren't being offered while other updates are](/windows/deployment/update/windows-update-troubleshooting#feature-updates-are-not-being-offered-while-other-updates-are). By default, the service is set to *Manual (Trigger Start)*, which allows it to run when needed.
