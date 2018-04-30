---
title: "Enable or Disable a Windows Driver"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c13462bf-4652-46c4-9f26-818951bb7fe0
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Enable or Disable a Windows Driver in Configuration Manager
You enable or disable a Windows driver in the operating system deployment driver catalog, in System Center Configuration Manager, by setting the `IsEnabled` property of the [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) object. A driver can be disabled to prevent it from being installed by the Auto Apply Driver action in a task sequence.  

### To enable or disable a Windows driver  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the `SMS_Driver` object for the driver you want enable or disable.  

3.  Set the `IsEnabled` property to `true` to enable the driver, or to `false` to disable the driver.  

4.  Commit the `SMS_Driver` object changes.  

## Example  
 The following example method enables or disables a driver depending on the value of the `enableDriver` parameter.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub EnableDriver(connection,driverID,vEnableDriver)  

        ' Get the driver.  
        Set driver = connection.Get("SMS_Driver.CI_ID=" & driverID)  

        ' Set the flag.  
        driver.IsEnabled=vEnableDriver  

        ' Commit changes.  
        driver.Put_  

End Sub  
```  

```c#  
public void EnableDriver(  
    WqlConnectionManager connection,   
    int driverID,   
    bool enableDriver)  
{  
    try  
    {  
        // Get the driver.  
        IResultObject driver = connection.GetInstance("SMS_Driver.CI_ID=" + driverID);  

        // Set the flag.  
        driver["IsEnabled"].BooleanValue = enableDriver;  

        // Commit the changes.  
        driver.Put();  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed: " + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`driverID`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The Windows driver identifier available in `SMS_Driver.CI_ID`.|  
|`enableDriver`|-   Managed: `String`<br />-   VBScript: `String`|Flag to enable or disable the driver.<br /><br /> `true` - The driver is enabled.<br /><br /> `false` -  The driver is disabled.|  

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
