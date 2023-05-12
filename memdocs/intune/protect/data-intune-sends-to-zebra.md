---
# required metadata

title: Data Intune sends to Zebra
titleSuffix: Microsoft Intune
description: List of data that Intune sends to Zebra when Android enterprise device management is enabled with Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/11/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: a5c3bec4-18ed-11e8-accf-0ed5f89f718b


# optional metadata

#ROBOTS:
#audience:

ms.reviewer: Jessica Yang 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Data Intune sends to Zebra

When Zebra LifeGuard Over-the-Air (LG OTA) is enabled for your tenant, Microsoft Intune establishes a connection with Zebra and shares the following data with Zebra:

The following table lists the data that Microsoft Intune sends to Google when device management is enabled on a device:


| Data sent to Zebra | Used for | Example |
|:---:|:---:|---|
| Serial number | Used to prove ownership of device against a known service contract with Zebra, determine current state of the device, and for the Android update process. | Unique identifier, example format: 124411614K0593 |
| Deployment settings | Used to deliver Android updates. |<li>Device Model: TC8300</li><li>Update type: Custom Time zone offset in minutes: 300</li><li>BSP (Board Support Package): 11.15.05.00</li><li>OS Version: 11</li><li>Patch Number: U20</li><li>Schedule mode: Latest</li><li>Schedule duration in days: 20</li><li>Download network type: Wifi</li><li>Download start date and time:</li><li>2022-03-25T15:04:51.8607086Z</li><li>Installation start date and time:</li><li>2022-03-25T15:04:51.8607086Z</li><li>Installation window start time: 19:00:00</li><li>Installation window end time: 19:00:00</li><li>Minimum Battery level percentage: 30</li><li>Require device to be on charger: true</li>|

To stop using Zebra services with Microsoft Intune and delete the data, you must both disconnect from Zebra LifeGuard OTA in Microsoft Intune, and also delete the data from your Zebra account by filing a customer request with Zebra.
