---
title: Collections security and privacy
titleSuffix: Configuration Manager
description: Recommendations for security and privacy with collections in Configuration Manager.
ms.date: 05/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Security and privacy for collections in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article contains security recommendations and privacy information for collections in Configuration Manager.

## Security recommendations

When you export or import a collection by using a managed object format (MOF) file that's saved to a network location, secure the location and the network channel. Restrict who can access the network folder. Use Server Message Block (SMB) signing or Internet Protocol security (IPsec) between the network location and the site server. These mechanisms help prevent an attacker from tampering with the exported collection data. Use IPsec to encrypt the data on the network to prevent information disclosure.

## Security issues

Collections have the following security issues:

- If you use collection variables, local administrators can read potentially sensitive information. Collection variables are only used when you deploy an OS. For more information, see [Collection and device variables](../../../../osd/understand/using-task-sequence-variables.md#bkmk_set-coll-var).

## Privacy information

There's no privacy information specifically for collections in Configuration Manager. Collections are containers for resources, such as users and devices. Collection membership often depends on the information that Configuration Manager collects during standard operation.

Configuration Manager can collect resource information from discovery or inventory. Using this information, you can configure a collection to contain the devices that meet your specified criteria. Collections might also be based on the current status information for client management operations.  For example, deploying software or checking for compliance. Along with query-based collections, you can also directly add resources to collections.

## Next steps

For more information about collections, see [Introduction to collections](introduction-to-collections.md).

For more information about other security features in Configuration Manager, see the [Security documentation hub](../../../../security/index.yml).
