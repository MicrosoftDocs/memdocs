---
title: "Modify the Supported Platforms for a Program"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 58f4f08b-bc7f-4e6e-989c-39769f0f3f12
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Modify the Supported Platforms for a Program
Your application can add supported platforms to a package, in Configuration Manager, by obtaining specific instances of the `SMS_Package` and `SMS_Program` classes and then adding an instance of the `SMS_OS_Details` class to the `SupportedOperatingSystems` property.  

### To modify the supported platforms for a program  

1.  Set up a connection to the SMS Provider.  

2.  Obtain an existing package object by using the `SMS_Package` class.  

3.  Obtain an existing program object by using the `SMS_Program` class.  

4.  Create and populate an instance of the `SMS_OS_Details` class.  

5.  Add the new `SMS_OS_Details` instance to the `SupportedOperatingSystems` property of the program object (from step 3).  

## Example  
 The following example method shows how to add supported platforms for a program.  

> [!NOTE]
>  A slight variation of this example could change property values for all of the programs associated with a specific package. For an example, see the [How to List All Programs and Their Maximum Run Time Value](../../../../develop/core/servers/configure/how-to-list-all-programs-and-their-maximum-run-time-value.md) code example. However, for a more efficient method of accessing a specific program, using the `PackageID` and `ProgramName`, see the [How to Modify Program Properties](../../../../develop/core/servers/configure/how-to-modify-program-properties.md) code example.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub ModifySupportedPlatformsForProgram(connection,          _  
                                       existingPackageID,   _  
                                       existingProgramName, _  
                                       newMaxVersion,       _  
                                       newMinVersion,       _  
                                       newName,             _  
                                       newPlatform)   

' Define a constant with the hexadecimal value for RUN_ON_ANY_PLATFORM.   
    Const wbemFlagReturnImmediately = 16  
    Const wbemFlagForwardOnly = 32  
    Const RUN_ON_ANY_PLATFORM = &H08000000  
    Dim packageQuery  
    Dim package  
    Dim allProgramsForPackage  
    Dim programQuery  
    Dim program  
    Dim programPath  
    Dim checkPlatformValue  
    Dim tempSupportedPlatform  
    Dim tempSupportedPlatformsArray  
    ' Build a query to get the specified package.   
     packageQuery = "SMS_Package.PackageID='" & existingPackageID & "'"  
    ' Run the query to get the package.   
    Set package = connection.Get(packageQuery)      
    ' Output package name and ID.   
    WScript.Echo "Package ID:     "  & package.PackageID  
    WScript.Echo "Package Name:   "  & package.Name      
    ' Build a query to get the programs for the package.   
    programQuery = "SELECT * FROM SMS_Program WHERE PackageID='" & existingPackageID & "'"      
    ' Run the query to get the programs.   
    Set allProgramsForPackage = connection.ExecQuery(programQuery, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)      
    'The query returns a collection of program objects that needs to be enumerated.   
    For Each program In allProgramsForPackage                         
        If program.ProgramName = existingProgramName Then              
            ' Get all program object properties (in this case we specifically need some lazy properties).   
            programPath = program.Put_  
            programPath = Mid(programPath, InStr(1, programPath, ":") + 1)   
            Set program = connection.Get(programPath)   
            ' Check whether RUN_ON_ANY_PLATFORM is set.   
            checkPlatformValue = (program.ProgramFlags AND RUN_ON_ANY_PLATFORM)   
            If checkPlatformValue <> 0 Then  
               ' RUN_ON_ANY_PLATFORM is set. Removing RUN_ON_ANY_PLATFORM value.   
                program.ProgramFlags = (program.ProgramFlags XOR RUN_ON_ANY_PLATFORM)   
            End If                           
            ' Output the program name that is being checked for supported platforms.   
            WScript.Echo "Program Name: "  & program.ProgramName             
            ' Create  
            Set tempSupportedPlatform = connection.Get("SMS_OS_Details").SpawnInstance_  
            ' Populate tempSupportedPlatform values.   
            tempSupportedPlatform.MaxVersion = newMaxVersion  
            tempSupportedPlatform.MinVersion = newMinVersion  
            tempSupportedPlatform.Name       = newName  
            tempSupportedPlatform.Platform   = newPlatform  
            ' Get the array of supported operating systems.   
            tempSupportedPlatformsArray = program.SupportedOperatingSystems  
            ' Add the new supported platform values (object) to the temporary array.   
            ReDim Preserve tempSupportedPlatformsArray (Ubound(tempSupportedPlatformsArray) + 1)   
            Set tempSupportedPlatformsArray(Ubound(tempSupportedPlatformsArray)) = tempSupportedPlatform  
            ' Replace the SupportedOperatingSystems object array with the new updated array.   
            program.SupportedOperatingSystems = tempSupportedPlatformsArray  
            ' Save the program.   
            program.Put_  
            ' Output success message.   
            WScript.Echo "Supported Platforms Updated "  
        End If  
    Next  
