---
title: Manage Windows Driver Updates
description: Learn how to manage Windows driver updates using Intune driver updates policies to keep Windows devices current and stable.
ms.date: 01/14/2026
ms.topic: how-to
ms.reviewer: davguy; davidmeb; bryanke
---

# Manage Windows driver updates

Windows driver updates provide updated device drivers and firmware that help ensure hardware compatibility, stability, and performance. These updates are released by device manufacturers and can include fixes for reliability issues, security vulnerabilities, and support for new hardware capabilities. Because driver updates can vary by device model and hardware configuration, organizations often prefer a more controlled approval process.

In Microsoft Intune, Windows driver updates are managed through **driver updates policies**, which provide a dedicated policy surface for reviewing, approving, and deploying driver updates to managed devices. This policy is built on cloud‑based update orchestration and works alongside other Windows update policies, such as feature updates and quality updates. Driver updates policies can be used independently or as part of Windows Autopatch. Client‑side install behavior—such as restarts and user notifications—continues to be governed by standard Windows Update policy settings.

Driver updates policies support **automatic or manual approval workflows**, allowing you to choose whether recommended drivers are deployed automatically or require administrator review before installation. This approach helps organizations balance hardware stability, risk management, and operational efficiency while maintaining visibility into which drivers are approved for deployment.

## Prerequisites

[!INCLUDE [prerequisites-network](includes/prerequisites-network.md)]
[!INCLUDE [prerequisites-cloud](includes/prerequisites-cloud.md)]
[!INCLUDE [prerequisites-tenant](includes/prerequisites-tenant.md)]
[!INCLUDE [prerequisites-licensing](includes/prerequisites-licensing.md)]
[!INCLUDE [prerequisites-platform](includes/prerequisites-platform.md)]
[!INCLUDE [prerequisites-device-configuration](includes/prerequisites-device-configuration.md)]
[!INCLUDE [prerequisites-rbac](includes/prerequisites-rbac.md)]

## Architecture

The following diagram illustrates the high‑level architecture for managing Windows driver updates by using Microsoft Intune and Windows Autopatch.

:::image type="content" source="./images/autopatch-ds.png" alt-text="A conceptual diagram of Windows driver update management." lightbox="./images/autopatch-ds.png" border="false":::

1. **Microsoft Intune** provides device identity, assignment, and driver update approval information. Intune sends policy settings, approved drivers, and pause commands to Windows Autopatch.
1. **Windows Autopatch** uses this information to configure Windows Update behavior for managed devices and to coordinate driver update deployment.
1. **Windows Update** evaluates device and hardware information to determine which driver updates are applicable, and installs only approved updates during regular update scans.
1. **Reporting data** collected during update operations is sent through Windows Autopatch and surfaced in Intune reporting.

This architecture allows administrators to approve and control driver updates centrally in Intune while relying on Windows Update and Autopatch to determine applicability and handle installation.

## Next steps

> [!div class="nextstepaction"]
> [Learn how to configure driver updates policies](driver-updates-policy.md)
