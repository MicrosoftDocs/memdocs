---
title: Create a Program
titleSuffix: Configuration Manager
ms.date: 03/23/2020
description: In Configuration Manager, the following example shows how to create a program by using the SMS_Program class and class properties.
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: de2289de-d10e-4454-be69-47209bf59113
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Create a Program
The following example shows how to create a program, in Configuration Manager, by using the `SMS_Program` class and class properties.  

> [!IMPORTANT]
>  Any advertised program will fail to run when the maintenance windows that are defined on the client computer are set for a period that is less than that program's **Maximum allowed run time setting**. For more information, see Program Run Scenario Using Maintenance Windows in the Configuration Manager documentation.  

### To create a program  

1. Set up a connection to the SMS Provider.  

2. Create the new program object by using the `SMS_Program` class.  

3. Populate the new program properties.  

   > [!TIP]
   >  When you create a program for a Task Sequence or a Virtual Application Package, the SMS_Program properties must be set to specific values. The following tables outline what those settings should be configured to.  

    Task Sequence  

    |Property Name|Property Value|  
   |-------------------|--------------------|  
   |ProgramName|*|  

    Virtual Application Package  

   | Property Name |                                                                                           Property Value                                                                                            |
   |---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |  CommandLine  | PkgGUID={E742FFD6-D539-42CC-9827-73535FC81E06}:VersionGUID={19366289-8C55-44E2-A5EC-7B385EFB4C30}<br /><br /> **Note:** The GUID values are taken from the virtual application's XML manifest file. |
   |  ProgramName  |                                                                                        [Virtual application]                                                                                        |


4. Save the new program and properties.  

## Example  
 The following example method creates a new program and populates its properties for use in software distribution.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub CreateProgram(connection, existingPackageID, newProgramName, newProgramComment, newProgramCommandLine, newMaxRunTime)  

    ' Create the new program object.    Dim newProgram  
    Set newProgram = connection.Get("SMS_Program").SpawnInstance_  

    ' Populate the program properties.  
    newProgram.PackageID = existingPackageID  
    newProgram.ProgramName = newProgramName  
    newProgram.Comment = newProgramComment  
    newProgram.CommandLine = newProgramCommandLine  
    newProgram.Duration = newMaxRunTime  

    ' Save the new program and properties.  
    newProgram.Put_  

    ' Output new program name.  
    wscript.echo "Created program: " & newProgramName  

End Sub  
```  

```c#  
public void CreateProgram(WqlConnectionManager connection,   
                          string existingPackageID,   
                          string newProgramName,   
                          string newProgramComment,   
                          string newProgramCommandLine,  
                          int newMaxRunTime)  
{  
    try  
    {  
        // Create an instance of SMS_Program.  
        IResultObject newProgram = connection.CreateInstance("SMS_Program");  

        // Populate basic program values.  
        newProgram["PackageID"].StringValue = existingPackageID;  
        newProgram["ProgramName"].StringValue = newProgramName;  
        newProgram["Comment"].StringValue = newProgramComment;  
        newProgram["CommandLine"].StringValue = newProgramCommandLine;  
        newProgram["Duration"].IntegerValue = newMaxRunTime;  

        // Save the new program instance and values.  
        newProgram.Put();  

        Console.WriteLine("Created program: " + newProgramName);  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to create program. Error: " + ex.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`<br /><br /> `swebemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingPackageID`|-   Managed: `String`<br />-   VBScript: `String`|The name of the package associated with the program.|  
|`newProgramName`|-   Managed: `String`<br />-   VBScript: `String`|The name for the new program.|  
|`newProgramComment`|-   Managed: `String`<br />-   VBScript: `String`|Comment that describes the program in the Configuration Manager console.|  
|`newProgramCommandLine`|-   Managed: `String`<br />-   VBScript: `String`|The command line that runs when the program is launched.|  
|`newMaxRunTime`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The approximate duration, in minutes, of program execution on the client computer. This parameter can have a max value of 720 minutes or 12 hours.|  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 System  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

 mscorlib  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## See Also  
 [Software distribution overview](software-distribution-overview.md)
