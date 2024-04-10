---
title: Common Education device restrictions configuration
description: Learn about common device restrictions configuration used by Education organizations in Intune.
ms.date: 4/9/2024
ms.topic: windows-start
author: yegor-a
ms.author: egorabr
---

# Start menu customization

To create a unified user experience you can deploy a customized Start and taskbar layout to managed Windows 10 and later devices.

#### Additional information:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](/mem/intune/configuration/settings-catalog)
- [Customize the Start menu and taskbar layout on Windows 10 and later devices](/windows/configuration/start/windows-10-start-layout-options-and-policies)
- [Customize and export the Start layout](/en-us/windows/configuration/start/customize-and-export-start-layout)
- [Configure Windows Taskbar](/en-us/windows/configuration/taskbar/?pivots=windows-11)

## Settings Catalog Policies

  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **Custom Start Menu** | | Create and deploy a custom Start menu and taskbar layout. Pease refer to articles in the Additional information above. | [StartLayout](/windows/client-management/mdm/policy-csp-start) |
  | **Force Start Size** | Force a fullscreen size of Start. | | [Start/ForceStartSize](/windows/client-management/mdm/policy-csp-start#ForceStartSize) |
  | **Hide App List** | None | | [Start/HideAppList](/windows/client-management/mdm/policy-csp-start#HideAppList) |
  | **Hide Change Account Settings** | Disabled | | [Start/HideChangeAccountSettings](/windows/client-management/mdm/policy-csp-start#HideChangeAccountSettings) |
  | **Hide Frequently Used Apps** | Enabled | | [Start/HideFrequentlyUsedApps](/windows/client-management/mdm/policy-csp-start#HideFrequentlyUsedApps) |
  | **Hide Lock** | Disabled | | [Start/HideLock](/windows/client-management/mdm/policy-csp-start#HideLock) |
  | **Hide Power Button** | Disabled | | [Start/HidePowerButton](/windows/client-management/mdm/policy-csp-start#HidePowerButton) |
  | **Hide Recent** **Jumplists** | Enabled | | [Start/HideRecentJumplists](/windows/client-management/mdm/policy-csp-start#HideRecentJumplists) |
  | **Hide Recently Added Apps** | Enabled | | [Start/HideRecentlyAddedApps](/windows/client-management/mdm/policy-csp-start#HideRecentlyAddedApps) |
  | **Hide Sign Out** | Disabled | | [Start/HideSignOut](/windows/client-management/mdm/policy-csp-start#HideSignOut) |
  | **Hide User Tile** | Disabled | | [Start/HideUserTile](/windows/client-management/mdm/policy-csp-start#HideUserTile) |

