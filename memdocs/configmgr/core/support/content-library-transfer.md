---
title: Content Library Transfer tool
titleSuffix: Configuration Manager
description: Use the Content Library Transfer tool to transfer content from one disk drive to another on a Configuration Manager distribution point.
ms.date: 07/30/2018
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
ms.author: baladell 
author: BalaDelli
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Content Library Transfer tool

*Applies to: Configuration Manager (current branch)*

The Content Library Transfer tool is one of the [Configuration Manager tools](tools.md). It transfers content from one disk drive to another. The tool is designed to run on distribution point site systems. It supports distribution points colocated with a site or remote site systems.  

The tool is useful for the scenario when the disk drive hosting the content library becomes full. First add or identify another hard disk with sufficient space to host the content library. Then use **ContentLibraryTransfer.exe** to transfer content from the old filled hard disk to the new, empty drive.
 
Once the transfer is complete, content is accessible to client computers from the new location.



## Usage 

Run **ContentLibraryTransfer.exe** as a user with administrative permissions on the distribution point. 

#### Syntax 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### Example
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## Limitations

- Run the tool locally on the distribution point. You can't run it from a remote computer.  

- Only use it when clients aren't actively accessing the distribution point. If you run the tool while clients are accessing content, the content library on the destination drive may have incomplete data. The data transfer might fail altogether leading to an unusable content library.  

- Don't distribute content to the distribution point when you run the tool. If you run the tool while content is being written to the distribution point, the content library on the destination drive may have incomplete data. The data transfer might fail altogether leading to an unusable content library.



## See also

- [Fundamental concepts for content management](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [The content library](../plan-design/hierarchy/the-content-library.md)
