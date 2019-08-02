---
title: "Console Extension Architecture"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 4248fae0-66fa-44a9-b5bb-0fa23426194a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---
# Configuration Manager Console Extension Architecture
The System Center Configuration Manager console architecture is built on the following four distinct layers.  

-   SMS Provider  

-   Managed SMS Provider SDK  

-   User interface framework  

-   Configuration Manager console XML  

## SMS Provider in Configuration Manager  
 The SMS Provider is essentially the same as the SMS 2007 Provider, with the addition of new classes that support new Configuration Manager features. You can access the SMS Provider through the usual WBEM interfaces, but for managed code you must use the managed SMS Provider SDK.  

## Managed SMS Provider SDK  
 The managed SMS Provider SDK provides a managed code library that abstracts the SMS Provider. It provides .NET Framework classes and interfaces that connect to the SMS Provider, make queries, and otherwise manipulate Configuration Manager objects and the site control file. You can use the managed SMS Provider SDK in stand-alone applications, or you can use the user interface framework to extend the existing Configuration Manager console.  

## User Interface Framework  
 The user interface framework lies on top of the managed SMS Provider SDK. The user interface framework provides functionality for dialog boxes and the Configuration Manager console, and it provides user interface validation within the Configuration Manager console. You can extend this user interface framework to add your own forms to the Configuration Manager console, or you can integrate your own forms within existing Configuration Manager console forms.  

## Configuration Manager Console XML  
 The Configuration Manager console XML defines how the Configuration Manager console looks and behaves. The XML defines nodes, queries, actions, forms, and everything else that is necessary to render the Configuration Manager console hierarchy, the results pane, and the action pane.  

 The XML files that are used by the Configuration Manager console are stored under %*ProgramFiles%*\Microsoft Configuration Manager\AdminConsole\XmlStorage\\. The following table shows the subfolders.  

|Folder|Description|  
|------------|-----------------|  
|ConsoleRoot|This folder contains various XML files that define built in user interface elements and classes.<br /><br /> ManagementClassDescriptions.xml: definitions for the SMS Provider classes.<br /><br /> ConnectedConsole.xml: definitions for sticky nodes and go-to navigation.<br /><br /> AssetManagementNode.xml, MonitoringNode.xml, SiteConfigurationNode.xml, SoftwareLibraryNode.xml: definitions for each workspace in the Configuration Manager console.|  
|Extensions|Location for XML that is related to the SMS Provider. There are four types of extension folders:<br /><br /> -   Actions. XML files for Configuration Manager console actions. For more information, see [About Configuration Manager console actions](/sccm/develop/core/servers/console/configuration-manager-actions).<br />-   Forms. XML files for form extensions to the Configuration Manager console. For more information, see [About console forms](/sccm/develop/core/servers/console/about-configuration-manager-console-forms).<br />-   Nodes. XML files for node extensions to the Configuration Manager console. For more information, see [About console nodes](/sccm/develop/core/servers/console/about-configuration-manager-console-nodes).<br />-   Management Classes. XML files for management class extensions to the Configuration Manager console. For more information, see [About console management classes](/sccm/develop/core/servers/console/about-configuration-manager-console-management-classes).|  
|Other|Various helper XML files.|  
|Validation|Validation rules for the Configuration Manager console forms.|  

## See Also  
 [About Configuration Manager Console Extension](../../../../develop/core/servers/console/about-configuration-manager-console-extension.md)   
 [About Configuration Manager console actions](/sccm/develop/core/servers/console/configuration-manager-actions)
 [About console forms](/sccm/develop/core/servers/console/about-configuration-manager-console-forms)
[About console management classes](/sccm/develop/core/servers/console/about-configuration-manager-console-management-classes)
 [About console nodes](/sccm/develop/core/servers/console/about-configuration-manager-console-nodes)
 [About console views](/sccm/develop/core/servers/console/about-configuration-manager-console-views)
