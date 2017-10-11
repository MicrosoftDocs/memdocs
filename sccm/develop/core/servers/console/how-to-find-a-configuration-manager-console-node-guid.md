---
title: "Find a Console Node GUID"
titleSuffix: "Configuration Manager"
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
ms.assetid: 80fd9154-6ec2-4586-bd9d-4cf88aa835a6searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Find a Configuration Manager Console Node GUID
Globally Unique Identifiers (GUIDs) are used, in Adminconsole.xml, to identify parts of the System Center Configuration Manager console. For example, the action you create in [How to Create a Configuration Manager Action](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-action.md) is placed on the **Site Configuration** node in the console tree view by using the GUID 9770fc1b-0885-40e7-8a83-5dfc5eaaa8c2.  

 Elements that contain the `namespaceGuid` attribute are part of the console. For example, the following element declares the software updates node:  

 `<RootNodeDescription NamespaceGuid="392b72f3-1c83-42e1-90ed-611798bc0dd0" Id="SmsSoftwareUpdatesNode" DisplayName="SUMName" Description="SUMDescription" HelpTopic="9af099dc-3713-463d-bd50-0e4cd07c48fb">`  

 Determining the correct GUID for your Configuration Manager console extension to use can be difficult because you must navigate through console root XML files to the correct element.  

 One approach is to open the any one of the console root XML files in Visual Studio and collapse all the XML nodes. After the XML is collapsed, expand `ConsoleNodesRootDescription` and then `RootNodeDescription`.  

 `RootNodeDescription` contains further `RootNodeDescription` elements for each of the major Configuration Manager features displayed in the Configuration Manager console tree view. By expanding these, you can navigate to the required part of the Configuration Manager console and get the GUID from the appropriate XML element.  

 Namespace GUIDs can be associated with several types of elements. For more information, see [Configuration Manager Console Node XML](../../../../develop/core/servers/console/console-node-xml.md).  

## See Also  
 [Configuration Manager Console Nodes](../../../../develop/core/servers/console/console-nodes.md)   
 [Configuration Manager Console Node XML](../../../../develop/core/servers/console/console-node-xml.md)
