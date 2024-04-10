---
title: Common Education privacy configuration
description: Learn about common privacy configuration used by Education organizations in Intune.
ms.date: 4/9/2024
ms.topic: windows-privacy
author: yegor-a
ms.author: egorabr
---

# Privacy

Settings described in this article should only be deployed after careful consideration as they're affecting users’ privacy.

#### Additional information:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS, and macOS devices](/mem/intune/configuration/settings-catalog)

## Settings Catalog Policies

  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **Let Apps Access Location** | Force allow. | Windows apps are allowed to access location. You can specify either a default setting for all apps or a per-app setting by specifying a Package Family Name. You can get the Package Family Name for an app by using the Get-AppPackage Windows PowerShell cmdlet. A per-app setting overrides the default setting. | [LetAppsAccessLocation](/windows/client-management/mdm/policy-csp-privacy#LetAppsAccessLocation) |
