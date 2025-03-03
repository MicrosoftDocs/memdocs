---
title: Prerequisites to deploy user-available apps
titleSuffix: Configuration Manager
description: When you deploy apps as Available to user collections, there are other requirements for some types of clients.
ms.date: 04/08/2022
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: install-set-up-deploy
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Prerequisites to deploy user-available apps

*Applies to: Configuration Manager (current branch)*

When you deploy applications as **Available** to user collections, then users can browse Software Center and install the apps they need.

For on-premises domain-joined clients, Software Center uses the user's domain credentials to get the list of available applications from the management point.

There are other requirements for clients that are internet-based, joined to Microsoft Entra ID, or both.

<a name='azure-ad-joined-devices'></a>

## Microsoft Entra joined devices
<!-- 1322613 -->

If you deploy applications as available to users, they can browse and install them through Software Center on Microsoft Entra devices. Configure the following prerequisites to enable this scenario:

- Enable HTTPS on the management point or enable Enhanced HTTP on the site.<!-- memdocs#1761 -->

- Integrate the site with [Microsoft Entra ID](../../core/servers/deploy/configure/azure-services-wizard.md) for **Cloud Management**.

  - Configure [Microsoft Entra user Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc).

- Deploy an application as available to a collection of users from Microsoft Entra ID.

- Enable the client setting **Use new Software Center** in the [Computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent) group.

- The client OS must be Windows 10 or later, and joined to Microsoft Entra ID. Either as purely cloud domain-joined, or Microsoft Entra hybrid joined.

- To support internet-based clients:

  - Deploy a [cloud management gateway](../../core/clients/manage/cmg/overview.md) (CMG).

  - Distribute any application content to a content-enabled CMG.

  - Enable the client setting: **Enable user policy requests from Internet clients** in the [Client Policy](../../core/clients/deploy/about-client-settings.md#client-policy) group.

- To support clients on the intranet:

  - Add the content-enabled CMG to a boundary group used by the clients.

  - Clients must resolve the fully qualified domain name (FQDN) of the management point.

  > [!NOTE]
  > For a client detected as on the intranet, but communicating via the cloud management gateway (CMG), it uses Microsoft Entra identity for devices joined to Microsoft Entra ID. These devices can be cloud-joined or hybrid-joined.<!--6935376-->

## Internet-based domain-joined devices

<!--7033501-->

An internet-based, domain-joined device that isn't joined to Microsoft Entra ID and communicates via a cloud management gateway (CMG) can get apps deployed as available. The Active Directory domain user of the device needs a matching Microsoft Entra identity. When the user starts Software Center, Windows prompts them to enter their Microsoft Entra credentials. They can then see any available apps.

Configure the following prerequisites to enable this functionality:

- Windows 10 or later device, and:

  - Joined to your on-premises Active Directory domain.

  - Can communicate via [CMG](../../core/clients/manage/cmg/plan-cloud-management-gateway.md).

- The site has discovered the user by _both_ [Active Directory](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) and [Microsoft Entra user discovery](../../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc).

> [!NOTE]
> If you apply a [software restriction policy](/windows-server/identity/software-restriction-policies/administer-software-restriction-policies) to the device, it can block the authentication prompt in Windows. Review any domain or local group policies that you apply to the device. Then remove any that might interfere with this Software Center behavior.

## Next steps

[Deploy applications](../deploy-use/deploy-applications.md)
