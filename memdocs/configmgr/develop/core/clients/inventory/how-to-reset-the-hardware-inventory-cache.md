---
title: "Reset the Hardware Inventory Cache"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, you reset the hardware inventory cache by connecting to the inventory agent namespace and deleting the inventory action status instance for hardware inventory."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 5dbda4e2-ce2b-4fa4-9573-aad2087d4477
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Reset the Hardware Inventory Cache
In Configuration Manager, you reset the hardware inventory cache by connecting to the inventory agent namespace and deleting the inventory action status instance for hardware inventory.  

### To reset the hardware inventory cache  

1.  Connect to the inventory agent namespace (root\ccm\invagt).  

2.  Delete the inventory action status instance for hardware inventory ({00000000-0000-0000-0000-000000000001}).  

## Example  
 The following example method shows how to reset the hardware inventory cache by connecting to the inventory agent namespace and deleting the inventory action status instance for hardware inventory.  

 For information about calling the sample code, see [How to Call a Configuration Manager Object Class Method by Using WMI](../../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-wmi.md)  

```vbs  

Sub ResetHardwareInventoryCache()  

     ' Get a connection to the "root\ccm\invagt" namespace.  
    Dim locator  
    Set locator = CreateObject("WbemScripting.SWbemLocator")  
    Dim services  
    Set services = locator.ConnectServer( , "root\ccm\invagt")     

    ' Delete the specified InventoryActionStatus instance.  
    services.Delete "InventoryActionStatus.InventoryActionID='{00000000-0000-0000-0000-000000000001}'"        

    ' Display message.  
    wscript.echo "Reset Hardware Inventory cache."  

End Sub  

```  

```c#  

// How to Reset the Hardware Inventory Cache  
public void ResetHardwareInventoryCache()  
{  
    try  
    {  
        // Define the scope (namespace).  
        ManagementScope inventoryAgentScope = new ManagementScope(@"root\ccm\invagt");  

        // Load the class that you want to work with.  
        ManagementClass inventoryClass = new ManagementClass(inventoryAgentScope.Path.Path, "InventoryActionStatus", null);  

        // Query the class for the InventoryActionID object (create query, create searcher object, execute query).  
        ObjectQuery query = new ObjectQuery("SELECT * FROM InventoryActionStatus WHERE InventoryActionID = '{00000000-0000-0000-0000-000000000001}'");  
        ManagementObjectSearcher searcher = new ManagementObjectSearcher(inventoryAgentScope, query);  
        ManagementObjectCollection queryResults = searcher.Get();  

        // Enumerate the collection to get to the result (there should only be one item returned from the query).  
        foreach (ManagementObject result in queryResults)  
        {  
            // Display message and delete the object.  
            Console.WriteLine("Resetting Hardware Inventory cache.");  
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
