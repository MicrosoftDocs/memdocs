---
title: Setup wizard
titleSuffix: Configuration Manager
description: Use the Configuration Manager setup wizard to install a new site.
ms.date: 03/28/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Use the Setup Wizard to install Configuration Manager sites

*Applies to: Configuration Manager (current branch)*

To install a new Configuration Manager site by using a guided user interface, use the Configuration Manager Setup Wizard (setup.exe). The wizard supports installing a primary site or central administration site (CAS). You also use the wizard to [upgrade an evaluation installation](upgrade-an-evaluation-install-to-a-full-install.md) of Configuration Manager to a fully licensed installation. When you don't want to use the wizard, you can instead use an [installation script](use-a-command-line-to-install-sites.md) and run an unattended command-line installation.

Install a secondary site from within the Configuration Manager console. Secondary sites don't support a scripted command-line installation.

Before you install a site, be familiar with the details in the following articles:

- [Design a hierarchy of sites](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md)
- [Site and site system prerequisites](../../../plan-design/configs/site-and-site-system-prerequisites.md)
- [Prepare to install sites](prepare-to-install-sites.md)
- [Prerequisites for installing sites](prerequisites-for-installing-sites.md)
- Assess server readiness with the [Prerequisite Checker](prerequisite-checker.md)
- [Release notes](release-notes.md)

> [!TIP]
> If you need assistance with site installation, see the [Support options and community resources](../../../understand/find-help.md#support-options-and-community-resources). For example, the Microsoft Q&A forum for [Configuration Manager site and client deployment](/answers/topics/mem-cm-site-deployment.html).

When you're ready to get started, see the following articles for the specific processes:

[Use the setup wizard to install a central administration or primary site](setup-wizard-central-primary.md)

[Use the setup wizard to install a secondary site](setup-wizard-secondary.md)
