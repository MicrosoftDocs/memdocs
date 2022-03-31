---
title: Known issues for Windows 365 Enterprise
description: Learn about known issues for Windows 365 Enterprise.
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 03/25/2022
audience: Admin
ms.topic: troubleshooting
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ivivano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection: M365-identity-device-management
---

# Known issues: Windows 365 Enterprise

The following items are known issues for Windows 365 Enterprise.

[!INCLUDE [Missing start menu and taskbar when using iPad and the Remote Desktop app to access a Cloud PC](../includes/known-issues.md)]

## Using resize with restore

A [resize](resize-cloud-pc.md) of a Cloud PC eliminates all existing [restore](restore-overview.md) points for that Cloud PC. New restore points will be captured at the intervals defined in the user setting.

## Windows doesn’t scan for software updates until the first time a user signs in<!--38212344-->

 While a Windows PC (physical or Cloud PC) sits idle before the first user signs in, Windows Update doesn’t scan for or install monthly quality patches. This means that the PC might miss important security updates. Without the latest security updates, the device is exposed to security vulnerabilities.

 **Troubleshooting steps**: Make sure that a user signs in to new Cloud PCs as soon as possible.

## Windows 365 provisioning fails<!--38483005-->

Windows 365 provisioning failures may occur because both:

- the Desired State Configuration (DSC) extension isn't signed and
- the PowerShell Execution policy is set to Allsigned in the Group Policy Object (GPO)

**Troubleshooting steps**: Follow these steps:

1. Did the on-premises network connection (OPNC) fail with the following error: `"An internal error occurred. The virtual machine deployment timed out."`?
2. If yes, review the related GPO. Is PowerShell Execution set to AllSigned?
3. If it is, either remove the GPO or reset the PowerShell Execution to RemoteSigned/ByPass.
4. Retry the OPNC health check. If this succeeds, retry provisioning.

## Default and custom Enrollment Status Page profiles for Windows 365 Cloud PCs

Only the default Enrollment Status Page (ESP) profile is supported for Windows 365 Cloud PCs. Custom ESP profiles aren’t supported for Cloud PCs.

For default ESP profiles, when using hybrid Azure Active Directory (Azure AD) Join, you must set the **Only show page to devices provisioned by out-of-box experience (OOBE)** setting to **No**.

## Cloud PC reports as not compliant for compliance policy

The following device compliance settings report as **Not applicable** when being evaluated for a Cloud PC:

- **Trusted Platform Module (TPM)**
- **Require encryption of data storage on device.**

The following device compliance settings report as **Not Compliant** when being evaluated for a Cloud PC:

- **Require BitLocker**
- **Require Secure Boot to be enabled on the device.**

**Troubleshooting steps**: Follow these steps:

1. [Create a filter for all Cloud PCs](create-filter.md#create-a-filter-for-all-cloud-pcs).
2. For any existing device compliance policies that both evaluate to a Cloud PC and contain either of the **Not Compliant** settings, use this new filter to exclude Cloud PCs from the policy assignment.
3. Create a new device compliance policy without either of the **Not Compliant** settings and use this new filter to include Cloud PCs for the policy assignment. 

## Next steps

[Troubleshoot Windows 365 Enterprise Cloud PC](troubleshooting.md)
