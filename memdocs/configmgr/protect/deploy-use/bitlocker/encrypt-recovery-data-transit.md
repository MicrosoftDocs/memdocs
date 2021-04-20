---
title: Encrypt recovery data over the network
titleSuffix: Configuration Manager
description: Encrypt BitLocker recovery keys, recovery packages, and TPM password hashes over the network.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: eddfaaba-5e07-41dc-9b14-a7f5169799c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Encrypt recovery data over the network

*Applies to: Configuration Manager (current branch)*

<!--3601034-->

When you create a BitLocker management policy, Configuration Manager deploys the recovery service to a management point. On the **Client Management** page of the BitLocker management policy, when you **Configure BitLocker Management Services**, the client backs up key recovery information to the site database. This information includes BitLocker recovery keys, recovery packages, and TPM password hashes. When users are locked out of their protected device, you can use this information to help them recover access to the device.

Given the sensitive nature of this information, you need to protect it.

## HTTPS certificate requirements

Configuration Manager requires an HTTPS connection between the client and the recovery service to encrypt the data in transit across the network. Use one of the following options:

- Enable the site for [enhanced HTTP](../../../core/plan-design/hierarchy/enhanced-http.md). This option applies to version 2103 or later.<!-- 9503186 -->

- HTTPS-enable the IIS website on the management point that hosts the recovery service, not the entire management point role. This option applies to version 2002 or later.<!-- 5925660 -->

- Configure the management point for HTTPS. On the properties of the management point, the **Client connections** setting must be **HTTPS**. This option applies to all supported versions of Configuration Manager.

## Configure the management point for HTTPS

In Configuration Manager current branch version 1910, to integrate the BitLocker recovery service you had to HTTPS-enable a management point. The HTTPS connection is necessary to encrypt the recovery keys across the network from the Configuration Manager client to the management point. Configuring the management point and all clients for HTTPS can be challenging for many customers.

## HTTPS-enable the IIS website

Starting in version 2002, the HTTPS requirement is for the IIS website that hosts the recovery service, not the entire management point role. This change relaxes the certificate requirements, and still encrypts the recovery keys in transit.

The **Client connections** property of the management point can be **HTTP** or **HTTPS**. If the management point is configured for **HTTP**, to support the BitLocker recovery service:

1. Acquire a server authentication certificate. Bind the certificate to the IIS website on the management point that hosts the BitLocker recovery service.

2. Configure clients to trust the server authentication certificate. There are two methods to accomplish this trust:

    - Use a certificate from a public and globally trusted certificate provider. For example, but not limited to, DigiCert, Thawte, or VeriSign. Windows clients include trusted root certificate authorities (CAs) from these providers. By using a server authentication certificate that's issued by one of these providers, your clients should automatically trust it.

    - Use a certificate issued by a CA from your organization's public key infrastructure (PKI). Most PKI implementations add the trusted root CAs to Windows clients. For example, using Active Directory Certificate Services with group policy. If you issue the server authentication certificate from a CA that your clients don't automatically trust, add the CA trusted root certificate to clients.

> [!TIP]
> The only clients that need to communicate with the recovery service are those clients that you plan to target with a BitLocker management policy and includes a **Client Management** rule.

On the client, use the **BitLockerManagementHandler.log** to troubleshoot this connection. For connectivity to the recovery service, the log shows the URL that the client is using. Locate an entry that starts with `Checking for Recovery Service at`.

> [!NOTE]
> If your site has more than one management point, enable HTTPS on all management points at the site with which a BitLocker-managed client could potentially communicate. If the HTTPS management point is unavailable, the client could fail over to an HTTP management point, and then fail to escrow its recovery key.
>
> This recommendation applies to both options: enable the management point for HTTPS, or enable the IIS website that hosts the recovery service on the management point.

## Next steps

[Encrypt recovery data in the database](encrypt-recovery-data.md) is an optional prerequisite before deploying policy for the first time.

[Deploy BitLocker management client](deploy-management-agent.md)
