---
author: Yusuke Shinoki (HE/HIM)
ms.date: 04/10/2024
---
### (Optional) Privacy

Settings described in this article should only be deployed after careful consideration as they are affecting users’ privacy.

Additional information:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](https://learn.microsoft.com/mem/intune/configuration/settings-catalog)

  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **Let Apps Access Location** | Force allow. | Windows apps are allowed to access location.You can specify either a default setting for all apps or a per-app setting by specifying a Package Family Name. You can get the Package Family Name for an app by using the Get-AppPackage Windows PowerShell cmdlet. A per-app setting overrides the default setting. | [LetAppsAccessLocation](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-privacy) |

### (Optional) Start menu customization

To create a unified user experience you can deploy a customized Start and taskbar layout to managed Windows 10 and later devices.

Additional information:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](https://learn.microsoft.com/mem/intune/configuration/settings-catalog)
- [Customize the Start menu and taskbar layout on Windows 10 and later devices](https://learn.microsoft.com/en-us/windows/configuration/start/windows-10-start-layout-options-and-policies)
- [Customize and export the Start layout](https://learn.microsoft.com/en-us/windows/configuration/start/customize-and-export-start-layout)
- [Configure Windows Taskbar](https://learn.microsoft.com/en-us/windows/configuration/taskbar/?pivots=windows-11)

  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **Custom Start Menu** | | Create and deploy a custom Start menu and taskbar layout. Pease refer to articles in the Additional information above. | [StartLayout](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-start) |
  | **Force Start Size** | Force a fullscreen size of Start. | | [Start/ForceStartSize](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-start) |
  | **Hide App List** | None | | [Start/HideAppList](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-start) |
  | **Hide Change Account Settings** | Disabled | | [Start/HideChangeAccountSettings](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-start) |
  | **Hide Frequently Used Apps** | Enabled | | [Start/HideFrequentlyUsedApps](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-start) |
  | **Hide Lock** | Disabled | | [Start/HideLock](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-start) |
  | **Hide Power Button** | Disabled | | [Start/HidePowerButton](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-start) |
  | **Hide Recent** **Jumplists** | Enabled | | [Start/HideRecentJumplists](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-start) |
  | **Hide Recently Added Apps** | Enabled | | [Start/HideRecentlyAddedApps](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-start) |
  | **Hide Sign Out** | Disabled | | [Start/HideSignOut](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-start) |
  | **Hide User Tile** | Disabled | | [Start/HideUserTile](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-start) |

