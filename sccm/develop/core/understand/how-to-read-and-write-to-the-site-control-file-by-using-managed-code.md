---
title: "Read and Write to the Site Control File by Using Managed Code"
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
ms.assetid: 7fc4e08d-bccf-4616-a789-71070d3c6f7bsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Read and Write to the Configuration Manager Site Control File by Using Managed Code
To write to the System Center Configuration Manager site control file by using the managed SMS Provider, you get the site definition file by querying for the required resource or component. You then update the embedded property, embedded property list, or multi-string list as required.  

> [!NOTE]
>  You can also use connection manager [GetInstance](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.connectionmanagerbase.getinstance.aspx) to get the required resource or component.  

 The managed System Center Configuration Manager manages the connection session to the site control file automatically for you. Therefore you treat the [IResultObject](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.iresultobject.aspx) objects returned from the query in the same way as you treat [IResultObject](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.iresultobject.aspx) objects retrieved from the SMS Provider.  

### To read and write to the site control file  

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md).  

2.  Use the Connection Manager **QueryProcessor** object *ExecQuery* or *GetInstance* method to get the required site control file resource or component [IResultObject](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.iresultobject.aspx) object.  

3.  Using the [IResultObject](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.iresultobject.aspx) update the site control file.  

4.  Use the [IResultObject](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.iresultobject.aspx) object [Put](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.iresultobject.put.aspx) method to commit the changes.  

## Example  
 The following C# example accesses the client agent component of the site control file and creates a dummy property, property list and multi-string list. It then removes the updates that were made. The example demonstrates how to query the site control file, make updates, and commit changes to the site control file.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```  
public void ReadWriteSCF(WqlConnectionManager connection,string siteCode)  
{  
    try  
    {  

    // Query for the site's site control file client agent settings.  
    IResultObject resources =  
    connection.QueryProcessor.ExecuteQuery  
    ("SELECT * FROM SMS_SCI_ClientComp WHERE ClientComponentName = 'Client Agent' AND SiteCode = '" +  
    siteCode + "'");  

    foreach (IResultObject resource in resources)  
    {          
            // Embedded Properties  

            Console.WriteLine("Embedded property");  
            Console.WriteLine("-----------------");  

            int value = 0;  
            string value1 = "";  
            string value2 = "";  

            // Write a dummy embedded property.  
            this.WriteScfEmbeddedProperty(resource, "Test", 10, "Hello", "World");  

            // Get the embedded property back and display the values.  
            if (this.GetScfEmbeddedProperty(resource, "Test", ref value, ref value1, ref value2))  
            {  
                Console.WriteLine("Value: " + value);  
                Console.WriteLine("Value1: " + value1);  
                Console.WriteLine("Value2: " + value2);  

                // Remove the dummy embedded property.  
                Dictionary<string, IResultObject> EmbeddedProperties = resource.EmbeddedProperties;  
                EmbeddedProperties.Remove("Test");  
                resource.EmbeddedProperties = EmbeddedProperties;  
                resource.Put();  

                // See if the dummy embedded property is still there.  
                if (this.GetScfEmbeddedProperty(resource, "Test", ref value, ref value1, ref value2))  
                {  
                    Console.WriteLine("Test exists");  
                }  
                else  
                {  
                    Console.WriteLine("Test does not exist");  
                }  
            }  
            else  
            {  
                Console.WriteLine("Property not found");  
            }  

            Console.WriteLine();  

            // Embedded property list.  

            Console.WriteLine("Embedded property list");  
            Console.WriteLine("----------------------");  

            // values contains the embedded property list.  
            ArrayList values = new ArrayList();  

            values.Add("Elephant");  
            values.Add("Giraffe");  

            // Write to the resource.  
            this.WriteScfEmbeddedPropertyList(resource, "Animals", values);  

            ArrayList retrievedValues;  

            // Get the embedded property list and display.  
            if (this.GetScfEmbeddedPropertyList(resource, "Animals", out retrievedValues))  
            {  
                foreach (string retrievedValue in retrievedValues)  
                {  
                    Console.WriteLine(retrievedValue);  
                }  

                // Remove one of the entries.  
                retrievedValues.Remove("Elephant");  
                Console.WriteLine();  

                // Update the list.  
                this.WriteScfEmbeddedPropertyList(resource, "Animals", retrievedValues);  

                // Display the list again.  
                this.GetScfEmbeddedPropertyList(resource, "Animals", out retrievedValues);  
                foreach (string retrievedValue in retrievedValues)  
                {  
                    Console.WriteLine(retrievedValue);  
                }  

            }  
            else  
            {  
                Console.WriteLine("None");  
            }  

            Console.WriteLine();  

            // RegMultiStringList.  

            Console.WriteLine("RegMultiStringList");  
            Console.WriteLine("------------------");  

            // valuesStrings is the RegMultiString List.  
            ArrayList valueStrings = new ArrayList();  

            valueStrings.Add("Tom");  
            valueStrings.Add("Harry");  

            this.WriteScfRegMultiStringList(resource, "Names", valueStrings);  

            ArrayList retrievedValuesStrings;  

            if (this.GetScfRegMultiStringList(resource, "Names", out retrievedValuesStrings))  
            {  
                foreach (string retrievedValue in retrievedValuesStrings)  
                {  
                    Console.WriteLine(retrievedValue);  
                }  

                // Remove one of the entries.  
                retrievedValuesStrings.Remove("Tom");  
                Console.WriteLine();  

                // Update the list.  
                this.WriteScfRegMultiStringList(resource, "Names", retrievedValuesStrings);  

                // Display the list again.  
                this.GetScfRegMultiStringList(resource, "Names", out retrievedValuesStrings);  
                foreach (string retrievedValue in retrievedValuesStrings)  
                {  
                    Console.WriteLine(retrievedValue);  
                }  
            }  
            else  
            {  
                Console.WriteLine("None");  
            }  
        }  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed: " + e.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|`siteCode`|-   `String`|The site code for the Configuration Manager site.|  

## Compiling the Code  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Collections  

 System.ComponentModel  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 The Configuration Manager exceptions that can be raised are [SmsConnectionException](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsconnectionexception.aspx) and [SmsQueryException](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsqueryexception.aspx). These can be caught together with [SmsException](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsexception.aspx).  

## See Also  
 [About the Configuration Manager Provider](../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md)   
 [About the Configuration Manager Site Control File](../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)    
 [How to Read a Configuration Manager Site Control File Embedded Property List](../../../develop/core/understand/how-to-read-a-configuration-manager-site-control-file-embedded-property-list.md)    
 [How to Use Configuration Manager Objects With Managed Code](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)   
