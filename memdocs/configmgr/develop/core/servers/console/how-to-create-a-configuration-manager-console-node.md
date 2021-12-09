---
title: "Create a Console Node"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: df3f9be7-c724-40f9-8d1e-368de8018bbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Create a Configuration Manager Console Node
In Configuration Manager, to create a Configuration Manager console node, you create an XML description of the node and add it to the %*ProgramFiles*%\Microsoft Endpoint Manager\AdminConsole\Extensions\Nodes\\<GUID\> folder. GUID is the GUID namespace for the parent node.  

 The following procedure shows how to add a new node to the Configuration Manager**Site Configuration** node. The new node displays the available collections.  

### To create a Configuration Manager console node  

1.  If the Configuration Manager console is open, close it.  

2.  In the Configuration Manager SDK, locate the XML file, CollectionsNode.XML.  

3.  If it does not already exist, create a folder named Nodes in %*ProgramFiles*%\AdminConsole\XmlStorage\Extensions\\.  

4.  In the Nodes folder, create a folder named `d61498cb-7b3f-4748-ae3e-026674fb0cbd`. This GUID identifies the **Site Configuration** node.  

5.  Copy the XML file to the GUID folder.  

6.  Start the Configuration Manager console, and in the console tree, navigate to the **Site Configuration** node. You should see a new **Collections** node.  

## See Also  
 [About Configuration Manager Administrator Console Nodes](../../../../develop/core/servers/console/about-configuration-manager-console-nodes.md)   
 [Configuration Manager Console Node XML](../../../../develop/core/servers/console/console-node-xml.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)
