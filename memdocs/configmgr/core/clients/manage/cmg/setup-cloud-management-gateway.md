---
title: Set up cloud management gateway
titleSuffix: Configuration Manager
description: Use this step-by-step process for setting up a cloud management gateway (CMG).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 05/04/2021
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
---

# Set up cloud management gateway for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Once you have the prerequisites in place, you can start the process to set up a cloud management gateway (CMG). Before you start this process, make sure you have the necessary information and prerequisites to create a CMG. For more information, see [Set up checklist for cloud management gateway](set-up-checklist.md).

This step of the overall process includes the following actions:

- Use the Configuration Manager console to create the CMG service in Azure.
- Configure the primary site for client certificate authentication.
- Add the CMG connection point site system role.
- Configure the management point and software update point for CMG traffic.
- Configure boundary groups.

> [!NOTE]
> Some sections that were previously in this article have moved:
>
> - **Before you begin**: [Set up checklist for CMG](set-up-checklist.md)
> - **Configure clients for CMG**: [Configure clients for CMG](configure-clients.md)
> - **Modify a CMG**: [Modify a CMG](modify-cloud-management-gateway.md)

## Set up a CMG

> [!IMPORTANT]
> Starting in version 2010,<!--3601040--> customers with a Cloud Solution Provider (CSP) subscription can deploy the CMG with a **virtual machine scale set** in Azure. In this version of Configuration Manager, it's a pre-release feature. To enable it, see [Pre-release features](../../../servers/manage/pre-release-features.md).
>
> Also note the following limitations for a **virtual machine scale set** deployment as you set it up:
>
> - It's only supported with a standalone primary site.
> - It doesn't support Azure US Government Cloud environments.
>
> If you already deployed a CMG with the **cloud service (classic)** method, you can't deploy another CMG as a **virtual machine scale set**. First [delete the existing CMG](modify-cloud-management-gateway.md#delete-the-service), and then create a new one with the other deployment method. All CMG instances for the site need to use the same deployment method.

Do this procedure on the top-level site. That site is either a standalone primary site, or the central administration site.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select **Cloud Management Gateway**.

1. Select **Create Cloud Management Gateway** in the ribbon.

1. On the **General** page of the wizard, first specify the **Azure environment** for this CMG:

    - **AzurePublicCloud**: Create the service in the global Azure cloud.
    - **AzureUSGovernmentCloud**: Create the service in the Azure US Government cloud.

1. Next choose how you want to deploy the CMG in Azure:

    > [!NOTE]
    > In version 2006 and earlier, you don't have this choice. All deployments use the **cloud service (classic)** method.

    - **Virtual machine scale set**: Starting in version 2010, you have to enable this pre-release feature to see it. It's currently intended for customers with a Cloud Solution Provider (CSP) subscription. If you already deployed a CMG with the **cloud service (classic)** method, this option is unavailable. For more information, see [Topology design: Virtual machine scale sets](plan-cloud-management-gateway.md#virtual-machine-scale-sets).

    - **Cloud service (classic)**: In version 2010, most customers should use this deployment method.

1. Select **Sign in**. Authenticate with an Azure **Subscription Owner** account. The wizard automatically populates the remaining fields from the information stored during the Azure AD integration prerequisite. If you own multiple subscriptions, select the **Subscription ID** of the subscription you want to use.

    Select **Next**, and wait as the site tests the connection to Azure.

