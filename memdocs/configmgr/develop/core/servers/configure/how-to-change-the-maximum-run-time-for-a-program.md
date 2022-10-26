---
title: Change the Maximum Run Time for a Program
titleSuffix: Configuration Manager
description: In Configuration Manager, the following example shows how to modify a program by using the SMS_Package and SMS_Program classes and properties.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: af806aee-a8da-499b-9d46-86d888c6ddc4
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Change the Maximum Run Time for a Program
The following example shows how to modify a program, in Configuration Manager, by using the `SMS_Package` and `SMS_Program` classes and properties.  

> [!IMPORTANT]
>  Any advertised program fails to run when the maintenance windows defined on the client computer are set for a period that is less than that program's `Maximum allowed run time setting`. See the topic "Program Run Scenario Using Maintenance Windows" in the Configuration Manager documentation for more information.  

### To change the maximum run time for a program  

1.  Set up a connection to the SMS Provider.  

2.  Query for the programs associated with the existing package ID provided.  

3.  Enumerate through the programs until a match for the program name is found.  

4.  Replace the program maximum run time property with the one passed into the method.  

5.  Save the program object and properties.  

## Example  
 The following example method changes the maximum run time for an existing program.  

> [!NOTE]
>  A slight variation of this example could change property values for all of the programs associated with a specific package. For an example, see the [How to List All Programs and Their Maximum Run Time Value](../../../../develop/core/servers/configure/how-to-list-all-programs-and-their-maximum-run-time-value.md) code example. However, for a more efficient method of accessing a specific program, using the `PackageID` and `ProgramName`, see the [How to Modify Program Properties](../../../../develop/core/servers/configure/how-to-modify-program-properties.md) code example.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ModifyProgram(connection, existingpackageID, existingProgramNameToModify, newMaxRunTime)  

    Const wbemFlagReturnImmediately = 16  
    Const wbemFlagForwardOnly = 32  
    Dim query  
    Dim programsForPackage  
    Dim program  

    ' Build a query to get the programs for the package.   
    query = "SELECT * FROM SMS_Program WHERE PackageID='" & existingPackageID & "'"  

    ' Run the query.  
    Set programsForPackage = connection.ExecQuery(query, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

    ' The query returns a collection that needs to be enumerated.  
    For Each program In programsForPackage       

        ' If a match for the program name is found, make the change(s).  
        If program.ProgramName=existingProgramNameToModify Then  

            ' Replace the existing package property (in this case the package description).  
            program.Duration = newMaxRunTime  

            ' Save the program with the modified properties.  
            program.Put_  

            ' Output program name.  
            wscript.echo "Modified program: "  & program.ProgramName  

            Exit For  
        End If  
    Next  

End Sub  
```  

```c#  
public void ModifyProgram(WqlConnectionManager connection, string existingPackageID, string existingProgramNameToModify, int newMaxRunTime)  
{  

    try  
    {  
        // Build query to get the programs for the package.  
        string query = "SELECT * FROM SMS_Program WHERE PackageID='" + existingPackageID + "'";  

        // Load the specific program to change (programname is a key value and must be unique).  
        IResultObject programsForPackage = connection.QueryProcessor.ExecuteQuery(query);  

        // The query returns a collection that needs to be enumerated.  
        foreach(IResultObject program in programsForPackage)       
        {  
            // If a match for the program name is found, make the change(s).  
            if (program["ProgramName"].StringValue == existingProgramNameToModify)  
            {                      
                 // Replace the existing package property (in this case the package description).  
                 program["Duration"].IntegerValue = newMaxRunTime;  

                 // Save the program with the modified properties.  
                 program.Put();  

                 // Output program name.  
                 Console.WriteLine("Modified program: "  + program["ProgramName"].StringValue);  
            }  
        }  

    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to modify the program. Error: " + ex.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`<br /><br /> `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingPackageID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of an existing package with which to associate the program.|  
|`existingProgramNameToModify`|-   Managed: `String`<br />-   VBScript: `String`|The name for the program to modify.|  
|`newMaxRunTime`|-   Managed: `Integer`<br />-   VBScript: `Integer`|New approximate duration, in minutes, of program execution on the client computer.|  

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
