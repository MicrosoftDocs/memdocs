---
description: Learn how to import a MOF file to extend inventory, in Configuration Manager, by using the ImportInventoryReport method.
title: "Import a MOF File to Extend Inventory"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 4b57f922-9029-4617-8c21-6c75ccebbb5d
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3


---
# How to Import a MOF File to Extend Inventory
You import a MOF file to extend inventory, in Configuration Manager, by using the `ImportInventoryReport` method.  

### To import MOF file to extend hardware inventory  

1.  Connect to the site server namespace (root\sms\site_\<site code>).  

2.  Get the [SMS_InventoryReport](../../../../develop/reference/core/clients/manage/sms_inventoryreport-server-wmi-class.md) class.  

3.  Invoke the [ImportInventoryReport](../../../../develop/reference/core/clients/manage/importinventoryreport-method-in-class-sms_inventoryreport.md) method, passing in the *InventoryReportID*, *ImportType*, and *MofBuffer* parameters.  

## Example  
 The following example imports a MOF file to extend inventory using the ImportInventoryReport method.  

```c#  

public class ImportInventory{            public const string HardwareInventoryReportID = "{00000000-0000-0000-0000-000000000001}";    static void Main(string[] args)    {        if (args != null && args.Length >= 2)        {            string fileName = args[0];            string siteCode = args[1];            ImportInventoryReport(siteCode, fileName);        }        else        {            Console.WriteLine("Usage: InventoryImportExample <MofFileName> <site code>");        }        Console.WriteLine("Press any key to exit");        Console.ReadLine();    }    public static void ImportInventoryReport(string siteCode, string fileName,         string inventoryReportID = HardwareInventoryReportID,         InventoryImportType importOption = InventoryImportType.BothClassAndReport)    {        if (File.Exists(fileName)==false)        {            throw new FileNotFoundException("MOF file not found", fileName);        }        string mofToImport = File.ReadAllText(fileName);        // Get the SMS_InventoryReport class.        try        {            string scope = string.Format(@"root\sms\site_{0}",siteCode);            ManagementClass cls = new ManagementClass(scope, "SMS_InventoryReport", null);            ManagementBaseObject inParams = cls.GetMethodParameters("ImportInventoryReport");            inParams["InventoryReportID"] = inventoryReportID;            inParams["ImportType"] = (uint)importOption;            inParams["MofBuffer"] = mofToImport;            ManagementBaseObject retVal = cls.InvokeMethod("ImportInventoryReport", inParams, null);            // Get current site code.            uint resultCode = (uint)retVal["StatusCode"];            if (resultCode == 0)            {                Console.WriteLine("ImportInventoryReport for file {0} succeed ", fileName);            }            else            {                Console.WriteLine("ImportInventoryReport for file {0} failed with error code:{1} ", fileName,resultCode);            }        }        catch (ManagementException e)        {            Console.WriteLine("Failed to execute method ImportInventoryReport for file {0}: {1}", fileName, e.ToString());        }    }    public enum InventoryImportType    {        ClassOnly = 1,         ReportOnly = 2,         BothClassAndReport = 3    }}  

```  

```wmimof  
An example MOF file.================================[ SMS_Report (TRUE),  SMS_Group_Name ("User Account"),  SMS_Class_ID ("MICROSOFT|USER_ACCOUNT|1.0"),  Namespace ("root\\\\cimv2") ]class Win32_UserAccount : SMS_Class_Template{    [ SMS_Report (TRUE), key ]    String     Domain;    [ SMS_Report (TRUE), key ]    String     Name;    [ SMS_Report (TRUE) ]    UInt32     AccountType;    [ SMS_Report (TRUE) ]    String     Caption;    [ SMS_Report (TRUE) ]    String     Description;    [ SMS_Report (TRUE) ]    Boolean     Disabled;    [ SMS_Report (TRUE) ]    String     FullName;    [ SMS_Report (TRUE) ]    DateTime     InstallDate;    [ SMS_Report (TRUE) ]    Boolean     LocalAccount;    [ SMS_Report (TRUE) ]    Boolean     Lockout;    [ SMS_Report (TRUE) ]    Boolean     PasswordChangeable;    [ SMS_Report (TRUE) ]    Boolean     PasswordExpires;    [ SMS_Report (TRUE) ]    Boolean     PasswordRequired;    [ SMS_Report (TRUE) ]    String     SID;    [ SMS_Report (TRUE) ]    UInt8     SIDType;    [ SMS_Report (TRUE) ]    String     Status;};  
```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`siteCode`|-   Managed: `String`|The site code.|  
|`fileName`|-   Managed: `String`|The name of the MOF file to import.|  
|`inventoryReportID`|-   Managed: `String`|Inventory report identifier.|  
|`importOption`|-   Managed: `String`|Import type. Possible values are:<br /><br /> -   1 – Class Only<br />-   2 – Report Only<br />-   3 – Both Class and Report|  
|`mofToImport`|-   Managed: `String`|The MOF content that contains the inventory class or report to import. This is the same format as the Configuration Manager 2007 sms_def.mof file, or the file format that you export from inventory client settings.|  

## Compiling the Code  
 This C# example requires:  

### Assembly  
 System.Management  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [Configuration Manager Software Development Kit](../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [About Configuration Manager Inventory](../../../../develop/core/clients/inventory/about-configuration-manager-inventory.md)
