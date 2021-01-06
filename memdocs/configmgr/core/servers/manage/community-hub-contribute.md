---
title: Contribute to the community hub
titleSuffix: Configuration Manager
description: Contribute to the Configuration Manager community hub
ms.date: 01/07/2021
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fd401c9-4646-452d-beb4-1cc42d12caf3
author: mestew
ms.author: mstewart
manager: dougeby 
---

# Contribute to the community hub
<!--3555935, 3555936-->
The community hub fosters creativity by building on others work and having other people build on yours. GitHub already has industry-wide processes and tools built for sharing. Now, the community hub can leverage those tools directly in the Configuration Manager console as foundational pieces for driving this new community. You can share the following objects for use by others in the community:  

[!INCLUDE [Community hub object type information](includes/community-hub-object-types.md)]

## Prerequisites

- All [Community hub prerequisites and permissions](community-hub.md#prerequisites)
- A [GitHub](https://github.com) account
  - A GitHub account is only required to contribute and share content from the **Your hub** page.
  - If you don't already have a GitHub account, you can create one before you join.
   - If you don't wish to share, you can use contributions from others without having a GitHub account.

[!INCLUDE [Community hub security role information](includes/community-hub-security-roles.md)]

## Join the community hub to contribute content

1. Go to the **Community hub** node in the **Community** workspace.
1. Select **Your hub** and you'll be prompted to sign into GitHub. If you don't have an account, you'll be redirected to GitHub where you can create one. A GitHub account is only required to contribute and share content from the **Your hub** page.
1. Once you've signed into GitHub, select the **Join** button to join the community hub.

   ![Join Configuration Manager's community hub](./media/3555935-join-community-hub.png)

1. After joining, you'll see your membership request is pending. Your account needs approval by the Configuration Manager Content Curation team. Approvals are done once a day, so it may take up to one business day for your approval to be granted.
1. Once you're granted access, you'll get an email from GitHub. Open the link in the email to accept the invitation.
   > [!IMPORTANT]
   > You must accept the invitation sent in the email otherwise you won't be able to contribute content.

## Contribute content

Once you've accepted the invitation, you can contribute content.

1. Go to **Community** > **Community hub** > **Your hub**.
1. Select **Add an Item** to open the contribution wizard.
      ![Add an item to the community hub](./media/3555935-add-community-hub.png)
1. Specify the **Type** of object you want to share from the drop-down menu. The following object types are available:

     [!INCLUDE [Community hub object type information](includes/community-hub-object-types.md)]

1. Select **Browse** to load your environment's object list for the selected type. The object's **Name** and **Description** (if available) will automatically load in the contribution wizard.
1. Edit the following information to reflect what the community should see for your contribution:
   - **Name:** Name of your object
   - **Description:** The description of the object you're contributing.
1. Select **Next** to submit the contribution.
1. Once the contribution is complete, you'll see the GitHub pull request (PR) link. The link is also emailed to you. You can paste the link into a browser to view the PR. Your PR will go though the standard GitHub merge process.
   - PRs should be submitted through the Configuration Manager console, not directly to the GitHub repository.
1. Choose **Close** to exit the contribution wizard.
1. Once the PR has been completed and merged, the new item will display in the community hub home page for others to see.

## Update contributed content

You can update content you've contributed to the community hub.

1. Select an item that you previously contributed. Currently, you can only edit items that you contributed.
1. In the item details, select **Push Update** to open the contribute item wizard.
1. Edit the **Description** of the item to note what changes were made.  
1. Select **Next** to upload the item.
1. Once the item is uploaded, you'll be given the pull request URL of the change for monitoring.
1. Select **Close** when you're done to exit the wizard.

## <a name="bkmk_deeplink"></a> Directly link to community hub items
<!--4224406-->
[!INCLUDE [Community hub direct link information](includes/community-hub-links.md)]

## Next steps

Learn more about creating and using the following objects:

- [Create and run PowerShell scripts](../../../apps/deploy-use/create-deploy-scripts.md)
- [Introduction to reporting](introduction-to-reporting.md)
- [Create and manage task sequences](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Create and deploy an application](../../../apps/get-started/create-and-deploy-an-application.md)
- [Create configuration items](../../../compliance/deploy-use/create-configuration-items.md)