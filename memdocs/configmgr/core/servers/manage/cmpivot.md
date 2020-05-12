---
title: CMPivot for real-time data
titleSuffix: Configuration Manager
description: Learn how to use CMPivot in Configuration Manager to query clients in real time.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart 
manager: dougeby
---

# CMPivot for real-time data in Configuration Manager

<!--1358456-->

*Applies to: Configuration Manager (current branch)*

Configuration Manager has always provided a large centralized store of device data, which customers use for reporting purposes. The site typically collects this data on a weekly basis. Starting in version 1806, CMPivot is a new in-console utility that now provides access to real-time state of devices in your environment. It immediately runs a query on all currently connected devices in the target collection and returns the results. Then filter and group this data in the tool. By providing real-time data from online clients, you can more quickly answer business questions, troubleshoot issues, and respond to security incidents.

For example, in [mitigating speculative execution side channel vulnerabilities](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974), one of the requirements is to update the system BIOS. You can use CMPivot to quickly query on system BIOS information, and find clients that aren't in compliance.

 > [!IMPORTANT]  
 > - Some security software may block scripts running from c:\windows\ccm\scriptstore. This can prevent successful execution of CMPivot queries. Some security software may also generate audit events or alerts when running CMPivot PowerShell.
 > - Certain anti-malware software may inadvertently trigger events against the Configuration Manager Run Scripts or CMPivot features. It is recommended to exclude %windir%\CCM\ScriptStore so that the anti-malware software permits those features to run without interference.


## Prerequisites

The following components are required to use CMPivot:

- Upgrade the target devices to the latest version of the Configuration Manager client.  

- Target clients require a minimum of PowerShell version 4.

- To gather data for the following entities, target clients require PowerShell version 5.0:  
  - Administrators
  - Connection
  - IPConfig
  - SMBConfig


- Permissions for CMPivot:
  - **Read** permission on the **SMS Scripts** object
  - **Run Scripts** permission on the **Collection**
    - Alternatively, starting in version 1906, you can use **Run CMPivot** on **Collection**.
  - **Read** permission on **Inventory Reports**
  - The default scope.

>[!NOTE]
> **Run Scripts** is a super set of the **Run CMPivot** permission.
 
## Limitations

