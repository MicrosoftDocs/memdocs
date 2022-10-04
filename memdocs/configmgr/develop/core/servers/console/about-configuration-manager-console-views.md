---
title: Configuration Manager Console Views
description: Configuration Manager console views are displayed in the results pane of the Configuration Manager console.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: cf102999-d4b1-46c9-a7cb-2af86423f140
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# About Configuration Manager Console Views
Configuration Manager console views are displayed in the results pane of the Configuration Manager console. You can create your own views and make them available anywhere in the tree view hierarchy.  

## Creating the View Assembly  
 To create a view, you must define a class within that implements the **IConsoleView2** interface.  

 After you create the class and build the assembly, place it in the %*ProgramFiles*%\Microsoft Endpoint Manager\AdminConsole\bin folder where it is loaded by the Configuration Manager console.  

 For more information, see [How to Create a Configuration Manager Administrator Console View](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-console-custom-view.md).  

## Creating the Node XML  
 The view is integrated into the Configuration Manager console when you create an XML file that describes the location, queries, actions, and resources that are needed for the node that displays the view. The node XML file is placed in the %*ProgramFiles*%\Microsoft Endpoint Manager\AdminConsole\ConsoleRoot\Extensions\Nodes folder, under a folder that is named with the GUID of the parent node for the node.  

 For more information, see [How to Create Node XML for a Configuration Manager Administrator Console View](../../../../develop/core/servers/console/how-to-create-node-xml-for-a-configuration-manager-console-grid-view.md).  

 For more information about node XML, see [About console nodes](about-configuration-manager-console-nodes.md).  

## Help  

### F1 Help  
 You can add F1 Help support to your views by specifying the `HelpID` attribute of the view `QueryDescription` element in the node XML. In the `HelpID` attribute you specify the path to the .chm file and the topic that you want to display in the following format:  

 `HelpID="<path to chm>::<path to topic><topic name>.htm"`  

 For example, the following `QueryDescription` element declaration loads the "How to Create a Package" topic from the Configuration Manager .chm. The .chm is assumed to be in c:\chm.  

> [!NOTE]
>  The assembly referenced below (ConfigMgrObjectsControl.dll) is created in the [How to Create a Configuration Manager Console Custom View](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-console-custom-view.md).  

```  
<ViewAssemblyDescriptions>    <ViewAssemblyDescription>         <Assembly> ConfigMgrObjectsControl.dll </Assembly>        <Type> Microsoft.ConfigurationManagement.AdminConsole.ConfigMgrObjectsView.ConfigMgrObjectsViewDescription </Type>   <CustomData>            <ConfigurationData xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">       <PropertyItemsData>               <Properties>                       <string>MyProperty1</string>           <string>MyProperty2</string>                   </Properties>                    <ClassName>_SDK</ClassName>               </PropertyItemsData>    </ConfigurationData>         </CustomData>      </ViewAssemblyDescription>   </ViewAssemblyDescriptions>   <Actions>  </Actions>   <Queries>      <QueryDescription NamespaceGuid="a4b9867e-8fc8-4fae-8a1a-0c798c22e010" Type="WQL" HelpTopic="C:\chm\SystemCenterConfigurationManager_SDK.chm::/html/2c295b3b-e23c-4084-ad4a-8bba328ef6fc.htm">          <Query>GetData</Query>          <ReturnedClassType>_SDK</ReturnedClassType>         <Actions>               <ActionDescription Class="ShowDialog" DisplayName="ShowDialogActionName" Description="ShowDialogActionDescription">                <ShowOn>                   <string>DefaultHomeTab</string>                   <string>ContextMenu</string>              </ShowOn>               <ResourceAssembly>                  <Assembly>UIExtensionsDemo.dll</Assembly>                      <Type>UIExtensionsDemo.Resources.resources</Type>              </ResourceAssembly>             <ImagesDescription>                <ResourceAssembly>                   <Assembly>UIExtensionsDemo.dll</Assembly>                  <Type>UIExtensionsDemo.Resources.resources</Type>    </ResourceAssembly>                  <ImageResourceName>ActionIcon</ImageResourceName>  </ImagesDescription>             <DialogId>MyDialog</DialogId>          </ActionDescription>      </Actions>    </QueryDescription>  </Queries>  
```  

 For more information about using the `QueryDescription` element, see [How to Create Node XML for a Configuration Manager Console View](../../../../develop/core/servers/console/how-to-create-node-xml-for-a-configuration-manager-console-grid-view.md).  

### Custom Help  
 You can also display your own .chm outside of the F1 Help system. For example, you can add a button to your form that opens your Help .chm. For more information about opening Help from Windows forms, see the [Help class](/dotnet/api/system.windows.forms.help) in the .NET Framework Class Library.  

## See Also  
[About console extensions](about-configuration-manager-console-extension.md)
 [How to Create a Configuration Manager Console](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-console-custom-view.md)   
 [How to Create Node XML for a Configuration Manager Console View](../../../../develop/core/servers/console/how-to-create-node-xml-for-a-configuration-manager-console-grid-view.md)
