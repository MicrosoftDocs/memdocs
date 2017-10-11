---
title: "Console RootNodes Element"
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
ms.assetid: 28814bf8-e339-4b32-85bc-0676d530dcffsearchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager Console RootNodes Element
`RootNodes` elements are the topmost nodes for a feature. For example, software distribution.  

 The `RootNodes` element is responsible for rendering a node. It defines the queries and layout that are used to display the results pane and any dynamic nodes that are added to the Configuration Manager console tree node. The `NodeDescription` node defines these user interface elements.  

 A root node has one type of child node, \<ChildNodes>.  

## Child Nodes  
 `ChildNode` elements are static nodes that appear under the root node for a feature. For example, Packages is a child node of the software distribution node. Child nodes appear under the `ChildNodes` node and each child node is described by a `RootNodeDescription` node. Each child node may have further child nodes described in a child `RootNode` element.  

## Describing the Tree View Pane and Results Pane  
 As a child of `RootNodes`, `NodeDescription` provides a description of the tree view pane and results pane used in the Configuration Manager console. `NodeDescription` includes the following three child elements:  

-   `QueryDescription`  

-   `DetailsPaneDescription`  

## QueryDescription  
 The `QueryDescription` element can be used to query the SMS Provider for objects to be displayed in the node. The `QueryDescription` element includes the following attributes:  

|Attribute|Description|  
|---------------|-----------------|  
|`NamespaceGuid`|The node that the query applies to.|  
|`Type`|The type of the query. Typically this is a WQL query.|  
|`DisplayName Description`|Displays text strings for the name and description in the Configuration Manager console. Typically, though you will use the results of the query. The code examples in the next section display the name property of the collection.|  

 The following elements are some of the child elements of `QueryDescription`:  

|Element|Description|  
|-------------|-----------------|  
|`Query`|The WQL query that is used to populate the node.|  
|`ReturnedClassType`|The type of the Configuration Manager or custom object returned.|  

## DetailPaneDescription  
 The `DetailsPaneDescription` element is used to define the details panel associated with a particular node. The `DetailsPaneDescription` element includes the following attributes:  

|Attribute|Description|  
|---------------|-----------------|  
|`ObjectClass`|The object type that the details pane applies to.|  

 The following elements are some of the child elements of `DetailsPaneDescription`:  

|Element|Description|  
|-------------|-----------------|  
|`PanePageDescription`|Defines the details page that should load in the details pane. Includes the assembly where the page is located, the page title, and query that should be run in order to retrieve any data for display.|  

 Below is an XML example of a `DetailsPaneDescription` element definition. The details pane is targeted at a `SMS_Package` type and returns all `SMS_Package` objects that are included in the selected `SMS_Package` object.  The returned collection is then displayed in a grid view. The properties for display are defined in the `PropertyList` element.  

```  
<DetailsPaneDescription ObjectClass="SMS_Package">    <PanePageDescription ObjectClass="SMS_Package" PageGuid="ce027fe6-ffd8-4825-ad7b-029c39e97327" Description="ProgramsTabDescription">   <ResourceAssembly>      <Assembly>AdminUI.Program.dll</Assembly>       <Type>Microsoft.ConfigurationManagement.AdminConsole.Program.Properties.Resources.resources</Type>   </ResourceAssembly>   <PageTitle>ProgramsTabName</PageTitle>   <QuerySettingsDescription QueryClass="SMS_Program">    <Queries>       <QueryDescription NamespaceGuid="d13e9848-2c76-418c-ab96-9a2940aaf0de" Type="WQL" DisplayName="##SUB:ProgramName##" Description="##SUB:ProgramName##">         <Query>SELECT * FROM SMS_Program WHERE PackageId='##SUB:PackageId##'</Query>          <ReturnedClassType>SMS_Program</ReturnedClassType>        <Actions>      </Actions>      </QueryDescription>  </Queries>   <PropertyList>       <PropertyDescription Name="ProgramName" />       <PropertyDescription Name="CommandLine" />       <PropertyDescription Name="Run" />       <PropertyDescription Name="DiskSpaceReq" />      <PropertyDescription Name="Comment" />    </PropertyList>   </QuerySettingsDescription> </PanePageDescription></DetailsPaneDescription>  
```  

## See Also  
 [How to Create a Configuration Manager Administrator Console Node](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-console-node.md)   
 [About Configuration Manager Administrator Console Nodes](../../../../develop/core/servers/console/about-configuration-manager-console-nodes.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)
