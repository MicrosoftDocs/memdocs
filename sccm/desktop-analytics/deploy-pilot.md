---
title: How to deploy to pilot
titleSuffix: Configuration Manager
description: A how-to guide for deploying to a Desktop Analytics pilot group.
ms.date: 12/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
---

# How to deploy to pilot with Desktop Analytics

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

One of the benefits of Desktop Analytics is to help identify the smallest set of devices that provide the widest coverage of factors. It focuses on the factors that are most important to a pilot of Windows and Office upgrades and updates. Making sure the pilot is more successful allows you to move more quickly and confidently to broad deployments in production.  



## Address issues

Use the Desktop Analytics portal to review any reported issues with assets that might block your deployment. Then approve, reject, or modify the suggested fix. All items must be marked **Ready** or **Ready (with remediation)** before the pilot deployment starts. 

1. Go to the Desktop Analytics portal, and select **Deployment plans** in the Manage group.  

2. Open a deployment plan by selecting its name.  

3. Select **Prepare pilot** in the Prepare group of the deployment plan menu.  

4. On the **Apps** tab, review the apps that need your input.  

5. For each app, select the app name. In the information pane, review the recommendation, and select the upgrade decision. If you choose **Not reviewed** or **Unable**, then Desktop Analytics doesn't include devices with this app in the pilot deployment.  

6. Repeat this review for other assets.  

<!-- {OUR MASSIVE DISCUSSION OF UNDERSTANDING THE HEALTH STUFF IS CURRENTLY IN ‘DEPLOY TO PRODUCTION’—SHOULD IT GO HERE INSTEAD?}
 -->



## Create software

Before you can deploy Windows or Office, first create the software objects in Configuration Manager.

- [Office 365 ProPlus application](https://docs.microsoft.com/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)  

- [Windows 10 in-place upgrade task sequence](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)



## Deploy to pilot devices

Configuration Manager uses the data from Desktop Analytics to create a collection for the pilot deployment. Don't deploy the application or task sequence using a traditional deployment. Use the following procedure to create a Desktop Analytics-integrated deployment:

1. In the Configuration Manager console, go to the **Software Library**, expand **Desktop Analytics Servicing**, and select the **Deployment Plans** node.  

2. Select your deployment plan, and then select **Deployment Plan Details** in the ribbon.  

3. In the **Pilot status** tile, choose one of the following object types from the drop-down list:  

    - **Application** for Office 365 ProPlus  

    - **Task sequence** for Windows 10  
  
   Select **Deploy**. This action launches the Deploy Software Wizard for the selected object type. 


For more information, see the following articles:  

- [Deploy an application](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy)  

- [Deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)  


If your deployment plan is for both Windows 10 and Office 365, repeat this process to create a second deployment. For example, if the first deployment is for the task sequence, create a second deployment for the application.



## Monitor

Use Configuration Manager deployment monitoring the same as any other application and task sequence deployment. For more information, see the following articles:  

- [Monitor application from the Configuration Manager console](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

- [Monitor OS deployments](/sccm/osd/deploy-use/monitor-operating-system-deployments)  


Use the Desktop Analytics portal to view the status of any deployment plan. Select the deployment plan, and then select **Plan overview**. 

<!-- screenshot
[![deployment plan main view](UDRimages/UDR-dep-prog-master.png)](UDRimages/UDR-dep-prog-master.png)
 -->

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

When your pilot deployment meets your success criteria, go to the next article to deploy to production.
> [!div class="nextstepaction"]  
> [Deploy to production](/sccm/desktop-analytics/deploy-prod)  
