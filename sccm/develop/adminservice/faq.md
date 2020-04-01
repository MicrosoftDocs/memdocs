---
title: Admin service FAQ
titleSuffix: Configuration Manager
description: Frequently asked questions (FAQ) about the Configuration Manager administration service
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 4902b9ea-eaff-4f59-a9cf-c600d008eade
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Administration service frequently asked questions (FAQ)

*Applies to: Configuration Manager (current branch, technical preview branch, long-term servicing branch)*

## Technical

### Should I rewrite my existing automation to use the administration service?

It depends. There are some benefits to using the administration service over other APIs like WMI or PowerShell. For example, some PowerShell cmdlets loop on a single interaction, so there's multiple calls to set up, query, and tear down. With the administration service, the same query may be faster as it makes a single call for the group.

Existing WMI and PowerShell cmdlets are still supported and will continue to work. Configuration Manager may only expose some new features through the administration service, and not have comparable WMI or PowerShell APIs.

### What if an existing WMI class or method doesn't work over the administration service?

If you find an existing WMI class or method that doesn't GET or PUT as expected, send a frown to inform the engineering team. For more information, see [Find help for Configuration Manager](/configmgr/core/understand/find-help#send-a-frown).

### Are Swagger definitions available?

No, the administration service currently doesn't publish an [OpenAPI (Swagger) document](https://apidocs.microsoft.com/).

## Remote access

### Can I use the administration service with internet-based client management?

No, internet-based client management (IBCM) doesn't support exposing the SMS Provider role to the internet. For internet access to the administration service, you need a cloud management gateway. For more information, see [Enable internet access](/configmgr/develop/adminservice/set-up#bkmk_cmg).

### Isn't it too risky to open this API to the internet?

It depends upon your organization's risk level, and what controls you use or put in place to help mitigate the risks:

- The administration service still uses Configuration Manager built-in role-based authorization.

- Control access to the web service with the certificate trust. If a device doesn't trust the certificate chain, a user on that device can't query the administration service.

- Add additional security layers. For example, [Azure App Proxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).

### Can I use it with conditional access?

Yes, and that configuration is easiest if you use [Azure App Proxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).

## Miscellaneous

### How do I learn about what's new with the administration service in each Configuration Manager release?

For more information, see [Release notes](/configmgr/develop/adminservice/release-notes).
