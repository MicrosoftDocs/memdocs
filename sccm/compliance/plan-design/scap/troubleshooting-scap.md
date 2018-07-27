---
title: Troubleshoot SCAP
titleSuffix: Configuration Manager
description: Learn how to troubleshoot the SCAP extensions for Configuration Manager.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---


# Troubleshoot the SCAP extensions for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The SCAP extensions for Configuration Manager are designed to work with the SCAP data streams intended for the SCAP validated tool with ACS capability to support USGCB. Typically, you won't experience problems with these USGCB SCAP data streams that are downloaded from the NIST website.

Diagnose and troubleshoot issues using the following methods:  

- Ensure the SCAP extensions client (scmdcm.msi) components are installed on all the target computers.  

- Review the log file output of the Microsoft.Sces.ScapToDcm.exe tool.  

- Review common problems and solutions when using SCAP extensions.  

- Contact Microsoft for questions or feedback about SCAP extensions.



## Review Microsoft.Sces.ScapToDcm.exe log

The Microsoft.Sces.ScapToDcm.exe tool creates a customized named log file when you specify the `–log` parameter. The log file has information about the results of running the Microsoft.Sces.ScapToDcm.exe tool. For example, it includes the number of items in the XCCDF/DataStream input file that were dropped or skipped while running the Microsoft.Sces.ScapToDcm.exe tool.

The following table lists some of the information that appears in the log file and a description of each type of information.

### Information found in the Microsoft.Sces.ScapToDcm.exe log file

| Information | Description |
| --- | --- |
| **Drop** | An item may be dropped because the test type isn't a supported test type. |
| **Skip** | The OVAL definition ID is for an invalid platform. </br> </br> The OVAL definition ID isn't referred to by the XCCDF/DataStream input file.</br> </br> The OVAL test ID isn't referred to by the XCCDF/DataStream input file. </br> </br> The XCCDF profile ID doesn't contain any `@select` statements equal to 1. </br> </br> The XCCDF profile ID includes an abstract attribute that's true. </br> </br> The XCCDF profile ID doesn't contain a qualifying rule.|



## Common problems and solutions

Here are some common problems and solutions to assist you with troubleshooting.

- You see an **Error** or **Unknown** status for a baseline, and Internet Explorer can't successfully show the report. The browser error is, "The report is either empty or invalid."  

     - Run the baseline again. Select the baseline and click **Evaluate**. Then wait to monitor the **Compliant State**/**Last Evaluation update**. After the Last Evaluation date is updated to the current date/time, which means it completed the evaluation, select the baseline and view the report again.  

     - If Internet Explorer still can't view the report, it may mean the baseline is too large. Regenerate the content using a smaller batch size to create smaller child baselines.  

     - If this issue happens on the parent baselines, try deploying the child baselines instead.  

- I created group policy objects (GPOs) that include the prescribed USGCB settings. I linked them to the organizational units (OUs) that contain computers running Windows 7. The compliance reports indicate that some of the settings aren't correctly configured.  

     - It's possible that the group policy permissions are incorrect, or they haven't been linked to the correct OU.  

     - It's more likely that the new settings haven't yet taken effect. By default, Active Directory clients check for updates to group policy every 90 minutes. This cycle may be one reason why the settings don't appear to have been applied, even though you've correctly configured the policies.  

     - Many computer settings require a restart before they can take effect. For example, the setting for  **System cryptography: Use FIPS compliant algorithms for encryption, hashing, and signing** requires you to restart the computer before Windows can use the specified encryption algorithms. Bypass the group policy refresh interval by entering the following command at a command prompt with administrator privileges: `gpupdate /force`. After the Group Policy refresh completes, restart the computer to ensure that all of the settings take effect. For more information, see [A description of the group policy update utility](https://support.microsoft.com/help/298444).

- I'm having trouble providing the database connection with my organizational information.  

     - For more information about how to configure your database connection, see [Install and configure SCAP](/sccm/compliance/plan-design/scap/install-configure-scap).  
