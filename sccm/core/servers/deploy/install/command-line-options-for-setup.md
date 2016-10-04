---
title: "Setup command-line options | System Center Configuration Manager"
description: "Use information in this article to configure scripts or install System Center Configuration Manager from a command line."
ms.custom: na
ms.date: 07/22/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
caps.latest.revision: 3
author: Brendunsms.author: brendunsmanager: angrobe
---
# Command-line options for Setup for System Center Configuration Manager

 Use information in the following tables when configuring scripts or installing System Center Configuration Manager from a command line.  

##  <a name="bkmk_setup"></a> Command-line options for Setup  
 **/DEINSTALL**  
 Uninstalls the site. You must run Setup from the site server computer.  

 **/DONTSTARTSITECOMP**  
 Install a site, but prevent the Site Component Manager service from starting. Until the Site Component Manager service starts, the site is not active. The Site Component Manager is responsible for installing and starting the SMS_Executive service, and additional processes at the site. After the site install is completed, when you start the Site Component Manager service, it will then install the SMS_Executive and additional processes necessary for the site to operate.  

 **/HIDDEN**  
 Hides the user interface during setup. This option must be used in conjunction with the **/SCRIPT** option, and the unattended script file must provide all required options, or Setup fails.  

 **/NOUSERINPUT**  
 Disables user input during Setup, but display the **Setup Wizard** interface. This option must be used in conjunction with the **/SCRIPT** option, and the unattended script file must provide all required options, or Setup fails.  

 **/RESETSITE**  
 Performs a site reset that resets the database and service accounts for the site. You must run Setup from **&lt;ConfigMgrInstallationPath\>\BIN\X64** on the site server. For more information about the site reset, see the [Run a site reset](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) section in the [Modify your System Center Configuration Manager infrastructure](../../../../core/servers/manage/modify-your-infrastructure.md) topic.  

 **/TESTDBUPGRADE &lt;*InstanceName\DatabaseName*>**  
 Performs a test on a backup of the site database to ensure that it is capable of an upgrade. You must provide the instance name and database name for the site database. If you specify only the database name, Setup uses the default instance name.  

