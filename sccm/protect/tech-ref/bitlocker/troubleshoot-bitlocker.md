---
title: Troubleshoot BitLocker
titleSuffix: Configuration Manager
description: Learn how to troubleshoot problems with BitLocker management in Configuration Manager
ms.date: 11/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Troubleshoot BitLocker

*Applies to: Configuration Manager (current branch)*

Use the information in this article to help you troubleshoot issues with BitLocker management in Configuration Manager.

## Server error in self-service

When trying to open the self-service portal (https://webserver.contoso.com/SelfService) for the first time, you see the following error message:

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

To fix this issue, make sure you installed the [prerequisite](/configmgr/protect/plan-design/plan-for-bitlocker#prerequisites) for **Microsoft ASP.NET MVC 4.0** on the web server.

## See also

For more information about using BitLocker event logs, see [BitLocker event logs](/configmgr/protect/tech-ref/bitlocker/about-event-logs).

For a list of known errors and possible causes for event log entries, see the following articles:

- [Client event logs](/configmgr/protect/tech-ref/bitlocker/client-event-logs)
- [Server event logs](/configmgr/protect/tech-ref/bitlocker/server-event-logs)

To understand why clients are reporting not compliant with the BitLocker management policy, see [Non-compliance codes](/configmgr/protect/tech-ref/bitlocker/non-compliance-codes).
