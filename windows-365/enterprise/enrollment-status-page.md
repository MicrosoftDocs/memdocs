---
# required metadata
title: Use the Enrollment Status Page with Cloud PCs
titleSuffix:
description: Learn how to use the Enrollment Status Page with Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/15/2022
ms.topic: how-to
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ericor
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Use the Enrollment Status Page with Cloud PCs

When a user signs in to a device for the first time, the Enrollment Status Page (ESP) displays the Intune provisioning status. Windows 365 supports the ESP, which provides a common experience for users who sign into their physical and Cloud PCs for the first time.  For full information about the ESP, see [Set up the Enrollment Status Page]( /mem/intune/enrollment/windows-enrollment-status).

## Windows 365 and the ESP process

When a Cloud PC is provisioned, the Windows 365 service:

1. Creates a Cloud PC.
2. Enrolls the Cloud PC in Intune.
3. Waits for the user to sign in to the new Cloud PC for the first time.
    - While waiting, the Cloud PC:
        - Continues to perform a sync action to request Intune policies.
        - Performs background actions that are device targeted.
4. After the user signs in for the first time, the Cloud PC performs user targeted installations and configurations.
    - If ESP is enabled, the **Account setup** phase of ESP is shown to the user. (The **Device setup** phase isn't supported for Cloud PCs. It only occurs during Autopilot in OOBE.)

## Targeting ESP profiles in Windows 365

Windows 365 uses a userless enrollment process. There's no pre-registering of resources as used in Autopilot. Because the ESP profile is set during enrollment, the grouping and targeting is time sensitive. For this reason, using Azure Active Directory (Azure AD) dynamic groups for targeting the ESP profile isn’t supported.

There are two ways to target ESP profiles with Cloud PCs:

- Default ESP profiles targeting the **All devices** built-in virtual group.
- Custom ESP profiles targeting the **All devices** built-in virtual group and using a filter based on the **enrollmentProfileName (Enrollment profile name)** property. For more information, see [Create a filter for all Cloud PCs from a specific provisioning policy](create-filter.md#create-a-filter-for-all-cloud-pcs-from-a-specific-provisioning-policy).

Both targeting strategies are supported for Hybrid Azure AD join and Azure AD join identity types. For more information, see [Device join types](./identity-authentication.md#device-join-types).

<!-- ########################## -->
## Next steps

[Learn more about the Enrollment Status Page](/mem/intune/enrollment/windows-enrollment-status).