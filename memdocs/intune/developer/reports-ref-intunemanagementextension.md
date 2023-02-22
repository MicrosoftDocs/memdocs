---
# required metadata
title: IntuneManagementExtension Entity
titleSuffix: Microsoft Intune 
description: Reference topic for the IntuneManagementExtension Entity category of entity collections in the Intune Data Warehouse API.
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
ms.assetid: 73DF3B90-6D52-4EF6-AFFD-1873A18C7421

# optional metadata
#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier3
- M365-identity-device-management
---

# Reference for Intune Management Extensions

The **intuneManagementExtensions** category contains entities for mobile devices that track information such as:

- Versions of an IntuneManagementExtension
- Installation status of an IntuneManagementExtension

## intuneManagementExtensionVersions

The **intuneManagementExtensionVersion** entity lists all the versions used by intuneManagementExtensions.

| Property  | Description | Example |
|---------|------------|--------|
| extensionVersionKey |Unique identifier of the intuneManagementExtensions version. | 1 |
| extensionVersion |The 4 digit version number. |1.0.2.0 |

## intuneManagementExtensionHealthStates

The **intuneManagementExtensionHealthState** lists all possible health states of the intuneManagementExtensions.

| Property  | Description | Example |
|---------|------------|--------|
| extensionStateKey |Unique identifier of health state. | 2 |
| extensionState |Health state of a IntuneManagementExtension. | Healthy |

## intuneManagementExtensions

The **intuneManagementExtension** lists the IntuneManagementExtensions health on each Windows 10 device per day.
The data is retained for the last 60 days. 


|      Property       |                         Description                         | Example |
|---------------------|-------------------------------------------------------------|---------|
|       dateKey       |               Unique identifier of the Date.                |   123   |
|      tenantKey      |              Unique identifier of the Tenant.               |   456   |
|      deviceKey      |              Unique identifier of the Device.               |   789   |
| extensionVersionKey | Unique identifier of the intuneManagementExtension version. |    1    |
|  extensionStateKey  |             Unique identifier of health state.              |    2    |

