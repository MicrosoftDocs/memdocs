---
title: "Import a Windows Driver Described by an INF File"
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
ms.assetid: 7855f112-ef75-4754-affb-170ded8e1d0csearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Import a Windows Driver Described by an INF File into Configuration Manager
You can import a Windows driver that is described by an information (.inf) file, in System Center Configuration Manager, by using the [CreateFromINF Method in Class SMS_Driver](../../develop/reference/osd/createfrominf-method-in-class-sms_driver.md).  

### To import a Windows driver  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Call the [CreateFromINF Method in Class SMS_Driver](../../develop/reference/osd/createfrominf-method-in-class-sms_driver.md) to get the initial [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) management base object.  

3.  Create an instance of [SMS_Driver](../../develop/reference/osd/sms_driver-server-wmi-class.md) by using the management base object.  

4.  Populate the `SMS_Driver` object.  

5.  Commit the `SMS_Driver` object.  

## Example  
 The following example method creates an `SMS_Driver` object for a Windows driver by using the supplied path and file name. The example also enables the driver by setting the value of the `IsEnabled` property to `true`. The helper function `GetDriverName` is used to get the name of the driver from the driver package XML.  

> [!NOTE]
>  The `path` parameter must be supplied as a Universal Naming Convention (UNC) network path, for example, \\\localhost\Drivers\ATIVideo\\.  

 In the example, the `LocaleID` property is hard-coded to English (U.S.). If you need the locale for non-U.S. installations, you can get it from the [SMS_Identification Server WMI Class](../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md) `LocaleID` property.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub ImportINFDriver(connection, path, name)  

    Dim driverClass  
    Dim inParams  
    Dim outParams  

    On Error Resume Next  

    ' Obtain an instance of the class   
    ' using a key property value.  

    Set driverClass = connection.Get("SMS_Driver")  

    ' Obtain an InParameters object specific  
    ' to the method.  
    Set inParams = driverClass.Methods_("CreateFromINF"). _  
        inParameters.SpawnInstance_()  

    ' Add the input parameters.  
    inParams.Properties_.Item("DriverPath") =  path  
    inParams.Properties_.Item("INFFile") =  name  

    ' Call the method.  
    ' The OutParameters object in outParams  
    ' is created by the provider.  
    Set outParams = connection.ExecMethod("SMS_Driver", "CreateFromINF", inParams)  

   If Err <> 0 Then  
        Wscript.Echo "Failed to add to the driver catalog: " + path + "\" + name  
        Exit Sub  
    End If      

    outParams.Driver.IsEnabled =  True  

    Dim LocalizedSettings(0)  
    Set LocalizedSettings(0) = connection.Get("SMS_CI_LocalizedProperties").SpawnInstance_()  
    LocalizedSettings(0).Properties_.item("LocaleID") =  1033   
    LocalizedSettings(0).Properties_.item("DisplayName") = _  
            GetDriverName(outParams.Driver.SDMPackageXML, "//DisplayName", "Text")  

    LocalizedSettings(0).Properties_.item("Description") = ""          
    outParams.Driver.LocalizedInformation = LocalizedSettings  

    ' Save the driver.  
    outParams.Driver.Put_  

End Sub  

