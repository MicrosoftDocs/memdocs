---
author: Yusuke Shinoki (HE/HIM)
ms.date: 04/10/2024
---
### (Optional) OneDrive Known Folder Move

For devices used by the same user all the time (1:1 scenario) it is common to enable OneDrive Known Folder Move to redirect user’s Documents, Desktop and Pictures folders to OneDrive to prevent data loss.

Additional information:

- [Redirect and move Windows known folders to OneDrive](https://learn.microsoft.com/sharepoint/redirect-known-folders)

  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **Allow syncing OneDrive accounts for only specific organizations** | Enabled | Only enables the setting configuration. | [AllowTenantList](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Allow syncing OneDrive accounts for only specific organizations\Tenant ID: (Device)** | _tenant ID_ | **Important!** This is a tenant-specific value. | [AllowTenantList](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Block file downloads when users are low on disk space** | Enabled | | [MinDiskSpaceLimitInMB](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Block file downloads when users are low on disk space\Minimum available disk space: (Device)** | 1024 | Only enables the setting configuration. | [MinDiskSpaceLimitInMB](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Convert synced team site files to online-only files** | Enabled | Files in currently syncing team sites are changed to online-only files, by default. Files later added or updated in the team site are also downloaded as online-only files. | [DehydrateSyncedTeamSites](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Disable the tutorial that appears at the end of OneDrive Setup (User)** | Enabled | | [DisableTutorial](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Use OneDrive Files On-Demand** | Enabled | New users who set up the sync app see online-only files in File Explorer, by default. | [FilesOnDemandEnabled](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Prevent users from redirecting their Windows known folders to their PC** | Enabled | | [KFMBlockOptOut](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Prevent users from syncing libraries and folders shared from other organizations** | Enabled | | [BlockExternalSync](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Prevent users from syncing personal OneDrive accounts (User)** | Enabled | | [DisablePersonalSync](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Set the sync app update ring** | Enabled | Only enables the setting configuration. | [GPOSetUpdateRing](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Set the sync app update ring\Update ring: (Device)** | Production | Users get the latest features as they become available. | [GPOSetUpdateRing](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Silently move Windows known folders to OneDrive** | Enabled | **Important:** Make sure to pick the setting with 5 sub-settings listed below.Redirect and move your users' Documents, Pictures, and/or Desktop folders to OneDrive without any user interaction. | [KFMSilentOptIn](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Silently move Windows known folders to OneDrive\Desktop (Device)** | TRUE | | [KFMSilentOptIn](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Silently move Windows known folders to OneDrive\Documents (Device)** | TRUE | | [KFMSilentOptIn](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Silently move Windows known folders to OneDrive\Pictures (Device)** | TRUE | | [KFMSilentOptIn](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Silently move Windows known folders to OneDrive\Show notification to users after folders have been redirected: (Device)** | No | | [KFMSilentOptIn](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Silently move Windows known folders to OneDrive\Tenant ID: (Device)** | _{tenant ID}_ | | [KFMSilentOptIn](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Silently sign in users to the OneDrive sync app with their Windows credentials** | Enabled | Users who are signed in on a PC that's joined to Microsoft Entra ID can set up the sync app without entering their account credentials. | [SilentAccountConfig](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Warn users who are low on disk space** | Enabled | Only enables the setting configuration. | [WarningMinDiskSpaceLimitInMB](https://learn.microsoft.com/sharepoint/use-group-policy) |
  | **Warn users who are low on disk space\Minimum available disk space: (Device)** | 2048 | | [WarningMinDiskSpaceLimitInMB](https://learn.microsoft.com/sharepoint/use-group-policy) |

