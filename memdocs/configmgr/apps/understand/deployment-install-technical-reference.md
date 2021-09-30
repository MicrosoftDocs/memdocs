---
title: Application installation technical reference
titleSuffix: Configuration Manager
description: Troubleshooting application installations technical reference for Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Application Installation

*Applies to: Configuration Manager (current branch)*

Before you continue, please review [Application deployment client components](client-components-technical-reference.md) to understand DCM and CI Agent job processing.

Application installation is performed by DCM Agent and CI Agent components when the deployment is enforced. The enforcement time differs for Available and Required deployments. To understand when the assignment is enforced, see the [Application Deployment to Device Collections](device-deployment-technical-reference.md) or [Application Deployment to User Collections](user-deployment-technical-reference.md) articles.

## Enforcement Initiation

Application installation is initiated by the CI Agent component on the client during the **StateEnforcingCIs** phase. This process is the same, regardless of whether the application is deployed to a Device Collection or a User collection.

- For **Available** deployments, the application is installed when the user initiates the application installation from Software Center.
- For **Required** deployments, the application is installed at deployment deadline. However, the user can initiate the installation from Software Center before the deadline.

When CI Agent initiates the application installation, it creates a task that is handled by the CI Task Manager component. CI Task Manager then initiates the installation. This activity can be tracked in the **CITaskMgr.log** by using the Deployment Type Unique ID.

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## Application Enforcement

After the application enforcement is initiated, the client performs the application detection again to ensure the application isn't already installed. Once it's determined that the application isn't installed, the application installation is initiated. This activity can be tracked in the **AppEnforce.log** on the client using the Deployment Type Unique ID.

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## Installation Verification

After the application is installed, the application detection method is used again to ensure that the application was detected as installed.

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

Finally, after enforcement is complete, CI Agent receives the task complete notification and the CI Agent job moves to the next phase.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## Next Steps

- [Troubleshoot application deployments](/troubleshoot/mem/configmgr/troubleshoot-application-deployment?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)

- [Common error codes for app installation](../../tenant-attach/app-install-error-reference.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)
