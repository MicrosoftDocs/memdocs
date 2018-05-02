---
title: "Deploy a Site System Role"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e9e44ed6-c85e-44b6-9446-3e859c3bfcc4
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Deploy a Site System Role (Example:  Fallback Status Point)
The features and capabilities of a site are determined by the site roles applied to it. A site can contain one or more site roles. Some roles depend on other roles. For more information about specific site roles see [Configure sites and hierarchies for System Center Configuration Manager](https://technet.microsoft.com/en-us/library/mt621987.aspx).  

 Configuring a site is performed through Windows Management Instrumentation (WMI) classes. For example, [SMS_SCI_Component Server WMI Class](../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md) holds information about the server components stored on a Configuration Manager site server. These classes derive from [SMS_SiteControlItem Server WMI Class](../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md). For more information, see [Configuration Manager Site Configuration Server WMI Classes](../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md).  

> [!NOTE]
>  In earlier versions of Configuration Manager, the `SMS_SiteControlFile` WMI class  was used to receive the latest copy of a site’s configuration, to update a site’s configuration, and to manage update sessions. This is no longer required as the changes that are made to a site’s configuration are immediately written to the database and a file is no longer used.  

 Site control items generally use three types’ properties for individual settings, embedded properties, property lists, and multi-string lists. They are accessed by using the following classes:  

|Type|WMI Class|  
|----------|---------------|  
|Embedded property|[SMS_EmbeddedProperty Server WMI Class](../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md)|  
|Embedded property list|[SMS_EmbeddedPropertyList Server WMI Class](../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md) (array)|  
|Multi-string list|[SMS_Client_Reg_MultiString_List Server WMI Class](../../../develop/reference/core/servers/configure/sms_client_reg_multistring_list-server-wmi-class.md) (array)|  

### To deploy a site role  

1.  Set up a connection to the SMS Provider.  

2.  Create an instance of the `SMS_SCI_SysResUse` WMI class  

3.  Set the `NALPath`, `NALType`, `RoleName`, and `Sitecode` properties.  

4.  Depending on the role chosen, set the correct embedded properties or embedded property list values.  

5.  Save the role.  

## Example  
 The following example creates a `Fallback Status Point` role:  

```vbs  
Sub CreateRole(connection, computerName, siteCode, domainName)    Dim role    Dim props    ' Create an instance of the class that defines a role    Set role = connection.Get("SMS_SCI_SysResUse").SpawnInstance_()    ' Configure the basic information of a role    role.NALPath  = "[""Display=\\" &  computerName & "." & domainName & "\""]MSWNET:[""SMS_SITE=" & siteCode & """]\\" & computerName & "." & domainName & "\"    role.NALType  = "Windows NT Server"    role.RoleName = "SMS Fallback Status Point"    role.Sitecode = siteCode    ' Initialize the properties array    props = Array()    ' Add each required property to the array    SetProperty connection, props, "FSPInternetFacing", 0, "", ""    SetProperty connection, props, "Throttle Count", 10000, "", ""    SetProperty connection, props, "Throttle Interval", 3600000, "", ""    SetProperty connection, props, "Server Remote Name", 0, computerName & "." & domainName, ""    ' Set the role's properties and commit the role    role.Props = props    role.Put_    ' Cleanup    Set role = Nothing    Set props = NothingEnd SubSub SetProperty(connection, propsArray, propertyName, intValue, strValue1, strValue2)    Dim index    Dim foundProperty    Dim newProperty    foundProperty = False    ' Loop through properties until a match is found and then set the properties using the values passed in.    For index = 0 to UBound(propsArray)        If propsArray(index).PropertyName = propertyName then            foundProperty = true            propsArray(index).Value = intValue            propsArray(index).Value1 = strValue1            propsArray(index).Value2 = strValue2            Exit For        End if    Next    ' If the property does not exist, then create it and set the property values using the values passed in.    If not foundProperty then        Set newProperty = connection.Get("SMS_EmbeddedProperty").SpawnInstance_        newProperty.PropertyName = propertyName        newProperty.Value = intValue        newProperty.Value1 = strValue1        newProperty.Value2 = strValue2        ReDim Preserve propsArray(UBound(propsArray) + 1)        Set propsArray(UBound(propsArray)) = newProperty     End if    ' Cleanup    Set newProperty = NothingEnd Sub  
```  

```c#  
public void CreateRole(WqlConnectionManager connection, string computerName, string siteCode, string domainName){    IResultObject role = connection.CreateInstance("SMS_SCI_SysResUse");    string fqdn = computerName + "." + domainName;    role.Properties["NALPath"].StringValue = string.Format(@"[""Display=\\{0}\""]MSWNET:[""SMS_SITE={1}""]\\{0}\", fqdn, siteCode);    role.Properties["NALType"].StringValue = "Windows NT Server";    role.Properties["RoleName"].StringValue = "SMS Fallback Status Point";    role.Properties["Sitecode"].StringValue = siteCode;    WriteEmbeddedProperty(role, "FSPInternetFacing", 0, "", "");    WriteEmbeddedProperty(role, "Throttle Count", 10000, "", "");    WriteEmbeddedProperty(role, "Throttle Interval", 3600000, "", "");    WriteEmbeddedProperty(role, "Server Remote Name", 0, fqdn, "");    role.Put();}public void WriteEmbeddedProperty(IResultObject container, string propertyName, int value, string value1, string value2){    // Get the property, or create it.    IResultObject newProperty;    Dictionary<string, IResultObject> propertiesCopy = container.EmbeddedProperties;    if (propertiesCopy.ContainsKey(propertyName))    {        newProperty = propertiesCopy[propertyName];    }    else    {        newProperty = container.ConnectionManager.CreateEmbeddedObjectInstance("SMS_EmbeddedProperty");        propertiesCopy.Add(propertyName, newProperty);    }    newProperty["PropertyName"].StringValue = propertyName;    newProperty["Value"].IntegerValue = value;    newProperty["Value1"].StringValue = value1;    newProperty["Value2"].StringValue = value2;    container.EmbeddedProperties = propertiesCopy;}  
```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`computerName`|`String`|The name of the site server.|  
|`siteCode`|`String`|The site code.|  
|`domainName`|`String`|The fully qualified domain name of the site server.|  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 System.Collections.Generic  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## See Also  
 [SMS_EmbeddedProperty Server WMI Class](../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md)   
 [SMS_SCI_SysResUse Server WMI Class](../../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md)   
 [Configuration Manager Site Control File](../../../develop/core/understand/site-control-file.md)
