---
title: "Create a Dialog Box"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 7f82876f-dfd0-42b5-a2cb-52d39572c8d6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Create a Configuration Manager Dialog Box
These procedures show you how to create a modeless dialog box assembly, in Configuration Manager, by using Visual Studio.  

 Creating the dialog box is very similar to creating a property sheet. You create a class derived from SmsPageControl and an XML file to describe the dialog.  

 For more information about the property manager, see [How to Use Objects Passed to a Configuration Manager Forms](../../../../develop/core/servers/console/how-to-use-objects-passed-to-a-configuration-manager-form.md).  

 After you have successfully built the dialog box assembly, you must do the following to integrate it into the Configuration Manager console:  

1. Define and deploy the form XML that links the selected action to the assembly you create in this topic. For more information, see [How to Create Form XML for a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-dialog-box.md).  

2. Define and deploy the action XML for displaying the context menu that the user selects. For more information, see [How to Create Action XML for a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-action-xml-for-a-configuration-manager-dialog-box.md).  

   When you have created the dialog assembly and XML, right-click a package in the Configuration Manager console tree **Packages** node, and then click **Show my Dialog Box**. A dialog box appears with a button on it. Clicking the button displays a message box containing the name of the package you selected.  

## Create the Control Class  
 The following procedure creates the control for the dialog box.  

#### To create the Visual Studio project  

1.  In Visual Studio 2010, on the **File** menu, point to **New**, and then click **Project** to open the **New Project** dialog box.  

2.  From the list of Visual C#, Windows projects, select the **Windows Control Library** project template, and type `ConfigMgrDialogControl` in the **Name** box.  

3.  Click **OK** to create the Visual Studio project.  

4.  In Solution Explorer, right-click **UserControl1.cs**, click **Rename**, and change the name to **ConfigMgrDialogControl.cs**.  

5.  In Solution Explorer, right-click **References**, and then click **Add Reference**.  

6.  In the **Add Reference** dialog box, click the **Browse** tab, navigate to **%ProgramFiles%\Microsoft Endpoint Manager\AdminConsole\bin** and then select **microsoft.configurationmanagement.exe**, **microsoft.configurationmanagement.managementprovider.dll**, **Microsoft.ConfigurationManagement.DialogFoundation.dll** and **AdminUI.DialogFoundation.dll**. Click **OK** to add the assemblies as project references.  

7.  In Solution Explorer, right-click **ConfigMgrDialogControl.cs** and then click **View Code**.  

8.  In the source code, change the namespace to `Microsoft.ConfigurationManagement.AdminConsole.ConfigMgrDialogBox`  

9. Change the class `ConfigMgrDialogControl` so that it derives from `SmsCustomDialog`.  

10. In Solution Explorer, right-click **ConfigMgrDialogControl.Designer.cs** and then click **View Code**.  

11. In the source code, change the namespace to `Microsoft.ConfigurationManagement.AdminConsole.ConfigMgrDialogBox`  

12. Change the class `ConfigMgrDialogControl` so that it derives from `SmsCustomDialog`.  

13. In **ConfigMgrDialogControl.cs**, add the following code to initialize the control:  

    ```  
    public override bool Initialize(System.Reflection.Assembly assembly, SmsFormData formData, SmsPageData pageData)  
    {  
        base.Initialize(assembly, formData, pageData);  
        return true;  
    }   
    ```  

14. In Solution Explorer, right-click **ConfigMgrDialogControl.cs** and select **View Designer**.  

15. In the Toolbox, click the **Common Controls** tab, and then double-click **Button**. A button named **button1** is added to your control on the **User Control Designer**.  

16. In the **User Control Designer**, double-click **button1** and type the following code in the **button1_Click** method source code displayed:  

    ```  
    MessageBox.Show( PageData.PropertyManager["Name"].StringValue);  
    ```  

## Deploy the Assembly  
 The following procedure builds and copies the assembly that you have created to the Configuration Manager console `assemblies` folder. For important information about deploying Configuration Manager console extensions, see [About Configuration Manager Console Extension Deployment](../../../../develop/core/servers/console/console-extension-deployment.md).  

#### To deploy the dialog box assembly  

1.  Build the project, and depending on where you created your project, your Visual Studio installation, the assembly is created as \Visual Studio 2010\Projects\ConfigMgDialogControl\ConfigMgrDialogControl\bin\Debug\ConfigMgrDialogControl.dll.  

2.  Copy the assembly to the folder %*ProgramFiles*%\Microsoft Endpoint Manager\AdminConsole\bin.  

## See Also  
 [How to Add a Property Page to an Existing Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-add-a-property-page-to-an-existing-configuration-manager-property-sheet.md)   
 [How to Create Action XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-action-xml-for-a-configuration-manager-property-sheet.md)   
 [How to Create Form XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-property-sheet.md)   
 [How to Use Objects Passed to a Configuration Manager Forms](../../../../develop/core/servers/console/how-to-use-objects-passed-to-a-configuration-manager-form.md)
