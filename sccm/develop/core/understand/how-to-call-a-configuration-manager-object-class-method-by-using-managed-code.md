---
title: "How to Call a Configuration Manager Object Class Method by Using Managed Code"
ms.custom: ""
ms.date: "2016-09-20"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "System Center Configuration Manager (current branch)"
ms.assetid: 46cb95e6-9dae-4c08-9cfb-1a570e4c05bc
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Call a Configuration Manager Object Class Method by Using Managed Code
To call a SMS Provider class method, in System Center Configuration Manager, you use the <xref:Microsoft.ConfigurationManagement.ManagementProvider.ConnectionManagerBase.ExecuteMethod*> method. You populate a [Dictionary](assetId:///Dictionary?qualifyHint=False&autoUpgrade=True) object with the method's parameters, and the return value is an [IResultObject](assetId:///IResultObject?qualifyHint=False&autoUpgrade=True) object that contains the result of the method call.  
  
> [!NOTE]
>  To call a method on an object instance, use the <xref:Microsoft.ConfigurationManagement.ManagementProvider.IResultObject.ExecuteMethod*> method on the assetId:///IResultObject?qualifyHint=False&autoUpgrade=True object instance.  
  
### To call a Configuration Manager object class method  
  
1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  
  
2.  Create the input parameters as a assetId:///Dictionary?qualifyHint=False&autoUpgrade=True object.  
  
3.  Using the [WqlConnectionManager](assetId:///WqlConnectionManager?qualifyHint=False&autoUpgrade=True) object instance, call [ExecuteMethod](assetId:///ExecuteMethod?qualifyHint=False&autoUpgrade=True) and specify the class name and input parameters.  
  
4.  Retrieve the method return value from the [ReturnValue](assetId:///ReturnValue?qualifyHint=False&autoUpgrade=True) property in the returned assetId:///IResultObject?qualifyHint=False&autoUpgrade=True object.  
  
## Example  
 The following example validates a collection rule query by calling the [SMS_CollectionRuleQuery](assetId:///SMS_CollectionRuleQuery?qualifyHint=False&autoUpgrade=True) class [ValidateQuery](assetId:///ValidateQuery?qualifyHint=False&autoUpgrade=True) class method.  
  
 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling code snippets.md).  
  
```  
public void ValidateQueryRule(WqlConnectionManager connection, string wqlQuery)  
{  
    try  
    {  
        Dictionary<string,object> validateQueryParameters = new Dictionary<string,object>();  
  
        // Add the sql query as the WQLQuery parameter.  
        validateQueryParameters.Add("WQLQuery",wqlQuery);  
  
        // Call the method  
        IResultObject result=connection.ExecuteMethod("SMS_CollectionRuleQuery", "ValidateQuery", validateQueryParameters);  
  
        if (result["ReturnValue"].BooleanValue == true)  
        {  
            Console.WriteLine (wqlQuery + " is a valid query");  
        }  
        else  
        {  
            Console.WriteLine (wqlQuery + " is not a valid query");  
        }  
     }  
     catch (SmsException ex)  
     {  
           Console.WriteLine("Failed to validate query rule: ",ex.Message);  
           throw;  
     }  
}  
  
```  
  
 This example method has the following parameters:  
  
|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: assetId:///WqlConnectionManager?qualifyHint=False&autoUpgrade=True|A valid connection to the SMS Provider.|  
|`wqlQuery`|-   Managed: assetId:///IResultObject?qualifyHint=False&autoUpgrade=True|A WQL query string. For this example, `SELECT * FROM SMS_R_System` is a valid query.|  
  
## Compiling the Code  
  
### Namespaces  
 System  
  
 System.Collections.Generic  
  
 System.ComponentModel  
  
 Microsoft.ConfigurationManagement.ManagementProvider  
  
 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  
  
### Assembly  
 microsoft.configurationmanagement.managementprovider  
  
 adminui.wqlqueryengine  
  
## Robust Programming  
 The Configuration Manager exceptions that can be raised are <xref:Microsoft.ConfigurationManagement.ManagementProvider.SmsConnectionException> and <xref:Microsoft.ConfigurationManagement.ManagementProvider.SmsQueryException>. These can be caught together with <xref:Microsoft.ConfigurationManagement.ManagementProvider.SmsException>.  
  
## See Also  
 [About Configuration Manager Objects](../../../develop/core/understand/about-configuration-manager-objects.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../develop/core/understand/2a435561-01b7-45d5-b7cf-89fc1845025f.md)   
 [How to Create a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Modify a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/cfbb34e8-9b47-48db-a8ef-408a0a89ad17.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)   
 [How to Read a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)