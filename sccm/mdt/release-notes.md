---
title: MDT release notes
description: Understand supported platforms, prerequisites, and limitations of Microsoft Deployment Toolkit.
ms.date:  06/04/2018
ms.prod: configuration-manager
ms.technology:
  - configmgr-osd
ms.topic: article
ms.assetid:  6e32ce6d-585d-4801-a345-ff0f6f2d90ad
author: aczechowski  
ms.author: aaroncz 
manager: dougeby
---

# Microsoft Deployment Toolkit release notes  

This article provides details on the latest release of the Microsoft Deployment Toolkit (MDT). These details include supported platforms, prerequisites, and any limitations. It assumes familiarity with MDT version concepts, features, and capabilities.



## Latest release

**MDT build 8450** is the latest version available on the [Microsoft Download Center](https://aka.ms/mdtdownload). 

This update begins support for the Windows Assessment and Deployment Kit (ADK) for Windows 10, version 1709 (adksetup.exe file version 10.1.16299.15). For more information, see the [supported platforms](#supported-platforms) section.

### Significant changes
Here is a summary of the significant changes in this build of MDT.

#### Supported configuration updates
- Windows ADK for Windows 10, version 1709
- Windows 10, version 1709
- Configuration Manager, version 1710

#### Quality updates
The following are the titles of bug fixes in this release:
- Win10 Sideloaded App dependencies and license not installed
- CaptureOnly task sequence doesn't allow capturing an image
- Error received when starting an MDT task sequence: Invalid DeploymentType value "" specified. The deployment will not proceed
- ZTIMoveStateStore looks for the state store folder in the wrong location causing it to fail to move it
- xml contains a simple typo that caused undesirable behavior
- Install Roles & Features doesn't work for Windows Server 2016 IIS Management Console feature
- Browsing for OS images in the upgrade task sequence doesn't work when using folders
- MDT tool improperly provisions the TPM into a Reduced Functionality State. For more information, see [KB 4018657](https://support.microsoft.com/help/4018657/tpm-is-in-reduced-functionality-mode-after-successful-deployment-of-wi).
- Updates to ZTIGather chassis type detection logic
- Upgrade OS step leaves behind SetupComplete.cmd, breaking future deployments
- Windows 10 ADK 1607 and later UEFI boot issue on some hardware
- Includes updated Configuration Manager task sequence binaries



## Supported platforms

MDT releases are no longer tagged with year or update version. To better align with the current branches of Windows 10 and Configuration Manager, and to simplify the branding and release process, it's now simply **Microsoft Deployment Toolkit**. The build number is used to distinguish each release. For example, the latest build available for download is 8450.

Unlike Configuration Manager with a predetermined release schedule, MDT only releases as required to support new versions of Windows 10, the Windows ADK, or Configuration Manager current branch. Any known issues with these components will be documented in this article as necessary.

The following OS versions are supported for deployment with MDT:
- Windows 10 version 1803
- Windows 10 version 1709
- Other [supported versions](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) of Windows 10
- Windows 8.1
- Windows 7
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2



## Prerequisites

MDT requires the following components, which are included in Windows:
- Microsoft .NET Framework 4.0
- Windows PowerShell version 3.0

Use the latest [Windows ADK for Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install). 

> [!Note]  
> Windows recommends using the Windows ADK that matches the version of Windows you're deploying. For example, use the Windows ADK for Windows 10 version 1703 when deploying Windows 10 version 1703. For more information on Windows ADK component supportability, see [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) and [USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1).

When integrating MDT with Configuration Manager for ZTI and UDI scenarios, use the latest version of Configuration Manager current branch.



## Upgrading MDT

The MDT installation process removes any existing instances of MDT installed on the same computer. Existing deployment shares, distribution points, and databases are preserved during this process. They must be upgraded when the installation is complete.

The current release of MDT supports upgrading from the following versions of MDT:
- MDT build 8443

> [!Tip]  
> Create a backup of the existing MDT infrastructure before attempting an upgrade.

### LTI
After installing MDT, upgrade an existing deployment share by running the **Open Deployment Share Wizard** from the Deployment Shares node in the Deployment Workbench. Specify the path to the existing deployment share directory, and then select the **Upgrade** check box. This process also upgrades existing network deployment shares and media deployment shares, so those shares should be accessible. Don't perform this upgrade while performing deployments, because in-use files can cause upgrade problems.

### ZTI
Existing MDT task sequences present in Configuration Manager aren't modified during the installation process of MDT. They should continue to work without any issue. No mechanism is provided to upgrade these task sequences. If you want to use any of the new MDT capabilities, create new MDT-integrated task sequences in Configuration Manager.

When the upgrade process is complete:  

- Run the **Configure ConfigMgr Integration Wizard** after the upgrade. It registers the new components and installs the updated ZTI task sequence templates.  

- Create a new **Microsoft Deployment Toolkit Files** package for any new ZTI task sequences you create. You can use the existing Microsoft Deployment Toolkit Files package for any ZTI task sequences created prior to the upgrade, but you must create a new Microsoft Deployment Toolkit Files package for new ZTI task sequences.



<!--
## Known issues
-->



## Frequently asked questions

#### What's the MDT support life cycle?  
For more information, see [Microsoft Deployment Toolkit support life cycle](https://support.microsoft.com/help/2872000/microsoft-deployment-toolkit-support-life-cycle).

#### Is this release only supported with Windows 10, Windows ADK, or Configuration Manager version *X*?
We primarily tested this build of MDT with the configuration listed above. Unless there are any explicit known issues, anything outside of the above configuration has a high probability of still working. Your mileage may vary as we haven’t explicitly tested other combinations.

#### How do I get help with MDT?
Use one of the following methods to get help with MDT (in prioritized order):

1. Post to the [MDT forum](https://social.technet.microsoft.com/Forums/en/home?forum=mdt). MVPs and others in the community watch and respond to posts there. Probably the most efficient way to get help.
2. Contact Microsoft Support. Get a support case open and get some professional help.
3. If you can consistently reproduce an issue and think it's a product bug, file it in the Windows 10 [Feedback Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app). The product team investigates everything that's reported. Use the **Enterprise Management** category and **OS Deployment** subcategory when filing feedback. This categorization helps classify and route your feedback to the MDT team.
     - The Feedback Hub can also be used to submit suggestions (design change requests or DCRs) on the product.
     - If you previously filed feedback via Connect, you don't need to refile in the Feedback Hub.