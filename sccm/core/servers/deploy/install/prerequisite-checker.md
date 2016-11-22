---
title: "Prerequisite checker | Microsoft Docs"
description: "Learn how to use the prerequisite checker to identify and fix problems that would block an actual site or site system role installation."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
caps.latest.revision: 3
author: Brendunsms.author: brendunsmanager: angrobe
---
# Prerequisite checker for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*

 Before you run Setup to install or upgrade a System Center Configuration Manager site, or before you install a site system role on a new server, you can use this stand-alone application (**Prereqchk.exe**) from the version of Configuration Manager that you want use to verify server readiness. The use of prerequisite checker enables you to identify and fix problems that would block an actual site or site system role installation.  

> [!NOTE]  
>  Prerequisite checker always runs as part of Setup.  

By default, when prerequisite checker runs:  

-   It validates the server where it runs  

-   The local computer is scanned for an existing site server, and only the checks that are applicable to the site are run  

-   If no existing sites are detected, all prerequisite rules are run  

-   It checks rules to verify that software and settings required for setup are installed. It is possible that required software requires additional configurations or software updates that are not verified by the prerequisite checker  

-   It logs its results in the **ConfigMgrPrereq.log** file on the system drive of computer. The log file can contain additional information that does not display in user interface.  

When you run prerequisite checker at a command prompt and specify specific command-line options:  

-   Prerequisite checker only performs the checks that are associated with the site server or site systems that you specified in the command line  

-   To check a remote computer, your User account must have Administrative rights to the remove computer  

For more information about the prerequisite checks that prerequisite checker performs, see [List of Prerequisite Checks for System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md)  

## Copy prerequisite checker files to another computer  

1.  In Windows Explorer, browse to one of the following locations:  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  Copy the following files to the destination folder on the other computer:  

    -   Prereqchk.exe  

    -   Prereqcore.dll  

    -   Basesql.dll  

    -   Basesvr.dll  

    -   Baseutil.dll  

##  Run prerequisite checker with default checks  

1.  In Windows Explorer, browse to one of the following locations:  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  Run **prereqchk.exe** to start Prerequisite Checker.   
    Prerequisite Checker detects existing sites, and if found, performs checks for upgrade readiness. If no sites are found, all checks are performed. The **Site Type** column provides information about the site server or site system with which the rule is associated.  

##  Run prerequisite checker from a command prompt for all default checks  

1.  Open a Command Prompt window and change directories to one of the following locations:  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  Enter  **prereqchk.exe /LOCAL** to start Prerequisite Checker and run all prerequisite checks on the server.  

## Run prerequisite checker from a command prompt  for specified options  

1.  Open a Command Prompt window and change directories to one of the following locations:  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  Enter  **prereqchk.exe** with the addition of one or more of the following command-line options.  

    For example, to check a primary site you might use the following:  

    -   **prereqchk.exe [/NOUI] /PRI /SQL &lt;FQDN of SQL Server\> /SDK &lt;FQDN of SMS Provider\> [/JOIN &lt;FQDN of central administration site\>] [/MP &lt;FQDN of management point\>] [/DP &lt;FQDN of distribution point\>]**  

    **Central administration site server:**  

    -   **/NOUI**  

         Not required -  Starts Prerequisite Checker without displaying the user interface. You must specify this option before any other option in the command line.  

    -   **/CAS**  

         Required - Verifies that the local computer meets the requirements for the central administration site.  

    -   **/SQL &lt;*FQDN of SQL Server*>**  

         Required - Verifies that the specified computer meets the requirements for SQL Server to host the Configuration Manager site database.  

    -   **/SDK &lt;*FQDN of SMS Provider*>**  

         Required - Verifies that the specified computer meets the requirements for the SMS Provider.  

    -   **/Ssbport**  

         Not required - Verifies that a firewall exception is in effect to allow communication on the SSB port. The default is port number 4022.  

    -   **InstallDir &lt;*ConfigMgrInstallationPath*>**  

         Not required - Verifies minimum disk space on requirements for site installation.  

    **Primary site server:**  

    -   **/NOUI**  

        Not required -  Starts Prerequisite Checker without displaying the user interface. You must specify this option before any other option in the command line.  

    -   **/PRI**  

         Required - Verifies that the local computer meets the requirements for the primary site.  

    -   **/SQL &lt;*FQDN of SQL Server*>**  

         Required - Verifies that the specified computer meets the requirements for SQL Server to host the Configuration Manager site database.  

    -   **/SDK &lt;*FQDN of SMS Provider*>**  

         Required - Verifies that the specified computer meets the requirements for the SMS Provider.  

    -   **/JOIN &lt;*FQDN of central administration site*>**  

         Not required - Verifies that the local computer meets the requirements for connecting to the central administration site server.  

    -   **/MP &lt;*FQDN of management point*>**  

         Not required - Verifies that the specified computer meets the requirements for the management point site system role. This option is only supported when you use the **/PRI** option.  

    -   **/DP &lt;*FQDN of distribution point*>**  

         Not required - Verifies that the specified computer meets the requirements for the distribution point site system role. This option is only supported when you use the **/PRI** option.  

    -   **/Ssbport**  

         Not required - Verifies that a firewall exception is in effect to allow communication on the SSB port. The default is port number 4022.  

    -   **InstallDir &lt;*ConfigMgrInstallationPath*>**  

         Not required - Verifies minimum disk space on requirements for site installation.  

    **Secondary site server:**  

    -   **/NOUI**  

         Not required -  Starts Prerequisite Checker without displaying the user interface. You must specify this option before any other option in the command line.  

    -   **/SEC &lt;*FQDN of secondary site server*>**  

         Required - Verifies that the specified computer meets the requirements for the secondary site.  

    -   **/INSTALLSQLEXPRESS**  

         Not required - Verifies that SQL Server Express can be installed on the specified computer.  

    -   **/Ssbport**  

         Not required -      
        Verifies that a firewall exception is in effect to allow communication for the SQL Server Service Broker (SSB) port. The default is port number 4022.  

    -   **/Sqlport**  

         Not required - Verifies that a firewall exception is in effect to allow communication for the SQL Server service port and that the port is not in use by another named instance of SQL Server. The default port is 1433.  

    -   **InstallDir &lt;*ConfigMgrInstallationPath*>**  

         Not required - Verifies minimum disk space on requirements for site installation.  

    -   **/SourceDir**  

         Not required - Verifies that the computer account of the secondary site can access the folder that hosts the source files for Setup.  

     **Configuration Manager console:**  

    -   **/Adminui**  

         Required - Verifies that the local computer meets the requirements for installing the Configuration Manager.  

3.  In the Prerequisite Checker UI, Prerequisite Checker creates a list of discovered problems in the **Prerequisite result** section.  

    -   Click an item in the list for details about how to resolve the problem.  

    -   You must resolve all items in the list that have an **Error** status before you install the site server, site system, or Configuration Manager console.  

    -   You can also open the **ConfigMgrPrereq.log** file in the root of the system drive to review Prerequisite Checker results. The log file can contain additional information that are not displayed in the user interface.  
