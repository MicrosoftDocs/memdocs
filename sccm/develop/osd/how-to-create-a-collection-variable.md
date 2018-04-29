---
title: "Create a Collection Variable"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: a309d431-d654-42f6-883b-07dac70216f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Create a Collection Variable in Configuration Manager
You create a collection variable for a System Center Configuration Manager collection by adding instances of [SMS_CollectionVariable Server WMI Class](../../develop/reference/osd/sms_collectionvariable-server-wmi-class.md) to the `CollectionVariables` property of [SMS_CollectionSettings Server WMI Class](../../develop/reference/core/clients/collections/sms_collectionsettings-server-wmi-class.md).  

### To create a collection variable  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get an instance of [SMS_CollectionSettings](../../develop/reference/core/clients/collections/sms_collectionsettings-server-wmi-class.md).  

3.  For each variable to be added, add instances of the embedded object [SMS_CollectionVariable](../../develop/reference/osd/sms_collectionvariable-server-wmi-class.md) to the *CollectionVariables* array property.  

4.  Commit the changes to the `SMS_CollectionSettings` class instance.  

## Example  
 The following example method creates a collection variable and adds it to the collection identified by the supplied identifier. If the `SMS_CollectionSettings` object for the collection does not exist, it is created.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub CreateCollectionVariable( connection, name, value, mask, collectionId, precedence)  

    Dim collectionSettings  
    Dim collectionVariables  
    Dim collectionVariable  
    Dim Settings  

    ' See if the settings collection already exists. if it does not, create it.  
    Set settings = connection.ExecQuery _  
      ("Select * From SMS_CollectionSettings Where CollectionID = '" & collectionID & "'")  

    If settings.Count = 0 Then  
        Wscript.Echo "Creating collection settings object"  
        Set collectionSettings = connection.Get("SMS_CollectionSettings").SpawnInstance_  
        collectionSettings.CollectionID = collectionId  
        collectionSettings.Put_  
    End If    

    ' Get the collection settings object.  
    Set collectionSettings = connection.Get("SMS_CollectionSettings.CollectionID='" & collectionId &"'" )  

    ' Get the collection variables.  
    collectionVariables=collectionSettings.CollectionVariables  

    ' Create and populate a new collection variable.  
    Set collectionVariable = connection.Get("SMS_CollectionVariable").SpawnInstance_  
    collectionVariable.Name = name  
    collectionVariable.Value = value  
    collectionVariable.IsMasked = mask  

    ' Add the new collection variable.  
    ReDim Preserve collectionVariables (UBound (collectionVariables)+1)  
    Set collectionVariables(UBound(collectionVariables)) = collectionVariable  

    collectionSettings.CollectionVariables=collectionVariables  

    collectionSettings.Put_  

 End Sub     
```  

```c#  
public void CreateCollectionVariable(  
    WqlConnectionManager connection,   
    string name,   
    string value,   
    bool mask,   
    string collectionId,   
    int precedence)  
{  
    try  
    {  
        IResultObject collectionSettings = null;  

        // Get the collection settings. Create it if necessary.  

         IResultObject collectionSettingsQuery = connection.QueryProcessor.ExecuteQuery(  
                    "Select * from SMS_CollectionSettings where CollectionID='" + collectionId + "'");  

         foreach (IResultObject setting in collectionSettingsQuery)  
         {  
             collectionSettings = setting;  
         }  

        if ( collectionSettings == null)  
         {  
             collectionSettings = connection.CreateInstance("SMS_CollectionSettings");  
             collectionSettings["CollectionID"].StringValue = collectionId;  
             collectionSettings.Put();  
             collectionSettings.Get();  
         }  

        // Create the collection variable.  
        List<IResultObject> collectionVariables = collectionSettings.GetArrayItems("CollectionVariables");  
        IResultObject collectionVariable = connection.CreateEmbeddedObjectInstance("SMS_CollectionVariable");  
        collectionVariable["Name"].StringValue = name;  
        collectionVariable["Value"].StringValue = value;  
        collectionVariable["IsMasked"].BooleanValue = mask;  

        // Add the collection variable to the collection settings.  
        collectionVariables.Add(collectionVariable);  
        collectionSettings.SetArrayItems("CollectionVariables", collectionVariables);  

        // Set the collection variable precedence.  
        collectionSettings["CollectionVariablePrecedence"].IntegerValue = precedence;  

        collectionSettings.Put();  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to create collection variable: " + e.Message);  
        throw;  
   }  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`Connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`Name`|-   Managed: `String`<br />-   VBScript: `String`|The name of the variable to be created.|  
|`Value`|-   Managed: `String`<br />-   VBScript: `String`|The value of the variable|  
|`Mask`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|Specifies whether the value is displayed in the Configuration Manager console.<br /><br /> `true` - the variable value is not displayed.<br /><br /> `false` - the variable value is displayed.|  
|`CollectionID`|-   Managed: `String`<br />-   VBScript: `String`|The collection that the variable is added to.|  
|`Precedence`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The precedence of the variable over other variables in the array.|  

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
 [Configuration Manager Operating System Deployment](../../develop/osd/operating-system-deployment.md)   
 [Configuration Manager Objects](../../develop/core/understand/configuration-manager-objects.md)   
 [Configuration Manager Programming Fundamentals](../../develop/core/understand/configuration-manager-programming-fundamentals.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager  by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Create a Computer Variable in Configuration Manager](../../develop/osd/how-to-create-a-computer-variable.md)   
 [How to Create a Configuration Manager Object by Using Managed Code](../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Create a Configuration Manager Object by Using WMI](../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-wmi.md)   
 [Operating System Deployment Computer Management](../../develop/osd/operating-system-deployment-computer-management.md)
