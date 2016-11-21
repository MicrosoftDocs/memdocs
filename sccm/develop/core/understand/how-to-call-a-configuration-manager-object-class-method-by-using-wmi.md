---
title: "Call an Object Class Method by Using WMI | Configuration Manager"
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
ms.assetid: b83b28f0-0af9-44b9-a7c8-4901e3e08b51
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Call a Configuration Manager Object Class Method by Using WMI
To call a SMS Provider class method, in System Center Configuration Manager, you use the [SWbemServices](assetId:///SWbemServices?qualifyHint=False&autoUpgrade=True) object [ExecMethod](assetId:///ExecMethod?qualifyHint=False&autoUpgrade=True) method to call methods that are defined by the class.  

> [!NOTE]
>  To call a method on an object instance, call the method from the object directly. For example,  `ObjectInstance.MethodName parameters`.  

### To call a Configuration Manager object class method  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Using the assetId:///SWbemServices?qualifyHint=False&autoUpgrade=True you obtain in step one, call [Get](assetId:///Get?qualifyHint=False&autoUpgrade=True) to get the class definition.  

3.  Create the input parameters as a SWbemMethodSet.  

4.  Using the assetId:///SWbemServices?qualifyHint=False&autoUpgrade=True object instance, call [ExecuteMethod](assetId:///ExecuteMethod?qualifyHint=False&autoUpgrade=True) and specify the class name and input parameters.  

5.  Retrieve the method return value from the [ReturnValue](assetId:///ReturnValue?qualifyHint=False&autoUpgrade=True) property in the returned [SWbemObject](assetId:///SWbemObject?qualifyHint=False&autoUpgrade=True) object.  

## Example  
 The following example validates a collection rule query by calling the [SMS_CollectionRuleQuery](assetId:///SMS_CollectionRuleQuery?qualifyHint=False&autoUpgrade=True) class [ValidateQuery](assetId:///ValidateQuery?qualifyHint=False&autoUpgrade=True) class method.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling code snippets.md).  

```vbs  
Sub ValidateQueryRule(connection, wqlQuery)  

    Dim inParams  
    Dim outParams  
    Dim collectionRuleClass  

    On Error Resume Next  

    ' Obtain the class definition object of a SMS_CollectionRuleQuery object.  
    Set collectionRuleClass = connection.Get("SMS_CollectionRuleQuery")  

    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't get collection rule query object"  
        Exit Sub  
    End If  

    ' Set up the in parameter.  
    Set inParams = collectionRuleClass.Methods_("ValidateQuery").InParameters.SpawnInstance_  
    inParams.WQLQuery = wqlQuery  
    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't get in parameters object"  
        Exit Sub  
    End If  

    ' Call the method.  
    Set outParams = _  
        connection.ExecMethod( "SMS_CollectionRuleQuery", "ValidateQuery", inParams)  
    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't run method"  
        Exit Sub  
    End If  

    If outParams.ReturnValue = True Then  
        Wscript.Echo "Valid query"  
    Else   
        WScript.Echo "Not a valid query"  
    End If            
  End Sub  

```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: assetId:///SWbemServices?qualifyHint=False&autoUpgrade=True|A valid connection to the SMS Provider.|  
|`wqlQuery`|-   `String`|A WQL query string. For this example, `SELECT * FROM SMS_R_System` is a valid query.|  

## Compiling the Code  

## See Also  
 [Windows Management Instrumentation](http://go.microsoft.com/fwlink/?LinkId=43950)   
 [Configuration Manager Objects](../../../develop/core/understand/configuration-manager-objects-overview.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Create a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-wmi.md)   
 [How to Delete a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-delete-a-configuration-manager-object-by-using-wmi.md)   
 [How to Modify a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-wmi.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-an-asynchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Read a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-wmi.md)   
 [How to Read Lazy Properties by Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md)   
 [How to Use Configuration Manager Objects With WMI](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md)
