---
title: "Modify Program Properties"
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
ms.assetid: 7e4018e2-f4df-426a-b3f1-b6837aee7fa8searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Modify Program Properties
The following example shows how to modify a program, in System Center Configuration Manager, by using the `SMS_Package` and `SMS_Program` classes and properties.  

### To modify program properties  

1.  Set up a connection to the SMS Provider.  

2.  Get the program instance using the package ID and program name provided.  

3.  Replace the program description property with the one passed into the method.  

4.  Save the program object and properties.  

## Example  
 The following example method modifies program properties for software distribution.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ModifyProgram(connection, existingpackageID, existingProgramNameToModify, newProgramDescription)    

     ' Load the specific program to change (programname is a key value and must be unique).     Dim program  
     Set program = connection.Get("SMS_Program.PackageID='" & existingPackageID & "'" & ",ProgramName='" & existingProgramNameToModify & "'")  

     ' Replace the existing program property (in this case the program description).  
     program.Description = newProgramDescription  
     program.Comment = newProgramDescription  
     ' Save the program with the modified properties.  
     program.Put_  

     ' Output program name.  
     WScript.echo "Modified program: " & program.ProgramName              

End Sub  

```  

```c#  

public void ModifyProgram(WqlConnectionManager connection, string existingPackageID, string existingProgramNameToModify, string newProgramDescription)  
{  

    try  
    {  

        // Load the specific program to change (programname is a key value and must be unique).  
        IResultObject program = connection.GetInstance(@"SMS_Program.PackageID='" + existingPackageID + "',ProgramName='" + existingProgramNameToModify + "'");  

        // Replace the existing program property (in this case the program description).  
        program["Description"].StringValue = newProgramDescription;  
        program["Comment"].StringValue = newProgramDescription;  
        // Save the program with the modified properties.  
        program.Put();  

        // Output program name.  
        Console.WriteLine("Modified program: " + program["ProgramName"].StringValue);  

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
|`connection`<br /><br /> `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`existingPackageID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of an existing package with which to associate the program.|  
|`existingProgramNameToModify`|-   Managed: `String`<br />-   VBScript: `String`|The name for the program to modify.|  
|`newProgramDescription`|-   Managed: `String`<br />-   VBScript: `String`|The description for the new program.|  

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
 [Configuration Manager Software Distribution](../../../../develop/core/servers/configure/software-distribution.md)   
 [Software Distribution Packages](../../../../develop/core/servers/configure/software-distribution-packages.md)   
 [Software Distribution Programs](../../../../develop/core/servers/configure/software-distribution-programs.md)
