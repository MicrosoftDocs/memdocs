---
title: "Get the Unique Identifier Value for a Client"
titleSuffix: "Configuration Manager"
description: When you discover system resource data for a client, in Configuration Manager, you must specify the client's unique identifier value in the data discovery record (DDR).
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 5c2a9bd7-9a0f-439d-9238-5bad67a0ad58
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Get the Unique Identifier Value for a Client
When you discover system resource data for a client, in Configuration Manager, you must specify the client's unique identifier value in the data discovery record (DDR), such as:  

```  
DDRAddString("SMS Unique Identifier",  
             "GUID:12345678-1234-1234-1234-123456789012", 64,  
             ADDPROP_GUID | ADDPROP_KEY);  
```  

 The client's unique identifier can be found in Windows Management Instrumentation (WMI) at:  

```  
root\ccm:CCM_Client=@:ClientId  
```  

## Procedures  

#### To identify the client's unique identifier in WMI  

1.  Connect to the CCM namespace (root\ccm).  

2.  Load the `CCM_Client` class.  

3.  Enumerate through the objects in the `CCM_Client` class and display the unique identifier (ClientId).  

## Example  

### Description  
 The following example method shows how obtain the client's unique identifier from WMI by connecting to the CCM namespace, loading the `CCM_Client` class and getting the ClientId property.  

> [!IMPORTANT]
>  The following C# example requires the System.Management namespace.  

 For information about calling the sample code, see [How to Call a Configuration Manager Object Class Method by Using WMI](../../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-wmi.md)  

### Code  

```vbs  

Sub GetClientUniqueID()  

    ' Get a connection to the root\ccm namespace on the local system.  
    Set objWMIService = GetObject("winmgmts:\\.\root\ccm")  

    ' Get all objects in the CCM_Client class.  
    set allCCMClientObjects = objWMIService.ExecQuery("Select * from CCM_Client")  

    ' Loop through the available objects (only one) and display ClientId value.  
    For Each eachCCMClientObject in allCCMClientObjects  
       wscript.echo "ClientId (GUID): " & eachCCMClientObject.ClientId         
    Next   

End Sub  
```  

```c#  

public void GetClientUniqueID()  
{  
    try  
    {  
        // Define the scope (namespace) to connect to.  
        ManagementScope inventoryAgentScope = new ManagementScope(@"root\ccm");  

        // Load the class to work with (CCM_Client).  
        ManagementClass inventoryClass = new ManagementClass(inventoryAgentScope.Path.Path, "CCM_Client", null);  

        // Query the class for the objects (create query, create searcher object, execute query).  
        ObjectQuery query = new ObjectQuery("SELECT * FROM CCM_Client");  
        ManagementObjectSearcher searcher = new ManagementObjectSearcher(inventoryAgentScope, query);  
        ManagementObjectCollection queryResults = searcher.Get();  

        // Loop through the available objects (only one) and display the ClientId value.  

        foreach (ManagementObject result in queryResults)  
        {  
            Console.WriteLine("ClientId (GUID): " + result["ClientId"]);  
        }  
    }  

    catch (System.Management.ManagementException ex)  
    {  
        Console.WriteLine("Failed to get client ID (GUID). Error: " + ex.Message);  
        throw;  
    }  
}  

```  

### Comments  

## Compiling the Code  
 This C# example requires:  

#### Namespaces  
 System.Management  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [How to Call a WMI Class Method by Using System.Management](../../../../develop/core/clients/programming/how-to-call-a-wmi-class-method-by-using-system.management.md)
