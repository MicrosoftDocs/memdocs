---
title: "About Security Content Automation Protocol (SCAP) extensions"
titleSuffix: "System Center Configuration Manager"
description: "Learn about the Security Content Automation Protocol (SCAP) extensions"
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
---

# About the Security Content Automation Protocol (SCAP) extensions

*Applies to: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> This feature was first introduced in Technical Preview version 1803 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). This pre-release version of the SCAP extensions can be installed on any currently supported versions of Configuration Manager. 

The SCAP Extensions for Microsoft System Center Configuration Manager helps you analyze and assess your network environment for compliance with the Security Content Automation Protocol (SCAP). SCAP is defined and maintained by the U.S. National Institute of Standards and Technology (NIST).

The SCAP Extensions for Microsoft System Center Configuration Manager use the Compliance Settings feature in Microsoft System Center Configuration Manager to scan the computers in your environment and then document their level of compliance with the United States Government Configuration Baseline (USGCB) mandate.

The extensions enable Configuration Manager to consume Security Content Automation Protocol (SCAP) data streams, assess systems for compliance, and generate report results in SCAP format. Your organization can use your existing Configuration Manager infrastructure to help ensure computers you manage meet this federal compliance requirement and generate the requisite USGCB reports for the National Institute of Standards and Technology (NIST) and the U.S. Office of Management and Budget (OMB).

This guide provides information to help you install, configure, and run the SCAP Extensions in your System Center Configuration Manager infrastructure.



# What&#39;s New in SCAP Extensions Prerelease for Microsoft System Center Configuration Manager

Use this section to learn what&#39;s new in the latest version.

SCAP Extensions Prerelease for System Center Configuration Manager:

- Includes a Configuration Manager Console extension that fully supports converting SCAP Content to Compliance Settings baselines for System Center Configuration Manager current branch
- Supports SCAP version 1.2 and is backward compatible with SCAP versions 1.1 and 1.0.


  - Supports Extensible Configuration Checklist Description Format (XCCDF) version 1.2.
  - Supports Open Vulnerability and Assessment Language (OVAL) versions up to 5.10.
  - Supports generating Asset Reporting Format (ARF) 1.1 reports.
  - Supports Common Platform Enumeration (CPE) 2.3
  - Supports Common Vulnerabilities and Exposures (CVE)
  - Supports Common Configuration Enumeration (CCE) version 5
  - Supports USGCB Internet Explorer 8, USGCB Windows 7, and USGCB Windows 7 Firewall.

- Includes a UI wizard to import SCAP 1.2/1.1/1.0 and OVAL content for conversion to Configuration Baselines.


  - Allows selection of SCAP Source Data Streams, and XCCDF benchmarks and profiles for conversion.

- Includes a UI wizard to export Configuration Evaluation Result to SCAP format XML report


  - Displays the source file, SCAP Datastream, XCCDF Benchmark, and XCCDF Profile used to generate the baseline.
  - Supports generating the Cyberscope Lightweight Asset Summary Results (LASR) report.

- Supports generating SCAP reports based on Configuration Baseline deployment. Includes a new dashboard to visualize the client compliance as well as XCCDF Rule compliance. The dashboard supports drilling through to more detailed reports where you can search and filter.
- Improves the performance of several types Configuration Items converted from OVAL tests, allowing faster evaluation.

- Fixes several issues found in Windows 10 DISA v1r3 content.

# SCAP Extensions for Microsoft System Center Configuration Manager Deployment Process

This guide describes how to analyze, assess, and report on SCAP compliance using the SCAP Extensions for Microsoft System Center Configuration Manager. Here&#39;s a brief summary of the procedures you&#39;ll follow:

- Prepare the prerequisite infrastructure to take advantage of the extensions.
- Install and configure the SCAP Extensions for Microsoft System Center Configuration Manager.
- Download, install, and configure the SCAP data stream files from the [National Vulnerability Database](http://nvd.nist.gov) (NVD).
- Convert and import the SCAP data stream files directly into a System Center Configuration Manager compliance settings baseline using the Import Wizard **or** via a cabinet (.cab) file using the command-line Microsoft.Sces.ScapToDcm.exe tool.
- Export compliance results to SCAP format using the Export Wizard or the command-line Microsoft.Sces.DcmToScap.exe tool.

# Terms

**OVAL ID:** An identifier for a specific OVAL definition that conforms to the format for OVAL IDs.

**SCAP Result Data Stream:** A bundle of SCAP components, along with the mappings of references between SCAP components, that hold output (result) content.

**SCAP Source Data Stream:** A bundle of SCAP components, along with the mappings of references between SCAP components, that hold input (source) content.

# Prepare the Prerequisite Infrastructure

Make sure that the following software and hardware requirements are met to take advantage of the SCAP Extensions for Microsoft System Center Configuration Manager.

## Software Requirements

To install, configure, and run the SCAP Extensions for Microsoft System Center Configuration Manager, you need a computer with the following software:

- A [supported version](/sccm/core/servers/manage/current-branch-versions-supported) of the System Center Configuration Manager current branch console.
- An operating system compatible with the System Center Configuration Manager console. For a list of compatible operating systems, see the [Supported operating systems for System Center Configuration Manager consoles](/sccm/core/plan-design/configs/supported-operating-systems-consoles) article.

In addition to the computer running the SCAP Extensions, you will also need the following items:

- A System Center Configuration Manager current branch infrastructure. For more information about the requirements for a Configuration Manager deployment, see the [Supported Configurations for Configuration Manager](/sccm/core/plan-design/configs/supported-configurations) article.

The computers that you want to assess for SCAP compliance need the following software and configurations:

- The Compliance and Settings Management component enabled on the Configuration Manager client.
- Windows PowerShell 2.0 or higher.
- The Configuration Manager PowerShell execution policy set to **Bypass**. For more information, see the [PowerShell execution policy](/sccm/core/clients/deploy/about-client-settings#computer-agent) article.
- One of the following operating systems
  - Windows 7 release version or Sp1, 32-bit or 64-bit
  - Windows 10 32-bit or 64-bit
  - Windows Server 2012 R2

## Hardware Requirements

The minimum system requirements are provided here:

[Planning for Hardware Configurations for Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware)



## Accessibility Features

The SCAP Extensions for System Center Configuration Manager include Windows command-line tools that can take advantage of the accessibility features and tools in Windows.

- Command-line parameters are documented in this user guide for Microsoft.Sces.ScapToDcm.exe and Microsoft.Sces.DcmToScap.exe.
- -help and -? will print tool usage to the screen where it will be available to screen readers and other assistive technology.
- Windows [Accessibility](http://windows.microsoft.com/windows/help/accessibility)

The SCAP Extensions also make use of features in System Center Configuration Manager.  Configuration Manager includes features that make the product more accessible for people with disabilities.

- [Accessibility Features in System Center Configuration Manager](/sccm/core/understand/accessibility-features)

For general information about Microsoft accessibility products and services, visit the [Microsoft Accessibility website](http://go.microsoft.com/fwlink/p/?LinkId=9212).

## Next step
[Install and configure SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)