---
title: "Prerequisite Checker"
titleSuffix: "Configuration Manager"
description: "Learn how to use Prerequisite Checker to identify and fix problems that might block a site or site system role installation."
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Prerequisite Checker for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

 Before you run Setup to install or upgrade a System Center Configuration Manager site, or before you install a site system role on a new server, you can use this stand-alone application (**Prereqchk.exe**) from the version of Configuration Manager that you want use to verify server readiness. Use Prerequisite Checker to identify and fix problems that would block a site or site system role installation.  

> [!NOTE]  
>  Prerequisite Checker always runs as part of Setup.  

By default, when Prerequisite Checker runs:  

-   It validates the server where it runs.  
-   The local computer is scanned for an existing site server, and only the checks that are applicable to the site are run.  
-   If no existing sites are detected, all prerequisite rules are run.  
-   It checks rules to verify that software and settings required for setup are installed. It's possible that required software will require additional configuration or software updates that are not verified by Prerequisite Checker.  
-   It logs its results in the **ConfigMgrPrereq.log** file on the system drive of the computer. The log file might contain additional information that doesn't appear in the application interface.  

When you run Prerequisite Checker at a command prompt and specify specific command-line options:  

-   Prerequisite Checker performs only the checks that are associated with the site server or site systems that you specify in the command line.  
-   To check a remote computer, your user account must have Administrator rights to the remote computer.  

For more information about the checks that Prerequisite Checker performs, see [List of prerequisite checks for System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

## Copy Prerequisite Checker files to another computer  

1.  In Windows Explorer, go to one of the following locations:  

    -   **&lt;*Configuration Manager installation media*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager installation path*\>\BIN\X64**  

2.  Copy the following files to the destination folder on the other computer:  

    -   Prereqchk.exe  
    -   Prereqcore.dll  
    -   Basesql.dll  
    -   Basesvr.dll  
    -   Baseutil.dll  

##  Run Prerequisite Checker with default checks  

1.  In Windows Explorer, go to one of the following locations:  

    -   **&lt;*Configuration Manager installation media*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager installation path*\>\BIN\X64**  

2.  Run **prereqchk.exe** to start Prerequisite Checker.   
    Prerequisite Checker detects existing sites, and if found, performs checks for upgrade readiness. If no sites are found, all checks are performed. The **Site Type** column provides information about the site server or site system with which the rule is associated.  

##  Run Prerequisite Checker from a command prompt for all default checks  

1.  Open a Command Prompt window and change directories to one of the following locations:  

    -   **&lt;*Configuration Manager installation media*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager installation path*\>\BIN\X64**  

2.  Enter  **prereqchk.exe /LOCAL** to start Prerequisite Checker and run all prerequisite checks on the server.  

## Run Prerequisite Checker from a command prompt to use options  

1. Open a Command Prompt window and change directories to one of the following locations:  

   -   **&lt;*Configuration Manager installation media*\>\SMSSETUP\BIN\X64**  
   -   **&lt;*Configuration Manager installation path*\>\BIN\X64**  

2. Enter  **prereqchk.exe** with the addition of one or more of the following command-line options.  

   For example, to check a primary site, you might use the following:  

      **prereqchk.exe [/NOUI] /PRI /SQL &lt;FQDN of SQL Server\> /SDK &lt;FQDN of SMS Provider\> [/JOIN &lt;FQDN of central administration site\>] [/MP &lt;FQDN of management point\>] [/DP &lt;FQDN of distribution point\>]**  

   **Central administration site server:**  

   -   **/NOUI**  

        Not required. Starts Prerequisite Checker without displaying the user interface. You must specify this option before any other option in the command line.  

   -   **/CAS**  

        Required. Verifies that the local computer meets the requirements for the central administration site.  

   -   **/SQL &lt;*FQDN of SQL Server*>**  

        Required. Using the fully qualified domain name (FQDN), verifies that the specified computer meets the requirements for SQL Server to host the Configuration Manager site database.  

   -   **/SDK &lt;*FQDN of SMS Provider*>**  

        Required. Verifies that the specified computer meets the requirements for the SMS Provider.  

   -   **/Ssbport**  

        Not required. Verifies that a firewall exception is in effect to allow communication on the SQL Server Service Broker (SSB) port. The default SSB port is 4022.  

   -   **InstallDir &lt;*Configuration Manager installation path*>**  

        Not required. Verifies the minimum disk space on requirements for site installation.  

   **Primary site server:**  

   -   **/NOUI**  

       Not required. Starts Prerequisite Checker without displaying the user interface. You must specify this option before any other option in the command line.  

   -   **/PRI**  

        Required. Verifies that the local computer meets the requirements for the primary site.  

   -   **/SQL &lt;*FQDN of SQL Server*>**  

        Required. Verifies that the specified computer meets the requirements for SQL Server to host the Configuration Manager site database.  

   -   **/SDK &lt;*FQDN of SMS Provider*>**  

        Required. Verifies that the specified computer meets the requirements for the SMS Provider.  

   -   **/JOIN &lt;*FQDN of central administration site*>**  

        Not required. Verifies that the local computer meets the requirements for connecting to the central administration site server.  

   -   **/MP &lt;*FQDN of management point*>**  

        Not required. Verifies that the specified computer meets the requirements for the management point site system role. This option is only supported when you use the **/PRI** option.  

   -   **/DP &lt;*FQDN of distribution point*>**  

        Not required. Verifies that the specified computer meets the requirements for the distribution point site system role. This option is only supported when you use the **/PRI** option.  

   -   **/Ssbport**  

        Not required. Verifies that a firewall exception is in effect to allow communication on the SSB port. The default SSB port is 4022.  

   -   **InstallDir &lt;*Configuration Manager installation path*>**  

        Not required. Verifies the minimum disk space on requirements for site installation.  

   **Secondary site server:**  

   -   **/NOUI**  

        Not required. Starts Prerequisite Checker without displaying the user interface. You must specify this option before any other option in the command line.  

   -   **/SEC &lt;*FQDN of secondary site server*>**  

        Required. Verifies that the specified computer meets the requirements for the secondary site.  

   -   **/INSTALLSQLEXPRESS**  

        Not required. Verifies that SQL Server Express can be installed on the specified computer.  

   -   **/Ssbport**  

        Not required. Verifies that a firewall exception is in effect to allow communication for the SSB port. The default SSB port is 4022.  

   -   **/Sqlport**  

        Not required. Verifies that a firewall exception is in effect to allow communication for the SQL Server service port, and that the port is not in use by another named instance of SQL Server. The default port is 1433.  

   -   **InstallDir &lt;*Configuration Manager installation path*>**  

        Not required. Verifies the minimum disk space on requirements for site installation.  

   -   **/SourceDir**  

        Not required. Verifies that the computer account of the secondary site can access the folder that hosts the source files for Setup.  

   **Configuration Manager console:**  

   -   **/Adminui**  

        Required. Verifies that the local computer meets the requirements for installing Configuration Manager.  

3. In the Prerequisite Checker user interface, Prerequisite Checker creates a list of discovered problems in the **Prerequisite result** section.  

   -   Click an item in the list for details about how to resolve the problem.  
   -   You must resolve all items in the list that have an **Error** status before you install the site server, site system, or the Configuration Manager console.  
   -   You also can open the **ConfigMgrPrereq.log** file in the root of the system drive to review Prerequisite Checker results. The log file might contain additional information that is not displayed in the Prerequisite Checker user interface.  
