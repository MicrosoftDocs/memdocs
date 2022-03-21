---
title: "Create a Console Custom View"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 4bd77dc3-97d1-475b-a860-bff0157054be
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Create a Configuration Manager Console Custom View
In Configuration Manager, to create a custom console view, you must create two .NET Framework classes. If you do not wish to create your own custom view control, see [How to Create Node XML for a Configuration Manager Console View](../../../../develop/core/servers/console/how-to-create-node-xml-for-a-configuration-manager-console-grid-view.md) for more information.  

 The following procedure creates a view that displays a custom control. In this case, the view displays the string content of a label control.  

 The procedures in this topic create a "My View" console extension node that displays. beneath the **Site Configuration** console node in the Administration workspace. When you click the "My View" node, your custom view control will load into the Configuration Manager console.  

## Creating a Custom View  
 The following procedures create an extension node with a custom view control.  

### Create the View Controller Class  
 The following procedure creates the `OverviewControllerBase` derived class. The controller class's Content property is set contain your custom control. In the example below, the Content property is assigned a simple label control.  

##### To create a console view class  

-   Create the following new class. In this case, your custom control is a simple label control:  

    ```  

    public class MyViewController : OverviewControllerBase{   public MyViewController(): base()   {}   public override void EndInit()   {                 base.EndInit();     this.Content = new Label() { Content = "My Content" };   }}  
    ```  

### Create the View Description Class  
 The following procedure creates the `IConsoleView2` derived class.  

##### To create a console view class  

-   Create the following new class:  

    ```  

    public class MyViewDescription : IConsoleView2  
    {  
        override protected Type TypeOfViewController    {       get { return typeof(MyViewController); }     }  
        override protected Type TypeOfView     {      get { return typeof(Overview); }     }        public override bool TryConfigure(ref XmlElement persistedConfigurationData)    {        return false;    }  
    new public bool TryInitialize(ScopeNode scopeNode, AssemblyDescription resourceAssembly, ViewAssemblyDescription viewAssemblyDescription)    {      return true;    }  
    }  
    ```  

### Create the extension node XML  
 The following XML is required in order to load your extension into the console. Note that the `DisplayName` and `Description` properties refer to names in your assembly's resource file.  

```  
<RootNodeDescription NamespaceGuid="c192799c-82cd-43cc-bc11-12996bca800f" Id="MyViewNode" DisplayName="ViewNodeName" Description="ViewNodeDescription">  <ResourceAssembly>    <Assembly>NameofMyAssembly.dll</Assembly>    <Type>NameofMyAssembly.Resources.resources</Type>  </ResourceAssembly>  <ImagesDescription>    <ResourceAssembly>      <Assembly> NameofMyAssembly.dll</Assembly>      <Type> NameofMyAssembly.Resources.resources</Type>    </ResourceAssembly>    <ImageResourceName>NodeIcon</ImageResourceName>  </ImagesDescription>  <ViewAssemblyDescriptions>    <ViewAssemblyDescription>      <Assembly> NameofMyAssembly.dll</Assembly>      <Type>NameofMyAssembly.MyViewDescription</Type>    </ViewAssemblyDescription>  </ViewAssemblyDescriptions></RootNodeDescription>  
```  

## Deploy the Assembly  
 The following procedure builds the assembly you have created and copies it to the Configuration Manager console assemblies folder. For important information about deploying Configuration Manager console extensions, see [Configuration Manager Console Extension Deployment](../../../../develop/core/servers/console/console-extension-deployment.md).  

#### To deploy the view assembly  

1.  Build the project, and depending on where you created your project, the assembly should be created as \Visual Studio 2010\Projects\ConfigMgrControl\ConfigMgrObjectsControl\bin\Debug\NameofMyAssembly.dll.  

    > [!NOTE]
    >  In other parts of the Console Extension section, the examples use an assembly named `ConfigMgrObjectsControl.dll`. If you are building the examples in other sections, make sure to name the assembly `ConfigMgrObjectsControl.dll` at this step (or change the other assembly references to your specific assembly name).  

2.  Copy the assembly to the %*ProgramFiles*%\Microsoft Endpoint Manager\AdminConsole\bin folder.  

## See Also  
 [About Configuration Manager Administrator Console Views](../../../../develop/core/servers/console/about-configuration-manager-console-views.md)   
 [How to Create Node XML for a Configuration Manager Administrator Console View](../../../../develop/core/servers/console/how-to-create-node-xml-for-a-configuration-manager-console-grid-view.md)
