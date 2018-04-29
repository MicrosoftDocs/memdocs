---
title: "Add a Category to a Windows Driver"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ed70a6c3-137b-41f9-b428-675737fb6a86
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Add a Category to a Windows Driver
In System Center Configuration Manager, you add a category to a Windows driver by adding the unique identifier for the category to the [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md)`CategoryInstance_UniqueIDs` array property. The array contains one or more string identifiers that match the [SMS_CategoryInstance Server WMI Class](../../develop/reference/compliance/sms_categoryinstance-server-wmi-class.md)`CategoryInstance_UniqueID` property value. There is an instance of [SMS_CategoryInstance Server WMI Class](../../develop/reference/compliance/sms_categoryinstance-server-wmi-class.md) object for each category in the system.  

> [!NOTE]
>  The unique identifier for a driver category is prepended with the text "DriverCategories". Other category types have different text.  

 A category has localization information, and it is from the [SMS_CategoryInstance Server WMI Class](../../develop/reference/compliance/sms_categoryinstance-server-wmi-class.md)`LocalizedCategoryInstanceName` property that the display name of the category is obtained.  

### To add a category to a Windows driver  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the [SMS_Driver](../../develop/reference/osd/sms_driver-server-wmi-class.md) object for the driver you want to add a category to.  

3.  Get the category name identifier from the [SMS_CategoryInstance Server WMI Class](../../develop/reference/compliance/sms_categoryinstance-server-wmi-class.md) object that matches the desired category.  

4.  Add the category identifier to the [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) object `CategoryInstance_UniqueIDs` array property.  

5.  Commit the [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) changes.  

## Example  
 The following example methods adds a category to a Windows driver. `driverID` is a valid [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) object. For more information, see [About Operating System Deployment Driver Management](../../develop/osd/about-operating-system-deployment-driver-management.md).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AddDriverCategory(connection,driver,categoryName)  

    Dim categories  
    Dim category  
    Dim driverCategoryID  
    Dim categoryID  
    Dim results  
    Dim existingCategory  

    ' Find the category that matches the supplied category name.  
    Set results = _  
      connection.ExecQuery("SELECT * From SMS_CategoryInstance WHERE LocalizedCategoryInstanceName = '" _  
      + categoryName+ "'")  

    ' If the category was found, add it to the driver.  
    For Each category in results  

        If IsNull(driver.CategoryInstance_UniqueIDs) or UBound (driver.CategoryInstance_UniqueIDs) = -1 Then  
            ' It is empty. Add the category.  
            driver.CategoryInstance_UniqueIDs =  Array(category.CategoryInstance_UniqueID)  
         Else  

            ' Determine if the category is already applied to the driver.  
            For each existingCategory in driver.CategoryInstance_UniqueIDs   
                if existingCategory = category.CategoryInstance_UniqueID Then  
                    WScript.Echo "Already added"  
                    Exit Sub  
                End If  
            Next      

            ' Add the category.  
            categories = driver.CategoryInstance_UniqueIDs  
            Redim Preserve categories (UBound (driver.CategoryInstance_UniqueIDs)+1)  
            categories (Ubound (categories)) =  category.CategoryInstance_UniqueID   
            driver.CategoryInstance_UniqueIDs = categories  
        End If  

        driver.Put_         
    Next      
End Sub  
```  

```c#  
public void AddDriverCategory(  
    WqlConnectionManager connection,  
    IResultObject driver,  
    string categoryName)  
{  
    try  
    {  
        // Get the category.  
        IResultObject results = connection.QueryProcessor.ExecuteQuery(  
        "SELECT * From SMS_CategoryInstance WHERE LocalizedCategoryInstanceName = '" + categoryName + "'");  

       ArrayList driverCategories = new ArrayList(driver["CategoryInstance_UniqueIDs"].StringArrayValue);//;driverCategories);  

        foreach (IResultObject category in results)  
        {  
            foreach (string driverCategory in driverCategories)  
            {  
                // Do nothing if the driver already has the category.  
                if (driverCategory == category["CategoryInstance_UniqueID"].StringValue)  
                {  
                    Console.WriteLine("Already exists");  
                    return;  
                }  
           }  

            // Add the category to the action.  
           driverCategories.Add(category["CategoryInstance_UniqueID"].StringValue);  
        }  

        // Update the driver.  
        driver["CategoryInstance_UniqueIDs"].StringArrayValue = (string[])driverCategories.ToArray(typeof(string));  
        driver.Put();  

    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to add the category" + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`Connection`|-   Managed: `WqlConnectionManager]<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393868.aspx)|A valid connection to the SMS Provider.|  
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
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [About Operating System Deployment Driver Management](../../develop/osd/about-operating-system-deployment-driver-management.md)   
 [Operating System Deployment Driver Management](../../develop/osd/operating-system-deployment-driver-management.md)   
 [How to Remove a Category from a Windows Driver](../../develop/osd/how-to-remove-a-category-from-a-windows-driver.md)
