---
# required metadata
title: Cloud PC utilization report for Windows 365
titleSuffix:
description: Learn about the Cloud PC utilization report in Endpoint analytics for Windows 365 Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 03/28/2023
ms.topic: overview
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;
ms.collection:
- M365-identity-device-management
- tier2
---

# Cloud PC utilization report (preview)

The Cloud PC utilization report helps you make sure that your licenses are assigned to active users. By reviewing Cloud PCs with low usage, you can decide if a Windows 365 license would better serve other users who might use these resources more often.

## Use the Cloud PC utilization report

To get to the **Cloud PC utilization** report, sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Cloud PC performance (preview)** > **View report** (under **Cloud PCs with low utilization**).

:::image type="content" source="./media/report-cloud-pc-utilization/view-report.png" alt-text="Screenshot of getting to the Cloud PC utilization report." lightbox="./media/report-cloud-pc-utilization/view-report.png":::

The report shows the following data aggregated for the last 28 days:

- This histogram shows user connection time in three sections:
  - **High active time connected**: More than 80 hours.
  - **Average active time connected**: 40-80 hours.
  - **Low active time connected**: Less than 40 hours.
  - **No active time connected**: Zero hours.
- List of individual Cloud PCs with the following columns:
  - **Device name**
  - **Primary user UPN**
  - **Active time connected**: The total hours that the user has been connected to the Cloud PC over the last 28 days.
  - **Last active time**: Last time the user was active on the Cloud PC.

You can use the filter options to see results for specific **Active time connected** and **Last active time** values. These options can help you understand usage patterns and identify Cloud PCs that are under-utilized (for example, those that are listed when using the filter **Last active time: No sign in for 28 days or more**.)

## Other reports

You can see similar utilization data on a per-Cloud PC basis:

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All Devices**.
2. Select a device and then select **Performance (preview)**.
3. You'll see **Time connected to device**. Under this chart, select **View report** to see more utilization data specific to this Cloud PC.

<!-- ########################## -->
## Next steps

[Remoting connection report](report-remoting-connection.md)