1. On the **Settings** page of the wizard, first **Browse** to the .PFX file for the CMG server authentication certificate. The common name from this certificate is used to populate the **Service name** and **Deployment name** fields.

    If you use a wildcard certificate, replace the asterisk (`*`) in the **Service name** field with the globally unique deployment name prefix for your CMG.<!--491233-->

    1. Optionally specify a **Description** to further identify this CMG in the Configuration Manager console.

    1. Select an Azure **Region** for this CMG. The list of available regions may vary based on the selected subscription.

    1. Select a **Resource Group** option:

        - If you choose **Use existing**, then select an existing resource group from the list. This resource group needs to already exist in the same region you selected for the CMG. If you select an existing resource group, and it's in a different region than the previously selected region, the CMG will fail to deploy.

        - If you choose **Create new**, then enter the new resource group name.

    1. In the **VM Instance** field, enter the number of VMs for this service. The default is one, but you can scale up to 16 VMs per CMG.

    1. If you're using client authentication certificates, select **Certificates** to add trusted root certificates. Add all of the certificates in the trust chain.

        > [!NOTE]
        > A trusted root certificate isn't required when using Azure Active Directory (Azure AD) or site-issued tokens for client authentication.

    1. By default, the wizard enables the option to **Verify Client Certificate Revocation**. A certificate revocation list (CRL) must be publicly published for this verification to work. For more information, see [Publish the certificate revocation list](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).

    1. **Enforce TLS 1.2**: Enable this option to require the Azure cloud service VM to use the TLS 1.2 encryption protocol. It doesn't apply to any on-premises Configuration Manager site servers or clients. For more information on TLS 1.2, see [How to enable TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).<!-- SCCMDocs-pr#4021 -->

    1. By default, the wizard enables the option to **Allow CMG to function as a cloud distribution point and serve content from Azure storage**. A CMG can also serve content to clients. This functionality reduces the required certificates and cost of Azure VMs. When you enable this option, you don't need to also deploy a cloud distribution point.

1. Next is the **Alerts** page of the wizard. To monitor CMG traffic with a 14-day threshold, enable the threshold alert. Then specify the threshold, and the percentage at which to raise the different alert levels. Choose **Next** when you're done.

1. Review the settings, and complete the wizard.

Configuration Manager starts to set up the service. After you close the wizard, it takes 5 to 15 minutes to completely provision the service in Azure. To determine when the service is ready, view the **Status** column for the new CMG.

> [!NOTE]
> To troubleshoot CMG deployments, use **CloudMgr.log** and **CMGSetup.log**. For more information, see [Log files](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).

> [!TIP]
> Starting in version 2010, you can also use the PowerShell cmdlet **New-CMCloudManagementGateway** for this process.<!--6978300--> Optionally use this cmdlet to create the CMG service. While it was available in earlier versions, version 2010 includes significant improvements to this cmdlet. For more information, see [New-CMCloudManagementGateway](/powershell/module/configurationmanager/New-CMCloudManagementGateway).

## Configure primary site for client certificate authentication

If you're using [client authentication certificates](configure-authentication.md#pki-certificate) for clients to authenticate with the CMG, follow this procedure to configure each primary site.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select **Sites**.

1. Select the primary site to which your internet-based clients are assigned, and choose **Properties**.

1. Switch to the **Communication Security** tab, and select **Use PKI client certificate (client authentication) when available**.

1. If you don't publish a CRL, disable the following option: **Clients check the certificate revocation list (CRL) for site systems**.

## Add the CMG connection point

The CMG connection point is the site system role that's required for communication from your on-premises Configuration Manager deployment to the cloud-based CMG. To add the CMG connection point, the following steps summarize the instructions to [install site system roles](../../../servers/deploy/configure/install-site-system-roles.md):

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

    Depending upon your CMG design and Configuration Manager version, you may need to enable the **HTTPS** option. For more information, see [Enable management point for HTTPS](configure-authentication.md#bkmk_mphttps).

1. Select **OK** to close the management point properties window.

Repeat these steps for additional management points as needed, and for any software update points.

## Configure boundary groups

<!--3640932-->
You can associate a CMG with a boundary group. This configuration allows clients to use the CMG for client communication according to boundary group relationships. This configuration is beneficial for VPN or branch office clients where it might be better to manage them via a CMG than over the VPN or WAN connection.

For more information on boundary groups, see [Configure boundary groups](../../../servers/deploy/configure/boundary-groups.md).

When you [create or configure a boundary group](../../../servers/deploy/configure/boundary-group-procedures.md), on the **References** tab, add a cloud management gateway. This action associates the CMG with this boundary group.

## Next steps

Continue your CMG setup by configuring clients for CMG:
  
> [!div class="nextstepaction"]
> [Configure clients for CMG](configure-clients.md)
