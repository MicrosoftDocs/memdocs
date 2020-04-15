---
title: About log files
titleSuffix: Configuration Manager
description: Use log files to troubleshoot issues with Configuration Manager clients and site systems.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual


ms.assetid: b1751e3c-a60c-4ab7-a943-2595df1eb612
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# About log files in Configuration Manager

*Applies to: Configuration Manager (current branch)*

In Configuration Manager, client and site server components record process information in individual log files. You can use the information in these log files to help you troubleshoot issues that might occur. By default, Configuration Manager enables logging for client and server components.

This article provides general information about the Configuration Manager log files. It includes tools to use, how to configure the logs, and where to find them. For more information on specific log files, see [Log files reference](/sccm/core/plan-design/hierarchy/log-files).


## <a name="BKMK_AboutLogs"></a> How it works

Most processes in Configuration Manager write operational information to a log file that is dedicated to that process. The log files are identified by **.log** or **.lo_** file extensions. Configuration Manager writes to a .log file until that log reaches its maximum size. When the log is full, the .log file is copied to a file of the same name but with the .lo_ extension, and the process or component continues to write to the .log file. When the .log file again reaches its maximum size, the .lo_ file is overwritten and the process repeats. Some components establish a log file history by appending a date and time stamp to the log file name and by keeping the .log extension.


## <a name="bkmk_tools"></a> Log viewer tools

All Configuration Manager log files are plain text, so you can view them with any text reader like Notepad. The logs use unique formatting that's best viewed with one of the following specialized tools:

