---
title: CMPivot for real-time data
titleSuffix: Configuration Manager
description: Learn how to use CMPivot in Configuration Manager to query clients in real time.
ms.date: 08/27/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.author: gokarthi
author: gowdhamankarthikeyan
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
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

- CMPivot and the [Microsoft Edge](../../../apps/deploy-use/deploy-edge.md) installer are currently signed with the **Microsoft Code Signing PCA 2011** certificate. If you set PowerShell execution policy to **AllSigned**, then you need to make sure that devices trust this signing certificate. You can export the certificate from a computer where you've installed the Configuration Manager console. View the certificate on `"C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\CMPivot.exe"`, and then export the code signing certificate from the certification path. Then import it to the _machine_'s **Trusted Publishers** store on managed devices. You can use the process in the following blog, but make sure to export the _code signing certificate_ from the certification path: [Adding a Certificate to Trusted Publishers using Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/adding-a-certificate-to-trusted-publishers-using-intune/ba-p/1974488).<!--CMADO-7585106, MEMDocs#1571-->

## Permissions

The following permissions are needed for CMPivot:

- **Run CMPivot** permission on the **Collection**
- **Read** permission on **Inventory Reports**
- **Read** permission on the **SMS Scripts** object
   - **Read** for **SMS Scripts** isn't required starting in version 2107 <!--7898885-->
   - CMPivot doesn't need **Read** for **SMS Scripts** for it's primary scenario starting in version 2107. However, if the administration service is down and the permission has been removed, then when the administration service falls back, CMPivot will fail. <!--10304720--> The [SMS Provider](../../plan-design/hierarchy/plan-for-the-sms-provider.md) still requires **Read** permission on **SMS Scripts**  if the [administration service](../../../develop/adminservice/overview.md) falls back to it due to a 503 (Service Unavailable) error, as seen in the CMPivot.log. <!--8403036-->
- The **default scope**.
   - The **default scope** isn't required starting in version 2107 <!--7898885-->

### CMPivot permissions by Configuration Manager version

|1902 and earlier| Versions 1906 through 2103| 2107 or later <!--7898885-->|
|---|---|---|
|**Run Script** permission on the **Collection**|**Run CMPivot** permission on the **Collection**|**Run CMPivot** permission on the **Collection**|
|**Read** permission on **Inventory Reports**|**Read** permission on **Inventory Reports**|**Read** permission on **Inventory Reports**|
|**Read** permission on **SMS Scripts**|**Read** permission on **SMS Scripts**|N/A </br></br>  The [SMS Provider](../../plan-design/hierarchy/plan-for-the-sms-provider.md) still requires **Read** permission on **SMS Scripts** if the [administration service](../../../develop/adminservice/overview.md) falls back to it due to a 503 (Service Unavailable) error, as seen in the CMPivot.log.|
|**Default scope** permission|**Default scope** permission|N/A|

## Limitations

