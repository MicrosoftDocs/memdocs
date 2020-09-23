---
title: Modify a cloud management gateway
titleSuffix: Configuration Manager
description: If you need to change the configuration, you can modify the cloud management gateway (CMG).
ms.date: 09/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
ms.assetid: aded6f2c-b47a-4615-bf6c-1b5d8f77c6bd
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Modify a cloud management gateway

*Applies to: Configuration Manager (current branch)*

If you need to change the configuration, you can modify the cloud management gateway (CMG).

## Configure properties

After you create a CMG, you can modify some of its settings. Select the CMG in the Configuration Manager console and select **Properties**. Configure settings on the following tabs:

### Settings tab

- **Certificate file**: Change the server authentication certificate for the CMG. This option is useful when you renew the certificate before it expires. When you get a new certificate, make sure its common name is the same.

  > [!NOTE]
  > When you renew the server authentication certificate for the CMG, the FQDN that you specify for the certificate's common name (CN) is case-sensitive. For example, if the CN of the current certificate is `https://granitefalls.contoso.com`, create the new certificate with the same lowercase CN. The wizard won't accept a certificate with the CN `https://GRANITEFALLS.CONTOSO.COM`.

- **VM Instance**: change the number of virtual machines that the service uses in Azure. This setting allows you to dynamically scale the service up or down based on usage or cost considerations.

- **Certificates**: add or remove trusted root or intermediate CA certificates. This option is useful when adding new CAs, or retiring expired certificates.

- **Verify Client Certificate Revocation**: If you didn't originally enable this setting when you created the CMG, you can enable it afterwards after you publish the CRL. For more information, see [Publish the certificate revocation list](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).

- **Enforce TLS 1.2**: Require the CMG to use the TLS 1.2 encryption protocol. For more information on TLS 1.2, see [How to enable TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).

- **Allow CMG to function as a cloud distribution point and serve content from Azure storage**: The CMG enables this option by default. A CMG can also serve content to clients. This functionality reduces the required certificates and cost of Azure VMs.<!--1358651-->

### Alerts tab

Reconfigure the alerts at any time after you create the CMG. For more information, see [Monitor the CMG: Set up outbound traffic alerts](monitor-clients-cloud-management-gateway.md#set-up-outbound-traffic-alerts).

### Content tab

View the packages that are assigned to the cloud storage account for this CMG. See how much space each package uses in the storage account. When you select a package, you can redistribute or remove the content files.

To verify that the content files for a package are available on the content-enabled CMG, go to the **Content Status** node in the **Monitoring** workspace. For more information, see [Monitor content you distribute](../../../servers/deploy/configure/monitor-content-you-have-distributed.md).

## Redeploy the service

More significant changes, such as the following configurations, require that you redeploy the service:

- Subscription
- Service name
- Region
- Resource group

Always keep at least one active CMG for internet-based clients to receive updated policy. Internet-based clients can't communicate with a removed CMG. Clients don't know about a new one until they refresh policy. When you create a second CMG instance to delete the first, also create another CMG connection point.

Clients refresh policy by default every 24 hours. Before you delete the old CMG, wait at least one day after you create a new one. If clients are turned off or without an internet connection, you may need to wait longer.

If you have an existing CMG from Configuration Manager version 1810 or earlier, it uses the Azure Service Manager deployment method with an Azure management certificate. Redeploy a new CMG to use the Azure Resource Manager deployment method.<!--509753-->

The process to redeploy the service depends upon your service name and whether you want to reuse it.

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

## Determine deployment model

To determine the current deployment model of a CMG:<!--SCCMDocs issue #611-->

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Management Gateway** node.  

1. Select the CMG instance.  

1. In the Details pane at the bottom of the window, look for the **Deployment Model** attribute. For a Resource Manager deployment, this attribute is **Azure Resource Manager**. The legacy deployment model with the Azure management certificate displays as **Azure Service Manager**.

You can also add the **Deployment Model** attribute as a column to the list view.  

## Modifications in the Azure portal

Only modify the CMG from the Configuration Manager console. Making modifications to the service or underlying VMs directly in Azure isn't supported. Any changes may be lost without notice. As with any platform as a service (PaaS), the service can rebuild the VMs at any time. These rebuilds can happen for backend hardware maintenance, or to apply updates to the VM OS.

## Delete the service

If you need to delete the CMG, only do it from the Configuration Manager console. Manually removing any components in Azure causes the system to be inconsistent. This state leaves orphaned information, and unexpected behaviors may occur.
