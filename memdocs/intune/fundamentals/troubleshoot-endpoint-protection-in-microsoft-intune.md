---
# required metadata

title: Common endpoint protection messages in Microsoft Intune - Azure | Microsoft Docs
description: See common messages and possible solution when using and troubleshooting endpoint protection and Microsoft Defender in Microsoft Intune.
keywords:
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/13/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: e31df2d2-bb1b-491b-9a71-04e0b18829c1
ROBOTS:

# optional metadata

#audience:

ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Endpoint protection issues and possible solutions in Microsoft Intune

This article lists and describes potential causes and solutions for some errors and warnings. Use the information to help solve problems when using endpoint protection.

## Microsoft Defender error codes

Review event logs and error codes to [troubleshoot issues with Microsoft Defender AV](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/troubleshoot-windows-defender-antivirus).

## Common Intune errors and possible resolutions

### Endpoint Protection engine unavailable

**Potential cause**: The Intune endpoint protection engine was corrupted or deleted.

**Possible solutions**:

- If endpoint protection is corrupt or won't update, then update or reinstall the program.
- Force an immediate update. In the endpoint protection client program (possibly in the taskbar), choose **Update**.
- In Control Panel > Programs, select **Microsoft Intune Endpoint Protection Agent**. Uninstall the application.
- During the next update synchronization, the Microsoft Online Management Update Manager detects the missing program and reinstalls it at the scheduled installation time.

### Features are disabled

You may get a message that some features are disabled. These messages can happen if Intune endpoint protection or Microsoft Defender is disabled by an administrator using a configuration profile. Or, it's disabled by an end user on the device. Possible messages:

`Endpoint Protection disabled`  
`Real-time protection disabled`  
`Download scanning disabled`  
`File and program activity monitoring disabled`  
`Behavior monitoring disabled`  
`Script scanning disabled`  
`Network Inspection System disabled`  

**Possible solutions**: Enable these features. For guidance, see:

- [Add endpoint protection settings](../protect/endpoint-protection-configure.md)
- [Microsoft Defender Antivirus](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus)
- [End users: Turn on real-time protection to access company resources](../user-help/turn-on-defender-windows.md)

### Malware definitions out of date

This status shows when the malware definitions on the device are out of date by 14 days or more. For example, the message may show if the device is disconnected from the Internet, or the malware definitions are outdated.

**Possible solutions**: If malware definitions are out of date, update the definitions using [Microsoft Defender Antivirus](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus).

### Full scan overdue or Quick scan overdue

A full scan or quick scan hasn't completed for 14 days. This scenario can happen if the device restarts during a full scan.

**Possible solutions**: If a scan is overdue, you can run a one-time scan or schedule recurring scans. See [Microsoft Defender Antivirus](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus).

### Another endpoint protection application running

Another endpoint protection application is running, and the device is healthy.

**Possible solutions**: If another endpoint protection application is installed and Intune detects that application, the device may become unstable.

## Next steps

Get [support help from Microsoft](get-support.md), or use the [community forums](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
