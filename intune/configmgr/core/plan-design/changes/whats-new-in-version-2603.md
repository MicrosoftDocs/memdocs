---
title: What's new in version 2603
description: Get details about changes and new capabilities introduced in version 2603 of Configuration Manager current branch.
ms.date: 04/27/2026
ms.subservice: core-infra
ms.topic: whats-new
ms.collection: tier3
---

# What's new in version 2603 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2603 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2409 or later.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2603](../../servers/manage/checklist-for-installing-update-2509.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2509.md#post-update-checklist).

To take full advantage of new Configuration Manager changes, after you update the site, also update clients to the latest version. New functionality appears in the Configuration Manager console when you update the site and console, but the complete scenario isn't functional until the client version is also the latest.

## General enhancements

As part of Microsoft's Secure Future Initiative (SFI) the 2603 version of Configuration Manager continues to focus on security, quality, and infrastructure modernization. For more information, see the [Microsoft Trust Center](https://www.microsoft.com/trust-center/security/secure-future-initiative).
For a list of significant customer-reported issues resolved in this release, see the [Summary of changes in Configuration Manager version 2603](../../../hotfix/2603/37426535.md) knowledge base article.

### Security improvements for Network Access Account

This update enhances security by improving access controls for the Network Access Account (NAA). Access to NAA information is now restricted to supported OSD media task sequence scenarios by enforcing additional permission requirements and removing legacy access paths to reduce exposure and align with least privilege principles. For more information, see [KB 37447175](../../../hotfix/2503/37447175.md).

### Weak ciphers disabled on Cloud Management Gateway

Weak DHE (Diffie-Hellman Ephemeral) cipher suites are now disabled on Cloud Management Gateway (CMG) instances. Only TLS 1.3 (AES_256_GCM, AES_128_GCM) and TLS 1.2 ECDHE ciphers remain enabled, improving the security posture of CMG connections.

Additionally, the `EnableCertPaddingCheck` registry keys are now set by default on CMG Virtual Machine Scale Set instances to mitigate CVE-2013-3900 (WinVerifyTrust Signature Validation Vulnerability).

### SQL Server Native Client dependency removed

All Configuration Manager components and site roles are updated to remove the dependency on the deprecated SQL Server Native Client (sqlncli.msi). Customers can now safely uninstall sqlncli from site systems. The product no longer includes sqlncli.msi in its redistributables.

### SQL Server Management Objects updated

The Microsoft SQL Server Management Objects and Microsoft System CLR Types for SQL Server are updated from the deprecated SQL Server 2014 versions to the SQL Server 2016 versions (SMO 17).

### PKI certificate support for site system-to-SQL Server communication

Added support and testing for PKI certificates used in site system-to-SQL Server communication. This includes proper handling of certificate trust, private key access, and BitLocker Management portal registry thumbprint configuration.

### ARM64 support improvements

- The `Import-CMDriver` PowerShell cmdlet now correctly includes ARM64 platform support when importing drivers from INF files. Previously, ARM64 was filtered out from the Supported Platforms list.
- Client push installation (CcmSetup) no longer fails with error code `0x80070643` on Windows 11 ARM64 devices when upgrading from ConfigMgr 2403 or 2503.

### Cloud Management Gateway improvements

- The `New-CMCloudManagementGateway` PowerShell cmdlet now allows combining the `-IsUsingExistingGroup $true` parameter with `-ServerAppClientId`, enabling automated CMG deployment into existing Azure resource groups without requiring interactive credentials.
- CMG deployment error handling is improved to capture and display detailed Azure error response information when Attribute-Based Access Control (ABAC) conditions block role assignments.
- The CMG outbound traffic alert and "Total Outbound data" metric now work correctly for CMGv2 (VMSS-based) deployments.

### Updated Feedback experience

The Configuration Manager console In-App Feedback feature is updated to support the new OCV Feedback SDK with authenticated submissions. Both authenticated and offline feedback submission modes are supported.

### Deprecated and removed features

- An internal service required for device compliance checks will be deprecated in October 2026. Following the deprecation, compliance checks in Software Center may fail in co-managed environments where the Compliance workload is managed by Intune. To prevent this issue, apply this update before October 2026.
- The deprecated Asset Intelligence synchronization point site role is removed from the site roles selection UI.
- The Software Update Health Troubleshooting Dashboard is hidden in this release due to performance issues in large environments.

## Next steps

<!-- As of MM DD, YYYY, version 2603 is globally available for all customers to install. -->

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2603](../../servers/manage/checklist-for-installing-update-2509.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2509.md#post-update-checklist).
