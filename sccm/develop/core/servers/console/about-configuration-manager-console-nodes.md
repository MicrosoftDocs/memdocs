---
title: "Configuration Manager Console Nodes"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 725d0da7-7e9b-4a53-a68f-41074e851646
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# About Configuration Manager Console Nodes
System Center Configuration Manager uses XML to define the nodes and their content, that you see in the Configuration Manager console. New nodes can be added anywhere in the existing node hierarchy.  

 The XML for a node describes the navigation pane, results pane, and action pane, and the resources that are needed by each pane to display the node.  

 When writing a new node, consider the following:  

-   **The position of the node in the hierarchy.** Each node is uniquely identified by a GUID. For an example, see [How to Create a Configuration Manager Administrator Console Node](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-console-node.md).  

-   **The node hierarchy.** The node structure is hierarchical, and you can nest nodes as deeply as you require. You can also use regular expressions to determine whether a node should be displayed. For an example, see [How to Create a Configuration Manager Administrator Console Node](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-console-node.md).  

-   **Actions.** You can define actions that the user selects in the Configuration Manager console. You can use an action to launch forms, run programs, call methods, show reports, and define action menus. For more information, see [Configuration Manager Actions](../../../../develop/core/servers/console/configuration-manager-actions.md).  

-   **Queries.** You can define queries that populate the navigation pane and results pane with SMS Provider objects. You can specify regular expressions to pick the properties that are displayed from the objects queried. For an example, see [Configuration Manager Administrator Console RootNodes Element](../../../../develop/core/servers/console/console-rootnodes-element.md).  

-   **Security.** You can secure a node based on security flags that you specify. For an example that sets security for an action, see [Configuration Manager Conditional Actions](../../../../develop/core/servers/console/conditional-actions.md).  

-   **Views.** You can launch views in the Configuration Manager console at desired nodes. For more information about views, see [Configuration Manager Administrator Console Views](../../../../develop/core/servers/console/console-views.md).  

> [!NOTE]
>  The Configuration Manager SDK includes a sample XML file and GUID folder for a node that displays the available collections. The GUID folder is the namespace identifier for the tools node  

 For information about node XML, see [Configuration Manager Console Node XML](../../../../develop/core/servers/console/console-node-xml.md).  

## See Also  
 [Configuration Manager Administrator Console Actions](../../../../develop/core/servers/console/console-actions.md)   
 [Configuration Manager Administrator Console Forms](../../../../develop/core/servers/console/console-forms.md)   
 [Configuration Manager Administrator Console Views](../../../../develop/core/servers/console/console-views.md)   
 [How to Create a Configuration Manager Administrator Console Node](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-console-node.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)   
 [Configuration Manager Console Node XML](../../../../develop/core/servers/console/console-node-xml.md)
