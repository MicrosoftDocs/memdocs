---
# required metadata
title: Cloud PC connection quality report for Windows 365
titleSuffix:
description: Learn about the Cloud PC connection quality report for Windows 365 Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 09/13/2023
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

# Cloud PC connection quality report (preview)

The **Cloud PC connection quality** report helps you evaluate your users' connection experiences on their Cloud PCs.

## Use the Cloud PC connection quality report

To get to the **Cloud PC connection quality** report, sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Cloud PC performance (preview)** > **View report** (under **Connection quality (preview)**).

![Screenshot of getting to the Cloud PC connection quality report](./media/report-cloud-pc-connection-quality/view-report-connection-quality.png)

The device list shows the individual Cloud PCs with the following columns:

- **Device name**
- **Round-trip time (P50)** (RTT): The number of milliseconds it took to establish the user connection to the Cloud PC. Lower values indicate better round-trip connectivity.
- **Available bandwidth (P50)**: Internet bandwidth during the user's attempt to connect to their Cloud PC.
- **Remoting sign-in time (P50)**: The number of seconds it took the user to complete the sign-in process.

Each metric is aggregated to a P50 median level over the last 24 hours. This is to ensure spikes and troughs are smoothed in order to provide a good understanding of the overall end-user connectivity experience.

You can use **Add filter** to limit the histogram and table data to specific time spans and round-trip time ranges.

## Other reports

You can see similar quality data on a per-Cloud PC basis:

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All Devices**.
2. Select a device and then select **Performance (preview)**.
3. You'll see **Connection quality (preview)**. Under this chart, select **View report** to see more connection data specific to this Cloud PC.

<!-- ########################## -->
## Next steps

[Remoting connection report](report-remoting-connection.md)
