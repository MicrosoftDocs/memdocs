---
title: "Remove a Windows Driver from a Boot Image Package"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0d142253-1065-4b18-be64-d0513c7a3044
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Remove a Windows Driver from a Boot Image Package
In System Center Configuration Manager, you remove a Windows driver from an operating system deployment boot image package by removing it from the `ReferencedDrivers` property of the [SMS_BootImagePackage Server WMI Class](../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md) object.  

> [!NOTE]
>  The driver is not removed until the boot image package is refreshed and updated on the distribution points.  

### To remove a Windows driver from a boot image package  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the [SMS_BootImagePackage](../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md) object for the boot image package that contains the driver you want to remove.  

3.  Remove the driver from the `ReferencedDrivers` property. The driver is identified by its configuration item identifier represented by the `ID` property of the [SMS_Driver_Details Server WMI Class](../../develop/reference/osd/sms_driver_details-server-wmi-class.md) object. This identifier matches the `CI_ID` property of `SMS_Driver`.  

4.  Commit the `SMS_BootImagePackage` object changes.  

5.  Refresh the boot image package by calling `RefreshPkgSource`.  

## Example  
 The following example method removes the Windows driver from the boot image package. The package is identified by its `PackageID` property and the driver is identified by its `CI_ID` property.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub RemoveDriverFromBootImagePackage(connection, driverId, packageId)  
    Dim bootImagePackage  
    Dim driver   
    Dim driverDetails  
    Dim newReferencedDrivers()  
    Dim found  
    Dim index  

    ' Get the boot image package.  
    Set bootImagePackage = connection.Get("SMS_BootImagePackage.PackageID='" & packageId &"'" )  

    found = False  
    index=0  

    ' Copy the contents and leave out the driver.  
    For Each driver In bootImagePackage.ReferencedDrivers  
        If driver.ID = driverID Then  
            found=True  
        Else  
           Set newReferencedDrivers(index)=driver  
           index = index + 1   
        End If  
    Next  

    ' Update the referenced drivers.  
    If found=True Then    
        ReDim preserve newReferencedDrivers(UBound(bootImagePackage.ReferencedDrivers)-1)  
        bootImagePackage.ReferencedDrivers=newReferencedDrivers  
        bootImagePackage.Put_  
        bootImagePackage.RefreshPkgSource  
   End If           

End Sub  
```  

```c#  
public void RemoveDriverFromBootImagePackage(  
    WqlConnectionManager connection,  
    int driverId,  
    string packageId)  
{  
    try  
    {  
        // Get the boot image package.  
        IResultObject bootImagePackage = connection.GetInstance(@"SMS_BootImagePackage.packageId='" + packageId + "'");  

        // Get the (SMS_Driver_Details) drivers referenced by the package.  
        List<IResultObject> referencedDrivers = bootImagePackage.GetArrayItems("ReferencedDrivers");  

        foreach (IResultObject ro in referencedDrivers)  
        {  
            if (ro["ID"].IntegerValue == driverId) // Remove the driver that matches driverId.  
            {  
                referencedDrivers.Remove(ro);  
                break;  
            }  
        }  

        bootImagePackage.SetArrayItems("ReferencedDrivers", referencedDrivers);  

        // Commit the changes.  
        bootImagePackage.Put();  
        bootImagePackage.ExecuteMethod("RefreshPkgSource", null);  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine(e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`Connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`driverID`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The Windows driver identifier available in `SMS_Driver.CI_ID`.|  
|`PackageID`|-   Managed: `String`<br />-   VBScript: `String`|The boot image package identifier available in `SMS_BootImagePackage.PackageID`.|  

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
 [About Operating System Deployment Driver Management](../../develop/osd/about-operating-system-deployment-driver-management.md)   
 [How to Add a Windows Driver to a Configuration Manager Boot Image Package](../../develop/osd/how-to-add-a-windows-driver-to-a-configuration-manager-boot-image-package.md)   
 [Operating System Deployment Driver Management](../../develop/osd/operating-system-deployment-driver-management.md)
