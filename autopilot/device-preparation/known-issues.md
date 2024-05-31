---
title: Windows Autopilot device preparation known issues
description: Inform yourself about known issues that might occur during a Windows Autopilot device preparation deployment.
ms.service: windows-client
ms.subservice: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/03/2024
ms.collection:
  - M365-modern-desktop
  - highpri
  - tier2
ms.topic: troubleshooting
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation - known issues

This article describes known issues that can often be resolved with configuration changes, through cumulative updates, or might be resolved automatically in a future release.

## Known issues

### Initial release of Windows Autopilot device preparation

The initial release of Windows Autopilot device preparation has the following known issues and limitations:

- Dependency and supersedence relationships are marked in reports as **Dependent**.
- Application uninstall intent is marked in reports as **Installed** if completed successfully.
- Managed Installer policy during the out-of-box experience (OOBE) isn't supported due to the possibility of incorrect reporting.
- Custom compliance isn't supported during Windows Autopilot device preparation deployments.
- The device health script isn't supported during Windows Autopilot device preparation deployments.

### Device is stuck at 100% during the out-of-box experience (OOBE)

If during Windows Autopilot device preparation deployment a device gets stuck at 100% during the out-of-box experience (OOBE), the end-user needs to manually restart the device for the deployment to continue. This issue is a known issue and a fix is being worked on.

### Object with AppID of f1346770-5b25-470b-88bd-d5744ab7952c displays as Intune Autopilot ConfidentialClient

In some tenants, when trying to set the owner of the device group used in the Windows Autopilot device preparation policy, the service principle with AppID of **f1346770-5b25-470b-88bd-d5744ab7952c** displays as **Intune Autopilot ConfidentialClient** instead of **Intune Provisioning Client**. As long as the service principle has an AppID of **f1346770-5b25-470b-88bd-d5744ab7952c**, it's the correct service principle and can be selected.

### User gets to Desktop without required applications installed due to conflict between Microsoft Entra ID and Windows Autopilot device preparation local administrator setting

There's a compatibility problem between the Windows Autopilot device preparation policy **User account type** setting and the Microsoft Entra ID **Local administrator settings**. Specifically, when the Windows Autopilot device preparation policy **User account type** setting is set to **Standard user** and the Microsoft Entra ID setting **Registering user is added as local administrator on the device during Microsoft Entra join (Preview)** under **Local administrator settings** is set to either **Selected** or **None**, provisioning gets skipped during a Windows Autopilot device preparation deployment. This settings conflict leads to a scenario where users could reach the Desktop without having the expected applications installed. The Microsoft Entra ID **Local administrator settings** can be found by signing into the [Azure portal](https://portal.azure.com/) and navigating to **Microsoft Entra ID** > **Manage | Devices** > **Manage | Devices settings**.

Use one of the following two workarounds until a fix is available:

- If the Microsoft Entra ID **Local administrator settings** is set to either **Selected** or **None**, then the Windows Autopilot device preparation policy **User account type** setting needs to be set to **Administrator**.
- The Microsoft Entra ID **Local administrator settings** can be changed to **All** and the Windows Autopilot device preparation policy **User account type** setting can be left at **Standard user**.

In both cases, the end result is that the user is a standard user.
