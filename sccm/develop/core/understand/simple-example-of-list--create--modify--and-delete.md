---
title: "Example of List, Create, Modify, and Delete"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 6f31059a-ec25-4113-b3a7-8de92269a351
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Simple Example of List, Create, Modify, and Delete
The following example shows set of very basic methods using the `SMS_Package` class to demonstrate List, Create, Modify and Delete operations using the SMS Provider. This is a look at the structure of a basic Configuration Manager program – there are more useful method snippets in other areas of the SDK that accomplish specific tasks.  

> [!IMPORTANT]
>  To simplify the code example, some methods are commented out, as they need additional information (an existing package identifier). Use the `ListPackages` method to obtain the package identifier for use with the `ModifyPackage` and `DeletePackage` methods.  

### To list packages  

1.  Set up a connection to the SMS Provider.  

2.  Run a query, which populates a variable with a collection of `SMS_Package` class instances.  

3.  Enumerate through the collection and list the packages returned by the query.  

### To create a package  

1.  Set up a connection to the SMS Provider.  

2.  Create the new package object by using the `SMS_Package` class.  

3.  Populate the new package properties.  

4.  Save the package.  

### To modify a package  

1.  Set up a connection to the SMS Provider.  

2.  Load the existing package object by using the `SMS_Package` class.  

3.  Modify a package property.  

4.  Save the package.  

### To delete a package  

1.  Set up a connection to the SMS Provider.  

2.  Load the existing package object by using the `SMS_Package` class.  

3.  Delete the package by using the delete method.  

## Example  
 The following example method shows set of very basic methods using `SMS_Package` class to demonstrate List, Create, Modify and Delete operations using the SMS Provider.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

> [!NOTE]
>  The below example embeds the calling code in the code. Most other examples in SDK the simply show a method with parameters.  

