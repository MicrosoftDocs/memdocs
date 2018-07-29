---
title: DP Job Queue Manager
titleSuffix: Configuration Manager
description: Use the DP Job Queue Manager to troubleshoot and manage content distribution jobs to Configuration Manager distribution points. 
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# DP Job Queue Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The Distribution Point (DP) Job Queue Manager is one of the [Configuration Manager tools](/sccm/core/support/tools). Use it to troubleshoot and manage ongoing content distribution jobs to Configuration Manager distribution points. 

The tool displays the list of jobs that the package transfer manager component has in its queue. It also shows the status of the jobs: ready to be executed, running, or retrying. It lets you manipulate the jobs in the queue, move jobs higher on the list, cancel a job, or manually start running a job.

It also gets information from the site server on which distribution point is running a job. The tool connects through the provider to the site server. It doesn't connect to every remote distribution point to gather this information. Because it triggers actions and gets information through the provider, there's a delay in reflecting changes from remote distribution points.



## Usage

Run **DPJobMgr.exe**. The main menu of the tool contains the following tabs: 

- [Connect](#bkmk_connect): Establish the initial connection to the primary site server  

- [Overview](#bkmk_overview): Summarizes in a single view all the jobs that are running on all distribution points  

- [Distribution Point Info](#bkmk_dp-info): Multi-select distribution points to track them, and manage a single job of interest  

- [Manage Jobs](#bkmk_manage-jobs): Shows in one flat view a list of all the jobs and their statuses. Manipulate jobs, move them up, cancel, or manually start.  


### <a name="bkmk_connect"></a> Connect tab

Use this tab to establish the initial connection to the primary site server. It uses the currently signed-in user's credentials. You can't connect to the central administration site or secondary sites. The connection requires the **Full Administrator** security role.

Once the tool successfully establishes a connection, a notification at the bottom of the tool confirms that it's connected to the site server. 


### <a name="bkmk_overview"></a> Overview tab

Shows a summary of all the jobs on all distribution points. See the following columns:  

- **Distribution Point**: Lists the names of the distribution points  

- **Running Jobs**: Shows the number of concurrent jobs that are running on a particular distribution point.  

    > [!Tip]  
    > The number of concurrent software distributions is a site setting. Modified this setting in the Software Distribution Component Properties.  

- **Total Jobs**: Shows the number of all the jobs targeted to a particular distribution point. This number includes the jobs that are running, retrying, or waiting to be executed.  

- **Total Retries**: Shows the number of times jobs have been retrying in a particular distribution point. A higher number may represent a general problem with that particular distribution point.  


> [!Tip]  
> - To sort each column in this tab, click on the column name  
> 
> - Manually refresh the information in this tab by clicking **Refresh**  
> 
> - Automatically refresh the information in this tab by clicking **Start Auto Refresh** and setting the auto refresh interval. The default refresh interval is two minutes.  


### <a name="bkmk_dp-info"></a> Distribution Point Info tab

Shows the list of all the distribution points under the connected site. The pane on the left lists all the distribution points. Click **Select All** or **Unselect All** as necessary, or multi-select specific distribution points in this list. The pane on the right shows the jobs for the selected distribution points.

There are eight columns:  

- **Status Icon**: There are three possible status icons:  

    - **Ready**: Indicates that a particular job has finished all the verification steps. It's ready to be added to the running concurrent jobs. Jobs in this state are usually in a waiting stage. They wait for the current running processes to finish to open up a space for them.  

    - **Running**: Indicates that a particular job is currently running on a distribution point. For long running jobs (large packages), usually there's time to get the progress (%) towards completion. It shows this percentage in the **Progress** column in this view. For small packages, the **Progress** column may stay empty. The job may already be completed by the time it receives status from the remote distribution point.  

    - **Retry**: Indicates that a particular job has failed and is now in a retry state. This job is retried after the retry interval. This interval is configurable, and set to 30 minutes by default.  

- **Software**: Name of the package that's targeted to a particular distribution point  

- **Package ID**: Package ID of the package that's targeted to a particular distribution point  

- **Size**: Size of the package in KB  

- **Progress**: Job completion percentage. For more information, see the **Running** status icon description.  

- **Start/Restart Time**: For a running job, this value is the start time (green). For a retry job, this value is the time that it will retry the job.  

- **Retries**: Number of times it has retried this package.  

- **Distribution Point Name**: The fully qualified domain name (FQDN) of the distribution point  

> [!Tip]  
> - To sort each column in this tab, click on the column name  
> 
> - Manually refresh the information in this tab by clicking **Refresh**  
> 
> - Automatically refresh the information in this tab by clicking **Start Auto Refresh** and setting the auto refresh interval. The default refresh interval is two minutes.  
> 
> - If you need to modify a particular job, right-click the job in this view, and select **Manage Job**. This action opens the [Manage Jobs tab](#bkmk_manage-jobs).  


### <a name="bkmk_manage-jobs"></a> Manage Jobs tab

Shows in one flat view a list of all the jobs and their statuses. It contains the same eight columns as the [Distribution Point Info tab](#bkmk_dp-info). In this view, right-click the jobs for the following actions:  

- **Run**: Starts a job that's in any state other than running  

- **Move To Top**: Moves one or more jobs to the top of the queue. This action may result in the jobs running immediately. A lower priority job may pause because of this action.  

- **Move Up**: Moves a particular job one row above. A lower priority job may pause running because of this action.  

- **Move Down**: Moves a particular job one row below.  

- **Move To Bottom**: Moves one or more jobs to the bottom of the queue.  

    > [!Tip]  
    > Drag-and-drop jobs in the list to move them.  

- **Cancel**: Tries to cancel one or more jobs.  

    > [!Note]  
    > You can't cancel jobs near their final completion time. If the site server is also a distribution point, you can't cancel jobs on the site server.  



## See also

- [Fundamental concepts for content management](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [Package transfer manager](/sccm/core/plan-design/hierarchy/package-transfer-manager)
