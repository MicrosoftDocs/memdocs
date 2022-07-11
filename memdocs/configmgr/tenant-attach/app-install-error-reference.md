---
title: Application installation error codes reference
titleSuffix: Configuration Manager
description: Reference Application installation errors for tenant attach
ms.date: 10/05/2021
ms.topic: reference
ms.prod: configuration-manager
ms.technology: configmgr-core
manager: dougeby
author: mestew
ms.author: mstewart
ms.localizationpriority: high
---

# Application installation common error codes reference

Applications can be installed on clients by creating deployments from the Configuration Manager console or by [targeting applications to tenant attached devices](./applications.md) from the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/). Use the information in this article to assist with troubleshooting application installation errors. <!--8364465-->

## <a name="bkmk_general"></a> General troubleshooting tips

Generally, if an application installs successfully on a device with the given command line in the system context, it will install successfully through Configuration Manager and from the Microsoft Endpoint Manager admin center. You can simulate this by using [PSExec](/sysinternals/downloads/psexec). 

1. Open an administrative command prompt.
1. Change directory to where you saved [PSExec](/sysinternals/downloads/psexec).
1. Type in `psexec -accepteula -s -i cmd`.
1. This opens a new command prompt window running interactively in the system context. Check that you're in the system context by running a `whoami` command.
1. Run the install from the new windows with the installation command line. For example, `msiexec /i "My App.msi" /q` would be a quiet install of the "My App" msi file.  

You may also find that searching through multiple files for a specific string is useful. For instance, you might want to search all the client `.mof` files for a specific class, or you might want to search logs for a specific ID. Using a specific ID when searching can give you an understanding of how components are related to each other. Use the [select-string cmdlet](/powershell/module/Microsoft.PowerShell.Utility/Select-String) in those instances.

```powershell
select-string -Path "c:\windows\ccm\*.mof" -Pattern 'CacheInfoEx'
select-string -Path "c:\windows\ccm\logs\*.log" -Pattern 'CacheInfoEx.CacheId="ccfe8120-4b9b-4f6e-b8fb-f8c1b1fd74d8'
```
## <a name="bkmk_configmgr"></a> Configuration Manager errors

