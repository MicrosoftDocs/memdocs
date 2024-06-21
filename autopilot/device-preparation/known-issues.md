---
title: Windows Autopilot device preparation known issues
description: Information regarding known issues that might occur during a Windows Autopilot device preparation deployment.
ms.service: windows-client
ms.subservice: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/19/2024
ms.collection:
  - M365-modern-desktop
  - highpri
  - tier2
ms.topic: troubleshooting
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation - known issues

This article describes known issues that can often be resolved with:

- Configuration changes.
- Cumulative updates.
- Might be resolved automatically in a future release.

## Known issues

## Windows Autopilot device preparation policy shows 0 groups assigned

*2024/06/18*

There's a known issue that the Windows Autopilot device preparation policy shows **0 groups assigned** even when:

- An assigned device security group was properly added to the policy.
- The **Intune Provisioning Client** service principal with AppID of **f1346770-5b25-470b-88bd-d5744ab7952c** is the owner of the device security group specified in the policy.

The issue is being investigated. As a workaround, create a new assigned device security group with the **Intune Provisioning Client** service principal with AppID of **f1346770-5b25-470b-88bd-d5744ab7952c** as the owner, and then assign the new device group to the Windows Autopilot device preparation policy. For more information on creating the assigned device group, see [Create a device group](tutorial/user-driven/entra-join-device-group.md#create-a-device-group).

## Unable to assign Windows Autopilot device preparation policy to user group

- *2024/06/18*

There's a known issue where an administrator might not be able to assign the Windows Autopilot device preparation policy to a user group. When the issue occurs, the following error might occur:

> **Unable to save group assignment for <policy_name>. You do not have permission to save these assignments.**

The issue is being investigated. As a workaround, add the following additional role-based access control (RBAC) permission for the Windows Autopilot device preparation administrator role:

- **Device configurations**
  - Assign

For more information, see [Required RBAC permissions](requirements.md?tabs=rbac#required-rbac-permissions).

> [!NOTE]
>
> The [Required RBAC permissions](requirements.md?tabs=rbac#required-rbac-permissions) article doesn't list the **Device configurations** - **Assign** permission. The requirement of this permission is only temporary until the issue is resolved. However, the article can be used as a guide on how to properly add this permission.

### Initial release of Windows Autopilot device preparation

> *2024/06/03*

The initial release of Windows Autopilot device preparation has the following known issues and limitations:

- Dependency and supersedence relationships are marked in reports as **Dependent**.
- Application uninstall intent is marked in reports as **Installed** if completed successfully.
- Managed Installer policy during the out-of-box experience (OOBE) isn't supported due to the possibility of incorrect reporting.
- Custom compliance isn't supported during Windows Autopilot device preparation deployments.
- The device health script isn't supported during Windows Autopilot device preparation deployments.

### Device is stuck at 100% during the out-of-box experience (OOBE)

2024/06/03

If during Windows Autopilot device preparation deployment a device gets stuck at 100% during the out-of-box experience (OOBE), the end-user needs to manually restart the device for the deployment to continue. This issue is a known issue and a fix is being worked on.

### Object with AppID of f1346770-5b25-470b-88bd-d5744ab7952c displays as Intune Autopilot ConfidentialClient (2024/06/03)

In some tenants, when trying to set the owner of the device group used in the Windows Autopilot device preparation policy, the service principal with AppID of **f1346770-5b25-470b-88bd-d5744ab7952c** displays as **Intune Autopilot ConfidentialClient** instead of **Intune Provisioning Client**. As long as the service principal has an AppID of **f1346770-5b25-470b-88bd-d5744ab7952c**, it's the correct service principal and can be selected.

### User gets to desktop without required applications installed due to conflict between Microsoft Entra ID and Windows Autopilot device preparation local administrator setting

There's a compatibility problem between the Windows Autopilot device preparation policy **User account type** setting and the Microsoft Entra ID **Local administrator settings**. Specifically, when the Windows Autopilot device preparation policy **User account type** setting is set to **Standard user** and the Microsoft Entra ID setting **Registering user is added as local administrator on the device during Microsoft Entra join (Preview)** under **Local administrator settings** is set to either **Selected** or **None**, provisioning gets skipped during a Windows Autopilot device preparation deployment. This settings conflict leads to a scenario where users could reach the desktop without having the expected applications installed. The Microsoft Entra ID **Local administrator settings** can be found by signing into the [Azure portal](https://portal.azure.com/) and navigating to **Microsoft Entra ID** > **Manage | Devices** > **Manage | Devices settings**.

Until the issue is fixed, for users to be standard non-administrators on their device, make sure that the settings are set to one of the following three setting combinations:

- The Microsoft Entra ID **Local administrator settings** is set to **None**.
- The Windows Autopilot device preparation policy **User account type** setting is set to **Administrator**.

- The Microsoft Entra ID **Local administrator settings** is set to **Selected** and the standard non-administrator users aren't selected.
- The Windows Autopilot device preparation policy **User account type** setting is set to **Administrator**.

- The Microsoft Entra ID **Local administrator settings** is set to **All**.
- The Windows Autopilot device preparation policy **User account type** is set to **Standard user**.

In all three cases, the end result is that the user is a standard non-administrative user on the device.

If the intention is for the user to be a local administrator user on the device, make sure that the settings are set to one of the following two setting combinations:

- The Microsoft Entra ID **Local administrator settings** is set to **All**.
- The Windows Autopilot device preparation policy **User account type** setting is set to **Administrator**.

- The Microsoft Entra ID **Local administrator settings** is set to **Selected** and the administrator users are selected.
- The Windows Autopilot device preparation policy **User account type** setting is set to **Administrator**.

### Corporate identifiers isn't working in initial release of Windows Autopilot device preparation

Corporate identifiers isn't working in the initial release of Windows Autopilot device preparation. If the personal device restriction is enabled and personal devices aren't allowed, enrollment always fails during the Windows Autopilot device preparation deployment. For this reason, Windows Autopilot device preparation doesn't work when the personal device restriction is enabled. The issue is being investigated. Microsoft recommends that customers that have personal device restrictions enabled wait for the issue to be resolved before trying to use Windows Autopilot device preparation.
