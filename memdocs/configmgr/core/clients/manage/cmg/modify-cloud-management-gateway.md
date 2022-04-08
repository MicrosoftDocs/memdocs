---
title: Modify a CMG
titleSuffix: Configuration Manager
description: If you need to change the configuration, you can modify the cloud management gateway (CMG).
ms.date: 04/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
ms.collection: highpri
---

# Modify a CMG

*Applies to: Configuration Manager (current branch)*

If you need to change the configuration, you can modify the cloud management gateway (CMG).

## Configure properties

After you create a CMG, you can modify some of its settings. Select the CMG in the Configuration Manager console and select **Properties**. Configure settings on the following tabs:

### Settings tab

- **Certificate file**: Change the server authentication certificate for the CMG. This option is useful when you renew the certificate before it expires. When you get a new certificate, make sure its common name is the same.

  > [!NOTE]
  > When you renew the server authentication certificate for the CMG, the FQDN that you specify for the certificate's common name (CN) is case-sensitive. For example, if the CN of the current certificate is `granitefalls.contoso.com`, create the new certificate with the same lowercase CN. The wizard won't accept a certificate with the CN `GRANITEFALLS.CONTOSO.COM`.
  >
  > If you make significant changes to the certificate, you may need to [Redeploy the service](#redeploy-the-service). For example, changing the organization name on the certificate.<!-- memdocs#1927 -->

- **Description**: Specify an optional description to further identify this CMG in the Configuration Manager console.

- **VM Instance**: Change the number of virtual machines that the service uses in Azure. This setting allows you to dynamically scale the service up or down based on usage or cost considerations.

- **Certificates**: Add or remove trusted root or intermediate CA certificates. This option is useful when adding new CAs, or retiring expired certificates.

- **Verify Client Certificate Revocation**: If you didn't originally enable this setting when you created the CMG, you can enable it afterwards after you publish the CRL. For more information, see [Publish the certificate revocation list](security-and-privacy-for-cloud-management-gateway.md#publish-the-certificate-revocation-list).

- **Enforce TLS 1.2**: The CMG enables this option by default. Require it to use the TLS 1.2 encryption protocol. Starting in version 2107 with the [update rollup](../../../../hotfix/2107/11121541.md), this setting also applies to the CMG storage account.<!--10800237--> For more information, see [How to enable TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).

- **Allow CMG to function as a cloud distribution point and serve content from Azure storage**: The CMG enables this option by default. If you plan on targeting deployments with content to clients, you need to configure the CMG to serve content.<!--1358651-->

### Alerts tab

Reconfigure the alerts at any time after you create the CMG. For more information, see [Monitor the CMG: Set up outbound traffic alerts](monitor-clients-cloud-management-gateway.md#set-up-outbound-traffic-alerts).

### Content tab

View the packages that are assigned to the cloud storage account for this CMG. See how much space each package uses in the storage account. When you select a package, you can redistribute or remove the content files.

To verify that the content files for a package are available on the content-enabled CMG, go to the **Content Status** node in the **Monitoring** workspace. For more information, see [Monitor content you distribute](../../../servers/deploy/configure/monitor-content-you-have-distributed.md).

## Convert

> [!NOTE]
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](../../../servers/manage/optional-features.md).

<!--8959690-->

Starting in version 2107, if you have a CMG that uses the classic cloud service, convert it to use a virtual machine scale set.

> [!TIP]
> This process reuses the underlying storage account.

When you convert a CMG, you can't change all settings:

| Setting | Convert |
|---------|---------|
| VM size | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| VM instances | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Verify CRL | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Require TLS | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Serve content | :::image type="content" source="media/green-check.png" border="false" alt-text="Supported."::: |
| Azure environment | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Subscription | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Azure AD app | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Region | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |
| Resource group | :::image type="content" source="media/red-x.png" border="false" alt-text="Not supported."::: |

To make changes that the conversion process doesn't support, you need to [Redeploy the service](#redeploy-the-service).

> [!IMPORTANT]
> If your CMG's _service name_ is in the `cloudapp.net` domain, you can't convert it to a virtual machine scale set. For example, you issued a server authentication certificate from your internal PKI with a common name of `GraniteFalls.cloudapp.net`. Since Microsoft owns the `cloudapp.net` domain, you can't create a DNS CNAME to map this service name to the new deployment name in the `cloudapp.azure.com` domain.<!-- 10362079 -->
>
> 1. Issue a new server authentication certificate from your internal PKI with a new service name. Consider using your domain name instead of a Microsoft domain. For more information, see [Use an enterprise PKI certificate](server-auth-cert.md#use-an-enterprise-pki-certificate).
> 1. Deploy a new CMG as a virtual machine scale set with the new certificate.
> 1. Once clients refresh policy to get this new CMG, delete the old CMG.
>
> For more information, see [Replace a CMG with a new service name](#replace-a-cmg-with-a-new-service-name).

### Process to convert a CMG to a virtual machine scale set

> [!IMPORTANT]
> First review the prerequisites for [virtual machine scale sets](plan-cloud-management-gateway.md#virtual-machine-scale-sets). For example, make sure that you register the necessary [Azure resource providers](configure-azure-ad.md#configure-azure-resource-providers) in the subscription.<!-- memdocs#2434 -->

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Management Gateway** node.

1. Select a CMG instance whose **Status** is _Ready_. In the ribbon, select **Convert**. This action opens the Convert CMG wizard.

1. On the General page, select **Next**. You can't change any of these settings.

1. On the Settings page, note the new _Deployment name_ with the suffix for the virtual machine scale set.

1. Make other configuration changes as needed. Then select **Next** and complete the wizard.

Monitor the conversion process the same as a new deployment. For example, view the state in the console, and review **cloudmgr.log**. For more information, see [Monitor CMG](monitor-clients-cloud-management-gateway.md#monitor-logs).

### Update or create a DNS CNAME

Since the deployment name changed, you need to update or create a DNS canonical name record (CNAME). This alias maps the service name to the deployment name. For more information, see [Create a DNS CNAME alias](server-auth-cert.md#create-a-dns-cname-alias).

For example:

- The CMG's _service name_ is `GraniteFalls.contoso.com`.

- For the _deployment name_:

  - Classic: `GraniteFalls.cloudapp.net`

  - Virtual machine scale set: `GraniteFalls.EastUS.CloudApp.Azure.Com`

## Redeploy the service

More significant changes, such as the following configurations, require that you redeploy the service:

- Subscription
- Service name
- Region
- Resource group
- Significant changes to the server authentication certificate

Always keep at least one active CMG for internet-based clients to receive updated policy. Internet-based clients can't communicate with a removed CMG. Clients don't know about a new one until they refresh policy. When you create a second CMG instance to delete the first, also create another CMG connection point.

Clients refresh policy by default every 24 hours. Before you delete the old CMG, wait at least one day after you create a new one. If clients are turned off or without an internet connection, you may need to wait longer.

If you have an existing CMG from version 1810 or earlier, it uses the Azure Service Manager deployment method. This method used an Azure management certificate. This method is deprecated, and support will be removed in a later version of Configuration Manager. Redeploy a new CMG to use the Azure Resource Manager deployment method.<!--509753-->

The process to redeploy the service depends upon your service name and whether you want to reuse it.

> [!NOTE]
> In version 2107 and later, you can have multiple CMGs that use different deployment methods. You can also convert a **cloud service (classic)** CMG to a **virtual machine scale set**. For more information, see [Convert](#convert).
>
> In versions 2010 and 2103, if you already deployed a CMG with the **cloud service (classic)** method, you can't deploy another CMG as a **virtual machine scale set**, and vice versa. First [delete the existing CMG](#delete-the-service), and then create a new one with the other deployment method. All CMG instances for the site need to use the same deployment method. For more information, see [Plan for CMG: Virtual machine scale sets](plan-cloud-management-gateway.md#virtual-machine-scale-sets).

### Replace a CMG and reuse the same service name

<!--
You can reuse the same service name and CMG server authentication certificate, but the process depends upon the service name.

- If you issue the CMG server authentication certificate for your own domain name (`GraniteFalls.contoso.com`):

    1. Create a new CMG with the same CMG server authentication certificate.

    1. When you're ready to switch the service:

        1. Update the CNAME record in DNS to use the new deployment name. For example, change the CNAME mapping for `GraniteFalls.contoso.com` to `GraniteFalls.EastUS.CloudApp.Azure.Com`.

        1. Reconfigure the CMG connection point to use the new CMG.

        1. Delete the old CMG.

- If you issue the CMG server authentication certification from your PKI for `cloudapp.net`:
 -->

> [!IMPORTANT]
> This process assumes that you already have at least two CMG services, and are replacing one of them at a time. You need to have at least one active CMG for internet-based clients.

1. Delete the old CMG.

1. Create a new CMG with the same server authentication certificate.

1. Reconfigure the CMG connection point to use the new CMG.

### Replace a CMG with a new service name

1. Get a new server authentication certificate.

1. Create a new CMG.

1. Create a new CMG connection point and link it with the new CMG.

1. Wait at least one day for internet-based clients to receive policy about the new CMG. If clients are turned off or without an internet connection, you may need to wait longer.

1. Delete the old CMG and associated CMG connection point.

## Stop and start the service

Use the Configuration Manager console to stop and start the service if you need to.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Management Gateway** node.  

1. Select the CMG instance.  

1. In the ribbon, select one of the following actions:

    - To stop a running CMG, select **Stop service**.
    - To start a stopped CMG, select **Start service**.

Configuration Manager can stop a CMG service when the total data transfer goes over your limit. For more information, see [Stop CMG when it exceeds threshold](monitor-clients-cloud-management-gateway.md#stop-cmg-when-it-exceeds-threshold)

> [!IMPORTANT]
> Even if the service isn't running, there are still costs associated with the cloud service. Stopping the service doesn't eliminate all associated Azure costs. To remove all cost for the cloud service, [delete the CMG](#delete-the-service).
>
> When you stop the CMG service, internet-based clients can't communicate with Configuration Manager.

You can also use PowerShell to stop and start a CMG:

- [Start-CMCloudManagementGateway](/powershell/module/configurationmanager/Start-CMCloudManagementGateway)
- [Stop-CMCloudManagementGateway](/powershell/module/configurationmanager/Stop-CMCloudManagementGateway)

## Determine deployment model

To determine the current deployment model of a CMG:<!--SCCMDocs issue #611-->

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Management Gateway** node.  

1. Select the CMG instance.  

1. In the Details pane at the bottom of the window, look for the **Deployment Model** attribute.

    Starting in version 2010, you'll see either **Cloud service (classic)** or **Virtual machine scale set**.

    In version 2006 and earlier, for a Resource Manager deployment, this attribute is **Azure Resource Manager**. The legacy deployment model with the Azure management certificate displays as **Azure Service Manager**.

    > [!IMPORTANT]
    > CMG deployments using Azure Service Manager are deprecated. Support will be removed in a later version of Configuration Manager. Redeploy a new CMG to use the Azure Resource Manager deployment method.

You can also add the **Deployment Model** attribute as a column to the list view.  

## Modifications in the Azure portal

Only modify the CMG from the Configuration Manager console. Making modifications to the service or underlying VMs directly in Azure isn't supported. Any changes may be lost without notice. As with any platform as a service (PaaS), the service can rebuild the VMs at any time. These rebuilds can happen for backend hardware maintenance, or to apply updates to the VM OS.

## Renew Azure service secret key

When you first configure Azure Active Directory (Azure AD) for the CMG to create the **Cloud Management** Azure service, you specify a secret key validity period on the web (server) app registration. By default, the secret key is valid for one year, or you can specify two years. Before the secret key expires, make sure to renew it. For more information, see [Renew secret key](../../../servers/deploy/configure/azure-services-wizard.md#bkmk_renew).<!-- MEMDocs#916 -->

## Delete the service

If you need to delete the CMG, only do it from the Configuration Manager console. Manually removing any components in Azure causes the system to be inconsistent. This state leaves orphaned information, and unexpected behaviors may occur.
