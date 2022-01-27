---
# required metadata
title: Troubleshoot connection errors
titleSuffix:
description: Troubleshoot provisioning errors in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/07/2022
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

## We couldn't connect because there are currently no available resources

**Potential cause**: The Cloud PC hasn’t completed provisioning.
**Possible solution**: Wait for provisioning to complete. Provisioning time can be variable and may exceed 45 minutes or more.

## We couldn't connect to the gateway because of an error. If this keeps happening, ask your admin or tech support for help.

**Potential cause**: This error can be caused by network configuration settings, like:

- Custom DNS Settings
- Network Virtual Appliance blocking
- Network Security group configuration 
- Resource Locks
- Blocks on required endpoints

**Possible solution**: Review the settings and confirm that they aren’t interfering with connections.

## The remote PC ended your session. If this keeps happening, contact your network administrator for assistance. Error code: 0x3

**Potential cause**: This error can occur when the Cloud PC’s processor is overutilized.
**Possible solution**: If the issue persists, try restarting the Cloud PC from the admin portal.

## Other connection error causes

Some other possible causes for Cloud PC connection failures include:

### Out-of-date third-party VPN client versions

**Possible solution**: Update VPN clients to the most up-to-date versions.

### Signing in to the Cloud PC with Azure Active Directory-only user accounts

**Possible solution**: ??

### Using a client PC with Remote Credential Guard enabled

**Possible solution**: Turn off Remote Credential Guard on the client PC used to access the Cloud PC.

## Other troubleshooting steps

### Move the Cloud PC to a new organizational unit (OU) with no group policies

Connection problems may be caused by settings delivered by group policies. To test this, you can move the Cloud PC to a separate OU that’s blocked from receiving group policies.

## Next steps

[Review other troubleshooting steps](troubleshooting.md)
