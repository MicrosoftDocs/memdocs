---
title: "Encrypt Passwords or Data for a Site"
titleSuffix: "Configuration Manager"
description: "Encrypt Passwords or Data for a Site. Using a new WMI method, the user accounts' passwords can be encrypted for a specific site."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: c640a87a-9eb6-400d-b9e2-eb71d265f50e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Encrypt Passwords or Data for a Site
In Configuration Manager, user accounts connect to site systems and Active Directory to perform various tasks. Prior to System Center 2012 Configuration Manager, the Manage Site Accounts tool (MSAC) was used to manage these user accounts. The MSAC tool has been deprecated. Using a new WMI method, these account passwords can be encrypted for a specific site. The following code snipped demonstrates how user account passwords can be encrypted for a specific site.  

### To Encrypt Data for a Site  

1.  Connect to the Configuration Manager site.  

2.  Get the parameters for the [EncryptDataEx Method in Class SMS_Site](../../../develop/reference/core/servers/configure/encryptdataex-method-in-class-sms_site.md) method.  

3.  Add the data to be encrypted to the `Data` parameter.  

4.  Add the site code of the specific site for which the data should be encrypted to the `SiteCode` parameter.  

5.  Encrypt the data for the specified site by invoking the [EncryptDataEx Method in Class SMS_Site](../../../develop/reference/core/servers/configure/encryptdataex-method-in-class-sms_site.md).  

6.  In this case, the encrypted string is output as a test.  

## Example  
 The following example encrypts data for a specific site.  

```  
using System;   
using System.Management;   

namespace Encryption  
{  
    class Program  
    {  
        static void Main(string[] args)   
        {  
            // SMS_Site::EncryptDataEx is a class level method,   
            // it will encrypt data for the site based on passed in site code.  
            try  
            {  
                ManagementScope scope = new ManagementScope(@"root\sms\site_ABC");  
                ManagementClass cls = new ManagementClass(scope.Path.Path, "SMS_Site", null);   
                // Set up input parameters.   
                ManagementBaseObject inParams = cls.GetMethodParameters("EncryptDataEx");  
                inParams["Data"] = @"pass123";  // data to be encrypted  
                inParams["SiteCode"] = @"ABC";  // encrypt the data for that specific site  

                // Get the encrypted data.  
                ManagementBaseObject outSiteParams = cls.InvokeMethod("EncryptDataEx", inParams, null);   

                // print the encrypted data  
                Console.WriteLine(outSiteParams["EncryptedData"].ToString());  
            }  
            catch (ManagementException e)   
            {  
                Console.WriteLine("Failed to execute method {0}", e.ToString());  
            }  
        }  
    }  
}  

```  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 System  

 System.Management  

### Assembly  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  
