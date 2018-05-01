---
title: "SMS_CombinedDeviceResources Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 751f3d1d-5fbe-4d98-aa44-81a4b52969b5
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_CombinedDeviceResources Server WMI Class
The `SMS_CombinedDeviceResources` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents all the device and user resources in the system.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CombinedDeviceResources : SMS_CombinedResources  
{  
    DateTime ADLastLogonTime;  
    String ADSiteName;  
    String AMTFullVersion;  
    UInt32 AMTStatus;  
    SInt32 ClientActiveStatus;  
    UInt32 ClientCertType;  
    SInt32 ClientCheckPass;  
    UInt32 ClientEdition;  
    SInt32 ClientRemediationSuccess;  
    UInt32 ClientType;  
    String ClientVersion;  
    String DeviceAccessState;  
    String DeviceCategory;  
    String DeviceOS;  
    UInt32 DeviceOwner;  
    String DeviceType;  
    String Domain;  
    String EASDeviceID;  
    UInt32 EnrollmentStatus;  
    Boolean EPAntispywareEnabled;  
    DateTime EPAntispywareSignatureLastUpdateDateTime;  
    String EPAntispywareSignatureLastVersion;  
    Boolean EPAntivirusEnabled;  
    DateTime EPAntivirusSignatureLastUpdateDateTime;  
    String EPAntivirusSignatureLastVersion;  
    String EPClientVersion;  
    String EPDeploymentDescription;  
    UInt32 EPDeploymentErrorCode;  
    UInt32 EPDeploymentState;  
    Boolean EPEnabled;  
    String EPEngineVersion;  
    DateTime EPLastFullScanDateTimeEnd;  
    DateTime EPLastFullScanDateTimeStart;  
    UInt32 EPInfectionStatus;  
    DateTime EPLastInfectionTime;  
    DateTime EPLastQuickScanDateTimeEnd;  
    DateTime EPLastQuickScanDateTimeStart;  
    String EPLastThreatName;  
    Boolean EPPendingFullScan;  
    Boolean EPPendingManualSteps;  
    Boolean EPPendingOfflineScan;  
    Boolean EPPendingReboot;  
    String EPPolicyApplicationDescription;  
    UInt32 EPPolicyApplicationErrorCode;  
    UInt32 EPPolicyApplicationState;  
    String EPPolicyName; (removed in SP1)  
    UInt32 EPProductStatus;  
    String ExchangeOrganization;  
    String ExchangeServer;  
    String IMEI;  
    Boolean IsActive;  
    Boolean IsAlwaysInternet;  
    UInt32 IsApproved;  
    Boolean IsBlocked;  
    Boolean IsClient;  
    Boolean IsInternetEnabled;  
    Boolean IsObsolete;  
    Boolean IsVirtualMachine;  
    DateTime LastActiveTime;  
    DateTime LastClientCheckTime;  
    DateTime LastDDR;  
    DateTime LastHardwareScan;  
    UInt32 LastInstallationError;  
    String LastMPServerName;  
    DateTime LastPolicyRequest;  
    DateTime LastSoftwareScan;  
    DateTime LastStatusMessage;  
    DateTime LastSuccessSyncTimeUTC;  
    DateTime LatestProcessingAttempt;  
    String Name;  
    String PhoneNumber;  
    String PolicyApplicationStatus;  
    UInt32 ResourceID;  
    UInt32 ResourceType;  
    String SerialNumber;  
    String SiteCode;  
    String SMSID;  
    String Status;  
    Boolean SuppressAutoProvision;  
    Boolean Unknown;  
    String UserDomainName;  
    String UserName;  
    UInt32 WipeStatus;  
};  
```  

## Methods  
 The SMS_CombinedDeviceResources class does not define any methods.  

## Properties  
 `ADLastLogonTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last logon timestamp of the computer (discovered from Active Directory).  

 `ADSiteName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Active Directory site to which the resource belongs.  

 `AMTFullVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The version number for Active Management Technology.  

 `AMTStatus`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The status for Active Management Technology.  

|||  
|-|-|  
|0|Not AMT capable|  
|1|AMT capable|  
|2|Not provisioned|  
|3|Provisioned|  
|4|Provisioned by others|  
|5|Unknown|  

 `ClientActiveStatus`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Comes from Client Health.  

