---
title: Application evaluation technical reference
titleSuffix: Configuration Manager
description: Troubleshooting application evaluation technical reference for Configuration Manager.
ms.date: 11/04/2019
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: troubleshooting
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Application Deployment Evaluation

*Applies to: Configuration Manager (current branch)*

Before you continue, please review [Application deployment client components](client-components-technical-reference.md) to understand DCM and CI Agent job processing.

Application evaluation is performed by the DCM Agent and CI Agent components when the deployment is activated. To understand when the assignment is activated, see the [Application Deployment to Device Collections](device-deployment-technical-reference.md) or [Application Deployment to User Collections](user-deployment-technical-reference.md) articles.

## Application Detection and Evaluation

Application evaluation is performed during the **InvokingSdmMethod** phase of a CI Agent job. This phase is where the client evaluates the detection method defined for the application to determine if the application is installed on the device. This activity can be tracked in **AppDiscovery.log** using the Deployment Type Unique ID or Deployment Type Name.

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> Above example shows detection for an MSI application where the detection is done by checking if the MSI Product Code is installed on the device. For applications using alternate detection methods, the appropriate detection method is used to check if the application is installed.

Next, the client evaluates the desired state of the application based on the Deployment Purpose. This step also involves detecting whether the application has any dependencies or supersedence rules that should be honored for the application. This activity can be tracked in **AppIntentEval.log** using the Application and Deployment Type Unique ID.

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

In the log entry above, **Current State** indicates whether the application is currently installed on the device. **Applicability** indicates whether the application is applicable based on defined requirement rules. **ResolvedState** indicates the desired state of the application based on the deployment purpose.

> [!TIP]
> Use the [Deployment Monitoring Tool](../../core/support/deployment-monitoring-tool.md) to view the application state, applicability state and requirement violations.

## Next Steps

- [Application Download](deployment-download-technical-reference.md)
