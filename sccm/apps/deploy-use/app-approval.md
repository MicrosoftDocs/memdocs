---
title: Approve applications
titleSuffix: Configuration Manager
description: Learn about the settings and behaviors for application approval in Configuration Manager.
ms.date: 12/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Approve applications in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

When [deploying an application](/sccm/apps/deploy-use/deploy-applications) in Configuration Manager, you can require approval before installation. Users request the application in Software Center, and then you review the request in the Configuration Manager console. You can approve or deny the request. 



## <a name="bkmk_approval"></a> Approval settings

The application approval behavior depends upon your version of Configuration Manager. One of the following approval settings appears on the **Deployment Settings** page of the application deployment:  

#### Require administrator approval if users request this application
*Applies to versions 1710 and earlier*

The administrator approves any user requests for the application before the user can install it. This option is grayed out when the deployment purpose is **Required**, or when you deploy the application to a device collection.  

Application approval requests are displayed in the **Approval Requests** node, under **Application Management** in the **Software Library** workspace. If a request isn't approved within 30 days, it's removed. Reinstalling the client might cancel any pending approval requests.  

After you've approved an application for installation, you can **Deny** the request in the Configuration Manager console. This action doesn't cause the client to uninstall the application from any devices. It stops users from installing new copies of the application from Software Center.  


#### An administrator must approve a request for this application on the device
*Applies to versions 1802 and later <sup>[Note 1](#bkmk_note1)</sup>*

<a name="bkmk_note1"></a>

> [!Note]  
> **Note 1**: Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options). 
> 
> If you don't enable this feature, you see the prior experience.  

The administrator approves any user requests for the application before the user can install it on the requested device. If the administrator approves the request, the user is only able to install the application on that device. The user must submit another request to install the application on another device. This option is grayed out when the deployment purpose is **Required**, or when you deploy the application to a device collection. <!--1357015-->  

> [!Note]  
> To take advantage of new Configuration Manager features, first update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.<!--SCCMDocs issue 646-->  

View **Approval Requests** under **Application Management** in the **Software Library** workspace of the Configuration Manager console. There's now a **Device** column in the list for each request. When you take action on the request, the Application Request dialog also includes the device name from which the user submitted the request.  

If a request isn't approved within 30 days, it's removed. Reinstalling the client might cancel any pending approval requests.  

After you've approved an application for installation, you can **Deny** the request in the Configuration Manager console. This action doesn't cause the client to uninstall the application from any devices. It stops users from installing new copies of the application from Software Center.  

> [!Important]  
> Starting in version 1806, *the behavior has changed* when you revoke approval for an application that was previously approved and installed. Now when you **Deny** the request for the application, the client uninstalls the application from the user's device.<!--1357891-->  



## <a name="bkmk_email-approve"></a> Email notifications
<!--1321550-->

Starting in version 1810, configure email notifications for application approval requests. When a user requests an application, you receive an email. Click links in the email to approve or deny the request, without requiring the Configuration Manager console.


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

        1. Go to the [Azure portal](https://portal.azure.com), select **Azure Active Directory**, and then select **App registrations**.  

        2. Select the application of type **Native** that you created for Configuration Manager **Cloud Management** integration.  

        3. In the app properties, select **Settings**, then select **Redirect URIs**.  

            1. In the Redirect URIs pane, paste in the following path: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

            2. Replace `<CMG FQDN>` with the fully qualified domain name (FQDN) of your cloud management gateway (CMG) service. For example, GraniteFalls.Contoso.com.  

            3. Then select **Save**. Close the **Settings** pane.  

        4. In the app properties, select **Manifest**.  

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

Configuration Manager stores the information about the application approval request in the site database. For requests that are cancelled or denied, the site deletes the request history after 30 days. You can configure this deletion behavior with the **Delete Aged Application Request Data** [site maintenance task](/sccm/core/servers/manage/maintenance-tasks). The site never deletes any approved or pending application requests.

