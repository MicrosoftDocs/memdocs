---
title: "List All Programs and Their Maximum Run Time Value"
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
ms.assetid: 8334dc55-78fe-4305-bd01-ce595c1a924asearchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to List All Programs and Their Maximum Run Time Value
In System Center Configuration Manager, you can list all programs with their maximum run time values by using the `SMS_Package` and `SMS_Program` classes and class properties.  

### To list all programs and their maximum run times  

1.  Set up a connection to the SMS Provider.  

2.  Load the available packages by using the `SMS_Package` class.  

3.  Enumerate through each set of programs using the `SMS_Program` class and the `PackageID` property from each package.  

4.  Output the package name, program name, and maximum run time value for each program.  

## Example  
 The following example method shows how to list all programs, with corresponding package name, program name, and maximum run times.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ListPackagesProgramsandMaximumRunTimeValue(connection)  
    Const wbemFlagReturnImmediately = 16    Const wbemFlagForwardOnly = 32    Dim packageQuery    Dim allPackages    Dim package    Dim packageID    Dim program    Dim programsForPackage  
    ' Build query to get all of the packages.   
    packageQuery = "SELECT * FROM SMS_Package"  

    ' Run query.  
    Set allPackages = connection.ExecQuery(packageQuery, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

    ' The query returns a collection of package objects that needs to be enumerated.  
    For Each package In allPackages       

        ' Output package name and get the PackageID value to use in program query.  
        WScript.Echo ""  
        WScript.Echo "Package: "  & package.Name  
        packageID = package.PackageID  

        ' Build query to get the programs for the package.   
        packageQuery = "SELECT * FROM SMS_Program WHERE PackageID='" & packageID & "'"  

        ' Run query.  
        Set programsForPackage = connection.ExecQuery(packageQuery, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

        ' The query returns a collection of program objects that needs to be enumerated.  
        For Each program In programsForPackage       

            ' Output Maximum Runtime Value for each program found.  
            WScript.Echo "  Program: "  & program.ProgramName  
            WScript.Echo "  Maximum Runtime Value: "  & program.Duration  

        Next                             
    Next  

End Sub  

```  

```c#  

public void ListPackagesProgramsandMaximumRunTimeValue(WqlConnectionManager connection)  
{      
    try  
    {  
        // Build query to get the packages.   
        string packageQuery = "SELECT * FROM SMS_Package";  

        // Load the specific program to change (programname is a key value and must be unique).  
        IResultObject allPackages = connection.QueryProcessor.ExecuteQuery(packageQuery);  

        // The query returns a collection of packages that needs to be enumerated.  
        foreach(IResultObject package in allPackages)       
        {        
            // Output package name and get the PackageID value to use in program query.  
            Console.WriteLine();  
            Console.WriteLine("Package: "  + package["Name"].StringValue);  
            string packageID = package["PackageID"].StringValue;  

            // Build query to get the programs for the package.   
            string programQuery = "SELECT * FROM SMS_Program WHERE PackageID='" + packageID + "'";  

            // Load the all programs belonging to the package.  
            IResultObject programsForPackage = connection.QueryProcessor.ExecuteQuery(programQuery);  

            // The query returns a collection of programs that needs to be enumerated.  
            foreach(IResultObject program in programsForPackage)       
            {        
                // Output Maximum Runtime Value for each program found.  
                Console.WriteLine("   Program: "  + program["ProgramName"].StringValue);  
                Console.WriteLine("   Maximum Runtime Value: "  + program["Duration"].IntegerValue);  
            }                 
        }  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to list the packages and programs. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  

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
