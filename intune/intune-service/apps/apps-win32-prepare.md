---
title: Prepare a Win32 App to Be Uploaded to Microsoft Intune
description: Learn how to prepare a Win32 app to be uploaded to Microsoft Intune.
ms.date: 02/06/2026
ms.topic: how-to
ms.reviewer: bryanke
ms.collection:
- M365-identity-device-management
- highpri
- FocusArea_Apps_Win32
---

# Prepare Win32 App Content for Upload

Before you can add a Win32 app to Microsoft Intune, you must prepare the app by using the [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730).

> [!TIP]
> As a companion to this article, see our Intune app protection for Windows setup guide](https://go.microsoft.com/fwlink/?linkid=2309605) to review best practices and learn to enforce policies, deploy apps, and protect corporate data across various devices. For a customized experience based on your environment, you can access the [Intune app protection for Windows guide](https://go.microsoft.com/fwlink/?linkid=2309606) in the Microsoft 365 admin center.  

## Prerequisites

To use Win32 app management, be sure you meet the following criteria:

- Use a [supported Windows version](../fundamentals/supported-devices-browsers.md) (Enterprise, Pro, and Education versions).
- Devices must be registered or joined to Microsoft Entra ID and autoenrolled. The Intune management extension supports devices that are:
    - Microsoft Entra registered
    - Microsoft Entra joined
    - hybrid domain joined
    - group policy enrolled

  > [!NOTE]
  > For the scenario of group policy enrollment, the user uses the local user account to Microsoft Entra join their Windows device. The user must sign in the device by using their Microsoft Entra user account and enroll in Intune. Intune management extension is installed automatically when a PowerShell script or Win32 app, Microsoft Store apps, Custom compliance policy settings, or Proactive remediations is assigned to the user or device.
- Windows application size is capped at 30 GB per app.
- Apps must support silent installation: Win32 apps deployed through Intune must be able to install without user interaction. Ensure your application installers support silent or unattended installation modes before packaging them with the Content Prep Tool.

## Convert the Win32 app content

Use the [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730) to preprocess Windows classic (Win32) apps. The tool converts application installation files into the *.intunewin* format. The tool also detects some of the attributes that Intune requires to determine the application installation state. After you use this tool on the app installer folder, you'll be able to create a Win32 app in the Microsoft Intune admin center.

> [!IMPORTANT]
> The [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730) zips all files and subfolders when it creates the *.intunewin* file. Be sure to keep the Microsoft Win32 Content Prep Tool separate from the installer files and folders, so that you don't include the tool or other unnecessary files and folders in your *.intunewin* file.

You can download the [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730) from GitHub as a .zip file. The zipped file contains a folder named *Microsoft-Win32-Content-Prep-Tool-master*. The folder contains the prep tool, the license, a readme, and the release notes.

### Process flow to create a .intunewin file

   <img alt="Flow chart of the process to create a .intunewin file." src="./media/apps-win32-app-management/prepare-win32-app.png" width="700">

### Running the Microsoft Win32 Content Prep Tool

If you run `IntuneWinAppUtil.exe` from the command window without parameters, the tool guides you to enter the required parameters step by step. Or, you can add the parameters to the command based on the following available command-line parameters.

### Available command-line parameters

|    **Command-line   parameter**    |    **Description**    |
|--------------------------------|------------------------------------------------------------|
|    `-h`     |    Help    |
|    `-c <setup_folder>`     |    Folder for all setup files. All files in this folder are compressed into an *.intunewin* file.    |
|    `-s <setup_file>`     |    Setup file (such as *setup.exe* or *setup.msi*).    |
|    `-o <output_folder>`     |    Output folder for the generated *.intunewin* file.    |
|    `-q`       |    Quiet mode.    |

### Example commands

|    **Example command**    |    **Description**    |
|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `IntuneWinAppUtil -h`    |    This command shows usage information for the tool.    |
|    `IntuneWinAppUtil -c c:\testapp\v1.0 -s c:\testapp\v1.0\setup.exe -o c:\testappoutput\v1.0 -q`    |    This command generates the *.intunewin* file from the specified source folder and setup file. For the MSI setup file, this tool retrieves required information for Intune. If `-q` is specified, the command runs in quiet mode. If the output file already exists, it's overwritten. Also, if the output folder doesn't exist, it's created automatically.    |

When you're generating an *.intunewin* file, put any files you need to reference into a subfolder of the setup folder. Then, use a relative path to reference the specific file you need. For example:

**Setup source folder:** *c:\testapp\v1.0*<br>
**License file:** *c:\testapp\v1.0\licenses\license.txt*

Refer to the *license.txt* file by using the relative path *licenses\license.txt*.

## Next steps

- [Add a Win32 app to Microsoft Intune](apps-win32-add.md)
