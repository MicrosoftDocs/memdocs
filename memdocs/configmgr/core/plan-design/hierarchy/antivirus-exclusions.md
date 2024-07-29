---
title: Antivirus exclusions
titleSuffix: Configuration Manager
description: Learn about recommended antivirus exclusions for use when troubleshooting possible issues.
ms.date: 10/31/2019
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Recommended antivirus exclusions for Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article contains recommendations that may help an administrator determine the cause of potential instability on a computer that is running a supported version of Configuration Manager site servers, site systems, and clients when it's used together with antivirus software.

> [!IMPORTANT]
>
> - We recommend that you temporarily apply these procedures to evaluate a system. If your system performance or stability is improved by the recommendations that are made in this article, contact your antivirus software vendor for instructions or for an updated version of the antivirus software.
> - This article contains information that shows how to help lower security settings or how to temporarily turn off security features on a computer. You can make these changes to understand the nature of a specific problem. Before you make these changes, we recommend that you evaluate the risks that are associated with implementing this workaround in your particular environment.

## Possible symptoms 

Antivirus real-time protection can cause many problems on Configuration Manager site servers, site systems, and clients.

The following is a non-comprehensive list of possible symptoms:

- Remote site system components aren't installed. SiteComp.log, Distmgr.log, hman.log, or other Configuration Manager log files may contain errors such as error 80070005.
- The Configuration Manager client can't be installed by using Client Push.
- Client inventory information is inaccurate, missing, or out-of-date.
- Backlogs occur in the *Install_Directory*\Program Files\Microsoft Configuration Manager\Inboxes folders.
- Software Center is not populated by deployed software on client systems, or doesn't start. Also, the CCMRepair.log file may contain errors that resemble the following example:

  > Database verification failed with result: 0x80004005 but DB: C:\Windows\CCM\filename.sdf could be opened, skipping DB repair.

- Software that is deployed to clients can't be installed.
- Compliance data for software deployments is inaccurate.

## Exclusions

To prevent such problems, we recommend that you add the following real-time protection exclusions:

### Default Installation Folders

|Folder|Path|
| - | - |
|*ConfigMgr Installation Folder*  |  %ProgramFiles%\Microsoft Configuration Manager  |  
|*MP Installation Folder*  |%ProgramFiles%\SMS_CCM  |  
|*Client Installation Folder*  |%Windir%\CCM  |  

### Folder exclusions for site servers

- *ConfigMgr Installation Folder*\Inboxes
- *ConfigMgr Installation Folder*\Logs
- *ConfigMgr Installation Folder*\EasySetupPayload

### Folder exclusions for site systems

- Management points
  - *MP installation folder*\ServiceData
  - Either of the following:
    - *ConfigMgr installation folder*\MP\OUTBOXES
    - *Installation drive*\SMS\MP\OUTBOXES
- Distribution points
  - *Client installation folder*\ServiceData
  - *ContentLib_Drive*\SMS_DP$
  - *ContentLib_Drive*\SMSPKG*Drive_Letter*$
  - *ContentLib_Drive*\SMSPKG
  - *ContentLib_Drive*\SMSPKGSIG
  - *ContentLib_Drive*\SMSSIG$
- Site database servers
  - [How to choose antivirus software to run on computers that are running SQL Server](https://support.microsoft.com/en-us/help/309422)

### Folder exclusions for clients

- *Client Installation Folder*\\\*.sdf
- *Client Installation Folder*\ServiceData
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- *Client Installation Folder*\Logs

### File exclusions for MPs

- POL00000.pol in
  - *MP Installation Folder*\PolReqStaging

### Process exclusions

Process exclusions are necessary only if aggressive antivirus programs consider Configuration Manager program files (.exe files) to be high-risk processes.

- *ConfigMgr Installation Folder*\bin\64\Smsexec.exe
- Either of the following processes:
  - *Client Installation Folder*\Ccmexec.exe
  - *MP Installation Folder*\Ccmexec.exe
- *Client Installation Folder*\CmRcService.exe (client-side)
- *ConfigMgr Installation Folder*\bin\64\Sitecomp.exe
- *ConfigMgr Installation Folder*\bin\64\Smswriter.exe
- *ConfigMgr Installation Folder*\bin\64\Smssqlbkup.exe, or SMS_*SQLFQDN*\bin\x64\Smssqlbkup.exe
- *ConfigMgr Installation Folder*\bin\64\Cmupdate.exe
- *Client Installation Folder*\Ccmrepair.exe (client-side)
- %*windir*%\CCMSetup\Ccmsetup.exe (client-side)

## Next steps

For more information about antivirus exclusions, see the following articles:

[Configuration Manager Current Branch Antivirus Exclusions -System Center Premier Field Engineer Blog](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-current-branch-antivirus-exclusions/ba-p/884831)

[Updated System Center 2012 Configuration Manager Antivirus Exclusions with more details on OSD and Boot Images](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/updated-system-center-2012-configuration-manager-antivirus/ba-p/884371)

[How to choose antivirus software to run on computers that are running SQL Server](https://support.microsoft.com/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server)

[Virus scanning recommendations for Enterprise computers that are running currently supported versions of Windows](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)
