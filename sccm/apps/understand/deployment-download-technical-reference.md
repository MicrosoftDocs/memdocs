---
title: Application download technical reference
titleSuffix: Configuration Manager
description: Troubleshooting application download technical reference for Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Application Download in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Before you continue, please review [Application deployment client components](client-components-technical-reference.md) to understand DCM and CI Agent job processing.

## Download Initiation

Application content download is initiated by the CI Agent component on the client during the **StateDownloadingContents** phase. This process is the same, regardless of whether the application is deployed to a Device Collection or a User collection.

- For **Available** deployments, application content is downloaded when the user initiates the application installation from Software Center.
- For **Required** deployments, application content is downloaded when the assignment is activated and the application is found Applicable after evaluation. To understand when the assignment is activated, see the [Application Deployment to Device Collections](device-deployment-technical-reference.md) or [Application Deployment to User Collections](user-deployment-technical-reference.md) articles.

When CI Agent initiates the content download, it creates a task that is handled by the CI Task Manager component. CI Task Manager then initiates the content download. This activity can be tracked in the **CITaskMgr.log** by using the Deployment Type Unique ID.

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## Distribution Point Location

All download tasks are handled by Content Access component, which is responsible for managing the client cache. After the download task is created, Content Access component checks if the content is already available in the client cache. If the content isn't available, it creates a location request to get a list of Distribution Points from where the content can be obtained. This activity can be tracked in **CAS.log** and **LocationServices.log** on the client using the Content Unique ID.

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> Although Location Services component handles the location requests, it doesn't directly request locations from the Management Point. All requests to the Management Point typically go through CCM Messaging component, which logs to **CcmMessaging.log**.

Location reply XML contains the list of distribution points based on the client's boundary group. This list is parsed and persisted in WMI on the client according to the [Content Source Priority](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority). This activity can be seen in **ContentTransferManager.log**, by using the Content Unique ID and looking for `Persisted location`. 

If the location reply XML doesn't contain any distribution points, **ContentTransferManager.log** would show `Received empty location update` and the client may get stuck at 0% while downloading the application. This reply can typically occur because of boundary group configuration issues. For more information, see [Download failures](../deploy-use/troubleshoot-application-deployment.md#download-failures).

## Content Download

Once the Distribution Point locations are obtained, Content Access component creates a Content Transfer job. This activity can be tracked in **CAS.log** using the Content Unique ID.

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

Content Transfer Manager then creates a Data Transfer Service job to do the content download. This activity can be tracked in **ContentTransferManager.log** on the client using the Content Unique ID.

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> This log entry can be used to identify the CTM and DTS job ID's, which can be used to track the progress of the Content Transfer in **ContentTransferManager.log** and **DataTransferService.log** respectively.

Data Transfer Service performs the download of the application content by creating a Background Intelligent Transfer Service (BITS) job and waiting for the download to complete. This activity can be tracked in **DataTransferService.log** on the client using the DTS Job ID obtained from **ContentTransferService.log**.

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

After the download is complete, Content Access component is notified. Content Access component then verifies the downloaded content to ensure that the content was not altered during download. This activity can be tracked in **CAS.log** using the Content Unique ID.

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

Finally, after content is verified, CI Agent receives the task complete notification and the CI Agent job moves to the next phase.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## Next Steps

- [Application Installation](deployment-install-technical-reference.md)
