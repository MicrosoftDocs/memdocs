---
title: Set up Desktop Analytics
titleSuffix: Configuration Manager
description: A how-to guide for setting up and onboarding to Desktop Analytics.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
---

# How to set up Desktop Analytics 

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

Use this procedure to sign in to Desktop Analytics and configure it in your subscription. This procedure is a one-time process to set up Desktop Analytics for your organization.  



## Initial onboarding

1. Open the [Desktop Analytics portal](https://aka.ms/m365aprod) in Microsoft 365 Device Management as a user with **Company Admin** permissions. Select **Start**.  

2. On the **Accept service agreement** page, review the service agreement, and select **Accept**.  

3. On the **Confirm your subscription** page, review the list of required qualifying licenses. Switch the setting to **Yes** next to **Do you have one of the supported or higher subscriptions**, and then select **Next**.  

4. On the **Give users access** page, Desktop Analytics pre-configures two security groups in Azure Active Directory:  

    - **Workspace Owners**: Create and manage workspaces. These accounts need owner access to the Azure subscription.  

    - **Workspace Contributors**: Create and manage deployment plans in this workspace. They don't need any additional Azure access.  
  
   To add a user to either group, type their name or e-mail address in the **Enter name or email address** section of the appropriate group. When finished, select **Next**. 

5. On the page to **Set up your workspace**:  

    - To use an existing workspace for Desktop Analytics, select it, and continue with the next step.  

        > [!Note]  
        > If you're already using Windows Analytics, select that same workspace. You need to reenroll devices to Desktop Analytics that you previously enrolled in Windows Analytics. 
        > 
        > You can only have one Desktop Analytics workspace per Azure AD tenant. Devices can only send diagnostic data to one workspace.   

    - To create a workspace for Desktop Analytics, select **Add workspace**.  

        1. Enter a **Workspace name**.<!--do we have any guidance for this name?-->  

        2. Select the drop-down list to **Select the Azure subscription name for this workspace**, and choose the Azure subscription for this workspace.  

        3. Select the **Region** from the list, and then select **Add**.  

6. Select a new or existing workspace, and then select **Set as Desktop Analytics workspace**.  Then select **Continue** in the **Confirm and grant access** dialog.  

7. In the new browser tab, pick an account to use to sign in. Select the option to **Consent on behalf of your organization** and select **Accept**.  

    > [!Note]  
    > This consent is to assign the MALogAnalyticsReader application the Log Analytics Reader role for the workspace. This application role is required by Desktop Analytics. For more information, see [MALogAnalyticsReader application role](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. Back on the page to **Set up your workspace**, select **Next**.  

9. On the **Last steps** page, select **Go to Desktop Analytics**. 

The Azure portal shows the Desktop Analytics **Home** page.



## Create app for Configuration Manager

Create an app in Azure AD for Configuration Manager.

1. In the [Azure portal](http://portal.azure.com), go to **Azure Active Directory**, and select **App registrations**. Then select **New application registration**.  

2. In the **Create** panel, configure the following settings:  

    - **Name**: a unique name that identifies the app, for example: `Desktop-Analytics-Connection`  

    - **Application type**: **Web app / API**  

    - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`  
  
   Select **Create**.  

3. Select the app, and note the **Application ID**. This value is a GUID that's used to configure the Configuration Manager connection.  

4. Select **Settings** on the app, and then select **Keys**. In the **Passwords** section, enter a **Key description**, specify an expiration **Duration**, and then select **Save**. Copy the **Value** of the key, which is used to configure the Configuration Manager connection. 

    > [!Important]  
    > This is the only opportunity to copy the key value. If you don't copy it now, you need to create another key.  
    > 
    > Save the key value in a secure location.  

5. On the app **Settings** panel, select **Required permissions**.  

    1. On the **Required permissions** panel, select **Add**.  

    2. In the **Add API access** panel, **Select an API**.  

    3. Search for the **Configuration Manager Microservice** API. Select it, and then choose **Select**.  

    4. On the **Enable Access** panel, select both of the application permissions: **Write CM Collection Data** and **Read CM Collection Data**. Then choose **Select**.  

    5. On the **Add API access** panel, select **Done**.  

6. On the **Required permissions** page, select **Grant permissions**. Select **Yes**.  

7. Copy the Azure AD tenant ID. This value is a GUID that's used to configure the Configuration Manager connection. Select **Azure Active Directory** in the main menu, and then select **Properties**. Copy the **Directory ID** value.  



## Next steps

Advance to the next article to connect Configuration Manager with Desktop Analytics.
> [!div class="nextstepaction"]  
> [Connect Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
