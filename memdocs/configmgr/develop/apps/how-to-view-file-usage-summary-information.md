---
title: "View File Usage Summary Information"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: c8b466d3-3f6b-4f6b-a0fd-5928de665e60
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to View File Usage Summary Information
You view file usage summary information, in Configuration Manager, by using the [SMS_MeteredFiles](../../develop/reference/apps/sms_meteredfiles-server-wmi-class.md) and [SMS_FileUsageSummary](../../develop/reference/apps/sms_fileusagesummary-server-wmi-class.md) classes.  

### To view file usage summary information  

1.  Set up a connection to the SMS Provider.  

2.  Get a collection of all of the metered files [SMS_MeteredFiles](../../develop/reference/apps/sms_meteredfiles-server-wmi-class.md).  

3.  Get a collection of all of the summarized files [SMS_FileUsageSummary](../../develop/reference/apps/sms_fileusagesummary-server-wmi-class.md).  

4.  Loop through the summarized file information, displaying information as required.  

## Example  
 The following example method displays file usage summary information by using the [SMS_MeteredFiles](../../develop/reference/apps/sms_meteredfiles-server-wmi-class.md) and [SMS_FileUsageSummary](../../develop/reference/apps/sms_fileusagesummary-server-wmi-class.md) classes.  

> [!NOTE]
>  The example code below is relatively inefficient. In an environment with large amounts of data (large result sets), it would be better to do the query on SMS_MeteredFiles, then loop over that result, doing individual queries for SMS_FileUsageSummary where SMS_FileUsageSummary.FileID=meteredFile.FileID.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

sub ViewFileUsageSummaryInfo(connection)  

' Get SMS_MeteredFiles - used to match FileID to a file name  

' Build query to get all metered files.  
meteredFilesQuery = "SELECT * FROM SMS_MeteredFiles"  

' Run query.  
Set meteredFiles = connection.ExecQuery(meteredFilesQuery, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

' Get the summarized files.  

' Build query to get all file usage summary information.  
fileUsageSummaryQuery = "SELECT * FROM SMS_FileUsageSummary"  

' Run query.  
Set fileUsageSummary = connection.ExecQuery(fileUsageSummaryQuery, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

' Output file usage summary information.  
For Each summariedFile in fileUsageSummary  

    For each meteredFile in meteredFiles  

        if meteredFile.MeteredFileID=summariedFile.FileID then  
            wscript.echo "File Name: " & meteredFile.FileName  
            Exit For   
        end if  

    next      

    ' As matching summary information is found, output details.  
    wscript.echo "File ID: "             & summariedFile.FileID  
    wscript.echo "Distinct User Count: " & summariedFile.DistinctUserCount  
    wscript.echo "Interval Start: "      & summariedFile.IntervalStart  
    wscript.echo "Interval Width: "      & summariedFile.IntervalWidth  
    wscript.echo "Site Code: "           & summariedFile.SiteCode  
    wscript.echo " "  

Next  

end sub  

```  

```c#  

public void ViewFileUsageSummaryInfo(WqlConnectionManager connection)  
{  
    try  
    {  
        // Build query to get all metered files.  
        string meteredFilesQuery = "SELECT * FROM SMS_MeteredFiles";  

        // Run meteredFiles query.  
        IResultObject meteredFilesTemp = connection.QueryProcessor.ExecuteQuery(meteredFilesQuery);  

        // Cache values to local list.  
        List<IResultObject> meteredFiles = new List<IResultObject>();  
        foreach (IResultObject meteredFileTemp in meteredFilesTemp)  
        {  
            meteredFiles.Add(meteredFileTemp);  
        }  

        // Build query to get all the file usage summary information.  
        string fileUsageSummaryQuery = "SELECT * FROM SMS_FileUsageSummary";  

        // Run fileUsageSummary query.  
        IResultObject fileUsageSummaryTemp = connection.QueryProcessor.ExecuteQuery(fileUsageSummaryQuery);  

        // Cache values to local list.   
        List<IResultObject> fileUsageSummary = new List<IResultObject>();  
        foreach (IResultObject summariedFileTemp in fileUsageSummaryTemp)  
        {  
            fileUsageSummary.Add(summariedFileTemp);  
        }  

        // Enumerate through the files.  
        foreach (IResultObject summariedFile in fileUsageSummary)  
        {                      
            foreach (IResultObject meteredFile in meteredFiles)  
            {  
                if (meteredFile["MeteredFileID"].StringValue == summariedFile["FileID"].StringValue)  
                {  
                    // As matching summary information is found, output details.                      
                    Console.WriteLine("File Name: " + meteredFile["MeteredFileName"].StringValue);  
                    break;  
                };  
            };  

            // As matching summary information is found, output details.                      
            Console.WriteLine("File ID: " + summariedFile["FileID"].StringValue);  
            Console.WriteLine("Distinct User Count: " + summariedFile["DistinctUserCount"].StringValue);  
            Console.WriteLine("Interval Start: " + summariedFile["IntervalStart"].StringValue);  
            Console.WriteLine("Interval Width: " + summariedFile["IntervalWidth"].StringValue);  
            Console.WriteLine("Site Code: " + summariedFile["SiteCode"].StringValue);  
            Console.WriteLine(" ");  
        };  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine();  
        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);  
    }  
}  

```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  

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
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [Configuration Manager Software Development Kit](../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [About the Configuration Manager Site Control File](../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_Component Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)
