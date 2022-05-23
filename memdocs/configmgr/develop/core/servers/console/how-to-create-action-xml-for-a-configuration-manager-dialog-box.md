---
description: Learn how to create action XML for dialog boxes.
title: "Create Action XML for a Dialog Box"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: b946a1cb-d54a-48d3-a3f1-5db70c426513
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Create Action XML for a Configuration Manager Dialog Box
In Configuration Manager, to display a dialog box in the Configuration Manager console, you create a [Configuration Manager ShowDialog Action](../../../../develop/core/servers/console/showdialog-action.md) action. To define the `ShowDialog` action, you create an XML file that describes a [ActionDescription](/previous-versions/system-center/developer/cc147252(v=msdn.10)) element.  

 The following procedure creates the action XML for showing a dialog box. You must complete the procedures in the [How to Create a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-dialog-box.md) and [How to Create Form XML for a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-dialog-box.md) topics before you complete this procedure.  

> [!NOTE]
>  The dialog identifier <`DialogId`> must match the file name, without the XML extension, of the form XML you created in [How to Create Form XML for a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-dialog-box.md).  

### To create an action for a dialog box  

1.  If it is open, close the Configuration Manager console.  

2.  In Notepad, create an XML file that contains the following XML:  

    ```  
    <ActionDescription Class="ShowDialog" DisplayName="Show my Dialog Box" MnemonicDisplayName="Mnemonic" Description="Description"> <ShowOn>      <string>DefaultContextualTab</string> <!-- RIBBON -->     <string>ContextMenu</string> <!-- Context Menu -->   </ShowOn>        
     <DialogId>ConfigMgrDialogControl</DialogId>  
    </ActionDescription>  
    ```  

3.  Save the XML file in the folder, %*ProgramFiles*%\AdminUI\XmlStorage\Extensions\Actions\32815086-cce9-42de-95a4-0941da31114e. The GUID value identifies packages in the results pane. The file name can be anything with an .xml extension. Be sure to save the file as type `All Files`.  

4.  Start the Configuration Manager console, and in the console tree **Packages** node, right-click a package in the results pane, and then click **Show my Dialog Box**. A dialog box appears.  

## See Also  
 [How to Create a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-dialog-box.md)   
 [How to Create Form XML for a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-dialog-box.md)   
 [How to Create Action XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-action-xml-for-a-configuration-manager-property-sheet.md)   
 [How to Use Objects Passed to a Configuration Manager Forms](../../../../develop/core/servers/console/how-to-use-objects-passed-to-a-configuration-manager-form.md)   
 [How to Bind Configuration Manager Data to a Form](../../../../develop/core/servers/console/how-to-bind-configuration-manager-data-to-a-form.md)
