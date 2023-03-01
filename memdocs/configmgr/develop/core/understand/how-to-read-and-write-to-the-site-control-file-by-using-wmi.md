---
title: Read and Write to the Site Control File by Using WMI
titleSuffix: Configuration Manager
description: In Configuration Manager, you write to the site control file using Windows Management Instrumentation (WMI) by using the `SMS_SiteControlFile` class methods.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 815a4ee8-b211-48de-ba9f-6eff7497dd2b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Read and Write to the Configuration Manager Site Control File by Using WMI
In Configuration Manager, you write to the site control file using Windows Management Instrumentation (WMI) by using the `SMS_SiteControlFile` class methods.  

 When writing to the site control file by using WMI, you use a session handle to identify your application. This is used to manage concurrent updates to the file.  

 When you have finished writing to the site control file, you must commit your changes.  

 [SMS_SiteControlFile](../../../develop/reference/core/servers/configure/sms_sitecontrolfile-server-wmi-class.md) has the following methods to manage changes to the site control file.  

|Method|Description|  
|------------|-----------------|  
|`CommitSCF`|Applies your changes to the Configuration Manager database.|  
|`RefreshSCF`|Refreshes your in-memory copy of the site control file with any recent changes from the Configuration Manager database.|  
|`GetSessionHandle`|Gets your in-memory copy of the site control file and a session handle. You place the session handle in an `IWbemContext` object that is passed to all `IWbemServices` methods.|  
|`ReleaseSessionHandle`|Releases your in-memory copy of the site control file and any resources associated with your session handle.|  

> [!CAUTION]
>  You should be experienced in managing a site's configuration before using the SMS Provider classes to modify the site configuration. You can cause great harm to a site by changing some configurable items. You should use extreme caution or avoid using the `SMS_SCI_FileDefinition` and `SMS_SCI_SiteDefinition` classes altogether. These classes manage the site control file itself. If you are not careful, you can render the site useless.  

### To write to the site control file  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](sms-provider-fundamentals.md).  

2.  Create a `SWbemNameValue` value set to hold your context data.  

3.  Get a session handle from `SMS_SiteControlFile` class `GetSessionHandle`.  

4.  Add the session handle to your context data.  

5.  Call the `SMS_SiteControlFile` object `RefreshSCF` to get the latest copy of the site control file. Use the context data in the call.  

6.  Query for the site control file resource you want to update using your context data.  

7.  Update the resource using your context data.  

8.  Commit your changes to the site control file using the `SMS_SiteControlFile` object `CommitSCF` method.  

9. Call the `SMS_SiteControlFile` object `ReleaseSessionHandle` method to release your session handle.  

## Example  
 The following VBScript example access the client agent component of the site control file and creates a dummy property, property list and multi-string list. It then removes the updates that were made. The example demonstrates how to set up the session handle, get the site control file, query the site control file, make updates and commit changes to the site control file.

 In the example, the `LocaleID` property is hard-coded to English (U.S.). If you need the locale for non-U.S. installations, you can get it from the [SMS_Identification Server WMI Class](../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md) `LocaleID` property.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub ReadWriteScf(connection, siteCode)  

    Dim context  
    Dim query  
    Dim resource  
    Dim resources  
    Dim inParams  

    Set context = CreateObject("WbemScripting.SWbemNamedValueSet")  

    ' Add the standard SMS context qualifiers to the context object.  
    context.Add "LocaleID", "MS\1033"  
    context.Add "MachineName", "MyMachine"  
    context.Add "ApplicationName", "MyApp"  

    ' Add the session handle.  
    context.Add "SessionHandle", _  
         connection.ExecMethod("SMS_SiteControlFile", "GetSessionHandle").SessionHandle  

   ' Load site control file.  
       Set inParams = connection.Get("SMS_SiteControlFile").Methods_("RefreshSCF").InParameters.SpawnInstance_  
