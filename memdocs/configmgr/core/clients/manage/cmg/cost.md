---
title: Cost of CMG
titleSuffix: Configuration Manager
description: Understand the costs of operating the cloud management gateway (CMG) service in Microsoft Azure.
ms.date: 07/16/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Cost of CMG

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

- In version 2103 and earlier, CMG uses a Standard A2_v2 VM. The VM size isn't configurable.

- In version 2107 and later, you can configure the VM size, which will affect this cost.<!-- 3555749 -->

  - Lab (B2s)
  - Standard (A2_v2)
  - Large (A4_v2)

  > [!IMPORTANT]
  > The **Lab (B2s)** size VM is only intended for lab testing and small proof-of-concept environments. They aren't intended for production use with the CMG. The B2s VMs are low cost and low performing.

- You select how many VM instances support the CMG. One is the default, and 16 is the maximum. This number is set when you create the CMG, but you can change it afterwards to scale the service as needed.

- For more information on how many VMs you need to support your clients, see [CMG performance and scale](perf-scale.md).

## Virtual machine scale set

<!--3601040-->
If you deploy the CMG with a [virtual machine scale set](plan-cloud-management-gateway.md#virtual-machine-scale-sets) in Azure. When estimating cost, this deployment method replaces the [virtual machine](#virtual-machine). The specific details are otherwise the same, including the VM size. The cost difference between a virtual machine and a virtual machine scale set should be negligible, but may vary by Azure region.

## Outbound data transfer

- Charges are based on data flowing out of Azure, otherwise referred to as egress or download.

- CMG data flows out of Azure include policy to the client, client notifications, and client responses that the CMG forwards to the site. These responses include inventory reports, status messages, and compliance status.

- Even without any clients communicating with a CMG, some background communication causes network traffic between the CMG and the on-premises site.

- View the **Outbound data transfer (GB)** in the Configuration Manager console. For more information, see [Monitor clients on CMG](monitor-clients-cloud-management-gateway.md).

- *For estimating purposes only*, expect approximately 100-300 MB per client per month for internet-based clients. The lower estimate is for a default client configuration. The upper estimate is for a more aggressive client configuration. Your actual usage may vary depending upon how you configure client settings.

    > [!NOTE]
    > Other administrative actions can increase the amount of outbound data transfer from Azure. For example, deployments for software updates or applications.

- Internet-based clients get Microsoft software update content from Windows Update at no charge. Don't distribute update packages with Microsoft update content to a content-enabled CMG. If you do distribute software update packages to your cloud content sources, you may incur storage and data egress costs.

- Misconfiguration of the CMG option to **Verify client certificate revocation** can cause additional traffic from clients to the CMG. This additional traffic can increase the Azure egress data, which can increase your Azure costs.<!-- SCCMDocs#1434 --> For more information, see [Publish the certificate revocation list](security-and-privacy-for-cloud-management-gateway.md#publish-the-certificate-revocation-list).

> [!TIP]
> Any data flows into Azure are free. These flows are otherwise referred to as ingress or upload. When you distribute content from the site to the content-enabled CMG, you're uploading the content to Azure.

## Content storage

- Internet-based clients get Microsoft software update content from Windows Update at no charge. Don't distribute update packages with Microsoft update content to a content-enabled CMG. If you do distribute software update packages to your cloud content sources, you may incur storage and data egress costs.

> [!NOTE]
> The cloud-based distribution point (CDP) is deprecated. Starting in version 2107, you can't create new CDP instances. To provide content to internet-based devices, enable the CMG to distribute content.<!-- 10247883 -->

- CMG uses Azure locally redundant storage (LRS). For more information, see [Locally redundant storage](/azure/storage/common/storage-redundancy-lrs).

- For any other necessary content, distribute it to a content-enabled CMG. This other content includes applications or third-party software updates.

  > [!NOTE]
  > If you enable the client setting to [Download delta content when available](../../deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available), the content for third-party updates won't download to clients.<!--6598587-->

## Other costs

Each cloud service has a dynamic IP address. Each distinct CMG uses a new dynamic IP address. Adding additional VMs per CMG doesn't increase these addresses.

If you get a CMG server authentication certificate from a public provider, there's generally a cost associated with this certificate. For more information, see [CMG server authentication certificate](server-auth-cert.md).

## Control and monitor

Configuration Manager includes the following options to help control costs and monitor data access:

- Control and monitor the amount of content that you store in a cloud service.

- Configure Configuration Manager to alert you when thresholds for client downloads meet or exceed monthly limits.

For more information, see [Monitor CMG](monitor-clients-cloud-management-gateway.md).

To help reduce the number of data transfers from cloud-based sources by clients, use one of the following peer caching technologies:

- Configuration Manager peer cache
- Windows BranchCache
- Windows 10 Delivery Optimization  

For more information, see [Fundamental concepts for content management](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).

## Next steps

Now that you have your CMG design, understand the supported configurations and cost, you're ready to set up the CMG:
  
> [!div class="nextstepaction"]
> [Set up checklist for cloud management gateway](set-up-checklist.md)
