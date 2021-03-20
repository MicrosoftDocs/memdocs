---
title: Console extensions for Configuration Manager
titleSuffix: Configuration Manager
description: Learn about managing Configuration Manager console extensions
ms.date: 03/26/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dfda09bc-5eca-4fb6-9064-4e51705cfe58
author: mestew
ms.author: mstewart
manager: dougeby
---

# Manage Configuration Manager console extensions

*Applies to: Configuration Manager (current branch)*

Starting in Configuration Manager 2103, You can download console extensions from the [Community hub](community-hub.md) and have it applied to all consoles connected to a hierarchy. The **Console extensions** node allows you to start managing the approval and installation of console extensions used in your environment. Getting an extension from community hub doesn't make it immediately available. First, an administrator has to approve the extension for the site. Then console users can install the extension to their local console.

After you approve an extension, when you open the console, you'll see a [console notification](community-hub.md#bkmk_hub_os). From the notification, you can start the extension installer. After the installer completes, the console restarts automatically, and then you can use the extension.

[!INCLUDE [console extensions node](includes/console-extensions-node.md)]
