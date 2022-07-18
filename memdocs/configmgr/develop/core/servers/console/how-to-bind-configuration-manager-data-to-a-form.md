---
title: "Bind Configuration Manager Data to a Form"
ms.date: "09/20/2016"
description: "In Configuration Manager, to bind console data to a property sheet, you use the DataBindings property of the property sheet's control class."
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: c8ae07f8-0d77-4cf2-850f-c13fc140eab6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Bind Configuration Manager Data to a Form
In Configuration Manager, to bind Configuration Manager console data to a property sheet, you use the `DataBindings` property of the property sheet's control class.  

 The `DataBindings` property is used to bind to the objects in the form's `Property Manager`. After an object changes, mark the object as changed with *SetDirtyFlag*. This ensures that the object is serialized properly when the dialog box is dismissed.  

### To bind Configuration Manager data to a form  

1.  If the Configuration Manager console is open, close it.  

2.  In Visual Studio 2010, open the project you created in [How to Create a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-property-sheet.md).  

3.  In Solution Explorer, right-click **ConfigMgrControl.cs**, and then click **View Designer**.  

4.  In the Toolbox, click the **Common Controls** tab, and then double-click **TextBox**. A field named **textBox1** is added to your control on the **User Control Designer**.  

5.  In Solution Explorer, right-click **ConfigMgrControl.cs**, and then click **View Source**.  

6.  Add the following code to the `InitializePageControl` method:  

    ```  
    textBox1.DataBindings.Add("Text", PropertyManager["Name"], "StringValue");  
    ```  

7.  In Solution Explorer, right-click **ConfigMgrPropertySheet.cs**, and then click **View Designer**.  

8.  Double-click the text box you added. A new event handler, `TextChanged`, is created.  

9. In **textBox1_TextChanged**, add the following code to set the dirty flag when text is changed: `Dirty = true;`  

10. Build the project and copy the assembly to %*ProgramFiles*%\Microsoft Endpoint Manager\AdminConsole\bin.  

11. Open the Configuration Manager console, and navigate to the **Packages** node under **Software Distribution**.  

12. Right-click a package, and then click **Show My Property Sheet**.  

     In the property sheet that is displayed, the text box displays the name of the selected package.  

13. Type a new name for the package, and then click **OK**.  

     In the Configuration Manager console results pane, the package name is changed to the name you entered.  

## See Also  
 [How to Use Objects Passed to a Configuration Manager Forms](../../../../develop/core/servers/console/how-to-use-objects-passed-to-a-configuration-manager-form.md)   
 [About Configuration Manager Forms](../../../../develop/core/servers/console/about-configuration-manager-console-forms.md)
