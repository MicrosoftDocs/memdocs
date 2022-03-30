---
title: "Remove a Category from a Windows Driver"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 85b50703-f51d-470b-9d9f-4d065c2bcb88
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
description: Learn about how to remove a category from a Windows driver by modifying the CategoryInstance_UniqueIDs array property.

---
# How to Remove a Category from a Windows Driver
In Configuration Manager, you remove a category from a Windows driver by removing the unique identifier for the category from the [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) `CategoryInstance_UniqueIDs` array property.  

### To remove a category from a Windows driver  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../core/understand/sms-provider-fundamentals.md).  

2.  Get the [SMS_Driver](../../develop/reference/osd/sms_driver-server-wmi-class.md) object for the driver that you want remove the category from.  

3.  Get the category name identifier from the [SMS_CategoryInstance Server WMI Class](../../develop/reference/compliance/sms_categoryinstance-server-wmi-class.md) object that matches the desired category.  

4.  Remove the category identifier from the [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) object `CategoryInstance_UniqueIDs` array property.  

5.  Commit the [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) changes.  

## Example  
 The following example method removes a category from a Windows driver. `driverID` is a valid [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) object. For more information, see [About Operating System Deployment Driver Management](../../develop/osd/about-operating-system-deployment-driver-management.md).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub RemoveDriverCategory(connection,driver,categoryName)  

    Dim results  
    Dim driverCategoryID  
    Dim category  
    Dim categories   
    Dim i  

    If IsNull(driver.CategoryInstance_UniqueIDs) _  
           or UBound (driver.CategoryInstance_UniqueIDs) = -1 Then  
        ' There are no categories, so quit.  
        Wscript.Echo "No categories found"  
        Exit Sub  
    End If    

     Set results = _  
      connection.ExecQuery("SELECT * From SMS_CategoryInstance WHERE LocalizedCategoryInstanceName = '" _  
      + categoryName+ "'")  

    ' If the category was found, delete, if it is there, from the driver.  
    For Each category In results  

        ' Destination for copied categories.  
        categories = Array(driver.CategoryInstance_UniqueIDs)  
        i=0   

        For Each driverCategoryID in driver.CategoryInstance_UniqueIDs  
            If driverCategoryID = category.CategoryInstance_UniqueID Then  
                ' Found it, so skip it.  
                 Redim Preserve categories (UBound(categories))  
            Else  
                ' Copy the category.  
                categories(i) = driverCategoryID  
                i=i+1  
            End If   
        Next   

        ' Make sure the array is empty.  
        if i = 0  Then  
            Redim categories(-1)  
        End If  

         driver.CategoryInstance_UniqueIDs = categories  
         driver.Put_  
    Next  
End Sub     
```  

```c#  
public void RemoveDriverCategory(WqlConnectionManager connection,  
    IResultObject driver,  
    string categoryName)  
{  
    try  
    {  
        // Get the category.  
        IResultObject results =   
            connection.QueryProcessor.ExecuteQuery(  
            "SELECT * From SMS_CategoryInstance WHERE LocalizedCategoryInstanceName = '"   
            + categoryName   
            + "'");  

        ArrayList driverCategories = new ArrayList(driver["CategoryInstance_UniqueIDs"].StringArrayValue);  

        // Remove the category from the driver.  
        foreach (IResultObject category in results)  
        {  
            driverCategories.Remove(category["CategoryInstance_UniqueID"].StringValue);  
        }  

        // Update the driver.  
        driver["CategoryInstance_UniqueIDs"].StringArrayValue = (string[])driverCategories.ToArray(typeof(string));  
        driver.Put();  
    }  
    catch(SmsException e)  
    {  
        Console.WriteLine("Failed to remove category :" + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`Connection`|-   Managed:`WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`driver`|-   Managed: `IResultObject`<br />-   VBScript:  `SWbemObject`|The Windows driver. It is an instance of [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md).|  
|`categoryName`|-   Managed: `String`<br />-   VBScript:  `String`|The name of an existing category. This matches the [SMS_CategoryInstance Server WMI Class](../../develop/reference/compliance/sms_categoryinstance-server-wmi-class.md)e `LocalizedCategoryInstanceName` property.|  

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
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [About Operating System Deployment Driver Management](../../develop/osd/about-operating-system-deployment-driver-management.md)   
 [How to Add a Category to a Windows Driver](../../develop/osd/how-to-add-a-category-to-a-windows-driver.md)
