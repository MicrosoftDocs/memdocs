---
title: Known issues for Windows 365 Business Cloud PC setup issues
description: Learn about known issues for Windows 365 Business.
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 10/11/2021
audience: Admin
ms.topic: troubleshooting
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ivivano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection: M365-identity-device-management
---

# Known issues: Windows 365 Business

The following items are known issues for Windows 365 Business.

## Microsoft 365 Business Standard not activating on Cloud PCs

If a user tries to use a Microsoft 365 Business Standard license on their Cloud PC, they might see the following error:

``Account Issue: The products we found in your account cannot be used to activate Office in shared computer scenarios.``

### Troubleshooting steps

The user should uninstall the version of Office installed on their Cloud PC and install a new copy from Office.com.

## Some websites might display the wrong language

Some websites that are accessed from a Cloud PC use its IP address to determine how content is displayed. This means that users might see content based on where the Cloud PC was created, instead of content based on where the user is located.  

### Troubleshooting steps

There are two workarounds for this issue:

### Change language/locale in URLs

Users can manually change their language/locale in the URL for most websites.

For example, in the following URL, change the language/locale from "en-us" to "fr-fr" to get the French version:

docs.microsoft.com/**en-us**/microsoft-365/admin/setup/get-started-windows-365-business

docs.microsoft.com/**fr-fr**/microsoft-365/admin/setup/get-started-windows-365-business

### Set browser location

Users can manually set their internet search engine's location. For example, on Bing.com users can visit the **Settings** menu (in the top-right corner of the site) to manually set the Language, Country/Region, and Location.

## Next steps

[Troubleshoot Windows 365 Business Cloud PC setup issues](troubleshoot-windows-365-business.md)
