---
title: "Perform a Synchronous Query by Using System.Management"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 015c0e0a-3ef1-4c12-8796-7dc184ea584c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Perform a Synchronous Query by Using System.Management
To synchronously query the System Center Configuration Manager client Windows Management Instrumentation (WMI), you use a `ManagementObjectSearcher` object.  

 To read a lazy property from a System Center Configuration Manager object that is returned in a query, you get the object instance, which in turn retrieves any lazy object properties from the SMS Provider.  

### To perform a synchronous query  

1.  Set up a connection to the System Center Configuration Manager client WMI namespace. For more information, see [How to Connect to the Configuration Manager Client WMI Namespace by Using System.Management](../../../../develop/core/clients/programming/how-to-connect-to-the-client-wmi-namespace.md).  

2.  Create a ManagementObjectSearcher collection, and specify a WQL query.  

3.  Iterate through the ManagementObjectSearcher collection to view the ManagementObject for each WMI object that is returned by the query.  

## Example  
 The following C# code example queries for the single `SMS_Client` object that is on a System Center Configuration Manager client.  

 For information about calling the sample code, see [How to Call a WMI Class Method by Using System.Management](../../../../develop/core/clients/programming/how-to-call-a-wmi-class-method-by-using-system.management.md).  

```c#  

public void QueryObjects(ManagementScope scope)  
{  
    try  
    {  
        ManagementObjectSearcher s = new ManagementObjectSearcher  
            ((scope), new WqlObjectQuery("SELECT * FROM sms_client"));  

        foreach (ManagementObject o in s.Get())  
        {  
            // There is only one instance of SMS_Client, so this should enumerate only once.  
            Console.WriteLine("Client version: " + o["ClientVersion"].ToString());  
        }  
    }  
    catch (System.Management.ManagementException e)  
    {  
        Console.WriteLine("Failed to make query: ", e.Message);  
        throw;  
    }  
}  
```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`scope`|`ManagementScope`|Represents a scope (namespace) for management operations.|  

## Compiling the Code  

### Namespaces  
 System.  

 System.Management.  

### Assembly  
 System.Management.  

## Robust Programming  
 The exception that can be raised is [System.Management.ManagementException](https://msdn.microsoft.com/library/system.management.managementexception.aspx).  

## See Also  
 [About Configuration Manager WMI Programming](../../../../develop/core/clients/programming/about-configuration-manager-wmi-programming.md)   
 [How to Call a WMI Class Method by Using System.Management](../../../../develop/core/clients/programming/how-to-call-a-wmi-class-method-by-using-system.management.md)   
 [How to Connect to the Configuration Manager Client WMI Namespace by Using System.Management](../../../../develop/core/clients/programming/how-to-connect-to-the-client-wmi-namespace.md)   
 [How to Perform an Asynchronous Query by Using System.Management](../../../../develop/core/clients/programming/how-to-perform-an-asynchronous-query-by-using-system.management.md)   
 [How to Read a WMI Object Using System.Management](../../../../develop/core/clients/programming/how-to-read-a-wmi-object-by-using-system.management.md)
