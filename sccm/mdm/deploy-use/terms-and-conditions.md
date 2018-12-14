---
title: "Terms and Conditions"
titleSuffix: "Configuration Manager"
description: "Deploy terms and conditions to user groups in System Center Configuration Manager."
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4d3f9e6b-4d71-4fc4-9b91-47f1bfbd8c70
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Add Terms and Conditions with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can deploy System Center Configuration Manager terms and conditions to user groups to explain how device enrollment, access to work resources, and using the Company Portal affect devices and users. Users must accept the terms and conditions before they can use the Company Portal to enroll and access their work.  

 ## Working with terms and conditions policies in System Center Configuration Manager  
 You can create and deploy multiple set of terms and conditions. You can also produce versions of the same terms and conditions in different languages and then deploy these to their appropriate groups.  

## To create a terms and conditions  

1. In the Configuration Manager console, go **Assets and Compliance** > **Overview** > **Compliance Settings** > **Terms and Conditions**.  

2. Click **Create Terms and Conditions** to create new terms and conditions.  

3. On the **General** page, specify the following information:  

   - **Name** - A unique name displayed in the Configuration Manager console  

   - **Description** - Details that help you identify the terms and conditions  in the Configuration Manager console  

     And then click **Next**.  

4. On the **Terms** page, specify the following information:  

   - **Title** - The title displayed to users in the Company Portal  

   - **Text for terms** - The terms and conditions displayed to users in the Company Portal  

   - **Text to explain what it means if the user accepts** - Label users see regarding acceptance. **Example**: "I agree to the terms and conditions."  

     And then click **Next**.  

5. Complete the wizard to create the new terms and conditions. The new terms and conditions are displayed in the Terms and Conditions node of the Assets and Compliance workspace.  

## To deploy a terms and conditions  

1.  In the Configuration Manager console, go to **Assets and Compliance** > **Overview** > **Compliance Settings** > **Terms and Conditions**.  

2.  In the **Terms and Conditions** list, select the item you want to deploy, and then click **Deploy**.  

3.  **Browse** to the **Collection** you want to deploy the terms and conditions to, and then click **OK**.  

     When targeted devices access the Company Portal app, it displays the terms and conditions you deployed. Users must accept these terms before they can gain access to company resources.  

    > [!NOTE]  
    >  If you deploy a set of terms to multiple user collections to which a user belongs, that user will see multiple copies of identical terms when opening Company Portal. Since  users can only accept or decline all terms, there is no danger of being in an ambiguous acceptance state where the user has both accepted and rejected the terms. The Terms and Conditions acceptance report will include only one row for each set of terms for each user, so there is no error in the report.  

## To monitor terms and conditions  

1.  You can monitor terms and conditions deployments in the Configuration Manager console. In the Configuration Manager console, go to **Monitoring** > **Overview** > **Deployments**.  

2.  Select the terms and conditions deployment. from the list of deployments  

     The summary area will show the following statistics:  

    -   **Compliant** - Users have accepted the latest version of the terms and conditions  

    -   **Error**  

    -   **Noncompliant** - Users have accepted a version of the terms and conditions, but not the latest version  

    -   **Unknown** -  Users have never accepted the terms and conditions, including those without an enrolled device  

3.  Select a terms and conditions deployment and then select **Run Summarization** to see individual users' Deployment Status.  

     On the Deployment Status screen you can select the status tabs to view users with that status. You can click **Run Summarization** to update the data throughout the hierarchy. Click **Refresh** to update data in the console  

## To view  a terms and conditions report  

1.  In the Configuration Manager console, go **Monitoring** > **Overview** > **Reporting** > **Report**.  

2.  Select **Terms and conditions acceptance** and then click **Run**. The Terms and conditions acceptance report opens. The report displays each user to whom terms and conditions have been deployed. Fields include:  

    -   Name of terms and conditions  

    -   User name  

    -   Accepted version  

    -   Date accepted  

    -   Accepted latest  

## Updates and version control for terms and conditions  
 When you edit existing terms and conditions, you can choose the behavior when you deploy the terms and conditions. Use the following procedure to help you update existing terms and conditions.  

### How to work with multiple versions of terms and conditions  

1.  In the Configuration Manager console, go **Assets and Compliance** > **Overview** > **Compliance Settings** > **Terms and Conditions**.  

2.  Select the terms and conditions instance that you want to edit, and double-click  to open it.  

3.  You can modify  content on the **General** or the **Terms** page to make any required edits.  

4.  On the **Terms** page you can then specify whether this new version requires all users to accept the terms and conditions, or if only new users will see the new version.  

     We recommend you increase the version number and require acceptance any time you make significant changes to your terms and conditions. Keep the current version number if you are fixing typos or changing formatting, for example.

> [!div class="button"]
> [< Previous step](configure-intune-subscription.md)  [Next step >](create-service-connection-point.md)
