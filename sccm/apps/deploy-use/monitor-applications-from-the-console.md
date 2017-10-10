---
title: "Monitor applications from the System Center Configuration Manager console"
description: "Monitor deployment of software, including updates, compliance settings, and applications by using the Monitoring workspace in Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
caps.latest.revision: 5
author: mattbriggsms.author: mabrigg
manager: angrobe

---
# Monitor applications from the System Center Configuration Manager console*Applies to: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager, you can monitor the deployment of all software, including software updates, compliance settings, applications, task sequences, and packages and programs. You can monitor deployments by using the **Monitoring** workspace in the Configuration Manager console or by using reports.  

 Applications in Configuration Manager support state-based monitoring, which enables you to track the last application deployment state for users and devices. These state messages display information about individual devices. For example, if an application is deployed to a collection of users, you can view the compliance state of the deployment and the deployment purpose in the Configuration Manager console.  

## Learn about compliance states in System Center Configuration Manager
 An application deployment state has one of the following compliance states:  

-   **Success** – The application deployment succeeded or was found to be already installed.  

-   **In Progress** – The application deployment is in progress.  

-   **Unknown** – The state of the application deployment could not be determined. This state is not applicable for deployments with a purpose of **Available**. This state is typically displayed when state messages from the client are not yet received.  

-   **Requirements Not Met** – The application was not deployed because it was not compliant with a dependency or a requirement rule, or because the operating system to which it was deployed was not applicable.  

-   **Error** – The application failed to deploy because of an error.  

You can view additional information for each compliance state, including subcategories within the compliance state and the number of users and devices in this category. For example, the **Error** compliance state includes the following subcategories:  

-   Error evaluating requirements  

-   Content related errors  

-   Installation errors  

 When more than one compliance state applies for an application deployment, you can see the aggregate state that represents the lowest compliance. For example:  

    -   If a user signs in to two devices and the application is successfully installed on one device but fails to install on the second device, the aggregate deployment state of the application for that user displays as **Error**.  

    -   If an application is deployed to all users that sign in to a computer, you receive multiple deployment results for that computer. If one of the deployments fails, the aggregate deployment state for the computer displays as **Error**.  

The deployment state for package and program deployments is not aggregated.  

 Use these subcategories to help you to quickly identify any important issues with an application deployment. You can also view additional information about the devices that fall into a particular subcategory of a compliance state.  

 Application management in Configuration Manager includes a number of built-in reports that enable you to monitor information about applications and deployments. These reports have the report category of **Software Distribution – Application Monitoring**.  

 For more information about how to configure reporting in Configuration Manager, see [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## Monitor the state of an application in the Configuration Manager console  

1.  In the Configuration Manager console, choose **Monitoring** > **Deployments**.  

3.  To review deployment details for each compliance state and the devices in that state, select a deployment, and then, on the **Home** tab, in the **Deployment** group, choose **View Status** to open the **Deployment Status** pane. In this pane, you can view the assets with each compliance state. Choose any asset to view more detailed information about the deployment status to that asset.  

    > [!NOTE]  
    >  The number of items that can be displayed in the **Deployment Status** pane is limited to 20,000. If you need to see more items, use Configuration Manager reports to view application status data.  
    >   
    >  The status of deployment types is aggregated in the **Deployment Status** pane. To view more detailed information about the deployment types, use the report **Application Infrastructure Errors** in the report category **Software Distribution – Application Monitoring**.  

4.  To review general status information about an application deployment, select a deployment, and then choose the **Summary** tab in the **Selected Deployment** window.  

5.  To review information about the applications deployment type, select a deployment, and then choose the **Deployment Types** tab in the **Selected Deployment** window.  

The information that's shown in the **Deployment Status** pane after you choose **View Status** is live data from the Configuration Manager database. The information that's shown in the **Summary** tab and the **Deployment Types** tab is summarized data.

If the data that is shown in the **Summary** tab and the **Deployment Types** tab does not match the data that's shown in the **Deployment Status** pane, choose **Run Summarization** to update the data in these tabs. You can configure the default application deployment summarization interval as follows:  

1. In the Configuration Manager console, choose **Administration** > **Site Configuration** > **Sites**.

2. From the **Sites** list, select the site for which you want to configure the summarization interval, and then in the **Home** tab, in the **Settings** group, choose **Status Summarizers**.

3. In the **Status Summarizers** dialog box, choose **Application Deployment Summarizer**, and then choose **Edit**.  

4. In the **Application Deployment Summarizer Properties** dialog box, configure the required summarization intervals, and then choose **OK**.  
