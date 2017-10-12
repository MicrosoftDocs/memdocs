---
title: "Read a WMI Object by Using System.Management"
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
ms.assetid: 59065142-89c1-40f8-b4c0-83803650c06dsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Read a WMI Object by Using System.Management
To read a Configuration Manager client Windows Management Instrumentation (WMI) object, in System Center Configuration Manager, you use a `ManagementObject` object to read the WMI object.  

### To read a WMI object  

1.  Set up a connection to the Configuration Manager client WMI namespace. For more information, see [How to Connect to the Configuration Manager Client WMI Namespace by Using System.Management](../../../../develop/core/clients/programming/how-to-connect-to-the-client-wmi-namespace.md).  

2.  Create a `ManagementObject` object.  

3.  Create a `ManagementPath` object with the `ManagementScope` path you obtain from step one.  

4.  Assign the `ManagementPath` object to the `ManagementObject` path property.  

5.  Call the `ManagementObject` object Get method to get the object from the WMI provider.  

6.  Use the `ManagementObject` object to read the WMI provider object properties.  

## Example  
 The following C# code example gets the Configuration Manager client WMI object [SMS_Client](../../../../develop/reference/core/clients/client-classes/sms_client-client-wmi-class.md) object and displays its properties.  

 For information about calling the sample code, see [How to Call a WMI Class Method by Using System.Management](../../../../develop/core/clients/programming/how-to-call-a-wmi-class-method-by-using-system.management.md).  

```c#  

void ReadObject(ManagementScope scope)  
{  
    try  // Gets an instance of a CCM_InstalledComponent.  
    {  
        // Get the object.  
        ManagementObject obj = new ManagementObject();  
        ManagementPath path = new ManagementPath(scope.Path + ":CCM_InstalledComponent.Name='SMSClient'");  

        obj.Path = path;  
        obj.Get();  

        // Display a single property.  
        Console.WriteLine(obj["DisplayName"].ToString());  

        // Display all properties.  
        foreach (PropertyData property in obj.Properties)  
        {  
            Console.WriteLine(property.Name + " " + property.Value);  
        }  
    }  
    catch (ManagementException e)  
    {  
        Console.WriteLine("Failed to get component: " + e.Message);  
        throw;  
    }  
}  
```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`scope`|-   `ManagementScope`|The client management scope. The namespace should be root\ccm.|  

## Compiling the Code  

### Namespaces  
 System  

 System.Management  

### Assembly  
 System.Management  

## Robust Programming  
 The exception that can be raised is [System.Management.ManagementException](https://msdn.microsoft.com/library/system.management.managementexception.aspx).  

## See Also  
 [About Configuration Manager WMI Programming](../../../../develop/core/clients/programming/about-configuration-manager-wmi-programming.md)   
 [How to Call a WMI Class Method by Using System.Management](../../../../develop/core/clients/programming/how-to-call-a-wmi-class-method-by-using-system.management.md)   
 [How to Connect to the Configuration Manager Client WMI Namespace by Using System.Management](../../../../develop/core/clients/programming/how-to-connect-to-the-client-wmi-namespace.md)   
 [How to Perform an Asynchronous Query by Using System.Management](../../../../develop/core/clients/programming/how-to-perform-an-asynchronous-query-by-using-system.management.md)   
 [How to Perform a Synchronous Query by Using System.Management](../../../../develop/core/clients/programming/how-to-perform-a-synchronous-query-by-using-system.management.md)
