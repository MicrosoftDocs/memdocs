---
title: "Add a Property Page to an Existing Property Sheet"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 182335e6-3505-49a9-84a1-e16221a42ea3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Add a Property Page to an Existing Configuration Manager Property Sheet
To add a property page to an existing property sheet, in Configuration Manager, you add the property page XML to the property sheet's XML file. For existing Configuration Manager property sheets, you copy the existing property XML file to the XmlStorage\Extensions\Forms folder from XmlStorage\Forms. When the Configuration Manager console loads, it will use the XML it finds in the XmlStorage\Extensions\Forms folder in preference to existing forms in XmlStorage\Forms.  

 Because multiple vendors can extend existing property sheets, you must deploy and remove your property sheets with care. For more information, see [About Configuration Manager Administrator Console Extension Deployment](../../../../develop/core/servers/console/console-extension-deployment.md).  

 The following procedure demonstrates how to add a property page to the `Properties` page for a package. To complete it. you will first need to create a property page. For more information, see [How to Create a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-property-sheet.md).  

### To add a property page to a Properties property sheet  

1.  Copy the package.xml file from %*ProgramFiles*%\Microsoft Endpoint Manager\AdminConsole\XmlStorage\Forms to %ProgramFiles%\Microsoft Endpoint Manager\AdminConsole\XmlStorage\Extensions\Forms.  

2.  In the package.xml file, add the following property page XML (you should place it below the other `<Page>` elements, near the end of the file):  

    ```  
    <Page VendorId="My Company" Id="{3F52B74A-373A-4c97-A142-C93E230948F8}" Assembly="ConfigMgrControl" Namespace="Microsoft.ConfigurationManagement.AdminConsole.ConfigMgrPropertySheet" Type="ConfigMgrControlPage" />  
    ```  

3.  In Visual Studio 2010, on the **Tools** menu, click **Create GUID**.  

4.  In the **Create GUID** dialog box, in the **GUID format** panel, select **Registry Format**.  

5.  Click **New GUID**, and then click **Copy**.  

6.  In the XML above, paste the GUID into PROPERTYSHEETGUID. A single opening `{` and a single closing `}` must wrap the GUID. For example, `{ab60b75e-b64a-44c0-ad63-d96d289f39ca}`.  

7.  Save the file, and start the Configuration Manager console.  

8.  Using the **Packages** node results pane, right-click a package, and then click **Properties**. The properties dialog box is displayed with your property page.  

## See Also  
 [About Configuration Manager Forms](../../../../develop/core/servers/console/about-configuration-manager-console-forms.md)   
 [How to Create Form XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-property-sheet.md)   
 [How to Create a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-property-sheet.md)
