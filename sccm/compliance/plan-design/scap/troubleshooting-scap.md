---
title: "Troubleshoot SCAP"
titleSuffix: "System Center Configuration Manager"
description: "Import the SCAP compliance settings as configuration baselines and export the results"
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
---


# Troubleshoot the SCAP Extensions for Microsoft System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> This feature was first introduced in Technical Preview version 1803 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). This pre-release version of the SCAP extensions can be installed on any currently supported versions of Configuration Manager current branch and LTSB 1606. The install file is located at cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi starting in 1803 technical preview. 

SCAP Extensions for Microsoft System Center Configuration Manager are designed to work with the SCAP data streams intended for the SCAP validated tool with ACS capability to support USGCB. Typically, you won't experience problems with these USGCB SCAP data streams that are downloaded from the NIST Web site.

However, you can diagnose and troubleshoot issues that you may see using the following methods:

- Ensure the SCAP Extensions client (scmdcm.msi) components are installed on all the target computers.
- Review the log file output of the Microsoft.Sces.ScapToDcm.exe tool.
- Review common problems and solutions when using SCAP Extensions.
- Contact Microsoft for questions or feedback about SCAP Extensions.



## Review Microsoft.Sces.ScapToDcm.exe Tool Log

The Microsoft.Sces.ScapToDcm.exe tool creates a customized named log file when the –log parameter is specified. The log file has information about the results of running the Microsoft.Sces.ScapToDcm.exe tool. For example, the log file has the number of items in the XCCDF/DataStream input file that were dropped or skipped while running the Microsoft.Sces.ScapToDcm.exe tool.

The following table lists some of the information that appears in the log file and a description of each type of information.

### Description of Information found in Microsoft.Sces.ScapToDcm.exe Log Files

| Information | Description |
| --- | --- |
| Drop | An item may be dropped because the test type is not a supported test type. |
| Skip |The OVAL definition ID is for an invalid platform. </br> </br>The OVAL definition ID is not referred to by the XCCDF/DataStream input file.</br> </br>The OVAL test ID is not referred to by the XCCDF/DataStream input file. The XCCDF profile ID does not contain any @select statements equal to 1. </br></br> The XCCDF profile ID includes an abstract attribute that is true. </br></br> The XCCDF profile ID does not contain a qualifying rule.|

## Common Problems and Solutions

The following table lists some common problems and solutions to assist you with troubleshooting.

Table 1.6 Common Problems and Solutions

| Problem | Possible solution |
| --- | --- |
| If you see any **Error** or **Unknown** statuses of a baseline, and IE cannot successfully show the report. IE says &quot;The report is either empty or invalid&quot; | Select the baseline and click **Evaluate** to run the baseline again then wait to monitor the **Compliant State**/**Last Evaluation update**. After the Last Evaluation date is updated to the current date/time (means it completed the evaluation), select the baseline and view the report again. If IE still cannot view the report, it may mean the baseline is too large. Regenerate the content using a smaller batch size to create smaller child baselines. If this issue happens on the parent baselines, try deploying the child baselines instead. |
| I have created Group Policy objects (GPOs) that include the prescribed USGCB settings, and linked them to the organizational units (OUs) that contain computers running Windows 7, yet the compliance reports indicate that some of the settings are not configured correctly. | It is possible that the Group Policy permissions are incorrect or that they have not been linked to the correct OU. However, it is more likely that the new settings have not taken effect yet. By default, Group Policy, in client computers that belong to an Active Directory domain, check for updates to Group Policy every 90 minutes. This may be one reason why the settings do not appear to have been applied, even though you have configured the policies correctly. Another factor to remember is that many computer settings require a restart before they can take effect. For example, the setting called **System cryptography: Use FIPS compliant algorithms for encryption, hashing, and signing, requires you to restart the computer before Windows can use the specified encryption algorithms. You can bypass the Group Policy refresh interval by entering the following command at a command prompt with administrator privileges: gpupdate /force After the Group Policy refresh completes, restart the computer to ensure that all of the settings take effect. For more information, see: [A Description of the Group Policy Update Utility](http://support.microsoft.com/kb/298444), Knowledge Base article 298444. |
| I am having trouble providing the database connection with my organizational information. | For procedural information about how to configure your database connection information, see the [Install and configure SCAP](/sccm/compliance/plan-design/scap/install-configure-scap) article. 

## Next step
> [!div class="nextstepaction"]
> [Install and configure SCAP Extensions](/sccm/compliance/plan-design/scap/install-configure-scap)