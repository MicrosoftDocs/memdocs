---
title: Common Education OneDrive Known Folder Move configuration
description: Learn about common OneDrive Known Folder Move configuration used by Education organizations in Intune.
ms.date: 4/9/2024
ms.topic: onedrive-kfm
author: yegor-a
ms.author: egorabr
---

# OneDrive Known Folder Move

For devices used by the same user all the time (1:1 scenario) it is common to enable OneDrive Known Folder Move to redirect user’s Documents, Desktop and Pictures folders to OneDrive to prevent data loss.

#### Additional information:

- [Redirect and move Windows known folders to OneDrive](/sharepoint/redirect-known-folders)

## Settings Catalog Policies
  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **Allow syncing OneDrive accounts for only specific organizations** | Enabled | Only enables the setting configuration. | [AllowTenantList](/sharepoint/use-group-policy#AllowTenantList) |
  | **Allow syncing OneDrive accounts for only specific organizations\Tenant ID: (Device)** | _tenant ID_ | **Important!** This is a tenant-specific value. | [AllowTenantList](/sharepoint/use-group-policy#AllowTenantList) |
  | **Block file downloads when users are low on disk space** | Enabled | | [MinDiskSpaceLimitInMB](/sharepoint/use-group-policy#MinDiskSpaceLimitInMB) |
  | **Block file downloads when users are low on disk space\Minimum available disk space: (Device)** | 1024 | Only enables the setting configuration. | [MinDiskSpaceLimitInMB](/sharepoint/use-group-policy#MinDiskSpaceLimitInMB) |
  | **Convert synced team site files to online-only files** | Enabled | Files in currently syncing team sites are changed to online-only files, by default. Files later added or updated in the team site are also downloaded as online-only files. | [DehydrateSyncedTeamSites](/sharepoint/use-group-policy#)DehydrateSyncedTeamSites |
  | **Disable the tutorial that appears at the end of OneDrive Setup (User)** | Enabled | | [DisableTutorial](/sharepoint/use-group-policy#DisableTutorial) |
  | **Use OneDrive Files On-Demand** | Enabled | New users who set up the sync app see online-only files in File Explorer, by default. | [FilesOnDemandEnabled](/sharepoint/use-group-policy#FilesOnDemandEnabled) |
  | **Prevent users from redirecting their Windows known folders to their PC** | Enabled | | [KFMBlockOptOut](/sharepoint/use-group-policy#KFMBlockOptOut) |
  | **Prevent users from syncing libraries and folders shared from other organizations** | Enabled | | [BlockExternalSync](/sharepoint/use-group-policy#BlockExternalSync) |
  | **Prevent users from syncing personal OneDrive accounts (User)** | Enabled | | [DisablePersonalSync](/sharepoint/use-group-policy#DisablePersonalSync) |
  | **Set the sync app update ring** | Enabled | Only enables the setting configuration. | [GPOSetUpdateRing](/sharepoint/use-group-policy#GPOSetUpdateRing) |
  | **Set the sync app update ring\Update ring: (Device)** | Production | Users get the latest features as they become available. | [GPOSetUpdateRing](/sharepoint/use-group-policy#GPOSetUpdateRing) |
  | **Silently move Windows known folders to OneDrive** | Enabled | **Important:** Make sure to pick the setting with 5 sub-settings listed below.Redirect and move your users' Documents, Pictures, and/or Desktop folders to OneDrive without any user interaction. | [KFMSilentOptIn](/sharepoint/use-group-policy#KFMSilentOptIn) |
  | **Silently move Windows known folders to OneDrive\Desktop (Device)** | TRUE | | [KFMSilentOptIn](/sharepoint/use-group-policy#KFMSilentOptIn) |
  | **Silently move Windows known folders to OneDrive\Documents (Device)** | TRUE | | [KFMSilentOptIn](/sharepoint/use-group-policy#KFMSilentOptIn) |
  | **Silently move Windows known folders to OneDrive\Pictures (Device)** | TRUE | | [KFMSilentOptIn](/sharepoint/use-group-policy#KFMSilentOptIn) |
  | **Silently move Windows known folders to OneDrive\Show notification to users after folders have been redirected: (Device)** | No | | [KFMSilentOptIn](/sharepoint/use-group-policy#KFMSilentOptIn) |
  | **Silently move Windows known folders to OneDrive\Tenant ID: (Device)** | _{tenant ID}_ | | [KFMSilentOptIn](/sharepoint/use-group-policy#KFMSilentOptIn) |
  | **Silently sign in users to the OneDrive sync app with their Windows credentials** | Enabled | Users who are signed in on a PC that's joined to Microsoft Entra ID can set up the sync app without entering their account credentials. | [SilentAccountConfig](/sharepoint/use-group-policy#SilentAccountConfig) |
  | **Warn users who are low on disk space** | Enabled | Only enables the setting configuration. | [WarningMinDiskSpaceLimitInMB](/sharepoint/use-group-policy#WarningMinDiskSpaceLimitInMB) |
  | **Warn users who are low on disk space\Minimum available disk space: (Device)** | 2048 | | [WarningMinDiskSpaceLimitInMB](/sharepoint/use-group-policy#WarningMinDiskSpaceLimitInMB) |

