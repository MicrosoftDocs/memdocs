---
title: Manage Windows Feature Updates
description: Learn how to use Microsoft Intune policies to manage Windows feature updates.
ms.date: 01/14/2026
ms.topic: how-to
ms.reviewer: davidmeb; bryanke; davguy
---

# Manage Windows feature updates

Windows feature updates are periodic releases that introduce new Windows capabilities, improvements, and changes to existing functionality. These updates typically ship once per year and represent a full operating system upgrade, such as moving a device from one Windows version to a newer release. Because feature updates can affect user experience, application compatibility, and device readiness, organizations often deploy them using controlled and phased rollouts.

In Microsoft Intune, Windows feature updates are managed through **feature update policies**, which provide a dedicated policy surface for controlling which Windows version devices are offered and when that version can install. This policy uses cloud‑based update orchestration and can be used alongside other Windows update policies, such as quality updates and driver updates. Depending on your deployment model, feature updates may be managed manually through Intune or automatically through Windows Autopatch. Client‑side update behavior—such as restart experience and installation timing—continues to be influenced by standard Windows Update policy settings, including [update rings](update-rings.md) and [Windows Update client policies](/windows/deployment/update/waas-configure-wufb).

Feature update policies allow you to **lock devices to a specific Windows release** or **target an upgrade to a newer version** while preventing devices from moving beyond that version. This approach helps ensure version compliance, reduce unexpected upgrades, and coordinate OS updates with application readiness and organizational rollout plans.

## Prerequisites

[!INCLUDE [prerequisites-network](includes/prerequisites-network.md)]
[!INCLUDE [prerequisites-cloud](includes/prerequisites-cloud.md)]
[!INCLUDE [prerequisites-tenant](includes/prerequisites-tenant.md)]
[!INCLUDE [prerequisites-licensing](includes/prerequisites-licensing.md)]
[!INCLUDE [prerequisites-platform](includes/prerequisites-platform.md)]
[!INCLUDE [prerequisites-device-configuration](includes/prerequisites-device-configuration.md)]
[!INCLUDE [prerequisites-rbac](includes/prerequisites-rbac.md)]

## Plan feature update deployments

When planning feature update deployments, consider how feature update policies interact with other Windows update settings and services in your tenant.

### Interaction with update rings

If a device is targeted by both a feature update policy and an update ring policy, review the update ring configuration to avoid unintended delays:

- Set **Feature update deferral period (days)** to **0** so deferrals in update rings don't delay feature updates controlled by the feature update policy. For more information, see [Move from update ring deferrals to feature update policies](feature-update-policy.md#move-from-update-ring-deferrals-to-feature-update-policies).
- Ensure feature updates in the update ring aren't paused.
- Client‑side behaviors such as restart experience, deadlines, and active hours continue to be governed by update rings and Windows Update client settings.

### Deployment timing and enforcement

Feature update policies don't apply during Windows Autopilot out‑of‑box experience (OOBE). Instead, they take effect at the first Windows Update scan after provisioning is complete.

When devices check in with the Windows Update service, group membership is evaluated against the security groups assigned to feature update policies. Any configured holds are enforced during this evaluation.

Feature update policies also support scheduled and gradual deployments using rollout options. For details on configuring rollout timing, see [Rollout options for Windows Updates](rollout-options.md).

### Working with Windows Autopatch

Feature update policies can be used on their own or as part of Windows Autopatch. In Autopatch‑managed environments, the service uses feature update policies to coordinate controlled and phased OS upgrades.

If a device managed by Autopatch is no longer targeted by a feature update policy, the device remains enrolled in Autopatch. This behavior helps prevent unintended upgrades while administrators adjust policy targeting or deployment plans.

As a result, when a feature update policy no longer applies to a device, that device isn't offered any feature update until one of the following happens:
  - The device is assigned to a new feature update profile.
  - The device is unenrolled from Intune, which unenrolls the device from feature update management by Autopatch.
  - You use the [Windows Autopatch graph API](/graph/windowsupdates-enroll) to [remove the device](/graph/api/windowsupdates-updatableasset-unenrollassets) from feature update management.

## Next steps

> [!div class="nextstepaction"]
> [Learn how to manage Windows feature update policies](feature-update-policy.md)
