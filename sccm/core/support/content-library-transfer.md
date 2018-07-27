---
title: Content Library Transfer tool
titleSuffix: Configuration Manager
description: Use the Content Library Transfer tool to transfer content from one disk drive to another on a Configuration Manager distribution point.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Content Library Transfer tool

*Applies to: System Center Configuration Manager (Current Branch)*

The Content Library Transfer tool is one of the [Configuration Manager tools](/sccm/core/support/tools). It transfers content from one disk drive to another. The tool is designed to run on distribution point site systems. It supports distribution points colocated with a site or remote site systems.  

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

- [Fundamental concepts for content management](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [The content library](/sccm/core/plan-design/hierarchy/the-content-library)