|||  
|-|-|  
|0|Client is inactive|  
|1|Client is healthy|  

 `ClientCertType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Client certificate type. Possible values are:  

|||  
|-|-|  
|1|Self-signed Certificate|  
|2|PKI Certificate|  

 `ClientCheckPass`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Comes from Client Health.  

|||  
|-|-|  
|1|Client is healthy|  
|2|Client is unhealthy|  

 `ClientRemediationSuccess`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Comes from Client Health.  

|||  
|-|-|  
|1|Client remediation succeeded|  
|2|Client remediation failed|  

 `ClientEdition`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Edition of the client. Possible values are:  

|||  
|-|-|  
|0|Not Installed|  
|1|Windows RT|  
|2|Windows Mobile 6|  
|3|Nokia Symbian|  
|4|Windows Phone|  
|5|Mac|  
|6|Windows CE|  
|7|Windows Embedded|  
|8|iOS|  
|9|Andriod|  
|10|Unix/Linux|  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `ClientType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Type of client. Possible value are:  

|||  
|-|-|  
|1|Client|  
|3|Device|  

 `ClientVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Version of the installed client software.  

 `DeviceAccessState`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Used by the Exchange connector. Possible values are:  

||  
|-|  
|Allowed|  
|Blocked|  
|Quarantined|  

 `DeviceCategory`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Category of the device.  

 `DeviceOS`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Device operating system.  

 `DeviceOwner`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Owner of the device.  

|||  
|-|-|  
|1|Company|  
|2|Personal|  

 `DeviceType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Type of device, such as Nokia, Microsoft Pocket PC and Smartphone.  

 `Domain`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Domain to which the resource belongs.  

 `EASDeviceID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Identifier of the device - used by Exchange Active Sync (EAS). This is specific to device management.  

 `EnrollmentStatus`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates if the mobile device is newly enrolled or if the UDA has been created.  Possible values are:  

|||  
|-|-|  
|1|Newly enrolled.|  
|2|UDA has been created.|  

 `EPAntispywareEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if Endpoint Protection antimalware is enabled.  

 `EPAntispywareSignatureLastUpdateDateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The last update time of the Endpoint Protection antimalware signature file.  

 `EPAntispywareSignatureLastVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The last version of the Endpoint Protection antimalware signature file.  

 `EPAntivirusEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if Endpoint Protection antivirus is enabled.  

 `EPAntivirusSignatureLastUpdateDateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The last update time of the Endpoint Protection antivirus signature file.  

 `EPAntivirusSignatureLastVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The last version of the Endpoint Protection antivirus signature file.  

 `EPClientVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 EndPoint Protection client agent version, such as ‘4.1.522.0’.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `EPDeploymentDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Deployment description.  

 `EPDeploymentErrorCode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Deployment error code.  

 `EPDeploymentState`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Deployment state. Possible values are:  

|||  
|-|-|  
|1|Unmanaged|  
|2|To Be Installed|  
|3|Managed|  
|4|Install With Error|  
|5|Reboot Pending|  

 `EPEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if Endpoint Protection is enabled.  

 `EPEngineVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 EndPoint Protection engine version, such as ‘1.1.8904.0’.  

 `EPInfectionStatus`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Endpoint Protection infection status. Possible values are:  

|||  
|-|-|  
|0|Unknown|  
|1|None|  
|2|Cleaned|  
|3|Pending|  
|4|Failed|  

 `EPLastFullScanDateTimeEnd`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 End time of the last full EndPoint Protection scan.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `EPLastFullScanDateTimeStart`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Start time of last full EndPoint Protection scan.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `EPLastInfectionTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last infection time.  

 `EPLastQuickScanDateTimeEnd`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 End time of last quick EndPoint Protection scan.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `EPLastQuickScanDateTimeStart`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Start time of last quick EndPoint Protection scan.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `EPLastThreatName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Last threat name.  

 `EPPendingFullScan`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if Endpoint Protection is pending a full scan.  

 `EPPendingManualSteps`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if Endpoint Protection is pending manual steps.  

 `EPPendingOfflineScan`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if Endpoint Protection is pending an offline scan.  

 `EPPendingReboot`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if Endpoint Protection is pending a reboot.  

 `EPPolicyApplicationDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Antimalware Policy application description.  

 `EPPolicyApplicationErrorCode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Policy application error code.  

 `EPPolicyApplicationState`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Policy application state.  

