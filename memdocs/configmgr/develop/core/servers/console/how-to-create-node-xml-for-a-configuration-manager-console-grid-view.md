---
description: Learn how to create the node XML for the Configuration Manager console default grid view by creating an XML file describing a RootNodeDescription element.
title: How to Create Node XML for a Grid View
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: d3ce62b0-287a-496f-ad82-3c3ce420aa04
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Create Node XML for a Configuration Manager Console Grid View
To create the node XML for the Configuration Manager console default grid view you create an XML file describing a [RootNodeDescription](/previous-versions/system-center/developer/cc147277(v=msdn.10)) element.  

 The XML in this procedure is used with the assembly you create in [How to Create a Configuration Manager Administrator Console View](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-console-custom-view.md).  When the user clicks on the "My Node" node, it displays a list of `SMS_SCI_SysResUse` classes in the Configuration Manager in the view pane.  

 The following elements and attributes are particularly important:  

-   `RootNodeDescription`. The attribute `NamespaceGuid` identifies the **Site Configuration** node.  

### To create the node XML for a view  

1.  If it is open, close the Configuration Manager console.  

2.  In Notepad, create an XML file that contains the following XML:  

    ```  
    <RootNodeDescription NamespaceGuid="c192799c-82cd-43cc-bc11-12996bca800f" Id="MyNode" DisplayName="NodeName" Description="NodeDescription">    <ResourceAssembly>        <Assembly>UIExtensionsDemo.dll</Assembly>        <Type>UIExtensionsDemo.Resources.resources</Type>    </ResourceAssembly>  <ImagesDescription>      <ResourceAssembly>         <Assembly>UIExtensionsDemo.dll</Assembly>          <Type>UIExtensionsDemo.Resources.resources</Type>      </ResourceAssembly>     <ImageResourceName>NodeIcon</ImageResourceName>   </ImagesDescription>   <ViewAssemblyDescriptions>      <ViewAssemblyDescription>         <Assembly>AdminUI.ConsoleView.dll</Assembly>         <Type>Microsoft.ConfigurationManagement.AdminConsole.ConsoleView.ViewDescription</Type>    <CustomData>           <ConfigurationData xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">             <PropertyItemsData>    <Properties>                    <string>RoleName</string>                  <string>SiteCode</string>                </Properties>                <ClassName>SMS_SCI_SysResUse</ClassName>                </PropertyItemsData>  </ConfigurationData>       </CustomData>     </ViewAssemblyDescription>   </ViewAssemblyDescriptions>   <Actions>  </Actions>   <Queries>      <QueryDescription NamespaceGuid="81957874-9c03-4261-84eb-3cf6c31bf251" Type="WQL">         <Query>SELECT * FROM SMS_SCI_SysResUse</Query>         <ReturnedClassType>MyClass</ReturnedClassType>      </QueryDescription>   </Queries></RootNodeDescription>  
    ```  

3.  Save the XML file in the folder %*ProgramFiles*%\AdminConsole\XmlStorage\Extensions\Nodes\c192799c-82cd-43cc-bc11-12996bca800f with the file name ConfigMgrObjectsView.xml. Be sure to save the file as type `All Files`. If the Extensions, Nodes, or GUID folders do not yet exist, create them.  

4.  Start the Configuration Manager console, select **Site Configuration** in the tree view, and select the **My Node** node. You should see a list of `SMS_SCI_SysResUse` classes in the view.  

## See Also  
 [About Configuration Manager Administrator Console Views](../../../../develop/core/servers/console/about-configuration-manager-console-views.md)   
 [How to Create a Configuration Manager Administrator Console View](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-console-custom-view.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)
