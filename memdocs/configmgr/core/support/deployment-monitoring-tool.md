---
title: Deployment Monitoring Tool
titleSuffix: Configuration Manager
description: Use the Deployment Monitoring Tool to troubleshoot software deployments on a Configuration Manager client.
ms.date: 09/24/2019
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: install-set-up-deploy
ms.author: baladell 
author: BalaDelli
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Deployment Monitoring Tool

*Applies to: Configuration Manager (current branch)*

The Deployment Monitoring Tool is one of the [Configuration Manager tools](tools.md). It's a graphical user interface designed to assist in troubleshooting application, software update, and configuration baseline deployments on a Configuration Manager client. The tool is read-only as it doesn't change any state on the client. You can safely use it to diagnose common deployment scenarios.


## Features

- Run it as an administrator to troubleshoot deployments on a local client.  

- Troubleshoot deployments on a remote client. Launch the tool and connect to a remote machine as an administrator.  

- Export to XML all the data collected in the tool. Share the XML file with others, and use it as a common platform for talking about troubleshooting deployments.  

- Import previously exported data to a different machine, and use it to run the tool in offline mode.   


## Usage

The Deployment Monitoring Tool supports graphical user interface only. To launch the tool, run **DeploymentMonitoringTool.exe** as an administrator. There are three views:  

- **Client Properties**: A list of useful attributes about the device and the Configuration Manager client. This view is the default.   

- **Deployments**: View all of the currently targeted deployments. Select a deployment in the results pane to view more information in the details pane.  

- **All Updates**: View all of the software updates and their status.  

To copy data in any view, select a cell, and press **CTRL** + **C**.


### Actions menu

The following actions are available in the **Actions** menu:  

- **Connect to remote machine**: Select a computer to connect to. When you don't specify a user name and password, it uses the current credentials. Click **Save** to connect to remote computer.  

- **Export Data**: Select the file to write the data into, and click **Save**. Use the exported XML file for remote troubleshooting on a different computer.  

- **Import Data**: Select a file to import into the tool.  

- **View Log**: Opens an associated log file, depending upon the view:  
    - Client Properties: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Deployments: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - All Updates: `C:\Windows\WindowsUpdate.log`



## See also

- [Deploy applications](../../apps/deploy-use/deploy-applications.md)
- [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md)
- [Deploy configuration baselines](../../compliance/deploy-use/deploy-configuration-baselines.md)
