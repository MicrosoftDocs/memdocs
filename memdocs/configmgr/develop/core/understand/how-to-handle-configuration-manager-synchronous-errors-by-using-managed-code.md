---
title: "Handle Synchronous Errors by Using Managed Code"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 70b565ae-76c1-472c-8988-be24dd3e3644
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Handle Configuration Manager Synchronous Errors by Using Managed Code
To handle a Configuration Manager error that is raised in a synchronous query, you catch the [SmsQueryException](/previous-versions/system-center/developer/cc147436(v=msdn.10)) exception. Because this exception is also caught by SMS_Exception], you can catch it and the [SmsConnectionException](/previous-versions/system-center/developer/cc147431(v=msdn.10)) exception in the same catch block.  

 If the exception that is caught in an SMS_Exception is an [SmsQueryException](/previous-versions/system-center/developer/cc147436(v=msdn.10)), you can use it to get to the underlying `__ExtendedException` or `SMS_ExtendedException`. Because the managed SMS Provider library does not wrap these exceptions, you will need to use the System.Management namespace [ManagementException](/dotnet/api/system.management.managementexception) object to access them.  

> [!NOTE]
>  For clarity, most examples in this documentation simply re-throw exceptions. You can replace them with the following example if you want more informative exception information.  

### To handle a synchronous query error  

1.  Write code to access the SMS Provider.  

2.  Use the following example code to catch the [SmsQueryException](/previous-versions/system-center/developer/cc147436(v=msdn.10)) and [SmsConnectionException](/previous-versions/system-center/developer/cc147431(v=msdn.10)) exceptions.  

## Example  
 The following C# example function attempts to open a nonexistent `SMS_Package` package. In the exception handler, the code determines what type of error has been raised and displays its information.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```c#  
public void ExerciseException(WqlConnectionManager connection)  
{  
    try  
    {  

        IResultObject package = connection.GetInstance(@"SMS_Package.PackageID='UNKNOWN'");  
        Console.WriteLine("Package Name: " + package["Name"].StringValue);  
        Console.WriteLine("Package Description: " + package["Description"].StringValue);  

    }  
    catch (SmsException e)  
    {  
        if (e is SmsQueryException)  
        {  
            SmsQueryException queryException = (SmsQueryException)e;  
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
        if (e is SmsConnectionException)  
        {  
            Console.WriteLine("There was a connection error :" + ((SmsConnectionException)e).Message);  
            Console.WriteLine(((SmsConnectionException)e).ErrorCode);  
        }  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   `WqlConnectionManager`|A valid connection to the provider.|  

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
 [How to Handle Configuration Manager Asynchronous Errors by Using Managed Code](../../../develop/core/understand/how-to-handle-configuration-manager-asynchronous-errors-by-using-managed-code.md)
