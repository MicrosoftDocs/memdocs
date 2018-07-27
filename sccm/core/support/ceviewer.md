---
title: Collection Evaluation Viewer
titleSuffix: Configuration Manager
description: Use the Collection Evaluation Viewer to view and troubleshoot the collection evaluation process in Configuration Manager.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Collection Evaluation Viewer

*Applies to: System Center Configuration Manager (Current Branch)*

Collection Evaluation Viewer is one of the [Configuration Manager tools](/sccm/core/support/tools). Use it to view and troubleshoot the collection evaluation process on the primary site server.

The tool displays the following information:  

- Both historic and live information for full and incremental collection evaluations  

- The evaluation queue status  

- The time for collection evaluations to complete  

- Which collections are currently being evaluated  

- The estimated time that a collection evaluation will start and complete  



## About collection evaluation

The collection evaluation process runs by evaluating the membership rules of a collection to update its members. The site places a collection that it's evaluating in one of four different queues:  

- **Manual Queue**: For collections that an administrator has manually selected for evaluation from the console  

- **New Queue**: For newly created collections  

- **Full Queue**: For collections due for full evaluation  

- **Incremental Queue**: For collections with incremental evaluation  

There are four threads that run to evaluate the collections in the above queues. Each queue includes a series of arrays, and each array includes the collections to be evaluated. The thread that's running for the queue selects a collection from the array and runs the evaluation. The queue length indicates the number of arrays in the queue.



## Requirements

- Run the tool on the site server  

- Run the tool by an administrative user with at least the **Read-Only Analyst** role  

- The user also requires **Read** permission to the site database in SQL



## Usage

Run **CEViewer.exe**. The main menu of the tool contains the following tabs: 

- [Connect](#bkmk_connect): Establish the initial connection to the primary site server and SQL Server  

- [Full Evaluation](#bkmk_full-eval): Lists the detailed information about all past full evaluations   

- [Incremental evaluation](#bkmk_incremental-eval): Lists the detailed information about all past incremental evaluations  

- [All Queues](#bkmk_all-q): Summarizes the current collection evaluations for all four queues  

- [Manual Queue](#bkmk_manual-q): Lists the detailed information about the current collection evaluation in the manual queue  

- [New Queue](#bkmk_new-q): Lists the detailed information about the current collection evaluation in the new queue  

- [Full Queue](#bkmk_full-q): Lists the detailed information about the current collection evaluation in the full queue  

- [Incremental Queue](#bkmk_incremental-q): Lists the detailed information about the current collection evaluation in the incremental queue  


### <a name="bkmk_connect"></a> Connect tab

This tab allows you to establish the initial connection to the primary site server. The tool also establishes a connection to the SQL server that hosts the site database.

The connections to both primary site server and SQL servers use the current signed-in user credential. Connections to the central administration site or a secondary site aren't supported. No collection evaluation process runs on those sites.

Once the tool successfully establishes a connection, see a notification at the bottom of the Collection Evaluation Viewer that confirms the tool's connection to the SQL server. 


### <a name="bkmk_full-eval"></a> Full Evaluation tab

Shows detailed information about past full collection evaluations. There are eight columns:  

- **Collection Name**: Name of the collection  

- **Site ID**: Site ID of the collection   

- **Run Time**: How long the last collection evaluation ran, in seconds  

- **Last Evaluation Completion Time**: When the last collection evaluation completed  

- **Next Evaluation Time**: When the next full evaluation starts  

- **Member Changes**: The member changes in the last collection evaluation. These changes are either plus (members added) or minus (members removed).  

- **Last Member Change Time**: The most recent time that there was a membership change in the collection evaluation  

- **Percent**: The percentage of evaluation time for this collection over the total (all collections) evaluation time  


### <a name="bkmk_incremental-eval"></a> Incremental evaluation tab

Shows detailed information about past incremental collection evaluations. There are seven columns:  

- **Collection Name**: Name of the collection  

- **Site ID**: Site ID of the collection   

- **Run Time**: How long the last collection evaluation ran, in seconds  

- **Last Evaluation Completion Time**: When the last collection evaluation completed  

- **Member Changes**: The member changes in the last collection evaluation. These changes are either plus (members added) or minus (members removed).  

- **Last Member Change Time**: The most recent time that there was a membership change in the collection evaluation  

- **Percent**: The percentage of evaluation time for this collection over the total (all collections) evaluation time  


### <a name="bkmk_all-q"></a> All Queues tab

Summarizes the live collection evaluations for all four queues. There are six sections:  

- **Summary**: Lists the total collection number and the queue length for all collections in all four queues  

- **Running Evaluation**: Lists which collection is currently being evaluated in each queue, and how long it has been running  

- **Manual Update**: Shows a brief summary of the collections being evaluated, the estimated completion time, and the order of the evaluation in the manual queue  

- **New Collection**: Shows a brief summary of the collections being evaluated, the estimated completion time, and the order of the evaluation in the new collection queue  

- **Full Evaluation**: Shows a brief summary of the collections being evaluated, the estimated completion time, and the order of the evaluation in the full evaluation queue  

- **Incremental Evaluation**: Shows a brief summary of the collections being evaluated, the estimated completion time, and the order of the evaluation in the incremental evaluation queue  


### <a name="bkmk_manual-q"></a> Manual Queue tab

Shows information about the manual collection evaluation currently being evaluated. The order in the list is the order in which the collection will be evaluated. There are four columns:  

- **Collection Name**: Name of the collection  

- **Site ID**: Site ID of the collection   

- **Estimated Completion Time**: When the evaluation is estimated to complete  

- **Estimated Run Time**: How long the evaluation is estimated to run, in day:hour:minute:second format  


### <a name="bkmk_new-q"></a> New Queue tab

Shows the live information about the new collection evaluation being evaluated. The order in the list is the order in which the collection will be evaluated. There are four columns:  

- **Collection Name**: Name of the collection  

- **Site ID**: Site ID of the collection   

- **Estimated Completion Time**: When the evaluation is estimated to complete  

- **Estimated Run Time**: How long the evaluation is estimated to run, in day:hour:minute:second format  


### <a name="bkmk_full-q"></a> Full Queue tab

Shows information about the full collection evaluation currently being evaluated. The order in the list is the order in which the collection will be evaluated. There are four columns:  

- **Collection Name**: Name of the collection  

- **Site ID**: Site ID of the collection   

- **Estimated Completion Time**: When the evaluation is estimated to complete  

- **Estimated Run Time**: How long the evaluation is estimated to run, in day:hour:minute:second format  


### <a name="bkmk_incremental-q"></a> Incremental Queue tab

Shows information about the incremental collection evaluation currently being evaluated. The order in the list is the order in which the collection will be evaluated. There are four columns:  

- **Collection Name**: Name of the collection  

- **Site ID**: Site ID of the collection   

- **Estimated Completion Time**: When the evaluation is estimated to complete  

- **Estimated Run Time**: How long the evaluation is estimated to run, in day:hour:minute:second format  



