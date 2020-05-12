---
title: Use of diagnostics data
titleSuffix: Configuration Manager
description: Learn about how Microsoft uses the diagnostics and usage data that Configuration Manager collects.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How Microsoft uses Configuration Manager diagnostics and usage data

*Applies to: Configuration Manager (current branch)*

Diagnostic and usage data that Configuration Manager collects provides Microsoft nearly immediate feedback about how the product is working and is used to adjust future updates. Microsoft can also see configuration data that helps them engineer and test the configurations that you use in production. For example:

- The Windows server versions used on site servers

- Installed language packs

- The delta of the SQL schema against the product default

This data helps the engineering team plan future tests to make sure you have the best experience with the most common configurations. This data is crucial to quickly adjust and adapt with a frequent release cycle.

Equally important is how the diagnostics and usage data isn't used. Microsoft doesn't use this data for:

- Licensing audits, such as comparing customer usage against license agreements

- Auditing of products that are out of support

- Advertising based on available data such as feature usage or geolocation (time zone)

Microsoft uses available data to improve the product. For example:

- The initial support offered by the current branch of Configuration Manager limited the support timeline for Windows Server 2008 R2. Microsoft examined the usage data from customers who had upgraded to the Configuration Manager current branch. They then identified the need to revise and extend this timeline to support customers who still use this OS.

- Microsoft improved the prerequisite checks for installing an update. They removed obsolete rules, accounted for additional cases, and automatically remediated some issues.  

> [!div class="nextstepaction"]
> [How Configuration Manager collects data](how-diagnostics-and-usage-data-is-collected.md)
