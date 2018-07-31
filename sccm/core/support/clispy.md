---
title: Client Spy
titleSuffix: Configuration Manager
description: Use Client Spy to troubleshoot software distribution, inventory, and software metering on Configuration Manager clients.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Client Spy

*Applies to: System Center Configuration Manager (Current Branch)*

Client Spy is one of the [Configuration Manager tools](/sccm/core/support/tools). It's a tool for troubleshooting software distribution, inventory, and software metering on Configuration Manager clients. 

Most of the information retrieved by the tool pertains to software deployments:
- All current software deployments 
- Software distribution history
- The client cache configuration
- Cached items
- Pending required deployments
- Available deployments  

It also displays the following inventory information
- The latest inventory cycle date
- The last report date
- Software inventory major and minor versions
- File collection
- Hardware inventory
- IDMIF collection
- Discovery data records (DDRs) 

Software metering rules are also displayed. 

> [!Note]   
> To improve performance, the tool only collects information for each tab when you select it. Similarly, when you click **Refresh**, it only refreshes the information for the currently displayed tab.



## Usage


### Tools menu

The following actions are available in the **Tools** menu:  

#### Connect
Retrieve information from a different computer.  

- By default, the tool displays information from the current computer. 

- Connect using the remote computer name, user name, and password for the account. The tool makes a connection to the IPC$ share on the remote computer. It deletes the connection when either the tool exits or you connect to another computer.  

- It requires an account with sufficient credentials to obtain the information.  

- If you don't specify a user name and password, Client Spy uses the security context of the currently signed-in user to attempt to make the connection.  

- When you connect to a remote computer, all tabs that are displayed show information from the remote computer.

#### Software Distribution
Displays the [Software Distribution](#software-distribution) tabs and hides the other tabs. By default, Client Spy displays the Software Distribution tabs.

#### Inventory
Displays the Inventory tab and hides the other tabs.

#### Software Metering
Displays the Software Metering tab and hides the other tabs.

#### Save current tab to file
Saves the information in the currently displayed tab to a text file that you specify. 

#### Save all tabs to file
Saves the information in all tabs to a text file that you specify. It only saves information your account can see.



## Software Distribution tab

Configure settings on the following four tabs:
- [Software Distribution Execution Requests](#bkmk_exec-requests)
- [Software Distribution History](#bkmk_history)
- [Software Distribution Cache Information](#bkmk_cache-info)
- [Software Distribution Pending Executions](#bkmk_pending-exec)


### <a name="bkmk_exec-requests"></a> Software Distribution Execution Requests

This tab displays all existing deployments, including both device- and user-targeted deployments.

Each tree item in the Software Distribution Execution Requests tab contains the following four attributes:
- Advertisement ID. This value might be blank, if it's an available deployment. 
- Package ID 
- Program Name 
- User. This might be the targeted user SID or the SID of the user who initiated the request. If both are system requests, the displayed user is System. 

For each run request, it also displays the following information in a subtree structure:
- Program Name 
- Package ID 
- Package Name 
- Request Creation Time 
- State 
- Running State, if State is Running 
- Execution Context (User or Admin) 
- History State (Success, Failure, or NotRun) 
- LastRunTime (Never, if the program hasn't been run before) 
- RetryCount, if State is WaitingRetry 
- ContentAccess (Retry Count, if State is WaitingRetry) 
- FailureCode, if State is WaitingRetry 
- FailureReason, if State is WaitingRetry 

If the request requires content, the state is WaitingContent. The Software Distribution Cache Information tab shows the details for this download request.

If the run request is a download request, it also displays the number of bytes downloaded.

> [!Note]   
> It uses different icons for varying states of a run request.


### <a name="bkmk_history"></a> Software Distribution History

This tab contains information about all previously run programs. This information is stored in the registry.

The main branches of this tree are the different user histories, including System. It displays a subtree containing the list of packages from which programs have been run for each user. 

The package ID and package name for each package subtree displays a list of programs that have run. It displays the following attributes for each: 
- Program name
- Run state
- Last run time
- Failure code
- Failure reason  

The failure code and failure reason are blank when a program was successfully run.


### <a name="bkmk_cache-info"></a> Software Distribution Cache Information

#### Cache Config
Contains information about the Configuration Manager Client cache. This information includes the cache location, the cache size, and whether it's currently in use. 

#### Cached Items
Contains a subtree of all items currently in the cache. Each tree item includes the following information about each item: 
- The item's location (folder) in the cache
- Current state
- Package ID
- Package name
- Package version
- Package size
- Current reference count
- Last referenced time (UTC)  

#### Downloading Items
These are the items that the client is currently downloading. Each of them shows the same information displayed by the cached items, and the number of kilobytes downloaded. 


### <a name="bkmk_pending-exec"></a> Software Distribution Pending Executions

This tab contains information that details past and future required deployments and a list of available deployments.

Each tree branch is for each user account with deployments available, including System.

For each user, a sub tree contains the following three items:  

#### Mandatory Advertisements With Future Executions
These are mandatory advertisements that still have programs remaining to be run. These can be either recurring, one-time, or multiple schedule advertisements. Each displays the advertisement ID, the next run time, and the schedule on which the advertisement runs. 

#### Optional Advertisements
Displays a list of all advertisements that are published. It also displays details such as advertisement ID, program name, and package name for each. 

#### Past Mandatory Advertisements With No Future Scheduled Executions
This is a list of advertisements that exist on the client that have no future programs scheduled to run. The advertisement ID, package name, and program name are displayed. A subtree item is displayed for any advertisements that are optional.

> [!Note]  
> Package name information is only available for packages that have advertised policies associated to them on the computer being viewed. Packages that no longer have available policies associated to them display the message "Package Name No Longer Available".  



## Inventory tab

There's only one tab containing inventory information. The main tree contains the following five items:  

- **Software Inventory**: Contains the date that the last cycle started, the date of the last report, and the minor and major versions of the last report.  

- **File Collection**: Contains the date that the last cycle started, the date of the last report, and the minor and major versions of the last report.  

- **Hardware Inventory**: Contains the date that the last cycle started, the date of the last report, and the minor and major versions of the last report.  

- **IDMIF Collection**: Contains the date that the last cycle started, the date of the last report, and the minor and major versions of the last report.  

- **DDR**: Contains the date that the last cycle started, the date of the last report, and the minor and major versions of the last report. The DDR information is also displayed in a subtree.



## Software Metering tab

This tab displays information as a subtree, and includes all software metering rules. It displays each rule as a node, which it identifies by the file name and rule ID. Expand each node in the tree, and view the following information:
- Explorer file name 
- Original file name
- Rule ID
- File version
- Language


