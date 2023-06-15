---
title: Tutorial - Deploy Windows 10
titleSuffix: Configuration Manager
description: A tutorial on using Desktop Analytics and Configuration Manager to deploy Windows 10 to a pilot group.
ms.date: 08/24/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: tutorial
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
#Customer intent: As an IT Pro, I want to use Desktop Analytics to intelligently pilot Windows 10 so that I can understand the best devices to start with getting current with Windows.
ms.localizationpriority: medium
ms.collection: tier3
---

# Tutorial: Deploy Windows 10 to pilot

This tutorial uses Desktop Analytics and Configuration Manager to deploy Windows 10 to a pilot group. It highlights the integration of the cloud service to deliver insights to deploy Windows with the on-premises product. Use Desktop Analytics to determine the best devices to put in a pilot group. Then use Configuration Manager to get current with Windows.

In this tutorial, you learn how to:

> [!div class="checklist"]
> - Set up Desktop Analytics in the Microsoft Intune admin center
> - Connect Configuration Manager and configure device settings
> - Create a Desktop Analytics deployment plan for Windows 10
> - Use Configuration Manager to deploy Windows 10 to the pilot group

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin. When configured properly, use of Desktop Analytics doesn't incur any Azure cost.

Desktop Analytics uses a *Log Analytics workspace* in your Azure subscription. A workspace is essentially a container that includes account information and simple configuration information for the account. For more information, see [Manage workspaces](/azure/log-analytics/log-analytics-manage-access?toc=%2fazure%2fazure-monitor%2ftoc.json).

## Prerequisites

Before you start this tutorial, make sure you have the following prerequisites:

