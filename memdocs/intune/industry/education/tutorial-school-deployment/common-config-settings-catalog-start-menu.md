---
title: Common Education Start Menu configuration
description: Learn about common Start Menu configuration used by Education organizations in Intune.
ms.date: 4/9/2024
ms.topic: windows-start
author: yegor-a
ms.author: egorabr
---

# Start Menu Customization

To create a unified user experience, an Intune administrator can deploy a customized Start and taskbar layout to managed Windows 10 and later devices.

> [!NOTE]
> This is an optional policy

#### Additional information:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS, and macOS devices](/mem/intune/configuration/settings-catalog)
- [Customize the Start menu and taskbar layout on Windows 10 and later devices](/windows/configuration/start/windows-10-start-layout-options-and-policies)
- [Customize and export the Start layout](/en-us/windows/configuration/start/customize-and-export-start-layout)
- [Configure Windows Taskbar](/en-us/windows/configuration/taskbar/?pivots=windows-11)

## Settings Catalog Policies

| **Settings Catalog** | **Value** | **Notes** | **CSP** |
|---|---|---|---|
| **Custom Start Menu** | A custom XML string | Create and deploy a custom Start menu and taskbar layout. Please refer to articles in the Additional information. | [StartLayout](/windows/client-management/mdm/policy-csp-start) |
| **Hide App List** | None | | [Start/HideAppList](/windows/client-management/mdm/policy-csp-start#hideapplist) |
| **Hide Change Account Settings** | Disabled | | [Start/HideChangeAccountSettings](/windows/client-management/mdm/policy-csp-start#hidechangeaccountsettings) |
| **Hide Frequently Used Apps** | Enabled | | [Start/HideFrequentlyUsedApps](/windows/client-management/mdm/policy-csp-start#hidefrequentlyusedapps) |
| **Hide Power Button** | Disabled | | [Start/HidePowerButton](/windows/client-management/mdm/policy-csp-start#hidepowerbutton) |
| **Hide Recent Jumplists** | Enabled | | [Start/HideRecentJumplists](/windows/client-management/mdm/policy-csp-start#hiderecentjumplists) |
| **Hide Recently Added Apps** | Enabled | | [Start/HideRecentlyAddedApps](/windows/client-management/mdm/policy-csp-start#hiderecentlyaddedapps) |
| **Hide User Tile** | Disabled | | [Start/HideUserTile](/windows/client-management/mdm/policy-csp-start#hideusertile) |
| **Hide Lock** | Disabled | | [Start/HideLock](/windows/client-management/mdm/policy-csp-start#hidelock) |
| **Hide Sign Out** | Disabled | | [Start/HideSignOut](/windows/client-management/mdm/policy-csp-start#hidesignout) |
