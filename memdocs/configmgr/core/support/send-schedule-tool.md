---
title: Send Schedule Tool
titleSuffix: Configuration Manager
description: Use the Send Schedule Tool to trigger a schedule on a Configuration Manager client.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Send Schedule Tool

*Applies to: Configuration Manager (current branch)*

The Send Schedule Tool is one of the [Configuration Manager tools](tools.md). Use it to trigger a schedule on a client or trigger the evaluation of a specified configuration baseline. It works for the local computer or targeting a remote client.  

For example, use the tool to trigger an inventory schedule or compliance evaluation. If a number of Configuration Manager clients haven't recently reported inventory or compliance status, run the tool to initiate the necessary schedule on each client.



## Usage

Run **SendSchedule.exe** as an administrator. 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

After you trigger a message (GUID), see **SMSClientMethodProvider.log**. For more information about available message GUIDs, see [Message IDs](#bkmk_sendschedule-guids).

After you trigger the evaluation of a configuration baseline (DCM UID), see **DCMAgent.log**.



## Command-line options


### Option: `/L` 
List all Message GUID or DCM UID available for sending. Display the meaningful name of messages in the data table for each one. If the computer name is absent, it uses the local computer. If you specify a message without a machine name, then it sends the message to the local machine. 



## Examples

#### List the available messages on the local machine 
`SendSchedule /L` 

#### List the available messages on the client MyPC: 
`SendSchedule /L MyPC`

#### Trigger hardware inventory on the local machine
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### Trigger hardware inventory on MyPC: 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### Trigger the evaluation of a specific configuration baseline on MyPC: 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="bkmk_sendschedule-guids"></a> Message IDs

|Message ID  |Display Name  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|Hardware Inventory|
|{00000000-0000-0000-0000-000000000002}|Software Inventory|
|{00000000-0000-0000-0000-000000000003}|Discovery Inventory|
|{00000000-0000-0000-0000-000000000010}|File Collection|
|{00000000-0000-0000-0000-000000000011}|IDMIF Collection|
|{00000000-0000-0000-0000-000000000021}|Request Machine Assignments|
|{00000000-0000-0000-0000-000000000022}|Evaluate Machine Policies|
|{00000000-0000-0000-0000-000000000023}|Refresh Default MP Task|
|{00000000-0000-0000-0000-000000000024}|LS (Location Service) Refresh Locations Task|
|{00000000-0000-0000-0000-000000000025}|LS Timeout Refresh Task|
|{00000000-0000-0000-0000-000000000026}|Policy Agent Request Assignment (User)|
|{00000000-0000-0000-0000-000000000027}|Policy Agent Evaluate Assignment (User)|
|{00000000-0000-0000-0000-000000000031}|Software Metering Generating Usage Report|
|{00000000-0000-0000-0000-000000000032}|Source Update Message|
|{00000000-0000-0000-0000-000000000037}|Clearing proxy settings cache|
|{00000000-0000-0000-0000-000000000040}|Machine Policy Agent Cleanup|
|{00000000-0000-0000-0000-000000000041}|User Policy Agent Cleanup|
|{00000000-0000-0000-0000-000000000042}|Policy Agent Validate Machine Policy / Assignment|
|{00000000-0000-0000-0000-000000000043}|Policy Agent Validate User Policy / Assignment|
|{00000000-0000-0000-0000-000000000051}|Retrying/Refreshing certificates in AD on MP|
|{00000000-0000-0000-0000-000000000061}|Peer DP Status reporting|
|{00000000-0000-0000-0000-000000000062}|Peer DP Pending package check schedule|
|{00000000-0000-0000-0000-000000000063}|SUM Updates install schedule|
|{00000000-0000-0000-0000-000000000101}|Hardware Inventory Collection Cycle|
|{00000000-0000-0000-0000-000000000102}|Software Inventory Collection Cycle|
|{00000000-0000-0000-0000-000000000103}|Discovery Data Collection Cycle|
|{00000000-0000-0000-0000-000000000104}|File Collection Cycle|
|{00000000-0000-0000-0000-000000000105}|IDMIF Collection Cycle|
|{00000000-0000-0000-0000-000000000106}|Software Metering Usage Report Cycle|
|{00000000-0000-0000-0000-000000000107}|Windows Installer Source List Update Cycle|
|{00000000-0000-0000-0000-000000000108}|Software Updates Policy Action Software Updates Assignments Evaluation Cycle|
|{00000000-0000-0000-0000-000000000109}|PDP Maintenance Policy Branch Distribution Point Maintenance Task|
|{00000000-0000-0000-0000-000000000110}|DCM policy|
|{00000000-0000-0000-0000-000000000111}|Send Unsent State Message|
|{00000000-0000-0000-0000-000000000112}|State System policy cache cleanout|
|{00000000-0000-0000-0000-000000000113}|Update source policy|
|{00000000-0000-0000-0000-000000000114}|Update Store Policy|
|{00000000-0000-0000-0000-000000000115}|State system policy bulk send high|
|{00000000-0000-0000-0000-000000000116}|State system policy bulk send low|
|{00000000-0000-0000-0000-000000000121}|Application manager policy action|
|{00000000-0000-0000-0000-000000000122}|Application manager user policy action|
|{00000000-0000-0000-0000-000000000123}|Application manager global evaluation action|
|{00000000-0000-0000-0000-000000000131}|Power management start summarizer|
|{00000000-0000-0000-0000-000000000221}|Endpoint deployment reevaluate|
|{00000000-0000-0000-0000-000000000222}|Endpoint AM policy reevaluate|
|{00000000-0000-0000-0000-000000000223}|External event detection|