```c#  

using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  

// Added the below Configuration Manager DLL references to support basic SMS Provider operations:  
//    C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.ManagementProvider.dll  
//    C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\AdminUI.WqlQueryEngine.dll  
// Added the below Configuration Manager namespaces to support basic SMS Provider operations:  
      using Microsoft.ConfigurationManagement.ManagementProvider;                    
      using Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine;     

//  
// A set of very basic methods using the SMS_Package class to demonstrate List, Create, Modify and Delete operations using the SMS Provider.  
//   
// Note: To simplify the code example, some methods are commented out, as they need additional information (an existing package identifier).   
// Use the ListPackages method to obtain the package identifier for use with the ModifyPackage and DeletePackage methods.   
//  
namespace BasicApp  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            // Setup Objects  
            SnippetClass BasicCMAppSnippets = new SnippetClass();  

            // Setup a connection to the SMS Provider.  
            // Passing in <server name>, <domain\\account>, <password>.   
            WqlConnectionManager WMIConnection = BasicCMAppSnippets.Connect("CMLABSERVER", "CMLABSERVER\\cmlabuser", "password");  

            // List all packages (instances of SMS_Package).  
            BasicCMAppSnippets.ListPackages(WMIConnection);  

            // Create a new package.  
            // Note: This is not a useful package (too few properties), just a demonstration of creating a Configuration Manager object.  
            BasicCMAppSnippets.CreatePackage(WMIConnection, "New Package", "This is the new package.");  

            // Modifies a specific package (instance of SMS_Package).  
            // A valid PackageID needs to be passed to the ModifyPackage method - replace "ABC00000".  
            //BasicCMAppSnippets.ModifyPackage(WMIConnection, "ABC00000");  

            // Deletes a specific package (instance of SMS_Package).  
            // A valid PackageID needs to be passed to the DeletePackage method - replace "ABC00000".  
            //BasicCMAppSnippets.DeletePackage(WMIConnection, "ABC00000");  

            // Delay to keep the console output visible.  
            Console.ReadLine();  
        }  
    }  

    class SnippetClass  
    {  
        public WqlConnectionManager Connect(string serverName, string userName, string userPassword)  
        {  
            try  
            {  
                SmsNamedValuesDictionary namedValues = new SmsNamedValuesDictionary();  
                WqlConnectionManager connection = new WqlConnectionManager(namedValues);  
                if (System.Net.Dns.GetHostName().ToUpper() == serverName.ToUpper())  
                {  
                    connection.Connect(serverName);  
                }  
                else  
                {  
                    connection.Connect(serverName, userName, userPassword);  
                }  
                return connection;  
            }  
            catch (SmsException ex)  
            {  
                Console.WriteLine("Failed to connect. Error: " + ex.Message);  
                return null;  

            }  
            catch (UnauthorizedAccessException ex)  
            {  
                Console.WriteLine("Failed to authenticate. Error:" + ex.Message);  
                throw;  
            }  
        }  

        public void ListPackages(WqlConnectionManager connection)  
        {  
            try  
            {  
                // This query selects all packages (instances of SMS_Package).  
                string query = "SELECT * FROM SMS_Package";  

                // Run query, which populates 'listOfPackages' with a collection of package objects.   
                IResultObject listOfPackages = connection.QueryProcessor.ExecuteQuery(query);  

                // Output header for list of distribution points.  
                Console.WriteLine(" ");   
                Console.WriteLine("List of packages:  ");  
                Console.WriteLine("-------------------");  

                // Enumerate through the collection of objects returned by the query.  
                foreach (IResultObject package in listOfPackages)  
                {  
                    // Output the package name for each package object.  
                    Console.WriteLine("Package ID: {0} Package Name: {1}", package["PackageID"].StringValue, package["Name"].StringValue);    
                }  
            }  
            catch (SmsException ex)  
            {  
                Console.WriteLine("Failed to list packages. Error: " + ex.Message);  
                throw;  
            }  
        }  

        public void CreatePackage(WqlConnectionManager connection, string newPackageName, string newPackageDescription)  
        {  
            try  
            {  
                // Create new package object.  
                IResultObject newPackage = connection.CreateInstance("SMS_Package");  

                // Populate new package properties.  
                newPackage["Name"].StringValue = newPackageName;  
                newPackage["Description"].StringValue = newPackageDescription;  

                // Save the new package and the new package properties.  
                newPackage.Put();  
                // The key value 'PackageID' is created on the put, so getting the package object to output the unique 'PackageID' ('Name' is not guaranteed to be unique).   
                newPackage.Get();  

                // Output new package name.  
                Console.WriteLine("Created Package ID: {0} Package Name: {1}", newPackage["PackageID"].StringValue, newPackage["Name"].StringValue);    
            }  
            catch (SmsException ex)  
            {  
                Console.WriteLine("Failed to create package. Error: " + ex.Message);  
                throw;  
            }  
        }  

        public void ModifyPackage(WqlConnectionManager connection, string existingPackageID)  
        {  
            try  
            {  
                // Get the specific package instance to modify (PackageID is a key value).   
                IResultObject packageToModify = connection.GetInstance(@"SMS_Package.PackageID='" + existingPackageID + "'");  

                // Modify a package properties (in this case description).  
                packageToModify["Description"].StringValue = "This package has been modified. " + packageToModify["Description"].StringValue;  

                // Save the new package and the new package properties.  
                packageToModify.Put();  
            }  
            catch (SmsException ex)  
            {  
                Console.WriteLine("Failed to delete package. Error: " + ex.Message);  
                throw;  
            }  
        }  

        public void DeletePackage(WqlConnectionManager connection, string existingPackageID)  
        {  
            try  
            {                  
                // Get the specific package instance to delete (PackageID is a key value).   
                IResultObject packageToDelete = connection.GetInstance(@"SMS_Package.PackageID='" + existingPackageID + "'");  

                // Output package ID and name being deleted.  
                Console.WriteLine("Deleting Package ID: {0} Package Name: {1}", packageToDelete["PackageID"].StringValue, packageToDelete["Name"].StringValue);       

                // Delete the package.  
                packageToDelete.Delete();             
            }  
            catch (SmsException ex)  
            {  
                Console.WriteLine("Failed to delete package. Error: " + ex.Message);  
                throw;  
            }  
        }  

    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|`newPackageName`|-   Managed: `String`|The name of the new package.|  
|`newPackageDescription`|-   Managed: `String`|The description for the new package.|  
|`existingPackageID`|-   Managed: `String`|An existing Package identifier. This is a key value for the `SMS_Package` class and is used to return a specific instance of the `SMS_Package` class. The ListPackages method in the sample above returns the names and PackageIDs of the current package instances.|  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 System  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

 mscorlib  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## See Also  
 [Configuration Manager Software Distribution](../../../develop/core/servers/configure/software-distribution.md)   
 [Software Distribution Packages](../../../develop/core/servers/configure/software-distribution-packages.md)   
 [UPDATED: SMS_Package Server WMI Class](../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)   
 [Getting Started with Configuraiton Manager Programming](../../../develop/core/understand/getting-started-with-configuration-manager-programming.md)
