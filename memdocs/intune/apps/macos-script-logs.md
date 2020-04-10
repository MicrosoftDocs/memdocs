---
# required metadata

title: Troubleshoot macOS shell script policies using log collection in Microsoft Intune | Microsoft Docs
description: Understand how to troubleshoot macOS shell script policies using log collection in Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/10/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Troubleshoot macOS shell script policies using log collection

You can collect device logs to help troubleshoot script issues on macOS devices. 

## Requirements for log collection
The following items are required to collect logs on a macOS device:
- You must specify the full absolute log file path.
- File paths must be separated using only a semicolon (;).
- The maximum log collection size to upload is 60 MB (compressed) or 25 files, whichever occurs first.
- File types that are allowed for log collection include the following extensions: *.log, .zip, .gz, .tar, .txt, .xml, .crash, .rtf*

### Collect device logs
1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. In **Device status** or **User status** report, select a device.
3. Select **Collect logs**, provide folder paths of log files separated only by a semicolon (;) without spaces or newlines in between paths.<br>For example, multiple paths should be written as `/Path/to/logfile1.zip;/Path/to/logfile2.log`. 

   >[!IMPORTANT]
   > Multiple log file paths separated using comma, period, newline or quotation marks with or without spaces will result in log collection error. Spaces are also not allowed as separators between paths.

4. Select **OK**. Logs are collected the next time the Intune MDM agent on the device checks in with Intune. This check-in usually occurs every 8 hours.

   >[!NOTE]
   > 
   > - Collected logs are encrypted on the device, transmitted and stored in Microsoft Azure storage for 30 days. Stored logs are decrypted on demand and downloaded using Microsoft Endpoint Manager admin center.
   > - In addition to the admin-specified logs, Intune MDM agent logs are also collected from these folders: `/Library/Logs/Microsoft/Intune` and `~/Library/Logs/Microsoft/Intune`. The agent log file-names are `IntuneMDMDaemon date--time.log` and `IntuneMDMAgent date--time.log`. 
   > - If any admin-specified file is missing or has the wrong file-extension, you will find these file-names listed in `LogCollectionInfo.txt`.     

### Log collection errors
Log collection may not be successful due to any of the following reasons provided in the table below. To resolve these errors, follow the remediation steps.

| Error code (hex) | Error code (dec) | Error message | Remediation steps |
|------------------|------------------|---------------|-------------------|
| 0X87D300D1 | 2016214834 | Log file size cannot exceed 60 MB. | Ensure that compressed logs are less than 60 MB in size. |
| 0X87D300D1 | 2016214831 | The provided log file path must exist. The system user folder is an invalid location for log files. | Ensure that the provided file path is valid and accessible. |
| 0X87D300D2 | 2016214830 | Log collection file upload failed due to expiration of upload URL. | Retry the **Collect logs** action. |
| 0X87D300D3, 0X87D300D5, 0X87D300D7 | 2016214829, 2016214827, 2016214825 | Log collection file upload failed due to encryption failure. Retry log upload. | Retry the **Collect logs** action. |
| | 2016214828 | The number of log files exceeded the allowed limit of 25 files. | Only up to 25 log files can be collected at a time. |
| 0X87D300D6 | 2016214826 | Log collection file upload failed due to zip error. Retry log upload. | Retry the **Collect logs** action. |
| | 2016214740 | The logs couldn’t be encrypted as compressed logs were not found. | Retry the **Collect logs** action. |
| | 2016214739 | The logs were collected but couldn’t be stored. | Retry the **Collect logs** action. |

## Next steps

- [Use shell scripts on macOS devices in Intune](..\apps\macos-shell-scripts.md)
