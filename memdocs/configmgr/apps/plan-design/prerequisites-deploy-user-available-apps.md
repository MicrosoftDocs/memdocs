---
title: Prerequisites to deploy user-available apps
titleSuffix: Configuration Manager
description: When you deploy apps as Available to user collections, there are other requirements for some types of clients.
ms.date: 04/06/2022
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Prerequisites to deploy user-available apps

*Applies to: Configuration Manager (current branch)*

When you deploy applications as **Available** to user collections, then users can browse Software Center and install the apps they need.

For on-premises domain-joined clients, Software Center uses the user's domain credentials to get the list of available applications from the management point.

There are other requirements for clients that are internet-based, joined to Azure Active Directory (Azure AD), or both.

## Azure AD-joined devices
<!-- 1322613 -->

If you deploy applications as available to users, they can browse and install them through Software Center on Azure AD devices. Configure the following prerequisites to enable this scenario:

- Enable HTTPS on the management point or enable Enhanced HTTP on the site.<!-- memdocs#1761 -->

- Integrate the site with [Azure AD](../../core/servers/deploy/configure/azure-services-wizard.md) for **Cloud Management**.

  - Configure [Azure AD User Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc).

- Deploy an application as available to a collection of users from Azure AD.

- Enable the client setting **Use new Software Center** in the [Computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent) group.

- The client OS must be Windows 10 or later, and joined to Azure AD. Either as purely cloud domain-joined, or hybrid Azure AD-joined.

- To support internet-based clients:

  - Deploy a [cloud management gateway](../../core/clients/manage/cmg/overview.md) (CMG).

  - Distribute any application content to a content-enabled CMG.

  - Enable the client setting: **Enable user policy requests from Internet clients** in the [Client Policy](../../core/clients/deploy/about-client-settings.md#client-policy) group.

- To support clients on the intranet:

  - Add the content-enabled CMG to a boundary group used by the clients.

  - Clients must resolve the fully qualified domain name (FQDN) of the management point.

  > [!NOTE]
  > For a client detected as on the intranet, but communicating via the cloud management gateway (CMG), it uses Azure Active Directory (Azure AD) identity for devices joined to Azure AD. These devices can be cloud-joined or hybrid-joined.<!--6935376-->

## Internet-based domain-joined devices

<!--7033501-->

An internet-based, domain-joined device that isn't joined to Azure AD and communicates via a cloud management gateway (CMG) can get apps deployed as available. The Active Directory domain user of the device needs a matching Azure AD identity. When the user starts Software Center, Windows prompts them to enter their Azure AD credentials. They can then see any available apps.

Configure the following prerequisites to enable this functionality:

- Windows 10 or later device, and:

  - Joined to your on-premises Active Directory domain.

  - Can communicate via [CMG](../../core/clients/manage/cmg/plan-cloud-management-gateway.md).

- The site has discovered the user by _both_ [Active Directory](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) and [Azure AD user discovery](../../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc).

> [!NOTE]
> If you apply a [software restriction policy](/windows-server/identity/software-restriction-policies/administer-software-restriction-policies) to the device, it can block the authentication prompt in Windows. Review any domain or local group policies that you apply to the device. Then remove any that might interfere with this Software Center behavior.

## Next steps

[Deploy applications](../deploy-use/deploy-applications.md)
