---
title: "Track OS Deployment Migrations"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 08466d8e-e837-429d-a30b-2d90701a765e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Track Operating System Deployment Migrations in Configuration Manager
You track System Center Configuration Manager operating system migrations by inspecting the [SMS_StateMigration](../../develop/reference/osd/sms_statemigration-server-wmi-class.md) class.  

 The `StoreCreationDate`, `StoreDeletionDate`, and `StoreReleaseDate` properties can be used to identify the current state of the migration.  

### To track state migrations  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get an instance of [SMS_StateMigration](../../develop/reference/osd/sms_statemigration-server-wmi-class.md).  

3.  Calculate the current migration state using the `StoreCreationDate`, `StoreDeletionDate`, and `StoreReleaseDate` properties.  

## Example  
 The following example method enumerates through all migrations and determines whether they are in progress.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub MigrationState(connection)  

    Dim migrations  
    Dim migration  
    Dim inProgress  
    Dim zeroTime  

    zeroTime = "00000000000000.000000+***"  

    Set migrations = connection.ExecQuery( "Select * From SMS_StateMigration")  

    For Each migration in Migrations  
        inProgress=False  

        If migration.StoreCreationDate<>zeroTime Then  
            If migration.StoreReleaseDate = zeroTime Then  
                inProgress=True  
            Else If migration.StoreDeletionDate = zeroTime Then  
                inProgress = True  
            Else  
                inProgress = false  
            End If  
        End If     
        Else  
            inProgress=False  
        End If  

        WScript.StdOut.Write "Migration " + migration.MigrationID  
        If inProgress = True Then  
            Wscript.Echo " is in progress"  
        Else  
            WScript.Echo " is not in progress"  
        End If     
    Next  

End Sub     
```  

```c#  
public void MigrationState(WqlConnectionManager connection)  
{  
    try  
    {  
        IResultObject migrations =  
            connection.QueryProcessor.ExecuteQuery("Select * from SMS_StateMigration");  

        string zeroTime = "00000000000000.000000+***";  

        foreach (IResultObject migration in migrations)  
        {  
            Boolean inProgress = false;  

            if (migration["StoreCreationDate"].DateTimeValue.Equals(zeroTime) == false)  
            {  
                if (migration["StoreReleaseDate"].DateTimeValue.Equals(zeroTime) == true)  
                {  
                    inProgress = true;  
                }  
                else if (migration["StoreDeletionDate"].DateTimeValue.Equals(zeroTime) == true)  
                {  
                    inProgress = true;  
                }  
                else  
                {  
                    inProgress = false;  
                }  
            }  
            else  
            {  
                inProgress = false;  
            }  

            Console.Write("Migration " + migration["MigrationID"].StringValue);  
            if (inProgress)  
            {  
                Console.WriteLine(" is in progress");  
            }  
            else  
            {  
                Console.WriteLine(" is not in progress");  
            }  
        }  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed while displaying migration state: " + e.Message);  
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
 [Configuration Manager Operating System Deployment](../../develop/osd/operating-system-deployment.md)   
 [Configuration Manager Objects](../../develop/core/understand/configuration-manager-objects.md)   
 [Configuration Manager Programming Fundamentals](../../develop/core/understand/configuration-manager-programming-fundamentals.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [Operating System Deployment Computer Management](../../develop/osd/operating-system-deployment-computer-management.md)
