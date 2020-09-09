---
title: Troubleshoot Win32 apps in Microsoft Intune
titleSuffix:
description: Learn about the most common methods to troubleshoot Win32 app issues used with Microsoft Intune. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2

ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Troubleshoot Win32 app issues

When troubleshooting Win32 apps used in Microsoft Intune, you have a number of methods that you can use. This topic provides troubleshooting details, as well as additional information to help you solve Win32 app problems.  [Win32 app installation troubleshooting](troubleshoot-app-install.md#win32-app-installation-troubleshooting) resources.

> [!NOTE]
> This app management capability supports both 32-bit and 64-bit operating system architecture for Windows applications.

> [!IMPORTANT]
> When deploying Win32 apps, consider using the [Intune Management Extension](../apps/intune-management-extension.md) approach exclusively, particularly when you have a multi-file Win32 app installer. If you mix the installation of Win32 apps and line-of-business apps during AutoPilot enrollment, the app installation may fail. The Intune management extension is installed automatically when a PowerShell script or Win32 app is assigned to the user or device.

## App troubleshooting details

You can view installation issues, such as when the app was created, modified, targeted, and delivered to a device. The [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) provides these and other details in the **Troubleshoot + support** pane. For more information, see [App troubleshooting details](troubleshoot-app-installmd#app-troubleshooting-details).

## Troubleshoot app issues using logs

Viewing the details of logs can help you determine the cause of the issue you are seeing.

### Logs displayed in Intune

When an installation issue occurs with a Win32 app, you can choose the **Collect logs** option in the **Installation details** pane for the app in Intune. For more details, see [Win32 app installation troubleshooting](troubleshoot-app-install.md#win32-app-installation-troubleshooting).

### Logs displayed using CMTrace

Agent logs on the client machine are commonly in `C:\ProgramData\Microsoft\IntuneManagementExtension\Logs`. You can leverage `CMTrace.exe` to view these log files. For more information, see [CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace).

![Screenshot of the Agent logs on the client machine](./media/apps-win32-app-management/apps-win32-app-10.png)

> [!IMPORTANT]
> To allow proper installation and execution of LOB Win32 apps, anti-malware settings should exclude the following directories from being scanned:<p>
> **On X64 client machines**:<br>
> *C:\Program Files (x86)\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>  
> **On X86 client machines**:<br>
> *C:\Program Files\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>
> For more information, see [Virus scanning recommendations for Enterprise computers that are running currently supported versions of Windows](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers).

## Detecting the Win32 app file version using PowerShell

If you have difficulty detecting the Win32 app file version, consider using or modifying the following PowerShell command:

``` PowerShell

$FileVersion = [System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion
#The below line trims the spaces before and after the version name
$FileVersion = $FileVersion.Trim();
if ("<file version of successfully detected file>" -eq $FileVersion)
{
#Write the version to STDOUT by default
$FileVersion
exit 0
}
else
{
#Exit with non-zero failure code
exit 1
}
```

In the above PowerShell command, replace the `<path to binary file>` string with the path to your Win32 app file. An example path would be similar to the following:<br>
`C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`

Also, replace the `<file version of successfully detected file>` string with the file version that you need to detect. An example file version string would be similar to the following:<br>
`2019.0150.18118.00 ((SSMS_Rel).190420-0019)`

If you need to get the version information of your Win32 app, you can use the following PowerShell command:

``` PowerShell

[System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion

```

In the above PowerShell command, replace `<path to binary file>` with your file path.

## Additional troubleshooting areas to consider
- Check targeting to make sure agent is installed on the device - Win32 app targeted to a group or PowerShell Script targeted to a group will create agent install policy for security group.
- Check OS Version – Windows 10 1607 and above.  
- Check Windows 10 SKU - Windows 10 S, or Windows versions running with S-mode enabled, do not support MSI installation.

For more information about troubleshooting Win32 apps, see [Win32 app installation troubleshooting](troubleshoot-app-install.md#win32-app-installation-troubleshooting). For information about app types on ARM64 devices, see [App types supported on ARM64 devices](../apps/troubleshoot-app-install.md#app-types-supported-on-arm64-devices).

## Next steps

- [Troubleshoot app installation issues](troubleshoot-app-install.md).
