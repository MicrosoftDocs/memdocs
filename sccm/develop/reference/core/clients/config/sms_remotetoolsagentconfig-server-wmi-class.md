---
title: "SMS_RemoteToolsAgentConfig Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 9b0190b8-5eec-40f5-9bb1-da8223c95951
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_RemoteToolsAgentConfig Server WMI Class
The `SMS_RemoteToolsAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies the Remote Control settings on client computers.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_RemoteToolsAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AccessLevel;  
    UInt32 AgentID;  
    Boolean AllowClientChange;  
    Boolean AllowLocalAdminToDoRemoteControl;  
    Boolean AllowRAUnsolicitedControl;  
    Boolean AllowRAUnsolicitedView;  
    Boolean AllowRemCtrlToUnattended;  
    UInt32 AudibleSignal;  
    Boolean Enabled;  
    Boolean EnableRA;  
    Boolean EnableTS;  
    Boolean EnforceRAandTSSettings;  
    UInt32 FirewallExceptionProfiles;  
    Boolean ManageRA;  
    Boolean ManageTS;  
    Boolean PermissionRequired;  
    String PermittedViewers[];  
    Boolean RemCtrlConnectionBar;  
    Boolean RemCtrlTaskbarIcon;  
    Boolean TSUserAuthentication;  
};  
```  

## Methods  
 The `SMS_RemoteToolsAgentConfig` class does not define any methods.  

## Properties  
 `AccessLevel`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Access level allowed.  

|Possible values|
|----|
|No Access|  
|View Only|  
|Full Control|  

 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Remote Tools Agent Config ID is 3.  

 `AllowClientChange`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Users can change policy or notification settings in Software Center.  

 `AllowLocalAdminToDoRemoteControl`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Grant Remote Control permission to local Administrators group.  

 `AllowRAUnsolicitedControl`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client should configure Remote Assistance to allow a remote Unsolicited Control request.  

 `AllowRAUnsolicitedView`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client should configure Remote Assistance to allow a remote Unsolicited View request.  

 `AllowRemCtrlToUnattended`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Allow Remote Control of an unattended computer.  

 `AudibleSignal`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Value indicating if a control beep should be sounded during a remote control session to signify that the computer is being remotely controlled. This is only for Remote Control, not Remote Assistance. Possible values are:  

|Value|Definition|
|----|----|
|0|None|  
|1|Beginning and end of the session|  
|2|Repeatedly|  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the agent is enabled.  

 `EnableRA`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client should enable Remote Assistance for the client.  

 `EnableTS`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 This applied to the remote control setting ‘Allow permitted viewers to connect using Remote Desktop Connection at admin console UI item. This property can be set only when ManageTS is true.  

 `EnforceRAandTSSettings`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if Remote Assistance settings, which might be configured by the user in a Control Panel program, should be overridden by the Configuration Manager settings. This matches ‘Manage solicited Remote Assistance settings’.  

 `FirewallExceptionProfiles`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Firewall profile setting masks which is combine them as an OR of domain profile 0x4, private profile 0x2, and public profile 0x1.  

 `ManageRA`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client should set local Remote Assistance settings. This matches ‘Manage unsolicited Remote Assistance settings’.  

 `ManageTS`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Configuration Manager will manage Remote Desktop settings. This applies to the ‘Manage Remote Desktop Settings’ in the Admin Console’s remote desktop settings.  

 `PermissionRequired`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Value indicating that the helpdesk administrator is required to get permission from the remote user before starting remote control session. This is only applied when remote user is on an active session.  

|Value|Definition|
|----|----|
|false|Bypass remote control permission dialog.|  
|true|Ask permission to start a remote control session.|  

 `PermittedViewers`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 The list of user and group names that are allowed to use Remote Tools and Remote Assistance for the client. The format of the string is \<domain or computer>\\<user or group name\>.  

 `RemCtrlConnectionBar`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Show session connection bar.  

 `RemCtrlTaskbarIcon`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Show session notification icon on taskbar.  

 `TSUserAuthentication`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Allow connection only from computers running Remote Desktop with network-level authentication selected in Vista or later OSs.  This can be set only if EnableTS is true.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