InParams.SiteCode = siteCode  
connection.ExecMethod "SMS_SiteControlFile", "RefreshSCF", inParams, , context  

    ' Query for the client agent component.  
    query = "SELECT * FROM SMS_SCI_ClientComp " & _  
            "WHERE ClientComponentName = 'Client Agent' " & _  
           "AND SiteCode = '" & siteCode & "'"  

    Set resources = connection.ExecQuery(query, , , context)             

    For each resource in resources  

    ' Embedded property.  

        WScript.Echo "Embedded property"  
        Wscript.Echo "-----------------"  

        Dim value  
        Dim value1  
        Dim value2  

        Call WriteScfEmbeddedProperty(connection,context,resource,"Test2",20,"Hello","World")  

        If  GetScfEmbeddedProperty(resource,"Test2",value,value1,value2) = True Then  
            Wscript.Echo "Value: " + CStr(value)  
            WScript.Echo "Value1: " + value1  
            WScript.Echo "Value2: " + value2  
        End If  

        WScript.Echo   
        dim n,l  
        dim updatedProps   
        Dim scfProp  

        n = 0  
        ' Remove the property.  
        For l = 0 To UBound (resource.Props)   

            ' Copy each element except the one to delete.  
            If resource.Props(l).PropertyName <> "Test2" Then  
                Dim embeddedProperty  
                Set embeddedProperty = connection.Get("SMS_EmbeddedProperty").Spawninstance_()  
                If l = 0 Then  
                    ' Create an array to copy to.  
                    updatedProps = array(embeddedProperty)  
                    Redim updatedProps(Ubound(resource.Props)-1)  
                End If  
                ' Copy the element.  
                embeddedProperty.PropertyName = resource.Props(l).PropertyName  
                embeddedProperty.Value = resource.Props(l).value  
                embeddedProperty.Value1 = resource.Props(l).value1  
                embeddedProperty.Value2 = resource.Props(l).value2  

                Set updatedProps(n) = embeddedProperty  
                n = n + 1  
          End If    
        Next    

        ' Update  
        resource.Props = updatedProps  
        resource.Put_, context  

        WScript.Echo         

        ' Check that the property has been deleted.   
        If  GetScfEmbeddedProperty(resource,"Test2",value,value1,value2) = True Then  
            WScript.Echo "Property found"  
        Else  
            WScript.Echo "Property not found"  
        End If      

        WScript.Echo   

    ' Embedded property list.  

        WScript.Echo "Embedded property list"  
        WScript.Echo "----------------------"  

        Dim values  
        values = Array("Tiger","Wolf")  

        Call WriteScfEmbeddedPropertyList(connection,context,resource,"Animals",values)  

        Dim retrievedValues   

        If GetScfEmbeddedPropertyList(resource,"Animals",retrievedValues) = True Then  
            Dim i,c  
            Dim updatedValues  

            c = 0   

            ' Display the list and remove the property Tiger.  
            updatedValues = Array(UBound(retrievedValues)-1)  
            For i = 0 To  UBound (retrievedValues)  
                 Wscript.Echo retrievedValues(i)  
                 If retrievedValues(i) <> "Tiger" Then  

                    updatedValues(c) = retrievedValues(i)  
                    c = c + 1  
                 End If     
            Next  

            WScript.Echo  
            ' Update the property list.  
            Call WriteScfEmbeddedPropertyList(connection,context,resource,"Animals",updatedValues)  

            ' Get the property list and display.  
            Call GetScfEmbeddedPropertyList(resource,"Animals",retrievedValues)  

            For i = 0 To  UBound (retrievedValues)  
                 Wscript.Echo retrievedValues(i)  
             Next  
        Else  
            WScript.Echo "Not found"  
        End If   

        WScript.Echo          

    ' RegMultiString list.          

        WScript.Echo "Embedded RegMultiString list"  
        WScript.Echo "----------------------------"  

        Dim valueStrings  
        valueStrings= Array("Lisa","Julie")  

        ' Write the RegMultiString list.  
        Call WriteScfRegMultiStringList(connection,context,resource,"Names2",valueStrings)  

        Dim retrievedValueStrings   

        ' Get the RegMultiString list.            
        If GetScfRegMultiStringList(resource,"Names2",retrievedValueStrings) = True Then  

            Dim updatedValueStrings  

            c = 0   
            updatedValueStrings = Array(Ubound(retrievedValueStrings)-1)  
            For i = 0 To UBound (retrievedValueStrings)  
                 Wscript.Echo retrievedValueStrings(i)  
                 if retrievedValueStrings(i) <> "Lisa" Then  
                    updatedValueStrings(c) = retrievedValueStrings(i)  
                 End If  
            Next   

            Call WriteScfRegMultiStringList(connection,context,resource,"Names",updatedValueStrings)  

            WScript.Echo   

            Call GetScfRegMultiStringList(resource,"Names",retrievedValueStrings)  

            For i = 0 To UBound (retrievedValueStrings)  
                 Wscript.Echo retrievedValueStrings(i)  
             Next   
        Else  
            WScript.Echo "Not found"              
        End If     
    Next  

    ' Commit the changes.  
    Set inParams = connection.Get("SMS_SiteControlFile").Methods_("CommitSCF").InParameters.SpawnInstance_  
    inParams.SiteCode = siteCode  
    connection.ExecMethod "SMS_SiteControlFile", "CommitSCF", inParams, , context  

    ' Release the session handle.  
    Set inParams = connection.Get("SMS_SiteControlFile").Methods_("ReleaseSessionHandle").InParameters.SpawnInstance_  
    inParams.SessionHandle = context.Item("SessionHandle")  
    connection.ExecMethod "SMS_SiteControlFile", "ReleaseSessionHandle", inParams    
End Sub  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`siteCode`|-   `String`|The site code for the Configuration Manager site.|  

## Compiling the Code  
 This C# example requires:  

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
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page)   
 [About the Configuration Manager Site Control File](../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read a Configuration Manager Site Control File Embedded Property List](../../../develop/core/understand/how-to-read-a-configuration-manager-site-control-file-embedded-property-list.md)
