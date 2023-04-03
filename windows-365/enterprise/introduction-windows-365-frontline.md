---
# required metadata
title: What is Windows 365 Frontline?
titleSuffix:
description: Learn about Windows 365 Frontline.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 04/06/2023
ms.topic: overview
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: gkomatsu
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# What is Windows 365 Frontline?

Windows 365 Frontline is a version of [Windows 365](../overview.md) that helps organizations save costs by providing a single license to provision three Cloud PC virtual machines. For each Windows 365 Frontline license that you buy, you can provision three different Cloud PCs that can’t be used concurrently. Instead, each user receives a unique Cloud PC that they can use when the other two users on the same license aren’t signed into their Cloud PCs.

Windows 365 Frontline is designed specifically for workers who share computing resources and don't require 24/7 dedicated Cloud PCs. This system better supports organizations that are more elastic and distributed working across various of devices. Frontline Cloud PCs can be helpful for users who are:

- On a rotation schedule.
- Working across time zones and regions.
- Part-time workers.
- Contingent staff.

The maximum number of active Windows 365 Frontline Cloud PCs in your organization is equal to the number of Windows 365 Frontline licenses that you’ve purchased. For example, if you purchase 10 licenses, 30 Cloud PCs will be provisioned. Ten of those Cloud PCs can be active at a given time. The licenses are managed automatically based on active sessions. When a user ends their session, the license is released for another user to start using their Cloud PC.

Windows 365 Frontline is in [public preview](../public-preview.md).

## Licensing

During public preview, Windows 365 Frontline licenses can't be purchased through the Microsoft 365 admin center. Instead, contact your Microsoft representative.

Because Windows 365 Frontline licenses are applied at the tenant level, the Microsoft 365 admin center shows Windows 365 Frontline licenses as assigned to zero users. To see how many licenses are being used, use the Windows 365 [utilization report](report-cloud-pc-utilization.md).

To make sure users can continuously use their Cloud PCs after short breaks, the license isn't immediately released after a user signs off. 

## Managing Windows 365 Frontline Cloud PCs

Windows 365 Frontline Cloud PCs can be managed using Microsoft Intune, alongside other Cloud PCs and devices in your tenant. Windows 365 Frontline supports:

- Provisioning Cloud PCs after licenses are purchased.
- Managing Cloud PCs.
- Configuring and applying policies.
- Deploying applications.
- Performing remote actions on Cloud PCs.
- Reporting.

You can view your Cloud PCs on two pages:

- **All devices**: Turn on the **Model** column to differentiate between Frontline Cloud PCs and others.
- **All Cloud PCs**: This list can be filtered to show only Frontline Cloud PCs using the **PC type** filter. 

When inactive, Cloud PCs will be in a powered off state. This state makes sure that the license is available when another user on the same license signs in to their Cloud PC.

For the best user experience, make sure to:

- Configure the Windows Update Ring profiles.
- Set a time limit for idle Remote Desktop Sessions.

## Next steps

To learn more about Windows 365, see [What is Windows 365?](..\overview.md)
