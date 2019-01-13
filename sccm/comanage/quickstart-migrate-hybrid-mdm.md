---
title: Migrate from hybrid MDM
titleSuffix: Configuration Manager
description: Hybrid MDM is deprecated, Intune standalone is required for co-management.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 456f32d5-8590-499f-a54d-d00618bc61f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Migrate from hybrid MDM for co-management

Hybrid mobile device management (MDM) is a deprecated feature. Support for hybrid MDM ends on 1 September 2019. For more information, see [Hybrid MDM with Configuration Manager and Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

Intune standalone is the recommended deployment topology, and is required for co-management. If you want to enable co-management, migrate from an Intune hybrid configuration to Intune standalone. 

<!--update with final video for this quickstart-->
In the following video, principal program manager Andrew McMurray and senior product marketing manager Mayunk Jain discuss and demo migrating from hybrid MDM:

> [!VIDEO https://www.youtube.com/embed/gA5q0_3bxPs]



## How to do it

Your migration to Intune standalone will be most successful when use a phased approach. With a phased migration, you move a small subset of users and devices while most of your users and devices are still managed with hybrid MDM. Once you verify the migration is successful, you can begin migrating more resources to Intune.

To begin the migration, use the [Microsoft Intune Data Importer tool](/sccm/mdm/deploy-use/migrate-import-data) to collect and automate the process of recreating the objects from Configuration Manager in your Intune standalone tenant. Next, change your MDM authority for a specific set of users, and test the functionality in Intune standalone. When this verification is done, change your MDM authority to Intune standalone for all users.

> [!Important]  
> If you're using on-premises conditional access in Configuration Manager, this functionality currently requires Intune hybrid.  

For more information on this migration process, see [Migrate hybrid MDM users and devices to Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).



## Case studies

Microsoft IT recently moved 130,000 users from Intune hybrid to Intune standalone in three months. For more information, see [How Microsoft uses Conditional Access - Endpoint Zone 1812](https://youtu.be/offk-KH7eIA?t=651). This video is a conversation between Microsoft corporate vice president Brad Anderson and Microsoft's chief information security officer Bret Arsenault, who personally oversaw the migration. 

A large pharmaceutical company moved 10,000 users from Intune hybrid to Intune standalone within a few weeks.

A large IT consulting firm in India migrated 40,000 users from Intune hybrid to Intune standalone in less than a month.



## Contact FastTrack

If you need assistance migrating from hybrid MDM at any point in the process, go to [Microsoft FastTrack](https://Microsoft.com/FastTrack/), sign in, and request assistance. 

For more information, see [Get help from FastTrack](/sccm/comanage/quickstart-fasttrack). 

