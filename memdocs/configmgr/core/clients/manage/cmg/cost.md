---
title: Cost of cloud management gateway
titleSuffix: Configuration Manager
description: Understand the costs of operating the cloud management gateway (CMG) service in Microsoft Azure.
ms.date: 11/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51777075-22b9-4dc7-b206-7f2b6184039a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Cost of cloud management gateway

*Applies to: Configuration Manager (current branch)*

The cloud management gateway (CMG) in Configuration Manager uses several components in Microsoft Azure. These components incur charges to the Azure subscription account. Some costs are fixed, but some vary depending upon usage.

> [!IMPORTANT]
> The following cost information is for estimating purposes only. Your environment may have other variables that affect the overall cost of using CMG.

To help determine potential costs, use the following Azure resources:

- [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/)

    > [!NOTE]
    > Virtual machine costs vary by region.

- [Azure bandwidth pricing details](https://azure.microsoft.com/pricing/details/bandwidth/)

    > [!NOTE]
    > Pricing for data transfer is tiered. The more you use, the less you pay per gigabyte.

## Virtual machine

- CMG uses Azure Cloud Services as platform as a service (PaaS). This service uses virtual machines (VMs) that incur compute costs.

- CMG uses a Standard A2 V2 VM. The VM size isn't configurable.

- You select how many VM instances support the CMG. One is the default, and 16 is the maximum. This number is set when you create the CMG, but you can change it afterwards to scale the service as needed.

- For more information on how many VMs you need to support your clients, see [CMG performance and scale](perf-scale.md).

## Virtual machine scale set

<!--3601040-->
Starting in version 2010, customers with a Cloud Solution Provider (CSP) subscription can deploy the CMG with a **virtual machine scale set** in Azure. When estimating cost, this deployment method replaces the [virtual machine](#virtual-machine). The specific details are otherwise the same. For example, it also uses a Standard A2 V2 VM. The cost difference between a virtual machine and a virtual machine scale set should be negligible, but may vary by Azure region.

## Outbound data transfer

- Charges are based on data flowing out of Azure, otherwise referred to as egress or download. Any data flows into Azure are free, which are also known as ingress or upload.

- CMG data flows out of Azure include policy to the client, client notifications, and client responses that the CMG forwards to the site. These responses include inventory reports, status messages, and compliance status.

- Even without any clients communicating with a CMG, some background communication causes network traffic between the CMG and the on-premises site.

- View the **Outbound data transfer (GB)** in the Configuration Manager console. For more information, see [Monitor clients on CMG](monitor-clients-cloud-management-gateway.md).

- *For estimating purposes only*, expect approximately 100-300 MB per client per month for internet-based clients. The lower estimate is for a default client configuration. The upper estimate is for a more aggressive client configuration. Your actual usage may vary depending upon how you configure client settings.

    > [!NOTE]
    > Other administrative actions can increase the amount of outbound data transfer from Azure. For example, deployments for software updates or applications.

- Internet-based clients get Microsoft software update content from Windows Update at no charge. Don't distribute update packages with Microsoft update content to a content-enabled CMG or cloud distribution point. If you do distribute software update packages to your cloud content sources, you may incur storage and data egress costs.

- Misconfiguration of the CMG option to **Verify client certificate revocation** can cause additional traffic from clients to the CMG. This additional traffic can increase the Azure egress data, which can increase your Azure costs.<!-- SCCMDocs#1434 --> For more information, see [Publish the certificate revocation list](security-and-privacy-for-cloud-management-gateway.md#publish-the-certificate-revocation-list).

## Content storage

- Internet-based clients get Microsoft software update content from Windows Update at no charge. Don't distribute update packages with Microsoft update content to a content-enabled CMG or cloud distribution point. If you do distribute software update packages to your cloud content sources, you may incur storage and data egress costs.

- CMG uses Azure locally redundant storage (LRS). For more information, see [Locally redundant storage](/azure/storage/common/storage-redundancy-lrs).

- For any other necessary content, distribute it to a content-enabled CMG or cloud distribution point. This other content includes applications or third-party software updates.

  - When using a CMG for content storage, the content for third-party updates won't download to clients if you enable the client setting to [Download delta content when available](../../deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available).<!--6598587-->

- For more information, see the cost of using [cloud distribution points](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost).

- A CMG can also serve content to clients. This functionality reduces the required certificates and cost of Azure VMs.

## Other costs

Each cloud service has a dynamic IP address. Each distinct CMG uses a new dynamic IP address. Adding additional VMs per CMG doesn't increase these addresses.

If you get a CMG server authentication certificate from a public provider, there's generally a cost associated with this certificate. For more information, see [CMG server authentication certificate](server-auth-cert.md).

## Next steps

Now that you have your CMG design, understand the supported configurations and cost, you're ready to set up the CMG:
  
> [!div class="nextstepaction"]
> [Set up checklist for cloud management gateway](set-up-checklist.md)
