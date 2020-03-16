---
title: Client notification
titleSuffix: Configuration Manager
description: Manage clients by taking immediate action from the central Configuration Manager console.
ms.date: 03/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Client notification in Configuration Manager

*Applies to: Configuration Manager (current branch)*

To take immediate action on remote clients, send a client notification action from the Configuration Manager console. Start these actions on an individual device or on a collection of devices.

## Actions

The following actions are on the ribbon in the Device or Collection group of the Home tab.

### Install client

Opens the **Install Client Wizard**. This wizard uses client push installation to install a Configuration Manager client. For more information, see [Client push installation](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).

#### Permissions - Install client

This action requires the **Modify Resource** and **Read** permissions on the **Collection** object.

The following built-in roles have these permissions by default:

- Application Administrator  
- Full Administrator  
- Infrastructure Administrator  
- Operations Administrator  
- OS Deployment Manager  

Add these permissions to any custom roles that need to push the client.

### Run script

Opens the **Run Script** wizard to run a PowerShell script on all of the clients in the collection. For more information, see [Create and run PowerShell scripts](/sccm/apps/deploy-use/create-deploy-scripts).

#### Permissions - Run script

This action requires the **Run Script** permission on the **Collection** object.

The following built-in roles have this permission by default:

- Full Administrator  
- Infrastructure Administrator  
- Operations Administrator  

Add this permission to any custom roles that need to run scripts.

### Start CMPivot

Starts **CMPivot**, which runs real-time queries against the targeted devices. For more information, see [CMPivot](/sccm/core/servers/manage/cmpivot).

#### Permissions - Start CMPivot

This action requires the same permissions as the [Run script](#run-script) action.

Starting in version 1906, you can use the **Run CMPivot** permission on the **Collection** object.

## Client notification

These actions are under the **Client notification** menu, on the ribbon in the Device or Collection group of the Home tab.

In version 1806 or earlier, the **Client Notification** option is only available from either the Device Collection node or when you viewed the membership of a Device Collection. Starting in version 1810, you can start a **Client Notification** directly from the **Devices** node. There's no longer a requirement to be within a collection membership view. <!--SCCMDocs-pr issue 2972-->

#### Permissions - Client notification

<!--SCCMDocs-pr issue #2972-->
Starting in version 1810, client notification actions now require the **Notify Resource** permission on the Collection object. This permission applies to all actions under the **Client notification** menu.

The following built-in roles have this permission by default:

- Full Administrator  
- Operations Administrator  

Add this permission to any custom roles that need to use client notification actions.

### Download computer policy

Refresh the device policy. For more information, see [Initiate policy retrieval for a Configuration Manager client](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

### Download user policy

Refresh the user policy.  

### Collect discovery data

Trigger clients to send a discovery data record (DDR). For more information, see [Heartbeat discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat).  

### Collect software inventory

Trigger clients to run a software inventory cycle. For more information, see [Introduction to software inventory](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  

### Collect hardware inventory

Trigger clients to run a hardware inventory cycle. For more information, see [Introduction to hardware inventory](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).  

### Evaluate application deployments

Trigger clients to run an application deployment evaluation cycle. For more information, see [Schedule re-evaluation for deployments](/sccm/core/clients/deploy/about-client-settings#schedule-re-evaluation-for-deployments).  

### Evaluate software update deployments

Trigger clients to run a software updates deployment evaluation cycle. For more information, see [Introduction to software updates](/sccm/sum/understand/software-updates-introduction).  

### Switch to the next software update point

Trigger clients to switch to the next available software update point. For more information, see [Software update point switching](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  

### Evaluate device health attestation

Trigger Windows 10 clients to check and send their latest device health state. For more information, see [Health attestation](/sccm/core/servers/manage/health-attestation).  

### Wake Up

Starting in version 1810, trigger devices configured to support Wake-on-LAN to wake up using other devices on the same subnet to send the Wake-on-LAN package. For more information, see [How to configure Wake on LAN](/sccm/core/clients/deploy/configure-wake-on-lan).

### Restart

Trigger the selected devices to restart. For more information, see [Restart clients](/sccm/core/clients/manage/manage-clients#restart-clients).

## Client diagnostics
<!--4433455-->

Starting in version 1910, there are new device actions for **Client Diagnostics** in the Configuration Manager console. The following actions have been added:

- **Enable verbose logging**: Change the global log level for the CCM component to verbose, and enable debug logging.
- **Disable verbose logging**: Change the global log level to default, and disable debug logging.
- **Collect Client Logs** (starting in 2002): A client notification message is sent to the selected clients to gather the CCM logs. The logs are returned using software inventory file collection. <!--4226618-->
   - The size limit for the compressed client logs is 100 MB. <!--6366098-->
   - Use [Resource Explorer](configmgr/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory#bkmk_diag) manage and view these files.

   [![Collect client logs from the console](./media/4226618-collect-client-logs.png)](./media/4226618-collect-client-logs.png#lightbox)

> [!IMPORTANT]
> - These actions only change the log verbosity, not the size or history. More verbose logging can generate more log content.
> - The management point role also uses the CCM component. If the targeted device is also a management point, this action also applies to that role.

For more information about these settings, see [About log files](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_reg-client).

Track the status of the task in the **diagnostics.log** on the client.

### Prerequisites - Client diagnostics

- Update the target client to the latest version.

- Your Configuration Manager administrative user needs the **Notify resource** permission.

  The following built-in roles have this permission by default:

  - Full Administrator  
  - Infrastructure Administrator  

  Add this permission to any custom roles that need to use client notification actions.


## Endpoint Protection

The following actions are under the **Endpoint Protection** menu. This menu is on the ribbon in the Collection group of the Home tab. When you select one or more devices, these actions are on the **Selected Object** tab of the ribbon.

For more information, see [Endpoint Protection in Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).

### Permissions - Endpoint Protection

This action requires the **Enforce Security** permission on the **Collection** object.

The following built-in roles have this permission by default:

- Full Administrator  
- Endpoint Protection Manager  
- Operations Administrator  

Add this permission to any custom roles that need to trigger Endpoint Protection actions.

### Full Scan

Trigger Endpoint Protection or Windows Defender to run a *full* antimalware scan.  

### Quick Scan

Trigger Endpoint Protection or Windows Defender to run a *quick* antimalware scan.  

### Download Definition

Trigger Endpoint Protection or Windows Defender to download the latest antimalware definitions.  

## See also

- [How to manage clients](/sccm/core/clients/manage/manage-clients)
- [How to manage collections](/sccm/core/clients/manage/collections/manage-collections)
