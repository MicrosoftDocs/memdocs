---
# required metadata
title: Troubleshoot Azure network connections
titleSuffix:
description: Troubleshoot Azure network connections in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 06/15/2023
ms.topic: troubleshooting
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

# Troubleshoot Azure network connections

The Azure network connection (ANC) periodically checks your environment to make sure that all requirements are met and are in a healthy state. If any check fails, you can see error messages in the Microsoft Intune admin center. This guide contains some further instructions for troubleshooting issues that may cause checks to fail.

## Active Directory domain join

When a Cloud PC is provisioned, it’s automatically joined to the provided domain. To test the domain join process, a domain computer object is created in the defined Organizational Unit (OU) with a name similar to "CPC-Hth" every time Windows 365 health checks are run. These computer objects are disabled when the health check is complete. Active Directory domain join failure can occur for many reasons. If the domain join fails, make sure that:

- The domain join user has sufficient permissions to join the domain provided.  
- The domain join user can write to the organizational unit (OU) provided.  
- The domain join user isn't restricted in how many computers they can join. For example, the default maximum joins per user is 10 and this maximum can affect Cloud PC provisioning.
- The subnet being used can reach a domain controller.
- You test Add-Computer using the domain join credentials on a VM (virtual machine) connected to the Cloud PC vNet/subnet.
- You troubleshoot domain join failures like any physical computer in your organization.
- If you have a domain name that can be resolved on the internet (like contoso.com), make sure that your DNS servers are configured as internal. Also, make sure that they can resolve Active Directory domain DNS records and not your public domain name.  

<a name='azure-active-directory-device-sync'></a>

## Microsoft Entra device Sync

Before mobile device management (MDM) enrollment can take place during provisioning, a Microsoft Entra ID object must be present for the Cloud PC. This check is intended to make sure that your organizations computer accounts are syncing to Microsoft Entra ID in a timely manner.  

Make sure that your Microsoft Entra computer objects appear in Microsoft Entra ID quickly. We suggest within 30 minutes, and no longer than 60 minutes. If the computer object doesn’t arrive in Microsoft Entra ID within 90 minutes, provisioning fails.  

If provisioning fails, make sure that:

- The sync period configuration on Microsoft Entra ID is set appropriately. Speak with your identity team to make sure that your directory is syncing fast enough.  
- Your Microsoft Entra ID is active and healthy.  
- Microsoft Entra Connect is running correctly and there are no issues with the sync server.  
- You manually perform an Add-Computer into the OU provided for Cloud PCs. Time how long it takes for that computer object to appear in Microsoft Entra ID.

## Azure subnet IP address range usage

As part of the ANC setup, you're required to provide a subnet to which the Cloud PC will connect. For each Cloud PC, provisioning creates a virtual NIC and consumes an IP address from this subnet.

Make sure that there's sufficient IP Address allocation available for the number of Cloud PCs you expect to provision. Also, plan enough address space for provisioning failures and potential disaster recovery.  

If this check fails, make sure that you:

- Check the subnet in Azure Virtual Network. It should have enough address space available.  
- Make sure there are enough address to handle three provisioning retries, each of which may hold onto the network addresses used for a few hours.  
- Remove any unused vNICs. It’s best to use a dedicated subnet for Cloud PCs to make sure that no other services are consuming allocation of IP addresses.  
- Expand the subnet to make more addresses available. This can't be completed if there are devices connected.

During provisioning attempts, it’s important to consider any CanNotDelete locks that may be applied at the resource group level or above. If these locks are present, the network interfaces created in the process aren't automatically deleted. In they aren't automatically deleted, you must manually remove the vNICs before you can retry.

During provisioning attempts, it’s important to consider any existing locks at the resource group level or above. If these locks are present, the network interfaces created in the process won't be automatically deleted. In the event this occurs, you must manually remove the vNICs before you can retry.

## Azure tenant readiness

When checks are performed, we check that the provided Azure subscription is valid and healthy. If it's not valid and healthy, we’re unable to connect Cloud PCs back to your vNet during provisioning. Problems such as billing issues may cause subscriptions to become disabled.  

Many organizations use Azure policies to make sure that resources are only provisioned into certain regions and services. You should make sure that any Azure policies consider the Cloud PC service and the supported regions.

Sign in to the Azure portal and make sure that the Azure subscription is enabled, valid, and healthy.

Also, visit the Azure portal and view Policies. Make sure that there are no policies blocking resource creation.  

## Azure virtual network readiness

When creating an ANC, we block the use of any vNet located in an unsupported region. For a list of supported regions, see [Requirements](requirements.md).  

If this check fails, make sure that the vNet provided is in a region in the supported region list.

## DNS can resolve Active Directory domain

For Windows 365 to successfully perform a domain join, the Cloud PCs attached to the vNet provided must be able to resolve internal DNS names.  

This test attempts to resolve the domain name provided. For example, contoso.com or contoso.local. If this test fails, make sure that:

- The DNS servers in the Azure vNet are correctly configured to an internal DNS server that can successfully resolve the domain name.  
- The subnet/vNet is routed correctly so that the Cloud PC can reach the DNS server provided.  
- The Cloud PCs/virtual machines in the declared subnet can NSLOOKUP on the DNS server, and it responds with internal names.

Along with standard the DNS lookup on the supplied domain name, we also check for the existence of _ldap._tcp.yourDomain.com records. This record indicates the DNS server provided is an Active Directory domain controller. The record is a reliable way to confirm that AD domain DNS is reachable. Make sure that these records are accessible through the vNet provided in your Azure network connection.

## Endpoint connectivity

During provisioning, Cloud PCs must connect to multiple Microsoft publicly available services. These services include Microsoft Intune, Microsoft Entra ID, and Azure Virtual Desktop.  

You must make sure that all of the [required public endpoints](requirements-network.md#allow-network-connectivity) can be reached from the subnet used by Cloud PCs.

If this test fails, make sure that:

- You use the Azure Virtual Network troubleshooting tools to ensure that the provided vNet/subnet can reach the service endpoints listed in the doc.
- The DNS server provided can resolve the external services correctly.
- There's no proxy between the Cloud PC subnet and the internet.
- There are no firewall rules (physical, virtual, or in Windows) that might block required traffic.
- You consider testing the endpoints from a VM on the same subnet declared for Cloud PCs.

## Environment and configuration are ready

This check is used for many infrastructure related issues that might be related to infrastructure that customers are responsible for. It can include errors such as internal service time outs or errors caused by customers deleting/changing Azure resources while checks are being run.  

We suggest you retry the checks if you encounter this error. If it persists, contact support for help.  

## First party app permissions

When creating an ANC, the wizard grants a certain level of permissions on the resource group and subscription. These permissions let the service smoothly provision Cloud PCs.  

Azure admins holding such permissions can view and modify these permissions.  

If any of these permissions are revoked, this check fails. Make sure that the following permissions are granted to the Windows 365 application service principal:

- [Reader](/azure/role-based-access-control/built-in-roles#reader) role on the Azure subscription.
- [Windows365 Network Interface Contributor](/azure/role-based-access-control/built-in-roles#network-contributor) role on the specified resource group.
- [Windows365 Network User](/azure/role-based-access-control/built-in-roles#network-contributor) role on the virtual network.

The role assignment on the subscription is granted to the Cloud PC service principal.  

Also, make sure that the permissions aren't granted as [classic subscription administrator roles](/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles) or "Roles (Classic)". This role isn't sufficient. It must be one of the Azure role-based access control built-in roles as listed previously.

<!-- ########################## -->
## Next steps

[Learn about the ANC health checks](health-checks.md).
