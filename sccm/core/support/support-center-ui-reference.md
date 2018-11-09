---
title: Support Center UI reference
titleSuffix: Configuration Manager
description: Learn how to use the Support Center tools.
ms.date: 11/16/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 41cdebfe-b595-40aa-a385-32e0746255ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

## Support Center user interface reference

*Applies to: System Center Configuration Manager (Current Branch)*

This article is a reference describing the user interfaces (UI) of the Support Center tools:
- Support Center
- Support Center Log Viewer
- Support Center Viewer



## Support Center reference

This section describes the user interface for the **Support Center** tool. 
- [Window menu](#bkmk_support-window)  
- [Home tab](#bkmk_support-home)  
- [Client tab](#bkmk_support-client)  
- [Policy tab](#bkmk_support-policy)  
- [Content tab](#bkmk_support-content)  
- [Inventory tab](#bkmk_support-inventory)  
- [Troubleshooting tab](#bkmk_support-troubleshoot)  
- [Logs tab](#bkmk_support-logs)  


### <a name="bkmk_support-window"></a> Window menu

In the upper left corner of the Support Center window, select the arrow in the blue box to open this menu.

#### Local Machine Connection
Support Center gathers log files and performs troubleshooting on the client that's running Support Center.

#### Remote Connection
Establish a remote connection with another Configuration Manager client. After connecting, Support Center gathers log files and performs troubleshooting on the client to which it's connected.

#### About
Provides information about Support Center.

#### Options
In the **Options** dialog, you can:
- Reduce the movement of animated user interface elements  
- Change the default save location for data bundle files  
- Change the location of temporary files    
- Reset warnings. Any warning messages that you previously suppressed appear again when triggered.  
- Reset temporary file path to the default, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

#### Exit
Close Support Center.



### <a name="bkmk_support-home"></a> Home tab

#### Collect selected data
Support Center collects information from the Configuration Manager client. By default, it collects the following types:
- Log files
- Client configuration collector
- Operating system

To collect other types of information, select the checkbox next to the name for that type.

Select the drop-down at the bottom of the **Collect selected data** button in the ribbon, and select **Collect all data**. This action collects the complete set of client state data.

While Support Center is collecting data, select **Cancel collection** to stop it.

#### Data types
When you select the checkbox for an option, Support Center collects that type of data the next time you select **Collect selected data**. The following types are available:  

- **Log files**: Client log files including setup logs  

- **Policy**: Client policy collection  

- **Certificates**: Public key information for client certificates. Support Center doesn't collect certificate private keys.  

- **Client configuration collector**: Configuration Manager client information. You can't disable this data type.  

- **Client registry**: Collects client configuration information from the registry. Support Center only collects Configuration Manager registry information.  

- **Client WMI**: Client configuration information from WMI. Support Center doesn't collect client policy.  

- **Troubleshooting**: Real-time troubleshooting data to help diagnose common client problems with Active Directory, management points, networking, policy assignments, and registration.  

    > [!NOTE]  
    > This data type isn't supported when you make a remote connection to another client.  

- **Debug dumps**: Perform debug dump of client and related processes. Debug dumps can be large. Only enable this option when troubleshooting issues with client performance.  

    > [!WARNING]  
    > Collecting debug dumps will cause data bundles to become very large (in some cases, several hundred MB).  
    >  
    > Debug dumps contain may contain sensitive information, including passwords, cryptographic secrets, or user data. Debug dumps should only be collected on the recommendation of Microsoft Support personnel. Data bundles that contain debug dumps should be handled carefully to protect them from unauthorized access.  
    >  
    > This data type isn't supported when you make a remote connection to another client.  

- **Operating system**: Collects configuration information about the local machine. This data includes information about the Windows installation, network adapters, and system service configuration. You can't disable this data type.  



### <a name="bkmk_support-client"></a> Client tab

#### Load or Refresh
Support Center loads or refreshes details for the Configuration Manager client.

#### Control client agent service
Perform one of the following actions on the Configuration Manager client agent service (ccmexec) on the connected client:  

- **Restart client**  

    > [!IMPORTANT]  
    > If the client agent service doesn't successfully restart, the client isn't manageable by Configuration Manager until the service starts.  

- **Start client**  

- **Stop client**  

    > [!IMPORTANT]  
    > The client isn't manageable by Configuration Manager until the service starts.  

#### Properties
When you load client details, Support Center shows the following properties:  

- **Client ID**: A unique identifier that Configuration Manager uses to identify the client  

- **Hardware ID**: A unique identifier that Configuration Manager uses to identify the client hardware  

- **Approved**: Indicates whether the client is approved in Configuration Manager  

- **Registration State**: Indicates whether the client is registered with Configuration Manager  

- **Internet-facing**: Indicates whether the client is on the internet  

- **Version**: The version number of the installed Configuration Manager client  

- **Site Code**: The site code for the primary site to which the client is assigned  

- **Assigned MP**: The fully qualified domain name (FQDN) of the client's currently assigned management point  

- **Resident MP**: The FQDN of the resident management point  

- **Proxy MP**: The hostname or FQDN of the proxy management point (if it exists)  

- **Proxy Site Code**: The site code for the secondary site (if it exists)  

- **Proxy State**: The state of the Configuration Manager client's proxy management point. For example, **Active** or **Pending**.  



### <a name="bkmk_support-policy"></a> Policy tab

Use the actions on this tab instead of the older [PolicySpy](/sccm/core/support/policy-spy) tool.

#### Load policy
This option varies depending upon the view:

- **Load Actual policy**: Select **Actual** in the View group, and then select this option in the Policy group. Support Center loads the client policy that you've currently selected.  

- **Load Requested policy**: Select **Requested** in the View group, and then select this option in the Policy group. Support Center loads the client policy requested of the client.  

- **Load Default policy**: Select **Default** in the View group, and then select this option in the Policy group. Support Center loads the default policy for this client.  

Select the drop-down list at the bottom of this button for additional options:

- **Load or Refresh all**: Loads or refreshes the actual, requested, and default policy at the same time.  

#### Actual view
Opens the actual policy view

#### Requested view
Opens the requested policy view

#### Default view
Opens the default policy view. (This policy is what devices get when you install the Configuration Manager client.)

#### Request and evaluate policy
Support Center requests the client policy from the management point, and then evaluates that policy on the client.

Select the drop-down list at the bottom of this button for additional options:  

- **Request policy**: Support Center requests the client policy from the management point.  

- **Evaluate policy**: Support Center evaluates the client policy on the client.  

- **Reset policy to default**: Support Center tells the Configuration Manager client to reapply the default policy. It removes all machine and user policies on the client.  

#### Listen for policy events
Support Center listens for policy events. Select this option again to disable listening for policy events. To view **Policy events**, select the arrow at the bottom of this tab. 

#### Clear events
Support Center clears any policy events.



### <a name="bkmk_support-content"></a> Content tab

View content on the client, including cached content. Monitor the progress of software update and application deployments. 

#### Load or Refresh
*Applies to the Content and Cache views*

Support Center loads or refreshes the list of content currently on the client.

#### Invoke trigger
The following items on this menu request a client action related to content:  

- **Location services**  

    - **Refresh content locations**: Refreshes the distribution points used by any active content downloads.  

    - **Refresh management points**: Updates the internal list of management points used by the client.  

    - **Time out content requests**: If any content location requests have been running for too long, this action stops the request.  

 - **Application deployment evaluation**: Starts a task that evaluates deployed applications.  

 - **Software updates deployment evaluation**: Starts a task that evaluates deployed software updates.  

 - **Software updates source scan**: Starts a task that scans update source locations.  

 - **Windows Installer source list update**: Starts a task that updates the source location for Windows Installer (MSI) installations.  

#### Content view
See applications, packages, and updates that are loaded on the client. When you select an application, package or update, you can view details on that content. For some applications, you can also do the following actions:  

 - **Refresh**: Refresh the details view  

 - **Verify or Download**: Verify that an application is available for download  

 - **Install**: Install the application  

 - **Uninstall**: Uninstall the application  

#### Cache view
View the client cache configuration and details about the cache contents. When you connect Support Center to a local client, you ca also do the following actions:  

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
Select **Monitor** to view the active progress of software update and application update deployments. This view shows state messages raised from application and software updates event WMI messages.

For each event, the view shows the following properties:  

 - **Time**: The time that the client raised the event  
 - **Topic type**: The state message type  
 - **Topic ID**: ID of the state message, used to map to events in log files  
 - **Topic ID type**: The subtype of the state message  
 - **State ID**: The result of the action that you're monitoring  
 - **Details** and **Event data**: More information on the state messages shown in this view. State details may sometimes be blank.  



### <a name="bkmk_support-inventory"></a> Inventory tab

#### Load or Refresh
Support Center loads or refreshes the client inventory list for the currently selected view.

#### Invoke trigger

> [!Note]  
> For tasks other than **Software metering report cycle**:  
> - If you request the task when another inventory task is already running, the client queues the new task to run after it completes the current task and other queued tasks.  
> - Track the progress of the task in **InventoryAgent.log**.  

The following items on this menu request client action related to inventory:  

 - **Discovery data collection cycle (heartbeat)**: Triggers the client task used to collect device discovery information  

 - **File collection cycle**: Triggers the client task used to collect local files  

 - **Hardware inventory cycle**: Triggers the client task used to collect hardware inventory data  

 - **IDMIF collection cycle**: Triggers the client task used to collect IDMIF data  

 - **Software inventory cycle**: Triggers the client task used to collect software inventory data  

 - **Software metering report cycle**: Triggers the client task used to build a software metering report and send it to the management point. Track the progress of this task in **SWMTRReportGen.log**.

 - **Send unsent state messages in queue**: Triggers the client task to flush the queue of state messages.

 - **Advanced**  
     - **Hardware inventory cycle (full resynchronization)**  
     - **Software inventory cycle (full resynchronization)**  


#### Views
If a feature isn't enabled, the view doesn't display any data. 

- **Status**: Show the inventory data sets the client has collected  

- **DDR**: Information about the client discovery data collected from the client  

- **HINV**: Information about the hardware inventory data collected from the client  

- **SINV**: Information about the software inventory data collected from the client  

- **File collection**: Information about the files collected from the client  

- **IDMIF**: Information about the IDMIF and NOIDMIF data collected from the client  

- **Metering**: Information about the software metering data collected from the client  



### <a name="bkmk_support-troubleshoot"></a> Troubleshooting tab

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
Starts troubleshooting the client

- **Active Directory**: Queries Active Directory to retrieve published Configuration Manager site information  
- **MPCERTIFICATE**: Gets management point certificates  
- **MPLIST**: Gets a list of management points  
- **MPKEYINFORMATION**: Gets management point cryptographic key information	 
- **Networking**: Troubleshoots issues with networking  
- **Policy Assignments**: Retrieves policy assignments  
- **Registration**: Verifies that the client is registered with the site  

#### View selected log
After you select a row on the Troubleshooting tab, select this action to view the log file.

#### Keep previous results
If you troubleshoot the client, and then want to try troubleshooting again, choose this option to retain results from your first attempt. Otherwise, Support Center overwrites previous troubleshooting log files.



### <a name="bkmk_support-logs"></a> Logs tab

This section lists the items on the **Logs** tab of the Support Center tool. 

This tab is almost identical to the **Log Viewer** tool. The **Log Viewer** tool doesn't include the **Configure client logging** and **Log groups** features described in this section. The [Support Center Log Viewer reference](#bkmk_log-viewer) section details the other options available on this tab.

#### Configure client logging

> [!Note]  
> This feature is only on the **Logs** tab of the Support Center tool. It's not in the Log Viewer tool.  

Set the following options: 
- **Client log level**: Log verbosity and file size  
- **Maximum file count**: Allow more than one log file of a given type  
- **Maximum file size**: The size in bytes of any given log file before the client creates a new log  

> [!NOTE]  
> If you set these values too low, the client may not log any useful information. If you set these values too high, the client logs can consume large amounts of storage.  

#### Log groups

> [!Note]  
> This feature is only on the **Logs** tab of the Support Center tool. It's not in the Log Viewer tool.  

Instead of manually selecting log files using the **Open logs** button, use this drop-down list to open all log files associated with the following feature areas: 
- **Desired Configuration Management**
- **Inventory**
- **Software Distribution**
- **Software Updates**
- **Application Management**
- **Policy**
- **Client Registration**
- **Operating System Deployment**


## <a name="bkmk_log-viewer"></a> Support Center Log Viewer reference

This section describes the user interface for the **Support Center Log Viewer** tool. 

- [Window menu](#bkmk_log-window)  
- [Home tab](#bkmk_log-home)  

The **Log Viewer** tool is almost identical to the **Logs** tab of **Support Center**. The **Log Viewer** tool doesn't include the options to **Configure client logging** and **Log groups**.


### <a name="bkmk_log-window"></a> Window menu

In the upper left corner of the Support Center Log Viewer window, select the arrow in the blue box to open this menu.

#### Open logs
Browse to the location of log files to open. 

#### Options
In the **Options** dialog, you can:
- Reduce the movement of animated user interface elements  
- Register Log Viewer as the default app for log files with the .log and .lo_ file extensions  
- Reset warnings. Any warning messages that you previously suppressed appear again when triggered.  

#### About
Displays information about Support Center Log Viewer

#### Close
Closes Support Center Log Viewer


### <a name="bkmk_log-home"></a> Home tab

#### Open logs 
Support Center prompts you to select one or more log files to open.

Select the drop-down at the bottom of the **Open logs** button in the ribbon, and select one of the following additional options: 
- **Open logs in current view**: Opens the selected log files in the current view  
- **Open logs in new window**: Opens the selected log files in a new **Log Viewer** window  

#### Close and clear logs
Closes any open log files. Also clears any displayed log file entries from the window. Support Center won't display these entries in the future.

Select the drop-down at the bottom of the **Close and clear logs** button in the ribbon, and select one of the following additional options: 
- **Clear all entries**: Clears any displayed log file entries from the window. Support Center won't display these entries in the future.  
- **Close all logs**: Closes any open log files  

#### Find
Opens the **Find** dialog. Enter a string to search for. To avoid matches on short strings in other strings, you can choose to match whole words. You can also choose to do a case-sensitive match for the string.

#### Find next
After finding a match for the string that you're searching for, this option takes you to the next match.

#### Find previous
After finding two or more matches for the string that you're searching for, this option takes you to the previous match.

#### Options

- **Live updating**: Monitor a currently open log file for changes. This feature doesn't function when multiple log files are open. This option is enabled by default.  

- **Auto-scroll**: If you also chose the **Live updating** option, this option automatically scrolls the log view to show newly added entries. This feature doesn't function when multiple log files are open. This option is enabled by default.  

- **Show details**: When you select a log file message, the bottom of the **Logs** tab displays the details of the log file message. This option is enabled by default.  

- **Quick filter**: Filter the log file messages across all open log files to find a specific string. You can filter by log text, component name, and thread ID. To find similar log messages, right-click a log message and select **Quick filter** on log text.  

- **Wrap log text**: Wrap long and multi-line messages to fit into a single column. This behavior makes these messages easier to read. This option is enabled by default.  

- **Raw log entry display**: Displays unprocessed log lines.  

- **Advanced filters**: Open the **Advanced filters** dialog. For more information, see [Advanced log file filters](#bkmk_adv-filters).  

- **Error code links**: Error codes in log text are highlighted and clickable. This option is enabled by default.  

#### Error lookup
Enter an error code to search for that error code in currently open log files. Use the following error code formats:
 - **32-bit integer (signed)**: For example, `-2147024891`  
 - **32-bit integer (unsigned)**: For example, `2147942405`  
 - **32-bit hexadecimal**: For example, `0x80070005`  

#### Decode certificate
In the **Decode certificate** dialog box, paste the serialized certificate value for any certificate on the client. Find this value in the registry, in log files, or in WMI. Select **Process** to view general information and details on the certificate. This information includes its certification path. Select **Export** to export the certificate as a **.cer** file.



## <a name="bkmk_adv-filters"></a> Advanced log file filters

Advanced log file filters allow you to include, exclude, or highlight specific strings. These strings can occur in a log file or log file group when looking at log file entries. Use wildcard searches when creating a filter. When you have a useful combination of filters, save them as a *filter set*. 

Advanced log file filters supersede quick filters. Use both together, but quick filters only apply to the displayed log data. Advanced filters determine what data is initially displayed before any it applies any quick filters.

In the Advanced filters dialog, you can create complex filter sets. These filter sets search for strings across many log file components. These components include messages, threads, logging levels, and components. A filter set contains multiple filter statements that you use to include, exclude, or highlight log file messages. A filter defines a log file column to search within, an operator, and a value. The value can contain regular expressions, such as the *wildcard* character `*`.


### Add a filter

1. In the **Log Viewer** window, or on the Support Center **Logs** tab, select **Advanced filters**.  

2. In the Advanced filters dialog, select **Add**. Then select one of the following options to act on log entries that match your filter:  
    - **Include**  
    - **Exclude**  
    - **Highlight**  

3. In the **Advanced filter configuration** dialog, choose a column and an operator:  

    - **Column**: Choose where to look for strings that match your filter:  

         - **Log text**: Search within the text of a log file  

         - **Log severity**: Search for logs with a specific severity level. Set these severity levels in the **Value** field.  

         - **Component**: Search for a specific component by name  

         - **Thread ID**: Search for log messages with a specific thread ID  

         - **Source file**: Search for log messages that occur in a specific log file  

    - **Operator**: Choose an operator for your filter  

4. Enter a value to filter on in the **Value** field. If your value contains regular expressions, select **Enable regular expression matching**.  


### Manage filter sets

  - To edit a filter, select the filter, and then select **Edit**.  

  - To delete a filter, select the filter, and then select **Delete**.  

  - To clear all filters, select **Clear**.  

  - To save the current filter set, select **Save filters**. Then save your filter set as a **.filterset** file.  

  - To load a saved filter set, select **Load filters**. Then browse to a previously saved **.filterset** file.  



## <a name="bkmk_viewer"></a> Support Center Viewer reference

This section describes the user interface (UI) for the Configuration Manager **Support Center Viewer** tool. The available tabs vary based on the contents of the troubleshooting bundle. The [Window menu](#bkmk_viewer-window) and [Home tab](#bkmk_viewer-home) show by default.
- [Window menu](#bkmk_viewer-window)
- [Home tab](#bkmk_viewer-home)
- [Configuration tab](#bkmk_viewer-config)
- [Logs tab](#bkmk_viewer-logs)
- [Debug dumps tab](#bkmk_viewer-debug)
- [WMI tab](#bkmk_viewer-wmi)
- [Registry tab](#bkmk_viewer-registry)
- [Policy tab](#bkmk_viewer-policy)
- [Certificates tab](#bkmk_viewer-certs)
- [Troubleshooting tab](#bkmk_viewer-troubleshoot)


### <a name="bkmk_viewer-window"></a> Window menu

In the upper left corner of the Support Center Viewer window, select the arrow in the blue box to open this menu.

#### Open bundle
Browse to the location of a data bundle created by Support Center.

#### About
Displays information about Support Center Viewer.

#### Options
In the **Options** dialog, you can:
- Reduce the movement of animated user interface elements  
- Change the location of temporary files    
- Reset warnings. Any warning messages that you previously suppressed appear again when triggered.  
- Reset temporary file path to the default, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`  


#### Exit
Exits Support Center Viewer


### <a name="bkmk_viewer-home"></a> Home tab

#### Open bundle
Browse to the location of a data bundle created by Support Center.

#### Open log file
Select one or more log files to open.

#### Decode certificate
In the **Decode certificate** dialog box, paste the serialized certificate value for any certificate on the client. Find this value in the registry, in log files, or in WMI. Select **Process** to view general information and details on the certificate. This information includes its certification path. Select **Export** to export the certificate as a **.cer** file.


### <a name="bkmk_viewer-config"></a> Configuration tab

The **Configuration** tab of the Support Center Viewer tool provides the following views using data retrieved from WMI providers:

#### Client
This view displays the same information shown on the **Client** tab of Support Center.

#### Operating system
Details for the client's operating system. It uses the [Win32_OperatingSystem](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem) class.

#### Computer
Details for the client computer. It uses the [Win32_OperatingSystem](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem) class.

#### Services
Details for services running on the client computer. It uses the [Win32_Service](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-service) class.

#### Network adapters
Details for network adapters installed on the client computer. It uses the [Win32_NetworkAdapterConfiguration](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration) class.


### <a name="bkmk_viewer-logs"></a> Logs tab

The **Logs** tab shows a list of the log files included in the bundle. Each row on this tab provides the path, name, and size of the log file. 

#### Open
After selecting a log file, select this button to open the **Log Viewer**. It provides a subset of the functionality seen on the Support Center Logs tab.

#### Decode certificate
In the **Decode certificate** dialog box, paste the serialized certificate value for any certificate on the client. Find this value in the registry, in log files, or in WMI. Select **Process** to view general information and details on the certificate. This information includes its certification path. Select **Export** to export the certificate as a **.cer** file.


### <a name="bkmk_viewer-debug"></a> Debug dumps tab

Each row on this tab provides details on the debug dump files that are available to export. Use this tab to export debug dump files (.dmp) for further analysis. This analysis uses a debugging tool such as WinDbg. 

> [!WARNING]  
> Debug dumps may contain sensitive information, including passwords, cryptographic secrets, or user data. Only collect debug dumps on the recommendation of Microsoft Support personnel. Data bundles that contain debug dumps should be handled carefully to protect them from unauthorized access.  

#### Export
Save a copy of the selected debug dump file.


### <a name="bkmk_viewer-wmi"></a> WMI tab

This tab shows the set of WMI data from the Configuration Manager client that the data bundle includes. 

#### Find
Opens the Find dialog, which has the following features:  

- **Find what**: Enter a string to search for in the WMI data set. It supports wildcard characters.  

- **Look at**: Choose whether you want to search within the WMI data set for a matching **Class or instance name**, **Property**, or **Value**.  

- **Match whole string only**: By default, the find dialog searches for strings that contain the string for which you're looking. Choose this checkbox to only find strings that are an exact match to the string that you provided.  

#### Find next
This button opens the next instance of the string that you provided in the Find dialog within the WMI data set.

#### Decode certificate
In the **Decode certificate** dialog box, paste the serialized certificate value for any certificate on the client. Find this value in the registry, in log files, or in WMI. Select **Process** to view general information and details on the certificate. This information includes its certification path. Select **Export** to export the certificate as a **.cer** file.


### <a name="bkmk_viewer-registry"></a> Registry tab

Use the **Registry** tab to view registry data included in the data bundle, and to export that data for further analysis.

#### Export
Save a copy of the registry key and subkeys that you select as a registry (.reg) file.

#### Find
Opens the Find dialog, which has the following features:  

- **Find what**: Enter a string to search for in the WMI data set. It supports wildcard characters.  

- **Look at**: Choose whether you want to search within the WMI data set for a matching **Class or instance name**, **Property**, or **Value**.  

- **Match whole string only**: By default, the find dialog searches for strings that contain the string for which you're looking. Choose this checkbox to only find strings that are an exact match to the string that you provided.  

#### Find next
This button opens the next instance of the string that you provided in the Find dialog within the WMI data set.

#### Decode certificate
In the **Decode certificate** dialog box, paste the serialized certificate value for any certificate on the client. Find this value in the registry, in log files, or in WMI. Select **Process** to view general information and details on the certificate. This information includes its certification path. Select **Export** to export the certificate as a **.cer** file.


### <a name="bkmk_viewer-policy"></a> Policy tab

The **Policy** tab is used to view policy data included in the data bundle. 

#### Find
Opens the Find dialog, which has the following features:  

- **Find what**: Enter a string to search for in the WMI data set. It supports wildcard characters.  

- **Look at**: Choose whether you want to search within the WMI data set for a matching **Class or instance name**, **Property**, or **Value**.  

- **Match whole string only**: By default, the find dialog searches for strings that contain the string for which you're looking. Choose this checkbox to only find strings that are an exact match to the string that you provided.  

#### Find next
This button opens the next instance of the string that you provided in the Find dialog within the WMI data set.

#### Decode certificate
In the **Decode certificate** dialog box, paste the serialized certificate value for any certificate on the client. Find this value in the registry, in log files, or in WMI. Select **Process** to view general information and details on the certificate. This information includes its certification path. Select **Export** to export the certificate as a **.cer** file.


### <a name="bkmk_viewer-certs"></a> Certificates tab

The **Certificates** tab is used to view certificates included in the data bundle, and to export them.

#### View certificate
Displays information about a selected certificate.

#### Export
Opens a **Save As** dialog to save a copy of the certificate that you select.


### <a name="bkmk_viewer-troubleshoot"></a> Troubleshooting tab

Use the **Troubleshooting** tab to view log files created using the Support Center Troubleshooting tab.

#### View log
After you select a row on the **Troubleshooting** tab, select this option to view the log file with Log Viewer.