> [!IMPORTANT]  
>  It is not supported to run this command-line option on your production site database. Doing so upgrades the site database and could render your site inoperable.  

 **/UPGRADE**  
 Runs an unattended upgrade of a site. When you use /UPGRADE, you must also specify the product key, including the dashes (-). Additionally, you must specify the path to the previously downloaded Setup prerequisite files.  

 Example: **setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx &lt;path to external component files\>**  

 For more information about Setup prerequisite files, see  [Setup Downloader](#bkmk_SetupDownloader) in this topic.  

 **/SCRIPT &lt;*SetupScriptPath*>**  
 Performs unattended installations. A Setup initialization file is required when you use the **/SCRIPT** option. For more information about how to run Setup unattended, see  [Install sites using a command line](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/SDKINST &lt;*FQDN*>**  
 Installs the SMS Provider on the specified computer. You must provide the FQDN for the SMS Provider computer. For more information about the SMS Provider, see the [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/SDKDEINST &lt;*FQDN*>**  
 Uninstalls the SMS Provider on the specified computer. You must provide the FQDN for the SMS Provider computer.  

 **/MANAGELANGS &lt;*LanguageScriptPath*>**  
 Manages the languages that are installed at a previously installed site. To use this option, you must run Setup from **&lt;ConfigMgrInstallationPath\>\BIN\X64** on the site server and provide the location for the language script file that contains the language settings. For more information about the language options available in the language setup script file, see [Command line options to manage languages](#bkmk_Lang) in this topic.  

##  <a name="bkmk_Lang"></a> Command line options to manage languages  
 **Identification**  

-   **Key Name:** Action  

    -   **Required:** Yes  

    -   **Values:** ManageLanguages  

    -   **Details:** Manages the server, client, and mobile client language support at a site.  

**Options**  

-   **Key Name:** AddServerLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Specifies the server languages that will be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default.  

-   **Key Name:** AddClientLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Specifies the languages that will be available to client computers. English is available by default.  

-   **Key Name:** DeleteServerLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Specifies the languages to remove that will no longer be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default and cannot be removed.  

-   **Key Name:** DeleteClientLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Specifies the languages to remove that will no longer be available to client computers. English is available by default and cannot be removed.  

-   **Key Name:** MobileDeviceLanguage  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies whether the mobile device client languages are installed.  

-   **Key Name:** PrerequisiteComp  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = download  

         1 = already downloaded  

    -   **Details:** Specifies whether Setup prerequisite files have already been downloaded. For example, if you use a value of 0, Setup downloads the files.  

-   **Key Name:** PrerequisitePath  

    -   **Required:** Yes  

    -   **Values:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Specifies the path to the Setup prerequisite files. Depending on the **PrerequisiteComp** value, Setup uses this path to store downloaded files or to locate previously downloaded files.  

##  <a name="bkmk_Unattended"></a> Unattended Setup script file keys  
 Use the following sections to help you to create your script for unattended Setup. The tables list the available Setup script keys, their corresponding values, whether they are required, which type of installation they are used for, and a short description for the key.  

### Unattended install for a central administration site  
 Use the following details to install a central administration site by using an unattended Setup script file.  

**Identification**  

-   **Key Name:** Action  

    -   **Required:** Yes  

    -   **Values:** InstallCAS  

    -   **Details:** Installs a central administration site.  

**Options**  

-   **Key Name:** ProductID  

    -   **Required:** Yes  

    -   **Values:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* or  *Eval*  

    -   **Details:** Specifies the Configuration Manager installation product key, including the dashes. Enter **Eval** to install the evaluation version of Configuration Manager.  

-   **Key Name:** SiteCode  

    -   **Required:** Yes  

    -   **Values:** &lt;*SiteCode*>  

    -   **Details:** Specifies three alphanumeric characters that uniquely identify the site in your hierarchy.  

-   **Key Name:** SiteName  

    -   **Required:** Yes  

    -   **Values:** &lt;*SiteName*>  

    -   **Details:** Specifies the name for this site.  

-   **Key Name:** SMSInstallDir  

    -   **Required:** Yes  

    -   **Values:** *ConfigMgrInstallationPath*  

    -   **Details:** Specifies the installation folder for the Configuration Manager program files.  

-   **Key Name:** SDKServer  

    -   **Required:** Yes  

    -   **Values:** &lt;*FQDN of SMS Provider*>  

    -   **Details:** Specifies the FQDN for the server that will host the SMS Provider.  
        You can configure additional SMS Providers for the site after the initial installation.  

-   **Key Name:** PrerequisiteComp  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = download  

         1 = already downloaded  

    -   **Details:** Specifies whether Setup prerequisite files have already been downloaded. For example, if you use a value of 0, Setup will download the files.  

-   **Key Name:** PrerequisitePath  

    -   **Required:** Yes  

    -   **Values:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Specifies the path to the Setup prerequisite files. Depending on the PrerequisiteComp value, Setup uses this path to store downloaded files or to locate previously downloaded files.  

-   **Key Name:** AdminConsole  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies whether to install the Configuration Manager console.  

-   **Key Name:** JoinCEIP  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not join  

         1 = join  

    -   **Details:** Specifies whether to join the Customer Experience Improvement Program.  

-   **Key Name:** AddServerLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Specifies the server languages that will be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default.  

-   **Key Name:** AddClientLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Specifies the languages that will be available to client computers. English is available by default.  

-   **Key Name:** DeleteServerLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Modifies a site after it is installed.  
        Specifies the languages to remove that will no longer be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default and cannot be removed.  

-   **Key Name:** DeleteClientLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Modifies a site after it is installed.  
        Specifies the languages to remove that will no longer be available to client computers. English is available by default and cannot be removed.  

-   **Key Name:** MobileDeviceLanguage  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies whether the mobile device client languages are installed.  

**SQLConfigOptions**  

-   **Key Name:** SQLServerName  

    -   **Required:** Yes  

    -   **Values:** *SQLServerName*  

    -   **Details:** Specifies the name of the server, or name of the clustered instance, that is running SQL Server. It will host the site database.  

-   **Key Name:** DatabaseName  

    -   **Required:** Yes  

    -   **Values:** *&lt;SiteDatabaseName\>* or *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **Details:**  

         Specifies the name of the SQL Server database to create or use to install the central administration site database.  

        > [!IMPORTANT]  
        >  You must specify the instance name and site database name if you do not use the default instance.  

-   **Key Name:** SQLSSBPort  

    -   **Required:** No  

    -   **Values:** &lt;*SSBPortNumber*>  

    -   **Details:** Specifies the SQL Server Service Broker (SSB) port that SQL Server uses. Typically, SSB is configured to use TCP port 4022, but other ports are supported.  

-   **Key Name:** SQLDataFilePath  

    -   **Required:** No  

    -   **Values:** &lt;*FilePath to database .MDB file*>  

    -   **Details:** Specifies an alternate location to create the database .MDB file.  

-   **Key Name:** SQLLogFilePath  

    -   **Required:** No  

    -   **Values:** &lt;*FilePath to database .LDF file*>  

    -   **Details:** Specifies an alternate location to create the database .LDF file.  

**CloudConnectorOptions**  

-   **Key Name:** CloudConnector  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies if you will install a service connection point at this site. Because the service connection point can only be installed at the top-tier site of a hierarchy, this value must be 0 for a child primary site.  

-   **Key Name:** CloudConnectorServer  

    -   **Required:** Required when CloudConnector equals 1  

    -   **Values:** &lt;*Service connection point server FQDN*>  

    -   **Details:** Specifies the FQDN of the server that will host the service connection point site system role.  

-   **Key Name:** UseProxy  

    -   **Required:** Required when CloudConnector equals 1  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies if the service connection point will use a proxy server.  

-   **Key Name:** ProxyName  

    -   **Required:** Required when UseProxy equals 1  

    -   **Values:** &lt;*Proxy server FQDN*>  

    -   **Details:** Specifies the FQDN of the proxy server that will be used by the service connection point site system role.  

-   **Key Name:** ProxyPort  

    -   **Required:** Required when UseProxy equals 1  

    -   **Values:** &lt;*PortNumber*>  

    -   **Details:** Specifies the port number to use.  

### Unattended install for a primary site  
Use the following details to install a primary site by using an unattended Setup script file.  

Use the following details to install a central administration site by using an unattended Setup script file.  

**Identification**  

-   **Key Name:** Action  

    -   **Required:** Yes  

    -   **Values:** InstallPrimarySite  

    -   **Details:** Installs a primary site.  

**Options**  

-   **Key Name:** ProductID  

    -   **Required:** Yes  

    -   **Values:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* or  *Eval*  

    -   **Details:** Specifies the Configuration Manager installation product key, including the dashes. Enter **Eval** to install the evaluation version of Configuration Manager.  

-   **Key Name:** SiteCode  

    -   **Required:** Yes  

    -   **Values:** &lt;*SiteCode*>  

    -   **Details:** Specifies three alphanumeric characters that uniquely identify the site in your hierarchy.  

-   **Key Name:** SiteName  

    -   **Required:** Yes  

    -   **Values:** &lt;*SiteName*>  

    -   **Details:** Specifies the name for this site.  

-   **Key Name:** SMSInstallDir  

    -   **Required:** Yes  

    -   **Values:** *ConfigMgrInstallationPath*  

    -   **Details:** Specifies the installation folder for the Configuration Manager program files.  

-   **Key Name:** SDKServer  

    -   **Required:** Yes  

    -   **Values:** &lt;*FQDN of SMS Provider*>  

    -   **Details:** Specifies the FQDN for the server that will host the SMS Provider.  
        You can configure additional SMS Providers for the site after the initial installation.  

-   **Key Name:** PrerequisiteComp  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = download  

         1 = already downloaded  

    -   **Details:** Specifies whether Setup prerequisite files have already been downloaded. For example, if you use a value of 0, Setup will download the files.  

-   **Key Name:** PrerequisitePath  

    -   **Required:** Yes  

    -   **Values:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Specifies the path to the Setup prerequisite files. Depending on the **PrerequisiteComp** value, Setup uses this path to store downloaded files or to locate previously downloaded files.  

-   **Key Name:** AdminConsole  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies whether to install the Configuration Manager console.  

-   **Key Name:** JoinCEIP  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not join  

         1 = join  

    -   **Details:** Specifies whether to join the Customer Experience Improvement Program.  

-   **Key Name:** ManagementPoint  

    -   **Required:** No  

    -   **Values:** &lt;*Management point site server FQDN*>  

    -   **Details:** Specifies the FQDN of the server that will host the management point site system role.  

-   **Key Name:** ManagementPointProtocol  

    -   **Required:** No  

    -   **Values:** HTTPS or HTTP  

    -   **Details:** Specifies the protocol to use for the management point.  

-   **Key Name:** DistributionPoint  

    -   **Required:** No  

    -   **Values:** &lt;*Distribution Point site server FQDN*>  

    -   **Details:** Specifies the protocol to use for the management point.  

-   **Key Name:** DistributionPointProtocol  

    -   **Required:** No  

    -   **Values:** HTTPS or HTTP  

    -   **Details:** Specifies the protocol to use for the distribution point.  

-   **Key Name:** RoleCommunicationProtocol  

    -   **Required:** Yes  

    -   **Values:** EnforceHTTPS or HTTPorHTTPS  

    -   **Details:** Specifies whether to configure all site systems to accept only HTTPS communication from clients or for the communication method to be configured for each site system role. When you select to **EnforceHTTPS**, client computer must have a valid PKI certificate for client authentication.  

-   **Key Name:** ClientsUsePKICertificate  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not use  

         1 = use  

    -   **Details:** Specifies whether clients will use a client PKI certificate to communicate with site system roles.  

-   **Key Name:** AddServerLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Specifies the server languages that will be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default.  

-   **Key Name:** AddClientLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Specifies the languages that will be available to client computers. English is available by default.  

-   **Key Name:** DeleteServerLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Modifies a site after it is installed.  
        Specifies the languages to remove that will no longer be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default and cannot be removed.  

-   **Key Name:** DeleteClientLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Modifies a site after it is installed.  
        Specifies the languages to remove that will no longer be available to client computers. English is available by default and cannot be removed.  

-   **Key Name:** MobileDeviceLanguage  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies whether the mobile device client languages are installed.  

**SQLConfigOptions**  

-   **Key Name:** SQLServerName  

    -   **Required:** Yes  

    -   **Values:** *SQLServerName*  

    -   **Details:** Specifies the name of the server, or name of the clustered instance, that is running SQL Server. It will host the site database.  

-   **Key Name:** DatabaseName  

    -   **Required:** Yes  

    -   **Values:** *&lt;SiteDatabaseName\>* or *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **Details:**  

         Specifies the name of the SQL Server database to create or use to install the primary site database.  

        > [!IMPORTANT]  
        >  You must specify the instance name and site database name if you do not use the default instance.  

-   **Key Name:** SQLSSBPort  

    -   **Required:** No  

    -   **Values:** &lt;*SSBPortNumber*>  

    -   **Details:** Specifies the SQL Server Service Broker (SSB) port that SQL Server uses. Typically, SSB is configured to use TCP port 4022, but other ports are supported.  

-   **Key Name:** SQLDataFilePath  

    -   **Required:** No  

    -   **Values:** &lt;*FilePath to database .MDB file*>  

    -   **Details:** Specifies an alternate location to create the database .MDB file.  

-   **Key Name:** SQLLogFilePath  

    -   **Required:** No  

    -   **Values:** &lt;*FilePath to database .LDF file*>  

    -   **Details:** Specifies an alternate location to create the database .LDF file.  

**HierarchyExpansionOption**  

-   **Key Name:** CCARSiteServer  

    -   **Required:** No  

    -   **Values:** &lt;*FQDN of central administration site*>  

    -   **Details:** Specifies the central administration site that a primary site will attach to when it joins the Configuration Manager hierarchy. You must specify the central administration site during Setup.  

-   **Key Name:** CASRetryInterval  

    -   **Required:** No  

    -   **Values:** &lt;*Interval*>  

    -   **Details:** Specifies the retry interval (in minutes) to attempt a connection to the central administration site after the connection fails. For example, if the connection to the central administration site fails, the primary site waits the number of minutes that you specify for CASRetryInterval, and then re-attempts the connection.  

-   **Key Name:** WaitForCASTimeout  

    -   **Required:** No  

    -   **Values:** &lt;*Timeout*>  

         A value of 0 to 100  

    -   **Details:** Specifies the maximum time-out value (in minutes) for a primary site to connect to the central administration site. For example, if a primary site fails to connect to a central administration site, the primary site retries the connection to the central administration site, based on the CASRetryInterval until the WaitForCASTimeout period is reached. You can specify a value of 0 to 100.  

**CloudConnectorOptions**  

-   **Key Name:** CloudConnector  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies if you will install a service connection point at this site. Because the service connection point can only be installed at the top-tier site of a hierarchy, this value must be 0 for a child primary site.  

-   **Key Name:** CloudConnectorServer  

    -   **Required:** Required when CloudConnector equals 1  

    -   **Values:** &lt;*Service connection point server FQDN*\>  

    -   **Details:** Specifies the FQDN of the server that will host the service connection point site system role.  

-   **Key Name:** UseProxy  

    -   **Required:** Required when CloudConnector equals 1  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies if the service connection point will use a proxy server.  

-   **Key Name:** ProxyName  

    -   **Required:** Required when UseProxy equals 1  

    -   **Values:** &lt;*Proxy server FQDN*>  

    -   **Details:** Specifies the FQDN of the proxy server that will be used by the service connection point site system role.  

-   **Key Name:** ProxyPort  

    -   **Required:** Required when UseProxy equals 1  

    -   **Values:** &lt;*PortNumber*>  

    -   **Details:** Specifies the port number to use.  

### Unattended recovery for a central administration site  
 Use the following details to recover a central administration site by using an unattended Setup script file.  

**Identification**  

-   **Key Name:** Action  

    -   **Required:** Yes  

    -   **Values:** RecoverCCAR  

    -   **Details:** Recovers a central administration site.  

**RecoveryOptions**  

-   **Key Name:** ServerRecoveryOptions  

    -   **Required:** Yes  

    -   **Values:** 1, 2, or 4  

         1 = Recovery site server and SQL Server.  

         2 = Recover site server only.  

         4 = Recover SQL Server only.  

    -   **Details:** Specifies whether Setup will recover the site server, SQL Server, or both. The associated keys are required when you set the following value for the ServerRecoveryOptions setting:  

        -   Value = 1: You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

        -   Value = 2: You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

        -   Value = 4: The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.  

-   **Key Name:** DatabaseRecoveryOptions  

    -   **Required:** This key is required when the ServerRecoveryOptions setting has a value of **1** or **4**.  

    -   **Values:** 10, 20, 40, 80  

         10 = Restore the site database from backup.  

         20 = Use a site database that has been manually recovered by using another method.  

         40 = Create a new database for the site. Use this option when there is no site database backup available. Global and site data is recovered through replication from other sites.  

         80 = skip database recovery.  

    -   **Details:** Specifies how Setup recovers the site database in SQL Server.  

-   **Key Name:** ReferenceSite  

    -   **Required:** This key is required when the **DatabaseRecoveryOptions** setting has a value of **40**.  

    -   **Values:** &lt;*ReferenceSiteFQDN*>  

    -   **Details:** Specifies the reference primary site that the central administration site uses to recover global data if the database backup is older than the change tracking retention period or when you recover the site without a backup.  

         When you do not specify a reference site and the backup is older than the change tracking retention period, all primary sites are reinitialized with the restored data from the central administration site.  

         When you do not specify a reference site and the backup is within the change tracking retention period, only changes after the backup are replicated from primary sites. When there are conflicting changes from different primary sites, the central administration site uses the first one that it receives.  

-   **Key Name:** SiteServerBackupLocation  

    -   **Required:** No  

    -   **Values:** &lt;*PathToSiteServerBackupSet*>  

    -   **Details:** Specifies the path to the site server backup set. This key is optional when the **ServerRecoveryOptions** setting has a value of **1** or **2**. Specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

-   **Key Name:** BackupLocation  

    -   **Required:** This key is required when you configure a value of **1** or **4** for the **ServerRecoveryOptions** key, and configure a value of **10** for the **DatabaseRecoveryOptions** key.  

    -   **Values:** &lt;*PathToSiteDatabaseBackupSet*>  

    -   **Details:** Specifies the path to the site database backup set.  

**Options**  

-   **Key Name:** ProductID  

    -   **Required:** Yes  

    -   **Values:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* or  *Eval*  

    -   **Details:** Specifies the Configuration Manager installation product key, including the dashes. Enter **Eval** to install the evaluation version of Configuration Manager.  

-   **Key Name:** SiteCode  

    -   **Required:** Yes  

    -   **Values:** &lt;*SiteCode*>  

    -   **Details:** Specifies three alphanumeric characters that uniquely identify the site in your hierarchy. You must specify the site code that the site used before the failure. For more information about site code restrictions, see [About site names and site codes](#bkmk_codes) section in this topic.  

-   **Key Name:** SiteName  

    -   **Required:** No  

    -   **Values:** &lt;*SiteName*>  

    -   **Details:** Specifies the name for this site.  

-   **Key Name:** SMSInstallDir  

    -   **Required:** Yes  

    -   **Values:** &lt;*ConfigMgrInstallationPath*>  

    -   **Details:** Specifies the installation folder for the Configuration Manager program files.  

-   **Key Name:** SDKServer  

    -   **Required:** Yes  

    -   **Values:** &lt;*FQDN of SMS Provider*>  

    -   **Details:** Specifies the FQDN for the server that will host the SMS Provider. You must specify the server that hosted the SMS Provider before the failure.  

         You can configure additional SMS Providers for the site after the initial installation. For more information about the SMS Provider, see [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Key Name:** PrerequisiteComp  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = download  

         1 = already downloaded  

    -   **Details:** Specifies whether Setup prerequisite files have already been downloaded. For example, if you use a value of **0**, Setup downloads the files.  

-   **Key Name:** PrerequisitePath  

    -   **Required:** Yes  

    -   **Values:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Specifies the path to the Setup prerequisite files. Depending on the **PrerequisiteComp** value, Setup uses this path to store downloaded files or to locate previously downloaded files.  

-   **Key Name:** AdminConsole  

    -   **Required:** This key is required except when the **ServerRecoveryOptions** setting has a value of **4**.  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies whether to install the Configuration Manager console.  

-   **Key Name:** JoinCEIP  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not join  

         1 = join  

    -   **Details:** Specifies whether to join the Customer Experience Improvement Program.  

**SQLConfigOptions**  

-   **Key Name:** SQLServerName  

    -   **Required:** Yes  

    -   **Values:** *SQLServerName*  

    -   **Details:**Specifies the name of the server, or name of the clustered instance that is running SQL Server that will host the site database. You must specify the same server that hosted the site database before the failure.  

-   **Key Name:** DatabaseName  

    -   **Required:** Yes  

    -   **Values:** *&lt;SiteDatabaseName\>* or *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **Details:**  

         Specifies the name of the SQL Server database to create or use to install the central administration site database. You must specify the same database name that was used before the failure.  

        > [!IMPORTANT]  
        >  You must specify the instance name and site database name if you do not use the default instance.  

-   **Key Name:** SQLSSBPort  

    -   **Required:** Yes  

    -   **Values:** &lt;*SSBPortNumber*>  

    -   **Details:** Specifies the SQL Server Service Broker (SSB) port that SQL Server uses. Typically, SSB is configured to use TCP port 4022. You must specify the same SSB port that was used before the failure.  

-   **Key Name:** SQLDataFilePath  

    -   **Required:** No  

    -   **Values:** &lt;*FilePath to database .MDB file*>  

    -   **Details:** Specifies an alternate location to create the database .MDB file.  

-   **Key Name:** SQLLogFilePath  

    -   **Required:** No  

    -   **Values:** &lt;*FilePath to database .LDF file*>  

    -   **Details:** Specifies an alternate location to create the database .LDF file.  

**CloudConnectorOptions**  

-   **Key Name:** CloudConnector  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies if you will install a service connection point at this site. Because the service connection point can only be installed at the top-tier site of a hierarchy, this value must be 0 for a child primary site.  

-   **Key Name:** CloudConnecorServer  

    -   **Required:** Required when CloudConnector equals 1  

    -   **Values:** &lt;*Service connection point server FQDN*>  

    -   **Details:** Specifies the FQDN of the server that will host the service connection point site system role.  

-   **Key Name:** UseProxy  

    -   **Required:** Required when CloudConnector equals 1  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies if the service connection point will use a proxy server.  

-   **Key Name:** ProxyName  

    -   **Required:** Required when CloudConnector equals 1  

    -   **Values:** &lt;*Proxy server FQDN*>  

    -   **Details:** Specifies the FQDN of the proxy server that will be used by the service connection point site system role.  

-   **Key Name:** ProxyPort  

    -   **Required:** Required when CloudConnector equals 1  

    -   **Values:** &lt;*PortNumber*>  

    -   **Details:** Specifies the port number to use.  

### Unattended recovery for a primary site  
 Use the following details to recover a primary site by using an unattended Setup script file.  

**Identification**  

-   **Key Name:** Action  

    -   **Required:** Yes  

    -   **Values:** RecoverPrimarySite  

    -   **Details:** Recovers a primary site.  

**RecoveryOptions**  

-   **Key Name:** ServerRecoveryOptions  

    -   **Required:** Yes  

    -   **Values:** 1, 2, or 4  

         1 = Recovery site server and SQL Server.  

         2 = Recover site server only.  

         4 = Recover SQL Server only.  

    -   **Details:** Specifies whether Setup will recover the site server, SQL Server, or both. The associated keys are required when you set the following value for the ServerRecoveryOptions setting:  

        -   Value = 1: You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

        -   Value = 2: You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

        -   Value = 4: The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.  

-   **Key Name:** DatabaseRecoveryOptions  

    -   **Required:** This key is required when the ServerRecoveryOptions setting has a value of **1** or **4**.  

    -   **Values:** 10, 20, 40, 80  

         10 = Restore the site database from backup.  

         20 = Use a site database that has been manually recovered by using another method.  

         40 = Create a new database for the site. Use this option when there is no site database backup available. Global and site data is recovered through replication from other sites.  

         80 = skip database recovery.  

    -   **Details:** Specifies how Setup recovers the site database in SQL Server.  

-   **Key Name:** SiteServerBackupLocation  

    -   **Required:** No  

    -   **Values:** &lt;*PathToSiteServerBackupSet*>  

    -   **Details:**  

         Specifies the path to the site server backup set. This key is optional when the **ServerRecoveryOptions** setting has a value of **1** or **2**. Specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

-   **Key Name:** BackupLocation  

    -   **Required:** This key is required when you configure a value of **1** or **4** for the **ServerRecoveryOptions** key, and configure a value of **10** for the **DatabaseRecoveryOptions** key.  

    -   **Values:** &lt;*PathToSiteDatabaseBackupSet*>  

    -   **Details:** Specifies the path to the site database backup set.  

**Options**  

-   **Key Name:** ProductID  

    -   **Required:** Yes  

    -   **Values:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* or  *Eval*  

    -   **Details:** Specifies the Configuration Manager installation product key, including the dashes. Enter **Eval** to install the evaluation version of Configuration Manager.  

-   **Key Name:** SiteCode  

    -   **Required:** Yes  

    -   **Values:** &lt;*SiteCode*>  

    -   **Details:** Specifies three alphanumeric characters that uniquely identify the site in your hierarchy. You must specify the site code that the site used before the failure. For more information about site code restrictions, see [About site names and site codes](#bkmk_codes) section in this topic.  

-   **Key Name:** SiteName  

    -   **Required:** No  

    -   **Values:** &lt;*SiteName*>  

    -   **Details:** Specifies the name for this site.  

-   **Key Name:** SMSInstallDir  

    -   **Required:** Yes  

    -   **Values:** &lt;*ConfigMgrInstallationPath*>  

    -   **Details:** Specifies the installation folder for the Configuration Manager program files.  

-   **Key Name:** SDKServer  

    -   **Required:** Yes  

    -   **Values:** &lt;*FQDN of SMS Provider*>  

    -   **Details:** Specifies the FQDN for the server that will host the SMS Provider. You must specify the server that hosted the SMS Provider before the failure. You can configure additional SMS Providers for the site after the initial installation. For more information about the SMS Provider, see [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Key Name:** PrerequisiteComp  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = download  

         1 = already downloaded  

    -   **Details:** Specifies whether Setup prerequisite files have already been downloaded. For example, if you use a value of **0**, Setup downloads the files.  

-   **Key Name:** PrerequisitePath  

    -   **Required:** Yes  

    -   **Values:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Specifies the path to the Setup prerequisite files. Depending on the **PrerequisiteComp** value, Setup uses this path to store downloaded files or to locate previously downloaded files.  

-   **Key Name:** AdminConsole  

    -   **Required:** This key is required except when the **ServerRecoveryOptions** setting has a value of **4**.  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies whether to install the Configuration Manager console.  

-   **Key Name:** JoinCEIP  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not join  

         1 = join  

    -   **Details:** Specifies whether to join the Customer Experience Improvement Program.  

**SQLConfigOptions**  

-   **Key Name:** SQLServerName  

    -   **Required:** Yes  

    -   **Values:** *SQLServerName*  

    -   **Details:**Specifies the name of the server, or name of the clustered instance that is running SQL Server that will host the site database. You must specify the same server that hosted the site database before the failure.  

-   **Key Name:** DatabaseName  

    -   **Required:** Yes  

    -   **Values:**  &lt;*SiteDatabaseName*\> or                                &lt;*InstanceName*\>\\&lt;*SiteDatabaseName*\>

    -   **Details:**  

         Specifies the name of the SQL Server database to create or use to install the central administration site database. You must specify the same database name that was used before the failure.  

        > [!IMPORTANT]  
        >  You must specify the instance name and site database name if you do not use the default instance.  

-   **Key Name:** SQLSSBPort  

    -   **Required:** Yes  

    -   **Values:** &lt;*SSBPortNumber*>  

    -   **Details:** Specifies the SQL Server Service Broker (SSB) port that SQL Server uses. Typically, SSB is configured to use TCP port 4022. You must specify the same SSB port that was used before the failure.  

-   **Key Name:** SQLDataFilePath  

    -   **Required:** No  

    -   **Values:** &lt;*FilePath to database .MDB file*>  

    -   **Details:** Specifies an alternate location to create the database .MDB file.  

-   **Key Name:** SQLLogFilePath  

    -   **Required:** No  

    -   **Values:** &lt;*FilePath to database .LDF file*>  

    -   **Details:** Specifies an alternate location to create the database .LDF file.  

**HierarchyExpansionOptions**  

-   **Key Name:** CCARSiteServer  

    -   **Required:** See details.  

    -   **Values:** &lt;*SiteCodeForCentralAdministrationSite*>  

    -   **Details:** Specifies the central administration site to which a primary site attaches when it joins the Configuration Manager hierarchy. This setting is required if the primary site was attached to a central administration site before the failure. You must specify the site code that was used for the central administration site before the failure.  

-   **Key Name:** CASRetryInterval  

    -   **Required:** No  

    -   **Values:** &lt;*Interval*>  

    -   **Details:** Specifies the retry interval (in minutes) to attempt a connection to the central administration site after the connection fails. For example, if the connection to the central administration site fails, the primary site waits the number of minutes that you specify for **CASRetryInterval**, and then attempts the connection again.  

-   **Key Name:** WaitForCASTimeout  

    -   **Required:** No  

    -   **Values:** &lt;*Timeout*>  

    -   **Details:** Specifies the maximum time-out value (in minutes) for a primary site to connect to the central administration site. For example, if a primary site fails to connect to a central administration site, the primary site retries the connection to the central administration site, based on the **CASRetryInterval** until the **WaitForCASTimeout** period is reached. You can specify a value of 0 to 100.  

**CloudConnectorOptions**  

-   **Key Name:** CloudConnector  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies if you will install a service connection point at this site. Because the service connection point can only be installed at the top-tier site of a hierarchy, this value must be 0 for a child primary site.  

-   **Key Name:** CloudConnecorServer  

    -   **Required:** Required when CloudConnector equals 1  

    -   **Values:** &lt;*Service connection point server FQDN*>  

    -   **Details:** Specifies the FQDN of the server that will host the service connection point site system role.  

-   **Key Name:** UseProxy  

    -   **Required:** Required when CloudConnector equals 1  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies if the service connection point will use a proxy server.  

-   **Key Name:** ProxyName  

    -   **Required:** Required when CloudConnector equals 1  

    -   **Values:** &lt;*Proxy server FQDN*>  

    -   **Details:** Specifies the FQDN of the proxy server that will be used by the service connection point site system role.  

-   **Key Name:** ProxyPort  

    -   **Required:** Required when CloudConnector equals 1  

    -   **Values:** &lt;*PortNumber*>  

    -   **Details:** Specifies the port number to use.  
