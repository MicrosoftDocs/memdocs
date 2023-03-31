---
title: Known issues for Windows 365 Enterprise and Frontline
description: Learn about known issues for Windows 365 Enterprise.
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 04/06/2023
audience: Admin
ms.topic: troubleshooting
ms.service: windows-365
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
ms.collection:
- M365-identity-device-management
- tier2
---

# Known issues: Windows 365 Enterprise and Frontline

The following items are known issues for Windows 365 Enterprise.

[!INCLUDE [Missing start menu and taskbar when using iPad and the Remote Desktop app to access a Cloud PC](../includes/known-issues.md)]

## Windows doesn’t scan for software updates until the first time a user signs in<!--38212344-->

While a Windows PC (physical or Cloud PC) sits idle before the first user signs in, Windows Update doesn’t scan for or install monthly quality patches. Without such scans, the PC might miss important security updates. Without the latest security updates, the device is exposed to security vulnerabilities.

 **Troubleshooting steps**: Make sure that a user signs in to new Cloud PCs as soon as possible.

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

## Single sign-on users see a dialog to allow remote desktop connection during the connection attempt <!--42499792-->
When using single sign-on, you'll currently be prompted to authenticate to Azure AD and allow the Remote Desktop connection when launching a connection to a new Cloud PC. Azure AD remembers up to 15 devices for 30 days before prompting again. If you see this dialog, select **Yes** to connect.

## Single sign-on user connections are being denied through Azure AD Conditional Access <!--42317382-->
**Possible cause**: To log in through single sign-on, the remote desktop client requests an access token to the **Microsoft Remote Desktop** app in Azure AD which may be the cause of the failed connection.

**Troubleshooting**: Follow the steps to [troubleshoot sign-in problems](/azure/active-directory/conditional-access/troubleshoot-conditional-access).

## Single sign-on users are immediately disconnected when the Cloud PC locks
When single sign-on isn't used, users have the option to see the Cloud PC lock screen and enter credentials to unlock their Windows session. However, when single sign-on is used, the Cloud PC fully disconnects the session so that the user can relaunch the connection through the remote desktop client and perform the Azure AD-based single sign-on authentication flow.

## Single sign-on users aren't asked to re-authenticate to Azure AD when connecting from an unmanaged device <!--35593334-->
When using single sign-on, all authentication behavior (including supported credential types and sign-in frequency) is driven through Azure AD.

**Troubleshooting**: To enforce periodic re-authentication through Azure AD, create a Conditional Access policy using the [sign-in frequency control](/azure/active-directory/conditional-access/howto-conditional-access-session-lifetime#policy-1-sign-in-frequency-control).

## Windows 365 Frontline known issues

The following items are known issues specifically for Windows 365 Frontline.

### Error tells user to wait until Cloud PC is available

If you've reached the maximum number of active user sessions in your tenant, any more users who try to start a user session will see an error message in the end user portal. The message tells them to wait until their Cloud PC becomes available.

**Troubleshooting steps**:  Use the [utilization report](report-cloud-pc-utilization.md) to estimate the right amount of license for your organization.

### Frontline licenses can't be purchased through Microsoft 365 Admin Center during Public Preview

**Troubleshooting steps**: Contact your Microsoft representative.

### Frontline licenses isn't immediately released after user signs off

To ensure users can continuously use their Cloud PCs after short breaks, the license isn't immediately released.

### In Microsoft 365 admin center, Frontline licenses show zero users assigned

In the Microsoft 365 admin center, Windows 365 Frontline licenses are shown as assigned to zero users. This issue happens because the licenses are applied on a tenant level.

**Troubleshooting steps**: Use the Windows 365 [utilization report](report-cloud-pc-utilization.md) to capture how many licenses are being used.

## Next steps

[Troubleshoot Windows 365 Enterprise Cloud PC](troubleshooting.md)
