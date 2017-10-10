---
title: "Read a Site Control File Embedded Property List"
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
ms.assetid: 2b9ed9ec-4f07-4d87-891c-773badf6a694searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Read a Configuration Manager Site Control File Embedded Property List
In System Center Configuration Manager, you read an embedded property list from a site control file resource by getting the [SMS_EmbeddedPropertyList](../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md) object for the embedded object from the resources *PropLists* property array.  

 An embedded property list has the following properties that you can set. For more information, see [SMS_EmbeddedPropertyList](../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md).  

|Value|Description|  
|-----------|-----------------|  
|PropertyListName|The embedded property name.|  
|Values|An array of string values. Each array item represents a single property list item.|  

> [!CAUTION]
>  Making changes to the site control file can cause irreparable damage to your System Center Configuration Manager site.  

### To read  a site control file embedded property list  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Using the connection object from step one, get a site control file resource. For more information, see [About the Configuration Manager Site Control File](../../../develop/core/understand/about-the-configuration-manager-site-control-file.md).  

3.  Get the `SMS_EmbeddedPropertyList` for the required embedded property list.  

4.  Access the property list values by using the `SMS_EmbeddedPropertyList` object *Values* property array.  

## Example  
 The following example method populates the supplied `values` parameter with the *Values* array of the embedded property list `SMS_EmbeddedPropertyList` identified by the `propertyListName` parameter. `true` is returned if the embedded property list is found; otherwise, `false` is returned.  

 To view code that calls these functions, see [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md) or see [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Function GetScfEmbeddedPropertyList(resource,  _  
        propertyListName,               _  
        ByRef values)  

    Dim scfPropertyList  

    If IsNull(resource.PropLists) = True Then  
        GetScfPropertyList = False  
        Exit Function  
    End If      

    For each scfPropertyList in resource.PropLists  
       if   scfPropertyList.PropertyListName = propertyListName Then  
            ' Found property list, so return the values array.  
            values = scfPropertyList.Values  
            GetScfEmbeddedPropertyList = True  
            Exit Function  
        End If  
     Next    

     ' Did not find the property list.  
     GetScfEmbeddedPropertyList = False  
End Function  

```  

```c#  
public bool GetScfEmbeddedPropertyList(  
    IResultObject resource,  
    string propertyListName,  
    out ArrayList values)  
{  
    values = new ArrayList();  
    try  
    {  
        if (resource.EmbeddedPropertyLists.ContainsKey(propertyListName))  
        {  
            values.AddRange(resource.EmbeddedPropertyLists[propertyListName]["Values"].StringArrayValue);  
            return true;  
        }  
    }  
    catch(SmsException e)  
    {  
        Console.WriteLine("Couldn't get the embedded property list: " + e.Message);  
    }  
    return false;  

}  

```  

 The sample method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`Resource`|-   Managed: `IResultObject`<br />-   VBScript: [SWbemObject](https://msdn.microsoft.com/library/aa393741.aspx)|The site control file resource that contains the embedded property.|  
|`propertyListName`|-   Managed: `String`<br />-   VBScript: `String`|The embedded property list to be read.|  
|`Values`|-   Managed: `String` array<br />-   VBScript: `String` array|The `SMS_EmbeddedProperty` class Values property. An array of string values.|  

## Compiling the Code  
 The C# example has the following compilation requirements:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Collections  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [About the Configuration Manager Site Control File](../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)  
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)
