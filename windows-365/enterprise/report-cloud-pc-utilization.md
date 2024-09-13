---
# required metadata
title: Cloud PC utilization report for Windows 365
titleSuffix:
description: Learn about the Cloud PC utilization report in Endpoint analytics for Windows 365 Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 03/07/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
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

The Cloud PC utilization report helps you monitor and optimize Cloud PC usage in your organization. It shows you how much time users spend on their Cloud PCs and when they last connected to them.

By reviewing Cloud PCs with low usage, you can reduce costs by:

- Reassigning under-used Cloud PC licenses to other users who might use them more often.
- Identifying and deprovisioning Cloud PCs that are inactive for long periods of time.

## Use the Cloud PC utilization report

To get to the **Cloud PC utilization** report, sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Cloud PC performance** > **Cloud PCs utilization (preview)**.

:::image type="content" source="./media/report-cloud-pc-utilization/view-report.png" alt-text="Screenshot of getting to the Cloud PC utilization report." lightbox="./media/report-cloud-pc-utilization/view-report.png":::

## Cloud PC utilization (preview) report page (tenant data)

The report shows the following tenant data aggregated for the last four weeks:

- This histogram shows the number of Cloud PCs connected for each range:
  - **High time connected**: More than 80 hours.
  - **Average time connected**: 40-80 hours.
  - **Low time connected**: Less than 40 hours.
  - **No active time connected**: Zero hours.
- List of individual Cloud PCs with the following columns:
  - **Device name**
  - **Primary user UPN**: The user's identifier in Active Directory in the form of an email address.
  - **PC type**
  - **Time connected**: The total hours that the user has been connected to the Cloud PC over the last four weeks.
  - **Date last connected**: The date when the user most recently connected to their Cloud PC (within the last 60 days). If the user isn't currently connected to the Cloud PC, this date is the sign out time. If the user is connected to the Cloud PC, this date is the most recent connection time.
  - **Date created**: The date the Cloud PC was created.

### Filters

The **Add filters** control lets you filter the table by:

- **PC type**
- **Time connected**
- **Date last connected**

You can use these filters to help you understand usage patterns and identify Cloud PCs that are underused and can be deprovisioned or downgraded.

## Device level data

You can see similar utilization data on a per-Cloud PC basis:

1. sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Cloud PC performance** > **Cloud PCs utilization (preview)**.
2. Select a device and then select **Performance (preview)**.
3. The **Time connected** section shows usage data for this Cloud PC. For more detail, in this section, select **View report**.

<!-- ########################## -->
## Next steps

[Remoting connection report](report-remoting-connection.md)
