---
# required metadata

title: Data storage and processing in Intune
titleSuffix: Microsoft Intune
description: Learn how personal data is stored and processed in Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: edb07842-6a16-482e-8c1d-541a29e169a8

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Data storage and processing in Intune

After Intune [collects the data](privacy-data-collect.md), storage and processing of that data proceeds as detailed below.

## Storing personal data

All non-telemetry data collected is processed through the Intune service and is stored in one or more of the following storage locations: 

- SQLAzure 
- Reliable Collections (Service fabric)  
- Azure storage 

Telemetry (service logs, performance logs, errors, and so on) that are key to monitoring and providing a stable service are sent to Microsoft's telemetry data stores.

### Storage locations

Microsoft offers and operates Intune services in many regions worldwide. Intune respects the storage location elections made by the administrator for Customer Data.

For more information, see [Where your data is located?](https://www.microsoft.com/trust-center/privacy/data-location)

### Personal data retention

In general, personal data is retained by Intune until 30 days after the user is removed from Intune management.

Telemetry data collected as part of Intune usage is retained for a maximum of 30 days.

Audit logs are retained for up to one year.

## Processing personal data

Intune processes personal data with ISO certified systems. For more information, see the [Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp).

### Profiling and marketing

Microsoft Intune does not use any personal data collected as part of providing the service for profiling or marketing purposes. 

### Restrict processing of personal data

To restrict the processing of a user's personal data, you can delete the users account by:
1. Exporting an electronic copy of the personal data of the user, including
    - accounts
    - service data
    - associated logs
2. Deleting the user's account and associated data from Intune.

## Next steps

Find out more about how Intune [secures and shares](privacy-data-secure-share.md) personal data. 
