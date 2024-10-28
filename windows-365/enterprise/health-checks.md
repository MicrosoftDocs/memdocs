---
# required metadata
title: Azure network connection health checks in Windows 365
titleSuffix:
description: Learn about the health checks that are automatically run on Azure network connections.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/30/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Azure network connections health checks

A unique feature of Windows 365 is the Azure network connection (ANC) health checks. The health checks are periodically run to make sure that

- Cloud PC provisioning is successful.
- End-user Cloud PC experiences are optimal.

## Azure network connection status

In the **Azure network connection** tab, every ANC created displays a status. This status helps you determine if new Cloud PCs can be expected to provision successfully, and that existing end-users are having an optimal Cloud PC experience.

Statuses include:

- **Running checks**: The health checks are currently running. The ANC list view automatically refreshes every five minutes. Wait for the checks to complete before attempting to assign it to a provisioning policy.
- **Checks successful**: All health checks passed. The ANC is ready for use.
- **Checks successful with warnings**: All critical health checks passed. However at least one noncritical check may have issues. An example of a check that may trigger this state is the Microsoft Entra hybrid join sync check. Microsoft Entra hybrid join sync can take up to 90 minutes. Therefore, we check much of the Microsoft Entra hybrid join sync service but can’t confirm that the device sync succeeded until later. Provisioning policies can use ANCs with this status.
- **Checks failed**: One or more required checks failed. An ANC can’t be used if it's in a failed state. Resolve the underlying issue and Retry the health checks.
= **Inactive**: The ANC is inactive and health checks are paused. Reactivate the ANC to restart the health checks. After the health checks are passed, the ANC is ready for use.

## Status error details

Every failed ANC or success with warning error state includes the technical details behind the failure. Select the **View details** link for each failed check to view more information on the failure. After you fix the underlying issue, **Retry** the health check to rerun the tests. To retry the health check, you must:

- Have the [Intune Administrator](/azure/active-directory/roles/permissions-reference#intune-administrator) or [Windows 365 Administrator](/azure/active-directory/roles/permissions-reference) role.

## Supported checks

- **DNS can resolve Active Directory domain**: Resolve the provided Active Directory domain name.
- **Active directory domain join**: A domain join using the credentials, domain, and OU provided.
- **Endpoint connectivity**: Connectivity to the required [URL/endpoints](requirements-network.md).
- **Microsoft Entra device sync (warning)**: Device ID sync is enabled on the Microsoft Entra tenant, and the computer object is being synced within 90 minutes.
- **Azure subnet IP address usage**: Sufficient IP addresses are available in the provided Azure subnet.
- **Azure tenant readiness**: The defined Azure subscription is enabled and ready for use. No Azure policy restrictions are blocking Windows 365 resources from being created.
- **Azure virtual network readiness**: The defined vNet is in a Windows 365 supported region.
- **First party app permissions exist on Azure subscription**: Sufficient permissions exist on the Azure subscription.
- **First party app permissions exist on Azure resource group**: Sufficient permissions exist on the Azure resource group.
- **First party app permissions exist on Azure virtual network**: Sufficient permissions exist on the Azure vNet.
- **Environment and configuration is ready**: Underlying infrastructure is ready for provisioning to succeed.
- **Intune enrollment restrictions allow Windows enrollment**: Verify that Intune enrollment restrictions are configured to allow Windows enrollment.
- **Localization language package readiness**: Verify that the operating system and Microsoft 365 language packages are reachable. Also verify that the localization package download link is reachable.
- **UDP connection check**: Network configuration allows the use of UDP direct connection (STUN).
- **Single sign-on configuration**: Determine if the network is properly configured for [single sign-on](identity-authentication.md#single-sign-on-sso) to Microsoft Entra hybrid joined Cloud PCs by ensuring a Kerberos Server object exists.

<!-- ########################## -->
## Next steps

[Learn more about Azure network connections](azure-network-connections.md).
