---
title: "UpdatePrereqAndStateFlags Method"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, the UpdatePrereqAndStateFlags Windows Management Instrumentation class method updates the installation state of update packages."
ms.date: "09/20/2016"
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: eee2fd3a-3840-4201-8bf9-5b775234aa07
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3


---
# UpdatePrereqAndStateFlags Method in Class SMS_CM_UpdatePackages
The `UpdatePrereqAndStateFlags` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates the installation state of update packages.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 UpdatePrereqAndStateFlags(  
     UInt32 flag,  
     UInt32 state  
);  

```  

#### Parameters  
 `flag`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Pre-requisites  flag for an update package. Possible values are:  

| Value | Description |  
| ----- | ----------- |  
|0|NOT_CONTINUE_ON_PREREQ_WARNING. During installation, stop the upgrade if there is a prerequisite warning.|  
|1|PREREQ_ONLY. Run only the prerequisite.|  
|2|CONTINUE_ON_PREREQ_WARNING. During installation, ignore the prerequisite warning.|  

 `state`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Installation state of an update package. Possible values are:  

| Value | Installation state |  
| ----- | ------------------ |  
|0x2|ENABLED|  
|0x00040001|DOWNLOAD_IN_PROGRESS|  
|0x00040002|DOWNLOAD_SUCCESS|  
|0x0004FFFF|DOWNLOAD_FAILED|  
|0x00050001|APPLICABILITY_CHECKING|  
|0x00050002|APPLICABILITY_SUCCESS|  
|0x0005FFFD|APPLICABILITY_HIDE|  
|0x0005FFFE|APPLICABILITY_NA|  
|0x0005FFFF|APPLICABILITY_FAILED|  
|0x00010001|CONTENT_REPLICATING|  
|0x00010002|CONTENT_REPLICATION_SUCCESS|  
|0x0001FFFF|CONTENT_REPLICATION_FAILED|  
|0x00020001|PREREQ_IN_PROGRESS|  
|0x00020002|PREREQ_SUCCESS|  
|0x00020003|PREREQ_WARNING|  
|0x0002FFFF|PREREQ_ERROR|  
|0x00030001|INSTALL_IN_PROGRESS|  
|0x00030002|INSTALL_WAITING_SERVICE_WINDOW|  
|0x00030003|INSTALL_WAITING_PARENT|  
|0x00030004|INSTALL_SUCCESS|  
|0x00030005|INSTALL_PENDING_REBOOT|  
|0x0003FFFF|INSTALL_FAILED|  
|0x00030006|INSTALL_CMU_VALIDATING|  
|0x00030007|INSTALL_CMU_STOPPED|  
|0x00030008|INSTALL_CMU_INSTALLFILES|  
|0x00030009|INSTALL_CMU_STARTED|  
|0x0003000A|INSTALL_CMU_SUCCESS|  
|0x0003000B|INSTALL_WAITING_CMU|  
|0x0003FFFE|INSTALL_CMU_FAILED|  
|0x0003000C|INSTALL_INSTALLFILES|  
|0x0003000D|INSTALL_UPGRADESITECTRLIMAGE|  
|0x0003000E|INSTALL_CONFIGURESERVICEBROKER|  
|0x0003000F|INSTALL_INSTALLSYSTEM|  
|0x00030010|INSTALL_CONSOLE|  
|0x00030011|INSTALL_INSTALLBASESERVICES|  
|0x00030012|INSTALL_UPDATE_SITES|  
|0x00030013|INSTALL_SSB_ACTIVATION_ON|  
|0x00030014|INSTALL_UPGRADEDATABASE|  
|0x00030015|INSTALL_UPDATEADMINCONSOLE|  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CM_UpdatePackages Server WMI Class](../../../develop/reference/sum/sms_cm_updatepackages-server-wmi-class.md)   