Function GetDriverName(xmlContent, nodeName, attributeName)  
    ' Load the XML Document  
    Dim attrValue  
    Dim XMLDoc  
    Dim objNode  
    Dim displayNameNode  

    attrValue = ""  
    Set XMLDoc = CreateObject("Microsoft.XMLDOM")       
    XMLDoc.async = False  
    XMLDoc.loadXML(xmlContent)  

    'Check for a successful load of the XML Document.  
    If xmlDoc.parseError.errorCode <> 0 Then  
        WScript.Echo vbcrlf & "Error loading XML Document. Error Code : 0x" & hex(xmldoc.parseerror.errorcode)  
        WScript.Echo "Reason: " & xmldoc.parseerror.reason  
        WScript.Echo "Parse Error line " & xmldoc.parseError.line & ", character " & _  
                      xmldoc.parseError.linePos & vbCrLf & xmldoc.parseError.srcText  

        GetXMLAttributeValue = ""          
    Else  
        ' Select the node  
        Set objNode = xmlDoc.SelectSingleNode(nodeName)  

        If Not objNode Is Nothing Then  
            ' Found the element, now just pick up the Text attribute value  
            Set displayNameNode = objNode.attributes.getNamedItem(attributeName)  
            If Not displayNameNode Is Nothing Then  
               attrValue = displayNameNode.value  
            Else  
               WScript.Echo "Attribute not found"  
            End If  
        Else  
            WScript.Echo "Failed to locate " & nodeName & " element."  
        End If  
    End If  

    ' Save the results  
    GetDriverName = attrValue  
End Function  
```  

```c#  
public void ImportInfDriver(  
    WqlConnectionManager connection,   
    string path,   
    string name)  
{  
    try  
    {  
        Dictionary<string, object> inParams = new Dictionary<string, object>();  

        // Set up parameters for the path and file name.  
        inParams.Add("DriverPath", path);  
        inParams.Add("INFFile", name);  

        // Import the INF file.  
        IResultObject result = connection.ExecuteMethod("SMS_Driver", "CreateFromINF", inParams);  

        // Create the SMS_Driver driver instance from the management base object returned in result["Driver"].  
        IResultObject driver = connection.CreateInstance(result["Driver"].ObjectValue);  

        // Enable the driver.  
        driver["IsEnabled"].BooleanValue = true;  

        List<IResultObject> driverInformationList = driver.GetArrayItems("LocalizedInformation");  

        // Set up the display name and other information.  
        IResultObject driverInfo = connection.CreateEmbeddedObjectInstance("SMS_CI_LocalizedProperties");  
        driverInfo["DisplayName"].StringValue = GetDriverName(driver);  
        driverInfo["LocaleID"].IntegerValue = 1033;  
        driverInfo["Description"].StringValue = "";  

        driverInformationList.Add(driverInfo);  

        driver.SetArrayItems("LocalizedInformation", driverInformationList);  

        // Commit the SMS_Driver object.  
        driver.Put();  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to import driver: " + e.Message);  
        throw;  
    }  
}  

public string GetDriverName(IResultObject driver)          
{  
    // Extract   
    XmlDocument sdmpackage = new XmlDocument();  

    sdmpackage.LoadXml(driver.Properties["SDMPackageXML"].StringValue);  

    // Iterate over all the <DisplayName/> tags.  
    foreach (XmlNode displayName in sdmpackage.GetElementsByTagName("DisplayName"))           
    {                  
    // Grab the first one with a Text attribute not equal to null.  
        if (displayName != null && displayName.Attributes["Text"] != null    
            && !string.IsNullOrEmpty(displayName.Attributes["Text"].Value))    
        {                        
                // Return the DisplayName text.  
                return displayName.Attributes["Text"].Value;      
        }              
    }   
    // Default the driverName to the UniqueID.  
    return driver["CI_UniqueID"].StringValue;         
 }  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`path`|-   Managed: `String`<br />-   VBScript: `String`|A valid UNC network path to the folder that contains the driver contents. For example, \\\Servers\Driver\VideoDriver.|  
|`name`|-   Managed: `String`<br />-   VBScript: `String`|The name of the .inf file. For example, ATI.inf.|  

## Compiling the Code  
 This C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [CreateFromINF Method in Class SMS_Driver](../../develop/reference/osd/createfrominf-method-in-class-sms_driver.md)   
 [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md)   
 [How to Specify The Supported Platforms for a Driver](../../develop/osd/how-to-specify-the-supported-platforms-for-a-driver.md)   
 [Operating System Deployment Driver Management](../../develop/osd/operating-system-deployment-driver-management.md)
