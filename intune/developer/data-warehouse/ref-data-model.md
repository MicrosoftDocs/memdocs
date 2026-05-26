---
title: Data Warehouse Data Model
description: The Microsoft Intune Data Warehouse samples data daily to provide a historical view of your continually changing mobile environment.
ms.date: 10/30/2024
ms.topic: reference
ms.reviewer: jamiesil
ms.collection:
- M365-identity-device-management
---

# Microsoft Intune Data Warehouse Data Model

The Intune Data Warehouse samples data daily to provide a historical view of your continually changing environment of mobile devices. The view is composed of related entities in time.

## Entities: Entity sets

The warehouse exposes data in the following high-level areas:

- App protection enabled apps and usage
- Enrolled devices, properties, and inventory
- Apps and software inventory
- Device configuration and compliance policies

These areas contain the entities that are meaningful to your Intune environment. You find details about the entity sets in the following topics:

- [Application](ref-application.md)
- [Date](ref-date.md)
- [Devices](ref-devices.md)
- [Intune Management Extension](ref-intune-management-extension.md)
- [Policy](ref-policy.md)
- [Mobile App Management (MAM)](../../app-management/overview.md)
- [User](ref-user.md)
- [User Device Associations](ref-user-device.md)

## Relationships: Star-schema model

The warehouse organizes the entities in relationships that are meaningful to the type of questions you want to ask. For example, you can review the number of installations of an in-house developed Android application. The structure of the data warehouse enables you to gain insight into your mobile environment. In turn, analytics tools, such as Microsoft Power BI, can use the Data Warehouse data model to create visualizations and dynamic dashboards.

The entities and relationships use a star-schema model. A star-schema correlates facts over the dimension of time. A *fact* in the context of the model is a quantitative measurement such as the number of devices, number of apps, or time of enrollment. Fact tables store a lot of data. They can get very large, and so they typically limit information to 30 days. A *dimension* provides context to the facts. Where the fact measures what happened, the dimensions indicate to whom it happened. Dimension tables, such as the **User** table, are smaller and can retrain data for longer periods of time than fact tables.

A star-schema model is optimized for flexibility and data analysis so that you can create the reports needed to understand your evolving mobile environment.

## Time: Daily snapshots

The warehouse is downstream from your Intune data. Intune takes a daily snapshot at Midnight UTC and stores the snapshot in the warehouse. The duration of held snapshots vary from fact table to fact table. Some may hold seven days, others 30 days, and some even longer durations.

> [!NOTE]
> The Data Warehouse does not sync Jamf devices. For more information about Jamf, see [Troubleshooting Jamf Pro integration with Microsoft Intune](/troubleshoot/mem/intune/troubleshoot-jamf) and [Data Jamf Pro sends to Intune](../../privacy/data-sharing/ref-jamf-to-intune.md).

## Next steps

- To learn more about how the data warehouse tracks a user's lifetime in Intune, see [User lifetime representation in the Intune Data Warehouse](ref-user-timeline.md).
- To learn more about working with data warehouses, see [Microsoft Fabric Data Warehouse introduction](/fabric/data-warehouse/tutorial-introduction).
- To learn more about working with Power BI and a data warehouse in [Create a new Power BI report by importing a dataset](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/).
