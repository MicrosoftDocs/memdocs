---
description: Learn how to create an XML file that describes an SmsFormData class using a Create Form XML for a Configuration Manager property sheet.
title: Create Form XML for a Property Sheet
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: ce0a6939-840e-401c-9843-d5c94c00b9e6
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Create Form XML for a Configuration Manager Property Sheet
In Configuration Manager, to create the form XML for a Configuration Manager property sheet, you create an XML file that describes an `SmsFormData`.  

 Every Configuration Manager console form extension has an associated form XML file that describes the assembly, the type of the form to be displayed, and—in the case of property sheets—how the property pages are organized. The property sheet XML file is referenced by the action XML when an action is selected.  

> [!NOTE]
>  The name of the form XML file is significant because it is used in the action XML to identify the form XML.  

 The following procedure demonstrates how to create the form XML file for the control and property page you created in [How to Create a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-property-sheet.md).  

 After completing the following procedure, you must create an action to load the property sheet. For more information, see [How to Create Action XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-action-xml-for-a-configuration-manager-property-sheet.md).  

> [!NOTE]
>  To see the form XML used by the Configuration Manager console, see %*ProgramFiles*%\AdminConsole\XmlStorage\Forms. These can be useful for creating your own form XML.  

### To create the form XML for a property sheet  

1.  If it is open, close the Configuration Manager console.  

2.  In Notepad, create an XML file that contains the following XML:  

    ```xml
    <?xml version="1.0" encoding="utf-8"?>  
    <SmsFormData xmlns="https://schemas.microsoft.com/SystemsManagementServer/2005/03/ConsoleFramework" FormatVersion="1">  
      <Form Id="PROPERTYSHEETGUID" CustomData="SomeData" FormType="PropertySheet" ForceRefresh="true">  
        <Assembly Name="ConfigMgrControl.dll" Namespace="Microsoft.ConfigurationManagement.AdminConsole.ConfigMgrPropertySheet" />  
        <Pages>  
          <Page VendorId="YOURCOMPANY" Id="VENDORGUID" Type="ConfigMgrControlPage" />  
        </Pages>  
      </Form>  
    </SmsFormData>  
    ```  

3.  In Visual Studio 2010, on the **Tools** menu, click **Create GUID**.  

4.  In the **Create GUID** dialog box, in the **GUID format** panel, select **Registry Format**.  

5.  Click **New GUID**, and then click **Copy**.  

6.  In the XML above, paste the GUID into PROPERTYSHEETGUID. A single opening `{` and a single closing `}` must wrap the GUID. For example, `{ab60b75e-b64a-44c0-ad63-d96d289f39ca}`.  

7.  Repeat steps 3 through 5, and paste the GUID into VENDORGUID.  

8.  In the preceding XML, change YOURCOMPANY to your company name.  

9. Save the XML file in the folder %*ProgramFiles*%\AdminConsole\XmlStorage\Extensions\Forms with the file name ConfigMgrPropertySheet.xml. Be sure to save the file as type `All Files`. If the Extensions folder and Forms folder do not yet exist, create them.  

10. Start the Configuration Manager console, and select the action you defined in [How to Create Action XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-action-xml-for-a-configuration-manager-property-sheet.md).  

     The property sheet you created in [How to Create a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-property-sheet.md) appears.  

## See Also  
 [About Configuration Manager Forms](../../../../develop/core/servers/console/about-configuration-manager-console-forms.md)   
 [How to Create Action XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-action-xml-for-a-configuration-manager-property-sheet.md)   
 [How to Create a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-property-sheet.md)
