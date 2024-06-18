---
title: Create Form XML for a Dialog Box
titleSuffix: Configuration Manager
description: To create the form XML for a Configuration Manager dialog box, you create an XML file that describes an SmsFormData.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 811546e7-ae62-4b2a-af78-29293d81f182
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Create Form XML for a Configuration Manager Dialog Box
In Configuration Manager, to create the form XML for a Configuration Manager dialog box, you create an XML file that describes a [SmsFormData](/previous-versions/system-center/developer/cc147304(v=msdn.10)).  

 The form XML is similar to the property sheet form XML with the following exceptions:  

- `FormType` must be set to `Dialog`.  

  The following procedure demonstrates how to create the form XML file for the dialog box you created in [How to Create a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-dialog-box.md).  

### To create the form XML for a dialog box  

1.  If it is open, close the Configuration Manager console.  

2.  In Notepad, create an XML file that contains the following XML:  

    ```  

    <?xml version="1.0" encoding="utf-8"?>  
    <SmsFormData FormatVersion="1.0" xmlns="https://schemas.microsoft.com/SystemsManagementServer/2005/03/ConsoleFramework">  
      <Form Id="{DIALOGGUID}" CustomData="User Properties" FormType="CustomDialog" >  
        <Assembly Name="ConfigMgrDialogControl" Namespace="Microsoft.ConfigurationManagement.AdminConsole.ConfigMgrDialogBox" ClassType="ConfigMgrDialogControl"/>  
      </Form>  
    </SmsFormData>  
    ```  

3.  In Visual Studio 2010, on the **Tools** menu, click **Create GUID**.  

4.  In the **Create GUID** dialog box, in the **GUID format** panel, select **Registry Format**.  

5.  Click **New GUID**, and then click **Copy**.  

6.  In the XML above, paste the GUID into DIALOGGUID. Be sure to keep the open **{** and closing **}** in the XML.  

7.  Save the XML file in the folder, %*ProgramFiles*%\AdminConsole\XmlStorage\Extensions\Forms with the file name ConfigMgrDialogControl.xml. The file name must match the `DialogId` element of the action XML. If the Extensions folder does not yet exist, create it. Be sure to save the file as type `All Files`.  

8.  Start the Configuration Manager console, and select the action you defined in [How to Create Action XML for a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-action-xml-for-a-configuration-manager-dialog-box.md).  

     The property sheet you created in [How to Create a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-dialog-box.md) appears.  

## See Also  
 [How to Create a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-dialog-box.md)   
 [How to Create Action XML for a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-action-xml-for-a-configuration-manager-dialog-box.md)   
 [How to Create Form XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-property-sheet.md)
