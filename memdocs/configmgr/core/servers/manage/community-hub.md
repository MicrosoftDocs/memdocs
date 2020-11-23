---
title: Community hub and GitHub
titleSuffix: Configuration Manager
description: Enable and use Community hub in Configuration Manager
ms.date: 11/20/2020
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

The IT Admin community has developed a wealth of knowledge over the years. Rather than reinventing items like Scripts and Reports from scratch, we've built a **Configuration Manager Community hub** where IT Admins can share with each other. By leveraging the work of others, you can save hours of work. The community hub fosters creativity by building on others work and having other people build on yours. GitHub already has industry-wide processes and tools built for sharing. Now, the community hub can leverage those tools directly in the Configuration Manager Console as foundational pieces for driving this new community.

> [!Note]  
> Community hub is an optional cloud-based feature. It was first introduced in June 2020. For information on how to opt into **Community hub**, see [Optional features](install-in-console-updates.md#bkmk_options).

## About community hub

Community hub supports the following objects:

- CMPivot queries
- Applications
- Task sequences
- Configuration items
- PowerShell Scripts
- Reports

## Prerequisites

- The device running the Configuration Manager console used to access the community hub needs the following items:
   - .NET Framework version 4.6 or higher
   - Windows 10 build 17110 or higher
      - Windows Server isn't supported, so the Configuration Manager console needs to be installed on a Windows 10 device separate from the site server.
   - The logged-in user account can't be the built-in administrator account

- The [administration service](../../../develop/adminservice/set-up.md) in Configuration Manager needs to be set up and functional.

- If your organization restricts network communication with the internet using a firewall or proxy device, you need to allow the Configuration Manager console to access internet endpoints. For more information, see [Internet access requirements](../../plan-design/network/internet-endpoints.md#community-hub).


- A GitHub account
  - A GitHub account is only required to contribute and share content from the **Your hub** page.
  - If you don't wish to share, you can use contributions from others without having a GitHub account.
  - If you don't already have a GitHub account, you can create one before you join.

## Permissions

- To import a script: **Create** permission for **SMS_Scripts** class.
- To import a report: Full Administrator security role.
- Starting in version 2010, Full Administrators can opt in the hierarchy for uncurated content via hierarchy settings. Lower hierarchy administrators can't opt in the hierarchy for uncurated hub items.


Most [built-in security roles](../../../../understand/fundamentals-of-role-based-administration.md) will have access to Community hub:

|Role name|View the hub| Contribute hub content|Download hub content|
|---|---|---|---|
|Remote Tools Operator|No|N/A|N/A|
|Read Only Analyst|Yes|No|No|
|All other roles|Yes|Yes|Yes|

## Use the community hub

1. Go to the **Community hub** node in the **Community** workspace.
1. Select an item to download.
1. You'll need appropriate permissions in your Configuration Manager site to download objects from the hub and import them into the site.
    - To import a script: **Create** permission for SMS_Scripts class.
    - To import a report: Full Administrator security role.
1. Downloaded reports are deployed to a report folder called **hub** on the reporting services point. Downloaded scripts can be seen in the **Run Scripts** node.
1. View all items downloaded from the hub by your organization by selecting **Your downloads** from the **Community hub** node.

[![All items downloaded from the community hub](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)

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
     - Configuration item
     - CMPivot query
     - Report
     - PowerShell Script
     - Task sequence
     - Application

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

## <a name="bkmk_deeplink"></a> Direct links to community hub items
<!--4224406-->
*(Introduced in version 2006)*

You can easily navigate to and reference items in the Configuration Manager console **Community hub** node with a direct link. The intention for this feature is for easier collaboration by sharing links to community hub items with your colleagues. These deep links are currently only for items in the **Community hub** node of the console.

### Prerequisites for direct links

- Configuration Manager console version 2006 or later
- You can't use the local built-in administrator account when following a community hub link.

### Sharing and opening direct links

To share an item:
1. Go the item in the hub and select **Share**.
1. Paste the copied link and share it with others.

To open a shared link:
1. Open the link from a machine that has the Configuration Manager console installed.
   - For example, use this link to share the [Configure Microsoft Edge Auto Update script](https://communityhub.microsoft.com/item/7200) (`https://communityhub.microsoft.com/item/7200`).
1. Select **Launch the Community hub** when prompted.
1. The console opens directly to the script in the **Community hub** node.

## <a name="bkmk_category"></a> Categorize Community hub content
<!--8052494-->
*(Introduced in version 2010)*

Starting in Configuration Manager version 2010, Community hub content is grouped into a Microsoft, curated, or unreviewed category to allow admins to choose the types of content their environment displays. Admins can choose from the different categories of content that are provided in the Community hub to match their risk profile and their willingness to share and use content from those outside Microsoft and outside their own company. Only **Full Administrators** can opt in the hierarchy for uncurated content via hierarchy settings.

Community hub content has three categories for content sources:
- **Microsoft curated**: Content provided by Microsoft
- **Community curated**: Content provided by the community that gets reviewed by Microsoft
- **Community unreviewed**: General content from the community that doesn't get reviewed by Microsoft

:::image type="content" source="./media/8052494-community-hub-content-sources.png" alt-text="The three categories for content sources for Community hub":::

Admins can choose the types of content their environment displays from the following options:

- **Display Microsoft content**: Selecting this option means that only content created by Microsoft will be shown in the Community hub. This content has had some basic testing and scanning validation to confirm no malware and inappropriate text.
- **Display Microsoft and curated community content**: Show curated content from both Microsoft and community partners with basic level of review. Selecting this option means that only content that has been curated will be shown. The curation process includes basic review to confirm that the content doesn’t have malware and inappropriate text, but hasn’t necessarily been tested. It will include content from the community, not just from Microsoft.
- **Display all content including unreviewed content**:  Selecting this option means that all content is shown. This option includes unreviewed open-source type samples from the community, meaning that the content hasn’t necessarily been reviewed at all. It's provided as-is as open-source type sample content. Doing your own inspection and testing before using is highly encouraged, which is good practice on any content, but especially this class of content.

:::image type="content" source="./media/8052494-community-hub-content-hierarchy-settings.png" alt-text="Hierarchy settings for allowed content sources for Community hub":::

Since the content is *open-source* style content, admins should always review what is provided before consuming it. The new curation process is intended to vet the material to make sure there aren't obvious quality or compliance issues, but it will be somewhat of a cursory review. All content stored within GitHub and accessed from the Community hub isn’t supported by Microsoft. Microsoft doesn’t validate content collected from or shared by the general community. For more information, see [GitHub Terms of Service](https://help.github.com/terms) and [GitHub Privacy Statement](https://help.github.com/privacy).

### Select the content categories to display in Community hub for the environment

1. In the Configuration Manager console, go to **Administration** > **Overview** > **Site Configuration** > **Sites**.
1. Select the top-level site in your hierarchy and select **Hierarchy Settings** from the ribbon.
1. On the **General** tab, change the **Community hub** setting to **Display Microsoft content**.
1. Select **Ok** when you're finished changing the hierarchy setting.
1. Open the **Community hub** node in the **Community** workspace.
1. Ensure that only Microsoft content is displayed and available for download.
1. Go back to **Hierarchy Settings** and select another option such as **Display all content, including unreviewed content**.
1. Confirm that only the type of content is displayed and able to be downloaded from the Community hub, that matches the corresponding hierarchy setting category.
## <a name="bkmk_known"></a> Known issues

### Unable to access community hub node when running console as a different user
<!--7826897-->
If you're signed in as a user with lower rights and choose **Run as** a different user to open the Configuration Manager console, you may not be able to access the **Community hub** node.

### Downloaded reports don't get removed from your downloads page
<!--7851305-->
If you delete a downloaded report from the **Monitoring** > **Reports** node, the report isn't deleted from the **Community hub** > **Your downloads** page and you're unable to download the report again.

## Next steps

Learn more about creating and using the following objects:

- [Create and run PowerShell scripts](../../../apps/deploy-use/create-deploy-scripts.md)
- [Introduction to reporting](introduction-to-reporting.md)
- [Create and manage task sequences](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Create and deploy an application](../../../apps/get-started/create-and-deploy-an-application.md)
- [Create configuration items](../../../compliance/deploy-use/create-configuration-items.md)