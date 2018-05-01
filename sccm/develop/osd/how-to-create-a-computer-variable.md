---
title: "Create a Computer Variable"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e4db0e59-84c0-44eb-8e41-acb91c4ee463
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Create a Computer Variable in Configuration Manager
You create a computer variable for a computer that is running System Center Configuration Manager by adding instances of [SMS_MachineVariable](../../develop/reference/osd/sms_machinevariable-server-wmi-class.md) to the [SMS_MachineSettings](../../develop/reference/osd/sms_machinesettings-server-wmi-class.md) class `MachineVariables` array property.  

### To create a computer variable  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get an instance of `SMS_MachineSettings`.  

3.  For each variable to be added, add instances of the embedded object a `SMS_MachineVariable` to the `MachineVariables` array property.  

4.  Commit the changes to the `SMS_MachineSettings` class instance.  

## Example  
 The following example method creates a collection variable and adds it to the collection identified by the supplied identifier.  

 In the example, the `LocaleID` property is hard-coded to English (U.S.). If you need the locale for non-U.S. installations, you can get it from the [SMS_Identification Server WMI Class](../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md) `LocaleID` property.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub CreateComputerVariable(connection, siteCode, name, value, mask, computerId)  

    Dim computerSettings  
    Dim computerVariables  
    Dim computerVariable  
    Dim Settings  

    ' See if the computer settings object already exists. if it does not, create it.  
    Set settings = connection.ExecQuery _  
      ("Select * From SMS_MachineSettings Where ResourceID = '" & computerID & "'")  

    If settings.Count = 0 Then  
        Wscript.Echo "Creating computer settings object"  
        Set computerSettings = connection.Get("SMS_MachineSettings").SpawnInstance_  
        computerSettings.ResourceID = computerId  
        computerSettings.SourceSite = siteCode  
        computerSettings.LocaleID = 1033  
        computerSettings.Put_  
    End If    

    ' Get the computer settings object.  
    Set computerSettings = connection.Get("SMS_MachineSettings.ResourceID='" & computerId &"'" )  

    ' Get the computer variables.  
    computerVariables=computerSettings.MachineVariables  

    ' Create and populate a new computer variable.  
    Set computerVariable = connection.Get("SMS_MachineVariable").SpawnInstance_  
    computerVariable.Name = name  
    computerVariable.Value = value  
    computerVariable.IsMasked = mask  

    ' Add the new computer variable.  
    ReDim Preserve computerVariables (UBound (computerVariables)+1)  
    Set computerVariables(UBound(computerVariables)) = computerVariable  

    computerSettings.MachineVariables=computerVariables  

    computerSettings.Put_  

 End Sub     
```  

```c#  
public void CreateComputerVariable(  
    WqlConnectionManager connection,  
    string siteCode,   
    string name,   
    string value,   
    bool mask,   
    int computerId)  
{  
    try  
    {  
        // Get the computer settings.  
        IResultObject computerSettings=null;  

        IResultObject computerSettingsQuery = connection.QueryProcessor.ExecuteQuery(  
            "Select * from SMS_MachineSettings where ResourceId = '" + computerId + "'");  

        foreach (IResultObject settings in computerSettingsQuery)  
        {  
            computerSettings = settings;  
        }  

        if (computerSettings == null) // It does not exist, so create it.  
        {  
            computerSettings = connection.CreateInstance(@"SMS_MachineSettings");  
            computerSettings["ResourceID"].IntegerValue = computerId;  
            computerSettings["SourceSite"].StringValue = siteCode;  
            computerSettings["LocaleID"].IntegerValue = 1033;  
            computerSettings.Put();  
            computerSettings.Get();  
        }  

        // Create the computer variable.  
        List<IResultObject> computerVariables = computerSettings.GetArrayItems("MachineVariables");  
        IResultObject computerVariable = connection.CreateEmbeddedObjectInstance("SMS_MachineVariable");  
        computerVariable["Name"].StringValue = name;  
        computerVariable["Value"].StringValue = value;  
        computerVariable["IsMasked"].BooleanValue = mask;  

        // Add the computer variable to the computer settings.  
        computerVariables.Add(computerVariable);  
        computerSettings.SetArrayItems("MachineVariables", computerVariables);  

        computerSettings.Put();  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to create computer variable: " + e.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code of the source site.|  
|`name`|-   Managed: `String`<br />-   VBScript: `String`|The name of the variable to be created.|  
|`value`|-   Managed: `String`<br />-   VBScript: `String`|The value of the variable.|  
|`mask`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|Specifies whether the value is displayed in the Configuration Manager console.<br /><br /> `true` - the variable value is not displayed.<br /><br /> `false` - the variable value is displayed.|  
|`computerID`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The computer identifier. Typically this is the [SMS_R_System](../../develop/reference/core/clients/manage/sms_r_system-server-wmi-class.md) class `ResourceID` property.|  

## Compiling the Code  
 The C# example has the following compilation requirements:  

### Namespaces  
 System  

 System.Collections.Generic  

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
 [Operating System Deployment Computer Management](../../develop/osd/operating-system-deployment-computer-management.md)
