---
title: "Call a WMI Class Method by Using System.Management"
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
ms.assetid: 051ecc47-dfef-4586-9b50-abde4148bfffsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Call a WMI Class Method by Using System.Management
To call a client Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, you call the `InvokeMethod` of the WMI class's `ManagementClass`.  

### To call a WMI class method  

1.  Set up a connection to the System Center Configuration Manager client WMI namespace. For more information, see [How to Connect to the Configuration Manager Client WMI Namespace by Using System.Management](../../../../develop/core/clients/programming/how-to-connect-to-the-client-wmi-namespace.md).  

2.  Create a `ManagementClass` by using the `ManagementScope` path you obtain in step one, and also the name of the class you want to call a method on.  

3.  Create a `ManagementBaseObject` and specify any in parameters for the method.  

4.  Call the method by using the `ManagementClass` object `InvokeMethod` method.  

5.  Using the returned `ManagementBaseObject`, view the returned parameters.  

## Example  
 The following C# code example calls the `ISmsClient::GetAssignedSite` method to get the current assigned site for the client. It then sets the assigned site back to the same value using the `ISmsClient::SetAssignedSite` method.  

 For information about calling the sample code, see [How to Call a WMI Class Method by Using System.Management](../../../../develop/core/clients/programming/how-to-call-a-wmi-class-method-by-using-system.management.md).  

```c#  

public void CallMethod(ManagementScope scope)  
{  
    try// Get the client's SMS_Client class.  
    {  
        ManagementClass cls = new ManagementClass(scope.Path.Path, "sms_client", null);  

        // Get current site code.  
        ManagementBaseObject outSiteParams = cls.InvokeMethod("GetAssignedSite", null, null);  

        // Display current site code.  
        Console.WriteLine(outSiteParams["sSiteCode"].ToString());  

        // Set up current site code as input parameter for SetAssignedSite.  
        ManagementBaseObject inParams = cls.GetMethodParameters("SetAssignedSite");  
        inParams["sSiteCode"] = outSiteParams["sSiteCode"].ToString();  

        // Assign the Site code.  
        ManagementBaseObject outMPParams = cls.InvokeMethod("SetAssignedSite", inParams, null);  
    }  
    catch (ManagementException e)  
    {  
        throw new Exception("Failed to execute method", e);  
    }  
}  

```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`scope`|-   `ManagementScope`|A valid connection to the client WMI provider. The path is root\ccm.|  

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
 [How to Read a WMI Object by Using System.Management](../../../../develop/core/clients/programming/how-to-read-a-wmi-object-by-using-system.management.md)
