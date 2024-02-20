---
title: Read the Tally Intervals for a Site
titleSuffix: Configuration Manager
description: In Configuration Manager, you can read the available tally intervals for a site by inspecting the site control file SMS_COMPONENT_STATUS_SUMMARIZER object Summary_Intervals embedded property list.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 856f0bb5-25cd-4c54-b452-6a0d6acc7500
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Read the Tally Intervals for a Configuration Manager Site
In Configuration Manager, you can read the available tally intervals for a site by inspecting the site control file `SMS_COMPONENT_STATUS_SUMMARIZER` object `Summary_Intervals` embedded property list.  

 You use tally intervals for querying component (`SMS_ComponentSummarizer`) and site detail (`SMS_SiteDetailSummarizer`) summarizer classes. For more information, see [About Configuration Manager Status Summarizers](../../../../develop/core/servers/manage/about-configuration-manager-status-summarizers.md).  

### To read the tally intervals for a site  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../../understand/sms-provider-fundamentals.md).  

2.  Perform a query for the site's SMS_COMPONENT_STATUS_SUMMARIZER property lists  

3.  In the results from step two, search for the Summary_Intervals embedded property list.  

4.  Display the contents of the embedded property list.  

## Example  
 The following example method returns a [SMS_TaskSequence](../../../reference/osd/sms_tasksequence-server-wmi-class.md) object after importing it from the supplied XML.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub ShowSiteTallyIntervals(connection, siteCode)  

    Dim SCIComponent              'SMS_SCI_Component class  
    Dim SCIComponentSet         'Enumeration of SMS_SCI_Component  
    Dim query   
    Dim i   
    Dim vProperty                     'Embedded property  

    query = "SELECT PropLists FROM SMS_SCI_Component " & _  
            "WHERE ComponentName = 'SMS_COMPONENT_STATUS_SUMMARIZER' " & _  
            "AND SiteCode = '" + siteCode + "'"  

    ' You do not need to get a copy of the site control file just to read it.  
    Set SCIComponentSet = connection.ExecQuery(query)  

    ' The query returns only one instance.  
    For Each SCIComponent In SCIComponentSet  
        For Each vProperty In SCIComponent.PropLists  
            If vProperty.PropertyListName = "Summary_Intervals" Then  
                For i = 0 To UBound(vProperty.Values)  
                    WScript.Echo vProperty.Values(i)   
                Next  
            End If  
        Next  
    Next  
 End Sub  
```  

```c#  
public void ShowSiteTallyIntervals(WqlConnectionManager connection, string siteCode)  
{  
    try  
    {  
        // Query for the site's site control file SMS_COMPONENT_STATUS_SUMMARIZER property lists.  
        IResultObject query =   
            connection.QueryProcessor.ExecuteQuery("SELECT PropLists FROM SMS_SCI_Component " +  
            "WHERE ComponentName = 'SMS_COMPONENT_STATUS_SUMMARIZER' " +  
            "AND SiteCode = '" + siteCode + "'");  

        foreach (IResultObject r in query)  
        {  
            // Get the summary intervals and display them.  
          if (r.EmbeddedPropertyLists.ContainsKey("Summary_Intervals"))  
            {  
                Console.WriteLine(r.EmbeddedPropertyLists["Summary_Intervals"]["PropertyListName"].StringValue);  
                foreach (string value in r.EmbeddedPropertyLists["Summary_Intervals"]["Values"].StringArrayValue)  
                {  
                    Console.WriteLine(value);  
                }  
            }  
            else  
            {  
                Console.WriteLine("Not found");  
                return;  
            }  
        }  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to tally intervals: " + e.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: [WqlConnectionManager](../../understand/managed-sms-provider-fundamentals-in-configuration-manager.md#wqlconnectionmanager)<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../../understand/sms-provider-fundamentals.md).|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|A valid Configuration Manager site code.|  

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
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [About status messages](about-configuration-manager-status-messages.md)
 [About Configuration Manager Tally Intervals](../../../../develop/core/servers/manage/about-configuration-manager-tally-intervals.md)   
 [About Configuration Manager Status Summarizers](../../../../develop/core/servers/manage/about-configuration-manager-status-summarizers.md)
