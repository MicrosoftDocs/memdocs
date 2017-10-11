---
title: "SMS_Collection Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: 7b900446-4a60-4343-9f8b-2d6ecc7ac951searchScope: - ConfigMgr SDK
caps.latest.revision: 30
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_Collection Server WMI Class
The `SMS_Collection` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents a collection of resources related logically by rules, along with collection information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Collection : SMS_BaseClass   
{   
   String CollectionID;   
   SMS_CollectionRule CollectionRules[];   
   UInt32 CollectionType;   
   SInt32 CollectionVariablesCount;   
   String Comment;   
   UInt32 CurrentStatus;  
   Boolean HasProvisionedMember;   
   SInt32 IncludeExcludeCollectionsCount;   
   Boolean IsBuiltIn;   
   Boolean IsReferenceCollection;  
   UInt8 ISVData[];   
   UInt32 ISVDataSize;   
   String ISVString;  
   DateTime LastChangeTime;   
   DateTime LastMemberChangeTime;   
   DateTime LastRefreshTime;   
   String LimitToCollectionID;   
   String LimitToCollectionName;   
   SInt32 LocalMemberCount;   
   String MemberClassName;   
   SInt32 MemberCount;   
   UInt32 MonitoringFlags;   
   String Name;   
   Boolean OwnedByThisSite;   
   SInt32 PowerConfigsCount;   
   SMS_ScheduleToken RefreshSchedule[];   
   UInt32 RefreshType;   
   Boolean ReplicateToSubSites;   
   SInt32 ServiceWindowsCount;   
   Boolean UseCluster;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_Collection` class.  

|Method|Description|  
|------------|-----------------|  
|[AddMembershipRule Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/addmembershiprule-method-in-class-sms_collection.md)|Adds one new rule to the `CollectionRules` property of `SMS_Collection`.|  
|[AddMembershipRules Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/addmembershiprules-method-in-class-sms_collection.md)|Adds multiple new rules to the `CollectionRules` property of `SMS_Collection`.|  
|[AMTOperateForCollection Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/amtoperateforcollection-method-in-class-sms_collection.md)|Runs an Active Management Technology (neAMT) operation on this collection.|  
|[AMTOperateForMachines Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/amtoperateformachines-method-in-class-sms_collection.md)|Runs an AMT operation on a set of computers.|  
|[ApproveClients Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/approveclients-method-in-class-sms_collection.md)|Approves specified client computers to join the site.|  
|[BlockClients Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/blockclients-method-in-class-sms_collection.md)|Blocks specified client computers from communicating with the site.|  
|[ChangeOwnership Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/changeownership-method-in-class-sms_collection.md)|Changes ownership of machines to a device owner.|  
|[ClearDeploymentLocksForCollection Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/cleardeploymentlocksforcollection-method-in-class-sms_collection.md)|Clears deployment locks for a selected collection.|  
|[ClearDeviceCategory Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/cleardevicecategory-method-in-class-sms_collection.md)|Clears a category from a set of devices.|  
|[ClearLastNBSAdvForCollection Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/clearlastnbsadvforcollection-method-in-class-sms_collection.md)|Clears the last Network Boot advertisement for a selected collection.|  
|[ClearLastNBSAdvForMachines Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/clearlastnbsadvformachines-method-in-class-sms_collection.md)|Clears the last Network Boot advertisement for selected client computers.|  
|[ClientEditions Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/clienteditions-method-in-class-sms_collection.md)|Retrieves a list of client editions.|  
|[CreateCCR Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/createccr-method-in-class-sms_collection.md)|Creates a client configuration request (CCR) for a particular resource.|  
|[CreateCCRs Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/createccrs-method-in-class-sms_collection.md)|Generates client configuration requests (CCRs) for the computers in the collection.|  
|[DeleteAllMembers Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/deleteallmembers-method-in-class-sms_collection.md)|Deletes all members, that is, resources and discovery data, for the collection.|  
|[DeleteMembershipRule Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/deletemembershiprule-method-in-class-sms_collection.md)|Deletes a membership rule from the collection.|  
|[DeleteMembershipRules Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/deletemembershiprules-method-in-class-sms_collection.md)|Deletes multiple membership rules from the collection.|  
|[FindResourceSite Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/findresourcesite-method-in-class-sms_collection.md)|Gets site code information for a computer from SQL.|  
|[FindMachineSite Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/findmachinesite-method-in-class-sms_collection.md)|Gets site code information for resources from SQL.|  
|[GetNumResults Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/getnumresults-method-in-class-sms_collection.md)|Gets a count of all members in a collection, excluding subcollections.|  
|[GenerateCCRByName Method in Class SMS_Collecton](../../../../../develop/reference/core/clients/collections/generateccrbyname-method-in-class-sms_collecton.md)|Generates a client configuration request by computer name.|  
|[GetTotalNumResults Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/gettotalnumresults-method-in-class-sms_collection.md)|Gets a count of all members in a collection, including subcollections.|  
|[ReassignClientsToSite Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/reassignclientstosite-method-in-class-sms_collection.md)|Reassigns the site for the clients in the list.|  
|[RequestRefresh Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/requestrefresh-method-in-class-sms_collection.md)|Triggers a re-evaluation of collection membership by the System Center Configuration Manager collection evaluator component.|  
|[SetDeviceCategory Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/setdevicecategory-method-in-class-sms_collection.md)|Assigns a category to a set of devices.|  
|[SetMemberOrder Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/setmemberorder-method-in-class-sms_collection.md)|Sets the order of the members of a collection.|  
|[UpdateVisibilityInEPDashBoard in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/updatevisibilityinepdashboard-in-class-sms_collection.md)|Show this collection in the EndPoint Protection dashboard.|  
|[VerifyNoCircularDependencies Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/verifynocirculardependencies-method-in-class-sms_collection.md)|Verifies that no circular dependencies are formed if one collection is the parent of another.|  

## Properties  
 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Unique auto-generated ID containing eight characters. The default value is "".  

 The format of the collection ID is the site code that created the collection followed by a five-digit hexadecimal serial number, for example, "JAX0002C". The default Configuration Manager collections, created during the installation, use the "SMS" prefix, for example, "SMS00001".  

 `CollectionRules`  
 Data type: `SMS_CollectionRule` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 SMS_CollectionRule Server WMI Class objects defining the membership criteria for the collection.  

 `CollectionType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, enumeration]  

 Count of collection variables.  

