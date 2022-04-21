---
# required metadata
title: Managing Cloud PCs with Microsoft Intune
titleSuffix:
description: Learn how to  manage Windows 365 devices
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/02/2021
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Device management overview for Cloud PCs

To manage your Cloud PCs, you’ll use Microsoft Intune, a service of [Microsoft Endpoint Manager](https://admin.microsoft.com/). Intune is a 100% cloud-based mobile device management (MDM) and mobile application management (MAM) provider for your apps and devices (including Cloud PCs). To sign in to Intune, go to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

## Cloud PC overview page

The Overview tab is the landing page for managing your Cloud PCs. To see it, sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows 365** (under **Provisioning**).

Here you'll see some info to give you a quick idea of how your Cloud PCs are doing:

- **Provisioning** status: A summary of the Cloud PC state in your organization.
- **Connection health**:  A summary of the Azure network connection health in your organization.  

## All Cloud PCs page

The **All Cloud PCs** page displays a summary and list view detailing the state information for each of the Cloud PCs in your organization.

The list view lets you search, filter, and sort. It automatically refreshes every five minutes.

If a user has multiple Windows 365 SKUs assigned to them, they’ll get multiple Cloud PCs. This results in multiple rows for a single user in the **All Cloud PCs** list view.

### Column details

**Name**: The name of the Cloud PC, which is composed of the assigned provisioning policy and the assigned user’s name. For example, My first provisioning policy – Henry Ross.

**Device name**: The Windows computer name, which is also used in Intune and Azure AD.

**Image**: The image used during provisioning. This might not be the current Cloud PC version. For example, an administrator may have updated Windows using Windows Update for Business and this wouldn’t be reflected in this list view.  

**PC type**: The Windows 365 SKU assigned to the user. A user may have more than one license/SKU assigned to them. If so, they’ll have two Cloud PCs in this list view.  

**Status**: The current provisioning status of the Cloud PC. Possible states include:
  
- **Provisioned**: The Cloud PC provisioning was successful and the assigned user can log on.
- **Provisioning**: Provisioning is currently in progress.  
- **Provisioned with warnings**: If a non-critical step in the provisioning process fails, user access isn’t blocked but a warning is flagged.  
- **Not provisioned**: The user has been assigned a Windows 365 license but no provisioning policy has been targeted. To provision a Cloud PC, assign this user to a provisioning policy.

  When a user is licensed with a Windows 365 license, a new row is automatically created in the **All Cloud PCs** list. If the user also has a provisioning policy assigned to them, a Cloud PC is automatically provisioned.

  If they don’t have a provisioning policy assigned to them, no Cloud PC is created. This is indicated by a **Not provisioned** status. This is not a bad state. It’s an informational state and we encourage you to assign a provisioning policy to make the most of your Windows 365 investment.  

- **Deprovisioning**: This short-lived status indicates that the 7-day grace period has ended and the Cloud PC is now being actively deprovisioned. Once the deprovisioning is complete, the Cloud PC can’t be restored and a new Cloud PC must be provisioned for the affected user(s).
- **Failed**: The provisioning process failed for this Cloud PC. Select the link to get a detailed reason for the failure, troubleshoot, and retry provisioning.
- **In grace period**: When a license/assignment change occurs for a user with a current Cloud PC, the Cloud PC object is marked as **In grace period**. Grace periods help admins avoid licensing/targeting mistakes that might cause users to lose access to their Cloud PC.

  With the nature of dynamic Azure AD groups, users can become unassigned to a provisioning policy or Windows 365 license. As license and provisioning policies are required for a Cloud PC to function, removing either or both will result in the end user losing access to their Cloud PC.

  When a Cloud PC is in a grace period, the user can continue using the Cloud PC for seven days. After the seven day grace period expires, the user will be logged off the Cloud PC and they’ll lose access.

  If the grace period was triggered in error, you have seven days to resolve the breaking change to get the Cloud PC switched back to **Provisioned**.

  You can manually end the grace period by using the [End grace period](end-grace-period.md) option.
- **Pending**: If there are not enough available licenses in your tenant to process the provisioning request, new Cloud PCs are marked as **Pending**.

  Your Windows 365 tenant can only have as many active Cloud PCs as the license allocation allows. An active Cloud PC can either be in a **Provisioned** or **In grace period** state.

  To begin provisioning on Pending Cloud PCs, free up some Windows 365 licenses or end grace period on Cloud PCs in the grace period state. 

**User**: The user assigned to the Cloud PC.  

**Date modified**: The timestamp of the last change of state of the Cloud PC.  

<!-- ########################## -->
## Next steps

[Remotely managed Cloud PCs](remotely-manage-cloud-pc.md).
