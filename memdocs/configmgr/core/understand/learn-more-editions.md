---
title: Licensing and branches
titleSuffix: Configuration Manager
description: Learn about the licensing requirements for the installation options available with Configuration Manager
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Licensing and branches for Configuration Manager

*Applies to: Configuration Manager (current branch), & System Center Configuration Manager (long-term servicing branch)*

Use this article to learn about the licensing requirements for the installation options available with Configuration Manager. These installation options include the following branches:

- Current branch
- Long-term servicing branch (LTSB)
- Evaluation installation of the current branch
- Technical preview branch

## Licensing overview

Customers with active Software Assurance (SA) on Configuration Manager licenses or with equivalent subscription rights as of October 1, 2016 have rights to use the October 2016 version 1606 release of Configuration Manager. Customers with rights to Configuration Manager on or after October 1, 2016 will find two licensed options upon installation: current branch and long-term servicing branch (LTSB).

For the complete terms and conditions for the products you purchase through Microsoft Volume Licensing programs, see [Licensing Terms and Documentation](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1).


## Licensed branches

This article references the Software Assurance agreement or equivalent subscription rights. This Microsoft licensing agreement grants rights to install and use Configuration Manager.

### Current branch

The current branch requires an active Software Assurance agreement or equivalent rights to Configuration Manager. For more information, see [Software Assurance and the Current Branch](#software-assurance-and-the-current-branch).

This branch is supported for use in production environments that want to receive regular quality and feature updates from Microsoft. It provides access to use all features and improvements.

Beginning with the 1710 release, each update version remains in support for 18 months from its general availability release date. For more information, see [Support for Configuration Manager current branch versions](../servers/manage/current-branch-versions-supported.md).

### Long-term servicing branch (LTSB)

The LTSB requires a current Software Assurance agreement with Microsoft as of October 1, 2016. For more information, see [Software Assurance and the LTSB](#software-assurance-and-the-ltsb).

This branch is supported for use in production environments. It's intended for use by customers that have let their Software Assurance (SA) or equivalent subscriptions rights to Configuration Manager expire after October 1, 2016. This branch is limited when compared to the Current Branch.

Critical security updates for Configuration Manager are made available to this branch but no new features are made available.

### Evaluation installation of the current branch

The evaluation version doesn't require a Software Assurance agreement with Microsoft. [Evaluation installs](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) are always the current branch, and you can use them for 180 days.

You can upgrade the evaluation installation to a full installation of the current branch. You can't upgrade an evaluation installation to the long-term servicing branch.

### Technical preview branch

The [technical preview branch](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) is also available. This branch is a limited build of Configuration Manager that lets you try out new features. You install the technical preview using different media than the licensed versions. For more information, see [Technical Preview](../get-started/technical-preview.md).


## Software Assurance agreements

The status of Software Assurance on your Configuration Manager licenses, or equivalent subscription rights, on or after October 1, 2016, determines the branch you can install and use.

### Software Assurance and the current branch

Rights to use Configuration Manager current branch can be provided by:

- **System Center:** Customers with active SA on System Center Standard or Datacenter licenses can install and use the current branch option of Configuration Manager.

- **System Center Configuration Manager:** Customers with active SA on Configuration Manager licenses, or with equivalent subscription rights, can install and use the current branch option of Configuration Manager.

If you have active SA on Configuration Manager licenses or equivalent subscription rights on or after October 1, 2016:

- You can install and use the current branch.
- If you allow SA or subscription to lapse, you must uninstall the current branch.

### Software Assurance and the LTSB

If you have an active SA on Configuration Manager licenses or equivalent subscription rights on or after October 1, 2016:

- You can install and use the LTSB. Customers who have perpetual rights to Configuration Manager, or who allow their SA or subscription to lapse, can install the version of Configuration Manager LTSB that's current at the time of lapse.

LTSB is based on current branch version 1606, and has the following limitations:

- There's no support to convert a current branch to the LTSB. If you currently have a current branch site, you must install the LTSB as a new site.  

- LTSB doesn't support all the capabilities of the current branch. For more information, see [Introduction to the long-term servicing branch](introduction-to-the-ltsb.md). These limitations include a limited feature set, limited upgrade options, and a separate product support lifecycle.  

### Software Assurance expiration date

Beginning with the October 2016 release of the version 1606 baseline media for Configuration Manager, you can specify the expiration date of your Software Assurance agreement. The **Software Assurance expiration date** is an optional value as a convenient reminder. Add it when you run Configuration Manager setup or later from within the Configuration Manager console.

> [!NOTE]
> Microsoft doesn't validate the expiration date you specify, and doesn't use this date for license validation. Use it as a reminder of your expiration date. This value is useful when Configuration Manager periodically checks for new software updates offered online. Your Software Assurance license status should be current to be eligible to use these additional updates.

#### To specify the Software Assurance expiration date

- When you run Setup from the Configuration Manager media, specify the value on the **Product Key** page of the Setup wizard.

- In the Configuration Manager console, in **Hierarchy Settings**, specify the value on the **Licensing** tab.


## Licensing resources

To learn more about product licensing details, use the following resources.

### Microsoft Volume Licensing Service Center (VLSC)

- [Overview of VLSC](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Microsoft Volume Licensing Product Terms](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)

- Volume license customers can get a summary of their licenses from the [Volume License Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Go to the **Licenses** menu, and select **Licenses Summary**.

### VLSC videos

- For training videos on how VLSC works, go to [Microsoft Volume Licensing Service Center training and resources](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources) and select **How-to videos**.

- [Where to look up your active Software Assurance agreement](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (starting at 43 seconds)  

- [How to get permissions for VLSC](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4). You can delegate VLSC read and write permissions to other people in your organization.

## Next steps

[Frequently asked questions for Configuration Manager branches and licensing](product-and-licensing-faq.yml)
