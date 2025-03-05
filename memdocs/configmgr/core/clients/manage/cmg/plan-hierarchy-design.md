---
title: CMG hierarchy design
titleSuffix: Configuration Manager
description: Design how to use a cloud management gateway (CMG) in your Configuration Manager hierarchy.
ms.date: 03/11/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: article
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# CMG hierarchy design

*Applies to: Configuration Manager (current branch)*

Whether you have a central administration site (CAS), a standalone primary site, or a small test lab, design the cloud management gateway (CMG) for that environment. This article provides the information to help you decide how to position the CMG in your environment.

Create the CMG at the top-tier site of your hierarchy. If that's a CAS, then create CMG connection points at child primary sites. The cloud service manager component is on the service connection point, which is also on the CAS. This design can share the service across different primary sites if needed.

You can create multiple CMG services in Azure, and you can create multiple CMG connection points. Multiple CMG connection points provide load balancing of client traffic from the CMG to the on-premises roles.

Other factors, such as the number of clients to manage, also affect your CMG design. For more information, see [Performance and scale](perf-scale.md).

## Design examples

### Example 1: Standalone primary site

Contoso has a standalone primary site in an on-premises datacenter at their headquarters in New York City.

- They create a CMG in the East US Azure region to reduce network latency.
- They create two CMG connection points, both linked to the single CMG service.

As clients roam onto the internet, they communicate with the CMG in the East US Azure region. The CMG forwards this communication through both of the CMG connection points.

### Example 2: Hierarchy

Fourth Coffee has a CAS in an on-premises datacenter at their headquarters in Seattle. One primary site is in the same datacenter, and the other primary site is in their main European office in Paris.

- On the CAS, they create a CMG service in the West US Azure region. They scale the number of VMs for the expected load of roaming clients in the entire hierarchy.
- On the Seattle-based primary site, they create a CMG connection point linked to the single CMG.
- On the Paris-based primary site, they create a CMG connection point linked to the single CMG.

As clients roam onto the internet, they communicate with the CMG in the West US Azure region. The CMG forwards this communication to the CMG connection point in the client's assigned primary site.

> [!TIP]
> You don't need to deploy more than one CMG for the purposes of geolocation. The Configuration Manager client is mostly unaffected by the slight latency that can occur with the cloud service, even when geographically distant.

## Multiple environments
<!-- SCCMDocs#1225 -->
Many organizations have separate environments for production, test, development, or quality assurance. When you plan your CMG deployment, consider the following questions:

- How many Microsoft Entra tenants does your organization have?
  - Is there a separate tenant for testing?
  - Are user and device identities in the same tenant?

- How many subscriptions are in each tenant?
  - Are there subscriptions that are specific for testing?

Configuration Manager's Azure service for **Cloud management** supports multiple tenants. Multiple Configuration Manager sites can connect to the same tenant. A single site can deploy multiple CMG services into different subscriptions. Multiple sites can deploy CMG services into the same subscription. Configuration Manager provides flexibility depending upon your environment and business requirements.

For more information, see the following FAQ: [Do the user accounts have to be in the same Microsoft Entra tenant as the tenant associated with the subscription that hosts the CMG cloud service?](./cloud-management-gateway-faq.yml#do-the-user-accounts-have-to-be-in-the-same-microsoft-entra-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service-)

## Boundary groups

You can associate a CMG with a boundary group. This configuration allows clients to default or fall back to the CMG for client communication according to [boundary group relationships](../../../servers/deploy/configure/boundary-groups.md). This behavior is especially useful in branch office and VPN scenarios. You can direct client traffic away from expensive and slow WAN links to instead use faster services in Microsoft Azure.<!--3640932-->

Intranet clients can access a CMG-enabled software update point when it's assigned to a boundary group. For more information, see [Configure boundary groups](../../../servers/deploy/configure/boundary-groups-software-update-points.md#intranet-clients-can-use-a-cmg-software-update-point).<!--7102873-->

Internet-based clients don't rely on boundary groups. They only use internet-facing or cloud content sources. If you're only using content-enabled CMGs for these types of clients, then you don't need to include them in boundary groups.

If you want clients on your internal network to get content from a CMG, then it needs to be in the same boundary group as the clients. By default, clients prioritize cloud-based sources last in their list of content sources. This behavior is because there's a cost associated with downloading content from Azure. Cloud-based sources are typically used as a fallback source for intranet-based clients. If you want a cloud-first design, then design your boundary groups to meet this business requirement. For more information, see [Configure boundary groups](../../../servers/deploy/configure/boundary-groups.md). For more information on content location priority and when intranet-based clients use a cloud-based content source, see [Content source priority](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority).

Even though you install the CMG in a specific region of Azure, clients aren't aware of the Azure regions. They randomly select an available CMG as a content source. If you have CMGs in multiple regions, and a client receives more than one in the content location list, it may not download content from the same Azure region.

## Next steps

Next, review the features and configurations that the CMG supports:
  
> [!div class="nextstepaction"]
> [Supported configurations for CMG](supported-configurations.md)