- An active Azure subscription, with [**Global Admin**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions) permissions

    For more information, see [Desktop Analytics prerequisites](overview.md#prerequisites).

- A supported version of Configuration Manager with **Full administrator** role

- Installation media for the latest version of Windows 10

- At least one Windows 10 device with the following configurations:

    - A supported version of Windows 10, but less than the version of the installation media you plan to use

    - The latest Windows 10 cumulative quality update

    - A supported version of the Configuration Manager client

- Business approval to configure Windows diagnostic data level to **Optional (limited)** on the pilot devices

    For more information, see [Desktop Analytics privacy](privacy.md).

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
    - `https://kmwatsonc.events.data.microsoft.com`
    - `https://oca.telemetry.microsoft.com`
    - `https://login.live.com`
    - `https://graph.windows.net` (on Configuration Manager server role only)
    - `https://*.manage.microsoft.com` (on Configuration Manager server role only)

    For more information, see [How to enable data sharing for Desktop Analytics](enable-data-sharing.md#endpoints).

> [!IMPORTANT]
> These prerequisites are for the purposes of this tutorial. For more information about the general prerequisites for Desktop Analytics with Configuration Manager, see [Prerequisites](overview.md#prerequisites).

## Set up Desktop Analytics

Use this procedure to sign in to Desktop Analytics and configure it in your subscription. This procedure is a one-time process to set up Desktop Analytics for your organization.

1. Open the [Desktop Analytics portal](https://aka.ms/desktopanalytics) in Microsoft 365 Device Management as a user with **Global Admin** permissions. Select **Start**.

2. On the **Accept service agreement** page, review the service agreement, and select **Accept**.

3. On the **Confirm your subscription** page, the list of required qualifying licenses is for Windows device health features of Desktop Analytics. Select **Next** to continue.

4. On the **Give users access** page:

    - **Allow Desktop Analytics to manage Directory roles on your behalf**: Desktop Analytics automatically assigns the **Workspace Owners** the **Desktop Analytics Administrator** role. If those groups are already a **Global Admin**, there's no change.

        If you don't select this option, Desktop Analytics still adds users as members of the security group. A **Global Admin** needs to manually assign the **Desktop Analytics Administrator** role for the users.

        For more information about assigning administrator role permissions in Azure Active Directory (Azure AD) and the permissions assigned to **Desktop Analytics Administrators**, see [Azure AD built-in roles](/azure/active-directory/roles/permissions-reference#desktop-analytics-administrator).

    - Desktop Analytics preconfigures the **Workspace Owners** security group in Azure AD to create and manage workspaces and deployment plans.

        To add a user to the group, type their name or e-mail address in the **Enter name or email address** section. When finished, select **Next**.

5. On the page to **Set up your workspace**:

    > [!NOTE]
    > To complete this step, the user needs **Workspace Owner** permissions and additional access to the Azure subscription and Resource Group. For more information, see [prerequisites](overview.md#prerequisites).

    - Select your Azure subscription.

    - To use an existing workspace for Desktop Analytics, select it, and continue with the next step.

    - To create a workspace for Desktop Analytics, select **Add workspace**.

        1. Enter a **Workspace name**.

        2. Select the drop-down list to **Select the Azure subscription name for this workspace**, and choose the Azure subscription for this workspace.

        3. **Create new** Resource group or **Use existing**.

        4. Select the **Region** from the list, and then select **Add**.

6. Select a new or existing workspace, and then select **Set as Desktop Analytics workspace**. Then select **Continue** in the **Confirm and grant access** dialog.

7. In the new browser tab, pick an account to use to sign in. Select the option to **Consent on behalf of your organization** and select **Accept**.

    > [!NOTE]
    > This consent is to assign the MALogAnalyticsReader application the Log Analytics Reader role for the workspace. This application role is required by Desktop Analytics. For more information, see [MALogAnalyticsReader application role](troubleshooting.md#bkmk_MALogAnalyticsReader).

8. Back on the page to **Set up your workspace**, select **Next**.

9. On the **Last steps** page, select **Go to Desktop Analytics**. The admin center shows the Desktop Analytics **Home** page.

## Connect Configuration Manager

Use this procedure to connect to Desktop Analytics and configure device settings. This procedure is a one-time process to attach your hierarchy to the cloud service.

### Connect to the service

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node. Select **Configure Azure Services** in the ribbon.

2. On the **Azure Services** page of the Azure Services Wizard, configure the following settings:

    - Specify a **Name** for the object in Configuration Manager

    - Specify an optional **Description** to help you identify the service

    - Select **Desktop Analytics** from the list of available services
  
   Select **Next**.

3. On the **App** page, select the appropriate **Azure environment**. Then select **Browse** for the web app.

4. Select **Create** to easily add an Azure AD app for the Desktop Analytics connection.

5. Configure the following settings in the **Create Server Application** window:

    - **Application Name**: A friendly name for the app in Azure AD.

    - **HomePage URL**: This value isn't used by Configuration Manager, but required by Azure AD. By default this value is `https://ConfigMgrService`.

    - **App ID URI**: This value needs to be unique in your Azure AD tenant. It's in the access token used by the Configuration Manager client to request access to the service. By default this value is `https://ConfigMgrService`. Change the default to one of the following recommended formats:<!-- 10617402 -->

      - `api://{tenantId}/{string}`, for example, `api://5e97358c-d99c-4558-af0c-de7774091dda/ConfigMgrService`
      - `https://{verifiedCustomerDomain}/{string}`, for example, `https://contoso.onmicrosoft.com/ConfigMgrService`

    - **Secret Key validity period**: choose either **1 year** or **2 years** from the drop-down list. One year is the default value.

    Select **Sign in**. After successfully authenticating to Azure, the page shows the **Azure AD Tenant Name** for reference.

    > [!NOTE]
    > Complete this step as a **Global Admin**. These credentials aren't saved by Configuration Manager. This persona doesn't require permissions in Configuration Manager, and doesn't need to be the same account that runs the Azure Services Wizard.

    Select **OK** to create the web app in Azure AD and close the Create Server Application dialog. On the Server App dialog, select **OK**. Then select **Next** on the App page of the Azure Services Wizard.

6. On the **Diagnostic Data** page, configure the following settings:

    - **Commercial ID**: this value should automatically populate with your organization's ID

    - **Windows 10 diagnostic data level**: select at least **Optional (limited)**

    - **Allow Device Name in diagnostic data**: select **Enable**
  
   Select **Next**. The **Available functionality** page shows the Desktop Analytics functionality that's available with the diagnostic data settings from the previous page. Select **Next**.

7. On the **Collections** page, configure the following settings:

    - **Display name**: The Desktop Analytics portal displays this Configuration Manager connection using this name. Use it to differentiate between different hierarchies. For example, *test lab* or *production*.

    - **Target collection**: This collection includes all devices that Configuration Manager configures with your commercial ID and diagnostic data settings. It's the full set of devices that Configuration Manager connects to the Desktop Analytics service.

    - **Devices in the target collection use a user-authenticated proxy for outbound communication**: By default, this value is **No**. If needed in your environment, set to **Yes**.

    - **Select specific collections to synchronize with Desktop Analytics**: Select **Add** to include other collections. These collections are available in the Desktop Analytics portal for grouping with deployment plans. Make sure to include pilot and pilot exclusion collections.

        These collections continue to sync as their membership changes. For example, your deployment plan uses a collection with a Windows 7 membership rule. As those devices upgrade to Windows 10, and Configuration Manager evaluates the collection membership, those devices drop out of the collection and deployment plan.

8. Complete the wizard.

Configuration Manager creates a settings policy to configure devices in the Target Collection. This policy includes the diagnostic data settings to enable devices to send data to Microsoft. By default, clients update policy every hour. After receiving the new settings, it can be several hours more before the data is available in Desktop Analytics.

> [!NOTE]
> For more information on these settings, see [Windows settings](enroll-devices.md#windows-settings).

Monitor the configuration of your devices for Desktop Analytics. In the Configuration Manager console, go to the **Software Library** workspace, expand the **Desktop Analytics Servicing** node, and select the **Connection Health** dashboard.

Configuration Manager synchronizes your collections within 60 minutes of creating the connection. In the Desktop Analytics portal, go to **Global Pilot**, and see your Configuration Manager device collections. It may take two to three days for the rest of the portal to show complete data. For more information, see [Data latency](troubleshooting.md#data-latency).

## Create a Desktop Analytics deployment plan

Use this procedure to create a deployment plan in Desktop Analytics.

1. Open the [Desktop Analytics portal](https://aka.ms/desktopanalytics). Use credentials that have at least **Workspace Contributors** permissions.

2. Select **Deployment Plans** in the Manage group.

3. In the **Deployment Plans** pane, select **Create**.

4. In the **Create deployment plan** pane, configure the following settings:

    - **Name**: A unique name for the deployment plan, for example `Windows 10 pilot`

    - **Products and versions**: Choose which Windows 10 version to deploy. Microsoft recommends creating deployment plans that use the most recent version.

    - **Device groups**: Select one or more groups from the Configuration Manager tab, and then select **Set as Target Groups**. These groups are collections synchronized from Configuration Manager.

    - **Readiness rules**: These rules help to determine which devices qualify for upgrade. Select **Windows OS** and configure the following settings:

        - **My computers automatically get drivers from Windows Update**: The default setting is **Off**, which is recommended when deploying with Configuration Manager.

        - **Define a low install count threshold for your apps**: The default setting is `2%`. Apps below this threshold are automatically set to *Low install count*. Desktop Analytics doesn't validate these add-ins during the pilot.

            If an app is installed on a higher percentage of computers than this threshold, the deployment plan marks the app as *Noteworthy*. Then you can decide its importance to test during the pilot phase.

    - **Completion date**: Choose the date by which Windows should be fully deployed to all the targeted devices.

5. Select **Create**. The new plan appears in the list of deployment plans while its being processed. To speed up processing, request an on-demand data refresh. For more information, see [Desktop Analytics FAQ](faq.yml#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal-).

6. Open the deployment plan by selecting its name.

7. On the deployment plan menu, in the **Prepare** group, select **Identify importance**.

    1. On the **Apps** tab, select to show only **Not Reviewed** assets.

    2. Select each app, and then select **Edit**. You can select more than one app to edit at the same time.

    3. Choose an importance level from the **Importance** list. If you want Desktop Analytics to validate the app during the pilot, select **Critical** or **Important**. It doesn't validate apps marked as **Not Important**. Assess its [compatibility](compat-assessment.md) and other plan insights when assigning importance levels.

        When assigning importance levels, you can also choose the Upgrade decision.

    4. Select **Save** when complete.

8. On the deployment plan menu, in the **Prepare** group, select **Identify pilot**.

    1. Review the recommended devices for the pilot.

    2. Select each device, and select **Add to Pilot**. If you disagree with the recommendation, select **Replace**.

        For more information on how Desktop Analytics makes these recommendations, select the information icon in the top-right corner of the **Identify pilot** pane.

9. On the deployment plan menu, in the **Prepare** group, select **Prepare pilot**.

    1. Review the assets with [Microsoft known issues](compat-assessment.md#microsoft-known-issues) across the **Apps** and **Drivers** tabs.

    2. To unblock your pilot devices, change the **Upgrade Decision** to **Ready**. Starting in Configuration Manager version 2103 with update rollup 10036164, items can also be marked **Ready (with remediation)**.<!-- CMADO-9906461 -->

## Deploy Windows 10 in Configuration Manager

Use this procedure to deploy Windows 10 in Configuration Manager to the pilot group.

- If you don't already have one, first [create an OS upgrade package for Windows 10](#create-an-os-upgrade-package-for-windows-10)

- If you don't already have one, [create an OS upgrade task sequence for Windows 10](#create-an-os-upgrade-task-sequence-for-windows-10)

- [Deploy the task sequence](#deploy-the-task-sequence-using-the-desktop-analytics-deployment-plan) using the Desktop Analytics deployment plan

- [Install the task sequence](#install-the-task-sequence-from-software-center) from Software Center on a targeted device

### Create an OS upgrade package for Windows 10

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Operating System Upgrade Packages** node.

2. On the **Home** tab of the ribbon, in the **Create** group, select **Add Operating System Upgrade Package**. This action starts the Add Operating System Upgrade Wizard.

3. On the **Data Source** page, specify the network **Path** to the installation source files of the OS upgrade package. For example, `\\server\share\path`.

    > [!NOTE]
    > The installation source files contain setup.exe and other files and folders to install the OS.

4. On the **General** page, specify a unique **Name** for the OS upgrade package.

5. Complete the Add Operating System Upgrade Package Wizard.

#### Distribute content

Next, distribute the OS upgrade package to distribution points.

1. Select the OS upgrade package in the list. On the **Home** tab of the ribbon, in the **Deployment** group, select **Distribute Content**. The Distribute Content Wizard opens.

2. On the **General** page, verify that the content listed is the content that you want to distribute, and then select **Next**.

3. On the **Content Destination** page, select **Add**, and choose **Distribution Point**. Select an existing distribution point, and then select **OK**. When you finish adding content destinations, select **Next**.

4. Complete the Distribute Content Wizard.

### Create an OS upgrade task sequence for Windows 10

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select **Task Sequences**.

2. On the **Home** tab of the ribbon, in the **Create** group, select **Create Task Sequence**.

3. On the **Create a New Task Sequence** page of the Create Task Sequence Wizard, select **Upgrade an operating system from an upgrade package**, and then select **Next**.

4. On the **Task Sequence Information** page, specify a **Task sequence name** that identifies the task sequence.

5. On the **Upgrade the Windows Operating System** page, specify the following settings, and then select **Next**:

    - **Upgrade package**: Specify the upgrade package that contains the OS upgrade source files.

    - **Edition index**: If there are multiple OS edition indexes available in the package, select an edition index. By default, the wizard selects the first index.

    - **Product key**: Specify the Windows product key for the OS to install. Specify encoded volume license keys or standard product keys. If you use a standard product key, separate each group of five characters by a dash (`-`). For example: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. When the upgrade is for a volume license edition, the product key may not be required.

        > [!NOTE]
        > This product key can be a multiple activation key (MAK), or a generic volume licensing key (GVLK). A GVLK is also referred to as a key management service (KMS) client setup key. For more information, see [Plan for volume activation](/windows/deployment/volume-activation/plan-for-volume-activation-client). For a list of KMS client setup keys, see [Appendix A](/windows-server/get-started/kmsclientkeys) of the Windows Server activation guide.

6. On the **Include Updates** page, select **Next** to not install any software updates.

7. On the **Install Applications** page, select **Next** to not install any applications.

8. Complete the Create Task Sequence Wizard.

### Deploy the task sequence using the Desktop Analytics deployment plan

1. In the Configuration Manager console, go to the **Software Library**, expand **Desktop Analytics Servicing**, and select the **Deployment Plans** node.

2. Select your Windows 10 pilot deployment plan, and then select **Deployment Plan Details** in the ribbon.

3. In the **Pilot status** tile, select **Deploy**.

4. On the **General** page of the Deploy Software Wizard, select **Browse** next to the **Task sequence** field. Select your Windows 10 in-place upgrade task sequence, and select **Next**.

    > [!NOTE]
    > With the Desktop Analytics integration, Configuration Manager automatically creates pilot and production collections for the deployment plan. Before you can use them, it can take time for these collections to synchronize. For more information, see [Troubleshoot - Data latency](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > This collection is reserved for Desktop Analytics deployment plan devices. Manual changes to this collection aren't supported.<!-- 3866460, SCCMDocs-pr 3544 -->

5. On the **Content** page, select **Add**, and then select **Distribution point**. Select an available distribution point to host the installation content, and select **OK**. Then select **Next**.

6. On the **Deployment Settings** page, select **Next** to accept the default settings. (An available installation.)

7. On the **Scheduling** page, select **Next** to accept the default settings. (Available as soon as possible.)

8. On the **User Experience** page, select **Next** to accept the default settings. (Display in Software Center and only show notifications for computer restarts.)

9. On the **Alerts** page, select **Next** to accept the default settings.

10. Complete the wizard.

### Install the task sequence from Software Center

1. Sign in to a device that's a member of the pilot deployment plan.

2. Open **Software Center** and install the available OS for Windows 10.

## Next steps

Advance to the next article to learn more about Desktop Analytics deployment plans.

> [!div class="nextstepaction"]
> [Deployment plans](about-deployment-plans.md)
