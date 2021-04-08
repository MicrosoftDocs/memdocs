---
title: Tenant attach - Applications (preview) in the admin center
titleSuffix: Configuration Manager
description: "Install applications for uploaded Configuration Manager devices from the admin center."
ms.date: 04/05/2021
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 963dda08-87b8-4e80-90a7-25625efe8861
manager: dougeby
author: mestew
ms.author: mstewart
---

# <a name="bkmk_apps"></a> Tenant attach: Install an application from the admin center (preview)
<!--cm 6024389, in 7220536 pubpreview Aug 10, 2020-->
*Applies to: Configuration Manager (current branch)*

> [!Important]
> - This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Endpoint Manager admin center**. From the Microsoft Endpoint Management admin center, you can initiate an application install in real time for a tenant attached device.

   :::image type="content" source="media/6024389-tenant-attach-application-list.png" alt-text="Screenshot of applications in Microsoft Endpoint Manager admin center" lightbox="media/6024389-tenant-attach-application-list.png":::

## Prerequisites

For Configuration Manager versions 2103, or later:

- All of the prerequisites for [Tenant attach: ConfigMgr client details](client-details.md#prerequisites).
- An application that meets one of the following requirements: <!--8795301-->
   - Is deployed to the device
   - Is deployed to a user that's logged in to the device, primary user of the device, and applications previously installed for the user
     - When you have a large number of device available applications, using the **An administrator must approve a request for this application on the device** on application deployments is recommended. For more information, see [Display all applications for a device in the admin center](#bkmk_all).

For Configuration Manager versions 2010, and earlier:

- All of the prerequisites for [Tenant attach: ConfigMgr client details](client-details.md#prerequisites)
- A minimum of [Update Rollup for Microsoft Endpoint Configuration Manager version 2002](https://support.microsoft.com/help/4560496/)
- Enable the optional feature **Approve application requests for users per device**. For more information, see [Enable optional features from updates](../core/servers/manage/install-in-console-updates.md#bkmk_options).
- At least one application deployed to a device collection with the **An administrator must approve a request for this application on the device** option set on the deployment. For more information, see [Approve applications](../apps/deploy-use/app-approval.md#bkmk_opt).
   - User targeted applications or applications without the approval option set don't appear in the application list when you're using Configuration Manager version 2002.
- A minimum of Configuration Manager version 2006 is required for installing [user targeted applications](#bkmk_user)<!--7518897-->.

## Permissions

The user account needs the following permissions:

- The **Read** permission for the device's **Collection** in Configuration Manager.
   - Apply the permission to both targeted device collections and targeted user collections.
- The **Read** permission for **Application** in Configuration Manager.
- The **Approve** permission for **Application** in Configuration Manager.
- An [Intune role](../../intune/fundamentals/role-based-access-control.md) assigned to the user <!--7980141-->

## Application status

You can filter the application list based on the status. The application status can be one of the following labels:

- **Available**: The application has never been installed on the device.
- **Installed**: The application is installed on the device.
- **Installing**: The application is currently installing.
- **Install requested**: The installation has been requested, but the client hasn't acknowledged the request yet.
   - If the device is offline, the install request will be acknowledged once it comes back online and receives the policy.  
- **Failed**: The application installation failed.
- **Requirements not met**: The application requirements haven't been met.
- **Not installed**: The application isn't currently installed. Typically this status is seen if a different deployment or a user removed the application.
- **Restart pending**: The application is installed but needs a restart to complete (starting in version 2006).
- **Required**: Installation is required for the application (starting in version 2103)

## <a name="bkmk_deploy"></a> Deploy an application to a device

1. In a browser, navigate to [https://endpoint.microsoft.com](https://endpoint.microsoft.com).
1. Select **Devices** then **All Devices**.
1. Select a device that is synced from Configuration Manager via [tenant attach](device-sync-actions.md).
1. Select **Applications**.
1. Select the application and choose **Install**.

   :::image type="content" source="media/6024389-tenant-attach-application-install.png" alt-text="Screenshot of application installation from Microsoft Endpoint Manager admin center" lightbox="media/6024389-tenant-attach-application-install.png":::

You can export all of the data currently in the view into a .csv file. At the top of the page, select the **Export** option to create the file. If the view exceeds 500 rows, only the first 500 are exported.

## <a name="bkmk_user"></a> Deploy an application to a user
<!--7518897-->
*(Introduced in version 2006)*

Starting in Configuration Manager version 2006, user available applications appear in the **Applications** node for a ConfigMgr device. The list of applications available for the device also includes applications deployed to the device's currently logged on user.

Deploying applications to a user has the following limitations:
- Multi-user session scenarios aren't supported.
- Azure AD joined devices aren't currently supported.
   - Devices that are both domain joined and Azure AD joined are supported.

## <a name="bkmk_repair"></a> Uninstall, repair, re-evaluate, or reinstall an application
<!--7979972, 8227649-->
*(Introduced in version 2010)*

 Starting in Configuration manager version 2010, administrators can do the following actions for applications in the Microsoft Endpoint Manager admin center:

- **Uninstall** an application
- **Repair** installation of an application
- **Re-evaluate** the application installation status
- **Reinstall** an application has replaced **Retry installation**

:::image type="content" source="./media/7979972-application-repair.png" alt-text="Screenshot of application installation options in the Microsoft Endpoint Manager admin center" lightbox="./media/7979972-application-repair.png":::

### Prerequisites to uninstall, repair, reinstall, or re-evaluate an application

- Install the latest version of the Configuration Manager client
- Targeted clients need to be online
- To uninstall an application:
   - The application must have at least one [deployment type](../apps/deploy-use/create-applications.md#start-the-create-deployment-type-wizard) with the uninstall command defined
   - Required deployments of the application can't be targeted to the client
   - The application must currently be installed on the device
- To repair an application:
   - The application must have at least one [deployment type](../apps/deploy-use/create-applications.md#start-the-create-deployment-type-wizard) with the repair command defined
   - The application must currently be installed on the device

#### Uninstall, repair, reinstall, or re-evaluate an application

1. Sign in to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com).
1. Go to **Devices** then **All Devices**.
1. Select a device that is synced from Configuration Manager via [tenant attach](device-sync-actions.md).
1. Choose **Applications**.
1. Select the application then one of the following actions you want to perform on the device:
   - **Reinstall**
   - **Re-evaluate**
   - **Uninstall**
   - **Repair**

## <a name="bkmk_all"></a> Display all applications for a device in the admin center
<!--8795301-->
*(Introduced in version 2103)*

Starting in Configuration Manager 2103, the **Applications** view for a tenant attached device in Microsoft Endpoint Manager admin center displays more applications from Configuration Manager. This improvement allows you to review when application installations are expected to occur on a device. Displayed applications include applications that are:
- Deployed to the device
- Deployed to a user that's logged in to the device, primary user of the device, or was previously installed.

:::image type="content" source="./media/8795301-display-required-app.png" alt-text="Screenshot showing details about required deadlines for applications in Microsoft Endpoint Manager admin center":::

The option, **An administrator must approve a request for this application on the device**, is no longer required to be set on the device available deployment for applications to be listed in the admin center. However, we recommend using the **An administrator must approve a request for this application on the device** option on application deployments when you have a large number of device available applications. By using this option, it defers targeting a new policy to the client until installation is initiated by the admin. By not targeting a large number of application policies to the client, it increases the performance of the site servers and the client. For more information about determining installation behavior, see [When will the application install on the device?](#bkmk_behavior).

### Review status of an application

1. Go to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/) and sign in.
1. From **Devices** > **All devices**, choose a device managed by **ConfigMgr**.
1. Select **Applications (preview)** then select an application that has a **Status** of **Required**.
1. Review the details of the schedule for the installation of the application.

## <a name="bkmk_display"></a> What applications and actions are available for my version of Configuration Manager?

The displayed application and available actions are dependent on the version of Configuration Manager. Use the chart below to help determine what applications and actions are available in the admin center:

|Configuration Manager version|Applications displayed|Available actions|
|---|---|---|
|Configuration Manager version 2002 with devices running any client version| Device-available applications with the **An administrator must approve a request for this application on the device** option set on the deployment.| Install </br> Reinstall|
|Configuration Manager version 2006 with devices running any client version| Device-available applications with the **An administrator must approve a request for this application on the device** option set on the deployment. </br> </br> All user-available applications| Install </br> Reinstall|
|Configuration Manager version 2010 with devices running client versions before 2010| Device-available applications with the **An administrator must approve a request for this application on the device** option set on the deployment. </br> </br> All user-available applications| Install </br> Reinstall|
|Configuration Manager version 2010 with devices running 2010 client versions| Device-available applications with the **An administrator must approve a request for this application on the device** option set on the deployment. </br> </br> All user-available applications|Install </br> Reinstall </br> Re-evaluate </br> Uninstall </br> Repair|
|Configuration Manager version 2103 with devices running 2006 or earlier client versions| All applications targeted to the device </br> </br> All user targeted applications related to the device. For example, applications targeted to the logged in user, primary user, and applications previously installed for the user are displayed.| For user and device-available applications with the **An administrator must approve a request for this application on the device** option set on the deployment: </br>&nbsp;&nbsp;&nbsp;Install</br>&nbsp;&nbsp;&nbsp;Reinstall</br></br>  All other applications display status but no actions are available |
|Configuration Manager version 2103 with devices running 2010 or later client versions| All applications targeted to the device  </br> </br> All user targeted applications related to the device. For example, applications targeted to the logged in user, primary user, and applications previously installed for the user are displayed| Install </br> Reinstall </br> Re-evaluate </br> Uninstall </br> Repair |

## <a name="bkmk_behavior"></a> When will the application install on the device?

Use the following table to determine installation behavior on the device when you install an app from the admin center:

|Deployment options | Client requires policy sync before installation|Client must be online to queue the installation|
|--|--|--|
|Device required | Yes | Yes|
|Device available | Yes | Yes|
|Device requires approval |No |No </br> The installation will occur when the client next comes online |
|User required| Yes | Yes |
|User available |No | No </br> The installation will occur when the client next comes online|
|User requires approval | No| No </br> The installation will occur when the client next comes online|

## Next steps

[Troubleshoot applications](troubleshoot-applications.md)
