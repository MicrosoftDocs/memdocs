---
# required metadata
title: Cloud PC utilization report for Windows 365
titleSuffix:
description: Learn about the Cloud PC utilization report in Endpoint analytics for Windows 365 Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 10/12/2022
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

To get to the **Cloud PC utilization** report, sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Cloud PC performance (preview)** > **View report** (under **Cloud PCs with low utilization**).

![Screenshot of getting to the Cloud PC utilization report.](./media/report-cloud-pc-utilization/view-report.png)

The report shows the following data aggregated for the last 28 days:

- This histogram shows user connection time in three sections:
  - **High time connected**: More than 80 hours.
  - **Average time connected**: 40-80 hours.
  - **Low time connected**: Less than 40 hours.
- List of individual Cloud PCs with the following columns:
  - **Device name**
  - **Primary user UPN**
  - **Total time connected**: The total hours that the user has been connected to the Cloud PC over the last 28 days.
  - **Days since last sign in**

You can use the filter to see only data for a specific usage group.

## Other reports

You can see similar utilization data on a per-Cloud PC basis:

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All Devices**.
2. Select a device and then select **Performance (preview)**.
3. You'll see **Time connected to device**. Under this chart, select **View report** to see more utilization data specific to this Cloud PC.

<!-- ########################## -->
## Next steps

[Remoting connection report](report-remoting-connection.md)
