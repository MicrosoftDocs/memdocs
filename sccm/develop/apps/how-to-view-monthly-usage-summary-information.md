---
title: "View Monthly Usage Summary Information"
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
ms.assetid: 6c9c4ddf-0c0a-48ca-b9ef-099d2043fe27searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to View Monthly Usage Summary Information
You view monthly usage summary information, in System Center Configuration Manager, by using the [SMS_MeteredFiles](../../develop/reference/apps/sms_meteredfiles-server-wmi-class.md), [SMS_MonthlyUsageSummary](../../develop/reference/apps/sms_monthlyusagesummary-server-wmi-class.md), [SMS_MeteredUser](../../develop/reference/apps/sms_metereduser-server-wmi-class.md) and [SMS_R_System](../../develop/reference/core/clients/manage/sms_r_system-server-wmi-class.md) classes.  

> [!NOTE]
>  The metering data is only summarized at specified intervals (by default, daily at midnight). Metering data does not appear in the summarized data until the summarization task has run.  

### To view monthly usage summary information  

1.  Set up a connection to the SMS Provider.  

2.  Get all the metered files ([SMS_MeteredFiles](../../develop/reference/apps/sms_meteredfiles-server-wmi-class.md)).  

3.  Get all the monthly file usage summary information ([SMS_MonthlyUsageSummary](../../develop/reference/apps/sms_monthlyusagesummary-server-wmi-class.md)).  

4.  Get all the metered users ([SMS_MeteredUser](../../develop/reference/apps/sms_metereduser-server-wmi-class.md)).  

5.  Get all the computer names ([SMS_R_System](../../develop/reference/core/clients/manage/sms_r_system-server-wmi-class.md)).  

6.  Loop through the collections, displaying information as required.  

