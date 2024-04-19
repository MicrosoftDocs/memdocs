---
title: Common Education OneDrive Known Folder Move configuration
description: Learn about common OneDrive Known Folder Move configuration used by Education organizations in Intune.
ms.date: 4/9/2024
ms.topic: conceptual
author: yegor-a
ms.author: egorabr
ms.manager: dougeby
---

# OneDrive Known Folder Move

Microsoft Intune and Intune for Education can configure the settings to redirect and move Windows known folders to OneDrive. This article summarizes the configurations that are most commonly used for student and teacher devices to enable OneDrive Known Folder Move to redirect the user’s Documents, Desktop, and Pictures folders to OneDrive to prevent data loss.

> [!NOTE]
> This is an optional policy

To learn more, see [Redirect and move Windows known folders to OneDrive](/sharepoint/redirect-known-folders).

## Settings Catalog Policies

| **Settings Catalog** | **Value** | **Notes** | **CSP** |
|---|---|---|---|
| **Allow syncing OneDrive accounts for only specific organizations** | Enabled | Only enables the setting configuration. | [AllowTenantList](/sharepoint/use-group-policy#allow-syncing-onedrive-accounts-for-only-specific-organizations) |
| **Allow syncing OneDrive accounts for only specific organizations\Tenant ID: (Device)** | _tenant ID_ | **Important!** This is a tenant-specific value. [How to find your Microsoft Entra tenant ID](/entra/fundamentals/how-to-find-tenant)| [AllowTenantList](/sharepoint/use-group-policy#allow-syncing-onedrive-accounts-for-only-specific-organizations) |
| **Block file downloads when users are low on disk space** | Enabled | | [MinDiskSpaceLimitInMB](/sharepoint/use-group-policy#block-file-downloads-when-users-are-low-on-disk-space) |
| **Block file downloads when users are low on disk space\Minimum available disk space: (Device)** | 1024 | Only enables the setting configuration. | [MinDiskSpaceLimitInMB](/sharepoint/use-group-policy#block-file-downloads-when-users-are-low-on-disk-space) |
| **Convert synced team site files to online-only files** | Enabled | Files in currently syncing team sites are changed to online-only files, by default. Files later added or updated in the team site are also downloaded as online-only files. | [DehydrateSyncedTeamSites](/sharepoint/use-group-policy#convert-synced-team-site-files-to-online-only-files) |
| **Disable the tutorial that appears at the end of OneDrive Setup (User)** | Enabled | | [DisableTutorial](/sharepoint/use-group-policy#disable-the-tutorial-that-appears-at-the-end-of-onedrive-setup) |
| **Prevent users from redirecting their Windows known folders to their PC** | Enabled | | [KFMBlockOptOut](/sharepoint/use-group-policy#prevent-users-from-redirecting-their-windows-known-folders-to-their-pc) |
| **Prevent users from syncing libraries and folders shared from other organizations** | Enabled | | [BlockExternalSync](/sharepoint/use-group-policy#prevent-users-from-syncing-libraries-and-folders-shared-from-other-organizations) |
| **Prevent users from syncing personal OneDrive accounts (User)** | Enabled | | [DisablePersonalSync](/sharepoint/use-group-policy#prevent-users-from-syncing-personal-onedrive-accounts) |
| **Set the sync app update ring** | Enabled | Only enables the setting configuration. | [GPOSetUpdateRing](/sharepoint/use-group-policy#set-the-sync-app-update-ring) |
| **Set the sync app update ring\Update ring: (Device)** | Production | Users get the latest features as they become available. | [GPOSetUpdateRing](/sharepoint/use-group-policy#set-the-sync-app-update-ring) |
| **Silently move Windows known folders to OneDrive** | Enabled | **Important:** Make sure to pick the setting with 5 sub-settings listed below.Redirect and move your users' Documents, Pictures, and/or Desktop folders to OneDrive without any user interaction. | [KFMSilentOptIn](/sharepoint/use-group-policy#silently-move-windows-known-folders-to-onedrive) |
| **Silently move Windows known folders to OneDrive\Desktop (Device)** | True | | [KFMSilentOptIn](/sharepoint/use-group-policy#silently-move-windows-known-folders-to-onedrive) |
| **Silently move Windows known folders to OneDrive\Documents (Device)** | True | | [KFMSilentOptIn](/sharepoint/use-group-policy#silently-move-windows-known-folders-to-onedrive) |
| **Silently move Windows known folders to OneDrive\Pictures (Device)** | True | | [KFMSilentOptIn](/sharepoint/use-group-policy#silently-move-windows-known-folders-to-onedrive) |
| **Silently move Windows known folders to OneDrive\Show notification to users after folders have been redirected: (Device)** | No | | [KFMSilentOptIn](/sharepoint/use-group-policy#silently-move-windows-known-folders-to-onedrive) |
| **Silently move Windows known folders to OneDrive\Tenant ID: (Device)** | _{tenant ID}_ | | [KFMSilentOptIn](/sharepoint/use-group-policy#silently-move-windows-known-folders-to-onedrive) |
| **Silently sign in users to the OneDrive sync app with their Windows credentials** | Enabled | Users who are signed in on a PC that's joined to Microsoft Entra ID can set up the sync app without entering their account credentials. | [SilentAccountConfig](/sharepoint/use-group-policy#silently-sign-in-users-to-the-onedrive-sync-app-with-their-windows-credentials) |
| **Use OneDrive Files On-Demand** | Enabled | New users who set up the sync app see online-only files in File Explorer, by default. | [FilesOnDemandEnabled](/sharepoint/use-group-policy#use-onedrive-files-on-demand) |
| **Warn users who are low on disk space** | Enabled | Only enables the setting configuration. | [WarningMinDiskSpaceLimitInMB](/sharepoint/use-group-policy#warn-users-who-are-low-on-disk-space) |
| **Warn users who are low on disk space\Minimum available disk space: (Device)** | 2048 |  Specify a miminimum amount of available disk space in MB, and warn users when the OneDrive sync app (OneDrive.exe) downloads a file that causes them to have less than this amount. | [WarningMinDiskSpaceLimitInMB](/sharepoint/use-group-policy#warn-users-who-are-low-on-disk-space) |
