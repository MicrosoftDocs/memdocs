---
title: "Import Configuration Baselines and Items"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 9ce05e8b-bd49-47d4-827d-3676a96c28a8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Import Configuration Baselines and Configuration Items
In System Center Configuration Manager, importing a configuration baseline or configuration item by using the Configuration Manager SDK requires a properly formatted XML file. Unlike the Configuration Manager console, the Configuration Manager SDK does not support directly importing a CAB file.  

> [!IMPORTANT]
>  The encoding of the XML file must be set to UTF-16 encoded Unicode. The XML encoding can be identified in the XML header:  
>   
>  `<?xml version="1.0" encoding="utf-16" ?>`  

 When configuration data is imported into Configuration Manager, the format can be the following:  

-   DCM Digest XML only  

### To import Configuration Baselines and Configuration Items  

1.  Set up a connection to the SMS Provider.  

2.  Read the source XML file into a variable.  

3.  Create an instance the `SMS_ConfigurationItem` class.  

4.  Copy the source file contents (XML) into the `SMS_ConfigurationItem` property `SDMPackageXML`.  

5.  Save the configuration item instance.  

## Example  
 The following code examples show how to create an instance of a configuration baseline or a configuration item and then populate it by importing a configuration baseline or a configuration item XML definition.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub DCMImportBaselineOrCI(swbemServices,   _  
                          pathToFile)  

' Set required variables.  
readFile = 1  'constant   
fileContents          =    ""  
initialReadSucceeded  =    ""  
triStateTrue = -1  ' This sets the file read to Unicode.  

' Check if source xml file exists.  
set fileSytemObject = CreateObject("Scripting.FileSystemObject")  
If fileSytemObject.FileExists(pathToFile) Then  
    set textFile = fileSytemObject.OpenTextFile(pathToFile, readFile, False, triStateTrue)      
    fileContents = textFile.ReadAll  
    textFile.Close  

    initialReadSucceeded = true  

    set textFile = Nothing  

    Wscript.Echo " "  
    Wscript.Echo "Successfully read " & pathToFile  

Else  
    initialReadSucceeded = false  

    Wscript.Echo " "  
    Wscript.Echo "File does not exist."  
End If  
set fileSytemObject = Nothing  

If initialReadSucceeded Then  

    On Error Resume Next   

        ' Create an instance of configuration item.  
        set newCI = swbemServices.Get("SMS_ConfigurationItem").SpawnInstance_()        

        ' Copy specified file contents (XML) into SMS_ConfigurationItem property.  
        newCI.SDMPackageXML = fileContents  

        ' Save configuration item.  
        newCI.Put_  

        If Err.Number<>0 Then  
            Wscript.Echo "Couldn't create configuration item."  
            Wscript.Echo "Possible duplicate configuration item or invalid XML."  
            Wscript.Quit  
        End If  
    On Error Goto 0  
Else  
    Wscript.Echo " "  
    Wscript.Echo "Failed to create configuration item."     
End If    

End Sub  

```  

```c#  

public void DCMImportBaselineOrCI(WqlConnectionManager connection,  
                                  string pathToFile)  
{  

    // Set required variables.  
    string fileContents = null;  
    bool initialReadSucceeded = false;  

    // Load XML file using pathToFile variable.  
    try  
    {  
        // Open the file specified by the pathToFile variable and read the contents into a string.  
        using (StreamReader sr = new StreamReader(pathToFile, System.Text.Encoding.Unicode))  
        {  
            fileContents = sr.ReadToEnd();  
        }  

        Console.WriteLine("Successfully read " + pathToFile + ".");  

        initialReadSucceeded = true;  
    }  
    catch (Exception ex)  
    {  
        Console.WriteLine("Unable to read " + pathToFile + "." + "\n" + ex.Message);  
        throw;  
    }  

    // Run only if the initial read was successful.  
    if (initialReadSucceeded)  
    {  
        try  
        {  
            // Create an instance of Configuration Item.  
            IResultObject newCI = connection.CreateInstance("SMS_ConfigurationItem");  

            // Copy specified file contents (XML) into SMS_ConfigurationItem property.  
            newCI["SDMPackageXML"].StringValue = fileContents;  

            // Save new SMS_ConfigurationItem object.   
            newCI.Put();  
        }  
        catch (SmsException ex)  
        {  
            Console.WriteLine("Failed to create configuration item using " + pathToFile + ".");  
            Console.WriteLine(ex.Details);  
            throw;   
        }  
    }  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|-   `connection`<br />-   `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|pathToFile|-   Managed: `String`<br />-   VBScript: `String`|Path of the XML file to import.|  

## Compiling the Code  

### Namespaces  
 System  

 System.Collections.Generic  

 System.ComponentModel  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [About Configuration Baselines and Configuration Items](../../develop/compliance/about-configuration-baselines-and-configuration-items.md)   
 [How to Use Configuration Manager Objects With WMI](../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [SMS_BaselineAssignment Server WMI Class](../../develop/reference/compliance/sms_baselineassignment-server-wmi-class.md)   
 [SMS_ConfigurationItem Server WMI Class](../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md)
