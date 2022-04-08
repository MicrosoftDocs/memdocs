---
title: Installation scenarios
titleSuffix: Configuration Manager
description: Learn techniques for installing a new Configuration Manager hierarchy when you update or upgrade a site.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Scenarios to streamline your installation of Configuration Manager

*Applies to: Configuration Manager (current branch)*

With the release of update versions for Configuration Manager current branch, there are new scenarios to streamline the install of a new hierarchy to an update version. You can also use these techniques to upgrade from Microsoft System Center 2012 Configuration Manager.

The following list is a summary of the two main scenarios:

- [Install a new Configuration Manager current branch hierarchy that runs an update version](#install-a-new-hierarchy-to-an-update-version).

  - Install only the top-tier site with a baseline version. Then immediately install an update to bring that site current with the update version that you'll use. Then install others sites directly to that update version.
  - This process skips the installation of other sites to a baseline level, and then updating them to the update version that you want to use.
  - The process also skips the installation of clients to a baseline version, and then reinstalling them when you update to a later version.

- [Upgrade a Microsoft System Center 2012 Configuration Manager infrastructure to an update version of Configuration Manager](#upgrade-to-current-branch).

  - Manually upgrade your central administration site (CAS) and each primary site to a baseline version before you install an update version.
  - Don't upgrade secondary sites from Microsoft System Center 2012 Configuration Manager until your primary sites run the update version that you'll use.
  - Don't upgrade clients from Microsoft System Center 2012 Configuration Manager until your primary sites run the update version that you'll use.

## Install a new hierarchy to an update version

1. Install a top-level site for your new hierarchy by using the baseline media. You can use baseline media only to install the first site of a new hierarchy. For more information, see [Use the Setup Wizard to install sites](use-the-setup-wizard-to-install-sites.md).

    After this step, your top-level site runs the baseline version.

1. Use in-console updates to update your top-level site to a later version. Before you install any child sites or clients, update your top-level site to the update version that you plan to use. For more information, see [Updates for Configuration Manager](../../manage/updates.md).

    After this step, your top-level site runs the updated version.

1. If you intend for the first site to be a CAS, next install new child primary sites. Use the installation media from the CD.Latest folder on the CAS server to install child primary sites. Use this source media to make sure that new child primary sites match the version of the CAS. For more information, see [The CD.Latest folder for Configuration Manager](../../manage/the-cd.latest-folder.md).

1. Add other site system roles on remote servers at the CAS and primary sites. This action makes sure that the site systems run the updated version. For more information, see [Install site system roles](../configure/install-site-system-roles.md).

1. If you plan to have secondary sites, at each primary site, use the in-console option to install new secondary sites. Because you didn't install secondary sites while primary sites were at the baseline version, you don't need to update the secondary sites. Instead, you install new secondary sites that run the updated version. For more information, see [Install a secondary site](setup-wizard-secondary.md).

1. Install new clients at the primary site. Because you didn't install clients while primary sites were at the baseline version, you don't need to update clients. Instead, install new clients that run the updated version. For more information, see [Deploy clients](../../../clients/deploy/deploy-clients-to-windows-computers.md).

1. Install new consoles on remote computers. Because you didn't install consoles while primary sites were at the baseline version, you don't need to update consoles. Install them with the updated version. For more information, see [Install consoles](install-consoles.md).

## Upgrade to current branch

1. Upgrade your top-level System Center 2012 Configuration Manager site to a baseline version of the current branch. Use source media for Configuration Manager current branch. You always upgrade the top-level site of a hierarchy first, and then upgrade child sites. For more information, see [Upgrade to Configuration Manager](upgrade-to-configuration-manager.md).

    After this step, your top-level site runs the baseline version.

1. Upgrade each child primary site in your hierarchy to the same baseline version. When you upgrade from Microsoft System Center 2012 Configuration Manager, manually upgrade each primary site to a baseline version of the current branch. Don't upgrade secondary sites yet.

    After this step, each primary site runs the baseline version.

1. Set service windows on child-primary sites. After you upgrade all of your primary sites to the baseline version, configure maintenance windows to control when those sites install infrastructure updates. For more information, see [Service windows for site servers](../../manage/service-windows.md).

    - Child primary sites automatically install the same updates that you install at a CAS.
    - Secondary sties don't automatically install new versions. Update them manually from the console.

    After this step, child primary sites are ready to install updates during their service window.

1. Install the update version at your top-level site. This action updates your top-level site to the updated version. After a CAS installs the update version, each child primary site automatically installs the same update during its service window. For more information, see [Updates for Configuration Manager](../../manage/updates.md).

    After this step, your CAS and each primary site run the updated version.

1. Upgrade secondary sites. After a primary site installs the update, use the in-console option to update secondary sites. This action upgrades secondary sites directly from System Center 2012 Configuration Manager to the same update version as the primary site. For more information about upgrading a secondary site, see [Upgrade sites](upgrade-to-configuration-manager.md#upgrade-sites).

1. Upgrade clients. This process upgrades clients directly from System Center 2012 Configuration Manager to the update version that you installed at the primary site. For more information, see [How to upgrade clients for Windows computers](../../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

    After this step, run the updated version.

1. Upgrade consoles on remote computers. This process upgrades clients directly from System Center 2012 Configuration Manager to the update version that you installed at the primary site. For more information, see [Install consoles](install-consoles.md).

## Next steps

[Configure sites and hierarchies](../configure/configure-sites-and-hierarchies.md)
