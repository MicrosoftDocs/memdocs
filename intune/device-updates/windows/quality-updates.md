---
title: Manage Windows quality updates
description: Learn how to manage Windows quality updates in Microsoft Intune using quality update policies, expedited updates, and hotpatch to keep devices secure and compliant.
ms.date: 01/06/2026
ms.reviewer: mobattul
ms.topic: how-to
---

# Manage Windows quality updates

Windows quality updates are the regular Windows servicing updates that keep devices secure, reliable, and supported. These updates are released frequently—typically monthly—and include security fixes, non‑security improvements, and reliability enhancements. Because quality updates are cumulative, installing the latest update brings a device fully up to date for its currently installed Windows version.

In Microsoft Intune, you manage Windows quality updates through **quality update policies**. These policies provide a dedicated policy surface for targeting specific quality updates, and use cloud‑based update orchestration to deploy those updates to devices. Quality update policies work alongside other Windows update policies—such as **feature updates policies** and **driver updates policies**—and can be managed directly in Intune or automatically through **Windows Autopatch**, depending on your deployment model.

Quality update policies support targeted deployment scenarios for Windows quality updates. You can use them to **expedite updates** and accelerate the installation of critical or security updates when standard deployment timelines aren't acceptable. For eligible Windows editions and device configurations, you can also enable **hotpatch**, which installs certain security updates without requiring an immediate device restart—helping balance rapid protection, deployment control, and end‑user experience.

Client‑side update behavior—such as restart settings, deadlines, notifications, and deferral periods—continues to be configured through **update rings** and **Windows Update client policies**, which together with quality update policies complete the end‑to‑end update experience on devices.

## Prerequisites

[!INCLUDE [prerequisites-network](includes/prerequisites-network.md)]
[!INCLUDE [prerequisites-cloud](includes/prerequisites-cloud.md)]
[!INCLUDE [prerequisites-tenant](includes/prerequisites-tenant.md)]
[!INCLUDE [prerequisites-licensing](includes/prerequisites-licensing.md)]
[!INCLUDE [prerequisites-platform](includes/prerequisites-platform.md)]
[!INCLUDE [prerequisites-device-configuration](includes/prerequisites-device-configuration.md)]
[!INCLUDE [prerequisites-rbac](includes/prerequisites-rbac.md)]

## How quality update policies support different deployment scenarios

Quality update policies provide a single management surface for deploying Windows quality updates across different operational scenarios:

- **Standard deployment**: Use quality update policies to enable cloud‑based orchestration of regular monthly quality updates, while update rings and Windows Update client settings continue to control restarts, deadlines, and notifications.
- **Expedited deployment**: Use expedite policies to accelerate the installation of a specific security or critical update when faster remediation is required.
- **Restart‑optimized deployments**: On supported devices, enable hotpatch through quality update policies to apply qualifying security updates without requiring an immediate device restart.

These scenarios use cloud‑based update orchestration to control how updates are approved, timed, and applied, depending on the deployment model.

### Do I need a Windows quality update policy?

You don't need to create a Windows quality update policy for devices to continue receiving monthly Windows quality updates. Devices without a quality update policy continue to receive quality updates through standard Windows Update behavior, using update rings and Windows Update client policies to control deferrals, deadlines, restarts, and notifications.

Create a Windows quality update policy if you want to:
- Enable **cloud‑based orchestration** of Windows quality updates
- Use **Windows Autopatch-managed quality update deployments**
- Enable **hotpatch** for eligible devices
- View **policy‑based quality update reporting**

If you only need to **accelerate the installation of a specific quality update** for a limited set of devices, you can use an **expedite policy** without creating a quality update policy.

In most environments, you create a Windows quality update policy only when you need advanced deployment scenarios such as hotpatch or Windows Autopatch-managed update workflows.

## Next steps

- [Learn how hotpatch works with quality update policies](hotpatch.md)
- [Learn how expedite policies work with quality update policies](quality-updates.md)