- In a hierarchy, connect the Configuration Manager console to a *primary site* to run CMPivot. The **Start CMPivot** action doesn't appear in the console when it's connected to a central administration site (CAS).
  - Starting in Configuration Manager version 1902, you can run CMPivot from a CAS. In some environments, additional permissions are needed. For more information, see [CMPivot starting in version 1902](#bkmk_cmpivot1902).

- CMPivot only returns data for clients connected to the current site.  

- If a collection contains devices from another site, CMPivot results are only from devices in the current site.  

- You can't customize entity properties, columns for results, or actions on devices.  

- Only one instance of CMPivot can run at the same time on a computer that is running the Configuration Manager console.  

- In version 1806, the query for the **Administrators** entity only works if the group is named "Administrators". It doesn't work if the group name is localized. For example, "Administrateurs" in French.<!--SCCMDocs issue 759-->  


## Start CMPivot

1. In the Configuration Manager console, connect to the primary site. Go to the **Assets and Compliance** workspace, and select the **Device Collections** node. Select a target collection, and click **Start CMPivot** in the ribbon to launch the tool.  

    > [!Tip]  
    > If you don't see this option, check the following configurations:  
    > 
    > - Confirm with a site administrator that your account has the required permissions. For more information, see [Prerequisites](#prerequisites).  
    > 
    > - Connect the console to a *primary site*.  

2. The interface provides further information about using the tool.  

     - Manually enter query strings at the top, or click the links in the in-line documentation.  

     - Click one of the **Entities** to add it to the query string.  

     - The links for **Table Operators**, **Aggregation Functions**, and **Scalar Functions** open language reference documentation in the web browser. CMPivot uses the [Kusto Query Language (KQL)](https://docs.microsoft.com/azure/kusto/query/).  

3. Keep the CMPivot window open to view results from clients. When you close the CMPivot window, the session is complete.  

    > [!Note]  
    > If the query has been sent, then clients still send a state message response to the server.  



## How to use CMPivot

![CMPivot window sample](media/1358456-cmpivot-sample.png)

The CMPivot window contains the following elements:  

1. The collection that CMPivot currently targets is in the title bar at the top, and the status bar at the bottom of the window. For example, "PM_Team_Machines" in the above screenshot.  

2. The pane on the left lists the **Entities** that are available on clients. Some entities rely upon WMI while others use PowerShell to get data from clients.   

    - Right-click an entity for the following actions:  

       - **Insert**: Add the entity to the query at the current cursor position. The query doesn't automatically run. This action is the default when you double-click an entity. Use this action when building a query.  

       - **Query all**: Run a query for this entity including all properties. Use this action to quickly query for a single entity.  

       - **Query by device**: Run a query for this entity and group the results. For example, `Disk | summarize dcount( Device ) by Name`  

    - Expand an entity to see specific properties available for each entity. Double-click a property to add it to the query at the current cursor position.  

3. The **Home** tab shows general information about CMPivot, including links to sample queries and supporting documentation.  

4. The **Query** tab displays the query pane, results pane, and status bar. The query tab is selected in the above screenshot example.  

5. The query pane is where you build or type a query to run on clients in the collection.  

    - CMPivot uses a subset of the [Kusto Query Language (KQL)](https://docs.microsoft.com/azure/kusto/query/).  

    - Cut, copy, or paste content in the query pane.  
    <!-- markdownlint-disable MD038 -->
    - By default, this pane uses IntelliSense. For example, if you start typing `D`, IntelliSense suggests all of the entities that start with that letter. Select an option and press Tab to insert it. Type a pipe character and a space `| `, and then IntelliSense suggests all of the table operators. Insert `summarize` and type a space, and IntelliSense suggests all of the aggregation functions. For more information on these operators and functions, click the **Home** tab in CMPivot.  

    - The query pane also provides the following options:  

        - Run the query.  

        - Move backwards and forwards in the history list of queries.  

        - Create a direct membership collection.  

        - Export the query results to CSV or the clipboard.  

6. The results pane displays the data returned by active clients for the query.  

   - The available columns vary based upon the entity and the query.  

   - Click a column name to sort the results by that property.  

   - Right-click on any column name to group the results by the same information in that column, or sort the results.  

   - Right-click on a device name to take the following additional actions on the device:  

      - **Pivot to**: Query for another entity on this device.  

      - **Run Script**: Launch the Run Script wizard to run an existing PowerShell script on this device. For more information, see [Run a script](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script).  

      - **Remote Control**: Launch a Configuration Manager Remote Control session on this device. For more information, see [How to remotely administer a Windows client computer](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

      - **Resource Explorer**: Launch Configuration Manager Resource Explorer for this device. For more information, see [View hardware inventory](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) or [View software inventory](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

   - Right-click on any non-device cell to take the following additional actions:  

     - **Copy**: Copy the text of the cell to the clipboard.  

     - **Show devices with**: Query for devices with this value for this property. For example, from the results of the `OS` query, select this option on a cell in the Version row: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Show devices without**: Query for devices without this value for this property. For example, from the results of the `OS` query, select this option on a cell in the Version row: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Bing it**: Launch the default web browser to https://www.bing.com with this value as the query string.  

   - Click any hyperlinked text to pivot the view on that specific information.  

   - The results pane doesn't show more than 20,000 rows. Either adjust the query to further filter the data, or restart CMPivot on a smaller collection.  

7. The status bar shows the following information (from left to right):  

   - The status of the current query to the target collection. This status includes:  
     - The number of active clients that completed the query (3)  
     - The number of total clients (5)  
     - The number of offline clients (2)  
     - Any clients that returned failure (0)  

       For example: `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - The ID of the client operation. For example: `id(16780221)`  

   - The current collection. For example: `PM_Team_Machines`  

   - The total number of rows in the results pane. For example, `1 objects`  



## Example scenarios

The following sections provide examples of how you might use CMPivot in your environment:


### Example 1: Stop a running service

Your security administrator asks you to stop and disable the Computer Browser service as quickly as possible on all devices in the accounting department. You start CMPivot on a collection for all devices in accounting, and select **Query all** on the **Service** entity. 

`Service`

As results appear, you right-click on the **Name** column and select **Group by**. 

`Service | summarize dcount( Device ) by Name`

In the row for the **Browser** service, you click the hyperlinked number in the **dcount_** column. 

`Service | where (Name == 'Browser') | summarize count() by Device`

You multi-select all devices, right-click the selection, and choose **Run Script**. This action launches the Run Script wizard, from which you run an existing script you have for stopping and disabling a service. With CMPivot you quickly respond to the security incident for all active computers, viewing results in the Run Script wizard. You then followup to create a configuration baseline to remediate other computers in the collection as they become active in the future. 

![CMPivot example for Browser service and Run Script action](media/cmpivot-example1.png)


### Example 2: Proactively resolve application failures  

To be proactive with operational maintenance, once a week you run CMPivot against a collection of servers that you manage, and select **Query all** on the **AppCrash** entity. You right-click the **FileName** column and select **Sort Ascending**. One device returns seven results for sqlsqm.exe with a timestamp about 03:00 every day. You select the file name in one of the rows, right-click it, and select **Bing It**. Browsing the search results in the web browser, you find a Microsoft support article for this issue with more information and resolution. 


### Example 3: BIOS version

To [mitigate speculative execution side channel vulnerabilities](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974), one of the requirements is to update the system BIOS. You start with a query for the **BIOS** entity. You then **Group by** the **Version** property. Then right-click a specific value, such as "LENOVO - 1140", and select **Show devices with**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### Example 4: Free disk space

You need to temporarily store a large file on a network file server, but aren't sure which one has enough capacity. Start CMPivot against a collection of file servers, and query the **Disk** entity. Modify the query for CMPivot to quickly return a list of active servers with real-time storage data:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="bkmk_cmpivot"></a> CMPivot starting in version 1810
<!--1359068, 3607759-->

CMPivot includes the following improvements starting in Configuration Manager version 1810:

- [CMPivot utility and performance](#bkmk_cmpivot-perf)
- [Scalar functions](#bkmk_cmpivot-functions)  
- [Rendering visualizations](#bkmk_cmpivot-charts)  
- [Hardware inventory](#bkmk_cmpivot-hinv)  
- [Scalar operators](#bkmk_cmpivot-operators)  
- [Query summary](#bkmk_cmpivot-summary)  
- [Audit status messages](#cmpivot-audit-status-messages)

### <a name="bkmk_cmpivot-perf"></a> CMPivot utility and performance

- CMPivot will return up to 100,000 cells rather than 20,000 rows.
  - If the entity has 5 properties, meaning 5 columns, up to 20,000 rows will be shown.
  - For an entity with 10 properties, up to 10,000 rows will be shown.
  - The total data shown will be less than or equal to 100,000 cells.
- On the Query Summary tab, select the count of Failed or Offline devices, and then select the option to **Create Collection**. This option makes it easy to target those devices with a remediation deployment.
- Save **Favorite** queries by clicking the folder icon.
   ![Example of saving a favorite query in CMPivot](media/cmpivot-favorite.png)

- Clients updated to the 1810 version return output less than 80 KB to the site over a fast communication channel.
  - This change increases the performance of viewing script or query output.
  - If the script or query output is greater than 80 KB, the client sends the data via a state message.
  - If the client isn't updated to the 1810 client version, it continues to use state messages.

- You may see the following error when you start CMPivot:
   **You can't use CMPivot right now due to an incompatible script version. This issue may be because the hierarchy is in the process of upgrading a site. Wait until the upgrade is complete and then try again.**

  - If you see this message, it could mean:
    - The security scope isn't set up properly.
    - There are issues with Upgrade in the process.
    - The underlying CMPivot script is incompatible.


### <a name="bkmk_cmpivot-functions"></a> Scalar functions
CMPivot supports the following scalar functions:
- **ago()**: Subtracts the given timespan from the current UTC clock time  
- **datetime_diff()**: Calculates the calendar difference between two datetime values  
- **now()**: Returns the current UTC clock time  
- **bin()**: Rounds values down to an integer multiple of a given bin size  

> [!Note]  
> The datetime data type represents an instant in time, typically expressed as a date and time of day. Time values are measured in 1-second units. A datetime value is always in the UTC time zone. Always express date time literals in ISO 8601 format, for example, `yyyy-mm-dd HH:MM:ss`  

#### Examples
- `datetime(2015-12-31 23:59:59.9)`: A specific date time literal   
- `now()`: The current time  
- `ago(1d)`: The current time minus one day  


### <a name="bkmk_cmpivot-charts"></a> Rendering visualizations

CMPivot now includes basic support for the KQL [render operator](https://docs.microsoft.com/azure/kusto/query/renderoperator). This support includes the following types:  
- **barchart**: First column is x-axis, and can be text, datetime or numeric. The second columns must be numeric and is displayed as a horizontal strip.  
- **columnchart**: Like barchart, with vertical strips instead of horizontal strips.  
- **piechart**: First column is color-axis, second column is numeric.  
- **timechart**: Line graph. First column is x-axis, and should be datetime. Second column is y-axis.  

#### Example: bar chart
The following query renders the most recently used applications as a bar chart:

``` Kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

![Example of CMPivot bar chart visualization](media/1359068-cmpivot-barchart.png)

#### Example: time chart
To render time charts, use the new **bin()** operator to group events in time. The following query shows when devices have started in the last seven days:

``` Kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

![Example of CMPivot time chart visualization](media/1359068-cmpivot-timechart.png)

#### Example: pie chart
The following query displays all OS versions in a pie chart:

``` Kusto
OperatingSystem
| summarize count() by Caption
| render piechart
```

![Example of CMPivot pie chart visualization](media/1359068-cmpivot-piechart.png)


### <a name="bkmk_cmpivot-hinv"></a> Hardware inventory
Use CMPivot to query any hardware inventory class. These classes include any custom extensions you make to hardware inventory. CMPivot immediately returns cached results from the last hardware inventory scan stored in the site database. At the same time, it updates the results if necessary with live data from any online clients.

The color saturation of the data in the results table or chart indicates if the data is live or cached. For example, dark blue is real-time data from an online client. Light blue is cached data.

#### Example

``` Kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

![Example of CMPivot inventory query with column chart visualization](media/1359068-cmpivot-inventory.png)

#### Limitations
- The following hardware inventory entities aren't supported:  
    - Array properties, for example IP address  
    - Real32/Real64 <!--example?-->  
    - Embedded object properties <!--example?-->  
- Inventory entity names must begin with a character
- You can't overwrite the built-in entities by creating an inventory entity of the same name  


### <a name="bkmk_cmpivot-operators"></a> Scalar operators
CMPivot includes the following scalar operators:  

> [!Note]  
> - LHS: string to the left of the operator  
> - RHS: string to the right of the operator  


|Operator|Description|Example (yields true)|
|--------|-----------|---------------------|
|==|Equals|`"aBc" == "aBc"`|
|!=|Not equals|`"abc" != "ABC"`|
|like|LHS contains a match for RHS|`"FabriKam" like "%Brik%"`|
|!like|LHS doesn't contain a match for RHS|`"Fabrikam" !like "%xyz%"`|
|contains|RHS occurs as a subsequence of LHS|`"FabriKam" contains "BRik"`|
|!contains|RHS doesn't occur in LHS|`"Fabrikam" !contains "xyz"`|
|startswith|RHS is an initial subsequence of LHS|`"Fabrikam" startswith "fab"`|
|!startswith|RHS isn't an initial subsequence of LHS|`"Fabrikam" !startswith "kam"`|
|endswith|RHS is a closing subsequence of LHS|`"Fabrikam" endswith "Kam"`|
|!endswith|RHS isn't a closing subsequence of LHS|`"Fabrikam" !endswith "brik"`|


### <a name="bkmk_cmpivot-summary"></a> Query summary

Select the **Query Summary** tab at the bottom of the CMPivot window. This status helps you identify clients that are offline, or troubleshoot errors that may occur. Select a value in the Count column to open a list of specific devices with that status. 

For example, select the count of devices with a Failure status. See the specific error message, and export a list of these devices. If the error is that a specific cmdlet isn't recognized, create a collection from the exported device list to deploy a Windows PowerShell update.  

### CMPivot audit status messages

Starting in version 1810, when you run CMPivot, an audit status message is created with **MessageID 40805**. You can view the status messages by going to **Monitoring** > **System Status** > **Status Message Queries**. You can run **All Audit status Messages for a Specific User**, **All Audit status Messages for a Specific Site**, or create your own status message query.

The following format is used for the message:

MessageId 40805: User &lt;UserName> ran script &lt;Script-Guid> with hash &lt;Script-Hash> on collection &lt;Collection-ID>.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 is the Script-Guid for CMPivot.
- The Script-Hash can be seen in the client's scripts.log file.
- You can also see the hash stored in the client's script store. The filename on the client is &lt;Script-Guid>_&lt;Script-Hash>.
    - Example file name: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![CMPivot audit status message sample](media/cmpivot-audit-status-message.png)

## <a name="bkmk_cmpivot1902"></a> CMPivot starting in version 1902
<!--3610960-->
Starting in Configuration Manager version 1902, you can run CMPivot from the central administration site (CAS) in a hierarchy. The primary site still handles the communication to the client. When running CMPivot from the central administration site, it communicates with the primary site over the high-speed message subscription channel. This communication doesn't rely upon standard SQL replication between sites.

Running CMPivot on the CAS will require additional permissions when SQL or the provider aren't on the same machine or in the case of SQL Always On configuration. With these remote configurations, you have a "double hop scenario" for CMPivot.

To get CMPivot to work on the CAS in such a "double hop scenario", you can define constrained delegation. To understand the security implications of this configuration, read the [Kerberos constrained delegation](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) article. Kerberos needs to work through all of the hops between the machines.<!--5746133--> If you have more than one remote configuration such as SQL or SMS Provider being colocated with the CAS or not, or multiple trusted forests, you may require a combination of permission settings. Below are the steps that you may need to take:

### CAS has a remote SQL server

1. Go to each primary site's SQL server.
   1. Add the CAS remote SQL server and the CAS site server to the [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) group.
   ![Configmgr_DviewAccess group on a primary site's SQL server](media/cmpivot-dviewaccess-group.png)
1. Go to Active Directory Users and Computers.
   1. For each primary site server, right click and select **Properties**.
      1. In the delegation tab, choose the third option, **Trust this computer for delegation to specified services only**. 
      1. Choose **Use Kerberos only**.
      1. Add the CAS's SQL server service with port and instance.
      1. Make sure these changes align with your company security policy!
   1. For the CAS site, right click and select **Properties**.
      1. In the delegation tab, choose the third option, **Trust this computer for delegation to specified services only**. 
      1. Choose **Use Kerberos only**.
      1. Add each primary site's SQL server service with port and instance.
      1. Make sure these changes align with your company security policy!

   ![CMPivot AD delegation example for double hops](media/cmpivot-ad-delegation.png)

### CAS has a remote provider

1. Go to each primary site's SQL server.
   1. Add the CAS provider machine account and the CAS site server to the [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) group.
1. Go to Active Directory Users and Computers.
   1. Select the CAS provider machine, right click and select **Properties**.
      1. In the delegation tab, choose the third option, **Trust this computer for delegation to specified services only**. 
      1. Choose **Use Kerberos only**.
      1. Add each primary site's SQL server service with port and instance.
      1. Make sure these changes align with your company security policy!
   1. Select the CAS site server, right click and select **Properties**.
      1. In the delegation tab, choose the third option, **Trust this computer for delegation to specified services only**. 
      1. Choose **Use Kerberos only**.
      1. Add each primary site's SQL server service with port and instance.
      1. Make sure these changes align with your company security policy!
1. Restart the CAS remote provider machine.

### SQL Always On

1. Go to each primary site's SQL server.
   1. Add the CAS site server to the [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) group.
1. Go to Active Directory Users and Computers.
   1. For each primary site server, right click and select **Properties**.
      1. In the delegation tab, choose the third option, **Trust this computer for delegation to specified services only**. 
      1. Choose **Use Kerberos only**.
      1. Add the CAS's SQL server service accounts for the SQL nodes with port and instance.
      1. Make sure these changes align with your company security policy!
   1. Select the CAS site server, right click and select **Properties**.
      1. In the delegation tab, choose the third option, **Trust this computer for delegation to specified services only**. 
      1. Choose **Use Kerberos only**.
      1. Add each primary site's SQL server service with port and instance.
      1. Make sure these changes align with your company security policy!
1. Make sure the [SPN is published](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs) for the CAS SQL listener name and each primary SQL listener name.
1. Restart the primary SQL servers.
1. Restart the CAS site server and the CAS SQL servers.

## <a name="bkmk_cmpivot1906"></a> CMPivot starting in version 1906

Starting in version 1906, the following items were added to CMPivot:

- [Joins, additional operators, and aggregators](#bkmk_cmpivot_joins)
- [Added CMPivot permissions to the Security Administrator role](#bkmk_cmpivot_secadmin1906)
- [CMPivot standalone](#bkmk_standalone)

### <a name="bkmk_cmpivot_joins"></a> Add joins, additional operators, and aggregators in CMPivot
<!--4054074-->
You now have additional arithmetic operators, aggregators, and the ability to add query joins such as using Registry and File together. The following items have been added:

#### Table operators

|Table operators| Description|
|-----|-----|
| [join](https://docs.microsoft.com/azure/kusto/query/joinoperator)| Merge the rows of two tables to form a new table by matching row for the same device|
|render|Renders results as graphical output|

The render operator already exists in CMPivot. Support for multiple series and the **with** statement were added. For more information, see the [examples](#bkmk_cmpivot_examples1906) section and Kusto's [join operator](https://docs.microsoft.com/azure/kusto/query/joinoperator) article.

#### Limitations for joins

1. The join column is always implicitly done on the **Device** field.
1. You can use a maximum of 5 joins per query.
1. You can use a maximum of 64 combined columns.

#### Scalar operators

|Operator| Description|Example|
|-----|-----|-----|
| + | Add| `2 + 1, now() + 1d`|
| - |  Subtract| `2 - 1, now() - 1d`|
| * | Multiply| `2 * 2`|
| / | Divide | `2 / 1`|
| % | Modulo | `2 % 1`

#### Aggregation functions

|Function| Description|
|-----|-----|
| percentile()| Returns an estimate for the specified nearest-rank percentile of the population defined by Expr|
| sumif() | Returns a sum of Expr for which Predicate evaluates to true|

#### Scalar functions

|Function| Description|
|-----|-----|
| case()| Evaluates a list of predicates and returns the first result expression whose predicate is satisfied |
| iff() | Evaluates the first argument and returns the value of either the second or third arguments depending on whether the predicate evaluated to true (second) or false (third)|
 | indexof() | Function reports the zero-based index of the first occurrence of a specified string within input string|
| strcat() | Concatenates between 1 and 64 arguments |
| strlen()| Returns the length, in characters, of the input string|
| substring() | Extracts a substring from a source string starting from some index to the end of the string |
| tostring() | Converts input to a string operation |

#### <a name="bkmk_cmpivot_examples1906"></a> Examples

- Show device, manufacturer, model, and OSVersion:

   ``` Kusto
   ComputerSystem
   | project Device, Manufacturer, Model
   | join (OperatingSystem | project Device, OSVersion=Caption)
   ```

- Show graph of boot times for a device:

   ``` Kusto
   SystemBootData
   | where Device == 'MyDevice'
   | project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
   | order by SystemStartTime desc
   | render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
   ```

   ![Stacked bar chart showing boot times for a device in ms](./media/4054074-render-using-with-statement.png)

### <a name="bkmk_cmpivot_secadmin1906"></a> Added CMPivot permissions to the Security Administrator role
<!--4683130-->

Starting in version 1906, the following permissions have been added to Configuration Manager's built-in **Security Administrator** role:

 - **Read** on SMS Script
 - **Run CMPivot** on Collection
 - **Read** on Inventory Report

>[!NOTE]
> **Run Scripts** is a super set of the **Run CMPivot** permission.
 

### <a name="bkmk_standalone"></a> CMPivot standalone
<!--3555890, 4619340, 4683130 -->

Starting in version 1906, you can use CMPivot as a standalone app. CMPivot standalone is only available in English. Run CMPivot outside of the Configuration Manager console to view the real-time state of devices in your environment. This change enables you to use CMPivot on a device without first installing the console.

> [!Tip]  
> This feature was first introduced in version 1906 as a [pre-release feature](pre-release-features.md). Beginning with version 2002, it's no longer a pre-release feature.  

You can share the power of CMPivot with other personas, such as helpdesk or security admins, who don't have the console installed on their computer. These other personas can use CMPivot to query Configuration Manager alongside the other tools that they traditionally use. By sharing this rich management data, you can work together to proactively solve business problems that cross roles.

#### Install CMPivot standalone

1. Set up the permissions needed to run CMPivot. For more information, see [prerequisites](#prerequisites). You can also use the [Security Administrator role](#bkmk_cmpivot_secadmin1906) if the permissions are appropriate for the user.
2. Find the CMPivot app installer in the following path: `<site install path>\tools\CMPivot\CMPivot.msi`. You can run it from that path, or copy it to another location.
3. When you run the CMPivot standalone app, you'll be asked to connect to a site. Specify the fully qualified domain name or computer name of either the Central Administration or primary site server.
   - Each time you open CMPivot standalone you'll be prompted to connect to a site server.
4. Browse to the collection on which you want to run CMPivot, then run your query.

   ![Browse to the collection you want to run your query against](./media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> Right-click actions, such as **Run Scripts**, **Resource Explorer**, and web search aren't available in CMPivot standalone. CMPivot standalone's primary use is querying independently from the Configuration Manager infrastructure. To help security administrators, CMpivot standalone does include the ability to connect to Microsoft Defender Security Center. <!--5605358-->

## <a name="bkmk_cmpivot1910"></a> CMPivot starting in version 1910
<!--5410930, 3197353-->
Starting in version 1910, CMPivot was significantly optimized to reduce network traffic and load on your servers. Additionally, a number of entities and entity enhancements were added to aid in troubleshooting and hunting. The following changes were introduced for CMPivot in version 1910:

- [Optimizations to the CMPivot engine](#bkmk_optimization)
- Additional entities and entity enhancements:
  - Windows event logs ([WinEvent](#bkmk_WinEvent))
  - File content ([FileContent](#bkmk_File))
  - Dlls loaded by processes ([ProcessModule](#bkmk_ProcessModule))
  - Azure Active Directory information ([AADStatus](#bkmk_AadStatus))
  - Endpoint protection status ([EPStatus](#bkmk_EPStatus))
- [Local device query evaluation using CMPivot standalone](#bkmk_local-eval)
- [Other enhancements to CMPivot](#bkmk_Other)


### <a name="bkmk_optimization"></a> Optimizations to the CMPivot engine
<!--3197353-->
To reduce network traffic and load on your servers, CMPivot was optimized in 1910. Many query operations are now performed directly on the client rather than on the servers. This change also means that some CMPivot operations return minimal data from the first query. If you decide to drill into the data for more information, a new query might run to fetch the additional data from the client. For instance, previously a large data set was returned to the server when you ran a "summarized count" query.  While returning a large data set offered immediate drill-down, many times only the summarized count was needed. In 1910 when you choose to drill into a specific client, another collection of the data occurs to return the additional data you've requested. This change brings better performance and scalability to queries against a large number of clients. <!--3197353, 5458337-->

#### Examples

The CMPivot optimizations drastically reduce the network and server CPU load needed to run CMPivot queries. With these optimizations, we can now sift through gigabytes of client data in real time. The following queries illustrate these optimizations:

- Search all event logs on all clients in your enterprise for authentication failures.

   ``` Kusto
   EventLog('Security')
   | where  EventID == 4673
   | summarize count() by Device
   | order by count_ desc
   ```

- Search for a file by hash.

   ``` Kusto
   Device
   | join kind=leftouter ( File('%windir%\\system32\\*.exe')
   | where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
   | project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
   ```

### <a name="bkmk_WinEvent"></a> WinEvent(\<logname>,[\<timespan>])

This entity is used to get events from event logs and event tracing log files. The entity gets data from event logs that are generated by the Windows Event Log technology. The entity also gets events in log files generated by Event Tracing for Windows (ETW). WinEvent looks at events that have occurred within the last 24 hours by default. However, the 24-hour default can be overridden by including a timespan.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="bkmk_File"></a> FileContent(\<filename>)

FileContent is used to get the contents of a text file.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="bkmk_ProcessModule"></a> ProcessModule(\<processname>)  

This entity is used to enumerate the modules (dlls) loaded by a given process. ProcessModule is useful when hunting for malware that hides in legitimate processes.  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="bkmk_AadStatus"></a> AadStatus

This entity can be used to get the current Azure Active Directory identity information from a device.

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="bkmk_EPStatus"></a> EPStatus

EPStatus is used to get the status of antimalware software installed on the computer.

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="bkmk_local-eval"></a> Local device query evaluation using CMPivot standalone
<!--3197353-->
When using CMPivot outside of the Configuration Manager console, you can query just the local device without the need for the Configuration Manager infrastructure. You can now leverage the CMPivot Azure Log Analytics queries to quickly view WMI information on the local device. This also enables validation and refinement of CMPivot queries, before running them in a larger environment. CMPivot standalone is only available in English. For more information about installing CMPivot standalone, see [Install CMPivot standalone](#install-cmpivot-standalone).

#### Known issues for local device query evaluation

 - If you query on **This PC** for a WMI entity that you don't have access to, such as a locked down WMI class, you may see a crash in CMPivot. Run CMPivot using an account with elevated privileges to query those entities. <!--5753242-->
- If you query non-WMI entities on **This PC**, you'll see an **Invalid namespace** or an ambiguous exception.
- Run CMPivot standalone from the start menu shortcut, not directly from the path of the executable file. <!--5787962-->

### <a name="bkmk_Other"></a> Other enhancements

- You can do regular expression type queries using the new `like` operator. For example:<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- We've updated the **CcmLog()** and **EventLog()** entities to only look at messages in the last 24 hours by default. This behavior can be overridden by passing in an optional timespan. For example, the following query will look at events in the last 1 hour:

   ```kusto
   CcmLog('Scripts',1h)
   ```

- The **File()** entity has been updated to collect information about Hidden and System files, and include the MD5 hash. While an MD5 hash isn't as accurate as the SHA256 hash, it tends to be the commonly reported hash in most malware bulletins.  

- You can add comments in queries.<!-- 5431463 --> This behavior is useful when sharing queries. For example:

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- CMPivot automatically connects to the last site.<!-- 5420395 --> After you start CMPivot, you can connect to a new site if necessary.

- From the **Export** menu, select the new option to **Query link to clipboard**.<!-- 5431577 --> This action copies a link to the clipboard that you can share with others. For example:

    `cmpivot:Ly8gU2FtcGxlIHF1ZXJ5DQpPcGVyYXRpbmdTeXN0ZW0NCnwgc3VtbWFyaXplIGNvdW50KCkgYnkgQ2FwdGlvbg0KfCBvcmRlciBieSBjb3VudF8gYXNjDQp8IHJlbmRlciBiYXJjaGFydA==`

    This link opens CMPivot standalone with the following query:

    ``` Kusto
    // Sample query
    OperatingSystem
    | summarize count() by Caption
    | order by count_ asc
    | render barchart
    ```

    > [!TIP]
    > For this link to work, [install CMPivot standalone](#install-cmpivot-standalone).

- In query results, if the device is enrolled in Microsoft Defender Advanced Threat Protection (ATP), right-click the device to launch the **Microsoft Defender Security Center** online portal.

### Known issues for CMPivot in version 1910

- The maximum results banner may not be displayed when the limit is reached. <!--5431427-->
  - Each client is limited to 128 KB worth of data per query.
  - Results may be truncated if the results of the query exceed 128 KB.
  
## <a name="bkmk_2002"></a> CMPivot starting in version 2002
<!--5870934-->
We've made it easier to navigate CMPivot entities. Starting in Configuration Manager version 2002, you can search CMPivot entities. New icons have also been added to easily differentiate the entities and the entity object types.

![Searching CMPivot entities](./media/5870934-search-cmpivot-entities.png)

 
## Inside CMPivot

CMPivot sends queries to clients using the Configuration Manager "fast channel". This communication channel from server to client is also used by other features such as client notification actions, client status, and Endpoint Protection. Clients return results via the similarly quick state message system. State messages are temporarily stored in the database. For more information about the ports used for client notification, see the [Ports](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP) article.

The queries and the results are all just text. The entities **InstallSoftware** and **Process** return some of the largest result sets. During performance testing, the largest state message file size from one client for these queries was less than **1 KB**. Scaled to a large environment with 50,000 active clients, this one-time query would generate less than 50 MB of data across the network. All the items on the welcome page that are underlined, will return less than 1k of info per client.

![CMPivot underlined entities example](media/cmpivot-underlined-entities.png)

Starting in Configuration Manager 1810, CMPivot can query hardware inventory data, including extended hardware inventory classes. These new entities (entities not underlined on the welcome page) may return much larger data sets, depending on how much data is defined for a given hardware inventory property. For example, the "InstalledExecutable" entity might return multiple MB of data per client, depending on the specific data you query on. Be mindful of the performance and scalability on your systems when returning larger hardware inventory data sets from larger collections using CMPivot.

A query times out after one hour. For example, a collection has 500 devices, and 450 of the clients are currently online. Those active devices receive the query and return the results almost immediately. If you leave the CMPivot window open, as the other 50 clients come online, they also receive the query, and return results. 

## Log files

 CMPivot interactions are logged to the following log files:

**Server-side:**
- SmsProv.log
- BgbServer.log
- StateSys.log

**Client-side:**
- CcmNotificationAgent.log
- Scripts.log
- StateMessage.log

For more information, see [Log files](../../plan-design/hierarchy/log-files.md) and [Troubleshooting CMPivot](cmpivot-tsg.md).

## Next steps
 
[Troubleshooting CMPivot](cmpivot-tsg.md)

[Create and run PowerShell scripts](../../../apps/deploy-use/create-deploy-scripts.md)


