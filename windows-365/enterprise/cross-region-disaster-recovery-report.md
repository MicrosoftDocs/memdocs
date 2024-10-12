---
# required metadata
title: Cross region disaster recovery report.
titleSuffix:
description: Learn about the Cross region disaster recovery report in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/28/2024
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
# Cloud PCs cross region disaster recovery status report

The **Cloud PCs cross region disaster recovery status** report shows you pertinent information about the health of your [cross region disaster recovery](cross-region-disaster-recovery.md).

## Use the Cloud PCs cross region disaster recovery status report

To get to the **Cloud PCs cross region disaster recovery status report**, sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Cloud PC overview** > **Cross region disaster recovery status**.

The device list shows the individual Cloud PCs with the following columns:

- **Activation expiration**
- **Configuration alert**
  - **Healthy**
  - **Unhealthy**
- **Cross region enabled**
  - **Yes**
  - **No**
- **Current restore point**
- **Device name**
- **Disaster recover status**
  - **Active outage**
  - **Activation expiring**
  - **Not active**
- **License type**
  - **Cross region**
  - **Premium**
  - **None**
- **User principal name**
- **User settings**

Each row in the report gives links to the specific Cloud PC where you can find greater detail regarding the devices connection history and related performance.
You can use the **Columns** and **Add filter** options to customize the report. Filters are available for:

- **Activation expiration**
- **Configuration alert**
- **Cross region enabled**
- **Disaster recover status**
- **License type**

<!-- ########################## -->
## Next steps

Learn how to [set up](cross-region-disaster-recovery-set-up.md) and [activate/deactivate](cross-region-disaster-recovery-activate.md) cross region disaster recovery.
