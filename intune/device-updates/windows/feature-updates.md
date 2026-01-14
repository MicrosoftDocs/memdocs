---
title: Manage Windows Feature Updates
description: Learn how to use Microsoft Intune policies to manage Windows feature updates.
ms.date: 01/14/2026
ms.topic: how-to
ms.reviewer: davidmeb; bryanke; davguy
---

# Manage Windows feature updates

Windows feature updates are periodic releases that introduce new Windows capabilities, improvements, and changes to existing functionality. These updates typically ship once per year and represent a full operating system upgrade, such as moving a device from one Windows version to a newer release. Because feature updates can affect user experience, application compatibility, and device readiness, organizations often deploy them using controlled and phased rollouts.

In Microsoft Intune, Windows feature updates are managed through **feature updates policies**, which provide a dedicated policy surface for controlling which Windows version devices are offered and when that version can install. This policy uses cloud‑based update orchestration and can be used alongside other Windows update policies, such as quality updates and driver updates. Depending on your deployment model, feature updates may be managed manually through Intune or automatically through Windows Autopatch. Client‑side update behavior—such as restart experience and installation timing—continues to be influenced by standard Windows Update policy settings, including [update rings](update-rings.md) and [Windows Update client policies](/windows/deployment/update/waas-configure-wufb).

Feature updates policies allow you to **lock devices to a specific Windows release** or **target an upgrade to a newer version** while preventing devices from moving beyond that version. This approach helps ensure version compliance, reduce unexpected upgrades, and coordinate OS updates with application readiness and organizational rollout plans.

## Prerequisites

[!INCLUDE [prerequisites-network](includes/prerequisites-network.md)]
[!INCLUDE [prerequisites-cloud](includes/prerequisites-cloud.md)]
[!INCLUDE [prerequisites-tenant](includes/prerequisites-tenant.md)]
[!INCLUDE [prerequisites-licensing](includes/prerequisites-licensing.md)]
[!INCLUDE [prerequisites-platform](includes/prerequisites-platform.md)]
[!INCLUDE [prerequisites-device-configuration](includes/prerequisites-device-configuration.md)]
[!INCLUDE [prerequisites-rbac](includes/prerequisites-rbac.md)]

<!--
## Plan for feature updates policies

When planning your feature updates policies, consider the following guidance:

- If you deploy a feature updates policy to a device that is also targeted by an update ring policy, review the update ring for the following configurations:
  - We recommend setting the **Feature update deferral period (days)** to **0**. This configuration ensures your feature updates aren't delayed by update deferrals that might be configured in an update ring policy. For more information, see [Move from update ring deferrals to feature updates policy](feature-updates-policy.md#move-from-update-ring-deferrals-to-feature-updates-policy).
  - Feature updates for the update ring must be *running*. They must not be paused.
- Windows feature updates policies can't be applied during the Windows Autopilot out of box experience (OOBE). Instead, the policies apply at the first Windows Update scan after a device has finished provisioning, which is typically a day.
- When the device checks in to the Windows Update service, the device's group membership is validated against the security groups assigned to the feature updates policy settings for any feature update holds.
- Managed devices that receive feature update policy are automatically enrolled with [Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview). The service manages the updates a device receives. Microsoft Intune uses this service and works with your Intune policies for Windows updates to deploy feature updates to devices.
- When a device is no longer assigned to any feature update policies, the device remains enrolled in Autopatch. This change allows time to assign the device to a different policy and ensure that in the meantime the device doesn't receive a feature update that wasn't intended.\
  As a result, when a feature updates policy no longer applies to a device, that device isn't offered any feature update until one of the following happens:
  - The device is assigned to a new feature update profile.
  - The device is unenrolled from Intune, which unenrolls the device from feature update management by Autopatch.
  - You use the [Windows Autopatch graph API](/graph/windowsupdates-enroll) to [remove the device](/graph/api/windowsupdates-updatableasset-unenrollassets) from feature update management.
-->

## Plan feature update deployments

When planning feature update deployments, consider how feature update policies interact with other Windows update settings and services in your tenant.

### Interaction with update rings

If a device is targeted by both a feature update policy and an update ring policy, review the update ring configuration to avoid unintended delays:

- Set **Feature update deferral period (days)** to **0** so deferrals in update rings don't delay feature updates controlled by the feature update policy. For more information, see [Move from update ring deferrals to feature updates policy](feature-updates-policy.md#move-from-update-ring-deferrals-to-feature-updates-policy).
- Ensure feature updates in the update ring aren't paused.

Client‑side behaviors such as restart experience, deadlines, and active hours continue to be governed by update rings and Windows Update client settings.

### Deployment timing and enforcement

Feature update policies don't apply during Windows Autopilot out‑of‑box experience (OOBE). Instead, they take effect at the first Windows Update scan after provisioning is complete.

When devices check in with the Windows Update service, group membership is evaluated against the security groups assigned to feature update policies. Any configured holds are enforced during this evaluation.

### Working with Windows Autopatch

Feature update policies can be used on their own or as part of Windows Autopatch. In Autopatch‑managed environments, the service uses feature update policies to coordinate controlled and phased OS upgrades.

If a device managed by Autopatch is no longer targeted by a feature update policy, the device remains enrolled in Autopatch. This behavior helps prevent unintended upgrades while administrators adjust policy targeting or deployment plans.

## Next steps

> [!div class="nextstepaction"]
> [Learn how to configure feature updates policies](featrure-updates-policy.md)


<!-->
Toadd: 

Feature update policies support scheduled and gradual deployments using rollout options. For details on configuring rollout timing, see Rollout options for Windows Updates.-->