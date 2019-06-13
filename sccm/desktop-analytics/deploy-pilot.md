---
title: How to deploy to pilot
titleSuffix: Configuration Manager
description: A how-to guide for deploying to a Desktop Analytics pilot group.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
---

# How to deploy to pilot with Desktop Analytics

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

One of the benefits of Desktop Analytics is to help identify the smallest set of devices that provide the widest coverage of factors. It focuses on the factors that are most important to a pilot of Windows upgrades and updates. Making sure the pilot is more successful allows you to move more quickly and confidently to broad deployments in production.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]



## Address issues

Use the Desktop Analytics portal to review any reported issues with assets that might block your deployment. Then approve, reject, or modify the suggested fix. All items must be marked **Ready** or **Ready (with remediation)** before the pilot deployment starts.

1. Go to the Desktop Analytics portal, and select **Deployment plans** in the Manage group.  

2. Open a deployment plan by selecting its name.  

3. Select **Prepare pilot** in the Prepare group of the deployment plan menu.  

4. On the **Apps** tab, review the apps that need your input.  

5. For each app, select the app name. In the information pane, review the recommendation, and select the upgrade decision. If you choose **Not reviewed** or **Unable**, then Desktop Analytics doesn't include devices with this app in the pilot deployment. If you choose **Ready (with remediation)**, use the   **Remediation notes** to capture the actions to take to address an issue, like *reinstall* or *find the manufacturer’s recommended version*.

6. Repeat this review for other assets.  



## Create software

Before you can deploy Windows, first create the software objects in Configuration Manager. For more information, see [Windows 10 in-place upgrade task sequence](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).



## Deploy to pilot devices

Configuration Manager uses the data from Desktop Analytics to create collections for the pilot and production deployments. Don't deploy the task sequence using a traditional deployment. Use the following procedure to create a Desktop Analytics-integrated phased deployment:

1. In the Configuration Manager console, go to the **Software Library**, expand **Desktop Analytics Servicing**, and select the **Deployment Plans** node.  

2. Select your deployment plan, and then select **Deployment Plan Details** in the ribbon.  

3. Select **Create Phased Deployment** in the ribbon. This action launches the Create Phased Deployment wizard.

    > [!Tip]  
    > If you want to create a classic task sequence deployment for just the pilot collection, select **Deploy** in the **Pilot status** tile. This action launches the Deploy Software Wizard. For more information, see [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).  

4. Enter a name for the deployment, and select the task sequence to use. Then configure the following collections:  

    - **First Collection**: Expand the **Deployment Plans** folder and select the **Pilot** folder. Select the pilot collection for this deployment plan.

    - **Second Collection**: Expand the **Deployment Plans** folder and select the **Production** folder. Select the production collection for this deployment plan.

    > [!Note]  
    > With the Desktop Analytics integration, Configuration Manager automatically creates pilot and production collections for the deployment plan. It can take up to 10 minutes for these collections to synchronize before you can use them.<!-- 3887891 -->
    >
    > These collections are reserved for Desktop Analytics deployment plan devices. Manual changes to these collections aren't supported.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Complete the wizard to configure the phased deployment. For more information, see [Create phased deployments](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).



## Monitor

### Configuration Manager console

Use Configuration Manager deployment monitoring the same as any other task sequence deployment. For more information, see [Monitor OS deployments](/sccm/osd/deploy-use/monitor-operating-system-deployments).


### Desktop Analytics portal

Use the Desktop Analytics portal to view the status of any deployment plan. Select the deployment plan, and then select **Plan overview**.

![Screenshot of deployment plan overview in Desktop Analytics](media/deployment-plan-overview.png)

Select the **Pilot** tile. It summarizes the current state of the pilot deployment. This tile also displays data for the number of devices not started, in progress, completed, or returning issues.

Any devices reporting errors or other issues are also listed in the Pilot detail area to the right. To get details of the reported issue, select **Review**. This action changes the view to the **Deployment status** page

The **Deployment status** page lists devices in the following categories:

- Not started
- In progress
- Completed
- Needs attention - devices
- Needs attention - issues

The **Needs attention** categories show the same information, but sorted differently.

Select a specific listing in either view to get more details about the detected issue.

As you address these deployment issues, the dashboard continues to show the progress of devices. It updates as devices move from **Needs attention** to **Completed**.



## Next steps

Let the pilot run for a period of time to collect operational data. Encourage users of pilot devices to test apps.

When your pilot deployment meets your success criteria, go to the next article to deploy to production.
> [!div class="nextstepaction"]  
> [Deploy to production](/sccm/desktop-analytics/deploy-prod)  
