---
title: MDT release notes
description: Understand supported platforms, prerequisites, and limitations of the Microsoft Deployment Toolkit (MDT).
ms.date: 08/12/2022
ms.prod: configuration-manager
ms.technology: configmgr-mdt
ms.topic: article
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: null
ms.collection: openauth
---

# Microsoft Deployment Toolkit release notes  

This article provides details on the latest release of the Microsoft Deployment Toolkit (MDT). These details include supported platforms, prerequisites, and any limitations. It assumes familiarity with MDT version concepts, features, and capabilities.

## Latest release

**MDT build 8456** is the latest version available on the [Microsoft Download Center](https://aka.ms/mdtdownload).

This update begins support for Windows 10, version 1809, and Windows Server 2019. For more information, see the [supported platforms](#supported-platforms) section.

## Significant changes

Here is a summary of the significant changes in MDT build 8456.

### Supported configuration updates

- Windows ADK for Windows 10, version 1809
- Windows 10, version 1809
- Configuration Manager, version 1810

### Major changes

The following list is a summary of the major changes in this version:

- Nested task sequence support for LTI scenario
- Modern language pack support <sup>[Known issue](known-issues.md#modern-language-pack-support)</sup>
- Support for Configuration Manager version 1810
- IsVM evaluates to False on Parallels VMs
- IsVM = False when VMware VM is configured with EFI boot firmware
- Gather doesn't recognize All-in-One chassis type
- MDT doesn't automatically install BitLocker on Windows Server 2016
- BDEDisablePreProvisioning typo in ZTIGather.xml

## Supported platforms

MDT releases are no longer tagged with year or update version. To align better with the current branches of Windows 10 and Configuration Manager, and to simplify the branding and release process, it's now simply **Microsoft Deployment Toolkit**. The build number is used to distinguish each release. For example, the latest build available for download is 8456.

Unlike Configuration Manager with a predetermined release schedule, MDT only releases as required to support new versions of Windows, the Windows ADK, or Configuration Manager current branch. Any [known issues](known-issues.md) with these components will be documented in this article as necessary.

The following OS versions are supported for deployment with this build of MDT:

- Windows 10, version 1809
- Windows 10, version 1803
- Windows 10, version 1709
- Other [supported versions](/windows/release-information/) of Windows 10
- Windows 8.1
- Windows 7
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2

> [!NOTE]
> MDT doesn't support Windows 10 ARM64 devices, Windows 11 and Windows Server 2022 operating systems.

FAQ: [Is this release only supported with Windows 10, Windows ADK, or Configuration Manager version *X*?](./faq.yml#what-s-the-mdt-support-life-cycle-)

## Prerequisites

MDT requires the following components, which are included in Windows:

- Microsoft .NET Framework 4.0
- Windows PowerShell version 3.0

MDT requires the latest [Windows ADK for Windows 10](/windows-hardware/get-started/adk-install). MDT also requires the **Windows PE add-on** for the Windows ADK.

> [!NOTE]
> Windows recommends using the Windows ADK that matches the version of Windows you're deploying. For example, use the Windows ADK for Windows 10 version 1809 when deploying Windows 10 version 1809. For more information on Windows ADK component supportability, see [DISM supported platforms](/windows-hardware/manufacture/desktop/dism-supported-platforms) and [USMT requirements](/windows/deployment/usmt/usmt-requirements#bkmk-1).

When integrating MDT with Configuration Manager for ZTI and UDI scenarios, use the latest version of Configuration Manager current branch.

## Upgrade MDT

The MDT installation process removes any existing instances of MDT installed on the same computer. Existing deployment shares, distribution points, and databases are preserved during this process. They must be upgraded when the installation is complete.

The current release of MDT supports upgrading from the following versions of MDT:

- MDT build 8450

> [!TIP]
> Create a backup of the existing MDT infrastructure before attempting an upgrade.

### LTI

After installing MDT, upgrade an existing deployment share by running the **Open Deployment Share Wizard** from the Deployment Shares node in the Deployment Workbench. Specify the path to the existing deployment share directory, and then select the **Upgrade** check box. This process also upgrades existing network deployment shares and media deployment shares, so those shares should be accessible. Don't upgrade with active deployments, because in-use files can cause upgrade problems.

### ZTI

Existing MDT task sequences present in Configuration Manager aren't modified during the installation process of MDT. They should continue to work without any issue. No mechanism is provided to upgrade these task sequences. If you want to use any of the new MDT capabilities, create new MDT-integrated task sequences in Configuration Manager.

When the upgrade process is complete:

- Run the **Configure ConfigMgr Integration Wizard** after the upgrade. It registers the new components and installs the updated ZTI task sequence templates.

- Create a new **Microsoft Deployment Toolkit Files** package for any new ZTI task sequences you create. You can use the existing MDT Files package for any ZTI task sequences created before the upgrade. Create a new MDT Files package for new ZTI task sequences.

## Next steps

[Known issues](known-issues.md)

[Frequently asked questions](faq.yml)
