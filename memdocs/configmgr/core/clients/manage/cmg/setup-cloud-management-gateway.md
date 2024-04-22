---
title: Set up CMG
titleSuffix: Configuration Manager
description: Use this step-by-step process for setting up a cloud management gateway (CMG).
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.date: 09/18/2022
ms.topic: how-to
ms.subservice: client-mgt
ms.service: configuration-manager
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Set up CMG for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Once you have the prerequisites in place, you can start the process to set up a cloud management gateway (CMG). Before you start this process, make sure you have the necessary information and prerequisites to create a CMG. For more information, see [Set up checklist for CMG](set-up-checklist.md).

This step of the overall process includes the following actions:

- Use the Configuration Manager console to create the CMG service in Azure.
- Configure the primary site for client certificate authentication.
- Add the CMG connection point site system role.
- Configure the management point and software update point for CMG traffic.
- Configure boundary groups.

## Set up a CMG

> [!NOTE]
> Deploying a CMG with a **virtual machine scale set** in Azure was first introduced in version 2010 as a [pre-release feature](../../../servers/manage/pre-release-features.md).<!--3601040--> Beginning with version 2107, it's no longer a pre-release feature.<!-- 8959690 -->
>
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](../../../servers/manage/optional-features.md).

Do this procedure on the top-level site. That site is either a standalone primary site, or the central administration site (CAS).

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select **Cloud Management Gateway**.

1. Select **Create Cloud Management Gateway** in the ribbon.

1. On the **General** page of the wizard, first specify the **Azure environment** for this CMG:

    - **AzurePublicCloud**: Create the service in the global Azure cloud.
    - **AzureUSGovernmentCloud**: Create the service in the Azure US Government cloud.

