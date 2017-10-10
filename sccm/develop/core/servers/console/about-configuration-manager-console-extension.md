---
title: "Configuration Manager Console Extension"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: ebfd3530-07f9-4d58-9e0a-f362c0e6dcd7searchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# About Configuration Manager Console Extension
The System Center Configuration Manager console has an XML-based architecture that can be easily extended. The Configuration Manager console supports the following extensions:  

## Actions  
 An action is a task or command accessed through either a context menu or the ribbon. A number of standard actions are available, and you can extend them to add new functionality, such as displaying a dialog box or launching an application.  

## Forms  
 You can extend the Configuration Manager console with dialog boxes or property sheets. You can also add new property pages to existing Configuration Manager console property sheets, such as the properties dialog for an object.  

## Nodes  
 You can add new nodes to the Configuration Manager console.  

## Views  
 You can create new views that are displayed in the result pane. You can also create new home pages. For example, you might want to add a new home page that is associated with a new navigation node that you have created.  

## Wizards  
 You can integrate your own custom wizards into the Configuration Manager console by using a wizard framework of your choice.  

## Management Classes  
 You can define your own custom classes that can be used by your Configuration Manager console extension. For more information, see [Configuration Manager Console Management Classes](../../../../develop/core/servers/console/console-management-classes.md).  

## Unsupported Features  
 The Configuration Manager console does not support the following features:  

### Wizard Creation  
 You cannot create wizards by using the existing Configuration Manager console framework. You also cannot modify or remove steps from the existing Configuration Manager wizards.  

### Modification of Core Configuration Manager Console Items  
 Do not change or remove items in the core Configuration Manager console XML, because this could break the Configuration Manager console. The core XML is stored in *%ProgramFiles%*\Microsoft Configuration Manager\AdminConsole\XmlStorage\ConsoleRoot.  

### SMS 2003 IMMF Interfaces  
 The Configuration Manager console is built by using managed code and does not support the SMS 2003 IMMF interfaces.  

### Registry-Based Extensions  
 Registry-based extensions, similar to those available in SMS 2003, are not supported in the Configuration Manager console.  

### Microsoft Management Console SDK Extensions  
 Extensions written with the Microsoft Management Console SDK are not supported by the Configuration Manager console.  

## See Also  
 [Configuration Manager Console Extension Architecture](../../../../develop/core/servers/console/console-extension-architecture.md)   
 [Configuration Manager Console Actions](../../../../develop/core/servers/console/console-actions.md)   
 [Configuration Manager Console Forms](../../../../develop/core/servers/console/console-forms.md)   
 [Configuration Manager Console Management Classes](../../../../develop/core/servers/console/console-management-classes.md)   
 [Configuration Manager Console Nodes](../../../../develop/core/servers/console/console-nodes.md)   
 [Configuration Manager Console Views](../../../../develop/core/servers/console/console-views.md)
