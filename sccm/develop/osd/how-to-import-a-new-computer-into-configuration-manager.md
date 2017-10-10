---
title: "Import a New Computer"
titleSuffix: "Configuration Manager"
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
ms.assetid: 84858dfe-ba1f-448b-8da1-0fe38f619cd6searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Import a New Computer into Configuration Manager
You add a new computer directly to the System Center Configuration Manager database by calling the [ImportMachineEntry Method in Class SMS_Site](../../develop/reference/core/servers/configure/importmachineentry-method-in-class-sms_site.md). This can be used to deploy operating systems to computers that have not yet been discovered automatically by System Center Configuration Manager.  

 You must provide the following information:  

-   NETBIOS computer name  

-   MAC address  

-   SMBIOS GUID  

> [!NOTE]
>  The MAC address must be for a network adapter that has a driver in Windows PE. The MAC address must be in colon format. For example, `00:00:00:00:00:00`. Other formats will prevent the client from receiving policy.  

 You should add a newly imported computer to a collection. This allows you to immediately create advertisements for deploying operating systems to the computer.  

 You can associate a new computer with a reference computer. For more information, see [How to Create an Association Between Two Computers in Configuration Manager](../../develop/osd/how-to-create-an-association-between-two-computers-in-configuration-manager.md).  

### To add a new computer  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Call the [ImportMachineEntry Method in Class SMS_Site](../../develop/reference/core/servers/configure/importmachineentry-method-in-class-sms_site.md).  

3.  Add the resource identifier you get from ImportMachineEntry to a collection.  

## Example  
 The following example method adds a new computer to Configuration Manager. The [ImportMachineEntry Method in Class SMS_Site](../../develop/reference/core/servers/configure/importmachineentry-method-in-class-sms_site.md) is used to import the computer. Then, the computer is added to a custom collection. "All Systems" collection.  

> [!IMPORTANT]
>  In previous version of this example, the computer was added to the "All Systems" collection. It is no longer possible to modify the built-in collections, use a custom collection instead.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AddNewComputer (connection, netBiosName, smBiosGuid, macAddress)  

    Dim inParams  
    Dim outParams  
    Dim siteClass  
    Dim collection  
    Dim collectionRule  

    If (IsNull(smBiosGuid) = True) And (IsNull(macAddress) = True) Then  
        WScript.Echo "smBiosGuid or macAddress must be defined"  
        Exit Sub  
    End If       

    If IsNull(macAddress) = False Then  
        macAddress = Replace(macAddress,"-",":")  
    End If      

    ' Obtain an InParameters object specific  
    ' to the method.  

    Set siteClass = connection.Get("SMS_Site")  
    Set inParams = siteClass.Methods_("ImportMachineEntry"). _  
        inParameters.SpawnInstance_()  

    ' Add the input parameters.  
    inParams.Properties_.Item("MACAddress") =  macAddress  
    inParams.Properties_.Item("NetbiosName") =  netBiosName  
    inParams.Properties_.Item("OverwriteExistingRecord") =  False  
    inParams.Properties_.Item("SMBIOSGUID") =  smBiosGuid  

    ' Add the computer.  
    Set outParams = connection.ExecMethod("SMS_Site", "ImportMachineEntry", inParams)  

   ' Add the computer to the all systems collection.  
   set collection = connection.Get("SMS_Collection.CollectionID='ABC0000A'")  

   set collectionRule=connection.Get("SMS_CollectionRuleDirect").SpawnInstance_  

   collectionRule.ResourceClassName="SMS_R_System"  
   collectionRule.ResourceID= outParams.ResourceID  

   collection.AddMembershipRule collectionRule  

End Sub  
```  

```c#  
public int AddNewComputer(  
    WqlConnectionManager connection,   
    string netBiosName,   
    string smBiosGuid,   
    string macAddress)  
{  
    try  
    {  
        if (smBiosGuid == null && macAddress == null)  
        {  
            throw new ArgumentNullException("smBiosGuid or macAddress must be defined");  
        }  

        // Reformat macAddress to : separator.  
        if (string.IsNullOrEmpty(macAddress) == false)  
        {  
            macAddress = macAddress.Replace("-", ":");  
        }  

        // Create the computer.  
        Dictionary<string, object> inParams = new Dictionary<string, object>();  
        inParams.Add("NetbiosName", netBiosName);  
        inParams.Add("SMBIOSGUID", smBiosGuid);  
        inParams.Add("MACAddress", macAddress);  
        inParams.Add("OverwriteExistingRecord", false);  

        IResultObject outParams = connection.ExecuteMethod(  
            "SMS_Site",  
            "ImportMachineEntry",  
            inParams);  

        // Add to All System collection.  
        IResultObject collection = connection.GetInstance("SMS_Collection.collectionId='ABC0000A'");  
        IResultObject collectionRule = connection.CreateEmbeddedObjectInstance("SMS_CollectionRuleDirect");  
        collectionRule["ResourceClassName"].StringValue = "SMS_R_System";  
        collectionRule["ResourceID"].IntegerValue = outParams["ResourceID"].IntegerValue;  

        Dictionary<string, object> inParams2 = new Dictionary<string, object>();  
        inParams2.Add("collectionRule", collectionRule);  

        collection.ExecuteMethod("AddMembershipRule", inParams2);  

        return outParams["ResourceID"].IntegerValue;  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("failed to add the computer" + e.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|-   A valid connection to the SMS Provider.|  
|`netBiosName`|-   Managed: `String`<br />-   VBScript: `String`|-   The computer NETBIOS name.|  
|`smBiosGuid`|-   Managed: `String`<br />-   VBScript: `String`|The SMBIOS GUID for the computer.|  
|`MacAddress`|-   Managed: `String`<br />-   VBScript: `String`|The MAC address for the computer in the following format: `00:00:00:00:00:00`.|  

## Compiling the Code  
 The C# example has the following compilation requirements:  

### Namespaces  
 System  

 System.Collections.Generic  

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
 [ImportMachineEntry Method in Class SMS_Site](../../develop/reference/core/servers/configure/importmachineentry-method-in-class-sms_site.md)   
 [Operating System Deployment Computer Management](../../develop/osd/operating-system-deployment-computer-management.md)