- CMPivot only returns data for clients connected to the current site unless it's run from the central administration site (CAS).  
  - If a collection contains devices from another site, CMPivot results are only from devices in the current site unless CMPivot is run from the CAS.
  - In some environments, additional permissions are needed for CMPivot to run on the CAS. For more information, see [CMPivot changes for version 1902](cmpivot-changes.md#bkmk_cmpivot1902).  
- You can't customize entity properties, columns for results, or actions on devices.  
- Only one instance of CMPivot can run at the same time on a computer that is running the Configuration Manager console.  
- In CMPivot standalone, you're not able to access CMPivot queries stored in the Community hub. <!--9442715, 9310040, 9391017-->
- When single sign on with multifactor authentication is used, you may not be able to sign into Community hub from CMPivot when using Configuration Manager 2103 and earlier. <!--10436429-->

## Start CMPivot

1. In the Configuration Manager console, connect to the primary site or the CAS. Go to the **Assets and Compliance** workspace, and select the **Device Collections** node. Select a target collection, and select **Start CMPivot** in the ribbon to launch the tool. If you don't see this option, check the following configurations:  
   - Confirm with a site administrator that your account has the required permissions. For more information, see [Prerequisites](#prerequisites).  

2. The interface provides further information about using the tool.  

     - Manually enter query strings at the top, or select the links in the in-line documentation.  

     - Select one of the **Entities** to add it to the query string.  

     - The links for **Table Operators**, **Aggregation Functions**, and **Scalar Functions** open language reference documentation in the web browser. CMPivot uses the [Kusto Query Language (KQL)](/azure/kusto/query/).  

3. Keep the CMPivot window open to view results from clients. When you close the CMPivot window, the session is complete.
   - If the query has been sent, then clients still send a state message response to the server.  


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

    - CMPivot uses a subset of the [Kusto Query Language (KQL)](/azure/kusto/query/).  

    - Cut, copy, or paste content in the query pane.  
    <!-- markdownlint-disable MD038 -->
    - By default, this pane uses IntelliSense. For example, if you start typing `D`, IntelliSense suggests all of the entities that start with that letter. Select an option and press Tab to insert it. Type a pipe character and a space `| `, and then IntelliSense suggests all of the table operators. Insert `summarize` and type a space, and IntelliSense suggests all of the aggregation functions. For more information on these operators and functions, select the **Home** tab in CMPivot.  

    - The query pane also provides the following options:  

        - Run the query.
           - To rerun your current CMPivot query on the clients, hold **Ctrl** while clicking **Run**. 

        - Move backwards and forwards in the history list of queries.  

        - Create a direct membership collection.  

        - Export the query results to CSV or the clipboard.  

6. The results pane displays the data returned by active clients for the query.  

   - The available columns vary based upon the entity and the query.  

   - The color saturation of the data in the results table or chart indicates if the data is live or from the last hardware inventory scan stored in the site database.  For example, black is real-time data from an online client whereas grey is cached data.

   - Select a column name to sort the results by that property.  

   - Right-click on any column name to group the results by the same information in that column, or sort the results.  

   - Right-click on a device name to take the following additional actions on the device:  

      - **Pivot to**: Query for another entity on this device.
         - Starting in version 2006, **Pivot to** was replaced by **Device Pivot**. For more information, see [CMPivot changes for version 2006](cmpivot-changes.md#bkmk_2006).

      - **Run Script**: Launch the Run Script wizard to run an existing PowerShell script on this device. For more information, see [Run a script](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script).  

      - **Remote Control**: Launch a Configuration Manager Remote Control session on this device. For more information, see [How to remotely administer a Windows client computer](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

      - **Resource Explorer**: Launch Configuration Manager Resource Explorer for this device. For more information, see [View hardware inventory](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) or [View software inventory](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

   - Right-click on any non-device cell to take the following additional actions:  

     - **Copy**: Copy the text of the cell to the clipboard.  

     - **Show devices with**: Query for devices with this value for this property. For example, from the results of the `OS` query, select this option on a cell in the Version row: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Show devices without**: Query for devices without this value for this property. For example, from the results of the `OS` query, select this option on a cell in the Version row: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Bing it**: Launch the default web browser to https://www.bing.com with this value as the query string.  

   - Select any hyperlinked text to pivot the view on that specific information.  

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

> [!TIP]
> Starting in version 2107, use the **Query devices again** button, or **Ctrl** + **F5** to force the client to retrieve the data again for the query. Using **Query devices again** is useful when you expect the data to change on the device since the last query, such as during troubleshooting. Selecting **Run query** again after the initial results are returned only parses the data CMPivot has already retrieved from the client. <!--9966861--> 
>
>:::image type="content" source="media/query-devices-again.png" alt-text="Screenshot of the query devices again button showing the tooltip that Ctrl + F5 is a shortcut to force clients to retrieve the data again.":::

<!--9965423-using include for shared content-->

[!INCLUDE [Publish to Community hub from CMPivot](includes/cmpivot-publish.md)]

## Example scenarios for CMPivot

The following sections provide examples of how you might use CMPivot in your environment:


### Example 1: Stop a running service

Your security administrator asks you to stop and disable the Computer Browser service as quickly as possible on all devices in the accounting department. You start CMPivot on a collection for all devices in accounting, and select **Query all** on the **Service** entity.

`Service`

As results appear, you right-click on the **Name** column and select **Group by**. 

`Service | summarize dcount( Device ) by Name`

In the row for the **Browser** service, you select the hyperlinked number in the **dcount_** column. 

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


## <a name="bkmk_standalone"></a> CMPivot standalone

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)]


 
## Inside CMPivot

CMPivot sends queries to clients using the Configuration Manager "fast channel". This communication channel from server to client is also used by other features such as client notification actions, client status, and Endpoint Protection. Clients return results via the similarly quick state message system. State messages are temporarily stored in the database. For more information about the ports used for client notification, see the [Ports](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP) article.

The queries and the results are all just text. The entities **InstallSoftware** and **Process** return some of the largest result sets. During performance testing, the largest state message file size from one client for these queries was less than **1 KB**. Scaled to a large environment with 50,000 active clients, this one-time query would generate less than 50 MB of data across the network. All the items on the welcome page that are underlined, will return less than 1 KB of info per client.

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

- [Changes to CMPivot](cmpivot-changes.md)
- [Troubleshooting CMPivot](cmpivot-tsg.md)
- [Create and run PowerShell scripts](../../../apps/deploy-use/create-deploy-scripts.md)
