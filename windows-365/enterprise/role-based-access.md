---
# required metadata
title: Windows 365 role-based access
titleSuffix:
description: Learn about role-based access control in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 01/05/2023 
ms.topic: how-to
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: cohanley
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Role-based access control

Role-based access control (RBAC) helps you manage who has access to your organization's resources and what they can do with those resources. You can assign roles for your Cloud PCs by using the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

For more information, see [Role-based access control (RBAC) with Microsoft Intune](/mem/intune/fundamentals/role-based-access-control).

## Windows 365 Administrator role

Windows 365 supports the Windows 365 Administrator role available for role assignment through the Microsoft Admin Center and Azure Active Directory (Azure AD). With this role, you can manage Windows 365 Cloud PCs for both Enterprise and Business editions. The Windows 365 Administrator role can grant more scoped permissions than other Azure AD roles like Global Administrator. For more information, see [Azure AD built-in roles](/azure/active-directory/roles/permissions-reference).

## Cloud PC built-in roles

Two built-in roles are available for Cloud PC:

**Cloud PC Administrator**: Manages all aspects of Cloud PCs, like:

- OS image management
- Azure network connection configuration
- Provisioning

**Cloud PC Reader**: Views Cloud PC data available in the Windows 365 node in Microsoft Endpoint Manager, but can’t make changes.

## Custom roles

You can create custom roles for Windows 365 in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). For more information, see [Create a custom role]( /mem/intune/fundamentals/create-custom-role).

The following permissions are available when creating custom roles.

| Permission | Description |
| --- | --- |
| Audit Data/Read | Read the audit logs of Cloud PC resources in your tenant. |
| Azure Network Connections/Create | Create an on-premises connection for provisioning Cloud PCs. Subscription owner or user access administrator Azure role is also required to create an on-premises connection. |
| Azure Network Connections/Delete | Delete a specific on-premises connection. Reminder: You can't delete a connection in use. Subscription owner or user access administrator Azure role is also required to delete an on-premises connection. |
| Azure Network Connections/Read | Read the properties of on-premises connections. |
| Azure Network Connections/Update | Update the properties of a specific on-premises connection. Subscription owner or user access administrator Azure role is also required to update an on-premises connection. |
| Azure Network Connections/RunHealthChecks | Run health checks on a specific on-premises connection. Subscription owner or user access administrator Azure role is also required to run health checks. |
| Azure Network Connections/UpdateAdDomainPassword | Update Active Directory domain password of a specific on-premises connection. |
| Cloud PCs/Read | Read the properties of Cloud PCs in your tenant. |
| Cloud PCs/Reprovision | Reprovision Cloud PCs in your tenant. |
| Cloud PCs/Resize | Resize Cloud PCs in your tenant. |
| Cloud PCs/EndGracePeriod | End grace period for Cloud PCs in your tenant. |
| Cloud PCs/Restore | Restore Cloud PCs in your tenant. |
| Cloud PCs/Reboot | Reboot Cloud PCs in your tenant. |
| Cloud PCs/Rename | Rename Cloud PCs in your tenant. |
| Cloud PCs/Troubleshoot | Troubleshoot Cloud PCs in your tenant. |
| Cloud PCs/ChangeUserAccountType | Change user account type between local administrator and standard user of a Cloud PC in your tenant. |
| Cloud PCs/PlaceUnderReview | Set Cloud PCs under review in your tenant. |
| Cloud PCs/RetryPartnerAgentInstallation | Attempt to re-install party partner agents in a Cloud PC which were failed to install. |
| Cloud PCs/ApplyCurrentProvisioningPolicy | Apply current provisioning policy config to Cloud PCs in your tenant. |
| Cloud PCs/CreateSnapshot | Manually create snapshot for Cloud PCs in your tenant. |
| Device Images/Create | Upload a custom OS image that you can later provision on Cloud PCs. |
| Device Images/Delete | Delete an OS image from Cloud PC. |
| Device Images/Read | Read the properties of Cloud PC device images. |
| External Partner Settings/Read | Read the properties of a Cloud PC external partner setting. |
| External Partner Settings/Create | Create a new Cloud PC external partner setting. |
| External Partner Settings/Update | Update the properties of a Cloud PC external partner setting. |
| Organization Settings/Read | Read the properties of Cloud PC organization settings. |
| Organization Settings/Update | Update the properties of Cloud PC organization settings. |
| Performance Reports/Read | Read the Windows 365 Cloud PC remote connections related reports. |
| Provisioning Policies/Assign | Assign a Cloud PC provisioning policy to user groups. |
| Provisioning Policies/Create | Create a new Cloud PC provisioning policy. |
| Provisioning Policies/Delete | Delete a Cloud PC provisioning policy. You can't delete a policy that's in use. |
| Provisioning Policies/Read | Read the properties of a Cloud PC provisioning policy. |
| Provisioning Policies/Update | Update the properties of a Cloud PC provisioning policy. |
| Reports/Export | Export Windows 365 related reports. |
| Role Assignments/Create | Create a new Cloud PC role assignment. |
| Role Assignments/Update | Update the properties of a specific Cloud PC role assignment. |
| Role Assignments/Delete | Delete a specific Cloud PC role assignment. |
| Roles/Read | View permissions, role definitions, and role assignments for Cloud PC role. View operation or action that can be performed on a Cloud PC resource (or entity). |
| Roles/Create | Create role for Cloud PC. Create operations can be performed on a Cloud PC resource (or entity). |
| Roles/Update | Update role for Cloud PC. Update operations can be performed on a Cloud PC resource (or entity). |
| Roles/Delete | Delete role for Cloud PC. Delete operations can be performed on a Cloud PC resource (or entity). |
| Service Plan/Read | Read the service plans of Cloud PC. |
| SharedUseLicenseUsageReports/Read | Read the Windows 365 Cloud PC Shared use license usage related reports. |
| SharedUseServicePlans/Read | Read the properties of Cloud PC Shared Use Service Plans. |
| Snapshot/Read | Read the Snapshot of Cloud PC. |
| Snapshot/Share | Share the Snapshot of Cloud PC. |
| Supported Region/Read | Read the supported regions of Cloud PC. |
| User Settings/Assign | Assign a Cloud PC user setting to user groups. |
| User Settings/Create | Create a new Cloud PC user setting. |
| User Settings/Delete | Delete a Cloud PC user setting. |
| User Settings/Read | Read the properties of a Cloud PC user setting. |
| User Settings/Update | Update the properties of a Cloud PC user setting. |

To create a provisioning policy, an admin needs the following permissions:

- Provisioning Policies/Read
- Provisioning Policies/Create
- Azure Network Connections/Read
- Supported Region/Read
- Device Images/Read

<!-- ########################## -->
## Next steps
[Role-based access control (RBAC) with Microsoft Intune](/mem/intune/fundamentals/role-based-access-control).
