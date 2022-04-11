---
# required metadata
title: On-premises network connection overview
titleSuffix:
description: Learn about on-premises network connections in Windows 365
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/16/2022
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# On-premises network connection overview

An on-premises network connection (OPNC) is an object in the Microsoft Endpoint Manager admin center that provides Cloud PC provisioning profiles with required information to connect to network-based resources. OPNCs are used:

- When a Cloud PC is initially provisioned.
- When Windows 365 periodically checks the connection to the on-premises infrastructure to ensure the best end-user experience.

## Network connection types

There are two kinds of OPNCs based on their join type. Both let you manage traffic and Cloud PC access to network based resources but they have different connectivity requirements.

- **Azure AD Join**: Doesn't require connectivity to a Windows Server Active Directory (AD) domain.
- **Hybrid Azure AD Join**: Requires connectivity to a Windows Server AD domain. You must provide the AD domain details when you [create the OPNC](create-on-premises-network-connection.md).


## Provisioning

When a Cloud PC is provisioned, the information in the OPNC is used by the provisioning policy to provision the Cloud PC (to? or within?) the Azure subnet. The information required in an OPNC includes:

- **Network details**: The Azure subscription, resource group, virtual network, and subnet that the Cloud PC will be associated with. When a provisioning policy runs, it creates a Cloud PC in the Microsoft hosted Azure subscription. To connect to a customers on-premises network, a virtual network interface card (vNic) is injected into a customer-provided Azure virtual network (vNet). To create this vNic, Windows 365 needs sufficient access to an Azure subscription.
- **Active Directory domain**: The Active Directory domain to join, an Organizational Unit (OU) destination for the computer object, and Active Directory user credentials with sufficient permissions to perform the domain join. When a provisioning policy runs, the Cloud PC is joined to this Active Directory domain. The credentials will be stored securely in the Windows 365 service.

During provisioning, the Cloud PC is connected to the Azure subnet and joined to a domain (either Windows Server Active Directory or Azure Active Directory (Azure AD)). This process results in a Cloud PC that is:

- On your network.
- Registered to Azure AD.
- Enrolled into Microsoft Endpoint Manager.
- Ready to accept user sign-in requests.

The OPNC settings are applied to the Cloud PC only at the time of provisioning.

## First health check

The information included in the OPNC is used to provision a Cloud PC. For provisioning to succeed, the resources referenced in the OPNC must be healthy and accessible. After an OPNC object is created, Windows 365 verifies that:

- The objects referenced by the OPNC are healthy.
- Connections can be made to these objects.

These health checks use the OPNC information provided to provision a Cloud PC. For a complete list of checks, see [On-premises network connection health checks](health-checks.md).

While this first OPNC health check is underway, you can’t assign it to a provisioning policy. After the health check is complete and successful, the OPNC can be assigned to one or more provisioning policies.

## Periodic health checks

After provisioning, the information in an OPNC is also used to monitor the connection health between your network-based resources and the Cloud PC hosted in the Microsoft hosted subscription. Windows 365 will report configuration issues that may cause provisioning failures or poor end-user experiences. This monitoring reduces your management overhead. For more information on these periodic checks, see [On-premises network connection health checks](health-checks.md).

## Health check frequency

OPNC checks are performed once every one to six hours.

The comprehensive, end-to end health check can take up to 30 minutes. The health checks are run on a temporary Azure virtual machine that is automatically created specifically for this purpose. This virtual machine is created automatically and deleted when the health checks are completed. The virtual machine is connected to your specified vNet and checks are performed to ensure provisioning should be successful.

After a check is complete, the results are posted on the on-premises network connection pane of the Microsoft Endpoint Manager admin center. For information about the check results, see [On-premises network connections health checks](health-checks.md).  

## Retry health check

To manually trigger a full health check, sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows 365 (under Provisioning)** > **On-premises network connection** > select an on-premises network connection > **Retry**.

## Permissions required for on-premises network connections

The OPNC wizard requires access to Azure and, optionally, on-premises domain resources. The following permissions are required for the OPNC:

- Azure
  - Subscription Owner or Subscription User Access Administrator.
- Active directory (Hybrid Azure AD Join OPNCs only)
  - An Active Directory user account with sufficient permissions to join the AD domain into this Organizational Unit.

To create, edit , or delete an OPNC, you'll also need to have one of the following permissions:

- Intune Administrator in Azure AD
- Cloud PC administrator
- Global Administrator

For a full list of requirements, see [Windows 365 requirements](requirements.md).

## Changing an on-premises network connection

Changing the settings in an OPNC won’t affect Cloud PCs previously provisioned with that OPNC. Only Cloud PCs provisioned after the changes to the OPNC will reflect such later changes.

If you want to change the OPNC related settings on a previously provisioned Cloud PC, you must reprovision the Cloud PC. Reprovisioning is a destructive action, so be sure it's an action you really want to take. For more information, see [reprovisioning](provisioning.md#reprovisioning).  

## Delete an on-premises network connection

You can’t delete an OPNC that's in use. Before the object can be deleted, you must do one of the following actions for every provisioning policy that uses this OPNC:

- Change the policy to use a different OPNC.
- Delete the policy. For more information, [Delete an on-premises network connection](delete-on-premises-network-connection.md).

After completing either of these operations, you can delete the OPNC.

## Maximum on-premises network connections

Each tenant has a limit of 10 on-premises network connections. If your organization needs more than 10 on-premises network connections, contact support.

## User sign in

When users attempt to sign in to their Cloud PC, user authentication occurs.

For Hybrid Azure AD Join OPNCs, the OPNC is used to route the authentication request to your domain controllers. If the OPNC or the network connection to your domain is unhealthy, user sign-in can't occur. Windows cached credentials can't be used over the remote desktop channel, so domain controller availability is critical. Ensure your network is stable or place a domain controller server on the same subnet as your Cloud PCs.

For Azure AD Join OPNCs, the OPNC is used to route the authentication request to Azure AD. Windows cached credentials can’t be used over the remote desktop channel, so connectivity to Azure AD is critical.

<!-- ########################## -->
## Next steps

[Learn about device images](device-images.md)

[Create an on-premises network connection](create-on-premises-network-connection.md)
