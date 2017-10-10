---
title: "Create Action XML for a Property Sheet"
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
ms.assetid: ab60b75e-b64a-44c0-ad63-d96d289f39casearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create Action XML for a Configuration Manager Property Sheet
In System Center Configuration Manager, to display a property sheet or dialog box in the Configuration Manager console, you create a `ShowDialog` action. Like other actions, the `ShowDialog` action defines a context menu and action pane action that the user selects to show the dialog box. To define the `ShowDialog` action, you create an XML file that describes a [ActionDescription](https://msdn.microsoft.com/library/microsoft.configurationmanagement.adminconsole.schema.actiondescription.aspx) element.  

 For more information about property sheet and dialog box actions, see [Configuration Manager ShowDialog Action](../../../../develop/core/servers/console/showdialog-action.md).  

 The following procedure creates the action XML for showing the property sheet you created in [How to Create a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-property-sheet.md). You must also complete [How to Create Form XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-property-sheet.md) before completing the following procedure.  

### To create action XML for a property sheet  

1.  If it is open, close the Configuration Manager console.  

2.  In Notepad, create an XML file that contains the following XML:  

    ```  
    <?xml version="1.0"?>  
    <ActionDescription Description="DisplayDescription" DisplayName="DisplayName" SynchronousAction="true" Class="ShowDialog" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
       <ShowOn>       <string>DefaultHomeTab</string>  
           <string>ContextMenu</string>   
       </ShowOn>   
       <DialogId>Package</DialogId>   
    </ActionDescription>  
    ```  

3.  Save the XML file in the folder %*ProgramFiles*%\AdminConsole\XmlStorage\Extensions\Actions\9c69b0aa-a27c-43c9-8c26-5f964106a881. The GUID value identifies packages in the results pane. The file name can be anything with an .xml extension. Be sure to save the file as type `All Files`. If they do not exist, create the Actions folder and Actions subfolder.  

4.  Load the Configuration Manager console, and in the console tree **Packages** node, right-click a package in the results pane, and then click **DisplayName**. A property sheet appears.  

## See Also  
 [How to Create a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-property-sheet.md)   
 [How to Add a Property Page to an Existing Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-add-a-property-page-to-an-existing-configuration-manager-property-sheet.md)   
 [How to Create Form XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-property-sheet.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)
