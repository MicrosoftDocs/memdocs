---
title: SMS_HealthAttestationDetails Class
titleSuffix: Configuration Manager
description: The SMS_HealthAttestationDetails Windows Management Instrumentation class is an SMS Provider server class, in Configuration Manager, that represents Health Attestation details.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b402a603-f1cf-417a-a9f4-2f6bb79fd042
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_HealthAttestationDetails Server WMI Class
The `SMS_HealthAttestationDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents Health Attestation details.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_HealthAttestationDetails : SMS_BaseClass  
{  
     UInt32 AIKPresent;  
     SInt32 BitlockerStatus;  
     UInt32 BootDebuggingEnabled;  
     UIt32 CertRetrievalStatus;  
     UInt32 CodeIntegrityEnabled;  
     DateTime DateIssued;  
     UInt64 DEPPolicy;  
     UInt32 DeviceItemKey;  
     UInt32 ELAMDriverLoaded;  
     UInt32 HASSupported;  
     UInt32 OSKernelDebuggingEnabled;  
     UInt32 SafeMode;  
     UInt32 SecureBootEnabled;  
     UInt32 TestSigningEnabled;  
     UInt32 VSMEnabled;  
     UInt32 WinPE;  
};  

```  

## Methods  
 The `SMS_HealthAttestationDetails` class does not define any methods.  

## Properties  
 `AIKPresent`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates whether the Windows Automated Installation Kit (Windows AIK) is present.  

 `BitlockerStatus`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The status of BitLocker.  

 `BootDebuggingEnabled`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates whether boot debugging is enabled.  

 `CertRetrievalStatus`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The status of the certificate retrieval.  

 `CodeIntegrityEnabled`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates whether code integrity is enabled.  

 `DateIssued`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The date and time that the certificate was issued.  

 `DEPPolicy`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: none  

 The Apple Device Enrollment Program (DEP) policy.  

 `DeviceItemKey`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The device key.  

 `ELAMDriverLoaded`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Specifies whether the Early-Launch Anti-Malware (ELAM) driver is loaded.  

 `HASSupported`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Specifies whether health attestation is supported.  

 `OSKernelDebuggingEnabled`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates whether operating system kernel debugging is enabled.  

 `SafeMode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 `SecureBootEnabled`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Specifies whether secure boot is enabled.  

 `TestSigningEnabled`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Specifies whether test-signing is enabled.  

 `VSMEnabled`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Specifies whether VSM is enabled.  

 `WinPE`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)
