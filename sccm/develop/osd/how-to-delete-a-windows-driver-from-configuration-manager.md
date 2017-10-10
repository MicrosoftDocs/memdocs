---
title: "Delete a Windows Driver"
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
ms.assetid: 74926652-9b74-47cd-a0b4-2b93610b11f6searchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Delete a Windows Driver from Configuration Manager
You delete a Windows driver from the operating system deployment driver catalog, in System Center Configuration Manager, by deleting its [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) object. When you delete a driver, its definition is deleted, and it is no longer matched by the apply driver action task sequences. However, if the content associated with the driver was added to a driver package, or if the driver was added to a boot image package, the content remains there until the packages are updated.  

### To delete a Windows driver  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the `SMS_Driver` object for the driver that you want to delete.  

3.  Delete the `SMS_Driver` object.  

## Example  
 The following example method deletes a driver identified by its `CI_ID` property value.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub DeleteDriver(connection,driverID)  

        ' Get the driver.  
        Set driver = connection.Get("SMS_Driver.CI_ID=" & driverID)  

        ' Commit changes.  
        driver.Delete_  

End Sub  
```  

```c#  

public void DeleteDriver(WqlConnectionManager connection,   
                         int driverID)  
{  
    try  
    {  
        // Get the driver.  
        IResultObject driver = connection.GetInstance("SMS_Driver.CI_ID=" + driverID);  

        // Delete the driver.  
        driver.Delete();  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to delete driver: " + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed:`WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`driverID`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The Windows driver identifier available in `SMS_Driver.CI_ID`.|  

## Compiling the Code  
 This C# example requires:  

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
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [Operating System Deployment Driver Management](../../develop/osd/operating-system-deployment-driver-management.md)
