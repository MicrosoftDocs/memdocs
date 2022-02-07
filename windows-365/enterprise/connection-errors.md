---
# required metadata
title: Troubleshoot connection errors
titleSuffix:
description: Troubleshoot connection errors in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/08/2022
ms.topic: reference
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: traceyadams
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Troubleshoot Cloud PC connection errors

The following errors can occur when connecting to a Cloud PC.

## Errors when connecting to an Azure AD join Cloud PC

**Potential cause**: Possible causes for connection errors include:

- Windows sign-in works directly against Azure AD, potentially triggering Azure AD authentication controls.
- Sign-in attempts from the Windows desktop client to a Cloud PC use a different protocol, called PKU2U.

**Possible solution**: Follow the guidance to [troubleshoot connections to Azure AD joined VMs](/azure/virtual-desktop/troubleshoot-azure-ad-connections?context=/windows-365/context/pr-context).

## Specific connection errors

### We couldn't connect because there are currently no available resources

**Potential cause**: There may be a resource issue on your Cloud PC.

**Possible solution**: Sign in to [windows365.microsoft.com](https://windows365.microsoft.com) > select the cog icon next to the Cloud PC > **Restart**.

### We couldn't connect to the gateway because of an error. If this keeps happening, ask your admin or tech support for help.

**Potential cause**: This error can be caused by network configuration settings, like:

- Custom DNS Settings
- Network Virtual Appliance blocking
- Network Security group configuration
- Resource Locks
- Blocks on required endpoints

**Possible solution**: Review the settings and confirm that they aren’t interfering with connections.

### The remote PC ended your session. If this keeps happening, contact your network administrator for assistance. Error code: 0x3

**Potential cause**: This error can occur when the Cloud PC’s processor is over-utilized.

**Possible solution**: If the issue persists, sign in to [windows365.microsoft.com](https://windows365.microsoft.com) > select the cog icon next to the Cloud PC > **Restart**.

## Other connection error causes

Some other possible causes for Cloud PC connection failures include:

### Out-of-date third-party VPN client versions

**Possible solution**: Update VPN clients to the most up-to-date versions.

### Signing in to the Cloud PC with Azure Active Directory-only user accounts

**Possible solution**: Windows 365 is currently a Hybrid Azure Active Directory (Azure AD) Join device, requiring users to sign in with their on-premises Active Directory account.

### Using a client PC with Remote Credential Guard enabled

**Possible solution**: Remote Credential Guard requires connectivity to the on-premises Active Directory Domain Controller on the client PC used to access the Cloud PC. This connection is only possible using a VPN solution. Using a KDC proxy isn't currently available for Windows 365.

## Other troubleshooting steps

### Move the Cloud PC to a new organizational unit (OU) with no group policies

Connection problems may be caused by settings delivered by group policies. To test this possible cause, you can move the Cloud PC to a separate OU that’s blocked from receiving group policies.

### On-premises Group Policy Objects (GPO) may affect a Cloud PC's provisioning or behavior

Settings delivered by group policies may cause connection problems. To test this, you can move the Cloud PC to a separate OU that's blocked from receiving group policies.

## Next steps

[Review other troubleshooting steps](troubleshooting.md)
