---
title: Known issues for Windows 365 Enterprise
description: Learn about known issues for Windows 365 Enterprise.
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 07/12/2022
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

While a Windows PC (physical or Cloud PC) sits idle before the first user signs in, Windows Update doesn’t scan for or install monthly quality patches. Without such scans, the PC might miss important security updates. Without the latest security updates, the device is exposed to security vulnerabilities.

 **Troubleshooting steps**: Make sure that a user signs in to new Cloud PCs as soon as possible.

## Windows 10 to 11 in-place upgrade failure<!--40412134-->

Upgrading an existing Cloud PC from Windows 10 to Windows 11 using the Settings app may fail.

**Troubleshooting steps**:

1. Edit the related provisioning policy to change the gallery image to Windows 11.
2. Reprovision the Cloud PC.

## In-place Windows upgrade may change computer name

Upgrading an existing Cloud PC between release versions of Windows 10 to Windows 11 may cause the computer name to be changed to a name with a prefix of "pps" while leaving the Intune device name unchanged.

**Troubleshooting steps**: Find and manage the Cloud PC in Microsoft Endpoint Manager by using the unchanged Intune device name, either through the **Devices > All devices** list or the **Devices > Windows 365 > All Cloud PCs** list.


## Windows 365 provisioning fails<!--38483005-->

Windows 365 provisioning failures may occur because both:

- the Desired State Configuration (DSC) extension isn't signed and
- the PowerShell Execution policy is set to Allsigned in the Group Policy Object (GPO)

**Troubleshooting steps**:

1. Did the Azure network connection (ANC) fail with the following error: `"An internal error occurred. The virtual machine deployment timed out."`?
2. If yes, review the related GPO. Is PowerShell Execution set to AllSigned?
3. If it is, either remove the GPO or reset the PowerShell Execution to Unrestricted.
4. Retry the ANC health check. If the check succeeds, retry provisioning.

## Default and custom Enrollment Status Page profiles for Windows 365 Cloud PCs

Only the default Enrollment Status Page (ESP) profile is supported for Windows 365 Cloud PCs. Custom ESP profiles aren’t supported for Cloud PCs.

## Cloud PC reports as not compliant for compliance policy

The following device compliance settings report as **Not applicable** when being evaluated for a Cloud PC:

- **Trusted Platform Module (TPM)**
- **Require encryption of data storage on device.**

The following device compliance settings may report as **Not Compliant** when being evaluated for a Cloud PC:

- **Require BitLocker**
- **Require Secure Boot to be enabled on the device.** Cloud PC support for [Secure boot](/windows-hardware/design/device-experiences/oem-secure-boot) functionality is now available to all customers.

**Troubleshooting steps to enable secure boot on the Cloud PC**:

1. [Reprovision](reprovision-cloud-pc.md) the specific Cloud PC.

**Troubleshooting steps to remove not compliant settings**:

1. [Create a filter for all Cloud PCs](create-filter.md#create-a-filter-for-all-cloud-pcs).
2. For any existing device compliance policies that both evaluate to a Cloud PC and contain either of the **Not Compliant** settings, use this new filter to exclude Cloud PCs from the policy assignment.
3. Create a new device compliance policy without either of the **Not Compliant** settings and use this new filter to include Cloud PCs for the policy assignment.

## Next steps

[Troubleshoot Windows 365 Enterprise Cloud PC](troubleshooting.md)
