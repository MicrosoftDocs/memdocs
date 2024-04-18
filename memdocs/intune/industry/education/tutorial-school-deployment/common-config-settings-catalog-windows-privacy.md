---
title: Common Education privacy configuration
description: Learn about common privacy configuration used by Education organizations in Intune.
ms.date: 4/9/2024
ms.topic: windows-privacy
author: yegor-a
ms.author: egorabr
ms.manager: dougeby
---

# Windows Privacy

Microsoft Intune and Intune for Education can configure privacy settings for Windows 10 and later. This article summarizes the configurations that are most commonly used for student and teacher devices.

> [!IMPORTANT]
> The settings in this article configure user privacy. These settings should only be deployed after careful consideration.

> [!NOTE]
> This is an optional policy

To learn more, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS, and macOS devices](/mem/intune/configuration/settings-catalog)

## Settings Catalog Policies

| **Settings Catalog** | **Value** | **Notes** | **CSP** |
|---|---|---|---|
| **Allow Location** | Force Location On. All Location Privacy settings are toggled on and grayed out. Users can't change the settings and all consent permissions will be automatically suppressed. | Required to invoke **Locate device** action on Windows devices in Intune. | [System/AllowLocation](/windows/client-management/mdm/policy-csp-system#allowlocation) |
| **Let Apps Access Location** | Force allow. | Windows apps are allowed to access location. You can specify either a default setting for all apps or a per-app setting by specifying a Package Family Name. You can get the Package Family Name for an app by using the Get-AppPackage Windows PowerShell cmdlet. A per-app setting overrides the default setting. | [Privacy/LetAppsAccessLocation](/windows/client-management/mdm/policy-csp-privacy#letappsaccesslocation) |
