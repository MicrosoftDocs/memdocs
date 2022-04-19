---
# required metadata
title: Troubleshoot Azure network connections
titleSuffix:
description: Troubleshoot Azure network connections in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/02/2021
ms.topic: troubleshooting
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

# Troubleshoot Azure network connections

The Azure network connection (ANC) periodically checks your environment to make sure that all requirements are met and are in a healthy state. If any check fails, you'll see error messages in the Microsoft Endpoint Manager admin center. This guide contains some further instructions for troubleshooting issues that may cause checks to fail.

## Active Directory domain join

When a Cloud PC is provisioned, it’s automatically joined to the provided domain. Active Directory domain join failure can occur for many reasons. If the domain join fails, make sure that:

- The domain join user has sufficient permissions to join the domain provided.  
- The domain join user can write to the organizational unit (OU) provided.  
- The domain join user is not restricted in how many computers they can join. For example, the default maximum joins per user is 10 and this can effect Cloud PC provisioning.
- The subnet being used can reach a domain controller.
- You test Add-Computer using the domain join credentials on a VM connected to the Cloud PC vNet/subnet.
- You troubleshoot domain join failures like any physical computer in your organization.
- If you have a domain name that can be resolved on the internet (like contoso.com), make sure that your DNS servers are configured as internal. Also, make sure that they can resolve Active Directory domain DNS records and not your public domain name.  

## Azure Active Directory device Sync

Before MDM enrollment can take place during provisioning, an Azure Active Directory (Azure AD) object must be present for the Cloud PC. This check is intended to make sure that your organizations computer accounts are syncing to Azure AD in a timely manner.  

Make sure that your Azure AD computer objects appear in Azure AD quickly. We suggest within 30 minutes, and no longer than 60 minutes. If the computer object doesn’t arrive in Azure AD within 90 minutes, provisioning will fail.  

If provisioning fails, make sure that:

- The sync period configuration on Azure AD is set appropriately. Speak with your identity team to make sure that your directory is syncing fast enough.  
- Your Azure AD is active and healthy.  
- Azure AD Connect is running correctly and there are no issues with the sync server.  
- You manually perform an Add-Computer into the OU provided for Cloud PCs. Time how long it takes for that computer object to appear in Azure AD.

## Azure subnet IP address range usage

As part of the ANC setup, you provide a subnet. This subnet is used for all Cloud PCs during the provisioning process. Each Cloud PC provisioning will create a virtual NIC and consume an IP address from the subnet.  

Make sure that there is sufficient IP Address allocation available for the volume of Cloud PCs you expect to provision. Also, plan enough address space for provisioning failures and potential disaster recovery.  

If this check fails, make sure that:

- You check the subnet in Azure Virtual Network. It should have enough address space available.  
- There are enough address to handle three provisioning retries, each of which may hold onto the network addresses used for a few hours.  
- You clean out any unused vNICs and IP addresses. It’s best to use a dedicated subnet for Cloud PCs only to make sure that no other services are eating allocation.  
- You expand the subnet to make more addresses are available.

## Azure tenant readiness

When checks are performed, we check that the provided Azure subscription is valid and healthy. If it's not valid and healthy, we’re unable to connect Cloud PCs back to your vNet during provisioning. Problems such as billing issues may cause subscriptions to become disabled.  

Many organizations use Azure policies to make sure that resources are only provisioned into certain regions and services. You should make sure that any Azure policies have considered the Cloud PC service and the supported regions.

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

Along with standard the DNS lookup on the supplied domain name, we also check for the existence of _ldap._tcp.yourDomain.com records. This record indicates the DNS server provided is an Active Directory domain controller. The record is a reliable way to confirm that AD domain DNS is reachable. Make sure tht these records are accessible through the vNet provided in your Azure network connection.

## Endpoint connectivity

During provisioning, Cloud PCs must connect to multiple Microsoft publicly available services. These services include Microsoft Intune, Azure Active Directory, and Azure Virtual Desktop.  

You must make sure that all of the [required public endpoints](requirements-network.md#allow-network-connectivity) can be reached from the subnet being used by Cloud PCs.

If this test fails, make sure that:

- You use the Azure Virtual Network troubleshooting tools to ensure that the provided vNet/subnet can reach the service endpoints listed in the doc.
- The DNS server provided can resolve the external services correctly.
- There is no proxy between the Cloud PC subnet and the internet.
- There are no firewall rules (physical, virtual, or in Windows) that might block required traffic.
- You consider testing the endpoints from a VM on the same subnet declared for Cloud PCs.

## Environment and configuration is ready

This check is used for many infrastructure related issues that might be related to infrastructure that customers are responsible for. It can include errors such as internal service time outs or those caused by customers deleting/changing Azure resources while checks are being run.  

Sometimes, these service errors are intermittent and a retry will complete successfully. Other times there’s no further troubleshooting that can be performed without the help of support.  

We suggest you retry the checks in case of this error. If it persists, contact support for help.  

## First party app permissions

When creating an ANC, the wizard grants a certain level of permissions on the resource group and subscription. This lets the service smoothly provision Cloud PCs.  

These permissions can be viewed and modified by Azure admins who hold such permissions.  

If any of these permissions are revoked, this check will fail. Make sure that the following permissions are granted to the Windows 365 application service principal:

- [Reader](/azure/role-based-access-control/built-in-roles#reader) role on the Azure subscription.
- [Owner](/azure/role-based-access-control/built-in-roles#owner) role on the specified resource group.
- [Network Contributor](/azure/role-based-access-control/built-in-roles#network-contributor) role on the virtual network.

The role assignment on the subscription will be granted to the Cloud PC service principal.  

Also, make sure that the permissions haven't been granted as [classic subscription administrator roles](/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles) or "Roles (Classic)". This role is not sufficient. It must be one of Azure role-based access control built-in roles as listed above.

<!-- ########################## -->
## Next steps

[Learn about the ANC health checks](health-checks.md).
