---
title: "Delete a State Migration Point Role"
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
ms.assetid: 69475541-e5e3-45c4-8989-142cf986d94csearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Delete a State Migration Point Role
You delete the state migration point role, in System Center Configuration Manager, by deleting the role's [SMS_SCI_SysResUse Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md) object.  

### To delete a state migration point role  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the [SMS_SCI_SysResUse Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md) object for the state migration point role.  

3.  Set the corresponding state migration point to none.  

4.  Delete the state migration point [SMS_SCI_SysResUse Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md) object.  

## Example  
 The following example method deletes the state migration point identified by the site code and network abstraction layer (NAL) path. The example determines whether the state migration point has any incomplete state migration restores in process. If there are any, the current implementation still deletes the state migration point.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```c#  
public void DeleteSmpRole(  
     WqlConnectionManager connection,  
     string siteCode,  
     string nalPath)  
 {  
     try  
     {  
         bool smpFound = false;  
         Console.WriteLine("About to delete the state migration point");  
         string query = string.Format(CultureInfo.InvariantCulture,  
      @"SELECT * from SMS_SCI_SysResUse where SiteCode='{0}' AND FileType=2 AND RoleName='{1}'AND NALPath='{2}'",  
      siteCode,  
      "SMS State Migration Point",  
      nalPath.Replace(@"\", @"\\"));  

         IResultObject resultObjs = connection.QueryProcessor.ExecuteQuery(query);  

         foreach (IResultObject resultObj in resultObjs)  
         {  
             smpFound = true;  
             if (DeleteSmpOK(resultObj) == true)  
             {  
                 resultObj.Delete();  
             }  

             Console.WriteLine("Deleted");  
         }  

         if (smpFound == false)  
         {  
             Console.WriteLine("No state migration point was found");  
         }  
     }  
     catch (SmsException e)  
     {  
         Console.WriteLine("Couldn't delete the state migration point: " + e.Message);  
         throw;  
     }  

 }  

public bool DeleteSmpOK(IResultObject selectedResultObject)  
{  
    IResultObject resultObjs = null;  
    try  
    {  
        // Locate this state migration point, and determine if it is in QuiesceState or not, normal deletion  
        // if it is not.  
        string query = string.Format(CultureInfo.InvariantCulture,  
        @"SELECT * from SMS_SCI_SysResUse where SiteCode='{0}' AND FileType=2 AND NALPath='{1}' AND RoleName='{2}'",  
        selectedResultObject["SiteCode"].StringValue,  
        selectedResultObject["NALPath"].StringValue.Replace(@"\", @"\\"),  
        "SMS State Migration Point");  

        resultObjs = selectedResultObject.ConnectionManager.QueryProcessor.ExecuteQuery(query);  

        // Retrieve the state migration point server name because there could be more than one state migration point on the site, and you want to  
        // determine if there are unrestored data stores on only this one.  
        string smpServer = selectedResultObject["NetworkOsPath"].StringValue;  
        smpServer = smpServer.Replace(@"\", "");  

        foreach (IResultObject resultObj in resultObjs)  
        {  
            if (resultObj.EmbeddedProperties.ContainsKey("SMPQuiesceState") == true &&  
                resultObj.EmbeddedProperties["SMPQuiesceState"].Properties["Value"].IntegerValue != 0)  
            {  
                // Find out whether this state migration point contains any stateMigrationRestores that are incomplete on this  
                // server that is to be deleted.  
                string query2 = string.Format(CultureInfo.InvariantCulture, @"SELECT * from SMS_StateMigration where StorePath Like '%{0}%'", smpServer);  

                IResultObject resultObjs2 = selectedResultObject.ConnectionManager.QueryProcessor.ExecuteQuery(query2);  

                foreach (IResultObject resultObj2 in resultObjs2)  
                {  
                    // Look for state migration objects without a StoreReleaseData/Migration date  
                    // it's the one that will cause an exception when reading releasetime because it is not a valid datetime.  
                    try  
                    {  
                        DateTime releaseTime = resultObj2["StoreReleaseDate"].DateTimeValue;  
                    }  
                    catch (ArgumentOutOfRangeException)  
                    {  
                        // Alternatively return false if you do not to delete.  
                        return true;  
                    }  
                }  
            }  
        }  
    }  
    catch (SmsQueryException ex)  
    {  
        Console.WriteLine("Failed during smp state determination" + ex.Message);  
        throw;  
    }  
    finally  
    {  
        if (resultObjs != null)  
        {  
            resultObjs.Dispose();  
        }  
    }  

    // Delete the role.  
    return true;  
}  
```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|Managed: `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|`siteCode`|Managed: `String`|The Configuration Manager site code.|  
|`nalPath`|Managed: `String`|The NAL path to the state migration point. For example `["Display=\\SERVERNAME\"]MSWNET:["SMS_SITE=SITECODE"]\\SERVERNAME\`|  

## Compiling the Code  
 The C# example has the following compilation requirements:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

 System.Globalization  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [SMS_SCI_SysResUse Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md)   
 [About Operating System Deployment Site Role Configuration](../../develop/osd/about-operating-system-deployment-site-role-configuration.md)   
 [Configuration Manager Operating System Deployment](../../develop/osd/operating-system-deployment.md)   
 [Configuration Manager Programming Fundamentals](../../develop/core/understand/configuration-manager-programming-fundamentals.md)   
 [Operating System Deployment Site Role Configuration](../../develop/osd/operating-system-deployment-site-role-configuration.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)
