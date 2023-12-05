---
title: Windows 365 Business Cloud PC location
description: Learn where Cloud PCs are located geographically.
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 05/09/2023
audience: Admin
ms.topic: article
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: alcort
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Windows 365 Business Cloud PC location

Windows 365 Business Cloud PCs are created in a location based on the billing address country/region of your organization. The billing address is used to determine two things:

- Whether Windows 365 is available for purchase in that region.
- Where Windows 365 Cloud PCs are created.

## Check if Windows 365 Business is available in your country/region

To find out if Windows 365 can be purchased in your country/region, follow these steps:

1. In your internet browser, go to [Microsoft 365 and Office 365 International Availability]( https://www.microsoft.com/microsoft-365/business/international-availability).
2. Scroll down to the **Windows 365** section.
3. Your country/region is supported if it’s listed in the **Countries and Regions** column.

## Where is a Cloud PC created?

When a Cloud PC license is assigned, it’s created in a particular geographic location. To find that location, follow these steps:

1. In your internet browser, go to [Where your Microsoft customer data is stored article](/microsoft-365/enterprise/o365-data-locations).
2. Find the country/region that corresponds to your billing address and select **Click to expand**.
3. The **Exchange Online** row identifies the location that your Cloud PC is created by default. If there's no capacity in that location, your Cloud PC will be created in the nearest location with capacity.

The billing address country/region doesn’t mean that the Cloud PC will necessarily reside in that country/region. Cloud PCs are created in the nearest supported location with available capacity. This location may or may not be  the billing address country/region.

## Next steps

[Get started with Windows 365 Business](get-started-windows-365-business.md)