|||  
|-|-|  
|1|Success|  
|2|Failed|  

 `EPPolicyName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the policy that gets applied, such as ‘Antimalware Policy’.  

 This method/property has been removed or deprecated in System Center Configuration Manager SP1.  

 `EPProductStatus`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Product status. Possible values are:  

|||  
|-|-|  
|0|No status flags are set.|  
|0|Service not running.|  
|1|Service started without any malware protection engine.|  
|2|Pending a full scan due to threat action.|  
|4|Pending a reboot due to threat action.|  
|8|Pending manual steps due to threat action.|  
|16|AV signatures out of date.|  
|32|AS signatures out of date.|  
|64|No quick scan has happened for a specified period.|  
|128|No full scan has happened for a specified period.|  
|256|System initiated scan in progress.|  
|512|System initiated clean in progress.|  
|1024|There are samples pending submission.|  
|2048|Product running in evaluation mode.|  
|4096|Product running in non-genuine Windows mode.|  
|8192|Product expired.|  
|16384|Off-line scan required.|  

 `ExchangeOrganization`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the organization for Exchange Active Sync (EAS) .  

 `ExchangeServer`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the Exchange server for Exchange Active Sync (EAS).  

 `IMEI`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 IMEI number of the device.  

 `IsActive`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if there has been a recent heartbeat from the client.  

 `IsAlwaysInternet`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if a client that is installed has a sustained connection to the Internet.  

 `IsApproved`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if system is able to accept secure policy. Unapproved (anonymous) clients will not get policy. Clients that registered via windows authentication, or using PKI certificate chain trust, will be automatically approved.  

 `IsBlocked`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if a system is blocked. Block/unblock is a manual action in the Admin Console UI that the administrator can invoke. By blocking a client, client communication with the server will be cut off.  

 `IsClient`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true`, if the client is a Configuration Manager client.  

 `IsInternetEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if a client is enabled for communication with an internet facing management point.  

 `IsObsolete`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client has been marked obsolete.  

 `IsVirtualMachine`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client is a virtual machine.  

 `LastActiveTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Comes from Client Health. Represents the last reported time the client was active.  

 `LastClientCheckTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Comes from Client Health. Represents the last reported health evaluation time.  

 `LastDDR`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last heartbeat timestamp from client DDR discovery.  

 `LastHardwareScan`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Timestamp from the last hardware inventory scan.  

 `LastInstallationError`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Last reported error code from the installation on this client.  

 `LastMPServerName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Management Point server name where the client performed its last policy request.  

 `LastPolicyRequest`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Timestamp of the last policy request for this client.  

 `LastSoftwareScan`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Timestamp of the last software inventory scan for this client.  

 `LastStatusMessage`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Timestamp of the last status message received from this client.  

 `LastSuccessSyncTimeUTC`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Timestamp of the last successfully synchronization time for this client.  

 `LatestProcessingAttempt`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Timestamp of the last processing attempt for this client.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 NetBIOS name for this system. Comes from Discovery.  

 `PhoneNumber`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Phone number of the device, as reported by Exchange Active Sync (EAS).  

 `PolicyApplicationStatus`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Application policy status, as reported by Exchange Active Sync (EAS).  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, key]  

 Unique Configuration Manager-supplied ID for the resource.  

 `ResourceType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Type of resource, for example, system or user. For more information, see [SMS_ResourceMap Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resourcemap-server-wmi-class.md).  

 `SerialNumber`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Serial number of the device.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Site code of the site that created the collection.  

 `SMSID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique Configuration Manager ID of the client.  

 `Status`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Current status.   

 `SuppressAutoProvision`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Comes from AMT (Active Management Technology). Indicates whether the client should be blocked from being provisioned automatically.  

 `UserDomainName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The domain of the user to last log in to this client.  

 `Unknown`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the device is unknown.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `UserName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The name of the user to last log in to this client.  

 `WipeStatus`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Wipe status of the device, as reported through Exchange Active Sync (EAS).  

|||  
|-|-|  
|1|Wipe Pending|  
|2|Wipe Cancelling|  
|3|Wipe Confirmed/Registered|  

## Remarks  
 Similar to the members class that is generated for querying "All Systems," this class is designed for summarizing the major properties across different feature areas and is not bound by the same RBAC rules as the "All Systems" resource class.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
