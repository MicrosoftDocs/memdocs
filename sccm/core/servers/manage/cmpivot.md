---
title: CMPivot for real-time data
titleSuffix: Configuration Manager
description: Learn how to use CMPivot in Configuration Manager to query clients in real-time.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# CMPivot for real-time data in Configuration Manager

<!--1358456-->

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager has always provided a large centralized store of device data, which customers use for reporting purposes. However, that data is only as good as the last time it was collected from clients. Starting in version 1806, CMPivot is a new in-console utility that provides access to real-time state of devices in your environment. It immediately runs a query on all currently connected devices in the target collection and returns the results. Then filter and group this data in the tool. By providing real-time data from online clients, you can more quickly answer business questions, troubleshoot issues, and respond to security incidents.

For example, in [mitigating speculative execution side channel vulnerabilities](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), one of the requirements is to update the system BIOS. You can use CMPivot to quickly query on system BIOS information, and find clients that aren't in compliance.



## Prerequisites

The following components are required to use CMPivot:

- Upgrade the target devices to the latest version of the Configuration Manager client.  

- The Configuration Manager administrator needs permissions to run scripts. For more information, see [Security roles for scripts](/sccm/apps/deploy-use/create-deploy-scripts#bkmk_ScriptRoles).  

- To gather data for the following entities, target clients require PowerShell version 5.0:  
    - Administrators
    - Connection
    - IPConfig
    - SMBConfig 



## Limitations

- In a hierarchy, connect the Configuration Manager console to a primary site to run CMPivot.  

- CMPivot only returns data for clients connected to the current site.  

- If a collection contains devices from another site, CMPivot results are only from devices in the current site.  

- You can't customize entity properties, columns for results, or actions on devices.  

- Only one instance of CMPivot can run at the same time on a computer that is running the Configuration Manager console.  



## Start CMPivot

1. In the Configuration Manager console, connect to the primary site. Go to the **Assets and Compliance** workspace, and select the **Device Collections** node. Select a target collection, and click **Start CMPivot** in the ribbon to launch the tool.  

    > [!Tip]  
    > If you don't see this option, confirm with a site administrator that your account has the required permissions. For more information, see [Prerequisites](#prerequisites).  

2. The interface provides further information about using the tool.  

     - Manually enter query strings at the top, or click the links in the in-line documentation.  

     - Click one of the **Entities** to add it to the query string.  

     - The links for **Table Operators**, **Aggregation Functions**, and **Scalar Functions** open language reference documentation in the web browser. CMPivot uses the same query language as [Azure Log Analytics](https://docs.loganalytics.io/docs/Language-Reference/Change-log).  

3. Keep the CMPivot window open to view results from clients. When you close the CMPivot window, the session is complete.  

    > [!Note]  
    > If the query has been sent, then clients still send a state message response to the server.  



## How to use CMPivot

![CMPivot window sample](media/1358456-cmpivot-sample.png)

The CMPivot window contains the following elements:  

1. The collection that CMPivot currently targets is in the title bar at the top, and the status bar at the bottom of the window. For example, **All Systems** in the above screenshot.  

2. The pane on the left lists the **Entities** that are available on clients. Some entities rely upon WMI while others use PowerShell to get data from clients.   

    - Right-click an entity to insert it into the current query pane, run a query for this entity on all devices, or query for this entity by a specific device.  

    - Expand an entity to see specific properties available for each entity.  

3. The **Home** tab shows general information about CMPivot, including links to sample queries and supporting documentation.  

4. The **Query** tab displays the query pane, results pane, and status bar. The query tab is selected in the above screenshot example.  

5. The query pane is where you build or type a query to run on clients in the collection.  

    - CMPivot uses the same query language as [Azure Log Analytics](https://docs.loganalytics.io/docs/Language-Reference/Change-log).  

    - The query pane also provides the following options:  

        - Run the query  

        - Move backwards and forwards in the history list of queries  

        - Create a direct membership collection  

        - Export the query results to CSV or the clipboard  

6. The results pane displays the data returned by active clients for the query.  

    - The available columns vary based upon the entity and the query.  

    - Click a column name to sort the results by that property.  

    - Right-click on any column name to group the results by the same information in that column.  

    - Right-click on a column name, other than the Device column, to take additional actions.  

    - Right-click on a device row to take additional actions on the device, or pivot the view for that specific device.  

    - Click any hyperlinked text to pivot the view on that specific information.  

7. The status bar shows the following information (from left to right):  

    - The status of the current query on the active clients in the target collection. For example: `Query completed on 1 of 1 clients`  

    - The ID of the.... For example: `id(16778265)`  

    - The current collection. For example: `All Systems`  

    - The total number of objects in the results. For example, `55 objects`  



## Example scenarios

The following sections provide examples of how you might use CMPivot in your environment:

### Example 1: Stop a running service

Your security administrator asks you to stop and disable the Computer Browser service as quickly as possible on all devices in the accounting department. You start CMPivot on a collection for all devices in accounting, and select the **Services** entity. As results appear, you right-click on the Name column and select **Group by Name**. You right-click the row for the Computer Browser service, and select **Run Script**. This action launches the Run Script wizard, from which you run an existing script you have for stopping and disabling a service. With CMPivot you quickly respond to the security incident for all active computers, viewing results in the Run Script wizard. You then followup to create a configuration baseline to remediate other computers in the collection as they become active in the future. 


### Example 2: Investigate app crash  

To be proactive with operational maintenance, once a week you run CMPivot against a collection of servers that you manage, and select the **AppCrash** entity. One device returns seven results for sqlsqm.exe with a timestamp about 03:00 every day. You select the file name in one of the rows, right-click and select **Bing It**. Browsing the search results in the web browser, you find a Microsoft support article for this issue with more information and resolution. 


### Example 3: BIOS version

To [mitigate speculative execution side channel vulnerabilities](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), one of the requirements is to update the system BIOS. You use CMPivot to quickly query on system BIOS information, and find clients that aren't compliant. 

`Bios | simmarize countif( (Version == 'VRTUAL - 5001223') ) by Device | where (countif_ == 0)`


### Example 4: Free disk space

You need to temporarily store a large file on a network file server, but aren't sure which one has enough capacity. You start CMPivot against a collection of file servers, and add several properties from the **Disk** entity. CMPivot quickly returns a list of active servers with real-time storage data:

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`



## Inside CMPivot

CMPivot sends queries to clients using the Configuration Manager "fast channel". This communication channel from server to client is also used by other features such as client notification actions, client status, and Endpoint Protection. Clients return results via the similarly quick state message system. State messages are temporarily stored in the database. 

The queries and the results are all just text. The entities **InstallSoftware** and **Process** return some of the largest result sets. During performance testing, the largest state message file size from one client for these queries was less than **1 KB**. Scaled to a large environment with 50,000 active clients, this one-time query would generate less than 50 MB of data across the network.  

A query times out after one hour. For example, a collection has 500 devices, and 450 of the clients are curently online. Those active devices receive the query and return the results almost immediately. If you leave the CMPivot window open, as the other 50 clients come online, they too receive the query and return results. 



## See also
[Create and run PowerShell scripts](/sccm/apps/deploy-use/create-deploy-scripts)
