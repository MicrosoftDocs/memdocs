---
# required metadata
title: What is Windows 365 Frontline?
titleSuffix:
description: Learn about Windows 365 Frontline.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 04/15/2024
ms.topic: overview
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
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

The maximum number of active Windows 365 Frontline Cloud PC sessions in your organization is equal to the number of Windows 365 Frontline licenses that you’ve purchased. For example, if you purchase 10 licenses, up to 30 Cloud PCs can be provisioned. Ten of those Cloud PCs can be active at a given time. The active sessions are managed automatically. When a user signs off from their Cloud PC, the session is released for another user to start using their Cloud PC. A concurrency buffer exists to exceed this maximum a limited number of times per day. For more information, see [Exceeding the maximum concurrency limit ](#exceeding-the-maximum-concurrency-limit).

Windows 365 Frontline is currently only available for Azure Global Cloud.

Frontline Cloud PCs can't be accessed directly from Remote Desktop app. Instead, you must use the Windows 365 web portal if you want to access your Frontline Cloud PC with the Remote Desktop app.

## Licensing

To use Windows 365 Frontline, you must be licensed for:

- Windows 11 Enterprise or Windows 10 Enterprise
- Microsoft Intune
- Microsoft Entra ID P1.

In addition to being available independently, Windows Enterprise, Intune, and Microsoft Entra ID licenses are included in:

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

## Exceeding the maximum concurrency limit

Windows 365 Frontline includes a concurrency buffer to let a tenant temporarily exceed the maximum concurrency limit for Windows 365 Frontline Cloud PCs.

For example, when workers overlap during a shift change, a previous worker might need to finish up something before signing off. Or, an incoming worker might need to start a few minutes early. The concurrency buffer is intended to allow for such rare and brief over usage to make sure workers aren’t impacted by unforeseen lockouts.

The concurrency buffer can be used up to four times per day with maximum of one hour in each instance. This hour starts from the moment the tenant exceeded the max concurrency limit.

### Temporary blocks

Excessive use of the concurrency buffer will temporarily block its further use for the next 48 hours. A temporary block is imposed when:

- On two or more occasions within a 24-hour period, the concurrency buffer is used for more than one hour.

### Permanent blocks

If the tenant is temporarily blocked more than two times in a seven day period, the tenant is permanently blocked from using the concurrency buffer.

While permanently blocked, you can still use your Frontline Cloud PCs up to the maximum concurrency limit.

To unblock your tenant, open a ticket with support from the Intune portal.

### Monitor the concurrency buffer

You can monitor the use of concurrency buffer with the Frontline connection hourly report. You can use the Frontline concurrency alert to receive alerts each time the concurrency buffer is activated.

## Features not yet supported Windows 365 Frontline

The following features aren't yet supported for Windows 365 Frontline.

- GPU Cloud PCs
- Resize a Cloud PC remote action
- [Move a Cloud PC](move-cloud-pc.md)

## Next steps

To learn more about Windows 365, see [What is Windows 365?](..\overview.md)