- [CMTrace](#cmtrace)
- [OneTrace](#onetrace)
- [Support Center log viewer](#support-center-log-viewer)

### CMTrace

To view the logs, use the Configuration Manager log viewer tool **CMTrace**. It's located in the `\SMSSetup\Tools` folder of the Configuration Manager source media. The CMTrace tool is added to all boot images that are added to the Software Library. The CMTrace log viewing tool is automatically installed along with the Configuration Manager client.<!--1357971--> For more information, see [CMTrace](/sccm/core/support/cmtrace).

### OneTrace

Starting in version 1906, **OneTrace** is a new log viewer with Support Center. It works similarly to CMTrace, with improvements. For more information, see [Support Center OneTrace](/sccm/core/support/support-center-onetrace).

### Support Center log viewer

**Support Center** includes a modern log viewer. This tool replaces CMTrace and provides a customizable interface with support for tabs and dockable windows. It has a fast presentation layer, and can load large log files in seconds. For more information, see [Support Center Log Viewer reference](/sccm/core/support/support-center-ui-reference#bkmk_log-viewer).

> [!Note]  
> Support Center and OneTrace use Windows Presentation Foundation (WPF). This component isn't available in Windows PE. Continue to use CMTrace in boot images with task sequence deployments.


## <a name="bkmk_logoptions"></a> Configure logging options

You can change the configuration of the log files, such as the verbose level, size, and history. There are several ways to change these settings:

- [During client installation](#bkmk_logoptions-clientprop)
- [Using Configuration Manager Service Manager](#bkmk_logoptions-sm)
- [Using the Windows Registry](#bkmk_logoptions-registry)
- [In the Configuration Manager console](#bkmk_logoptions-console)

### <a name="bkmk_logoptions-clientprop"></a> Configure logging options during client installation

You can set the configuration of the client log files during installation. Use the following properties:

- CCMENABLELOGGING
- CCMDEBUGLOGGING
- CCMLOGLEVEL
- CCMLOGMAXHISTORY
- CCMLOGMAXSIZE

For more information, see [Client installation properties](/sccm/core/clients/deploy/about-client-installation-properties#clientMsiProps).

### <a name="bkmk_logoptions-sm"></a> Configure logging options by using Configuration Manager Service Manager

You can change where Configuration Manager stores the log files, and their size.  

To modify the size of log files, change the name and location of the log file, or to force multiple components to write to a single log file, do the following steps:  

#### Modify logging for a component  

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **System Status**, and then select either the **Site Status** or **Component Status** node.  

2. In the ribbon, select **Start**, and then select **Configuration Manager Service Manager**.  

3. When Configuration Manager Service Manager opens, connect to the site that you want to manage. If the site that you want to manage isn't shown, select **Site**, select **Connect**, and then enter the name of the site server for the correct site.  

4. Expand the site and go to **Components** or **Servers**, depending on where the components that you want to manage are located.  

5. In the right pane, select one or more components.  

6. On the **Component** menu, select **Logging**.  

7. In the **Configuration Manager Component Logging** dialog box, complete the available configuration options for your selection.  

8. Select **OK** to save the configuration.  

### <a name="bkmk_logoptions-registry"></a> Configure logging options by using the Windows Registry

<!-- SCCMDocs#992 -->
Use the Windows Registry on the servers or clients to change the following logging options:

- Verbose level
- Maximum history
- Maximum size

When troubleshooting a problem, you can enable verbose logging for Configuration Manager to write additional details in the log files.

> [!Warning]
> Misconfiguration of these settings can cause Configuration Manager to log large amounts of information, or none at all. While this data can be beneficial for troubleshooting, be cautious when changing these values in production sites. Always test these changes in a lab environment first. Excessive logging can occur, which might make it difficult to find relevant information in the log files.

After you make changes to these registry settings, restart the component:

- If you change the client settings, restart the **SMS Agent Host** service (CcmExec).
- If you change the server settings, restart the **SMS Executive** service.

The registry settings vary depending upon the component:

- [Client and management point](#bkmk_reg-client)
- [Site server](#bkmk_reg-site)
- [Site system role](#bkmk_reg-role)
- [Configuration Manager console](#bkmk_reg-console)

#### <a name="bkmk_reg-client"></a> Client and management point logging options

To configure logging options for all components on a client or management point site system, configure these **REG_DWORD** values under the following Windows Registry key:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\@Global`

|Name  |Values  |Description  |
|---------|---------|---------|
|LogLevel|`0`: Verbose<br>`1`: Default<br>`2`: Warnings and errors<br>`3`: Errors only|The level of detail to write to log files.|
|LogMaxHistory|Any integer greater than or equal to zero, for example:<br>`0`: No history<br>`1`: Default|When a log file reaches the maximum size, the client renames it as a backup and creates a new log file. Specify how many previous versions to keep.|
|LogMaxSize|Any integer greater than or equal to 10,000, for example:<br>250000|The maximum log file size in bytes. When a log grows to the specified size, the client renames it as a history file, and creates a new file. The default value is 250,000 bytes.|

> [!Note]  
> Don't change other values that may exist in this registry key.

For advanced debugging, you can also add this **REG_SZ** value under the following Windows Registry key:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\DebugLogging`

|Name  |Values  |Description  |
|---------|---------|---------|
|Enabled | `True`: enable debug logs<br>`False`: disable debug logs |Enables debug logging for troubleshooting purposes.|

This setting causes the client to log low-level information for troubleshooting. Avoid using this setting in production sites. Excessive logging can occur, which might make it difficult to find relevant information in the log files. Make sure to turn off this setting after you resolve the issue.

#### <a name="bkmk_reg-site"></a> Site server logging options

You can configure settings globally or for a specific component on the Configuration Manager site server.

Configure these values under the following Windows Registry key:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing`

|Name  |Values  |Type  |Description
|---------|---------|---------|---------|
|SqlEnabled| `1`: enable SQL tracing<br> `0`: disable SQL tracing |REG_DWORD|Add SQL trace logging to all site server logs.|
|ArchiveEnabled| `1`: enable log archives<br> `0`: disable log archives | REG_DWORD |Archive site server logs to a separate location for historical preservation.|
|ArchivePath| A valid folder path, for example `C:\Logs\Archive` | REG_SZ |The path to archive site server logs.|

Only enable SQL tracing for troubleshooting purposes. Avoid using it in production sites. Excessive logging can occur, which might make it difficult to find relevant information in the log files. Make sure to turn off this setting after you resolve the issue.

> [!Note]  
> Don't change other values that may exist in this registry key.

To configure logging options for a specific server component, configure these **REG_DWORD** values under the following Windows Registry key:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing\<ComponentName>`

|Name  |Values  |Description  |
|---------|---------|---------|
|LoggingLevel|`0`: Verbose<br>`1`: Default<br>`2`: Warnings and errors<br>`3`: Errors only|The level of detail to write to log files.|
|LogMaxHistory|Any integer greater than or equal to zero, for example:<br>`0`: No history<br>`1`: Default|When a log file reaches the maximum size, the server renames it as a backup and creates a new log file. Specify how many previous versions to keep.|
|MaxFileSize|Any integer greater than or equal to 10,000, for example:<br>250000|The maximum log file size in bytes. When a log grows to the specified size, the client renames it as a history file, and creates a new file. The default value is 250,000 bytes.|
|DebugLogging| `1`: enable debug logs<br>`0`: disable debug logs |Enables debug logging for troubleshooting purposes.|

The DebugLogging setting causes the server to log low-level information for troubleshooting. Avoid using this setting in production sites. Excessive logging can occur, which might make it difficult to find relevant information in the log files. Make sure to turn off this setting after you resolve the issue.

> [!Note]  
> Don't change other values that may exist in this registry key.

#### <a name="bkmk_reg-role"></a> Site system role logging options

You can configure settings globally or for a specific component on a site system that hosts a Configuration Manager server role.

To configure logging options for a specific server component, configure these **REG_DWORD** values under the following Windows Registry key:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\<ComponentName>\Logging`

For example, for the distribution point role:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP\Logging`

|Name  |Values  |Description  |
|---------|---------|---------|
|LogLevel|`0`: Verbose<br>`1`: Default<br>`2`: Warnings and errors<br>`3`: Errors only|The level of detail to write to log files.|
|LogMaxHistory|Any integer greater than or equal to zero, for example:<br>`0`: No history<br>`1`: Default|When a log file reaches the maximum size, the server renames it as a backup and creates a new log file. Specify how many previous versions to keep.|
|LogMaxSize|Any integer greater than or equal to 10,000, for example:<br>250000|The maximum log file size in bytes. When a log grows to the specified size, the server renames it as a history file, and creates a new file. The default value is 250,000 bytes.|

> [!Note]  
> Don't change other values that may exist in this registry key.

#### <a name="bkmk_reg-console"></a> Configuration Manager console logging options

To change the verbose level of the AdminUI.log for the Configuration Manager console, use the following procedure:

1. Open the console configuration file, **Microsoft.ConfigurationManagement.exe.config**, in an XML editor like Notepad. The default configuration file is in the following location: `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

1. Under the **system.diagnostics** > **sources** > **source** element, change the **switchValue** attribute from `Error` to `Verbose`. For example:

    Original: `<source name="SmsAdminUISnapIn" switchValue="Error">`
    New: `<source name="SmsAdminUISnapIn" switchValue="Verbose" >`

1. Save the file, and restart the console.

### <a name="bkmk_logoptions-console"></a> Configure logging options in the Configuration Manager console

<!-- 4433455 -->

Starting in version 1910, enable or disable verbose logging on a client or collection from the console:

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, select the **Devices** node, and choose a target device.

1. In the ribbon, on the **Home** tab, in the **Device** group, select **Client Diagnostics**. Choose one of the available actions.

For more information, see [Client diagnostics](/sccm/core/clients/manage/client-notification#client-diagnostics).

## <a name="BKMK_LogLocation"></a> Locating log files

Configuration Manager and dependent components store log files in various locations. These locations depend on the process that creates the log file and the configuration of your environment.

The following locations are the defaults. If you customized the installation directories in your environment, the actual paths may vary.

- Client: `C:\Windows\CCM\logs`
- Server: `C:\Program Files\Microsoft Configuration Manager\Logs`
- Management point: `C:\SMS_CCM\Logs`
- Configuration Manager console: `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog`
- IIS: `C:\inetpub\logs\logfiles\w3svc1`

### Task sequence log locations

The location of the task sequence log file **smsts.log** varies depending upon the phase of the task sequence:

- In Windows PE before [Format and Partition Disk](/sccm/osd/understand/task-sequence-steps#BKMK_FormatandPartitionDisk) step: `X:\Windows\temp\smstslog\smsts.log` (X is the Windows PE RAM drive)
- In Windows PE after **Format and Partition Disk** step: `X:\smstslog\smsts.log`, then copied to `C:\_SMSTaskSequence\Logs\smstslog\smsts.log` when drive is ready
- In the new Windows OS before the client is installed: `C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- In Windows after the client is installed: `C:\Windows\CCM\Logs\smstslog\smsts.log`
- In Windows after the task sequence completes: `C:\Windows\CCM\Logs\smsts.log`

> [!Tip]  
> The read-only task sequence variable [_SMSTSLogPath](/sccm/osd/understand/task-sequence-variables#SMSTSLogPath) always contains the path of the current log file.


## See also

- [Log files reference](/sccm/core/plan-design/hierarchy/log-files)

- [Support Center OneTrace](/sccm/core/support/support-center-onetrace)

- [Support Center log file viewer](/sccm/core/support/support-center#support-center-log-file-viewer)

- [CMTrace](/sccm/core/support/cmtrace)
