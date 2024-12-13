---
# required metadata
title: Managing Cloud PCs with Microsoft Intune
titleSuffix:
description: Learn how to  manage Windows 365 devices
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/25/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Device management overview for Cloud PCs

To manage your Cloud PCs, you’ll use the [Microsoft Intune admin center](https://admin.microsoft.com/). Intune is a 100% cloud-based mobile device management (MDM) and mobile application management (MAM) provider for your apps and devices (including Cloud PCs). To sign in to Intune, go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

## Cloud PC overview page

The Overview tab is the landing page for managing your Cloud PCs. To see it, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows 365** (under **Provisioning**).

Here you'll see some info to give you a quick idea of how your Cloud PCs are doing:

- **Provisioning** status: A summary of the Cloud PC state in your organization.
- **Azure network connection health**:  A summary of the Azure network connection health in your organization.  

If you have more Frontline Cloud PCs provisioned than available licenses, a warning appears on this page. Also, you can't provision new Cloud PCs until you deprovision Cloud PCs to match the number allowed.

## All Cloud PCs page

The **All Cloud PCs** page displays a summary and list view detailing the state information for each of the Cloud PCs in your organization.

The list view lets you search, filter, and sort. It automatically refreshes every five minutes.

If a user has multiple Windows 365 SKUs assigned to them, they get multiple Cloud PCs. This situation results in multiple rows for a single user in the **All Cloud PCs** list view.

### Column details

**Device name**: The Windows computer name, which is also used in Intune and Microsoft Entra ID.

**Provisioning policy**: The policy used to create the device.

**Image**: The image used during provisioning. This image might not be the current Cloud PC version. For example, an administrator may have updated Windows using Windows Update client policies and this update wouldn’t be reflected in this list view.  

**PC type**: The Windows 365 SKU assigned to the user. A user may have more than one license/SKU assigned to them. If so, they have more Cloud PCs in this list view.  

**Status**: The current provisioning status of the Cloud PC. Possible states include:
  
- **Provisioned**: The Cloud PC provisioning was successful and the assigned user can sign in.
- **Provisioning**: Provisioning is currently in progress.  
- **Provisioned with warnings**: If a non-critical step in the provisioning process fails, user access isn’t blocked, but a warning is flagged.  
- **Not provisioned**: The user has been assigned a Windows 365 license but no provisioning policy has been targeted. To provision a Cloud PC, assign this user to a provisioning policy.

  When a user is licensed with a Windows 365 license, a new row is automatically created in the **All Cloud PCs** list. If the user also has a provisioning policy assigned to them, a Cloud PC is automatically provisioned.

  If they don’t have a provisioning policy assigned to them, no Cloud PC is created. This situation is indicated by a **Not provisioned** status. This isn't a bad state. It’s an informational state and we encourage you to assign a provisioning policy to make the most of your Windows 365 investment.  

- **Deprovisioning**: This short-lived status indicates that the seven-day grace period has ended and the Cloud PC is now being actively deprovisioned. Once the deprovisioning is complete, the Cloud PC can’t be restored and a new Cloud PC must be provisioned for the affected user(s).
- **Failed**: The provisioning process failed for this Cloud PC. Select the link to get a detailed reason for the failure, troubleshoot, and retry provisioning.
- **In grace period**: When a license/assignment change occurs for a user with a current Cloud PC, the Cloud PC object is marked as **In grace period**. Grace periods help admins avoid licensing/targeting mistakes that might cause users to lose access to their Cloud PC.

  With the nature of dynamic Microsoft Entra groups, users can become unassigned to a provisioning policy or Windows 365 license. As license and provisioning policies are required for a Cloud PC to function, removing either or both results in the end user losing access to their Cloud PC.

  When a Cloud PC enters a grace period, an alert is triggered. The alert appears in the Microsoft Intune admin center as a pop-up notification. For more information about customizing alerts, including setting up e-mail notifications, see [Alerts in Windows 365](alerts.md).

  When a Cloud PC is in a grace period, the user can continue using the Cloud PC for seven days. After the seven day grace period expires, the user will be logged off the Cloud PC, and they’ll lose access.

  If the grace period was triggered in error, you have seven days to resolve the breaking change to get the Cloud PC switched back to **Provisioned**.

  You can manually end the grace period by using the [End grace period](end-grace-period.md) option.
- **Pending**: If there aren't enough available licenses in your tenant to process the provisioning request, new Cloud PCs are marked as **Pending**.

  Your Windows 365 tenant can only have as many active Cloud PCs as the license allocation allows. An active Cloud PC can either be in a **Provisioned** or **In grace period** state.

  To begin provisioning on Pending Cloud PCs, free up some Windows 365 licenses or end grace period on Cloud PCs in the grace period state. 

**User**: The user assigned to the Cloud PC.  

**Date modified**: The timestamp of the last change of state of the Cloud PC.

**Third-party connector**: If the third-party connector is installed and used on the Cloud PC, the connector provider is displayed along with the connector status. By default, this column is hidden and needs to be selected from the list of columns to be displayed.

**Azure network connection**: The Azure network connection, if any.

**Encryption status**

**Third party connector**

<!-- ########################## -->
## Next steps

[Remotely managed Cloud PCs](remotely-manage-cloud-pc.md).
