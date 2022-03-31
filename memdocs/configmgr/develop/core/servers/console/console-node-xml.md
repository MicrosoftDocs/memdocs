---
description: Learn how to use the Configuration Manager Console Node XML to cause a grid view to appear in the view panel displaying the RoleName and SiteCode properties.
title: "Console Node XML"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ae7c2e8f-06e9-487d-ba09-4b30cce7574c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Configuration Manager Console Node XML
The node XML for the Configuration Manager console is in workspace XML files located in the %*ProgramFiles*%\Microsoft Endpoint Manager\AdminConsole\XmlStorage\ConsoleRoot\ folder. Your extension node XML files, however, are placed in the folder AdminConsole\XmlStorage\Extensions\Nodes\\<GUID\>, where \<GUID> is the namespace GUID identifier for the parent node.  

 The following XML defines an extension node called "MyNode". The "MyNode" node is defined as a child of the **Site Configuration** node (d61498cb-7b3f-4748-ae3e-026674fb0cbd) in the Administration workspace of the Configuration Manager console. "MyNode" is associated with a **Microsoft.ConfigurationManagement.AdminConsole.ConsoleView.ViewDescription** type which is a grid view that ships with Configuration Manager. When the node is selected, it will cause a grid view to appear in the view panel. The grid view displays two properties (**RoleName** and **SiteCode**) of each `MyClass` custom management class instance that is returned by the WQL query.  

> [!NOTE]
>  The UIExtensionsDemo.dll referenced below is an example of referencing a custom assembly.  

```  

<RootNodeDescription NamespaceGuid="d61498cb-7b3f-4748-ae3e-026674fb0cbd" Id="MyNode" DisplayName="NodeName" Description="NodeDescription">   <ResourceAssembly>     <Assembly>UIExtensionsDemo.dll</Assembly>      <Type>UIExtensionsDemo.Resources.resources</Type>  </ResourceAssembly>  <ImagesDescription>     <ResourceAssembly>        <Assembly>UIExtensionsDemo.dll</Assembly>         <Type>UIExtensionsDemo.Resources.resources</Type>      </ResourceAssembly>   <ImageResourceName>NodeIcon</ImageResourceName>  </ImagesDescription>   <ViewAssemblyDescriptions>     <ViewAssemblyDescription>       <Assembly>AdminUI.ConsoleView.dll</Assembly>      <Type>Microsoft.ConfigurationManagement.AdminConsole.ConsoleView.ViewDescription</Type>      <CustomData>         <ConfigurationData xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">          <PropertyItemsData>                 <Properties>                      <string>RoleName</string>                      <string>SiteCode</string>                   </Properties>                     <ClassName>MyClass</ClassName>               </PropertyItemsData>           </ConfigurationData>        </CustomData>     </ViewAssemblyDescription>   </ViewAssemblyDescriptions>  <Actions>  </Actions>   <Queries>    <QueryDescription NamespaceGuid="81957874-9c03-4261-84eb-3cf6c31bf251" Type="WQL">             <Query>SELECT * FROM SMS_SCI_SysResUse</Query>                  <ReturnedClassType>MyClass</ReturnedClassType>        </QueryDescription>      </Queries>\</RootNodeDescription>  
```  

 The important elements are:  

|Element|Description|  
|-------------|-----------------|  
|[RootNodeDescription](/previous-versions/system-center/developer/cc147277(v=msdn.10))|Describes the root node for the node.|  
|[Configuration Manager Console RootNodes Element](../../../../develop/core/servers/console/console-rootnodes-element.md)|Root node for describing the node.|  
|[NodeDescription](/previous-versions/system-center/developer/cc147269(v=msdn.10))|Parent for nodes describing the tree view and result pane.|  
|[RootNodeDescription.resourceAssembly](/previous-versions/system-center/developer/cc144054(v=msdn.10))|The assembly from which to load resources for this node instance.|  
|[ActionDescription.imageDescription](/previous-versions/system-center/developer/cc143957(v=msdn.10))|The assembly containing the icon and other image resources used by the node.|  
|**ActionDescription.viewAssemblyDescription**|The view type of the node.|  

## Node hierarchy

Define cascading nodes in the following manner:  

```xml
<RootNodeDescription>
  <ChildNodes>
      <RootNodeDescription>
               <ChildNodes>
               ...
               </ChildNodes>
      </RootNodeDescription>
  </ChildNodes>
</RootNodeDescription>  
```  

## See also

 [How to Create a Configuration Manager Console Node](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-console-node.md)
 [About console nodes](about-configuration-manager-console-nodes.md)
