---
title: Community hub and GitHub
titleSuffix: Configuration Manager
description: Enable and use community hub in Configuration Manager
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby 
---

# Community hub and GitHub
<!--3555935, 3555936-->

The IT Admin community has developed a wealth of knowledge over the years. Rather than reinventing items like Scripts and Reports from scratch, we've built a **Configuration Manager community hub** where IT Admins can share with each other. By leveraging the work of others, you can save hours of work. The community hub fosters creativity by building on others work and having other people build on yours. GitHub already has industry-wide processes and tools built for sharing. Now, the community hub will leverage those tools directly in the Configuration Manager Console as foundational pieces for driving this new community.

## About community hub

Community hub supports the following objects:
- PowerShell Scripts
- Reports
- Task sequences
- Applications
- Configuration items  

The hub allows sharing these objects, but doesn't share any package source content associated with the objects. For example, boot images, OS upgrade packages, or driver packages referenced by a task sequence aren't shared.

The hub currently doesn't support object dependencies. For example, if you share app A that is dependent upon app B, it only shares app A with the community. Similarly, if a task sequence includes the Install Application step, the referenced apps aren't shared.

Passwords or other secrets are removed from a task sequence before sharing.


## Prerequisites

- A GitHub account

  - A GitHub account is only required to contribute and share content from the **My hub** page.
  - If you don't wish to share, you can use contributions from others without having a GitHub account.
  - If you don't already have a GitHub account, you can create one before you join.

- The device running the Configuration Manager console used to access the hub needs the following items:
   - Windows 10 build 17110 or higher
   - .NET Framework version 4.6 or higher


- To download reports, you need to turn on the option **Use Configuration Manager-generated certificates for HTTP site systems** at the site you're importing into. For more information, see [enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http). This prerequisite is also needed for updating hub objects.
   1. Go to **Administration** > **Site Configuration** > **Sites**.
   1. Select the site and choose **Properties** in the ribbon.
   1. On the **Communication Security** tab, select the option to **Use Configuration Manager-generated certificates for HTTP site systems**.

## Permissions

- To import a script: **Create** permission for SMS_Scripts class.
- To import a report: Full Administrator security role.

## Join the community hub to contribute content

1. Go to the **hub** node in the **Community** workspace.
1. Click on **My hub** and you'll be prompted to sign into GitHub. If you don't have an account, you'll be redirected to GitHub where you can create one.
1. Once you've signed into GitHub, click the **Join** button to join the community hub.

  [![Join Configuration Manager's community hub](./media/3555935-join-community-hub.png)](./media/3555935-join-community-hub.png#lightbox)

1. After joining, you'll see your membership request is pending. Your account needs approval by the Configuration Manager hub Content Curation team. Approvals are done once a day, so it may take up to one business day for your approval to be granted.
1. Once you're granted access, you'll get an email from GitHub. Open the link in the email to accept the invitation.

## Contribute content

Once you've accepted the invitation, you can contribute content.

1. Go to **Community** > **hub** > **My hub**.
1. Click **Add an Item** to open the contribution wizard.
1. Specify the settings for the object:
   - **Type:**
     - PowerShell Scripts
     - Reports
     - Task sequences
     - Applications
     - Configuration items  
   - **Name:** Name of your object
   - **Description:** The description of the object you're contributing.
1. Click **Next** to submit the contribution.
1. Once the contribution is complete, you'll see the GitHub pull request (PR) link. The link is also emailed to you. You can paste the link into a browser to view the PR. Your PR will go though the standard GitHub merge process.
1. Click **Close** to exit the contribution wizard.
1. Once the PR has been completed and merged, the new item will show up on the community hub home page for others to see.

## Updating hub objects

The hub manages updates to shared objects. There are two use cases for this scenario:

- You've downloaded an object from the hub. When you visit its entry in the Community hub, the hub detects that you have an older version of the object. You can update it in your site with the latest version from the hub.

- You created an object in your site, and share it in the hub. You then revise it in your site. When you revisit My hub, because the version changed, you can update the object in the hub.

> [!NOTE]
> Only the original contributor to the object uploaded to the hub can make changes and update their own item.
## Use the contributions of others

You don't need to sign into GitHub to use contributions others have made.

1. Go to the **hub** node in the **Community** workspace.
1. Select an item to download.
1. You'll need appropriate permissions in your Configuration Manager site to download objects from the hub and import them into the site.
    - To import a script: **Create** permission for SMS_Scripts class.
    - To import a report: Full Administrator security role.
1. Downloaded reports are deployed to a report folder called **hub** on the reporting services point. Downloaded scripts can be seen in the **Run Scripts** node.
1. View all items downloaded from the hub by your organization by clicking on **Your downloads** from the **hub** node.

[![All items downloaded from the community hub](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)


## Next steps

Learn more about creating and using the following objects:

- [Create and run PowerShell scripts](../../../apps/deploy-use/create-deploy-scripts.md)
- [Introduction to reporting](introduction-to-reporting.md)
- [Create and manage task sequences](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Create and deploy an application](../../../apps/get-started/create-and-deploy-an-application.md)
- [Create configuration items](../../../compliance/deploy-use/create-configuration-items.md)