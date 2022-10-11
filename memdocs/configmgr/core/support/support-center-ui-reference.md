---
title: Support Center UI reference
titleSuffix: Configuration Manager
description: Learn how to use the Support Center tools.
ms.date: 12/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Support Center user interface reference

*Applies to: Configuration Manager (current branch)*

This article is a reference that describes the user interfaces (UI) of the following Support Center tools:

- Support Center Client Data Collector
- Support Center Client Tools
- Support Center Viewer
- Support Center Log File Viewer

> [!NOTE]
> In version 2010 and earlier, the Client Data Collector and Client Tools are combined into a single tool called **Support Center**.<!--8693068-->

The Support Center suite also includes **OneTrace**. For more information, see [Support Center OneTrace](support-center-onetrace.md).

## Support Center Client Data Collector

> [!NOTE]
> In version 2010 and earlier, this tool is part of the **Support Center** tool. The **Collect selected data** action is on the **Home** tab of the **Support Center** tool.

### Window menu (Client Data Collector)

In the upper left corner of the Support Center Client Data Collector window, select the arrow in the blue box to open this menu.

- **Local Machine Connection**: Gather data from the client that's running Support Center Client Data Collector.

- **Remote Connection**: Establish a remote connection with another Configuration Manager client. After connecting, gather data from the remote client.

- **About**: Provides information about Support Center Client Data Collector, such as the version.

- **Options**:

  - Reduce the movement of animated user interface elements
  - Change the default save location for data bundle files
  - Change the location of temporary files
  - Reset warnings. Any warning messages that you previously suppressed appear again when triggered.
  - Reset temporary file path to the default, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

- **Exit**: Close Support Center Client Data Collector.

### Home tab

#### Collect selected data

