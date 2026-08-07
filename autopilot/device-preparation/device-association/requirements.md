---
title: Requirements for Windows Autopilot device association
description: Software, networking, licensing, and RBAC requirements for Windows Autopilot device association.
ms.date: 08/07/2026
ms.collection:
  - M365-modern-desktop
ms.topic: article
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Requirements for Windows Autopilot device association

The list of requirements for Windows Autopilot device association is organized into four categories:

- **Software** - OS requirements.
- **Networking** - Networking requirements.
- **Licensing** - Licensing requirements.
- **RBAC** - RBAC permissions required for Windows Autopilot device association.

Select the appropriate tab to see the relevant requirements:

## [:::image type="icon" source="../../images/icons/software-18.svg"::: **Software**](#tab/software)

### Software requirements

> [!IMPORTANT]
>
> Device association requires a **physical device**. Virtual machines aren't supported.

#### Windows 11

<!-- TODO: Replace each KBXXXXXXX value, support.microsoft.com link, and installation media date when the updates are published for versions 23H2, 24H2, and 25H2. -->

- Windows 11, version 25H2 with [KBXXXXXXX](https://support.microsoft.com/topic/) or later - Windows 11, version 25H2 installation media dated *Month Year* or later has [KBXXXXXXX](https://support.microsoft.com/topic/) included.
- Windows 11, version 24H2 with [KBXXXXXXX](https://support.microsoft.com/topic/) or later - Windows 11, version 24H2 installation media dated *Month Year* or later has [KBXXXXXXX](https://support.microsoft.com/topic/) included.
- Windows 11, version 23H2 with [KBXXXXXXX](https://support.microsoft.com/topic/) or later - Windows 11, version 23H2 installation media dated *Month Year* or later has [KBXXXXXXX](https://support.microsoft.com/topic/) included.

The following editions are supported:

- Windows 11 Pro.
- Windows 11 Pro Education.
- Windows 11 Pro for Workstations.
- Windows 11 Enterprise.
- Windows 11 Education.
- [Windows 11 Enterprise LTSC](/windows/whats-new/ltsc/overview).

#### Trusted Platform Module (TPM)

Device association requires a **physical device**—virtual machines aren't supported. Each device must have **TPM 2.0**, enabled and in a good state. The TPM shouldn't be in **Reduced Functionality Mode**. TPM attestation is enforced during association: device association uses the TPM to attest the device's identity before enrollment.

## [:::image type="icon" source="../../images/icons/wifi-ethernet-18.svg"::: **Networking**](#tab/networking)

### Networking requirements

Device association builds on Windows Autopilot device preparation and has the same baseline networking requirements. For the full list of endpoints and network configuration, see [Windows Autopilot device preparation requirements](../requirements.md?tabs=networking).

## [:::image type="icon" source="../../images/icons/license-18.svg"::: **Licensing**](#tab/licensing)

### Licensing requirements

Device association is part of Windows Autopilot device preparation and has the same licensing requirements. For the full list of supported subscriptions, see [Windows Autopilot device preparation requirements](../requirements.md?tabs=licensing).

## [:::image type="icon" source="../../images/icons/permissions-18.svg"::: **RBAC**](#tab/rbac)

### Required RBAC permissions

The following role-based access control (RBAC) permissions are required in an Intune role for Windows Autopilot device association.

#### Required for configuring the device preparation policy

- **Device configurations**
  - Read
  - Delete
  - Create
  - Update
- **Enrollment programs**
  - Enrollment time device membership assignment
- **Managed apps**
  - Read
- **Mobile apps**
  - Read
- **Organization**
  - Read

#### Required for managing associated devices

- **Enrollment programs**
  - Read device
  - Create device
  - Delete device
- **Device configurations**
  - Assign

To create a custom role with these permissions for use with Windows Autopilot device association:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Tenant administration** > **Roles**.
1. Select **Create** > **Intune role**.
1. On the **Basics** page, enter a name and description for the custom role, and then select **Next**.
1. On the **Permissions** page, set each of the permissions listed previously to **Yes**. Leave all other permissions at the default of **No**.
1. On the **Scope tags** page, select **Next**.
1. On the **Review + create** page, verify that all permissions are correct, and then select **Create**.

The new custom role can now be assigned to users who manage Windows Autopilot device association. For more information, see [Role-based access control (RBAC) with Microsoft Intune](/intune/fundamentals/role-based-access-control/overview).

---

## Next steps

[Tutorial: Set up Windows Autopilot device preparation with device association](../tutorial/user-driven/entra-join-workflow.md)