1. Next choose how you want to deploy the CMG in Azure:

    - **Virtual machine scale set**

        - Starting in version 2203, virtual machine scale set is the only option.<!-- 13235079 -->

        - Starting in version 2107, this option is the recommended deployment method.<!-- 8959690 --> Even if you have an existing CMG deployed with the cloud service (classic) method, deploy new CMG instances as a virtual machine scale set.

        - In versions 2010 and 2103, you have to enable this pre-release feature to see it. In these releases, it's only intended for customers with a Cloud Solution Provider (CSP) subscription. If you already deployed a CMG with the **cloud service (classic)** method, this option is unavailable. For more information, see [Plan for CMG: Virtual machine scale sets](plan-cloud-management-gateway.md#virtual-machine-scale-sets).

    - **Cloud service (classic)**

        > [!IMPORTANT]
        > Starting in version 2203, the option to deploy a CMG as a **cloud service (classic)** is removed.<!-- 13235079 --> All CMG deployments should use a [virtual machine scale set](plan-cloud-management-gateway.md#virtual-machine-scale-sets).<!--10966586--> For more information, see [Removed and deprecated features](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

        - In version 2107 and later, only use this option if you can't deploy with a virtual machine scale set because of one of the [limitations](plan-cloud-management-gateway.md#limitations-with-versions-2107-and-later).

        - In versions 2010 and 2103, most customers should use this deployment method.
     
1. Starting in version 2309,  select **Microsoft Entra tenant name**,  **Microsoft Entra app name** automatically populates. Select **Sign in**. Authenticate with an Azure **Subscription Owner** account. If you own multiple subscriptions, select the **Subscription ID** of the subscription you want to use.

   > [!NOTE]
   > Starting in version 2309, We have deprecated the use of first party app for the creation of CMG. Now, CMG uses a third party server app to get bearer tokens.

1. In versions 2303 and below, Select **Sign in**. Authenticate with an Azure **Subscription Owner** account. The wizard automatically populates the remaining fields from the information stored during the Microsoft Entra integration prerequisite. If you own multiple subscriptions, select the **Subscription ID** of the subscription you want to use.

    Select **Next**, and wait as the site tests the connection to Azure.

1. On the **Settings** page of the wizard, first **Browse** to the .PFX file for the CMG server authentication certificate (**Certificate file**). The common name from this certificate is used to populate the **Service name** and **Deployment name** fields.

    If you use a wildcard certificate, replace the asterisk (`*`) in the **Service name** field with the globally unique deployment name prefix for your CMG.<!--491233-->

    1. Optionally specify a **Description** to further identify this CMG in the Configuration Manager console.

    1. Select an Azure **Region** for this CMG. The list of available regions may vary based on the selected subscription.

    1. Select a **Resource Group** option:

        - If you choose **Use existing**, then select an existing resource group from the list. This resource group needs to already exist in the same region you selected for the CMG. If you select an existing resource group, and it's in a different region than the previously selected region, the CMG will fail to deploy.

        - If you choose **Create new**, then enter the new resource group name.

    1. By default, the **VM Size** is **Standard (A2_V2)**. Select another option as your design specifies. For example, **Large (A4_v2)** for increased client capacity per VM, or **Lab (B2s)** in a small test environment.<!--3555749-->

        > [!IMPORTANT]
        > The **Lab (B2s)** size VM is only intended for lab testing and small proof-of-concept environments. For example, with the  Configuration Manager technical preview branch. The B2s VMs aren't intended for production use with the CMG. They are low cost and low performing.

    1. In the **VM Instance** field, enter the number of VMs for this service. The default is one, but you can scale up to 16 VMs per CMG.

    1. If you're using client authentication certificates, select **Certificates** to add trusted root certificates. Add all of the certificates in the trust chain.

        > [!NOTE]
        > A trusted root certificate isn't required when using Microsoft Entra ID or site-issued tokens for client authentication.

    1. By default, the wizard enables the option to **Verify Client Certificate Revocation**. A certificate revocation list (CRL) must be publicly published for this verification to work. For more information, see [Publish the certificate revocation list](security-and-privacy-for-cloud-management-gateway.md#publish-the-certificate-revocation-list).

    1. By default, the wizard enables the option to **Enforce TLS 1.2**. This setting requires the Azure VM to use the TLS 1.2 encryption protocol. It doesn't apply to any on-premises Configuration Manager site servers or clients. Starting in version 2107 with the [update rollup](../../../../hotfix/2107/11121541.md), this setting also applies to the CMG storage account.<!--10800237--> For more information, see [How to enable TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).<!-- SCCMDocs-pr#4021 -->

    1. By default, the wizard enables the option to **Allow CMG to function as a cloud distribution point and serve content from Azure storage**. If you plan on targeting deployments with content to clients, you need to configure the CMG to serve content.

1. Next is the **Alerts** page of the wizard. To monitor CMG traffic with a 14-day threshold, enable the threshold alert. Then specify the threshold, and the percentage at which to raise the different alert levels. You can also enable a storage alert threshold. Choose **Next** when you're done.

1. Review the settings, and complete the wizard.

Configuration Manager starts to set up the service. The amount of time it takes to completely provision the service in Azure is dependent upon the settings that you specified. To determine when the service is ready, view the **Status** column for the new CMG.

To troubleshoot CMG deployments, use **CloudMgr.log** and **CMGSetup.log**. For more information, see [Monitor CMG](monitor-clients-cloud-management-gateway.md#monitor-logs).

> [!TIP]
> You can also use the PowerShell cmdlet **New-CMCloudManagementGateway** for this process.<!--6978300--> Optionally use this cmdlet to create the CMG service. For more information, see [New-CMCloudManagementGateway](/powershell/module/configurationmanager/New-CMCloudManagementGateway).

## Configure primary site for client certificate authentication

If you're using [client authentication certificates](configure-authentication.md#pki-certificate) for clients to authenticate with the CMG, follow this procedure to configure each primary site.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select **Sites**.

1. Select the primary site to which your internet-based clients are assigned, and choose **Properties**.

1. Switch to the **Communication Security** tab, and select **Use PKI client certificate (client authentication) when available**.

1. If you don't publish a CRL, disable the following option: **Clients check the certificate revocation list (CRL) for site systems**.

## Add the CMG connection point

The CMG connection point is the site system role that's required for communication from your on-premises Configuration Manager deployment to the cloud-based CMG. Before you start this process, you should have already developed a plan for the role, and identified at least one existing site system server. For more information, see [Plan for the CMG](plan-cloud-management-gateway.md).

To add the CMG connection point, the following steps summarize the instructions to [install site system roles](../../../servers/deploy/configure/install-site-system-roles.md):

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Servers and Site System Roles** node.

1. Select an existing site server to which you want to add this role. In the ribbon, on the **Home** tab, select **Add Site System Roles**.

1. On the System Role Selection screen, choose **Cloud management gateway connection point**, and then select **Next**. Choose the **Cloud management gateway name** to which this server connects. The wizard will show the region for the selected CMG.

> [!IMPORTANT]
> If you're using client authentication certificates, the CMG connection point needs this certificate. For more information, see [client authentication certificate](configure-authentication.md#pki-certificate).

To troubleshoot CMG service health, use **CMGService.log** and **SMS_Cloud_ProxyConnector.log**. For more information, see [Log files](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).

> [!TIP]
> Optionally, you can also use the PowerShell cmdlet **Add-CMCloudManagementGatewayConnectionPoint** to add the CMG connection point role to a site system server.
>
> For more information, see [Add-CMCloudManagementGatewayConnectionPoint](/powershell/module/configurationmanager/Add-CMCloudManagementGatewayConnectionPoint).

## <a name="bkmk_role"></a> Configure client-facing roles for CMG traffic

Configure the management point and software update point site systems to accept CMG traffic. Do this procedure on the primary site, for all management points and software update points that service internet-based clients.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Servers and Site System Roles** node. On the Home tab of the ribbon, in the View group, select **Servers with Role**. Then select **Management point** from the list.

1. Select the site system server you want to configure for CMG traffic. Select the **Management point** role in the details pane, and then in the Site Role group of the ribbon, select **Properties**.

1. In the Management point properties sheet, under Client Connections select **Allow Configuration Manager cloud management gateway traffic**.

    Depending upon your CMG design and Configuration Manager version, you may need to enable the **HTTPS** option. For more information, see [Enable management point for HTTPS](configure-authentication.md#enable-management-point-for-https).

1. Select **OK** to close the management point properties window.

Repeat these steps for other management points as needed, and for any software update points.

## Configure boundary groups

<!--3640932-->
You can associate a CMG with a boundary group. This configuration allows clients to use the CMG for client communication according to boundary group relationships. This configuration is beneficial for VPN or branch office clients where it might be better to manage them via a CMG than over the VPN or WAN connection. If you enable the option to **Prefer cloud-based sources over on-premises sources** then clients will prefer the CMG for both policy and content.

For more information on boundary groups, see [Configure boundary groups](../../../servers/deploy/configure/boundary-groups.md).

When you [create or configure a boundary group](../../../servers/deploy/configure/boundary-group-procedures.md), on the **References** tab, add a cloud management gateway. This action associates the CMG with this boundary group.

## BranchCache

To enable a content-enabled CMG to use Windows BranchCache, install the BranchCache feature on the site server.<!-- SCCMDocs-pr#4054 -->

- If the site server has an on-premises distribution point site system role, configure the option in that role's properties to **Enable and configure BranchCache**. For more information, see [Configure a distribution point](../../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-general).

- If the site server doesn't have a distribution point role, install the **BranchCache** feature in Windows. For more information, see [Install the BranchCache feature](/windows-server/networking/branchcache/deploy/install-the-branchcache-feature).

If you've already distributed content to a CMG, and then decide to enable BranchCache, first install the feature. Then redistribute the content to the CMG.

## Distribute and manage content

Distribute content to the content-enabled CMG the same as any other distribution point. The management point doesn't include the CMG in the list of content locations unless it has the content that clients request. For more information, see [Distribute and manage content](../../../servers/deploy/configure/deploy-and-manage-content.md).

Manage content on a CMG the same as any other distribution point. These actions include assigning it to a distribution point group and managing content packages. For more information, see [Install and configure distribution points](../../../servers/deploy/configure/install-and-configure-distribution-points.md).

## Next steps

Continue your CMG setup by configuring clients for CMG:
  
> [!div class="nextstepaction"]
> [Configure clients for CMG](configure-clients.md)