Support Center Client Data Collector collects information from the Configuration Manager client. You can then view this information using [Support Center Viewer](#support-center-viewer). By default, it collects the following types:

- Client log files
- Client configuration collector
- Operating system

To collect other types of information, select the checkbox next to the name for that type.

Select the drop-down at the bottom of the **Collect selected data** button in the ribbon, and select **Collect all data**. This action collects the complete set of client state data.

While Support Center Client Data Collector is collecting data, select **Cancel collection** to stop it.

For more information, see [Support Center quickstart guide](support-center-quickstart.md).

#### Data types

When you select the checkbox for an option, Support Center Client Data Collector collects that type of data the next time you select **Collect selected data**. The following types are available:

- **Log files**: Client log files including setup logs.

- **Policy**: Client policy collection.

- **Certificates**: Public key information for client certificates. Support Center Client Data Collector doesn't collect certificate private keys.

- **Client configuration collector**: Configuration Manager client information. You can't disable this data type.

- **Client registry**: Collects client configuration information from the registry. Support Center Client Data Collector only collects Configuration Manager registry information.

- **Client WMI**: Client configuration information from WMI. Support Center Client Data Collector doesn't collect client policy.

- **Troubleshooting**: Real-time troubleshooting data to help diagnose common client problems with Active Directory, management points, networking, policy assignments, and registration.

    > [!NOTE]
    > This data type isn't supported when you make a remote connection to another client.

- **Debug dumps**: Create a debug dump of client and related processes. Debug dumps can be large. Only enable this option when troubleshooting issues with client performance.

    > [!WARNING]
    > Collecting debug dumps will cause data bundles to become very large. In some cases, the size can be several hundred MB.
    >
    > Debug dumps contain may contain sensitive information, including passwords, cryptographic secrets, or user data. Only collect debug dumps on the recommendation of Microsoft Support personnel. Carefully handle data bundles that contain debug dumps to protect them from unauthorized access.
    >
    > This data type isn't supported when you make a remote connection to another client.

- **Operating system**: Collects configuration information about the local machine. This data includes information about the Windows installation, network adapters, and system service configuration. You can't disable this data type.

## Support Center Client Tools

This section describes the user interface for the **Support Center Client Tools** tool.

> [!NOTE]
> In version 2010 and earlier, this tool is called **Support Center**.
>
> Starting in version 2103, use the [Support Center Client Data Collector](#support-center-client-data-collector) for the **Collect selected data** action.

- [Window menu](#window-menu-client-tools)
- [Client tab](#client-tab)
- [Policy tab](#policy-tab-client-tools)
- [Content tab](#content-tab) 
- [Inventory tab](#inventory-tab)
- [Troubleshooting tab](#troubleshooting-tab-client-tools)
- [Logs tab](#logs-tab)

### Window menu (Client Tools)

In the upper left corner of the Support Center Client Tools window, select the arrow in the blue box to open this menu.

- **Local Machine Connection**: Gather log files and troubleshoot the client that's running Support Center.

- **Remote Connection**: Establish a remote connection with another Configuration Manager client. After connecting, gather log files and troubleshoot the remote client.

- **About**: Provides information about Support Center Client Tools, such as the version.

- **Options**:

  - Reduce the movement of animated user interface elements
  - Change the default save location for data bundle files
  - Change the location of temporary files
  - Reset warnings. Any warning messages that you previously suppressed appear again when triggered.
  - Reset temporary file path to the default, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

- **Exit**: Close Support Center Client Tools.

### Client tab

#### Load or Refresh (Client)

Load or refresh details for the Configuration Manager client.

#### Client information

When you load client details, this tool shows the following properties:

- **Client ID**: A unique identifier that Configuration Manager uses to identify the client.

- **Hardware ID**: A unique identifier that Configuration Manager uses to identify the client hardware.

- **Approved**: Indicates whether the client is approved in Configuration Manager.

- **Registration State**: Indicates whether the client is registered with Configuration Manager.

- **Internet-facing**: Indicates whether the client is on the internet.

- **Version**: The version number of the installed Configuration Manager client.

- **Site Code**: The site code for the primary site to which the client is assigned.

- **Assigned MP**: The fully qualified domain name (FQDN) of the client's currently assigned management point.

- **Resident MP**: The FQDN of the resident management point.

- **Proxy MP**: The hostname or FQDN of the proxy management point (if it exists).

- **Proxy Site Code**: The site code for the secondary site (if it exists).

- **Proxy State**: The state of the Configuration Manager client's proxy management point. For example, **Active** or **Pending**.

#### Maintenance windows

List all maintenance windows currently defined for this client. The next maintenance window displays a different status than future windows.

#### Control client agent service

Do one of the following actions for the Configuration Manager client agent service (ccmexec) on the connected client:

- **Restart client**

    > [!IMPORTANT]
    > If the client agent service doesn't successfully restart, the client isn't manageable by Configuration Manager until the service starts.

- **Start client**

- **Stop client**

    > [!IMPORTANT]
    > The client isn't manageable by Configuration Manager until the service starts.

### Policy tab (Client Tools)

Use the actions on this tab instead of the older [PolicySpy](policy-spy.md) tool.

#### Load policy

This option varies depending upon the view:

- **Load Actual policy**: Select **Actual** in the View group, and then select this option in the Policy group. Load the client policy that you've currently selected.

- **Load Requested policy**: Select **Requested** in the View group, and then select this option in the Policy group. Load the client policy requested of the client.

- **Load Default policy**: Select **Default** in the View group, and then select this option in the Policy group. Load the default policy for this client.

Select the drop-down list at the bottom of this button for other options:

- **Load or Refresh all**: Load or refresh the actual, requested, and default policy at the same time.

#### Actual view

Opens the actual policy view.

#### Requested view

Opens the requested policy view.

#### Default view

Opens the default policy view. This policy is what devices get when you install the Configuration Manager client.

#### Request and evaluate policy

Request the client policy from the management point, and then evaluate that policy on the client.

Select the drop-down list at the bottom of this button for other options:

- **Request policy**: Request the client policy from the management point.

- **Evaluate policy**: Evaluate the client policy on the client.

- **Reset policy to default**: Tell the Configuration Manager client to reapply the default policy. It removes all machine and user policies on the client.

#### Listen for policy events

Listen for policy events. Select this option again to disable listening for policy events. To view **Policy events**, select the arrow at the bottom of this tab.

#### Clear events

Clear any policy events.

### Content tab

View content on the client, including cached content. Monitor the progress of software update and application deployments.

#### Load or Refresh (Content)

*Applies to the Content and Cache views*

Load or refresh the list of content currently on the client.

#### Invoke trigger (Content)

The following items on this menu request a client action related to content:

- **Location services**

  - **Refresh content locations**: Refreshes the distribution points used by any active content downloads.

  - **Refresh management points**: Updates the internal list of management points used by the client.

  - **Time out content requests**: If any content location requests have been running for too long, this action stops the request.

- **Application deployment evaluation**: Starts a task that evaluates deployed applications.

- **Software updates deployment evaluation**: Starts a task that evaluates deployed software updates.

- **Software updates source scan**: Starts a task that scans update source locations.

- **Windows Installer source list update**: Starts a task that updates the source location for Windows Installer (MSI) installations.

#### Deployment view

See applications, packages, and updates that are loaded on the client. When you select an application, package, or update, you can view details on that content. For some applications, you can also do the following actions:

- **Refresh**: Refresh the details view.

- **Verify or Download**: Verify that an application is available for download.

- **Install**: Install the application.

- **Uninstall**: Uninstall the application.

Starting in Configuration Manager version 2107, the view is grouped by **Category** and **Status**. The view can be sorted and filtered to help you find the deployments you're interested in. Select a deployment in the results pane to display the following information in the details pane:

- **Properties** tab
   - **Name**: The name of the deployment property.
   - **Value**: The value assigned to the deployment property.

- **Policy** tab
   - **Display name**: Display name of the items in the deployment.
   - **Version**: Version for the item in the deployment.
   - **Model name**: Model name for the item in the deployment.
   - **CI XML**: XML for the configuration item.

- **Reporting** tab
   - **Time**: Timestamp of the state message.
   - **State** The state that was reported by the client.
   - **Topic ID**: ID of what the state message is reporting on, used to map to events in log files. In this context, it will typically be the Assignment ID of the deployment.
   - **Topic type**: The state message type.
   - **Topic type ID**: The subtype of the state message.
   - **State ID**: The result of the action that you're monitoring.
  

> [!Note]
> In Configuration Manager versions 2103 and earlier **Deployment view** is named **Content view**. <!--8272488-->

#### Cache view

View the client cache configuration and details about the cache contents. When you connect Support Center Client Tools to a local client, you can also do the following actions:

- To change the cache location, select **Change** next to the **Cache location** field.

- To adjust the size of the cache, select **Change** next to the **Cache size** field.

- To clear the client cache, select **Clear** next to the **Cache in use** field.

This view shows the following properties:

- **Location**: The location of each cache folder. Select the link to open the folder in Windows Explorer.
- **Content ID**
- **Cache ID**
- **Size**
- **Last Referenced**: This property is the date when the client last read from or wrote to this item in the cache.

#### Monitoring view

View the active progress of software update and application update deployments. This view shows state messages raised from application and software updates event WMI messages.

For each event, the view shows the following properties:

- **Time**: The time that the client raised the event.
- **Topic type**: The state message type.
- **Topic ID**: ID of the state message, used to map to events in log files.
- **Topic ID type**: The subtype of the state message.
- **State ID**: The result of the action that you're monitoring.
- **Details** and **Event data**: More information on the state messages shown in this view. State details may sometimes be blank.

#### All updates view

View details about software updates:

- State
- Article ID
- Bulletin
- Name
- Update ID
- Scan Time
- Source Version
- Source Unique ID

### Inventory tab

#### Load or Refresh (Inventory)

Load or refresh the client inventory list for the currently selected view.

#### Invoke trigger (Inventory)

> [!NOTE]
> For tasks other than **Software metering report cycle**:
>
> - If you request the task when another inventory task is already running, the client queues the new task to run after it completes the current task and other queued tasks.
> - Track the progress of the task in **InventoryAgent.log**.

The following items on this menu request client action related to inventory:

- **Discovery data collection cycle (heartbeat)**: Triggers the client task used to collect device discovery information.

- **File collection cycle**: Triggers the client task used to collect local files.

- **Hardware inventory cycle**: Triggers the client task used to collect hardware inventory data.

- **IDMIF collection cycle**: Triggers the client task used to collect IDMIF data.

- **Software inventory cycle**: Triggers the client task used to collect software inventory data.

- **Software metering report cycle**: Triggers the client task used to build a software metering report and send it to the management point. Track the progress of this task in **SWMTRReportGen.log**.

- **Send unsent state messages in queue**: Triggers the client task to flush the queue of state messages.

- **Advanced**

  - **Hardware inventory cycle (full resynchronization)**
  - **Software inventory cycle (full resynchronization)**

#### Views

If a feature isn't enabled, the view doesn't display any data.

- **Status**: Show the inventory data sets the client has collected.

- **DDR**: Information about the client discovery data collected from the client.

- **HINV**: Information about the hardware inventory data collected from the client.

- **SINV**: Information about the software inventory data collected from the client.

- **File collection**: Information about the files collected from the client.

- **IDMIF**: Information about the IDMIF and NOIDMIF data collected from the client.

- **Metering**: Information about the software metering data collected from the client.

### Troubleshooting tab (Client Tools)

Troubleshoot some of the most common issues with Configuration Manager clients:

- Issues with Active Directory
- Windows networking
- Configuration Manager
  - Management points
  - Policy assignment
  - Registration

> [!NOTE]
> This tab isn't available when you connect to a remote Configuration Manager client.

#### Start

Starts troubleshooting the client.

- **Active Directory**: Queries Active Directory to retrieve published Configuration Manager site information.
- **MPCERTIFICATE**: Gets management point certificates.
- **MPLIST**: Gets a list of management points.
- **MPKEYINFORMATION**: Gets management point cryptographic key information.
- **Networking**: Troubleshoots issues with networking.
- **Policy Assignments**: Retrieves policy assignments.
- **Registration**: Verifies that the client is registered with the site.

#### View selected log

After you select a row on the Troubleshooting tab, select this action to view the log file.

#### Keep previous results

If you troubleshoot the client, and then want to try troubleshooting again, choose this option to keep results from your first attempt. Otherwise, it overwrites previous troubleshooting log files.

### Logs tab

This tab of Support Center Client Tools is almost identical to the **Log Viewer** tool. The **Log Viewer** tool doesn't include the **Configure client logging** and **Log groups** features. The [Support Center Log File Viewer](#support-center-log-file-viewer) section details the other options available on this tab.

#### Tasks: Configure client logging

Set the following options:

- **Client log level**: Log verbosity and file size
- **Maximum file count**: Allow more than one log file of a given type
- **Maximum file size**: The size in bytes of any given log file before the client creates a new log

> [!NOTE]
> If you set these values too low, the client may not log any useful information. If you set these values too high, the client logs can consume large amounts of storage.

For more information, see [About log files](../plan-design/hierarchy/about-log-files.md).

#### Log groups

Instead of manually selecting log files using the **Open logs** button, use this drop-down list to open all log files associated with the following feature areas:

- **Desired Configuration Management**
- **Inventory**
- **Software Distribution**
- **Software Updates**
- **Application Management**
- **Policy**
- **Client Registration**
- **Operating System Deployment**

## Support Center Viewer

This section describes the user interface (UI) for the Configuration Manager **Support Center Viewer** tool. The available tabs vary based on the contents of the troubleshooting bundle. The [Window menu](#window-menu-viewer) and [Home tab](#home-tab-viewer) show by default.

- [Window menu](#window-menu-viewer)
- [Home tab](#home-tab-viewer)
- [Configuration tab](#configuration-tab)
- [Logs tab](#logs-tab-viewer)
- [Debug dumps tab](#debug-dumps-tab)
- [WMI tab](#wmi-tab)
- [Registry tab](#registry-tab)
- [Policy tab](#policy-tab-viewer)
- [Certificates tab](#certificates-tab)
- [Troubleshooting tab](#troubleshooting-tab-viewer)

### Window menu (Viewer)

In the upper left corner of the Support Center Viewer window, select the arrow in the blue box to open this menu.

- **Open bundle**: Browse to the location of a data bundle created by one of the following tools:

  - Version 2103 and later: Support Center Client Data Collector
  - Version 2010 and earlier: Support Center

- **About**: Displays information about Support Center Viewer, such as the version.

- **Options**:

  - Reduce the movement of animated user interface elements.
  - Change the location of temporary files.
  - Reset warnings. Any warning messages that you previously suppressed appear again when triggered.
  - Reset temporary file path to the default, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`

- **Exit**: Exits Support Center Viewer.

### Home tab (Viewer)

#### Open bundle

Browse to the location of a data bundle created by one of the following tools:

- Version 2103 and later: Support Center Client Data Collector
- Version 2010 and earlier: Support Center

#### Open log file

Select one or more log files to open.

#### Decode certificate (Viewer: Home)

In the **Decode certificate** window, paste the serialized certificate value for any certificate on the client. Find this value in the registry, in log files, or in WMI. Select **Process** to view general information and details on the certificate. This information includes its certification path. Select **Export** to export the certificate as a **.cer** file.

### Configuration tab

The **Configuration** tab of the Support Center Viewer tool provides the following views using data retrieved from WMI providers:

- **Client**: This view displays the same information shown on the **Client** tab of Support Center.

- **Operating system**: Details for the client's OS. It uses the [Win32_OperatingSystem](/windows/desktop/CIMWin32Prov/win32-operatingsystem) class.

- **Computer**: Details for the client computer. It uses the [Win32_OperatingSystem](/windows/desktop/CIMWin32Prov/win32-operatingsystem) class.

- **Services**:  Details for services running on the client computer. It uses the [Win32_Service](/windows/desktop/CIMWin32Prov/win32-service) class.

- **Network adapters**: Details for network adapters installed on the client computer. It uses the [Win32_NetworkAdapterConfiguration](/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration) class.

### Logs tab (Viewer)

The **Logs** tab shows a list of the log files included in the bundle. Each row on this tab provides the path, name, and size of the log file.

#### Open

After selecting a log file, select this button to open the **Log Viewer**. It provides a subset of the functionality seen on the Support Center Client Tools **Logs** tab.

#### Decode certificate (Viewer: Logs)

In the **Decode certificate** window, paste the serialized certificate value for any certificate on the client. Find this value in the registry, in log files, or in WMI. Select **Process** to view general information and details on the certificate. This information includes its certification path. Select **Export** to export the certificate as a **.cer** file.

### Debug dumps tab

Each row on this tab provides details on the debug dump files that are available to export. Use this tab to export debug dump files (.dmp) for further analysis. This analysis uses a debugging tool such as WinDbg.

> [!WARNING]
> Debug dumps may contain sensitive information, including passwords, cryptographic secrets, or user data. Only collect debug dumps on the recommendation of Microsoft Support personnel. Carefully handle data bundles that contain debug dumps to protect them from unauthorized access.

#### Export (Viewer: Debug dumps)

Save a copy of the selected debug dump file.

### WMI tab

This tab shows the set of WMI data from the Configuration Manager client that the data bundle includes.

#### Find (Viewer: WMI)

Opens the Find window, which has the following features:

- **Find what**: Enter a string to search for in the WMI data set. It supports wildcard characters.

- **Look at**: Choose whether you want to search within the WMI data set for a matching **Class or instance name**, **Property**, or **Value**.

- **Match whole string only**: By default, it searches for strings that contain the string for which you're looking. Choose this checkbox to only find strings that are an exact match to the string that you provided.

#### Find next (Viewer: WMI)

Open the next instance of the search string in the WMI data set.

#### Decode certificate (Viewer: WMI)

In the **Decode certificate** window, paste the serialized certificate value for any certificate on the client. Find this value in the registry, in log files, or in WMI. Select **Process** to view general information and details on the certificate. This information includes its certification path. Select **Export** to export the certificate as a **.cer** file.

### Registry tab

Use the **Registry** tab to view registry data included in the data bundle, and to export that data for further analysis.

#### Export (Viewer: Registry)

Save a copy of the registry key and subkeys that you select as a registry (.reg) file.

#### Find (Viewer: Registry)

Opens the Find window, which has the following features:  

- **Find what**: Enter a string to search for in the WMI data set. It supports wildcard characters.  

- **Look at**: Choose whether you want to search within the WMI data set for a matching **Class or instance name**, **Property**, or **Value**.  

- **Match whole string only**: By default, it searches for strings that contain the string for which you're looking. Choose this checkbox to only find strings that are an exact match to the string that you provided.  

#### Find next (Viewer: Registry)

Open the next instance of the search string in the WMI data set.

#### Decode certificate (Viewer: Registry)

In the **Decode certificate** window, paste the serialized certificate value for any certificate on the client. Find this value in the registry, in log files, or in WMI. Select **Process** to view general information and details on the certificate. This information includes its certification path. Select **Export** to export the certificate as a **.cer** file.

### Policy tab (Viewer)

The **Policy** tab is used to view policy data included in the data bundle.

#### Find (Viewer: Policy)

Opens the Find window, which has the following features:

- **Find what**: Enter a string to search for in the WMI data set. It supports wildcard characters.

- **Look at**: Choose whether you want to search within the WMI data set for a matching **Class or instance name**, **Property**, or **Value**.

- **Match whole string only**: By default, it searches for strings that contain the string for which you're looking. Choose this checkbox to only find strings that are an exact match to the string that you provided.

#### Find next (Viewer: Policy)

Open the next instance of the search string in the WMI data set.

#### Decode certificate (Viewer: Policy)

In the **Decode certificate** window, paste the serialized certificate value for any certificate on the client. Find this value in the registry, in log files, or in WMI. Select **Process** to view general information and details on the certificate. This information includes its certification path. Select **Export** to export the certificate as a **.cer** file.

### Certificates tab

Use the **Certificates** tab to view certificates included in the data bundle, and to export them.

#### View certificate

Displays information about a selected certificate.

#### Export (Viewer: Certificates)

Save a copy of the certificate that you select.

### Troubleshooting tab (Viewer)

Use the **Troubleshooting** tab to view log files created using the Troubleshooting tab of Support Center Client Tools.

#### View log

After you select a row on the **Troubleshooting** tab, select this option to view the log file with Log File Viewer.

## Support Center Log File Viewer

This section describes the user interface for the **Support Center Log File Viewer** tool.

- [Window menu](#window-menu-log-file-viewer)
- [Home tab](#home-tab-log-file-viewer)

This tool is almost identical to the **Logs** tab of **Support Center Client Tools**. The main difference is that this tool doesn't include the options to **Configure client logging** and **Log groups**.

Starting in version 2111, Support Center Log File Viewer display status messages in an easy to read format. Entries starting with `>>` are status messages that are automatically converted into a readable format when a log is opened. Search or filter on the `>>` string to find status messages in the log. <!--9348231, 10915091-->


### Window menu (Log File Viewer)

In the upper left corner of the Support Center Log File Viewer window, select the arrow in the blue box to open this menu.

- **Open logs**:  Browse to the location of log files to open.

- **Options**:

  - Reduce the movement of animated user interface elements.
  - Register Log File Viewer as the default app for log files with the `.log` and `.lo_` file extensions.
  - Reset warnings. Any warning messages that you previously suppressed appear again when triggered.

- **About**: Displays information about Support Center Log File Viewer, such as the version.

- **Close**: Closes Support Center Log File Viewer

### Home tab (Log File Viewer)

#### Open logs

Support Center Log File Viewer prompts you to select one or more log files to open.

Select the drop-down at the bottom of the **Open logs** button in the ribbon, and select one of the following options:

- **Open logs in current view**: Opens the selected log files in the current view.
- **Open logs in new window**: Opens the selected log files in a new **Log Viewer** window.

#### Close and clear logs

Closes any open log files. Also clears any displayed log file entries from the window. Support Center Log File Viewer won't display these entries in the future.

Select the drop-down at the bottom of the **Close and clear logs** button in the ribbon, and select one of the following options:

- **Clear all entries**: Clears any displayed log file entries from the window. Support Center Log File Viewer won't display these entries in the future.
- **Close all logs**: Closes any open log files.

#### Find (Log File Viewer)

Opens the **Find** window. Enter a string to search for. To avoid matches on short strings in other strings, you can choose to match whole words. You can also choose to do a case-sensitive match for the string.

#### Find next (Log File Viewer)

After finding a match for the string that you're searching for, this option takes you to the next match.

#### Find previous (Log File Viewer)

After finding two or more matches for the string that you're searching for, this option takes you to the previous match.

#### Options

- **Live updating**: Monitor a currently open log file for changes. This feature doesn't function when multiple log files are open. This option is enabled by default.

- **Auto-scroll**: If you also chose the **Live updating** option, this option automatically scrolls the log view to show newly added entries. This feature doesn't function when multiple log files are open. This option is enabled by default.

- **Show details**: When you select a log file message, the bottom of the **Logs** tab displays the details of the log file message. This option is enabled by default.

- **Quick filter**: Filter the log file messages across all open log files to find a specific string. You can filter by log text, component name, and thread ID. To find similar log messages, right-click a log message and select **Quick filter** on log text.

- **Wrap log text**: Wrap long and multi-line messages to fit into a single column. This behavior makes these messages easier to read. This option is enabled by default.

- **Raw log entry display**: Displays unprocessed log lines.

- **Advanced filters**: Open the **Advanced filters** window. For more information, see [Advanced log file filters](#advanced-log-file-filters).

- **Error code links**: Error codes in log text are highlighted and clickable. This option is enabled by default.

#### Error lookup

Enter an error code to search for that error code in currently open log files. Use the following error code formats:

- **32-bit integer (signed)**: For example, `-2147024891`
- **32-bit integer (unsigned)**: For example, `2147942405`
- **32-bit hexadecimal**: For example, `0x80070005`

#### Decode certificate (Log File Viewer)

In the **Decode certificate** window, paste the serialized certificate value for any certificate on the client. Find this value in the registry, in log files, or in WMI. Select **Process** to view general information and details on the certificate. This information includes its certification path. Select **Export** to export the certificate as a **.cer** file.

## Advanced log file filters

Advanced log file filters allow you to include, exclude, or highlight specific strings. These strings can occur in a log file or log file group when looking at log file entries. Use wildcard searches when creating a filter. When you have a useful combination of filters, save them as a *filter set*.

Advanced log file filters supersede quick filters. Use both together, but quick filters only apply to the displayed log data. Advanced filters determine what data is initially displayed before any it applies any quick filters.

In the Advanced filters window, you can create complex filter sets. These filter sets search for strings across many log file components. These components include messages, threads, logging levels, and components. A filter set contains multiple filter statements that you use to include, exclude, or highlight log file messages. A filter defines a log file column to search within, an operator, and a value. The value can contain regular expressions, such as the *wildcard* character `*`.

### Add a filter

1. In the Log File Viewer tool, or on the Support Center Client Tools **Logs** tab, select **Advanced filters**.

1. In the Advanced filters window, select **Add**. Then select one of the following options to act on log entries that match your filter:

    - **Include**
    - **Exclude**
    - **Highlight**

1. In the **Advanced filter configuration** window, choose a column and an operator:

    - **Column**: Choose where to look for strings that match your filter:

         - **Log text**: Search within the text of a log file

         - **Log severity**: Search for logs with a specific severity level. Set these severity levels in the **Value** field.

         - **Component**: Search for a specific component by name

         - **Thread ID**: Search for log messages with a specific thread ID

         - **Source file**: Search for log messages that occur in a specific log file

    - **Operator**: Choose an operator for your filter

1. Enter a value to filter on in the **Value** field. If your value contains regular expressions, select **Enable regular expression matching**.

### Manage filter sets

- To edit a filter, select the filter, and then select **Edit**.

- To delete a filter, select the filter, and then select **Delete**.

- To clear all filters, select **Clear**.

- To save the current filter set, select **Save filters**. Then save your filter set as a `.filterset` file.

- To load a saved filter set, select **Load filters**. Then browse to a previously saved `.filterset` file.
