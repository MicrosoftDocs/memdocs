---
title: Approve applications
titleSuffix: Configuration Manager
description: Learn about the settings and behaviors for application approval in Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Approve applications in Configuration Manager

*Applies to: Configuration Manager (current branch)*

When [deploying an application](/sccm/apps/deploy-use/deploy-applications) in Configuration Manager, you can require approval before installation. Users request the application in Software Center, and then you review the request in the Configuration Manager console. You can approve or deny the request.

## <a name="bkmk_approval"></a> Approval settings

The application approval behavior depends upon whether you enable the recommended [optional app approval experience](#bkmk_opt). One of the following approval settings appears on the **Deployment Settings** page of the application deployment:  

### <a name="bkmk_opt"></a> An administrator must approve a request for this application on the device

> [!Note]  
> Configuration Manager doesn't enable this feature by default. Before using it, enable the optional feature **Approve application requests for users per device**. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).
>
> If you don't enable this feature, you see the [prior experience](#bkmk_prior).  

The administrator approves any user requests for the application before the user can install it on the requested device. If the administrator approves the request, the user is only able to install the application on that device. The user must submit another request to install the application on another device. This option is grayed out when the deployment purpose is **Required**, or when you deploy the application to a device collection. <!--1357015-->  

> [!Note]  
> To take advantage of new Configuration Manager features, first update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.<!--SCCMDocs issue 646-->  

View **Application Requests** under **Application Management** in the **Software Library** workspace of the Configuration Manager console. (In version 1902 and earlier, this node is called **Approval Requests**.) There's now a **Device** column in the list for each request. When you take action on the request, the Application Request dialog also includes the device name from which the user submitted the request.

If a request isn't approved within 30 days, it's removed. Reinstalling the client might cancel any pending approval requests.  

When you require approval on a deployment to a device collection, the app isn't displayed in Software Center. If you require approval on a deployment to a user collection, the app is displayed in Software Center. You can still hide it from users with the client setting, **Hide unapproved applications in Software Center**. For more information, see [Software Center client settings](/sccm/core/clients/deploy/about-client-settings#software-center).

After you've approved an application for installation, you can **Deny** the request in the Configuration Manager console. This action doesn't cause the client to uninstall the application from any devices. It stops users from installing new copies of the application from Software Center.  

> [!Important]  
> Starting in version 1806, *the behavior has changed* when you revoke approval for an application that was previously approved and installed. Now when you **Deny** the request for the application, the client uninstalls the application from the user's device.<!--1357891-->  

Starting in version 1906, if you approve an app request in the console, and then deny it, you can now approve it again. The app is reinstalled on the client after you approve it.  <!-- 4224910 -->

Automate the approval process with the [Approve-CMApprovalRequest](https://docs.microsoft.com/powershell/module/configurationmanager/approve-cmapprovalrequest?view=sccm-ps) PowerShell cmdlet. Starting in version 1902, this cmdlet includes the **InstallActionBehavior** parameter. Use this parameter to specify whether to install the application right away or during non-business hours.<!-- SCCMDocs-pr issue #3418 -->

Starting in 1906, you can see which deployments require approval. Select an app in the **Applications** node. In the details pane, switch to the **Deployments** tab. There's a new column displayed by default, **Requires Approval**.

#### <a name="bkmk_retry"></a> Retry the install of pre-approved applications

<!--4336307-->
Starting in version 1906, you can retry the installation of an app that you previously approved for a user or device. The approval option is only for available deployments. If the user uninstalls the app, or if the initial install process fails, Configuration Manager doesn't reevaluate its state and reinstall it. This feature allows a support technician to quickly retry the app install for a user that calls for help.

1. Open the Configuration Manager console as a user that has the **Approve** permission on the Application object. For example, the **Application Administrator** or **Application Author** built-in roles have this permission.

1. Deploy an app that requires approval, and approve it.

    > [!Tip]  
    > Alternatively, [Install an application for a device](/sccm/apps/deploy-use/install-app-for-device). It creates an approved request for the app on the device.  

If the application doesn't install successfully, or the user uninstalls the app, use the following process to retry:

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Application Requests** node. (In version 1902 and earlier, this node is called **Approval Requests**.)

1. Select the previously approved app. In the Approval Request group of the ribbon, select **Retry install**.

#### Other app approval resources

- [Application approval improvements in ConfigMgr 1810](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Application-approval-improvements-in-ConfigMgr-1810/ba-p/303534)
- [Updates to the application approval process in Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Updates-to-the-application-approval-process-in-Configuration/ba-p/275048)

### <a name="bkmk_prior"></a> Require administrator approval if users request this application

> [!Note]  
> This experience applies if you don't enable the recommended [optional app approval experience](#bkmk_opt).

The administrator approves any user requests for the application before the user can install it. This option is grayed out when the deployment purpose is **Required**, or when you deploy the application to a device collection.  

Application approval requests are displayed in the **Application Requests** node, under **Application Management** in the **Software Library** workspace. (In version 1902 and earlier, this node is called **Approval Requests**.) If a request isn't approved within 30 days, it's removed. Reinstalling the client might cancel any pending approval requests.  

After you've approved an application for installation, you can **Deny** the request in the Configuration Manager console. This action doesn't cause the client to uninstall the application from any devices. It stops users from installing new copies of the application from Software Center.  


## <a name="bkmk_email-approve"></a> Email notifications

<!--1321550-->

Starting in version 1810, configure email notifications for application approval requests. When a user requests an application, you receive an email. Click links in the email to approve or deny the request, without requiring the Configuration Manager console.

You can define the email addresses of the users who can approve or deny the request while creating a new deployment for the application. If you need to change the list of email addresses afterwards, go to the **Monitoring** workspace, expand **Alerts**, and select the **Subscriptions** node. Select **Properties** from one of the **Approve application via email** subscriptions that's related to your application deployment.

If there is more than one alert, you can determine which alert goes with which deployment. Open the alert properties, and view the list of **Selected alerts** on the General tab. The deployment is enabled as the alert for this subscription.

Users can add a comment to the request from Software Center. This comment shows on the application request in the Configuration Manager console. Starting in version 1902, that comment also shows in the email. Including this comment in the email helps the approvers make a better decision to approve or deny the request.<!--3594063-->


### Prerequisites

#### To send email notifications and take action on internal network

With these prerequisites, recipients receive an email with notification of the request. If they are on the internal network, they can also approve or deny the request from the email.

- Enable the [optional feature](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Approve application requests for users per device**.  

- Configure [email notification for alerts](/sccm/core/servers/manage/use-alerts-and-the-status-system#to-configure-email-notification-for-alerts).  

- Enable the SMS Provider to use a certificate.<!--SCCMDocs-pr issue 3135--> Use one of the following options:  

    - Enable [Enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http) (recommended)  

        > [!Note]  
        > When the site creates a certificate for the SMS Provider, it won't be trusted by the web browser on the client. Based on your security settings, when responding to an application request, you may see a security warning.  

    - Manually bind a PKI-based certificate to port 443 in IIS on the server that hosts the SMS Provider role  

#### To take action from internet

With these additional optional prerequisites, recipients can approve or deny the request from anywhere they have internet access.

- Enable the SMS Provider administration service through the cloud management gateway. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Servers and Site System Roles** node. Select the server with the SMS Provider role. In the details pane, select the **SMS Provider** role, and select **Properties** in the ribbon on the Site Role tab. Select the option to **Allow Configuration Manager cloud management gateway traffic for administration service**.  

    - The SMS Provider requires **.NET 4.5.2** or later.  

- [Cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)  

- Onboard the site to [Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) for **Cloud Management**  

    - Enable [Azure AD User Discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Manually configure settings in Azure AD:  

        1. Go to the [Azure portal](https://portal.azure.com) as a user with *Global Admin* permissions. Go to **Azure Active Directory**, and select **App registrations**.  

        2. Select the application that you created for Configuration Manager **Cloud Management** integration.  

        3. In the **Manage** menu, select **Authentication**.  

            1. In the **Redirect URIs** section, paste in the following path: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

            2. Replace `<CMG FQDN>` with the fully qualified domain name (FQDN) of your cloud management gateway (CMG) service. For example, GraniteFalls.Contoso.com.  

            3. Then select **Save**.  

        4. In the **Manage** menu, select **Manifest**.  

            1. In the Edit manifest pane, find the **oauth2AllowImplicitFlow** property.  

            2. Change its value to **true**. For example, the entire line should look like the following line: `"oauth2AllowImplicitFlow": true,`  

            3. Select **Save**.  


### Configure email approval

1. In the Configuration Manager console, [deploy an application](/sccm/apps/deploy-use/deploy-applications) as available to a user collection. On the **Deployment Settings** page, enable it for approval. Then enter one or more email addresses to receive notification. Separate email addresses with a semi-colon (`;`).  

     > [!Note]  
     > Anyone in your Azure AD organization who receives the email can approve the request. Don't forward the email to others unless you want them to take action.  

2. As a user, request the application in Software Center.  

3. You receive an email notification within five minutes. The content of the email is similar to the following example:  

![Example email notification for application approval](media/1321550-email.png)

> [!Note]  
> The link to approve or deny is for one-time use. For example, you configure a group alias to receive notifications. Meg approves the request. Now Bruce can't deny the request.  

Review the **NotiCtrl.log** file on the site server for troubleshooting.


## Maintenance

Configuration Manager stores the information about the application approval request in the site database. For requests that are canceled or denied, the site deletes the request history after 30 days. You can configure this deletion behavior with the **Delete Aged Application Request Data** [site maintenance task](/sccm/core/servers/manage/maintenance-tasks). The site never deletes any approved or pending application requests.
