---
description: Learn how to define the resources that are used by the node with the ResourceAssembly element in Configuration Manager.
title: Console ResourceAssembly Element
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: article
ms.assetid: 43a057a5-3370-4c54-821a-5029e7c4bd8c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Configuration Manager Console ResourceAssembly Element
In Configuration Manager, the `ResourceAssembly` element defines the resources that are used by the node. The following XML defines the assembly, `AdminUI.CollectionProperty.dll`, and the type of the resource within the assembly.  

```  
<ResourceAssembly>  
    <Assembly>AdminUI.CollectionProperty.dll</Assembly>  
    <Type>Microsoft.ConfigurationManagement.AdminConsole.CollectionProperty.Properties.Resources.resources</Type>  
</ResourceAssembly>  

```  

## See Also  
 [About Configuration Manager Administrator Console Nodes](../../../../develop/core/servers/console/about-configuration-manager-console-nodes.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)   
 [Configuration Manager Console Node XML](../../../../develop/core/servers/console/console-node-xml.md)
