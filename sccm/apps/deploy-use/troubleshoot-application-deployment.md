---
title: Troubleshoot tips for app deployments
titleSuffix: Configuration Manager
description: Tips for troubleshooting application deployment problems in Configuration Manager
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Troubleshooting tips for application deployments

*Applies to: Configuration Manager (current branch)*

Typical problems with application deployments fall into one of the following categories:

- Application download failures

- Application deployment compliance stuck at 0%

If you experience either of these issues, this article provides some steps you can use to troubleshoot. For more in-depth troubleshooting, see [Troubleshooting application deployment technical reference](/sccm/apps/understand/app-deployment-technical-reference).


## Download failures

Application download failures include the following problems:

- The client is stuck downloading an application

- The client fails to download the application content

- The client gets stuck at 0% while downloading the application

The first thing to check when you experience application download failures is for missing or misconfigured boundaries and boundary groups. For example, if the client is on the intranet and not configured for internet-only client management, its network location must be in a configured boundary. There must also be a boundary group assigned to this boundary for the client to download content. For more information, see [Define site boundaries and boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups).

If you can't configure a boundary for a client, or if a specific boundary group can't be a member of another boundary group:

1. In the Configuration Manager console, open the properties of the **Deployment Type**.  

1. Switch to the **Content** tab.

1. In the section for using a distribution point from a neighbor boundary group or the default site boundary group, change the **Deployment options** to **Download content from distribution point and run locally**. (By default this setting is **Do not download content**.)

If the client can't download the application content, make sure it's distributed to a distribution point. To verify this configuration, use the in-console features to monitor content distribution to the distribution points. For more information, see [Monitor content you have distributed](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed).  


## Compliance stuck at 0%

When the application's deployment compliance is 0%, check the deployment status for the application in the **Monitoring** workspace under the **Deployments** node.

- **In Progress**: The client could be stuck [downloading content](#download-failures)

- **Error**: For more information on how to troubleshoot this problem, see the following blog post: [Tips and Tricks: How to Take Action on Assets That Report a Failed Deployment](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019)

- **Unknown**: This status usually means that the client hasn't received policy. Manually refresh client policy to see if the client receives it. For more information, see [Initiate policy retrieval for a Configuration Manager client](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).
  
If these actions don't resolve the issue, check the client status. There may be a deeper underlying problem with the client. For more information, see [How to monitor clients](/sccm/core/clients/manage/monitor-clients).


## Next steps

- [Monitor applications](/sccm/apps/deploy-use/monitor-applications-from-the-console)
- [Deploy applications](/sccm/apps/deploy-use/deploy-applications)
- [Management tasks for applications](/sccm/apps/deploy-use/management-tasks-applications)
- [Troubleshooting application deployment technical reference](/sccm/apps/understand/app-deployment-technical-reference)
