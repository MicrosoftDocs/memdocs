---
title: "Create a Property Sheet"
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
ms.assetid: aa27cdc3-1635-42cd-8681-5dc61966451esearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create a Configuration Manager Property Sheet
To create a System Center Configuration Manager console property sheet, in Configuration Manager, you create a .NET Framework assembly that inherits from the following class:  

|Class|Description|  
|-----------|-----------------|  
|[SmsPageControl](https://msdn.microsoft.com/library/microsoft.configurationmanagement.adminconsole.smspagecontrol.aspx)|The control displayed on the property page.|  

 The following procedures show you how to create a Configuration Manager property sheet assembly by using Visual Studio. The property sheet displays a property page that contains a button. When it is clicked, the button displays the name of a package selected in the Configuration Manager console **Packages** node.  

 After you have successfully built the dialog box assembly, you must do the following to integrate it into the Configuration Manager console:  

1.  Define and deploy the form XML that links the selected action to the assembly you create in this topic. For more information, see [How to Create the Form XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-property-sheet.md).  

2.  Define and deploy the action XML for displaying the context menu that the user selects. For more information, see [How to Create Action XML for  a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-action-xml-for-a-configuration-manager-property-sheet.md).  

 When you have created the property sheet assembly and XML, right-click a package in the Configuration Manager console tree **Packages** node results pane, and select the menu item **Show my Property Sheet**. A property sheet is displayed. You can enhance the control by accessing the package that was selected in the Configuration Manager console. For more information, see [How to Use Objects Passed to a Configuration Manager Forms](../../../../develop/core/servers/console/how-to-use-objects-passed-to-a-configuration-manager-form.md).  

## Create the Control Class  
 The following procedure creates the control for the property sheet.  

#### To create the Visual Studio project  

1.  In Visual Studio 2010, on the **File** menu, point to **New**, and then click **Project** to open the **New Project** dialog box.  

2.  From the list of Visual C#, Windows projects, select the **Windows Forms Control Library** project template, and then type `ConfigMgrControl` in the **Name** box.  

3.  Click **OK** to create the Visual Studio project.  

4.  In Solution Explorer, right-click the project and select Properties. On the Application tab, change Target framework to .NET Framework 4.  

5.  In Solution Explorer, right-click **UserControl1.cs**, click **Rename**, and then change the name to **ConfigMgrControl.cs**.  

6.  In Solution Explorer, right-click **References** and then click **Add Reference**.  

7.  In the **Add Reference** dialog box, click the **Browse** tab, navigate to **%ProgramFiles%\Microsoft Configuration Manager\AdminConsole\bin** and then select  **microsoft.configurationmanagement.exe**, **Microsoft.ConfigurationManagement.DialogFramework.dll** and **microsoft.configurationmanagement.managementprovider.dll** . Click **OK** to add the assemblies as project references.  

8.  In Solution Explorer, right-click **ConfigMgrControl.cs**, and then click **View Code**.  

9. In the source code, change the namespace to `Microsoft.ConfigurationManagement.AdminConsole.ConfigMgrPropertySheet`  

10. Change the class `ConfigMgrControlPage` so that it derives from `SmsPageControl`.  

11. In Solution Explorer, right-click **ConfigMgrControl.Designer.cs**, and then click **View Code**.  

12. In the source code, change the namespace to `Microsoft.ConfigurationManagement.AdminConsole.ConfigMgrPropertySheet`  

13. In **ConfigMgrControl.cs**, Add the following new constructor to the `ConfigMgrControlPage` class:  

    ```  
    public ConfigMgrControlPage (SmsPageData pageData) : base(pageData)  
    {  
        InitializeComponent();  
    }  
    ```  

14. Add the following method to initialize the control:  

    ```  
    public override void InitializePageControl()  
    {  
       base.InitializePageControl();  
    }  
    ```  

## Deploy the Assembly  
 The following procedure builds and copies the assembly that you have created to the Configuration Manager console assemblies folder. For important information about deploying Configuration Manager console extensions, see [About Configuration Manager Administrator Console Extension Deployment](../../../../develop/core/servers/console/console-extension-deployment.md).  

#### To deploy the property sheet assembly  

1.  Build the project. The assembly should be created as \Visual Studio 2010\Projects\ConfigMgrControl\ConfigMgrControl\bin\Debug\ConfigMgrControl.dll.  

2.  Copy the assembly to the folder %*ProgramFiles*%\Microsoft Configuration Manager\AdminConsole\bin.  

## See Also  
 [How to Add a Property Page to an Existing Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-add-a-property-page-to-an-existing-configuration-manager-property-sheet.md)   
 [How to Create Action XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-action-xml-for-a-configuration-manager-property-sheet.md)   
 [How to Create Form XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-property-sheet.md)   
 [How to Use Objects Passed to a Configuration Manager Forms](../../../../develop/core/servers/console/how-to-use-objects-passed-to-a-configuration-manager-form.md)
