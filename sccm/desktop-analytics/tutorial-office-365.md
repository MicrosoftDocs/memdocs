---
title: Tutorial - Deploy Office 365
titleSuffix: Configuration Manager
description: A tutorial on using Desktop Analytics and Configuration Manager to deploy Office 365 to a pilot group.
ms.date: 12/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 0b2b633a-91d7-4497-8c2a-1fc7aa310bb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
#Customer intent: As an IT Pro, I want to use Desktop Analytics to intelligently pilot Office 365 so that I can understand the best devices to start with getting current with Office.
---

# Tutorial: Deploy Office 365 to pilot 

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

This tutorial uses Desktop Analytics and Configuration Manager to deploy Office 365 ProPlus to a pilot group. It highlights the integration of the cloud service to deliver insights to deploy the app with the on-premises product. Use Desktop Analytics to determine the best devices to put in a pilot group. Then use Configuration Manager to get current with Office.

In this tutorial, you learn how to:  

> [!div class="checklist"]  
> * Set up Desktop Analytics in the Azure portal  
> * Connect Configuration Manager and configure device settings  
> * Create a Desktop Analytics deployment plan for Office 365 ProPlus  
> * Deploy Office 365 ProPlus in Configuration Manager to the pilot group  

If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

Desktop Analytics uses a *Log Analytics workspace* in your Azure subscription. A workspace is essentially a container that includes account information and simple configuration information for the account. For more information, see [Manage workspaces](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## Prerequisites

Before you start this tutorial, make sure you have the following prerequisites:  

<!-- ### Technical -->

- An active Azure subscription, with **Company Admin** permissions  

- Configuration Manager, version 1810 with hotfix KB4482615 or later, with **Full administrator** role  

- At least one Windows 10 device with the following configurations:  

    - Windows 10, version 1709, or later

    - The latest Windows 10 cumulative quality update  

    - Configuration Manager client version 1810 with hotfix KB4482615  

    - A Windows installer-based version of Office, such as Office 2013  

- Business approval to configure Windows diagnostic data level to **Enhanced** on the pilot devices  

    For more information, see [Desktop Analytics privacy](/sccm/desktop-analytics/privacy).

- Network connectivity from the device to the following internet endpoints:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://www.msftncsi.com`  
    - `https://www.msftconnecttest.com`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://nexusrules.officeapps.live.com`  
    - `https://nexus.officeapps.live.com`  
    - `https://office.pipe.aria.microsoft.com`  

    For more information, see [How to enable data sharing for Desktop Analytics](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

<!-- ### Licensing
<!--what's the minimum licensing that's needed for this tutorial?
These qualifying licenses only apply to the **Device Health** portion of Desktop Analytics:  

- Windows 10 Enterprise or Windows 10 Education: per-device with active Software Assurance  

- Windows 10 Enterprise E3 or E5: per-device or per-user subscription (included with Microsoft 365 F1, E3, or E5)  

- Windows 10 Education A3 or A5 (included with Microsoft 365 Education A3 or A5)  

- Windows Virtual Desktop Access E3 or E5: per-device of per-user subscription  
 -->

> [!Note]  
> These prerequisites are for the purposes of this tutorial. For more information about the general prerequisites for Desktop Analytics with Configuration Manager, see [Prerequisites](/sccm/desktop-analytics/overview#prerequisites).  



## Set up Desktop Analytics

Use this procedure to sign in to Desktop Analytics and configure it in your subscription. This procedure is a one-time process to set up Desktop Analytics for your organization.  

1. Open the [Desktop Analytics portal](https://aka.ms/m365aprod) in Microsoft 365 Device Management as a user with **Company Admin** permissions. Select **Start**.  

2. On the **Accept service agreement** page, review the service agreement, and select **Accept**.  

3. On the **Confirm your subscription** page, the list of required qualifying licenses are for Windows device health features of Desktop Analytics.<!--Switch the setting to **Yes** next to **Do you have one of the supported or higher subscriptions**--> Select **Next** to continue.  

4. On the **Give users access** page, Desktop Analytics pre-configures two security groups in Azure Active Directory:  

    - **Workspace Owners**: Create and manage workspaces. These accounts need owner access to the Azure subscription.  

    - **Workspace Contributors**: Create and manage deployment plans in this workspace. They don't need any additional Azure access.  
  
   To add a user to either group, type their name or e-mail address in the **Enter name or email address** section of the appropriate group. When finished, select **Next**. 

5. On the page to **Set up your workspace**:  

    - To use an existing workspace for Desktop Analytics, select it, and continue with the next step. <!--If you're already using Windows Analytics, select that workspace. Desktop Analytics transfers your data and configurations.-->  

    - To create a workspace for Desktop Analytics, select **Add workspace**.  

        1. Enter a **Workspace name**.<!--do we have any guidance for this name?-->  

        2. Select the drop-down list to **Select the Azure subscription name for this workspace**, and choose the Azure subscription for this workspace.  

        3. Select the **Region** from the list, and then select **Add**.  

6. Select a new or existing workspace, and then select **Set as Desktop Analytics workspace**.  Then select **Continue** in the **Confirm and grant access** dialog.  

7. In the new browser tab, pick an account to use to sign in. Select the option to **Consent on behalf of your organization** and select **Accept**.  

8. Back on the page to **Set up your workspace**, select **Next**.  

9. On the **Last steps** page, select **Go to Desktop Analytics**. The Azure portal shows the Desktop Analytics **Home** page.  

<!-- per Dhiren, this action happens automatically during onboarding
10. Assign the MALogAnalyticsReader application the Log Analytics Reader role for the workspace.  

    1. Go to the [Azure portal](http://portal.azure.com), and select **All resources**. Select the workspace of type **Log Analytics**.  

    2. In the workspace menu, select **Access control (IAM)**, then select **Add**.  

    3. In the **Add permissions** panel, configure the following settings:  

        - **Role**: **Log Analytics Reader**  

        - **Assign access to**: **Azure AD user, group, or application**  

        - **Select**: **MALogAnalyticsReader**  
  
   Select **Save**. The portal shows a notification that it added the role assignment.  
-->


### Update Configuration Manager

Install Configuration Manager hotfix KB4482615 to support integration with Desktop Analytics. 

1. Update the site  

    1. If you opted into the 1810 update by running a PowerShell script in late November or early December 2018, then first update to the generally available version.  

        1. First disable [automatic client upgrade](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#to-configure-automatic-client-upgrades). This action makes sure that clients don't upgrade twice.  

        2. Install the prerequisite 1810 GA rollup update **KB4479288**. (Package ID 930FA45E-530F-4B08-B1BF-DE3F5267B03C) This update is generally available in early January to all customers on the "fast ring" version of 1810.  

        > [!Note]  
        > If you updated to version 1810 when it was generally available after 19 December 2018, you don't need update KB4479288.  

    2. Download hotfix **KB4482615** from the [Microsoft Download Center](). (Package ID 86450B7D-3574-4CF7-8B11-486A2C1F62A6) <!--link will be available once the package is published-->  

    2. [Use the update registration tool to import hotfixes](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

2. Update clients. To simplify this process, consider using automatic client upgrade. For more information, see [Upgrade clients](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  


### Create an app in Azure AD for Configuration Manager  

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



## Connect Configuration Manager

Use this procedure to connect Configuration Manager to Desktop Analytics, and configure device settings. This procedure is a one-time process to attach your hierarchy to the cloud service.  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node. Select **Configure Azure Services** in the ribbon.  

2. On the **Azure Services** page of the Azure Services Wizard, configure the following settings:  

    - Specify a **Name** for the object in Configuration Manager  

    - Specify an optional **Description** to help you identify the service  

    - Select **Desktop Analytics** from the list of available services  
  
   Select **Next**.  

3. On the **App** page, select the appropriate **Azure environment**. Then select **Import** for the web app. Configure the following settings in the **Import Apps** window:  

    - **Azure AD Tenant Name**: This name is how it's named in Configuration Manager  

    - **Azure AD Tenant ID**: The **Directory ID** you copied from Azure AD   

    - **Client ID**: The **Application ID** you copied from the Azure AD app   

    - **Secret Key**: The key **Value** you copied from the Azure AD app   

    - **Secret Key Expiry**: The same expiration date of the key   

    - **App ID URI**: This setting should automatically populate with the following value: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Select **Verify**, and then select **OK** to close the Import Apps window. Select **Next** on the App page of the Azure Services Wizard.  

4. On the **Diagnostic Data** page, configure the following settings:  

    - **Commercial ID**: this value should automatically populate with your organization's ID  

    - **Windows 10 diagnostic data level**: select at least **Enhanced**  

    - **Allow Device Name in diagnostic data**: select **Enable**  
  
   Select **Next**. The **Available functionality** page shows the Desktop Analytics functionality that's available with the diagnostic data settings from the previous page. Select **Next**.  

5. On the **Collections** page, configure the following settings:  

    - **Display name**: The Desktop Analytics portal displays this Configuration Manager connection using this name. Use it to differentiate between different hierarchies. For example, *test lab* or *production*.  

    - **Target collection**: This collection includes all devices that Configuration Manager configures with your commercial ID and diagnostic data settings. It's the full set of devices that Configuration Manager connects to the Desktop Analytics service.  

    - **Devices in the target collection use a user-authenticated proxy for outbound communication**: By default, this value is **No**. If needed in your environment, set to **Yes**.   

    - **Select specific collections to synchronize with Desktop Analytics**: Select **Add** to include additional collections. These collections are available in the Desktop Analytics portal for grouping with deployment plans. Make sure to include pilot and pilot exclusion collections.  

        These collections continue to sync as their membership changes. For example, your deployment plan uses a collection with a Windows 7 membership rule. As those devices upgrade to Windows 10, and Configuration Manager evaluates the collection membership, those devices drop out of the collection and deployment plan.  

<!--         > [!Warning]  
        > For the Desktop Analytics private preview, the total membership of all collections shouldn't be more than 10,000 devices. These collections include the Target Collection and each additional collection.  
 -->
6. Complete the wizard.  

Configuration Manager creates a settings policy to configure devices in the Target Collection. This policy includes the diagnostic data settings to enable devices to send data to Microsoft. By default, clients update policy every hour. After receiving the new settings, it can be several hours more before the data is available in Desktop Analytics.

Monitor the configuration of your devices for Desktop Analytics. In the Configuration Manager console, go to the **Software Library** workspace, expand the **Microsoft 365 Servicing** node, and select the **Connection Health** dashboard.  

Configuration Manager synchronizes any Desktop Analytics deployment plans within 15 minutes of creating the connection. In the Configuration Manager console, go to the **Software Library** workspace, expand the **Microsoft 365 Servicing** node, and select the **Deployment Plans** node. 



## Create a Desktop Analytics deployment plan

Use this procedure to create a deployment plan in Desktop Analytics.

1. Open the [Desktop Analytics portal](https://aka.ms/m365aprod). Use credentials that have at least **Workspace Contributors** permissions.  

2. Select **Deployment Plans** in the Manage group.  

3. In the **Deployment Plans** pane, select **Create**.  

4. In the **Create deployment plan** pane, configure the following settings:  

    - **Name**: A unique name for the deployment plan, for example `Office 365 pilot`  

    - **Products and versions**: Select the **Office** product, and the latest available recommended version. For example, **Office 365 clients, version 1808 (recommended)**.  

    - **Device groups**: Select one or more groups, and then select **Set as Target Groups**. Groups with **sccm** as the source are collections synchronized from Configuration Manager.  

    - **Readiness rules**: These rules help to determine which devices qualify for upgrade. Select **Office Applications** and configure the following settings:  

        - Update Office 365 ProPlus from 32-bit to 64-bit. This setting only applies to devices running a 64-bit version of Windows. The default setting is **Yes**.  

        - When updating from an older version of Office, leave older deprecated Office apps. This behavior applies even if those apps don't exist in the newer version of Office. The default setting is **No**.  

        - Low install count threshold for your Office add-ins. The default threshold is `2%`. Add-ins below this threshold are automatically set to *Low install count*. Desktop Analytics doesn't validate these add-ins during the pilot. 

            If an add-in is installed on a higher percentage of computers than this threshold, the deployment plan marks the add-in as *Noteworthy*. Then you can decide its importance to test during the pilot phase.   

    - **Completion date**: Choose the date by which Office should be fully deployed to all the targeted devices.  

5. Select **Create**. The new plan appears in the list of deployment plans while its being processed. Processing can take up to 48 hours before you can proceed to the next step.  

6. Open the deployment plan by selecting its name.  

7. On the deployment plan menu, in the **Prepare** group, select **Identify importance**.  

    1. On the **Office Add-ins** tab, select to show only **Not Reviewed** assets.  

    2. Select each add-in, and then select **Edit**. You can select more than one app to edit at the same time.   

    3. Choose an importance level from the **Importance** list. If you want Desktop Analytics to validate the add-in during the pilot, select **Critical** or **Important**. It doesn't validate add-ins marked as **Not Important**. Consider the compatibility risk and other plan insights when assigning importance levels.  

        When assigning importance levels, you can also choose the Upgrade decision.  

    4. Select **Save** when complete.  

8. On the deployment plan menu, in the **Prepare** group, select **Identify pilot**.  

    1. Review the recommended devices for the pilot.  

    2. Select each device, and select **Add to Pilot**. If you disagree with the recommendation, select **Replace**.  

        For more information on how Desktop Analytics makes these recommendations, select the information icon in the top right corner of the **Identify pilot** pane.



## Deploy Office 365 in Configuration Manager

Use this procedure to deploy Office 365 ProPlus in Configuration Manager to the pilot group.

- If you don't already have one, first [create an app for Office 365 ProPlus](#bkmk_create-app)  

- [Deploy the app](#bkmk_deploy-app) using the Desktop Analytics deployment plan  

- [Install the app](#bkmk_install-app) from Software Center on a targeted device  

<!-- 
- [Monitor](#bkmk_monitor-app) status in Configuration Manager  
 -->

### <a name="bkmk_create-app"></a> Create an app for Office 365 ProPlus

1. In the Configuration Manager console, go to the **Software Library**, and select the **Office 365 Client Management** node. Select the **Office 365 Installer** tile on the dashboard.  

2. On the **Application Settings** page, provide a **Name** for this application. For example, `Office 365 ProPlus`. Optionally specify a **Description**. Specify the **Content location** for the installation files, and then select **Next**.  

3. On the **Office Settings** page, select **Go to the Office Customization Tool**. Configure any necessary deployment settings for your Office 365 installation:  

    1. In the **Products and releases** group, select **Office 365 ProPlus** from the list, and select **Add**.  

    2. In the **Language** group, select the primary language.  

    3. In the **Update and upgrade** group, make sure the setting to **Uninstall any MSI version of Office, including Visio and Project** is **On**.  

    4. Configure any additional settings as needed by your organization.  

    5. When complete, select **Review** in the upper right corner. Review the configured settings, and then select **Submit**.  

5. Select **Next**. On the **Deployment** page, select **No** to deploy it now. (The next procedure uses the Desktop Analytics deployment plan for the deployment.) Select **Next** and complete the wizard.  


### <a name="bkmk_deploy-app"></a> Deploy Office 365 using the Desktop Analytics deployment plan

1. In the Configuration Manager console, go to the **Software Library**, expand **Desktop Analytics Servicing**, and select the **Deployment Plans** node.  

2. Select your Office 365 pilot deployment plan, and then select **Deployment Plan Details** in the ribbon.  

3. In the **Pilot status** tile, choose **Application** from the drop-down list, and then select **Deploy**.  

4. On the **General** page of the Deploy Software Wizard, select **Browse** next to the **Software** field. Select your Office 365 application, for example, **Office 365 ProPlus**. With the Desktop Analytics integration, Configuration Manager automatically creates a collection for the pilot deployment plan. Select **Next**.  

5. On the **Content** page, select **Add**, and then select **Distribution point**. Select an available distribution point to host the installation content, and select **OK**. Then select **Next**.  

6. On the **Deployment Settings** page, select **Next** to accept the default settings. (An available installation.)  

7. On the **Scheduling** page, select **Next** to accept the default settings. (Available as soon as possible.)  

8. On the **User Experience** page, select **Next** to accept the default settings. (Display in Software Center and only show notifications for computer restarts.)  

9. On the **Alerts** page, select **Next** to accept the default settings.  

10. Complete the wizard.  


### <a name="bkmk_install-app"></a> Install Office 365 from Software Center

1. Sign in to a device that's a member of the pilot deployment plan.  

2. Open **Software Center** and install the available app for Office 365.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->




## Next steps

Advance to the next article to learn more about Desktop Analytics deployment plans.
> [!div class="nextstepaction"]  
> [Deployment plans](/sccm/desktop-analytics/deployment-plans)  

