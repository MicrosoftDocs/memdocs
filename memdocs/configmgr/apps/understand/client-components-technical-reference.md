---
title: Application deployment client components technical reference
titleSuffix: Configuration Manager
description: Client components used for troubleshooting application deployment in Configuration Manager.
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

# Understanding Application Deployment Client Components

*Applies to: Configuration Manager (current branch)*

Application deployment evaluation and enforcement operations are handled by the DCM Agent and CI Agent components on the client. This article explains how a typical DCM and CI Agent job operates.

## DCM Agent

DCM Agent is the high-level client component responsible for evaluation of configuration items, which includes applications. When a deployment is activated or enforced, a DCM Agent job is created which reads the assignment policy and determines the actions that need to be performed. This activity can be tracked in the **DCMAgent.log** on the client using the DCM Agent Job ID, which can be identified by looking for the Application Unique ID.

### Device Deployments

- For **Required** deployments, DCMAgent.log would show the applicable actions. These actions may differ depending on whether the deployment deadline has already passed.

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- For **Available** deployments, DCMAgent.log shows that the deployment `is not mandatory`. For these deployments, application evaluation is done but enforcement is skipped unless the user initiated the installation.

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### User Deployments

- For **Required** deployments, DCMAgent.log would show the applicable actions. These actions may differ depending on whether the deployment deadline has already passed.

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- For **Available** deployments, DCM Agent jobs are created for evaluation and enforcement when the application installation is initiated by the user.

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## CI Agent

CI Agent is the client component responsible for evaluation and remediation of configuration items. DCM Agent reads the assignment policy and creates a job for the CI Agent component to perform the requested actions. **DCMAgent.log** records the CI Agent Job ID, which is useful for tracking the CI Agent activity in the **CIAgent.log** on the client.

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

A typical CI Agent job goes through multiple phases, which can be identified by filtering **CIAgent.log** on the CI Agent Job ID and then looking for `TransitionState`. Some of the key phases for an application deployment CI Agent job are:

- **DownloadingCIs**
  - During this phase, application metadata required to evaluate the application is downloaded. The metadata includes detection method, requirement rules, global conditions, etc. This activity can be tracked in **CIDownloader.log** and **DataTransferService.log**. For **Available** deployments, this process occurs during the first evaluation of the application. For **Required** deployments however, this process occurs immediately after the policy is downloaded.

- **InvokingSdmMethod**
  - During this phase, the application detection method is used to check if the application is installed and the desired state is determined. This activity can be tracked in **AppDiscovery.log** and **AppIntentEval.log**. For more information about this phase, see [Application Evaluation](deployment-evaluation-technical-reference.md).

- **StateDownloadingContents**
  - During this phase, application content is downloaded if necessary. This activity can be tracked in **CAS.log**, **ContentTransferManager.log**, **LocationServices.log**, and **DataTransferService.log**. For more information about this phase, see [Application Download](deployment-download-technical-reference.md).

- **StateEnforcingCIs**
  - During this phase, the application installation is initiated. This activity can be tracked in **AppEnforce.log**. For more information about this phase, see [Application Installation](deployment-install-technical-reference.md).

- **StateEnforcementReporting**
  - During this phase, application installation state is recorded for reporting to the Management Point. This activity can be tracked in **StateMessage.log**.

Although the CI Agent job goes through all the phases, it skips the phase if it isn't required. As an example, for **Available** deployments StateDownloadingContents and StateEnforcingCIs phases are skipped until the user attempts to install the application from Software Center. However, for **Required** deployments, the StateDownloadingContents phase downloads application content (if necessary) when the assignment is activated, but the StateEnforcingCIs phase is skipped if the deadline is in the future. This behavior can be observed in the CIAgent.log by filtering on the CI Agent Job ID and looking for `Skipping policy`.

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## Next Steps

- [Application Evaluation](deployment-evaluation-technical-reference.md)
- [Application Download](deployment-download-technical-reference.md)
- [Application Installation](deployment-install-technical-reference.md)
