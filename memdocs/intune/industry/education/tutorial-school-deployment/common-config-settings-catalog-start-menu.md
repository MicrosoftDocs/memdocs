---
title: Common Education Start Menu configuration
description: Learn about common Start Menu configuration used by Education organizations in Intune.
ms.date: 4/9/2024
ms.topic: conceptual
author: yegor-a
ms.author: egorabr
ms.manager: dougeby
---

# Start Menu Customization

Microsoft Intune and Intune for Education can configure settings for a customized Start menu for Windows 10 and later. This article summarizes the configurations that are most commonly used for student and teacher devices.

Students can benefit from a Start menu that is customized to provide access to educational tools and resources while restricting distractions. By configuring policy settings, educational institutions can create a focused and conducive learning environment.

> [!NOTE]
> This is an optional policy

To learn more, see:

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
