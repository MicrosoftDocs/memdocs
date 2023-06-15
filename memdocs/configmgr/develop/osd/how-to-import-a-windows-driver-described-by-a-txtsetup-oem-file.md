---
title: Import a Windows Driver Described by a Txtsetup.oem File
titleSuffix: Configuration Manager
description: Use the CreateFromOEM Method in Class SMS_Driver to import a Windows driver that is described by a Txtsetup.oem file in Configuration Manager.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 1b6e61bc-ac48-4229-8c13-d470e4e8caf0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Import a Windows Driver Described by a Txtsetup.oem File into Configuration Manager
You can import a Windows driver that is described by a Txtsetup.oem file, in Configuration Manager, by using the [CreateFromOEM Method in Class SMS_Driver](../../develop/reference/osd/createfromoem-method-in-class-sms_driver.md). Configuration Manager can automatically create definitions for most drivers from just an .inf file. However, when installing mass-storage drivers on pre-Windows Vista operating systems, Configuration Manager also must have some information that is contained in the Txtsetup.oem file. To facilitate this, `CreateFromOEM` creates [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) objects for each .inf file that is referenced in the Txtsetup.oem file. You then have the opportunity to customize the driver properties before saving them.  

> [!NOTE]
>  If a driver manufacturer has provided a Txtsetup.oem file, you should import the driver by using this procedure instead of the .inf files if you plan to deploy Windows 2000, Windows XP, or Windows Server 2003.  

### To import a Windows driver  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../core/understand/sms-provider-fundamentals.md).  

2.  Call the [SMS_Driver](../../develop/reference/osd/sms_driver-server-wmi-class.md) class [CreateFromOEM](../../develop/reference/osd/createfromoem-method-in-class-sms_driver.md) method to get a collection of management base objects.  

3.  For the management base objects create an SMS_Driver object for each driver.  

4.  Populate the SMS_Driver object.  

5.  Commit the SMS_Driver object.  

## Example  
 The following example method creates an [SMS_Driver](../../develop/reference/osd/sms_driver-server-wmi-class.md) object for a Windows driver by using the supplied path and Txtsetup.oem file name. The example also enables the driver by setting the value of the *IsEnabled* property to `true`. The helper function `GetDriverName` is used to get the name of the driver from the driver package XML.  

> [!NOTE]
>  The `path` parameter must be supplied as a Universal Naming Convention (UNC) network path, for example, \\\localhost\Drivers\VMSCSI\\.  

 In the example, the `LocaleID` property is hard-coded to English (U.S.). If you need the locale for non-U.S. installations, you can get it from the [SMS_Identification Server WMI Class](../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md)`LocaleID` property.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub ImportOemDriver(connection,path,name)  

    Dim inParams  
    Dim outParams  
    Dim driver  
    Dim driverClass  

    On Error Resume Next  

    Set driverClass = connection.Get("SMS_Driver")  

    Set inParams = driverClass.Methods_("CreateFromOEM").inParameters.SpawnInstance_()  

    ' Set the driver path and INF file.  
    inParams.Properties_.item("DriverPath") = path  
    inParams.Properties_.item("OEMFile") = name  

    ' Execute the method.  
        Set outParams = driverClass.ExecMethod_("CreateFromOEM", inParams)      

    If Err <> 0 Then  
        Wscript.Echo "Failed to import driver: " + path +"\" + name   
        Exit Sub  
    End If      

    For Each driver In outParams.Drivers  
        ' Set driver name and enable the driver.  
        Dim LocalizedSettings  
        LocalizedSettings = array(0)  

        Set  LocalizedSettings(0) = connection.Get("SMS_CI_LocalizedProperties").SpawnInstance_()  
        LocalizedSettings(0).Properties_.item("LocaleID") = 1033  
        LocalizedSettings(0).Properties_.item("DisplayName") = _  
               GetDriverName(driver.Properties_.item("SDMPackageXML"), "//DisplayName", "Text")  
        LocalizedSettings(0).Properties_.item("Description") = ""          
        driver.Properties_.item("LocalizedInformation") = LocalizedSettings  
        driver.Properties_.item("IsEnabled") = true  
        driver.Put_   
    Next              
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
public void ImportOemDriver(  
WqlConnectionManager connection,  
string path,  
string name)  
{  
    try  
    {  
        Dictionary<string, object> inParams = new Dictionary<string, object>();  

        // Set up parameters for the path and file name.  
        inParams.Add("DriverPath", path);  
        inParams.Add("OEMFile", name);  

        // Import the INF file.  
        IResultObject outParams = connection.ExecuteMethod("SMS_Driver", "CreateFromOEM", inParams);  

        // Create the driver instance from the management base object returned in result["Drivers"].  

        foreach (object obj in outParams["Drivers"].ObjectArrayValue)  
        {  
            IResultObject driver = connection.CreateInstance(obj);  
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
    //  Default the driverName to the UniqueID.  
    return driver["CI_UniqueID"].StringValue;         
 }  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`Connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`path`|-   Managed: `String`<br />-   VBScript: `String`|A valid UNC network path to the folder that contains the driver contents. For example, \\\Servers\Driver\VideoDriver.|  
|`name`|-   Managed: `String`<br />-   VBScript: `String`|The name of the Txtsetup.oem file. For example, you might have \\\server\drivers\Video for `path` and Txtsetup.oem for `name`.|  

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
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../develop/core/servers/configure/role-based-administration.md).  

## See also

[How to specify the supported platforms for a driver](how-to-specify-the-supported-platforms-for-a-driver.md)