## Example  
 The following example method displays file usages summary information by using the [SMS_MeteredFiles](../../develop/reference/apps/sms_meteredfiles-server-wmi-class.md) and [SMS_FileUsageSummary](../../develop/reference/apps/sms_fileusagesummary-server-wmi-class.md) classes.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ViewMonthlySummary(connection)  

    ' Get SMS_MeteredFiles - used to match FileID to a file name  

        ' Build query to get all metered files.   
        meteredFilesQuery = "SELECT * FROM SMS_MeteredFiles"  

        ' Run query.  
        Set meteredFiles = connection.ExecQuery(meteredFilesQuery, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

    ' Get SMS_MonthlyUsageSummary  

        ' Build query to get all monthly summary information.  
        monthlyUsageSummaryQuery = "SELECT * FROM SMS_MonthlyUsageSummary"  

        ' Run query.  
        Set monthlyUsageSummaries = connection.ExecQuery(monthlyUsageSummaryQuery, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

    'Get SMS_MeteredUser  

        ' Build query to get all metered users.  
        meteredUserQuery = "SELECT * FROM SMS_MeteredUser"  

        ' Run query.  
        Set meteredUsers = connection.ExecQuery(meteredUserQuery, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

    'Get computer names   

        ' Build query to get all metered computers.  
        meteredComputerQuery = "SELECT * FROM SMS_R_System"  

        ' Run query.  
        Set meteredComputers = connection.ExecQuery(meteredComputerQuery, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

    For Each summary in monthlyUsageSummaries  

        For each meteredFile in meteredFiles  
            if meteredFile.MeteredFileID=summary.FileID then  
                wscript.echo "File Name:" & meteredFile.FileName  
                Exit For   
            end if  
        next      

        for each meteredUser in meteredUsers  
            if meteredUser.MeteredUserID=summary.MeteredUserID then  
                wscript.echo "User Name: " & meteredUser.FullName  
                Exit For  
            end if  
        next  

        wscript.echo "Usage Count:" & summary.UsageCount  
        wscript.echo "Terminal Service Usage Count:" & summary.TSUsageCount  

        for each computer in meteredComputers  
            if computer.ResourceId=summary.ResourceID then  
                wscript.echo "Computer:" & computer.Name  
                Exit For  
            end if  
        next  

        wscript.echo  

    Next  

end sub  

```  

```c#  

public void ViewMonthlySummaryInfo(WqlConnectionManager connection)  
{  
    try  
    {  
        // Get SMS_MeteredFiles - used to match FileID to a file name.  

            // Build query to get all metered files.  
            string meteredFilesQuery = "SELECT * FROM SMS_MeteredFiles";  

            // Run meteredFiles query.  
            IResultObject meteredFiles = connection.QueryProcessor.ExecuteQuery(meteredFilesQuery);  

        // Get SMS_MonthlyUsageSummary.  

            // Build query to get all of the monthly file usage summary information.  
            string monthlyUsageSummaryQuery = "SELECT * FROM SMS_MonthlyUsageSummary";  

            // Run monthlyUsageSummaryQuery query.  
            IResultObject monthlyUsageSummaries = connection.QueryProcessor.ExecuteQuery(monthlyUsageSummaryQuery);  

        // Get SMS_MeteredUsers.  

            // Build query to get all of the metered users.  
            string meteredUserQuery = "SELECT * FROM SMS_MeteredUser";  

            // Run meteredUser query.  
            IResultObject meteredUsers = connection.QueryProcessor.ExecuteQuery(meteredUserQuery);  

        // Get computer names.  

            // Build query to get all the metered computers.  
            string meteredComputersQuery = "SELECT * FROM SMS_R_System";  

            // Run fileUsageSummary query.  
            IResultObject meteredComputers = connection.QueryProcessor.ExecuteQuery(meteredComputersQuery);  

        // Enumerate through the lists, outputs results as matches are found.  
        foreach (IResultObject summary in monthlyUsageSummaries)  
        {                      
            foreach (IResultObject meteredFile in meteredFiles)  
            {                        
                if (meteredFile["MeteredFileID"].StringValue == summary["FileID"].StringValue)  
                {  
                    Console.WriteLine("File Name: " + meteredFile["FileName"].StringValue);  
                    break;  
                };  
            };  

            foreach(IResultObject meteredUser in meteredUsers)  
            {  
                if (meteredUser["MeteredUserID"].StringValue == summary["MeteredUserID"].StringValue)  
                {  
                    Console.WriteLine("User Name: " + meteredUser["FullName"].StringValue);  
                    break;  
                }  
            };  

            Console.WriteLine("Usage Count: " + summary["UsageCount"].StringValue);  
            Console.WriteLine("Terminal Service Usage Count: " + summary["TSUsageCount"].StringValue);  

            foreach(IResultObject computer in meteredComputers)  
            {  
                if(computer["ResourceId"].StringValue == summary["ResourceID"].StringValue)  
                {  
                    Console.WriteLine("Computer: " + computer["Name"].StringValue);  
                    break;  
                }  
            };  

            //   
            Console.WriteLine(" ");  
        };  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: **WqlConnectionManager**<br />-   VBScript: **SWbemServices**|A valid connection to the SMS Provider.|  

## Compiling the Code  
 This C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

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
 [System Center Configuration Manager Software Development Kit](../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Software Metering](../../develop/apps/software-metering.md)   
 [SMS_MeteredFiles Server WMI Class](../../develop/reference/apps/sms_meteredfiles-server-wmi-class.md)   
 [SMS_MeteredUser Server WMI Class](../../develop/reference/apps/sms_metereduser-server-wmi-class.md)   
 [SMS_MonthlyUsageSummary Server WMI Class](../../develop/reference/apps/sms_monthlyusagesummary-server-wmi-class.md)   
 [SMS_R_System Server WMI Class](../reference/core/clients/manage/sms_r_system-server-wmi-class.md)   
 [SMS_SummarizationInterval Server WMI Class](../../develop/reference/apps/sms_summarizationinterval-server-wmi-class.md)
