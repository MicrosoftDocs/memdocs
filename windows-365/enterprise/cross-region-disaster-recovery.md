---
# required metadata
title: Cross region disaster recovery in Windows 365
titleSuffix:
description: Learn cross region disaster recovery in Windows 365.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/01/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
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
- tier2
---

# Cross region disaster recovery in Windows 365

Windows 365 cross region disaster recovery is an optional service for Windows 365 Enterprise that protects Cloud PCs and data against regional outages. When properly licensed and activated, it creates geographically distant temporary copies of Cloud PCs that can be accessed in the selected backup region. These copies help increase availability and preserve productivity.

Admins must manually activate and deactivate cross region disaster recovery.

The ability to restore in an alternate region depends on available capacity in that region at the time of the outage. Regardless of whether the device is able to restore at any given time, restore points are resilient in the alternate region.

## Licensing

The following Windows 365 Enterprise add-on license is required for each user added to the service:

- Windows 365 cross region disaster recovery

## Temporary Cloud PC

When activated, cross region disaster recovery temporarily creates a copy of the users’ Clouds PCs in an alternate region. It uses the latest restore point for each Cloud PC, and includes all installed applications, user settings, and data.

When the admin deactivates cross region disaster recovery after the outage event, the temporary Cloud PC is deleted. No applications, settings, data, or other information is preserved from the temporary Cloud PC.

## Restore point objective (RPO) and restore time objective (RTO)

If there's an outage, the service has the following target objectives for cross region disaster recovery:

- RTO of < 4 hours for tenants with less than 50,000 Cloud PCs in a region.
- RPO of <4 hours.

Devices are restored as quickly as possible. You can target specific devices to recover earlier than others. The speed and scale of the restoration process is per region and per tenant. Therefore, when performing multiple cross region disaster recovery activation actions, you can prioritize certain devices to be restored in earlier actions. This strategy prioritizes certain devices but doesn’t change the overall RTO for the full environment.

## Multiple region outages

Cross region disaster recovery protects against data loss if there’s a regional outage or a complete data failure in the primary region. If the backup region lacks available capacity, or isn’t healthy during a disaster recovery event, the backup Cloud PC isn't provisioned. However, the data is still preserved and remain accessible in the backup region.

## User experience

When cross region disaster recovery is activated, affected users receive a warning the next time they sign in to their Cloud PC.

After the cross region disaster recovery activation is complete, when a user signs in to their Cloud PC they receive a temporary Cloud PC. With this device, they get full user context, including:

- Configuration
- Data stored on the local disk
- User-installed applications up to the RPO for the device.

When the cross region disaster recovery is deactivated, the temporary device is discarded. The user is returned to their primary device, as it was before the disaster recovery event. No applications, settings, data, or other information saved to the Local OS disk (C drive) is preserved. Data stored in cloud storage, cloud applications, and so on, are unaffected by the Cloud PC disaster recovery event.

<!-- ########################## -->
## Next steps

Learn how to [set up](cross-region-disaster-recovery-set-up.md), [activate/deactivate](cross-region-disaster-recovery-activate.md), and [monitor](cross-region-disaster-recovery-report.md) cross region disaster recovery.
