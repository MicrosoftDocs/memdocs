---
title: "How to Connect to the Configuration Manager Client WMI Namespace by Using System.Management"
ms.custom: ""
ms.date: "2016-09-20"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "System Center Configuration Manager (current branch)"
ms.assetid: dc9ff31d-249a-40e6-83d3-db2e7bd1d6db
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Connect to the Configuration Manager Client WMI Namespace by Using System.Management
To connect to the Configuration Manager client Windows Management Instrumentation (WMI) provider, you create a `ManagementScope` object in the \\\Client\root\ccm namespace.  
  
 You use the `ManagementScope` object to read and query WMI objects. For example, [How to Read a WMI Object Using System.Management](../../../../develop/core/clients/programming/how-to-perform-an-asynchronous-query-by-using-managed-code.md).  
  
### To connect to the Configuration Manager client WMI provider  
  
1.  In Visual Studio, create a new Visual C# Console Project.  
  
2.  Add a reference to the System.Management assembly.  
  
3.  In the C# source code, add a reference to the System.Management namespace with the following code.  
  
4.  `using System.Management;`  
  
5.  Create a new class and add the following connection example code.  
  
## Example  
 The following C# code example creates and returns a `ManagementScope` object on the root\ccm namespace.  
  
 For information about calling the sample code, see [How to Call a WMI Class Method by Using System.Management](../../../../develop/core/clients/programming/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md).  
  
```c#  
  
public ManagementScope Connect()  
{  
    try  
    {  
        return new ManagementScope(@"root\ccm");  
    }  
    catch (System.Management.ManagementException e)  
    {  
        Console.WriteLine("Failed to connect", e.Message);  
        throw;  
    }  
}  
  
```  
  
## Compiling the Code  
  
### Namespaces  
 System  
  
 System.Management  
  
### Assembly  
 System.Management.dll  
  
## Robust Programming  
 The exception that can be raised is [System.Management.ManagementException](assetId:///System.Management.ManagementException?qualifyHint=False&autoUpgrade=True).  
  
## See Also  
 [About Configuration Manager WMI Programming](../../../../develop/core/clients/programming/how-to-configure-advertised-programs-client-agent-settings.md)   
 [How to Call a WMI Class Method by Using System.Management](../../../../develop/core/clients/programming/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Perform an Asynchronous Query by Using System.Management](../../../../develop/core/clients/programming/how-to-enable-or-disable-the-advertised-programs-client-agent.md)   
 [How to Perform a Synchronous Query by Using System.Management](../../../../develop/core/clients/programming/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Read a WMI Object by Using System.Management](../../../../develop/core/clients/programming/how-to-perform-an-asynchronous-query-by-using-managed-code.md)