---
title: "Create a Schedule Token"
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
ms.assetid: 27028a26-7ec2-4f0c-842f-1c7a6255066bsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create a Schedule Token
You create a schedule token, in System Center Configuration Manager, by creating and populating an instance of the appropriate `SMS_ST_` schedule token class. `SMS_ST` schedule classes are child classes of the `SMS_ScheduleToken` class and handle the scheduling of events with differing frequencies such as daily, weekly and monthly.  

 The [SMS_ScheduleMethods](../../../develop/reference/core/servers/configure/sms_schedulemethods-server-wmi-class.md) Windows Management Instrumentation (WMI) class, and the corresponding [ReadFromString](../../../develop/reference/core/servers/configure/readfromstring-method-in-class-sms_schedulemethods.md) and [WriteToString](../../../develop/reference/core/servers/configure/writetostring-method-in-class-sms_schedulemethods.md) methods are used to decode and encode schedule tokens into and from an interval string. The interval strings can then be used to set schedule properties when defining or modifying objects. An example of this can be seen in the [How to Create a Maintenance Window for a Collection](../../../develop/core/servers/configure/how-to-create-a-maintenance-window-for-a-collection.md) topic where the `ServiceWindowSchedules` property is configured.  

### To create a schedule token and convert it to an interval string  

1.  Create a schedule token object by using one of the [SMS_ScheduleToken](../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md) child classes. This example uses the [SMS_ST_RecurInterval](../../../develop/reference/core/servers/configure/sms_st_recurinterval-server-wmi-class.md) class.  

2.  Populate the properties of the new schedule token object.  

3.  Convert the schedule token object to an interval string by using the `SMS_ScheduleMethods` class and `WriteToString` method.  

4.  Use the interval string to populate an object's schedule properties, as needed.  

## Example  
 The following example method shows how to create a schedule token by creating and populating an instance of the `SMS_ST_RecurInterval` schedule token class. In addition, the example shows how to convert the schedule to an interval string by using the `SMS_ScheduleMethods` class and `WriteToString` method.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub CreateDailyRecurringScheduleString(connection,   _  
                                       hourDuration, _  
                                       daySpan,      _   
                                       startTime,    _  
                                       isGmt)  

    ' Create a new recurring interval schedule object.  
    ' Note: There are several types of schedule classes available, each defines a different type of schedule.  
    Set recurInterval = connection.Get("SMS_ST_RecurInterval").SpawnInstance_  

    ' Populate the schedule properties.  
    recurInterval.DayDuration = 0  
    recurInterval.HourDuration = hourDuration  
    recurInterval.MinuteDuration = 0  
    recurInterval.DaySpan = daySpan  
    recurInterval.HourSpan = 0  
    recurInterval.MinuteSpan = 0  
    recurInterval.StartTime = startTime  
    recurInterval.IsGMT = isGmt  

    ' Call WriteToString method to decode the schedule token.  
    ' Note: The initial parameter of the WriteToString method requires an array.   
    Set clsScheduleMethod = connection.Get("SMS_ScheduleMethods")  
    clsScheduleMethod.WriteToString Array(recurInterval), scheduleString  

    ' Output schedule token as an interval string.  
    WScript.Echo "Schedule Token Interval String: " & scheduleString  

End Sub  
```  

```c#  

public void CreateDailyRecurringScheduleToken(WqlConnectionManager connection,  
                                              int hourDuration,   
                                              int daySpan,  
                                              string startTime,  
                                              bool isGmt)    
{  
    try  
    {                  
        // Create a new recurring interval schedule object.  
        // Note: There are several types of schedule classes available, each defines a different type of schedule.  
        IResultObject recurInterval = connection.CreateEmbeddedObjectInstance("SMS_ST_RecurInterval");  

        // Populate the schedule properties.  
        recurInterval["DayDuration"].IntegerValue = 0;  
        recurInterval["HourDuration"].IntegerValue = hourDuration;  
        recurInterval["MinuteDuration"].IntegerValue = 0;  
        recurInterval["DaySpan"].IntegerValue = daySpan;  
        recurInterval["HourSpan"].IntegerValue = 0;  
        recurInterval["MinuteSpan"].IntegerValue = 0;  
        recurInterval["StartTime"].StringValue = startTime;         
        recurInterval["IsGMT"].BooleanValue = isGmt;  

        // Creating array to use as a parameters for the WriteToString method.  
        List<IResultObject> scheduleTokens = new List<IResultObject>();  
        scheduleTokens.Add(recurInterval);  

        // Creating dictionary object to pass parameters to the WriteToString method.  
        Dictionary<string, object> inParams = new Dictionary<string, object>();  
        inParams["TokenData"] = scheduleTokens;  

        // Initialize the outParams object.  
        IResultObject outParams = null;  

        // Call WriteToString method to decode the schedule token.  
        outParams = connection.ExecuteMethod("SMS_ScheduleMethods", "WriteToString", inParams);  

        // Output schedule token as an interval string.  
        // Note: The return value for this method is always 0, so this check is just best practice.  
        if (outParams["ReturnValue"].IntegerValue == 0)  
        {  
            Console.WriteLine("Schedule Token Interval String: " + outParams["StringData"].StringValue);  
        }  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);  
    }  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`hourDuration`|-   Managed: `Integer`<br />-   VBScript: `Integer`|Number of hours during which the scheduled action occurs. Allowable values are in the range 0-23. The default value is 0, indicating no duration.|  
|`daySpan`|-   Managed: `Integer`<br />-   VBScript: `Integer`|Number of days spanning schedule intervals. Allowable values are in the range 0-31. The default value is 0.|  
|`startTime`|-   Managed: `String` (DateTime)<br />-   VBScript: `String` (DateTime)|Date and time when the scheduled action takes place. The default value is "19700201000000.000000+***". This is the format in which (WMI) CIM DATETIME values are stored.|  
|`isGmt`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|`true` if the time is in Coordinated Universal Time (UTC). The default value is `false`, for local time.|  

## Compiling the Code  
 The C# example has the following compilation requirements:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 microsoft.configurationmanagement.managmentprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [System Center Configuration Manager Software Development Kit](../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Scheduling Server WMI Classes](../../../develop/reference/core/servers/configure/scheduling-server-wmi-classes.md)   
 [SMS_ST_NonRecurring Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_nonrecurring-server-wmi-class.md)   
 [SMS_ST_RecurInterval Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_recurinterval-server-wmi-class.md)   
 [SMS_ST_RecurMonthlyByDate Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_recurmonthlybydate-server-wmi-class.md)   
 [SMS_ST_RecurMonthlyByWeekday Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_recurmonthlybyweekday-server-wmi-class.md)   
 [SMS_ST_RecurWeekly Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_recurweekly-server-wmi-class.md)   
 [SMS_ScheduleMethods Server WMI Class](../../../develop/reference/core/servers/configure/sms_schedulemethods-server-wmi-class.md)   
 [ReadFromString Method in Class SMS_ScheduleMethods](../../../develop/reference/core/servers/configure/readfromstring-method-in-class-sms_schedulemethods.md)   
 [WriteToString Method in Class SMS_ScheduleMethods](../../../develop/reference/core/servers/configure/writetostring-method-in-class-sms_schedulemethods.md)