|||  
|-|-|  
|0|OTHER|  
|1|USER|  
|2|DEVICE|  

 `CollectionVariablesCount`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of collection variables.  

 `Comment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 General comment or note that documents the collection. The default value is "".  

 `CurrentStatus`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, enumeration]  

 Current status of the collection. Possible values are:  

|||  
|-|-|  
|0|NONE|  
|1|READY|  
|2|REFRESHING|  
|3|SAVING|  
|4|EVALUATING|  
|5|AWAITING_REFRESH|  
|6|DELETING|  
|7|APPENDING_MEMBER|  
|8|QUERYING|  

 `HasProvisionedMember`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if this collection has provisioned members.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `IncludeExcludeCollectionsCount`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of collections that are included and excluded with this one.  

 `IsBuiltIn`  
 Data type: `Boolean`  

 Access type: Read-Only  

 Qualifiers: [read]  

 This value, when set to true, denotes that the collection is built in.  

 `IsReferenceCollection`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 This value, when set to true, denotes that the collection is not limited by another collection.  

 `ISVData`  
 Data type: `UInt8[]`  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 A data space for Partner extensibility.  

 `ISVDataSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The ISVData size.  

 `ISVString`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 A string for Partner extensibility.  

 `LastChangeTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time of when the collection was last altered in any way.  

 `LastMemberChangeTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time of when the collection membership was last altered.  

 `LastRefreshTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time of when the collection membership was last refreshed.  

 `LimitToCollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The CollectionID of the collection to limit the query results to.  

 `LimitToCollectionName`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 The Name of the collection to limit the query results to.  

 `LocalMemberCount`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of members visible at the local site.  

 `MemberClassName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Class name having instances that are the members of the collection. The collection membership is not contained in `SMS_Collection` but is instead contained in the class name specified by this property. The class name is generated dynamically and is derived from [SMS_CM_RES_COLL_CollectionID Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_cm_res_coll_collectionid-server-wmi-class.md).  

 `MemberCount`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 A count of the collection members.  

 `MonitoringFlags`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Enables the collection for certain kinds of monitoring.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_null]  

 The name of the collection. This value represents the collection in the System Center Configuration Manager console and should be unique. The default value is "New Collection".  

 `OwnedByThisSite`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifier: None  

 `true` if the collection originated at the local Configuration Manager site. The default value is `false`.  

 `PowerConfigsCount`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifier: [read]  

 A count of the power configurations.  

 `RefreshSchedule`  
 Data type: `SMS_ScheduleToken` Array  

 Access type: Read/Write  

 Qualifiers: [max(15), lazy]  

 [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md) objects indicating an update or refresh schedule for the collection. The collection membership is only updated if your application specifies a schedule or calls the [RequestRefresh Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/requestrefresh-method-in-class-sms_collection.md) method. For the collection evaluator to use the schedule, the `RefreshType` property must be set to PERIODIC.  

 `RefreshType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy, enumeration]  

 Refresh type indicating how Configuration Manager refreshes the collection. Possible values are listed below. The default value is MANUAL (1).  

|||  
|-|-|  
|1|MANUAL|  
|2|PERIODIC|  
|4|CONSTANT_UPDATE|  

 Set this property to PERIODIC to base the refresh on the schedule specified in `RefreshSchedule`. A setting of MANUAL manually updates the collection by using the [RequestRefresh Method in Class SMS_Collection](../../../../../develop/reference/core/clients/collections/requestrefresh-method-in-class-sms_collection.md).  

 `ReplicateToSubSites`  
 This property is not implemented.  

 `ServiceWindowsCount`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of maintenance windows.  

 `UseCluster`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 Specifies that this collection is a server group.  

## Remarks  
 Class qualifiers for this class include:  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Collection information represented by this class includes the refresh schedule and the members, represented by [SMS_CM_RES_COLL_CollectionID Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_cm_res_coll_collectionid-server-wmi-class.md) objects. Your application can use a collection to target resources for software distribution.  

 When you run a query against a dynamic collection represented by `SMS_Collection`, ensure that the SMS Provider is loaded or that another method or query has already run.  

 The application should use the `SMS_Collection` methods to add, update, or delete membership rules defined by the `CollectionRules` property. This property is not retrieved when your application enumerates `SMS_Collection`. To obtain the collection rules for a collection, your application must use `IWbemServices::GetObject` or `SWbemServices::Get`. For more information, see Configuration Manager Context Qualifiers.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CollectionRule Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionrule-server-wmi-class.md)   
 [Configuration Manager Collections Server WMI Classes](../../../../../develop/reference/core/clients/collections/collections-server-wmi-classes.md)