End Sub  
```  

```c#  

public void ModifyProgramSupportedPlatforms(WqlConnectionManager connection,  
                                    string existingPackageID,  
                                    string existingProgramNameToModify,  
                                    string newMaxVersion,  
                                    string newMinVersion,  
                                    string newName,  
                                    string newPlatform)  
{  
    try  
    {  
        // Define a constant with the hexadecimal value for RUN_ON_ANY_PLATFORM.   
        const Int32 RUN_ON_ANY_PLATFORM = 0x08000000;  

        // Build query to get the programs for the package.   
        string query = "SELECT * FROM SMS_Program WHERE PackageID='" + existingPackageID + "'";  

        // Load the specific program to change (programname is a key value and must be unique).  
        IResultObject programsForPackage = connection.QueryProcessor.ExecuteQuery(query);  

        // The query returns a collection that needs to be enumerated.  
        foreach (IResultObject program in programsForPackage)  
        {  
            // If a match for the program name is found, make the change(s).  
            if (program["ProgramName"].StringValue == existingProgramNameToModify)  
            {  
                // Get all properties, specifically the lazy properties, for the program object.  
                program.Get();  

                // Check whether RUN_ON_ANY_PLATFORM is already set.  
                Int32 checkPlatformValue = (program["ProgramFlags"].IntegerValue & RUN_ON_ANY_PLATFORM);  

                if (checkPlatformValue != 0)  
                {  
                    // RUN_ON_ANY_PLATFORM is set. Removing RUN_ON_ANY_PLATFORM value.  
                    program["ProgramFlags"].IntegerValue = program["ProgramFlags"].IntegerValue ^ RUN_ON_ANY_PLATFORM;  
                }  

                // Create a new array list to hold the supported platform window objects.  
                List<IResultObject> tempSupportedPlatformsArray = new List<IResultObject>();  

                // Create and populate a temporary SMS_OS_Details object with the new operating system values.  
                IResultObject tempSupportedPlatformsObject = connection.CreateEmbeddedObjectInstance("SMS_OS_Details");  

                // Populate temporary SMS_OS_Details object with the new supported platforms values.  
                tempSupportedPlatformsObject["MaxVersion"].StringValue = newMaxVersion;  
                tempSupportedPlatformsObject["MinVersion"].StringValue = newMinVersion;  
                tempSupportedPlatformsObject["Name"].StringValue = newName;  
                tempSupportedPlatformsObject["Platform"].StringValue = newPlatform;  

                // Populate the local array list with the existing supported platform objects (type SMS_OS_Details).  
                tempSupportedPlatformsArray = program.GetArrayItems("SupportedOperatingSystems");  

                // Add the newly created service window object to the local array list.  
                tempSupportedPlatformsArray.Add(tempSupportedPlatformsObject);  

                // Replace the existing service window objects from the target collection with the temporary array that includes the new service window.  
                program.SetArrayItems("SupportedOperatingSystems", tempSupportedPlatformsArray);  

                // Save the new values in the collection settings instance associated with the Collection ID.  
                program.Put();  

                // Output program name.  
                Console.WriteLine("Modified program: " + program["ProgramName"].StringValue);  
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

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingPackageID`|-   Managed: `String`<br />-   VBScript: `String`|The package ID for an existing package.|  
|`existingProgramName`|-   Managed: `String`<br />-   VBScript: `String`|The program name for an existing program.|  
|`newMaxVersion`|-   Managed: `String`<br />-   VBScript: `String`|The maximum supported version.|  
|`newMinVersionsion`|-   Managed: `String`<br />-   VBScript: `String`|The minimum supported version.|  
|`newName`|-   Managed: `String`<br />-   VBScript: `String`|The modified program name.|  
|`newPlatform`|-   Managed: `String`<br />-   VBScript: `String`|The new platform.|  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

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
