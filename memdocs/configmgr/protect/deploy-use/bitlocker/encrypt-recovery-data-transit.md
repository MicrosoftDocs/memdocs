---
title: Encrypt recovery data over the network
titleSuffix: Configuration Manager
description: Encrypt BitLocker recovery keys, recovery packages, and TPM password hashes over the network.
ms.date: 12/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Encrypt recovery data over the network

*Applies to: Configuration Manager (current branch)*

<!--3601034-->

When you create a BitLocker management policy, Configuration Manager deploys the recovery service to a management point. On the **Client Management** page of the BitLocker management policy, when you **Configure BitLocker Management Services**, the client backs up key recovery information to the site database. This information includes BitLocker recovery keys, recovery packages, and TPM password hashes. When users are locked out of their protected device, you can use this information to help them recover access to the device.

Given the sensitive nature of this information, you need to protect it.

[!INCLUDE [11108795 note about recovery service](includes/11108795-bitlocker-recovery-service.md)]

## HTTPS certificate requirements

> [!NOTE]
> These requirements only apply if the site is version 2010 or earlier, or if you deploy BitLocker management policies to devices with Configuration Manager client version 2010 or earlier.

Configuration Manager requires a secure connection between the client and the recovery service to encrypt the data in transit across the network. Use one of the following options:

- [HTTPS-enable the IIS website](#https-enable-the-iis-website) on the management point that hosts the recovery service, not the entire management point role.<!-- 5925660 -->

- [Configure the management point for HTTPS](#configure-the-management-point-for-https). On the properties of the management point, the **Client connections** setting must be **HTTPS**.

> [!NOTE]
> If your site has more than one management point, enable HTTPS on all management points at the site with which a BitLocker-managed client could potentially communicate. If the HTTPS management point is unavailable, the client could fail over to an HTTP management point, and then fail to escrow its recovery key.
>
> This recommendation applies to both options: enable the management point for HTTPS, or enable the IIS website that hosts the recovery service on the management point.

### Configure the management point for HTTPS

In earlier versions of Configuration Manager current branch, to integrate the BitLocker recovery service you had to HTTPS-enable a management point. The HTTPS connection is necessary to encrypt the recovery keys across the network from the Configuration Manager client to the management point. Configuring the management point and all clients for HTTPS can be challenging for many customers.

### HTTPS-enable the IIS website

The HTTPS requirement is now for the IIS website that hosts the recovery service, not the entire management point role. This configuration relaxes the certificate requirements, and still encrypts the recovery keys in transit.

The **Client connections** property of the management point can be **HTTP** or **HTTPS**. If the management point is configured for **HTTP**, to support the BitLocker recovery service:

1. Acquire a server authentication certificate. Bind the certificate to the IIS website on the management point that hosts the BitLocker recovery service.

2. Configure clients to trust the server authentication certificate. There are two methods to accomplish this trust:

    - Use a certificate from a public and globally trusted certificate provider.<!-- memdocs#1668 --> Windows clients include trusted root certificate authorities (CAs) from these providers. By using a server authentication certificate that's issued by one of these providers, your clients should automatically trust it.

    - Use a certificate issued by a CA from your organization's public key infrastructure (PKI). Most PKI implementations add the trusted root CAs to Windows clients. For example, using Active Directory Certificate Services with group policy. If you issue the server authentication certificate from a CA that your clients don't automatically trust, add the CA trusted root certificate to clients.

> [!TIP]
> The only clients that need to communicate with the recovery service are those clients that you plan to target with a BitLocker management policy and includes a **Client Management** rule.

## Troubleshoot the connection

On the client, use the **BitLockerManagementHandler.log** to troubleshoot this connection. For connectivity to the recovery service, the log shows the URL that the client is using. Locate an entry in the log based on the version of Configuration Manager:<!-- MEMDocs#1688 -->

- In version 2103 and later, the entry starts with `Recovery keys escrowed to MP`
- In version 2010 and earlier, the entry starts with `Checking for Recovery Service at`

## Next steps

[Encrypt recovery data in the database](encrypt-recovery-data.md) is an optional prerequisite before deploying policy for the first time.

[Deploy BitLocker management client](deploy-management-agent.md)
