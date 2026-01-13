---
title: Learn about Windows Driver updates policy for Windows devices in Intune
description: Learn about using Microsoft Intune policy to manage Windows driver updates.
ms.date: 09/10/2024
ms.topic: how-to
ms.reviewer: davguy; davidmeb; bryanke
---

# Manage Windows driver updates

Windows driver updates provide updated device drivers and firmware that help ensure hardware compatibility, stability, and performance. These updates are released by device manufacturers and can include fixes for reliability issues, security vulnerabilities, and support for new hardware capabilities. Because driver updates can vary by device model and hardware configuration, organizations often prefer a more controlled approval process.

In Microsoft Intune, Windows driver updates are managed through **driver updates policies**, which provide a dedicated policy surface for reviewing, approving, and deploying driver updates to managed devices. This policy is built on cloud‑based update orchestration and works alongside other Windows update policies, such as feature updates and quality updates. Driver updates policies can be used independently or as part of Windows Autopatch. Client‑side install behavior—such as restarts and user notifications—continues to be governed by standard Windows Update policy settings.

Driver updates policies support **automatic or manual approval workflows**, allowing you to choose whether recommended drivers are deployed automatically or require administrator review before installation. This approach helps organizations balance hardware stability, risk management, and operational efficiency while maintaining visibility into which drivers are approved for deployment.

## Prerequisites

[!INCLUDE [prerequisites-network](includes/prerequisites-network.md)]
[!INCLUDE [prerequisites-tenant](includes/prerequisites-tenant.md)]
[!INCLUDE [prerequisites-licensing](includes/prerequisites-licensing.md)]
[!INCLUDE [prerequisites-platform](includes/prerequisites-platform.md)]
[!INCLUDE [prerequisites-device-configuration](includes/prerequisites-device-configuration.md)]
[!INCLUDE [prerequisites-rbac](includes/prerequisites-rbac.md)]

<!--
## Control driver update approvals

Using Windows driver update policies, you remain in control of which driver updates can install on your devices. You can:

- **Enable automatic approvals of recommended driver updates**. Policies set for automatic approval automatically approve and deploy each new driver update version that is considered a *recommended driver* for the devices assigned to the policy. Recommended drivers are typically the latest driver update published by the driver publisher that the publisher has marked as *required*. Drivers that aren't identified as the current recommended driver are also available as *other drivers*, which can be considered to be optional driver updates.

  Later, when a newer driver update from the OEM is released and identified as the current *recommended* driver update, Intune automatically adds it to the policy and moves the previously recommended driver to the list of other drivers.

  > [!TIP]
  > An approved recommended driver update that is moved to the *other drivers* list due to a newer recommended driver update becoming available, remains approved. When a newer recommended and approved driver update is available, Windows Autopatch installs only that latest approved version. If the latest approved update version is paused, Autopatch automatically offers the next most recent and approved update version, which is now on the *other drivers* list. This behavior ensures that the last known-good driver update version that was approved can continue to install on devices, while the more recent recommended version remains paused.

  With this policy configuration, you can also choose to review the available updates to selectively approve, pause, or decline *any* update that remains available for devices with the policy.

- **Configure policy to require manual approval of all updates**. This policy ensures that administrators must approve a driver update before it can be deployed. Newer versions of driver updates for devices with this policy are automatically added to the policy but remain inactive until approved.

  Later, when a newer driver update from the OEM is recommended for a device in the policy, the policy status updates to indicate there are drivers pending your review. This status becomes a call to action to review the policy and decide if you want to approve deployment of the newest drivers to devices.

- **Manage which drivers are approved for deployment**. You can edit any driver update policy to modify which drivers are approved for deployment. You can pause the deployment of any individual driver update to stop its deployment to new devices, and then later reapprove the paused update to enable Windows Update to resume installing it on applicable devices.

Regardless of the policy configuration and the drivers included, only approved drivers can install on devices. Additionally, Windows Update only installs the latest available and approved update when the version is more recent than the one currently installed on the device.

-->

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
