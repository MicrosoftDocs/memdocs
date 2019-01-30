---
title: SCAP extensions
titleSuffix: Configuration Manager
description: Learn about the Security Content Automation Protocol (SCAP) extensions for Configuration Manager.
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# About the Security Content Automation Protocol (SCAP) extensions

*Applies to: System Center Configuration Manager (Current Branch)*

The SCAP extensions for Configuration Manager help you analyze and assess your network environment for compliance with the Security Content Automation Protocol (SCAP). SCAP is defined and maintained by the National Institute of Standards and Technology (NIST). For more information, see the [SCAP Project Overview](https://csrc.nist.gov/projects/security-content-automation-protocol).

> [!Note]  
> This version of the tool is a pre-release feature that's only available in version 1806. This version isn't certified by NIST. <!--SCCMDocs-pr issue 3323-->
> 
> If you require a certified tool, or are using another version of Configuration Manager current branch, use the following version of the SCAP extensions:
> - [Download SCAP Extensions for System Center Configuration Manager](https://www.microsoft.com/download/details.aspx?id=48741)
> - [Documentation for SCAP Extensions Version 3.0](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/mt228311\(v%3dtechnet.10\))

The SCAP extensions for Configuration Manager use the compliance settings feature to first scan the computers in your environment. It then documents their level of compliance with the United States Government Configuration Baseline (USGCB).

The extensions enable Configuration Manager to consume SCAP data streams, assess systems for compliance, and generate report results in SCAP format. Your organization can use your existing Configuration Manager infrastructure to help ensure computers you manage meet this federal compliance requirement. Also use Configuration Manager to generate the USGCB reports required by NIST and the Office of Management and Budget (OMB).

This article provides information to help you install, configure, and run the SCAP extensions in your Configuration Manager infrastructure.



## What's new

This version of the SCEP extensions for Configuration Manager includes and supports the following features:  

- A Configuration Manager console extension, which supports converting SCAP content to compliance settings baselines.  

- SCAP version 1.2, which includes the following components:  

  - Extensible Configuration Checklist Description Format (XCCDF) version 1.2
  - Open Vulnerability and Assessment Language (OVAL) versions up to 5.10
  - generating Asset Reporting Format (ARF) 1.1 reports
  - Common Platform Enumeration (CPE) 2.3
  - Common Vulnerabilities and Exposures (CVE)
  - Common Configuration Enumeration (CCE) version 5
  - USGCB Internet Explorer 8, USGCB Windows 7, and USGCB Windows 7 Firewall  

- Backward-compatible with SCAP versions 1.1 and 1.0.  

- A console wizard to import SCAP 1.2/1.1/1.0 and OVAL content for conversion to configuration baselines.  

  - Allows selection of SCAP source data streams, and XCCDF benchmarks and profiles for conversion.

- A console wizard to export configuration evaluation result to SCAP-formated XML report.  

  - Displays the source file, SCAP data stream, XCCDF benchmark, and XCCDF profile used to generate the baseline.
  - Generate the Cyberscope Lightweight Asset Summary Results (LASR) report.  

- Generate SCAP reports based on configuration baseline deployment. This component includes a new dashboard to visualize the client compliance as well as XCCDF rule compliance. The dashboard supports drilling through to more detailed reports where you can search and filter.  

- Improved performance of several types of configuration items converted from OVAL tests, which allows faster evaluation.  

- Fixes several issues found in Windows 10 DISA v1r3 content.  



## Terms

- **OVAL ID**: An identifier for a specific OVAL definition that conforms to the format for OVAL IDs.  

- **SCAP result data stream**: A bundle of SCAP components, along with the mappings of references between SCAP components, that hold output (result) content.  

- **SCAP source data stream**: A bundle of SCAP components, along with the mappings of references between SCAP components, that hold input (source) content.



## Deployment process

Here's a summary of the overall deployment process:  

- [Prepare the infrastructure](#bkmk_prepare) to use the extensions  

- [Install and configure the SCAP extensions](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_install) for Configuration Manager  

- [Download and install the SCAP data stream files](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_scap-data-stream-files) from NIST  

- Convert and import the SCAP data stream files into a Configuration Manager compliance settings baseline. Use one of the two following methods:   

    - [Manual process](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) using the import wizard in the Configuration Manager console  

    - [Automated process](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_auto-convert-and-import) with the Microsoft.Sces.ScapToDcm.exe command-line tool  

- [Deploy](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_deploy) the configuration baselines to collections  

- [Monitor](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_monitor) the compliance data  

- Export compliance results to SCAP format using one of the two following methods:  

    - [Manual process](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_export) using the export wizard in the console  

    - [Automated process](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_auto-export) using the Microsoft.Sces.DcmToScap.exe command-line tool  



## <a name="bkmk_prepare"></a> Prepare the infrastructure

### Software requirements

To install, configure, and run the SCAP extensions for Configuration Manager, you need a computer with the following software:

- A [supported version](/sccm/core/servers/manage/current-branch-versions-supported) of the Configuration Manager current branch console.  

- An OS version compatible with the Configuration Manager console. For more information, see [Supported operating systems for Configuration Manager consoles](/sccm/core/plan-design/configs/supported-operating-systems-consoles).  

In addition to the computer running the SCAP extensions, you also need the following items:

- A Configuration Manager current branch infrastructure. For more information about the requirements for a Configuration Manager deployment, see the [Supported Configurations for Configuration Manager](/sccm/core/plan-design/configs/supported-configurations) article.  

The computers that you want to assess for SCAP compliance need the following software and configurations:

- The Configuration Manager client.  

- Windows PowerShell 2.0 or higher.  

- The Configuration Manager PowerShell execution policy set to **Bypass**. For more information, see the [PowerShell execution policy](/sccm/core/clients/deploy/about-client-settings#computer-agent) article.  

- One of the following operating systems:  
  - Windows 7 SP1, 32-bit or 64-bit
  - Windows 10, 32-bit or 64-bit
  - Windows Server 2012 R2

### Hardware Requirements

For more information about the minimum system requirements for Configuration Manager, see [Planning for hardware configurations for Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware).



## Accessibility features

The SCAP extensions for Configuration Manager include Windows command-line tools. These tools can take advantage of the accessibility features and tools in Windows.

- Command-line parameters are documented for Microsoft.Sces.ScapToDcm.exe and Microsoft.Sces.DcmToScap.exe. For more information, see [Microsoft.Sces.ScapToDcm.exe. Command-Line Parameters](/sccm/compliance/plan-design/scap/install-configure-scap#microsoftscesscaptodcmexe-command-line-parameters) and [Microsoft.Sces.DcmToScap.exe Command-Line Parameters](/sccm/compliance/plan-design/scap/import-scap-compliance-settings#microsoftscesdcmtoscapexe-command-line-parameters).  

- The command-line parameters `-help` and `-?` for each tool print the usage to the screen. These usage details are then available to screen readers and other assistive technology.  

- For more information, see [Windows Accessibility](http://windows.microsoft.com/windows/help/accessibility).

The SCAP extensions also make use of accessibility features in Configuration Manager. For more information, see [Accessibility features in Configuration Manager](/sccm/core/understand/accessibility-features).

For more information about Microsoft accessibility products and services, see the [Microsoft Accessibility website](http://go.microsoft.com/fwlink/p/?LinkId=9212).



## Next step
> [!div class="nextstepaction"]
> [Install and configure SCAP extensions](/sccm/compliance/plan-design/scap/install-configure-scap)
