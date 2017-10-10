---
title: "Create an Association Between Two Computers"
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
ms.assetid: f3670fc7-3b07-4812-909b-d225580a7dcbsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create an Association Between Two Computers in Configuration Manager
You create an association between a reference and destination computer, in System Center Configuration Manager, by calling the [AddAssociation Method in Class SMS_StateMigration](../../develop/reference/osd/addassociation-method-in-class-sms_statemigration.md).  

> [!NOTE]
>  You call the [DeleteAssociation Method in Class SMS_StateMigration](../../develop/reference/osd/deleteassociation-method-in-class-sms_statemigration.md) to delete an association.  

### To create an association between two computers  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Call the [AddAssociation Method in Class SMS_StateMigration](../../develop/reference/osd/addassociation-method-in-class-sms_statemigration.md).  

## Example  
 The following example method adds an association between a source and reference computer.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AssociateComputer(connection, referenceComputerResourceId, destinationComputerResourceId)  

    Dim stateMigrationClass  
    Dim inParams  
    Dim outParams  

    ' Get the state migration class.  
    Set stateMigrationClass = connection.Get("SMS_StateMigration")  

    ' Set up the parameters.  
    Set inParams = _  
      stateMigrationClass.Methods_("AddAssociation").InParameters.SpawnInstance_  
    inParams.SourceClientResourceID = referenceComputerResourceId  
    inParams.RestoreClientResourceID = destinationComputerResourceId  

    ' Call the method.  
    Set outParams = _  
      connection.ExecMethod( "SMS_StateMigration", "AddAssociation", inParams)     

   End Sub  
```  

```c#  
public void AssociateComputer(  
    WqlConnectionManager connection,   
    int referenceComputerResourceId,   
    int destinationComputerResourceId)  
{  
    try  
    {  
        // Set up the reference and destination computer in parameters.  
        Dictionary<string, object> inParams = new Dictionary<string, object>();  
        inParams.Add("SourceClientResourceID", referenceComputerResourceId);  
        inParams.Add("RestoreClientResourceID", destinationComputerResourceId);  

        // Create the computer association.  
       connection.ExecuteMethod("SMS_StateMigration", "AddAssociation", inParams);  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("failed to make the association" + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`referenceComputerResourceID`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The Configuration Manager resource identifier for the reference computer. This is available from `SMS_R_System` class `ResourceId` property for the computer.|  
|`destinationComputerResourceID`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The Configuration Manager resource identifier for the destination computer. This is available from `SMS_R_System` class `ResourceId` property for the computer.|  

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
 [Operating System Deployment Computer Management](../../develop/osd/operating-system-deployment-computer-management.md)   
 [AddAssociation Method in Class SMS_StateMigration](../../develop/reference/osd/addassociation-method-in-class-sms_statemigration.md)   
 [DeleteAssociation Method in Class SMS_StateMigration](../../develop/reference/osd/deleteassociation-method-in-class-sms_statemigration.md)
