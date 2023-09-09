---
# required metadata
title: What is Windows 365 Frontline?
titleSuffix:
description: Learn about Windows 365 Frontline.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/17/2023
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

Windows 365 Frontline is a version of [Windows 365](../overview.md) that helps organizations save costs by providing a single license to provision three Cloud PC virtual machines. Each license:

- Lets you provision up to three Cloud PCs.
- Provides one concurrent session.

Windows 365 Frontline is designed specifically for workers who don't need 24/7 access to their dedicated Cloud PCs. This system better supports organizations that are more elastic and distributed, working across various devices. Frontline Cloud PCs can be helpful for users who are:

- On a rotation schedule.
- Working across time zones and regions.
- Part-time workers.
- Contingent staff.

The maximum number of active Windows 365 Frontline Cloud PC sessions in your organization is equal to the number of Windows 365 Frontline licenses that you’ve purchased. For example, if you purchase 10 licenses, up to 30 Cloud PCs can be provisioned. Ten of those Cloud PCs can be active at a given time. The active sessions are managed automatically. When a user signs off from their Cloud PC, the session is released for another user to start using their Cloud PC.

Windows 365 Frontline is currently only available for Azure Global Cloud.

Frontline Cloud PCs can't be accessed directly from Remote Desktop app. Instead, you must use the Windows 365 web portal if you want to access your Frontline Cloud PC with the Remote Desktop app.

## Licensing

To use Windows 365 Frontline, you must be licensed for:

- Windows 11 Enterprise or Windows 10 Enterprise
- Microsoft Intune
- Azure AD P1.

In addition to being available independently, Windows Enterprise, Intune, and Azure Active Directory (Azure AD) licenses are included in:

- Microsoft 365 E3
- Microsoft 365 E5
- Microsoft 365 F3
- Microsoft 365 A3
- Microsoft 365 A5
- Microsoft 365 Business Premium
- Microsoft 365 Education Student Use Benefit subscriptions

Windows 365 Frontline licenses can be purchased through the Microsoft 365 admin center. You can confirm your license quantities under **Billing - Your Products**.

Windows 365 Frontline licenses are pooled licenses applied at the tenant level, not assigned directly to users. The Microsoft 365 admin center shows Windows 365 Frontline licenses as assigned to zero users. To see how many licenses are being used, use the Windows 365 [utilization report](report-cloud-pc-utilization.md).

Windows 365 Frontline is a separate product and isn't governed by the Microsoft 365 F1/F3 license eligibility conditions.

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

When inactive, Cloud PCs are in a powered off state. You can confirm the power state of the Cloud PC in **Overview** page for a device.

For the best user experience, make sure to:

- Configure the Windows Update Ring profiles.
- Set a time limit for idle Remote Desktop Sessions.

## Next steps

To learn more about Windows 365, see [What is Windows 365?](..\overview.md)
