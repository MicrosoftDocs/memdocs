---
title: "Reset the Software Inventory Cache"
titleSuffix: "Configuration Manager"
description: "Learn how to reset the software inventory cache by connecting to the inventory agent namespace and deleting the inventory action status instance for software inventory."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: fbb32170-234c-44f2-80b8-51285790e8a4
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3


---
# How to Reset the Software Inventory Cache
In Configuration Manager, you reset the software inventory cache by connecting to the inventory agent namespace and deleting the inventory action status instance for software inventory.  

### To reset the software inventory cache  

1.  Connect to the inventory agent namespace (root\ccm\invagt).  

2.  Delete the inventory action status instance for software inventory ({00000000-0000-0000-0000-000000000002}).  

## Example  
 The following example method shows how to reset the software inventory cache by connecting to the inventory agent namespace and deleting the inventory action status instance for software inventory.  

 For information about calling the sample code, see [How to Call a Configuration Manager Object Class Method by Using WMI](../../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-wmi.md)  

```vbs  

Sub ResetSoftwareInventoryCache()  

    ' Get a connection to the "root\ccm\invagt" namespace.  
    Dim locator  
    Set locator = CreateObject("WbemScripting.SWbemLocator")  
    Dim services  
    Set services = locator.ConnectServer( , "root\ccm\invagt")  

    ' Delete the specified InventoryActionStatus instance.  
    services.Delete "InventoryActionStatus.InventoryActionID='{00000000-0000-0000-0000-000000000002}'"        

    ' Display message.  
    wscript.echo "Reset Software Inventory cache."  

End Sub  

```  

```c#  

public void ResetSoftwareInventoryCache()  
{  
    try  
    {  
        // Define the scope (namespace).  
        ManagementScope inventoryAgentScope = new ManagementScope(@"root\ccm\invagt");  

        // Load the class that you want to work with.  
        ManagementClass inventoryClass = new ManagementClass(inventoryAgentScope.Path.Path, "InventoryActionStatus", null);  

        // Query the class for the InventoryActionID object (create query, create searcher object, execute query).  
        ObjectQuery query = new ObjectQuery("SELECT * FROM InventoryActionStatus WHERE InventoryActionID = '{00000000-0000-0000-0000-000000000002}'");  
        ManagementObjectSearcher searcher = new ManagementObjectSearcher(inventoryAgentScope, query);  
        ManagementObjectCollection queryResults = searcher.Get();  

        // Enumerate the collection to get to the result (there should only be one item returned from the query).  
        foreach (ManagementObject result in queryResults)  
        {  
            // Display message and delete the object.  
            Console.WriteLine("Resetting Software Inventory cache.");  
            result.Delete();  
        }  
    }  

    catch (System.Management.ManagementException ex)  
    {  
        Console.WriteLine("Failed to run action. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

## Compiling the Code  
 This C# example requires:  

### Namespaces  
 System.Management  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [Configuration Manager Software Development Kit](../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [About Configuration Manager Inventory](../../../../develop/core/clients/inventory/about-configuration-manager-inventory.md)   
