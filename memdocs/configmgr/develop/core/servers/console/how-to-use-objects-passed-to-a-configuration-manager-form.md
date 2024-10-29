---
title: Use Objects Passed to a Form
titleSuffix: Configuration Manager
description: Learn how to use the SmsPageControl.PropertyManager object to access objects selected in the Configuration Manager console.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 673544cd-2f4c-4425-94a4-0269bfb7c329
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Use Objects Passed to a Configuration Manager Form
In Configuration Manager, you use the [SmsPageControl.PropertyManager](/previous-versions/system-center/developer/cc146982(v=msdn.10)) object to access objects that are selected in the Configuration Manager console.  

> [!NOTE]
>  If no object is selected in the Configuration Manager console, an empty PropertyManager object is created and passed to the form. This can be used for creating new objects.  

 The form manages the serialization of objects in the PropertyManager object, and any changes you make are automatically saved when you click **OK**, or they are abandoned when you click **Cancel**.  

 Depending on the SelectionMode attribute of the action's [ActionDescription](/previous-versions/system-center/developer/cc147252(v=msdn.10)) element, more than one object can be passed to the *PropertyManager* object. Changes that you make by using the *PropertyManager* object are then applied to all objects that are passed in. If you want to access the individual objects, you must cast the *PropertyManager* object to a [ResultObjectsManager](/previous-versions/system-center/developer/cc147410(v=msdn.10)). You then access the objects through the ResultObjectsManager object collection.  

 For more information, see [Configuration Manager Action XML](../../../../develop/core/servers/console/configuration-manager-action-xml.md).  

 For information about getting the property manager in a dialog box, see [How to Create a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-dialog-box.md).  

## Displaying the Package Name  
 The following procedure demonstrates using a [PropertyManager](/previous-versions/system-center/developer/cc146982(v=msdn.10)) object to access a single object passed to a property sheet. Clicking a button displays a message box that contains the name of a selected package. To complete these steps, you must first perform the actions in the following topics:  

-   [How to Create a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-property-sheet.md)  

-   [How to Create Form XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-property-sheet.md)  

-   [How to Create Action XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-action-xml-for-a-configuration-manager-property-sheet.md)  

#### To display the package name  

1.  If the Configuration Manager console is open, close it.  

2.  In Visual Studio 2010, open the project you created in [How to Create a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-property-sheet.md).  

3.  In Solution Explorer, right-click **ConfigMgrControl.cs**, and then click **View Designer**.  

4.  In the Toolbox, click the **Common Controls** tab, and then double-click **Button**. A button named **button1** is added to your control on the **User Control Designer**.  

5.  In the **User Control Designer**, double-click **button1** and type the following code in the **button1_Click** method source code that is displayed:  

    ```  
    MessageBox.Show(string.Format("The {0} package was selected", PropertyManager["Name"].StringValue));  
    ```  

6.  Build the project and copy the assembly to the %*ProgramFiles*%\Microsoft Endpoint Manager\AdminConsole\bin folder.  

7.  Open the Configuration Manager console, and navigate to the **Packages** node under **Software Distribution**.  

8.  Right-click a package, and then click **Show my Dialog Box**. The dialog box is displayed.  

9. Click the button, and the name of the package is displayed in the dialog box.  

## See Also  
 [About Configuration Manager Forms](../../../../develop/core/servers/console/about-configuration-manager-console-forms.md)   
 [How to Bind Configuration Manager Data to a Form](../../../../develop/core/servers/console/how-to-bind-configuration-manager-data-to-a-form.md)
