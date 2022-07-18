---
title: "Clear a PXE Advertisement for a Resource"
titleSuffix: "Configuration Manager"
description: "To clear a PXE advertisement for a Configuration Manager resource, call the SMS_Collection object ClearLastNBSAdvForMachines method."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 29ad0de3-fd1a-4a22-b5ac-61a762a8c1a6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Clear a PXE Advertisement for a Configuration Manager Resource
To clear a PXE advertisement for a Configuration Manager resource, you call the [SMS_Collection](../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) object [ClearLastNBSAdvForMachines](../../develop/reference/core/clients/collections/clearlastnbsadvformachines-method-in-class-sms_collection.md) method.  

 Clearing PXE advertisement is used to re-advertise a mandatory advertisement that is enabled for a PXE device or assigned to a collection. For information about clearing the PXE advertisement for a collection, see [How to Clear a PXE Advertisement For a Configuration Manager Collection](../../develop/osd/how-to-clear-a-pxe-advertisement-for-a-configuration-manager-collection.md).  

 Clearing a PXE advertisement forces the PXE server to re-evaluate the mandatory advertisement that a PXE device must execute on the next PXE boot. It is most often used when the last advertisement that was executed failed or when the advertisement must be re-run.  

### To clear a PXE advertisement for a resource  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../core/understand/sms-provider-fundamentals.md).  

2.  Create the `ClearLastNBSAdvForMachines` method resource identifier array for the method parameters.  

3.  Call the `ClearLastNBSAdvForMachines` method to clear the PXE advertisement for the resource.  

## Example  
 The following example clears the PXE advertisement for the resource identified by the `resourceID` parameter.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub ClearPxeAdvertisementResource(connection,resourceID)  

    On Error Resume Next  

    Dim resources  
    Dim InParams  

    ' Set up the Resource array parameter.  
    resources = Array(1)  
    resources(0) = resourceID  

    Set InParams = connection.Get("SMS_Collection").Methods_("ClearLastNBSAdvForMachines").InParameters.SpawnInstance_  
    InParams.ResourceIDs = resources  

    connection.ExecMethod "SMS_Collection","ClearLastNBSAdvForMachines", InParams  

    if Err.number <> 0 Then  
        WScript.Echo "Failed to clear PXE advertisement for resource: " & resourceID  
        Exit Sub  
    End If  

End Sub  

```  

```c#  
public void ClearPxeAdvertisementResource(WqlConnectionManager connection, int resourceID)  
{  
    try  
    {  
        List<int> resourceIDs = new List<int>();  
        Dictionary<string, object> inParams = new Dictionary<string, object>();  

        resourceIDs.Add(resourceID);  
        inParams.Add("ResourceIDs", resourceIDs.ToArray());  

        IResultObject outParams = connection.ExecuteMethod("SMS_Collection","ClearLastNBSAdvForMachines",inParams);  

        if (outParams == null || outParams["StatusCode"].IntegerValue != 0)  
        {  
            Console.WriteLine  
                ("Failed to clear PXE advertisement for resource " + resourceID);  
            return;  
        }  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to PXE advertisement " + e.Message);  
    }  
}  
```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`resourceID`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The resource identifier. You can obtain this from the [SMS_Resource](../../develop/reference/core/clients/manage/sms_resource-server-wmi-class.md) class `ResourceId` property.|  

## Compiling the Code  
 The C# example has the following compilation requirements:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [How to Clear a PXE Advertisement For a Configuration Manager Collection](../../develop/osd/how-to-clear-a-pxe-advertisement-for-a-configuration-manager-collection.md)   
 [About image management](about-operating-system-deployment-image-management.md)
