---
# required metadata
title: Data Warehouse data model
titleSuffix: Microsoft Intune
description: The Microsoft Intune Data Warehouse samples data daily to provide a historical view of your continually changing mobile environment.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: 4D04D3D9-4B6C-41CD-AAF8-466AF8FA6032

# optional metadata
#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Microsoft Intune Data Warehouse data model

The Intune Data Warehouse samples data daily to provide a historical view of your continually changing environment of mobile devices. The view is composed of related entities in time.

## Entities: Entity sets

The warehouse exposes data in the following high-level areas:

- App protection enabled apps and usage
- Enrolled devices, properties, and inventory
- Apps and software inventory
- Device configuration and compliance policies

These areas contain the entities that are meaningful to your Intune environment. You find details about the entity sets in the following topics:

- [Application](reports-ref-application.md)
- [Date](reports-ref-date.md)
- [Devices](reports-ref-devices.md)
- [Intune Management Extension](reports-ref-intunemanagementextension.md)
- [Policy](reports-ref-policy.md)
- [Mobile App Management (MAM)](../apps/app-management.md)
- [User](reports-ref-user.md)
- [User Device Associations](reports-ref-user-device.md)

## Relationships: Star-schema model

The warehouse organizes the entities in relationships that are meaningful to the type of questions you want to ask. For example, you can review the number of installations of an in-house developed Android application. The structure of the data warehouse enables you to gain insight into your mobile environment. In turn, analytics tools, such as Microsoft Power BI, can use the Data Warehouse data model to create visualizations and dynamic dashboards.

The entities and relationships use a star-schema model. A star-schema correlates facts over the dimension of time. A *fact* in the context of the model is a quantitative measurement such as the number of devices, number of apps, or time of enrollment. Fact tables store a lot of data. They can get very large, and so they typically limit information to 30 days. A *dimension* provides context to the facts. Where the fact measures what happened, the dimensions indicate to whom it happened. Dimension tables, such as the like the **User** table are smaller and can retrain data for longer periods of time= than fact tables.

A star-schema model is optimized for flexibility and data analysis so that you can create the reports needed to understand your evolving mobile environment.

## Time: Daily snapshots

The warehouse is downstream from your Intune data. Intune takes a daily snapshot at Midnight UTC and stores the snapshot in the warehouse. The duration of held snapshots vary from fact table to fact table. Some may hold seven days, others 30 days, and some even longer durations.

> [!NOTE]
> The Data Warehouse does not sync Jamf devices. For more information about Jamf, see [Troubleshooting Jamf Pro integration with Microsoft Intune](/troubleshoot/mem/intune/troubleshoot-jamf) and [Data Jamf Pro sends to Intune](..\protect\data-jamf-sends-to-intune.md).

## Next steps

- To learn more about how the data warehouse tracks a user's lifetime in Intune, see [User lifetime representation in the Intune Data Warehouse](reports-ref-user-timeline.md).
- To learn more about working with data warehouses in the [Create First Data WareHouse](https://www.codeproject.com/Articles/652108/Create-First-Data-WareHouse).
- To learn more about working with Power BI and a data warehouse in [Create a new Power BI report by importing a dataset](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/).