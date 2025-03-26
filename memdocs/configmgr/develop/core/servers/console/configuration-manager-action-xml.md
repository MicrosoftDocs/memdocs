---
description: Article describing the use of ActionDescription XML element in Configuration Manager to display the action, action type, and conditional tests made.
title: Configuration Manager Action XML
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: article
ms.assetid: 8a871fbf-ec8b-4c6f-8807-e5350ca2ffd7
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Configuration Manager Action XML
Every Configuration Manager action is defined by an `ActionDescription` XML element that defines the action type and other information that is used by the Configuration Manager console to display the action. An `ActionDescription` element has a variety of child elements that provide information specific to the action type and also conditional tests made before the action is displayed.  

 The following XML example describes an action that runs a command prompt, creates .txt file and opens that .txt file in notepad. The `ActionDescription` element `Class` attribute denotes an executable action and the `Executable` element provides both the  path of the executable and the parameters to pass to that executableThe `ShowOn` element tells the console to make this action available both on the context menu and the default home tab of the ribbon menu.  

```  
<ActionDescription Class="Executable" DisplayName="ExecutableActionName" Description="ExecutableActionDescription">  <ShowOn>    <string>DefaultHomeTab</string>    <string>ContextMenu</string>  </ShowOn>  <ResourceAssembly>    <Assembly>UIExtensionsDemo.dll</Assembly>    <Type>UIExtensionsDemo.Resources.resources</Type>  </ResourceAssembly>  <ImagesDescription>    <ResourceAssembly>      <Assembly>UIExtensionsDemo.dll</Assembly>      <Type>UIExtensionsDemo.Resources.resources</Type>    </ResourceAssembly>    <ImageResourceName>ActionIcon</ImageResourceName>  </ImagesDescription>  <Executable>    <FilePath>cmd</FilePath>    <Parameters>/C "echo ##SUB:__RELPATH## > %temp%\relpath.txt & notepad %temp%\relpath.txt"</Parameters>  </Executable></ActionDescription>  
```  

 The default actions used by the Configuration Manager console are defined in the XML files located in the *%ProgramFiles%*\Microsoft Endpoint Manager\AdminConsole\XmlStorage\ConsoleRoot\ folder. The XML files for custom actions can be placed in the *%ProgramFiles%*\Microsoft Endpoint Manager\AdminConsole\XmlStorage\Extensions\Actions folder under the appropriate Configuration Manager console node. The Configuration Manager console node is identified by a folder named with the GUID of the Configuration Manager console folder.  

 The following are typical attributes for an `ActionDescription` element:  

|Attribute|Description|  
|---------------|-----------------|  
|**ActionVerb**|Indicates whether the action is associated with a standard action.|  
|**Class**|The action type, for example, ShowDialog.|  
|**DisplayName**|The text displayed in the context menu.|  
|**MnemonicDisplayName**|The mnemonic display name.|  
|**Description**|The action description.|  
|**ImageDescription**|Information about the action's icon.|  
|**SelectionMode**|Determines when the action is displayed, as follows:<br /><br /> Single (default). Action is shown only when the selection set contains a single item.<br /><br /> Multiple. Action is shown when the selection set contains more than one item.<br /><br /> Both. Action is shown when one or more items are selected.|  

 For a complete list of attributes, see [ActionDescription](/previous-versions/system-center/developer/cc147252(v=msdn.10)).  

 There are a number of child elements for any given action type.  

## See Also  
[About Configuration Manager console actions](configuration-manager-actions.md)
 [Configuration Manager AssemblyType Action](../../../../develop/core/servers/console/assemblytype-action.md)   
 [Configuration Manager Conditional Actions](../../../../develop/core/servers/console/conditional-actions.md)   
 [Configuration Manager Executable Action](../../../../develop/core/servers/console/executable-action.md)   
 [Configuration Manager Group Action](../../../../develop/core/servers/console/group-action.md)   
 [Configuration Manager Report Action](../../../../develop/core/servers/console/report-action.md)   
 [Configuration Manager ShowDialog Action](../../../../develop/core/servers/console/showdialog-action.md)   
 [How to Create a Configuration Manager Action](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-action.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)
