---
description: Learn how the Configuration Manager console with an XML-based architecture can be easily extended.
title: "Configuration Manager Console Extension"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ebfd3530-07f9-4d58-9e0a-f362c0e6dcd7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# About Configuration Manager Console Extension
The Configuration Manager console has an XML-based architecture that can be easily extended. The Configuration Manager console supports the following extensions:  

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
 You can define your own custom classes that can be used by your Configuration Manager console extension. For more information, see [About console management classes](about-configuration-manager-console-management-classes.md).  

## Unsupported Features  
 The Configuration Manager console does not support the following features:  

### Wizard Creation  
 You cannot create wizards by using the existing Configuration Manager console framework. You also cannot modify or remove steps from the existing Configuration Manager wizards.  

### Modification of Core Configuration Manager Console Items  
 Do not change or remove items in the core Configuration Manager console XML, because this could break the Configuration Manager console. The core XML is stored in *%ProgramFiles%*\Microsoft Endpoint Manager\AdminConsole\XmlStorage\ConsoleRoot.  

### SMS 2003 IMMF Interfaces  
 The Configuration Manager console is built by using managed code and does not support the SMS 2003 IMMF interfaces.  

### Registry-Based Extensions  
 Registry-based extensions, similar to those available in SMS 2003, are not supported in the Configuration Manager console.  

### Microsoft Management Console SDK Extensions  
 Extensions written with the Microsoft Management Console SDK are not supported by the Configuration Manager console.  

## Accessibility

When developing console extensions, they should be based on designs with accessibility considerations.  For example, you can make use of color, layout, intelligent default values, sound, and exposing appropriate keyboard focus.  By using various accessibility techniques, you will make it easier for users with disabilities to use your software.  For more information, see [Resources for designing accessible applications](/visualstudio/ide/reference/resources-for-designing-accessible-applications).  


## See Also  
 [Configuration Manager Console Extension Architecture](../../../../develop/core/servers/console/console-extension-architecture.md)   
 [About Configuration Manager console actions](configuration-manager-actions.md)
 [About console forms](about-configuration-manager-console-forms.md)
 [About console management classes](about-configuration-manager-console-management-classes.md)
 [About console nodes](about-configuration-manager-console-nodes.md)
 [About console views](about-configuration-manager-console-views.md)
