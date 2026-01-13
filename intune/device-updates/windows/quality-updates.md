---
title: Windows quality update policy
description: Learn how to manage Windows quality updates in Microsoft Intune using quality updates policies, expedited updates, and Hotpatch to keep devices secure and compliant.
ms.date: 01/06/2026
ms.reviewer: Mounika
ms.topic: how-to
---

# Manage Windows quality updates


Windows quality updates are the regular Windows servicing updates that keep devices secure, reliable, and supported. These updates are released frequently—typically monthly—and include security fixes, non‑security improvements, and reliability enhancements. Because quality updates are cumulative, installing the latest update brings a device fully up to date for its currently installed Windows version.

In Microsoft Intune, Windows quality updates are managed through **quality updates policies**, which provide a dedicated policy surface for controlling how and when these updates are delivered to devices. The policy uses cloud‑based update orchestration and can be used alongside other Windows update policies, such as feature updates and driver updates. Depending on your deployment model, quality updates can be managed directly through Intune or automatically through Windows Autopatch. Client‑side update behavior—such as restart settings, deadlines, and notifications—continues to be configured through standard Windows Update policy settings, including [update rings](update-rings.md) and [Windows Update client policies](/windows/deployment/update/waas-configure-wufb).

Quality updates policies also support **targeted deployment options for specific scenarios**. You can **expedite updates** to fast‑track the installation of critical or security updates when waiting for normal deployment timelines isn't acceptable. For eligible Windows editions and device configurations, quality updates policies can also enable **Hotpatch**, which installs certain security updates without requiring an immediate device restart. Together, these options help organizations balance rapid protection, deployment control, and end‑user experience.

## Prerequisites

[!INCLUDE [prerequisites-network](includes/prerequisites-network.md)]
[!INCLUDE [prerequisites-cloud](includes/prerequisites-cloud.md)]
[!INCLUDE [prerequisites-tenant](includes/prerequisites-tenant.md)]
[!INCLUDE [prerequisites-licensing](includes/prerequisites-licensing.md)]
[!INCLUDE [prerequisites-platform](includes/prerequisites-platform.md)]
[!INCLUDE [prerequisites-device-configuration](includes/prerequisites-device-configuration.md)]
[!INCLUDE [prerequisites-rbac](includes/prerequisites-rbac.md)]

## How quality updates policies support different deployment scenarios

Quality updates policies provide a single management surface for deploying Windows quality updates across different operational scenarios:

- **Standard deployment**: Use quality updates policies with defined approval timing, combined with update rings and client settings, to manage regular servicing updates.
- **Expedited deployment**: Use the same policy to accelerate the installation of specific security or critical updates when faster remediation is required.
- **Restart‑optimized deployments**: On supported devices, enable Hotpatch through quality updates policies to apply qualifying security updates without requiring an immediate restart.

Each capability uses the same underlying cloud orchestration but differs in how updates are approved, timed, and applied. The following sections link to detailed guidance for each scenario.


## Next steps

> [!div class="nextstepaction"]
> [Learn how expedited updates work with quality updates policies](quality-updates.md)

> [!div class="nextstepaction"]
> [Learn how Hotpatch works with quality updates policies](hotpatch.md)

> [!div class="nextstepaction"]
> [Configure Windows quality updates policies](configure-quality-updates.md)
