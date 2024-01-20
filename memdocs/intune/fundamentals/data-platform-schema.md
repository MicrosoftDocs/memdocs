---
# required metadata

title: Intune data platform schema
description: Overview of Intune data platform schema.
keywords: 
ms.author: Smritib17
author: smbhardwaj 
manager: dougeby
ms.date: 02/01/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: Elizabeth cox 
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier2
- M365-identity-device-management
---

# Introduction

*Applies to: Microsoft Intune*

This article goes over the properties supported in the Intune Data Platform.

Device query allows you to quickly assess the state of devices in your environment and take action. When you enter a query on a selected device, Device query runs a query in real time. The data returned can then be filtered, grouped, and refined to answer business questions, troubleshoot issues in your environment, or respond to security threats.

Each table (entity) in this page lists the types of queries that are supported.

## BiosInfo

Description: Provides basic BIOS Information.  
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |


## H2: Certificate

Description: Certificate Authorities installed in Keychains/ca-bundles. Only certificates for computers are returned.
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## CPU

Description: Retrieves CPU hardware info on the machine.
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## DiskDrive

Description: Retrieves basic information about the physical disks of a system.
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## EncryptableVolume

Description: Retrieves encryptable volume status of the machine.
Supported for: Device query, single device on-demand

| Property | Type | Description |
| --- | --- | --- |

## FileInfo

Description: Lists all file info of the passed file or files under the passed directory.
Supported for: Device query, single device on-demand.

> [!NOTE]
> This is a parameterized entity where you must pass in the path of the File you want to query. For example, pass in `FileInfo('c:\windows\system32\drivers\etc\hosts') | take 10`.

| Property | Type | Description |
| --- | --- | --- |

## LocalGroup

Description: Lists local user groups.  
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## LocalUserAccount

Description: Lists local user accounts.
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## LogicalDrive

Description: Details for logical drives on the system. A logical drive generally represents a single partition.
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## MemoryInfo

Description: Memory Information.
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## OsVersion

Description: A single row containing the operating system name and version.
Supported for: Device query, single device on-demand,

| Property | Type | Description |
| --- | --- | --- |

## Process

Description: All running processes on the host system.  
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## SystemEnclosure

Description: Displays information pertaining to the chassis and its security status.
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## SystemInfo

Description: System information of the device.  
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## Tpm

Description: Provides TPM related information of the device.  
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## WindowsAppCrashEvent

Description: Provides App Crash info in Windows event log file Application in look back time.
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## WindowsDriver

Description: Details for in-use Windows device drivers. This does not display installed but unused drivers.
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## WindowsEvent

Description: Get Windows Event logs in the specified log name and look back in time.  
Supported for: Device query, single device on-demand.

> [!NOTE]
> When constructing the query, you must specify the log name and look back time, for example: `WindowsEvent(Application, 1d) | take 1`.

| Property | Type | Description |
| --- | --- | --- |

## WindowsQfe

Description: Information about security patches on the device.
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |

## WindowsRegistry

Description: Lists registry under the passed registry key.  
Supported for: Device query, single device on-demand.

> [!NOTE]
> You must pass in the registry key you are trying to query. For example, `WindowsRegistry('HKEY_LOCAL_MACHINE\\ServiceLastKnownStatus')`.

| Property | Type | Description |
| --- | --- | --- |

## WindowsService

Description: Lists all installed Windows services and their relevant data.
Supported for: Device query, single device on-demand.

| Property | Type | Description |
| --- | --- | --- |


