---
title: "SMS_PropertyDisplayNode Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: eb11b75c-4a5d-47f5-81cb-8869156fdb1f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_PropertyDisplayNode Server WMI Class
The `SMS_PropertyDisplayNode` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that defines the nodes that are displayed in Resource Explorer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PropertyDisplayNode : SMS_BaseClass  
{  
     String ClassDisplayName;  
     String ClassName;  
     UInt32 Flags;  
     UInt32 NodeKey;  
     String NodeName;  
     UInt32 PaneOrder;  
     UInt32 ParentNodeKey;  
     String ResourceDisplayName;  
     String ResultProperties[];  
     String ResultPropertyIDName;  
     String ScopePropertyIDName;  
     String ScopePropertyNames[];  
};  
```  

## Methods  
 The `SMS_PropertyDisplayNode` class does not define any methods.  

## Properties  
 `ClassDisplayName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Not used.  

 `ClassName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the inventory group class, for example, `SMS_G_System_CDROM`, that is displayed in the scope and details pane. This property is required for leaf nodes. The default value is "".  

 `Flags`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Flags that control the behavior of the node. Possible values are listed below. The default value is Static (0).  

 0  
 Static. Create a static node. Static nodes do not contain data.  

 1  
 RootNode. Create a root node that exists at the same level as the Hardware node in Resource Explorer.  

 2  
 LeafNode. Create a leaf node. Leaf nodes exist as children of user-defined static root nodes or as stand-alone leaf nodes at the top level in Resource Explorer.  

 3  
 HasHistory. Not used.  

 6  
 UserDefined. Create a user-defined node. This value is set for you by the SMS Provider. Do not set this bit.  

 Currently, you must use bits 0 and 1 together, which creates a static root node. The bits cannot be used separately. You can create only one static root node.  

 `NodeKey`  
 Data type: **UInt32**  

 Access type: Read-only  

 Qualifiers: [read, Not_null, key]  

 Node key that is auto-generated if you do not specify a value, which is the preferred behavior. If you do specify a value, it must be unique and greater than 1000. Values of 1000 and less are reserved for Configuration Manager. The default value is 0.  

 `NodeName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the node as displayed in Resource Explorer. This is the literal name of the node, unless a parent node exists and it declares a value for `ScopePropertyNames`. The default value is "".  

 `PaneOrder`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: None  

 Not used.  

 `ParentNodeKey`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: None  

 Value of the `NodeKey` property of the parent node. This property defines the parent-child relationship. Specify a value of 0 to create your node at the top level. The default value is 0.  

 `ResourceDisplayName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Not used.  

 `ResultProperties`  
 Data type: **String** Array  

 Access type: Read/Write  

 Qualifiers: None  

 List of the properties from the class specified in `ClassName` that are displayed in the details pane. The specified property names form the column headings in the details pane.  

 `ResultPropertyIDName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Not used for user-defined nodes. The name of the property to be used in the WHERE clause of the result query. The default value is "".  

 This property limits the result instances, shown in the details pane for the selected node, to those with property values that equal the property value of the selected node. For example, the Manufacturer node under Software groups software by the `CompanyName` property of [SMS_G_System_SoftwareProduct Server WMI Class](../../../develop/reference/core/clients/manage/sms_g_system_softwareproduct-server-wmi-class.md). When a particular manufacturer is selected, the details pane shows the software products for that manufacturer.  

 `ScopePropertyIDName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Not used for user-defined nodes. The name of a property from the class specified in `ClassName`. The value of this property is used for the name of child nodes in the scope pane. If the property is blank, the child nodes use the `NodeName` value. The default value is "".  

 `ScopePropertyNames`  
 Data type: **String** Array  

 Access type: Read/Write  

 Qualifiers: None  

 Not used for user-defined nodes. The list of property names that are concatenated to form the name of the node in the scope pane. This property has similar functionality to and applies the same rules as the `ResultProperties` property, except that the result is the name of the node. The concatenation creates a space between value fields. If this property is blank, the child node uses the `NodeName` value.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Resource Explorer uses the following steps to determine the text to use for the column names. Each step is skipped in turn if the qualifier does not exist.  

1.  Use the string identified by the DisplayName qualifier.  

2.  Use the property name itself.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Resource Management Server WMI Classes](../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)   
 [SMS_G_System_SoftwareProduct Server WMI Class](../../../develop/reference/core/clients/manage/sms_g_system_softwareproduct-server-wmi-class.md)
