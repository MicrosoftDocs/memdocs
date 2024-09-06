---
title: Known issues for Windows 365 Business Cloud PC
description: Learn about known issues for Windows 365 Business.
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 08/28/2024
audience: Admin
ms.topic: troubleshooting
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ivivano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Known issues: Windows 365 Business

The following items are known issues for Windows 365 Business.

## Microsoft 365 Business Standard not activating on Cloud PCs

If a user tries to use a Microsoft 365 Business Standard license on their Cloud PC, they might see the following error:

``Account Issue: The products we found in your account cannot be used to activate Office in shared computer scenarios.``

### Troubleshooting steps

The user should uninstall the version of Office installed on their Cloud PC and install a new copy from Office.com.

## Some websites might display the wrong language

Some websites that are accessed from a Cloud PC use its IP address to determine how content is displayed. Therefore, users might see content based on where the Cloud PC was created, instead of content based on where the user is located.  

### Troubleshooting steps

There are two workarounds for this issue:

#### Change language/locale in URLs

Users can manually change their language/locale in the URL for most websites.

For example, in the following URL, change the language/locale from `en-us` to `fr-fr` to get the French version:

Before: `https://learn.microsoft.com/en-us/microsoft-365/admin/setup/get-started-windows-365-business`

After: `https://learn.microsoft.com/fr-fr/microsoft-365/admin/setup/get-started-windows-365-business`

#### Set search engine location

Users can manually set their internet search engine's location. For example, on Bing.com users can visit the **Settings** menu (in the top-right corner of the site) to manually set the Language, Country/Region, and Location.

## Microsoft Narrator screen reader not turned on

When users sign into their Cloud PCs from windows365.microsoft.com, the Microsoft Narrator screen reader isn't turned on.

### Troubleshooting steps

To turn on Narrator when accessing your Cloud PC from the web interface:

1. Go to [Windows 365](https://windows365.microsoft.com/).

2. Sign into your Cloud PC.

3. On your keyboard, press Alt+F3+Ctrl+Enter.

## Sending outbound email messages using port 25 isn't supported

Sending outbound email messages directly on port 25 from a Windows 365 Business Cloud PC isn't supported. Communication over port TCP/25 is blocked at the Windows 365 Business network layer for security reasons.

### Troubleshooting steps

If your email service uses Simple Mail Transfer Protocol (SMTP) for your email client application, you can use their web interface, if available.

Or you can ask your email service provider for help with configuring their email client app to use secure SMTP over Transport Layer Security (TLS), which uses a different port.

## Virtual Private Network support<!--38270291-->

Because of the many Virtual Private Network (VPN) solutions available, Microsoft can't confirm which services work with Windows 365 Business. If you need more information, consult with your VPN provider. For organizations that have advanced networking needs, Windows 365 Enterprise is recommended. For more information, see [Network requirements](../enterprise/requirements-network.md).

[!INCLUDE [Missing start menu and taskbar when using iPad and the Remote Desktop app to access a Cloud PC](../includes/known-issues.md)]

## Next steps

[Troubleshoot Windows 365 Business Cloud PC setup issues](troubleshoot-windows-365-business.md)
