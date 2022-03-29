---
description: Learn how to display Configuration Manager actions by specified conditions such as Regular expressions, method calls, or security permissions.
title: "Conditional Actions"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f9e46b28-e6dc-48c8-aa0e-24079774d129
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Configuration Manager Conditional Actions
Configuration Manager actions can be displayed according to specified conditions. The conditions are defined by the following:  

-   Regular expressions  

-   Method calls  

-   Security permissions  

## Regular Expressions  
 Regular expressions allow you to apply string-based search patterns. The following elements specify a regular expression for an action:  

|Element|Description|  
|-------------|-----------------|  
|`MatchPattern`|Specifies the pattern to search for.|  
|`MatchValueToTest`|Specifies the value to compare against. The value following `##Sub` is a property on the selected object. The property must not be lazy and must exist on the select object.|  

 The following action displays a dialog box whenever the specified pattern (MS_ASYNC_RAS) matches the selected object's `AddressType` property:  

```  
<ActionDescription ActionVerb="Properties" Class="ShowDialog">  <ShowOn>  <string>DefaultContextualTab</string> <!-- Show on Ribbon -->           <string>ContextMenu</string> <!-- Show on Context Menu -->   </ShowOn>  <MatchPattern>MS_ASYNC_RAS</MatchPattern>  
 <MatchValueToTest>##SUB:AddressType##</MatchValueToTest>  
 <DialogId>AsyncRasSenderAddress</DialogId></ActionDescription>  
```  

## Method Calls  
 An action can be shown depending on the result of a method call. The `ActionDescription` child element `ActionStateAssembly` defines the assembly, type, and method to be called. If the method returns `true`, the action is shown; if the method returns `false`, the action is hidden.  

 The following XML calls a method named `EnableDecrementPriorityMenu` in the assembly AdminUI.Addresses.dll:  

```  
<ActionDescription>  
 <ShowOn>  
    <string>DefaultContextualTab</string> <!-- Show on Ribbon -->         <string>ContextMenu</string><!-- Show on Context Menu --> </ShowOn> <ActionStateAssembly>  
  <Assembly>AdminUI.Addresses.dll</Assembly>   <Type>Microsoft.ConfigurationManagement.AdminConsole.Addresses.AddressUtilityClass</Type>  
  <Method>EnableDecrementPriorityMenu</Method> </ActionStateAssembly>  
</ActionDescription>  
```  

 The method is implemented in a .NET Framework assembly with the following signature:  

 `public static bool EnableDecrementPriority(object sender, ScopeNode scopeNode, ActionDescription action, ResultObjectBase resultObject)`  

 For more information about calling methods in a .NET Framework assembly, see [Configuration Manager AssemblyType Action](../../../../develop/core/servers/console/assemblytype-action.md).  

## Security Permissions  
 You can restrict the availability of an action by applying security restrictions to the selected object or object class.  

### Object Instance Permissions  
 You can restrict the availability of an action by applying required permissions to the selected object. In the following XML example, the following elements specify the instance permissions for the selected object:  

|Element|Description|  
|-------------|-----------------|  
|`InstancePermissions`|The parent element to the list of instance permissions.|  
|`SecurityFlagsDetailDescription`|The security flags that must be set for the action to work.|  

 In the following XML example, the `Delete` action for a selected object is available only if the user has modify permissions:  

```  
<ActionDescription ActionVerb="Delete" Class="Default" SelectionMode="Both" InstanceDependsOn="SMS_Site">  
<ShowOn> <string>DefaultContextualTab</string> <!-- Show on Ribbon -->    <string>ContextMenu</string> <!-- Show on Context Menu --></ShowOn><InstancePermissions><SecurityFlagsDetailDescription BitName="Modify" BitValue="2" DependsOn="1" /></InstancePermissions>  
</ActionDescription>  
```  

### Object Class Permissions  
 You can use the `ClassPermissions` element to set the object class permissions required for an action. [ActionSecurityDescription](/previous-versions/system-center/developer/cc147257(v=msdn.10)) describes the object class and the required permissions for that object class. The following XML example describes the permissions required for SMS collections:  

```  
<ClassPermissions> <ActionSecurityDescription ClassObject="SMS_Collection" RequiredPermissions="1280" />  
</ClassPermissions>  
```  

### Permission Values  
 The permission values for the [RequiredPermissions](/previous-versions/system-center/developer/cc146816(v=msdn.10)) attribute are the same as for the [SecurityFlagsDetailDescription](/previous-versions/system-center/developer/cc147286(v=msdn.10)) class and are as follows:  

|Permission|Values|Depends on|  
|----------------|------------|----------------|  
|Read|1|None|  
|Modify|2|1|  
|Delete|4|1|  
|Distribute|8|1|  
|CreateChild|16|1|  
|RemoteControl|32|None|  
|Advertise|64|1|  
|ModifyResource|128|1|  
|Administer|256|7|  
|DeleteResource|512|1|  
|Create|1024|None|  
|ViewCollectedFiles|2048|1|  
|ReadResource|4096|1|  
|Delegate|8192|None|  
|Meter|16384|1|  
|ManageSqlCommand|32768|1|  
|ManageStatusFilter|65536|1|  
|ManageFolder|131072|1|  
|NetworkAccess|262144|1|  
|ImportMachineEntry|524288|1|  
|CreateMediaCertificate|1048576|1|  
|ModifyCollectionSetting|2097152|1|  
|ManageOsdCertificate|4194304|1|  

## See Also  
 [Configuration Manager Actions](../../../../develop/core/servers/console/configuration-manager-actions.md)   
 [Configuration Manager Action XML](../../../../develop/core/servers/console/configuration-manager-action-xml.md)   
 [Configuration Manager AssemblyType Action](../../../../develop/core/servers/console/assemblytype-action.md)   
 [Configuration Manager Executable Action](../../../../develop/core/servers/console/executable-action.md)   
 [Configuration Manager Group Action](../../../../develop/core/servers/console/group-action.md)   
 [Configuration Manager Report Action](../../../../develop/core/servers/console/report-action.md)   
 [Configuration Manager ShowDialog Action](../../../../develop/core/servers/console/showdialog-action.md)   
 [How to Create a Configuration Manager Action](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-action.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)
