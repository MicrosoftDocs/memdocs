---
title: Approve applications
titleSuffix: Configuration Manager
description: Learn about the settings and behaviors for application approval in Configuration Manager.
ms.date: 08/12/2022
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: how-to
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Approve applications in Configuration Manager

*Applies to: Configuration Manager (current branch)*

When [deploying an application](deploy-applications.md) in Configuration Manager, you can require approval before installation. Users request the application in Software Center, and then you review the request in the Configuration Manager console. You can approve or deny the request.

> [!NOTE]
> Starting in version 2111, you can also use most approval behaviors with [application groups](create-app-groups.md#app-approval).<!-- 10992210 -->

## <a name="bkmk_approval"></a> Approval settings

The application approval behavior depends upon whether you enable the recommended [optional app approval experience](#bkmk_opt). One of the following approval settings appears on the **Deployment Settings** page of the application deployment:

### <a name="bkmk_opt"></a> An administrator must approve a request for this application on the device

> [!NOTE]
> Configuration Manager doesn't enable this feature by default. Before using it, enable the optional feature **Approve application requests for users per device**. For more information, see [Enable optional features from updates](../../core/servers/manage/optional-features.md).
>
> If you don't enable this feature, you see the [prior experience](#bkmk_prior).

The administrator approves any user requests for the application before the user can install it on the requested device. If the administrator approves the request, the user is only able to install the application on that device. The user must submit another request to install the application on another device. This option is grayed out when the deployment purpose is **Required**, or when you deploy the application to a device collection. <!--1357015-->

> [!NOTE]
> To take advantage of new Configuration Manager features, first update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.<!--SCCMDocs issue 646-->

View **Application Requests** under **Application Management** in the **Software Library** workspace of the Configuration Manager console. There's a **Device** column in the list for each request. When you take action on the request, the Application Request dialog also includes the device name from which the user submitted the request.

If a request isn't approved within 30 days, it's removed. Reinstalling the client might cancel any pending approval requests.

When you require approval on a deployment to a device collection, the app isn't displayed in Software Center. If you require approval on a deployment to a user collection, the app is displayed in Software Center. You can still hide it from users with the client setting, **Hide unapproved applications in Software Center**. For more information, see [Software Center client settings](../../core/clients/deploy/about-client-settings.md#software-center).

After you've approved an application for installation, you can **Deny** the request in the Configuration Manager console. If users haven't already installed the application, this action stops them from installing new copies of the application from Software Center. If an application was previously approved and installed, when you **Deny** the request for the application, the client uninstalls the application from the user's device.<!--1357891-->

If you approve an app request in the console, and then deny it, you can approve it again. The app is reinstalled on the client after you approve it.<!-- 4224910 -->

Automate the approval process with the [Approve-CMApprovalRequest](/powershell/module/configurationmanager/approve-cmapprovalrequest) PowerShell cmdlet. This cmdlet includes the **InstallActionBehavior** parameter. Use this parameter to specify whether to install the application right away or during non-business hours.<!-- SCCMDocs-pr issue #3418 -->

You can see which deployments require approval. Select an app in the **Applications** node. In the details pane, switch to the **Deployments** tab. There's a column displayed by default, **Requires Approval**.

#### <a name="bkmk_retry"></a> Retry the install of pre-approved applications

<!--4336307-->
You can retry the installation of an app that you previously approved for a user or device. The approval option is only for available deployments. If the user uninstalls the app, or if the initial install process fails, Configuration Manager doesn't reevaluate its state and reinstall it. This feature allows a support technician to quickly retry the app install for a user that calls for help.

1. Open the Configuration Manager console as a user that has the **Approve** permission on the Application object. For example, the **Application Administrator** or **Application Author** built-in roles have this permission.

1. Deploy an app that requires approval, and approve it.

    > [!TIP]
    > Alternatively, [install an application for a device](install-app-for-device.md). It creates an approved request for the app on the device.

If the application doesn't install successfully, or the user uninstalls the app, use the following process to retry:

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Application Requests** node.

1. Select the previously approved app. In the Approval Request group of the ribbon, select **Retry install**.

#### Other app approval resources

- [Application approval improvements in ConfigMgr 1810](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Application-approval-improvements-in-ConfigMgr-1810/ba-p/303534)
- [Updates to the application approval process in Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Updates-to-the-application-approval-process-in-Configuration/ba-p/275048)

### <a name="bkmk_prior"></a> Require administrator approval if users request this application

> [!NOTE]
> This experience applies if you don't enable the recommended [optional app approval experience](#bkmk_opt).

The administrator approves any user requests for the application before the user can install it. This option is grayed out when the deployment purpose is **Required**, or when you deploy the application to a device collection.

Application approval requests are displayed in the **Application Requests** node, under **Application Management** in the **Software Library** workspace. If a request isn't approved within 30 days, it's removed. Reinstalling the client might cancel any pending approval requests.

After you've approved an application for installation, you can **Deny** the request in the Configuration Manager console. This action doesn't cause the client to uninstall the application from any devices. It stops users from installing new copies of the application from Software Center.

## <a name="bkmk_email-approve"></a> Email notifications

<!--1321550-->

You can configure email notifications for application approval requests. When a user requests an application, you receive an email. Click links in the email to approve or deny the request, without requiring the Configuration Manager console.

You can define the email addresses of the users who can approve or deny the request while creating a new deployment for the application. If you need to change the list of email addresses afterwards, go to the **Monitoring** workspace, expand **Alerts**, and select the **Subscriptions** node. Select **Properties** from one of the **Approve application via email** subscriptions that's related to your application deployment.

If there is more than one alert, you can determine which alert goes with which deployment. Open the alert properties, and view the list of **Selected alerts** on the General tab. The deployment is enabled as the alert for this subscription.

Users can add a comment to the request from Software Center. This comment shows on the application request in the Configuration Manager console. That comment also shows in the email. Including this comment in the email helps the approvers make a better decision to approve or deny the request.<!--3594063-->

### Prerequisites

#### To send email notifications and take action on internal network

With these prerequisites, recipients receive an email with notification of the request. If they are on the internal network, they can also approve or deny the request from the email.

- Enable the [optional feature](../../core/servers/manage/optional-features.md) **Approve application requests for users per device**.

- Configure [email notification for alerts](../../core/servers/manage/configure-alerts.md#configure-email-notification-for-alerts).

    > [!NOTE]
    > The administrative user that deploys the application needs permission to create an alert and subscription. If this user doesn't have these permissions, they'll see an error at the end of the **Deploy Software Wizard**: "You do not have security rights to perform this operation."<!-- 2810283 -->

- [Set up the administration service in Configuration Manager](../../develop/adminservice/set-up.md).

> [!NOTE]
> If you have multiple child primary sites in a hierarchy, configure these prerequisites for each primary site where you want to enable this feature. The links in the email notification are for the administration service at the primary site.<!-- 7108472 -->

#### To take action from internet

With these additional optional prerequisites, recipients can approve or deny the request from anywhere they have internet access.

- Enable the SMS Provider administration service through the cloud management gateway. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Servers and Site System Roles** node. Select the server with the SMS Provider role. In the details pane, select the **SMS Provider** role, and select **Properties** in the ribbon on the Site Role tab. Select the option to **Allow Configuration Manager cloud management gateway traffic for administration service**.

- Install a supported version of the .NET Framework. Starting in version 2107, the SMS Provider requires .NET version 4.6.2, and version 4.8 is recommended.<!--10402814--> In version 2103 and earlier, this role requires .NET 4.5 or later. For more information, [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md#net-version-requirements).

- Set up a [cloud management gateway](../../core/clients/manage/cmg/overview.md).

  > [!NOTE]
  > This scenario doesn't support CMG deployments with a virtual machine scale set until Configuration Manager version 2207 or later is installed.

- Onboard the site to [Azure services](../../core/servers/deploy/configure/azure-services-wizard.md) for **Cloud Management**.

- Enable [Microsoft Entra user Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc).

- Manually configure settings in Microsoft Entra ID:

    1. Go to the [Azure portal](https://portal.azure.com) as a user with *Global Admin* permissions. Go to **Microsoft Entra ID**, and select **App registrations**.

    1. Select the **Client** application created for Configuration Manager **Cloud Management** integration.

    1. In the **Manage** menu, select **Authentication**.

        1. Add a new **Single-page application** type if not already present.
          
        1. In the **Redirect URIs** section, paste in the following path: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`

        1. Replace `<CMG FQDN>` with the fully qualified domain name (FQDN) of your cloud management gateway (CMG) service. For example, GraniteFalls.Contoso.com.

        1. For Configuration Manager version 2111 and later, in the **Implicit grant and hybrid flows** section, select the following options:<!-- 12510370 -->

            - **Access tokens (used for implicit flows)**
            - **ID tokens (used for implicit and hybrid flows)**

        1. Then select **Save**.

    > [!NOTE]
    > If on an existing Client Registration Application the Redirect URI needs to be updated, it will need to be created as SPA and older Redirect URI being removed.

### Configure email approval

1. In the Configuration Manager console, [deploy an application](deploy-applications.md) as available to a user collection. On the **Deployment Settings** page, enable it for approval. Then enter one or more email addresses to receive notification. Separate email addresses with a semi-colon (`;`).

     > [!NOTE]
     > Anyone in your Microsoft Entra organization who receives the email can approve the request. Don't forward the email to others unless you want them to take action.

1. As a user, request the application in Software Center.

1. You receive an email notification within five minutes. The content of the email is similar to the following example:

:::image type="content" source="media/1321550-email.png" alt-text="Example email notification for application approval.":::

> [!NOTE]
> The link to approve or deny is for one-time use. For example, you configure a group alias to receive notifications. Meg approves the request. Now Bruce can't deny the request.

Review the **NotiCtrl.log** file on the site server for troubleshooting.

## Maintenance

Configuration Manager stores the information about the application approval request in the site database. For requests that are canceled or denied, the site deletes the request history after 30 days. You can configure this deletion behavior with the **Delete Aged Application Request Data** [site maintenance task](../../core/servers/manage/maintenance-tasks.md). The site never deletes any approved or pending application requests.

## Next steps

[Monitor applications from the Configuration Manager console](monitor-applications-from-the-console.md)
