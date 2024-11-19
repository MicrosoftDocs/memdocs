---
# required metadata
title: Windows 365 role-based access
titleSuffix:
description: Learn about role-based access control in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 05/8/2024 
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
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

Role-based access control (RBAC) helps you manage who has access to your organization's resources and what they can do with those resources. You can assign roles for your Cloud PCs by using the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

When a user with the Subscription Owner or User Access Administrator role creates, edits, or retries an ANC, Windows 365 transparently assigns the required built-in roles the following resources (if tehy're not already assigned):

- Azure Subscription
- Resource group
- Virtual network associated with the ANC

If you only have the Subscription Reader role, these assignments aren't automatic. Instead, you must manually configure the required built-in roles to the Windows First Party App in Azure.

For more information, see [Role-based access control (RBAC) with Microsoft Intune](/mem/intune/fundamentals/role-based-access-control).

## Windows 365 Administrator role

Windows 365 supports the Windows 365 Administrator role available for role assignment through the Microsoft Admin Center and Microsoft Entra ID. With this role, you can manage Windows 365 Cloud PCs for both Enterprise and Business editions. The Windows 365 Administrator role can grant more scoped permissions than other Microsoft Entra roles like Global Administrator. For more information, see [Microsoft Entra built-in roles](/azure/active-directory/roles/permissions-reference).

## Cloud PC built-in roles

The following built-in roles are available for Cloud PC:

### Cloud PC Administrator

Manages all aspects of Cloud PCs, like:

- OS image management
- Azure network connection configuration
- Provisioning

### Cloud PC Reader

Views Cloud PC data available in the Windows 365 node in Microsoft Intune, but can’t make changes.

### Windows 365 Network Interface Contributor

The Windows 365 Network Interface Contributor role is assigned to the resource group associated with the Azure network connection (ANC). This role allows the Windows 365 service to create and join the NIC and manage deployment in the resource group. This role is a collection of the minimum permissions required to operate Windows 365 when using an ANC.

| Action type | Permissions |
| --- | --- |
| actions | Microsoft.Resources/subscriptions/resourcegroups/read</br>Microsoft.Resources/deployments/read</br>Microsoft.Resources/deployments/write</br>Microsoft.Resources/deployments/delete</br>Microsoft.Resources/deployments/operations/read</br>Microsoft.Resources/deployments/operationstatuses/read</br>Microsoft.Network/locations/operations/read</br>Microsoft.Network/locations/operationResults/read</br>Microsoft.Network/locations/usages/read</br>Microsoft.Network/networkInterfaces/write</br>Microsoft.Network/networkInterfaces/read</br>Microsoft.Network/networkInterfaces/delete</br>Microsoft.Network/networkInterfaces/join/action</br>Microsoft.Network/networkInterfaces/effectiveNetworkSecurityGroups/action</br>Microsoft.Network/networkInterfaces/effectiveRouteTable/action</br> |
| notActions | None |
| dataActions | None |
| notDataActions | None |

### Windows 365 Network User

The Windows 365 Network User role is assigned to the virtual network associated with the ANC. This role allows the Windows 365 service to join the NIC to the virtual network. This role is a collection of the minimum permissions required to operate Windows 365 when using an ANC.

| Action type | Permissions |
| --- | --- |
| actions | Microsoft.Network/virtualNetworks/read<br>Microsoft.Network/virtualNetworks/subnets/read<br>Microsoft.Network/virtualNetworks/usages/read<br>Microsoft.Network/virtualNetworks/subnets/join/action |
| notActions | None |
| dataActions | None |
| notDataActions | None |

## Custom roles

You can create custom roles for Windows 365 in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). For more information, see [Create a custom role]( /mem/intune/fundamentals/create-custom-role).

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
| Cloud PCs/RetryPartnerAgentInstallation | Attempt to reinstall party partner agents in a Cloud PC which failed to install. |
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

## Migrating existing permissions

For ANCs created before November 26, 2023, the Network Contributor role is used to apply permissions on both the Resource Group and Virtual Network. To apply to the new RBAC roles, you can retry the ANC health check. The existing roles must be manually removed.

To manually remove the existing roles and add the new roles, refer to the following table for the existing roles used on each Azure resource. Before removing the existing roles make sure that the updated roles are assigned.

| Azure resource | Existing role (before November 26, 2023) | Updated role (after November 26, 2023) |
| --- | --- | --- |
| Resource group | Network Contributor | Windows 365 Network Interface Contributor |
| Virtual network | Network Contributor | Windows 365 Network User |
| Subscription | Reader | Reader |

For more details about removing a role assignment from an Azure resource, see [Remove Azure role assignments](/azure/role-based-access-control/role-assignments-remove).

## Scope tags

For RBAC, roles are only part of the equation. While roles work well to define a set of permissions, scope tags help define visibility of your organization’s resources. Scope tags are most helpful when organizing your tenant to have users scoped to certain hierarchies, geographical regions, business units, and so on.

Use Intune to create and manage scope tags. For more information on how scope tags are created and managed, see [Use role-based access control (RBAC) and scope tags for distributed IT](/mem/intune/fundamentals/scope-tags).  

In Windows 365, scope tags can be applied to the following resources:

- Provisioning policies
- Azure network connections (ANC)
- Cloud PCs
- Custom images
- Windows 365 RBAC role assignments

To make sure that both the Intune-owned **All devices** list and Windows 365-owned **All Cloud PCs** list show the same Cloud PCs based on scope, follow these steps after creating your scope tags and provisioning policy:

1. Create a Microsoft Entra ID dynamic device group with rule that enrollmentProfileName equals the exact name of the provisioning policy created.  
2. Assign the created scope tag  to the dynamic device group.
3. After the Cloud PC is provisioned and enrolled into Intune, both the All Devices list and All Cloud PCs list should display the same Cloud PCs.  

To let scoped administrators view which scope tags are assigned to them and the objects within their scope, they must be assigned one of the following roles:

- Intune read only
- Cloud PC reader/administrator
- A custom role with similar permissions.

### Graph API bulk actions and scope tags during the public preview

For the duration of the scope tags public preview, the following bulk actions don't honor scope tags when called directly from the Graph API:

- Restore
- Reprovision
- Place Cloud PC under review
- Remove Cloud PC under review
- Share Cloud PC restore point to storage
- Create Cloud PC manual restore point

<!-- ########################## -->
## Next steps
[Role-based access control (RBAC) with Microsoft Intune](/mem/intune/fundamentals/role-based-access-control).

[Understand Azure role definitions](/azure/role-based-access-control/role-definitions)

[What is Azure role-based access control (Azure RBAC)?](/azure/role-based-access-control/overview)
