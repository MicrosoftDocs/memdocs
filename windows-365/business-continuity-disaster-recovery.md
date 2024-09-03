---
# required metadata
title: Business continuity and disaster recovery with Windows 365
titleSuffix:
description: Learn about business continuity and disaster recovery with Windows 365
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/28/2024
ms.topic: overview
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: docoombs
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier1
---

# Business continuity and disaster recovery overview

Windows 365 provides highly resilient user cloud pcs, including:

- 99.9% highly available Windows 365 Cloud PC user sessions as defined in the [Windows 365 SLA](https://www.microsoft.com/licensing/docs/view/Service-Level-Agreements-SLA-for-Online-Services).
- Disk storage with data object resiliency of 11 9s.
- Automated in-zone disaster recovery for compute.
- Recovery Point Objective (RPO) of ~0.

Windows 365 is part of Microsoft 365 and seamlessly uses Windows and Microsoft 365 solutions, features, and tools. This integration helps to make sure that user data and user context are portable and resilient. Important optional Windows and Microsoft 365 solutions include:

- OneDrive
- OneDrive for Business
- OneDrive Known Folder Move
- Windows Sync Your Settings
- Enterprise State Roaming

Using these Windows and Microsoft 365 solutions preserves user context and user data in cases when an individual Cloud PC has a non-Azure failure. These failures, like a failed OS update or user configuration errors, can result in an inaccessible Cloud PC, even if the underlying system is healthy. When using Windows 365 with these solutions, you can enjoy highly resilient and portable user data and user context, even if a specific Cloud PC must be reprovisioned from a base image.

## Data Resilience

If there's a larger disruption, like a full zone or region outage, the disk storage provided makes sure that data objects on the Cloud PC OS disks are 99.999999999% resilient against data loss, over a given year.

## Automated in-zone Disaster Recovery for Compute

Although rare, in-zone failures may disrupt Cloud PC operations. Examples of such failures include:

- vNic failure
- compute failure
- storage plane failure
- compute power failure

Azure automatically identifies compute failures and automatically moves the user workload to another resource in the zone.

If a user is actively using a session, there may be a slight disruption to the user while the service is restored. After restoration, the user must restore the connection by signing into their Cloud PC session again. If an in-zone failure occurs while the user is signed in and actively using their Cloud PC session, the user loses access until the system is restored.

Storage systems are separate from compute functions, and use storage redundancy to help deliver Windows 365 disaster recovery with an RPO of ~0. Automated Windows 365 disaster recovery is based on an up-to-date copy of the OS disk, with an RPO of ~0. Therefore, the process of recovery starts automatically because there's no need to accept the data loss associated with a past point-in-time recovery.

## OneDrive, OneDrive for Business and OneDrive with Known Folder Move

Using Windows 365 with OneDrive and OneDrive Known Folder Move organizations provides these benefits:

- [Portable user data access](/onedrive/plan-onedrive-enterprise) across all physical and Cloud PCs.
- [Active/Active cross region user data resilience](/compliance/assurance/assurance-sharepoint-onedrive-data-resiliency) shared between Cloud PCs and all other authenticated use workspaces.
- User context portability and cross-region resilience using [Known Folder Move](/onedrive/redirect-known-folders).
- User data and Known Folder Move based context resilience with an [Recovery Time Objective (RTO) and RPO of 0](/compliance/assurance/assurance-sharepoint-onedrive-data-resiliency#blob-storage-resilience).
- Data [Versioning, corruption and accidental delete protection, and Point in Time Restore](/compliance/assurance/assurance-sharepoint-onedrive-data-resiliency#versioning-and-files-restore).

For more information on deploying and managing OneDrive for Small business, Medium-sized business, and Enterprises, see [this article](/onedrive/plan-onedrive-enterprise#deployment-and-management-options).

## Windows Sync Your Settings and Enterprise State Roaming

Both Windows base [Sync your Settings](https://support.microsoft.com/windows/about-sync-settings-on-windows-10-devices-deebcba2-5bc0-4e63-279a-329926955708) and [Enterprise State Roaming](/azure/active-directory/devices/enterprise-state-roaming-windows-settings-reference) retain Windows client user settings for portability and/or resilience (back up). To understand the differences between Sync your Settings and Enterprise State Roaming, see [What is enterprise state roaming?](/azure/active-directory/devices/enterprise-state-roaming-overview)

For an overview of Windows Settings, see [Windows Settings overview](/azure/active-directory/devices/enterprise-state-roaming-windows-settings-reference#windows-settings-overview) section of the Enterprise State Roaming document. To understand setting details such as grouping and applicability, see [Windows Settings details](/azure/active-directory/devices/enterprise-state-roaming-windows-settings-reference#windows-settings-details) in the Enterprise State Roaming document.

## Cloud PC Management Service

The Cloud PC management service includes:

- [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)
- [Cloud PC end user portal](https://Windows365.microsoft.com)

The Cloud PC Management Service has a regionally redundant architecture that is designed to be highly available, with a target uptime of 99.99%. If there's a Management Service outage, the service has the following target objectives:

- RTO of < 6 hours.
- RPO of <30 minutes for changes made in the management service.

If there's a Management Service outage, assuming no other impacting outages, users won’t be able to access their Cloud PC sessions through the end user portal. Users can still access their Cloud PC instances by using any of the following options:

- a native app.
- directly from a bookmark for their Cloud PC session.
- [https://rdweb.wvd.microsoft.com/webclient/index.html](https://rdweb.wvd.microsoft.com/webclient/index.html)

## Summary

Windows 365 offers organizations with user workspaces that are:

- Highly available and backed by a financially guaranteed SLA.
- Automatically recovered if there's an in-zone Azure compute failure, with an expected RTO of <10 minutes and an RPO of ~0.
- Automatic recovery, after the underlying regional or zone failure, with an RPO of ~0.

When organizations use Windows 365 with specified Windows and Microsoft 365 solutions and features, they enjoy:

- An even higher level of user data and user context resilience.
- Portable user data and user context.
- Active/Active data resilience providing ongoing access to user data, through OneDrive, even during a Windows 365 outage.

<!-- ########################## -->
## Next steps

[Learn about troubleshooting Windows 365 issues](troubleshooting.md).