|Error code|Error source|Error message|
|----|----|----|
|[0x87D00202](#0x87d00202)|Configuration Manager| Service is shutting down|
|[0x87D00207](#0x87d00207)|Configuration Manager| Parsing error|
|[0x87D00213](#0x87d00213)|Configuration Manager| Timeout occurred|
|[0x87D00215](#0x87d00215)|Configuration Manager| Item not found|
|[0x87D00235](#0x87d00235)|Configuration Manager | Syntax error occurred while parsing|
|[0x87D00244](#0x87d00244)|Configuration Manager| The object or subsystem has not been initialized|
|[0x87D0027C](#0x87d0027c)|Configuration Manager| CI documents download timed out|
|[0x87D00289](#0x87d00289)|Configuration Manager| Failed to decompress CI documents|
|[0x87D00314](#0x87d00314)|Configuration Manager| CI Version Info timed out|
|[0x87D00321](#0x87d00321)|Configuration Manager | The script execution has timed out|
|[0x87D00324](#0x87d00324)|Configuration Manager| The application was not detected after installation completed|
|[0x87D00325](#0x87d00325)|Configuration Manager| Application was still detected after uninstall completed|
|[0x87D00327](#0x87d00327)|Configuration Manager| Script is not signed|
|[0x87D00329](#0x87d00329)|Configuration Manager| Application requirement evaluation or detection failed|
|[0x87D00607](#0x87d00607)|Configuration Manager| Content not found|
|[0x87D00667](#0x87d00667)|Configuration Manager| No current or future service window exists to install software updates|
|[0x87D01106](#0x87d01106)|Configuration Manager| Failed to verify the executable file is valid or to construct the associated command line|
|[0x87D01107](#0x87d01107)|Configuration Manager| Failed to access all the provided program locations. This program may retry if the maximum retry count has not been reached|
|[0x87D01201](#0x87d01201)|Configuration Manager| The content download cannot be performed because there is not enough available space in cache or the disk is full|
|[0x87D01202](#0x87d01202)|Configuration Manager| The content download cannot be performed because the total size of the client cache is smaller than the size of the requested content|
|[0x87D01281](#0x87d01281)|Configuration Manager| A supported App-V client is not installed|
|[0x87D0128F](#0x87d0128f)|Configuration Manager| The App-V sftmime command returned failure|
|[0x87D01290](#0x87d01290)|Configuration Manager| An error occurred when querying the App-V WMI provider|
|[0x87D103E8](#0x87d103e8)|Configuration Manager| Error Unknown|
|[0x87D1076C](#0x87d1076c)|Configuration Manager| Application was successfully installed|

### <a name="bkmk_general-configmgr"></a> General Configuration Manager troubleshooting tips

When an application fails to install and the error source is **Configuration Manager**, typically, following the [application troubleshooting guide](../apps/understand/app-deployment-technical-reference.md) and using the [general troubleshooting tips](#bkmk_general) helps you resolve the error. You may also want to use [Support Center for Configuration Manager](../core/support/support-center.md) to help troubleshoot and review information about your clients. 

<!-- template

### code

**Message**: 

**Additional information for error resolution**:

-->
### 0x87D00202

**Message**: Service is shutting down

**Additional information for error resolution**:
Verify that the Configuration Manager client is running on the target device. Verify the client is running by:
- Reviewing the **CCMExec.log** on the device
- Verifying that the **SMS Agent Host** service is running on the device

### 0x87D00207

**Message**: Parsing error

**Additional information for error resolution**: This error generally occurs in one of the Configuration Manager components when a piece of data is invalid. This error could stem from something missing for the application, an old package version, or a number of other general errors. Follow the [application troubleshooting guide](../apps/understand/app-deployment-technical-reference.md) to help locate the error and resolve it. It may be necessary to review additional logs for components that support application installation. Searching for specific IDs or error codes in the logging may help you identify the problem. For more information, see [general troubleshooting tips](#bkmk_general).

### 0x87D00213

**Message**: Timeout occurred

**Additional information for error resolution**: Increase the [**Maximum allowed run time (minutes)**](../apps/deploy-use/create-applications.md) for the application. Ensure that the maintenance window on the client is large enough to support the runtime. For more information, see the [application troubleshooting guide](../apps/understand/app-deployment-technical-reference.md) to help resolve the error.

### 0x87D00215

**Message**: Item not found

**Additional information for error resolution**:  
Verify that the following exist and are accessible to the client:
- The [application deployment](../apps/understand/device-deployment-technical-reference.md) exists and the client sees the policy.
- The [application content exists and is available](../apps/understand/deployment-download-technical-reference.md) to the client

For more information, see the [application troubleshooting guide](../apps/understand/app-deployment-technical-reference.md) to help resolve the error.

### 0x87D00235

**Message**: Syntax error occurred while parsing

**Additional information for error resolution**: This error generally occurs in one of the Configuration Manager components when a piece of data is invalid. This error could stem from something missing for the application, an old package version, or a number of other general errors. Follow the [application troubleshooting guide](../apps/understand/app-deployment-technical-reference.md) to help locate the error and resolve it. It may be necessary to review additional logs for components that support application installation. Searching for specific IDs or error codes in the logging may help you identify the problem. For more information, see [general troubleshooting tips](#bkmk_general).

### 0x87D00244

**Message**: The object or subsystem has not been initialized

**Additional information for error resolution**: This error generally occurs in one of the Configuration Manager components when a piece of data is invalid. This error could stem from something missing for the application, an old package version, or a number of other general errors. Follow the [application troubleshooting guide](../apps/understand/app-deployment-technical-reference.md) to help locate the error and resolve it. It may be necessary to review additional logs for components that support application installation. Searching for specific IDs or error codes in the logging may help you identify the problem. For more information, see [general troubleshooting tips](#bkmk_general).

### 0x87D0027C

**Message**: CI documents download timed out

**Additional information for error resolution**: The CI documents activity can be tracked in **CIAgent.log**, **CIDownloader.log**, and **DataTransferService.log**. For more information, see the [CI Agent section](../apps/understand/client-components-technical-reference.md#ci-agent) of the application troubleshooting guide.
### 0x87D00289

**Message**: Failed to decompress CI documents

**Additional information for error resolution**:  The CI documents activity can be tracked in **CIAgent.log**, **CIDownloader.log**, and **DataTransferService.log**. For more information, see the [CI Agent section](../apps/understand/client-components-technical-reference.md#ci-agent) of the application troubleshooting guide.

### 0x87D00314

**Message**: CI Version Info timed out

**Additional information for error resolution**: Typically this error occurs when a change was made to the application and the client doesn't have the new information for it. Verify that the client is [getting the policy](../apps/understand/deployment-policy-technical-reference.md) and it knows about any [updated revisions](../apps/understand/deployment-evaluation-technical-reference.md#application-detection-and-evaluation) to the application.

### 0x87D00321

**Message**: The script execution has timed out

**Additional information for error resolution**: Check the **AppEnforce.log** for details. You may need to increase the [**Maximum allowed run time (minutes)**](../apps/deploy-use/create-applications.md) for the application. Ensure that the maintenance window on the client is large enough to support the run time. For more information, see the [application troubleshooting guide](../apps/understand/app-deployment-technical-reference.md) to help resolve the error.

### 0x87D00324

**Message**: The application was not detected after installation completed

**Additional information for error resolution**: Review the **AppDiscovery.log** and the **CIAgent.log**. Once an installation is completed, the [application detection](../apps/understand/deployment-evaluation-technical-reference.md) is used again to [verify the installation](../apps/understand/deployment-install-technical-reference.md#installation-verification).  

### 0x87D00325

**Message**: Application was still detected after uninstall completed

**Additional information for error resolution**: Verify the correct uninstall command was used in the **AppEnforce.log**. Review the **AppDiscovery.log** and the **CIAgent.log**. Once an uninstall is completed, the [application detection](../apps/understand/deployment-evaluation-technical-reference.md) is used again to [verify the uninstall](../apps/understand/deployment-install-technical-reference.md#installation-verification).  

### 0x87D00327

**Message**: Script is not signed

**Additional information for error resolution**: Verify the [PowerShell execution policy client setting](../core/clients/deploy/about-client-settings.md#powershell-execution-policy) for the device. The default for this client setting is **AllSigned** so an unsigned script will cause a failure.  

### 0x87D00329

**Message**: Application requirement evaluation or detection failed

**Additional information for error resolution**: Review the **AppIntentEval.log** to discover dependencies and supersedence rules for the application and their states. For more information, see [Application deployment evaluation](../apps/understand/deployment-evaluation-technical-reference.md).

### 0x87D00607

**Message**: Content not found

**Additional information for error resolution**: Verify the content for the application is on a distribution point and that the distribution point is accessible to the client. For more information, see [Application download in Configuration Manager](../apps/understand/deployment-download-technical-reference.md).

### 0x87D00667

**Message**: No current or future service window exists to install software updates

**Additional information for error resolution**: Ensure that the [maintenance window](../core/clients/manage/collections/use-maintenance-windows.md) on the client is large enough to support the [**Maximum allowed run time (minutes)**](../apps/deploy-use/create-applications.md) for the application installation and that the client has received the policy for the window.

### 0x87D01106

**Message**: Failed to verify the executable file is valid or to construct the associated command line

**Additional information for error resolution**: Verify that the executable file is installable on its own then verify it's installable with the given command line.  

### 0x87D01107

**Message**: Failed to access all the provided program locations. This program may retry if the maximum retry count has not been reached

**Additional information for error resolution**: The client is getting locations for the content, but can't reach the locations. Review the client's **LocationServices.log** for the `Distribution Point=`. Use **ContentTransferManager.log** and **DataTransferService.log** to monitor the download for errors.

### 0x87D01201

**Message**: The content download cannot be performed because there is not enough available space in cache or the disk is full

**Additional information for error resolution**: Check that the machine has enough space on the drive. Compare the size of the `ccmcache` directory with the [client cache settings](../core/clients/deploy/about-client-settings.md#client-cache-settings) and ensure the setting is adequate for the application's size.

### 0x87D01202

**Message**: The content download cannot be performed because the total size of the client cache is smaller than the size of the requested content

**Additional information for error resolution**: Compare the size of the `ccmcache` directory with the [client cache settings](../core/clients/deploy/about-client-settings.md#client-cache-settings) and ensure the setting is adequate for the application's size.

### 0x87D01281

**Message**: A supported App-V client is not installed

**Additional information for error resolution**: Verify that a [supported version](../apps/get-started/deploying-app-v-virtual-applications.md#supported-app-v-versions) of App-V is installed on the client.

### 0x87D0128F

**Message**: The App-V sftmime command returned failure

**Additional information for error resolution**: For information on sftmime commands, see [Manage Virtual Applications by Using the Command Line](/microsoft-desktop-optimization-pack/appv-v4/how-to-manage-virtual-applications-by-using-the-command-line).

### 0x87D01290

**Message**: An error occurred when querying the App-V WMI provider

**Additional information for error resolution**: For information on the App-V WMI provider, see [Application Virtualization Client WMI Provider](/microsoft-desktop-optimization-pack/appv-v4/application-virtualization-client-wmi-provider).

### 0x87D103E8

**Message**: Error Unknown

**Additional information for error resolution**: Follow the [application troubleshooting guide](../apps/understand/app-deployment-technical-reference.md) to help locate the error and resolve it. It may be necessary to review additional logs for components that support application installation. Searching for specific IDs or error codes in the logging may help you identify the problem. For more information, see [general troubleshooting tips](#bkmk_general).

### 0x87D1076C

**Message**: Application was successfully installed

**Additional information for error resolution**: The application was successfully installed.


## <a name="bkmk_msi"></a> MSI errors

|Error code|Error source|Error message|
|----|----|----|
|[1602](#1602)| MSI| User cancel installation|
|[1603](#1603)|MSI| Fatal error during installation|
|[1605](#1605)| MSI| This action is only valid for products that are currently installed|
|[1618](#1618)|MSI| Another program is being installed. Please wait until that installation is complete, and then try installing this software again|
|[1633](#1633)|MSI| This installation package is not supported by this processor type. Contact your product vendor|
|[1638](#1638)| MSI| Another version of this product is already installed.  Installation of this version cannot continue.  To configure or remove the existing version of this product, use Add/Remove Programs on the Control Panel|
|[1642](#1642)| MSI| The upgrade patch cannot be installed by the Windows Installer service because the program to be upgraded may be missing, or the upgrade patch may update a different version of the program. Verify that the program to be upgraded exists on your computer and that you have the correct upgrade patch|

### <a name="bkmk_general-msi"></a> General MSI troubleshooting tips

When errors are encountered from MSI, typically you'll need to [Enable Windows Installer logging](/troubleshoot/windows-client/application-management/enable-windows-installer-logging). After the logging is enabled, you can retry the problem installation and Windows Installer will track the progress and post it to the `%temp%` folder. The new log's file name is random. However, the first letters are `Msi` and the file name has a .log extension.

The  [MsiExec.exe and InstMsi.exe Error Messages](/windows/win32/msi/error-codes) and [Windows Installer Action Return Values](/windows/win32/msi/logging-of-action-return-values) lists are useful when reviewing a Windows Installer log as are the [general troubleshooting tips](#bkmk_general).

### 1602

**Message**: User cancel installation

**Additional information for error resolution**: The installation was canceled by the user. Ask the user to install the application fully. If possible, you can attempt to run the installation for the system rather than the user.

### 1603

**Message**: Fatal error during installation

**Additional information for error resolution**: [Enable Windows Installer logging](/troubleshoot/windows-client/application-management/enable-windows-installer-logging) and run the install again. When reviewing the installer log, typically an entry stating `Return value 3` is located near the failure reason in the log. For more information on possible return values and their meaning, see [Windows Installer Action Return Values](/windows/win32/msi/logging-of-action-return-values).

### 1605

**Message**: This action is only valid for products that are currently installed

**Additional information for error resolution**: Ensure that the product is installed before running a dependant install.

### 1618

**Message**: Another program is being installed. Please wait until that installation is complete, and then try installing this software again

**Additional information for error resolution**: Wait for the prior installation to complete before running a new one. If the prior installation stops responding, you can attempt to stop the installation or terminate the process. Terminating a process might have undesired results.

### 1633

**Message**: This installation package is not supported by this processor type. Contact your product vendor

**Additional information for error resolution**: Ensure that the device's processor architecture is appropriate for the software. Verify the target device meets or exceeds the minimum processor requirement for the application. Contact the product vendor if the device's processor meets the product's processor support specifications.

### 1638

**Message**: Another version of this product is already installed. Installation of this version cannot continue. To configure or remove the existing version of this product, use Add/Remove Programs on the Control Panel

**Additional information for error resolution**: Uninstall the the unwanted version of the product. If you aren't using Configuration Manager, a script, or another management tool to uninstall, uninstall from the device manually. For Windows 10 or later clients,  use **Windows Settings** > **Apps** to uninstall the unwanted version of the product. For earlier versions of Windows, use **Programs and Features** from the Control Panel to uninstall the unwanted version of the product.

### 1642

**Message**: The upgrade patch cannot be installed by the Windows Installer service because the program to be upgraded may be missing, or the upgrade patch may update a different version of the program. Verify that the program to be upgraded exists on your computer and that you have the correct upgrade patch

**Additional information for error resolution**: Verify the device meets the product versioning prerequisites for the installation.

## <a name="bkmk_windows"></a> Windows errors

|Error code|Error source|Error message|
|----|----|----|
|[1](#1)| Windows| Incorrect function|
|[2](#2)| Windows| The system cannot find the file specified|
|[692](#692)| Windows| Debugger terminated process|
|[0x80000003](#0x80000003)|Windows| One or more arguments are invalid|
|[0x80000007L](#0x80000007l)|Windows| Operation aborted|
|[0x80000009](#0x80000009)|Windows| General access denied error|
|[0x80004005](#0x80004005)|Windows| Unspecified error|
|[0x8000FFFF](#0x8000ffff)|Windows| Catastrophic failure|
|[0x80040154](#0x80040154)|Windows| Class not registered|
|[0x80091007](#0x80091007)|Windows| The hash value is not correct|
|[0xC0000142](#0xc0000142)|Windows| Initialization of the dynamic link library failed. The process is terminating abnormally|
### <a name="bkmk_general-windows"></a> General Windows troubleshooting tips

Use the [Windows system error codes](/windows/win32/debug/system-error-codes--0-499-) list or [Download the Microsoft Error Lookup Tool](/windows/win32/debug/system-error-code-lookup-tool) for looking up additional codes that aren't listed in this article. Using the Windows event logs and the [general troubleshooting tips](#bkmk_general) can also help identify the cause of these errors.

### 1

**Message**: Incorrect function

**Additional information for error resolution**: Review the Windows event logs around the time of the failure in combination with the installation logs to determine the possible cause of the error.

### 2

**Message**: The system cannot find the file specified

**Additional information for error resolution**: 
- If the missing file is a system file, run the [System File Checker tool to repair missing or corrupted system files](https://support.microsoft.com/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system). You can also use `/scanfile=file` or `/verifyfile` with the [sfc command](/windows-server/administration/windows-commands/sfc) to scan the binary and check if there is any issue with that file. 
- If the missing file is an application file, you can repair or uninstall and reinstall the application to replace the missing file. 
- If you're unsure which file is missing and the logs aren't listing it, you may want to use [Process Monitor](/sysinternals/downloads/procmon) to help identify the problematic file. 
   - You can launch Process Monitor without capturing events and filters by using `ProcMon.exe /NoConnect /NoFilter /AcceptEULA`

### 692

**Message**: Debugger terminated process

**Additional information for error resolution**: Detach any debuggers attached to the process and retry the application installation.

### 0x80000003

**Message**: One or more arguments are invalid

**Additional information for error resolution**: Review the Windows event logs around the time of the failure in combination with the installation logs to determine the possible cause of the error.

### 0x80000007L

**Message**: Operation aborted

**Additional information for error resolution**: Use the installation logs and Configuration Manager application logs to determine why installation stopped. Merge the logs so you can easily review what happened before the 0x80000007L error. Use `eventvwr.msc` to review the Windows event logs for additional events that occurred around the time of the installation failure.

### 0x80000009

**Message**: General access denied error

**Additional information for error resolution**: If the issue isn't clear from the logs, using `eventvwr.msc` to review Windows event logs and [Process Monitor](/sysinternals/downloads/procmon) can help identify problematic files or processes. If needed, use the Windows user interface or [icacls](/windows-server/administration/windows-commands/icacls) to modify permissions on the problematic file.

Additional tips for file permissions in Windows operating systems:
- Deny permissions always take precedence over Allow permissions.
- Explicit permissions take precedence over inherited permissions.
- If NTFS permissions conflict, or example, if group and user permissions are contradictory, the most liberal permissions take precedence.
- Permissions are cumulative.

### 0x80004005

**Message**: Unspecified error

**Additional information for error resolution**: Use the installation logs and Configuration Manager application logs to determine why installation stopped. Merge the logs so you can easily review what happened before the 0x80004005 error. Use `eventvwr.msc` to review the Windows event logs for additional events that occurred around the time of the installation failure. Follow the [application troubleshooting guide](../apps/understand/app-deployment-technical-reference.md) to help resolve the error.
[Process Monitor](/sysinternals/downloads/procmon) can also help identify the failure.

<!--note--> 
### 0x8000FFFF

**Message**: Catastrophic failure

**Additional information for error resolution**: Review the Windows event logs around the time of the failure in combination with the installation logs to determine the possible cause of the error.

### 0x80040154

**Message**: Class not registered

**Additional information for error resolution**: This is typically a configuration-related DCOM error. Review DCOM configuration settings using [dcomconfig](/windows/win32/com/enabling-com-security-using-dcomcnfg). If there's a problematic .dll file, you can use [regsvr32](/windows-server/administration/windows-commands/regsvr32) to register the dll file and try the install again. A large number of problematic files could be a sign of an underlying issue that needs to be resolved before you can install the application. 

### 0x80091007 

**Message**: The hash value is not correct

**Additional information for error resolution**: The hash of a file isn't correct and the installation can't complete. Typically you will see this error in the **CAS.log**. Check to see if file contents for the application were recently updated. There may be an issue with the package, in some cases you may need to rebuild and redistribute it. This issue can also happen if there is a sharing violation on a file, such as a security application scanning the file. Configuration Manager expects exclusive access to the file during a hash check. You can identify the problematic process by running a [Process Monitor](/sysinternals/downloads/procmon) and adding a filter. The condition to be met is if the **Result** *contains* **Sharing Violation** then **Include** the event.  

### 0xC0000142

**Message**: Initialization of the dynamic link library failed. The process is terminating abnormally

**Additional information for error resolution**: If there is a problematic .dll file, you can use [regsvr32](/windows-server/administration/windows-commands/regsvr32) to register the dll file and try again. A large number of problematic files could be a sign of an underlying issue that needs to be resolved before you can install the application.

## <a name="bkmk_wmi"></a> Windows Management Instrumentation (WMI) errors

|Error code|Error source|Error message|
|----|----|----|
|[0x80041001](#0x80041001)|Windows Management Instrumentation (WMI)|WBEM_E_FAILED|
|[0x80041009](#0x80041009)|Windows Management Instrumentation (WMI)|WBEM_E_NOT_AVAILABLE|
|[0x8004100E](#0x8004100e)|Windows Management Instrumentation (WMI)|WBEM_E_INVALID_NAMESPACE|

### <a name="bkmk_general-wmi"></a> General WMI troubleshooting tips

Problematic namespaces can typically be found in the [Configuration Manager log files](../core/plan-design/hierarchy/log-files.md) and the [WMI logging](/windows/win32/wmisdk/wmi-log-files). WMI relies on Component Object Model (COM)/Distributed Component Object Model (DCOM), the registry, the file system, and Remote Procedure Call (RPC). DCOM registrations and permissions are critical for WMI operations to be successful. You can review DCOM configuration settings using [dcomconfig](/windows/win32/com/enabling-com-security-using-dcomcnfg).

When troubleshooting WMI problems, typically you start by verifying that the needed namespaces, classes, and instances exists in the WMI repository and can be accessed.

Verify the namespace exists on the target first by running `wmimgmt.msc` from an elevated command prompt. When WMI Control launches:
1. Select **Action** then **Properties**.
1. Select the **Security** tab to see all the namespaces.
1. Navigate to the namespace in question.
1. Verify the namespace exists and review the security on the namespace.

To connect  WMI Control to another computer:
1.  Select **Action** then  **Connect to another computer**.
1. Select the option for **Another computer:** then supply the name.
1. Select **Properties** to connect. The connection to the WMI repository on the remote computer doesn't occur until you select **Properties**.
1. Verify the namespace exists and review the security on the namespace.
1. You may also wish to try to connect with the IP address too to verify that you can connect.

Verify the namespace exists on the target and that you can query it properly. Run the Windows Management Instrument Tester from an elevated command prompt by typing in `wbemtest`. When the Windows Management Instrument Tester launches:
1. Select **Connect...** 
2. Type in the problematic namespace such as `root\cimv2` or  `root\ccm` and user credentials if needed. To connect to another machine, supply the name or the IP address such as `\\Machine1\root\ccm` and credentials if needed.
1. Select **Enum Classes...** to verify you get classes listed for the problematic namespace.  
1. Set the superclass info to **Recursive** and select **OK** to verify classes list for the problematic namespace.
1. Launch the object editor for one of the classes by double-clicking on it. 
   - If you're using the `root\ccm` namespace, select a class that starts with "CCM_" such as CCM_ClientIdentificationInformation. 
   - If you're using `root\cimv2`, choose one that starts with "Win32_" such as Win32_BIOS.
1. Select **Instances** to verify the instances of the selected class load. For some classes, it's ok if there aren't any instances, just make sure that the **Query Result** window states **Done**. Long running queries to list of instances or queries that never finish may indicate a problem.


Verify the repository:
1. From an elevated command prompt, run `winmgmt /verifyrepository`. Verifying is typically useful for invalid class errors especially if you had to recently recompile a .mof file using [mofcomp](/windows/win32/wmisdk/mofcomp). 
1. If problems are found during verification, you can try to salvage using `winmgmt /salvagerepository`
1. Typically, you won't use /resetrepository unless it's truly needed an no other alternative exists. Some namespaces won't automatically rebuild and you'll need to either reinstall the software associated with the missing namespace or mofcomp the application's .mof files to rebuild them.

WMI resources:
- [Introduction to wbemtest](../develop/core/understand/introduction-to-wbemtest.md)
- [Winmgmt service](/windows/win32/wmisdk/winmgmt)
- [WMI Log Files](/windows/win32/wmisdk/wmi-log-files)
- [Enable trace and debug logging for WMI events](/windows/win32/wmisdk/tracing-wmi-activity#obtaining-wmi-events-through-event-viewer)
   - Ensure you change the default log size to cover your troubleshooting session.
   - Once you have finished troubleshooting, remember to disable the trace and debug logging.
- [Setting namespace security with the WMI Control](/windows/win32/wmisdk/setting-namespace-security-with-the-wmi-control)
- [WMI troubleshooting](/windows/win32/wmisdk/wmi-troubleshooting)
- [Ask The Performance Team: WMI](https://techcommunity.microsoft.com/t5/ask-the-performance-team/bg-p/AskPerf/label-name/wmi)

### 0x80041001

**Message**: WBEM_E_FAILED

**Additional information for error resolution**: WBEM_E_FAILED is a generic WMI failure error. The error can be caused by a number of things. The error will sometimes tell you which method or instance failed. You'll probably also see related log entires around the same time if you merge logs together based on similar function. For instance, if you see the error related to content for an application, you may want to merge together CAS.log, ContentTransferManager.log and DataTransfer.log. If the error happened on a site server not a client, you may want to review SMSProv.log for additional information. Use the [General WMI troubleshooting tips](#bkmk_general-wmi) to help identify the issue along with the application installation logs.

### 0x80041009

**Message**: WBEM_E_NOT_AVAILABLE

**Additional information for error resolution**: The resource, in many cases a remote machine, isn't currently available. Verify the device is online. Use the [General WMI troubleshooting tips](#bkmk_general-wmi) to help verify connectivity to WMI on the device.

### 0x8004100E

**Message**: WBEM_E_INVALID_NAMESPACE

**Additional information for error resolution**: The namespace specified could not be found. Verify the target computer can connect to WMI by following the [General WMI troubleshooting tips](#bkmk_general-wmi). Verify namespace specified exists.

## <a name="bkmk_wua"></a> Windows Update Agent errors

|Error code|Error source|Error message|
|----|----|----|
|[0x00240006](#0x00240006)|Windows Update Agent| The update to be installed is already installed on the system|
|[0x80240017](#0x80240017)|Windows Update Agent | Operation was not performed because there are no applicable updates|

### <a name="bkmk_general-wua"></a> General Windows Update Agent troubleshooting tips

The errors for the installation originated from the Windows Update Agent. In many cases, you can attempt to install these updates using the built-in software update management from Configuration Manager, Windows Update for Business, or Microsoft Update. In certain circumstances where it's not feasible to use your regular patching mechanism, the `.msu` package can be installed with the [Windows Update Standalone Installer (wusa.exe)](https://support.microsoft.com/help/934307/description-of-the-windows-update-standalone-installer-in-windows) like an application. Use the [Windows Update logging](/windows/deployment/update/windows-update-logs) and [general troubleshooting tips](#bkmk_general) to help determine the cause of the issue.
### 0x00240006

**Message**: The update to be installed is already installed on the system

**Additional information for error resolution**: The update is already installed on the device.

### 0x80240017

**Message**: Operation was not performed because there are no applicable updates

**Additional information for error resolution**: The update isn't applicable to the device. Verify that the device meets the requirements of the update. In cases where a superseding update has been installed, it's very rare that the superseded update would be applicable to the device.

<!-- template

### code

**Message**: 

**Additional information for error resolution**:

-->
