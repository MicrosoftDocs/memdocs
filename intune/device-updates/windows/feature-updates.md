---
title: Windows feature update releases
description: Learn about Windows feature update policy settings and how to create feature update releases in Microsoft Intune.
ms.date: 09/10/2024
ms.topic: how-to
ms.reviewer: davidmeb; bryanke; davguy
---

# Manage Windows feature updates

Windows feature updates are periodic releases that introduce new Windows capabilities, improvements, and changes to existing functionality. These updates typically ship once per year and represent a full operating system upgrade, such as moving a device from one Windows version to a newer release. Because feature updates can affect user experience, application compatibility, and device readiness, organizations often deploy them using controlled and phased rollouts.

In Microsoft Intune, Windows feature updates are managed through **feature updates policies**, which provide a dedicated policy surface for controlling which Windows version devices are offered and when that version can install. This policy uses cloud‑based update orchestration and can be used alongside other Windows update policies, such as quality updates and driver updates. Depending on your deployment model, feature updates may be managed manually through Intune or automatically through Windows Autopatch. Client‑side update behavior—such as restart experience and installation timing—continues to be influenced by standard Windows Update policy settings, including [update rings](update-rings.md) and [Windows Update client policies](/windows/deployment/update/waas-configure-wufb).

Feature updates policies allow you to **lock devices to a specific Windows release** or **target an upgrade to a newer version** while preventing devices from moving beyond that version. This approach helps ensure version compliance, reduce unexpected upgrades, and coordinate OS updates with application readiness and organizational rollout plans.

## Prerequisites

[!INCLUDE [prerequisites-network](includes/prerequisites-network.md)]
[!INCLUDE [prerequisites-tenant](includes/prerequisites-tenant.md)]
[!INCLUDE [prerequisites-licensing](includes/prerequisites-licensing.md)]
[!INCLUDE [prerequisites-platform](includes/prerequisites-platform.md)]
[!INCLUDE [prerequisites-device-configuration](includes/prerequisites-device-configuration.md)]
[!INCLUDE [prerequisites-rbac](includes/prerequisites-rbac.md)]

---

<!--
With Microsoft Intune, you can create and deploy policy settings that ensure your Windows devices remain on a specific Windows feature update version. These settings help you manage and control the feature set of Windows on your devices, providing stability and predictability for your organization's IT environment.

With Windows feature updates policies, you can:

- Select the Windows [feature update](/windows/deployment/update/get-started-updates-channels-tools#types-of-updates) version that you want devices to remain at. This option supports setting a feature level to any version that remains in support at the time you create the policy.
- [Upgrade devices that run Windows 10 to Windows 11](feature-updates-windows-10.md).

Windows feature updates policies work with update rings policies to prevent a device from receiving a Windows feature version that's later than the value specified in the feature updates policy.
-->
