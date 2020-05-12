---
title: "Handle Asynchronous Errors by Using Managed Code"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 1a37a005-07cd-476e-a744-fa345f3232c7
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# How to Handle Configuration Manager Asynchronous Errors by Using Managed Code
To handle a Configuration Manager error that is raised during an asynchronous query, you test the `RunWorkerCompletedEventArgs` parameter [Error](https://msdn.microsoft.com/library/t1yswz5k.aspx) Exception property that is passed to the [SmsBackgroundWorker.QueryProcessorCompleted](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsbackgroundworker.queryprocessorcompleted.aspx) event handler. If [Error](https://msdn.microsoft.com/library/t1yswz5k.aspx) is not `null`, an exception has occurred and you use [Error](https://msdn.microsoft.com/library/t1yswz5k.aspx) to discover the cause.  

 If [Error](https://msdn.microsoft.com/library/t1yswz5k.aspx) is an [SmsQueryException](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsqueryexception.aspx), you can use it to get to the underlying `__ExtendedException` or `SMS_ExtendedException`. Because the managed SMS Provider library does not wrap these exceptions you will need to use the System.Management namespace [ManagementException](https://docs.microsoft.com/dotnet/api/system.management.managementexception) object to access them.  

### To handle an asynchronous query error  

1.  Create an asynchronous query.  

2.  In the asynchronous query [SmsBackgroundWorker.QueryProcessorCompleted](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsbackgroundworker.queryprocessorcompleted.aspx) event handler, implement the code in the following example.  

3.  Run the asynchronous query. To test the exception handler, pass a badly formed query string such as `Select & from &&&` to the [QueryProcessorBase.ProcessQuery](https://msdn.microsoft.com/library/cc146295.aspx) method.  

## Example  
 The following example implements a [SmsBackgroundWorker.QueryProcessorCompleted](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsbackgroundworker.queryprocessorcompleted.aspx) event handler.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```c#  
void bw1_QueryProcessorCompleted(object sender, RunWorkerCompletedEventArgs e)  
{  
    if (e.Error != null)  
    {  
        Console.WriteLine("There was an Error");  
        if (e.Error is SmsQueryException)  
        {  
            SmsQueryException queryException = (SmsQueryException)e.Error;  
            Console.WriteLine(queryException.Message);  

            // Get either the __ExtendedStatus or SMS_ExtendedStatus object and display various properties.  
            ManagementException mgmtExcept = queryException.InnerException as ManagementException;  

            if (mgmtExcept != null)  
            {  
                if (string.Equals(mgmtExcept.ErrorInformation.ClassPath.ToString(), "SMS_ExtendedStatus", StringComparison.OrdinalIgnoreCase) == true)  
                {  
                    Console.WriteLine("Configuration Manager provider exception");  
                }  

                else if (string.Equals(mgmtExcept.ErrorInformation.ClassPath.ToString(), "__ExtendedStatus", StringComparison.OrdinalIgnoreCase) == true)  
                {  
                    Console.WriteLine("WMI exception");  
                }  
                Console.WriteLine(mgmtExcept.ErrorCode.ToString());  
                Console.WriteLine(mgmtExcept.ErrorInformation["ParameterInfo"].ToString());  
                Console.WriteLine(mgmtExcept.ErrorInformation["Operation"].ToString());  
                Console.WriteLine(mgmtExcept.ErrorInformation["ProviderName"].ToString());  
            }  

        }  
        if (e.Error is SmsConnectionException)  
        {  
            Console.WriteLine("There was a connection error :" + ((SmsConnectionException)e.Error).Message);  
            Console.WriteLine(((SmsConnectionException)e.Error).ErrorCode);  
        }  
    }  

    Console.WriteLine("Done...");  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`sender`|-   `Object`|The source of the event.|  
|`e`|-   `RunWorkerCompletedEventArgs`|The event data.<br /><br /> For more information, see [RunWorkerCompletedEventArgs Class](/dotnet/api/system.componentmodel.runworkercompletedeventargs).|  

## Compiling the Code  
 This C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

 System.Management  

 System.ComponentModel  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

 System.Management  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## See Also  
 [About errors](about-configuration-manager-errors.md)
