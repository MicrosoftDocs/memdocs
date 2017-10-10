---
title: "Setup command-line options"
description: "Use information in this article to configure scripts or to install System Center Configuration Manager from a command line."
ms.custom: na
ms.date: 03/27/2017
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
# Command-line options for Setup in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*

 Use the following information to configure scripts or to install System Center Configuration Manager from a command line.  

##  <a name="bkmk_setup"></a> Command-line options for Setup  
 **/DEINSTALL**  
 Uninstalls the site. You must run Setup from the site server computer.  

 **/DONTSTARTSITECOMP**  
 Installs a site, but prevents the Site Component Manager service from starting. Until the Site Component Manager service starts, the site is not active. The Site Component Manager is responsible for installing and starting the SMS_Executive service, and for additional processes at the site. After the site install is finished, when you start the Site Component Manager service, it installs the SMS_Executive service and additional processes that are necessary for the site to operate.  

 **/HIDDEN**  
 Hides the user interface during Setup. Use this option only in conjunction with the **/SCRIPT** option. The unattended script file must provide all required options or Setup fails.  

 **/NOUSERINPUT**  
 Disables user input during Setup, but displays the Setup Wizard. Use this option only in conjunction with the **/SCRIPT** option. The unattended script file must provide all required options or Setup fails.  

 **/RESETSITE**  
 Performs a site reset that resets the database and service accounts for the site. You must run Setup from **<*Configuration Manager installation path*>\BIN\X64** on the site server. For more information about the site reset, see the [Run a site reset](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) section in [Modify your System Center Configuration Manager infrastructure](../../../../core/servers/manage/modify-your-infrastructure.md).  

 **/TESTDBUPGRADE <*Instance name*>\\<*Database name*>**  
 Performs a test on a backup of the site database to ensure that the database is capable of an upgrade. You must provide the instance name and database name for the site database. If you specify only the database name, Setup uses the default instance name.  

> [!IMPORTANT]  
>  Do not run this command-line option on your production site database. Running this command-line option on your production site database upgrades the site database and could render your site inoperable.  

 **/UPGRADE**  
 Runs an unattended upgrade of a site. When you use **/UPGRADE**, you must specify the product key, including the dashes (-). Also, you must specify the path to the previously downloaded Setup prerequisite files.  

 Example: `setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

 For more information about Setup prerequisite files, see  [Setup Downloader](setup-downloader.md).  

 **/SCRIPT <*Setup script path*>**  
 Performs unattended installations. A Setup initialization file is required when you use the **/SCRIPT** option. For more information about how to run Setup unattended, see [Install sites using a command line](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/SDKINST <*SMS Provider FQDN*>**  
 Installs the SMS Provider on the specified computer. You must provide the fully qualified domain name (FQDN) for the SMS Provider computer. For more information about the SMS Provider, see [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/SDKDEINST <*SMS Provider FQDN*>**  
 Uninstalls the SMS Provider on the specified computer. You must provide the FQDN for the SMS Provider computer.  

 **/MANAGELANGS <*Language script path*>**  
 Manages the languages that are installed at a previously installed site. To use this option, you must run Setup from **<*Configuration Manager installation path*>\BIN\X64** on the site server and provide the location for the language script file that contains the language settings. For more information about the language options available in the language setup script file, see [Command-line options to manage languages](#bkmk_Lang) in this topic.  

##  <a name="bkmk_Lang"></a> Command-line options to manage languages  
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

    -   **Details:** Specifies the languages to remove, and which will no longer be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default and cannot be removed.  

-   **Key Name:** DeleteClientLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Specifies the languages to remove, and which will no longer be available to client computers. English is available by default and cannot be removed.  

-   **Key Name:** MobileDeviceLanguage  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether the mobile device client languages are installed.  

-   **Key Name:** PrerequisiteComp  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Download  

         1 = Already downloaded  

    -   **Details:** Specifies whether Setup prerequisite files have already been downloaded. For example, if you use a value of **0**, Setup downloads the files.  

-   **Key Name:** PrerequisitePath  

    -   **Required:** Yes  

    -   **Values:** <*Path to Setup prerequisite files*>  

    -   **Details:** Specifies the path to the Setup prerequisite files. Depending on the **PrerequisiteComp** value, Setup uses this path to store downloaded files or to locate previously downloaded files.  

##  <a name="bkmk_Unattended"></a> Unattended Setup script file keys  
 Use the following sections to help you create your script for unattended Setup. The lists show the available Setup script keys, their corresponding values, whether they are required, which type of installation they are used for, and a short description of the key.  

### Unattended install for a central administration site  
 Use the following details to install a central administration site by using an unattended Setup script file.  

**Identification**  

-   **Key Name:** Action  

    -   **Required:** Yes  

    -   **Values:** InstallCAS  

    -   **Details:** Installs a central administration site.  

-   **Key Name:** CDLatest  

    -   **Required:** Yes – Only when using media from the CD.Latest folder.    

    -   **Values:** 1
        Any value other than 1 is considered to not be using CD.Latest.

    -   **Details:** Your script must include this key and value when you run setup from media in a CD.Latest folder for the purpose of installing a primary or central administration site, or recovering a primary or central administration site. This value informs setup that media form CD.Latest is being used.

**Options**  

-   **Key Name:** ProductID  

    -   **Required:** Yes  

    -   **Values:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *or* Eval  

    -   **Details:** Specifies the Configuration Manager installation product key, including the dashes. Enter **Eval** to install the evaluation version of Configuration Manager.  

-   **Key Name:** SiteCode  

    -   **Required:** Yes  

    -   **Values:** <*Site code*>  

    -   **Details:** Specifies three alphanumeric characters that uniquely identify the site in your hierarchy.  

-   **Key Name:** Site name  

    -   **Required:** Yes  

    -   **Values:** <*Site name*>  

    -   **Details:** Specifies the name for this site.  

-   **Key Name:** SMSInstallDir  

    -   **Required:** Yes  

    -   **Values:** <*Configuration Manager installation path*>  

    -   **Details:** Specifies the installation folder for the Configuration Manager program files.  

-   **Key Name:** SDKServer  

    -   **Required:** Yes  

    -   **Values:** <*SMS Provider FQDN*>  

    -   **Details:** Specifies the FQDN for the server that will host the SMS Provider. You can configure additional SMS Providers for the site after the initial installation.  

-   **Key Name:** PrerequisiteComp  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Download  

         1 = Already downloaded  

    -   **Details:** Specifies whether Setup prerequisite files have already been downloaded. For example, if you use a value of **0**, Setup will download the files.  

-   **Key Name:** PrerequisitePath  

    -   **Required:** Yes  

    -   **Values:** <*Path to Setup prerequisite files*>  

    -   **Details:** Specifies the path to the Setup prerequisite files. Depending on the **PrerequisiteComp** value, Setup uses this path to store downloaded files or to locate previously downloaded files.  

-   **Key Name:** AdminConsole  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether to install the Configuration Manager console.  

-   **Key Name:** JoinCEIP  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not join  

         1 = Join  

    -   **Details:** Specifies whether to join the Customer Experience Improvement Program (CEIP).  

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

    -   **Details:** Modifies a site after it is installed. Specifies the languages to remove, and which will no longer be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default and cannot be removed.  

-   **Key Name:** DeleteClientLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Modifies a site after it is installed. Specifies the languages to remove, and which will no longer be available to client computers. English is available by default and cannot be removed.  

-   **Key Name:** MobileDeviceLanguage  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether the mobile device client languages are installed.  

**SQLConfigOptions**  

-   **Key Name:** SQLServerName  

    -   **Required:** Yes  

    -   **Values:** <*SQL server name*>  

    -   **Details:** Specifies the name of the server or clustered instance that is running SQL Server, and which will host the site database.  

-   **Key Name:** DatabaseName  

    -   **Required:** Yes  

    -   **Values:** <*Site database name*> or <*Instance name*>\\<*Site database name*>  

    -   **Details:** Specifies the name of the SQL Server database to create or the SQL Server database to use when installing the central administration site database.  

        > [!IMPORTANT]  
        >  You must specify the instance name and site database name if you do not use the default instance.  

-   **Key Name:** SQLSSBPort  

    -   **Required:** No  

    -   **Values:** <*SSB port number*>  

    -   **Details:** Specifies the SQL Server Service Broker (SSB) port that SQL Server uses. SSB typically is configured to use TCP port 4022, but you can use a different port.  

-   **Key Name:** SQLDataFilePath  

    -   **Required:** No  

    -   **Values:** <*Path to database .mdb file*>  

    -   **Details:** Specifies an alternate location to create the database .mdb file.  

-   **Key Name:** SQLLogFilePath  

    -   **Required:** No  

    -   **Values:** <*Path to database .ldf file*>  

    -   **Details:** Specifies an alternate location to create the database .ldf file.  

**CloudConnectorOptions**  

-   **Key Name:** CloudConnector  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether to install a service connection point at this site. Because the service connection point can only be installed at the top-tier site of a hierarchy, this value must be **0** for a child primary site.  

-   **Key Name:** CloudConnectorServer  

    -   **Required:** Required when **CloudConnector** equals 1  

    -   **Values:** <*Service connection point server FQDN*>  

    -   **Details:** Specifies the FQDN of the server that will host the service connection point site system role.  

-   **Key Name:** UseProxy  

    -   **Required:** Required when **CloudConnector** equals 1  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether the service connection point will use a proxy server.  

-   **Key Name:** ProxyName  

    -   **Required:** Required when **UseProxy** equals 1  

    -   **Values:** <*Proxy server FQDN*>  

    -   **Details:** Specifies the FQDN of the proxy server that will be used by the service connection point site system role.  

-   **Key Name:** ProxyPort  

    -   **Required:** Required when **UseProxy** equals 1  

    -   **Values:** <*Port number*>  

    -   **Details:** Specifies the port number to use for the proxy port.  

### Unattended install for a primary site  
Use the following details to install a primary site by using an unattended Setup script file.  

**Identification**  

-   **Key Name:** Action  

    -   **Required:** Yes  

    -   **Values:** InstallPrimarySite  

    -   **Details:** Installs a primary site.  

-   **Key Name:** CDLatest  

    -   **Required:** Yes – Only when using media from the CD.Latest folder.    

    -   **Values:** 1
        Any value other than 1 is considered to not be using CD.Latest.

    -   **Details:** Your script must include this key and value when you run setup from media in a CD.Latest folder for the purpose of installing a primary or central administration site, or recovering a primary or central administration site. This value informs setup that media form CD.Latest is being used.

**Options**  

-   **Key Name:** ProductID  

    -   **Required:** Yes  

    -   **Values:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *or* Eval  

    -   **Details:** Specifies the Configuration Manager installation product key, including the dashes. Enter **Eval** to install the evaluation version of Configuration Manager.  

-   **Key Name:** SiteCode  

    -   **Required:** Yes  

    -   **Values:** <*Site code*>  

    -   **Details:** Specifies three alphanumeric characters that uniquely identify the site in your hierarchy.  

-   **Key Name:** SiteName  

    -   **Required:** Yes  

    -   **Values:** <*Site name*>  

    -   **Details:** Specifies the name for this site.  

-   **Key Name:** SMSInstallDir  

    -   **Required:** Yes  

    -   **Values:** <*Configuration Manager installation path*>

    -   **Details:** Specifies the installation folder for the Configuration Manager program files.  

-   **Key Name:** SDKServer  

    -   **Required:** Yes  

    -   **Values:** <*SMS Provider FQDN*>  

    -   **Details:** Specifies the FQDN for the server that will host the SMS Provider. You can configure additional SMS Providers for the site after the initial installation.  

-   **Key Name:** PrerequisiteComp  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Download  

         1 = Already downloaded  

    -   **Details:** Specifies whether Setup prerequisite files have already been downloaded. For example, if you use a value of **0**, Setup will download the files.  

-   **Key Name:** PrerequisitePath  

    -   **Required:** Yes  

    -   **Values:** <*Path to Setup prerequisite files*>  

    -   **Details:** Specifies the path to the Setup prerequisite files. Depending on the **PrerequisiteComp** value, Setup uses this path to store downloaded files or to locate previously downloaded files.  

-   **Key Name:** AdminConsole  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether to install the Configuration Manager console.  

-   **Key Name:** JoinCEIP  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not join  

         1 = Join  

    -   **Details:** Specifies whether to join the CEIP.  

-   **Key Name:** ManagementPoint  

    -   **Required:** No  

    -   **Values:** <*Management point site server FQDN*>  

    -   **Details:** Specifies the FQDN of the server that will host the management point site system role.  

-   **Key Name:** ManagementPointProtocol  

    -   **Required:** No  

    -   **Values:** HTTPS *or* HTTP  

    -   **Details:** Specifies the protocol to use for the management point.  

-   **Key Name:** DistributionPoint  

    -   **Required:** No  

    -   **Values:** <*Distribution point site server FQDN*>  

    -   **Details:** Specifies the protocol to use for the distribution point.  

-   **Key Name:** DistributionPointProtocol  

    -   **Required:** No  

    -   **Values:** HTTPS *or* HTTP  

    -   **Details:** Specifies the protocol to use for the distribution point.  

-   **Key Name:** RoleCommunicationProtocol  

    -   **Required:** Yes  

    -   **Values:** EnforceHTTPS *or* HTTPorHTTPS  

    -   **Details:** Specifies whether to configure all site systems to accept only HTTPS communication from clients, or for the communication method to be configured for each site system role. When you select to **EnforceHTTPS**, client computer must have a valid public key infrastructure (PKI) certificate for client authentication.  

-   **Key Name:** ClientsUsePKICertificate  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not use  

         1 = Use  

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

    -   **Details:** Modifies a site after it is installed. Specifies the languages to remove, and which will no longer be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default and cannot be removed.  

-   **Key Name:** DeleteClientLanguages  

    -   **Required:** No  

    -   **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Details:** Modifies a site after it is installed. Specifies the languages to remove, and which will no longer be available to client computers. English is available by default and cannot be removed.  

-   **Key Name:** MobileDeviceLanguage  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether the mobile device client languages are installed.  

**SQLConfigOptions**  

-   **Key Name:** SQLServerName  

    -   **Required:** Yes  

    -   **Values:** <*SQL server name*>  

    -   **Details:** Specifies the name of the server or clustered instance that is running SQL Server, and which will host the site database.  

-   **Key Name:** DatabaseName  

    -   **Required:** Yes  

    -   **Values:** <*Site database name*> or <*Instance name*>\\<*Site database name*>  

    -   **Details:** Specifies the name of the SQL Server database to create or the SQL Server database to use when installing the primary site database.  

        > [!IMPORTANT]  
        >  You must specify the instance name and site database name if you do not use the default instance.  

-   **Key Name:** SQLSSBPort  

    -   **Required:** No  

    -   **Values:** <*SSB port number*>  

    -   **Details:** Specifies the SSB port that SQL Server uses. SSB typically is configured to use TCP port 4022, but you can use a different port.  

-   **Key Name:** SQLDataFilePath  

    -   **Required:** No  

    -   **Values:** <*Path to database .mdb file*>  

    -   **Details:** Specifies an alternate location to create the database .mdb file.  

-   **Key Name:** SQLLogFilePath  

    -   **Required:** No  

    -   **Values:** <*Path to database .ldf file*>  

    -   **Details:** Specifies an alternate location to create the database .ldf file.  

**HierarchyExpansionOption**  

-   **Key Name:** CCARSiteServer  

    -   **Required:** No  

    -   **Values:** <*Central administration site FQDN*>  

    -   **Details:** Specifies the central administration site that a primary site will attach to when it joins the Configuration Manager hierarchy. You must specify the central administration site during Setup.  

-   **Key Name:** CASRetryInterval  

    -   **Required:** No  

    -   **Values:** <*Interval*>  

    -   **Details:** Specifies the retry interval (in minutes) to attempt a connection to the central administration site after the connection fails. For example, if the connection to the central administration site fails, the primary site waits the number of minutes that you specify for the **CASRetryInterval** value, and then re-attempts the connection.  

-   **Key Name:** WaitForCASTimeout  

    -   **Required:** No  

    -   **Values:** <*Timeout*>  

         A value of **0** to **100**  

    -   **Details:** Specifies the maximum timeout value (in minutes) for a primary site to connect to the central administration site. For example, if a primary site fails to connect to a central administration site, the primary site retries the connection to the central administration site based on the **CASRetryInterval** value until the **WaitForCASTimeout** period is reached. You can specify a value of **0** to **100**.  

**CloudConnectorOptions**  

-   **Key Name:** CloudConnector  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether to install a service connection point at this site. Because the service connection point can only be installed at the top-tier site of a hierarchy, this value must be **0** for a child primary site.  

-   **Key Name:** CloudConnectorServer  

    -   **Required:** Required when **CloudConnector** equals 1  

    -   **Values:** <*Service connection point server FQDN*\>  

    -   **Details:** Specifies the FQDN of the server that will host the service connection point site system role.  

-   **Key Name:** UseProxy  

    -   **Required:** Required when **CloudConnector** equals 1  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether the service connection point will use a proxy server.  

-   **Key Name:** ProxyName  

    -   **Required:** Required when **UseProxy** equals 1  

    -   **Values:** <*Proxy server FQDN*>  

    -   **Details:** Specifies the FQDN of the proxy server that will be used by the service connection point site system role.  

-   **Key Name:** ProxyPort  

    -   **Required:** Required when **UseProxy** equals 1  

    -   **Values:** <*Port number*>  

    -   **Details:** Specifies the port number to use for the proxy port.  

### Unattended recovery for a central administration site  
 Use the following details to recover a central administration site by using an unattended Setup script file.  

**Identification**  

-   **Key Name:** Action  

    -   **Required:** Yes  

    -   **Values:** RecoverCCAR  

    -   **Details:** Recovers a central administration site.  

-   **Key Name:** CDLatest  

    -   **Required:** Yes – Only when using media from the CD.Latest folder.    

    -   **Values:** 1
        Any value other than 1 is considered to not be using CD.Latest.

    -   **Details:** Your script must include this key and value when you run setup from media in a CD.Latest folder for the purpose of installing a primary or central administration site, or recovering a primary or central administration site. This value informs setup that media form CD.Latest is being used.

**RecoveryOptions**  

-   **Key Name:** ServerRecoveryOptions  

    -   **Required:** Yes  

    -   **Values:** 1, 2, or 4  

         1 = Recover site server and SQL Server.  

         2 = Recover site server only.  

         4 = Recover SQL Server only.  

    -   **Details:** Specifies whether Setup will recover the site server, SQL Server, or both. The associated keys are required when you set the following value for the **ServerRecoveryOptions** setting:  

        -   Value = 1: You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

        -   Value = 2: You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

        -   Value = 4: The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.  

-   **Key Name:** DatabaseRecoveryOptions  

    -   **Required:** This key is required when the **ServerRecoveryOptions** setting has a value of **1** or **4**.  

    -   **Values:** 10, 20, 40, or 80  

         10 = Restore the site database from backup.  

         20 = Use a site database that has been manually recovered by using another method.  

         40 = Create a new database for the site. Use this option when there is no site database backup available. Global and site data is recovered through replication from other sites.  

         80 = Skip database recovery.  

    -   **Details:** Specifies how Setup recovers the site database in SQL Server.  

-   **Key Name:** ReferenceSite  

    -   **Required:** This key is required when the **DatabaseRecoveryOptions** setting has a value of **40**.  

    -   **Values:** <*Reference site FQDN*>  

    -   **Details:** Specifies the reference primary site that the central administration site uses to recover global data if the database backup is older than the change-tracking retention period or when you recover the site without a backup.  

         When you do not specify a reference site and the backup is older than the change-tracking retention period, all primary sites are reinitialized with the restored data from the central administration site.  

         When you do not specify a reference site and the backup is within the change-tracking retention period, only changes that are made after the backup are replicated from primary sites. When there are conflicting changes from different primary sites, the central administration site uses the first one that it receives.  

-   **Key Name:** SiteServerBackupLocation  

    -   **Required:** No  

    -   **Values:** <*Path to site server backup set*>  

    -   **Details:** Specifies the path to the site server backup set. This key is optional when the **ServerRecoveryOptions** setting has a value of **1** or **2**. Specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

-   **Key Name:** BackupLocation  

    -   **Required:** This key is required when you configure a value of **1** or **4** for the **ServerRecoveryOptions** key, and you configure a value of **10** for the **DatabaseRecoveryOptions** key.  

    -   **Values:** <*Path to site database backup set*>  

    -   **Details:** Specifies the path to the site database backup set.  

**Options**  

-   **Key Name:** ProductID  

    -   **Required:** Yes  

    -   **Values:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *or* Eval  

    -   **Details:** Specifies the Configuration Manager installation product key, including the dashes. Enter **Eval** to install the evaluation version of Configuration Manager.  

-   **Key Name:** SiteCode  

    -   **Required:** Yes  

    -   **Values:** <*Site code*>  

    -   **Details:** Specifies three alphanumeric characters that uniquely identify the site in your hierarchy. You must specify the site code that the site used before the failure.

-   **Key Name:** SiteName  

    -   **Required:** No  

    -   **Values:** <*Site name*>  

    -   **Details:** Specifies the name for this site.  

-   **Key Name:** SMSInstallDir  

    -   **Required:** Yes  

    -   **Values:** <*Configuration Manager installation path*>  

    -   **Details:** Specifies the installation folder for the Configuration Manager program files.  

-   **Key Name:** SDKServer  

    -   **Required:** Yes  

    -   **Values:** <*SMS Provider FQDN*>  

    -   **Details:** Specifies the FQDN for the server that will host the SMS Provider. You must specify the server that hosted the SMS Provider before the failure.  

         You can configure additional SMS Providers for the site after the initial installation. For more information about the SMS Provider, see [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Key Name:** PrerequisiteComp  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Download  

         1 = Already downloaded  

    -   **Details:** Specifies whether Setup prerequisite files have already been downloaded. For example, if you use a value of **0**, Setup downloads the files.  

-   **Key Name:** PrerequisitePath  

    -   **Required:** Yes  

    -   **Values:** <*Path to Setup prerequisite files*>  

    -   **Details:** Specifies the path to the Setup prerequisite files. Depending on the **PrerequisiteComp** value, Setup uses this path to store downloaded files or to locate previously downloaded files.  

-   **Key Name:** AdminConsole  

    -   **Required:** This key is required except when the **ServerRecoveryOptions** setting has a value of **4**.  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether to install the Configuration Manager console.  

-   **Key Name:** JoinCEIP  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not join  

         1 = Join  

    -   **Details:** Specifies whether to join the CEIP.  

**SQLConfigOptions**  

-   **Key Name:** SQLServerName  

    -   **Required:** Yes  

    -   **Values:** <*SQL server name*>  

    -   **Details:** Specifies the name of the server or clustered instance that is running SQL Server, and which will host the site database. You must specify the same server that hosted the site database before the failure.  

-   **Key Name:** DatabaseName  

    -   **Required:** Yes  

    -   **Values:** <*Site database name*> or <*Instance name*>\\<*Site database name*>  

    -   **Details:** Specifies the name of the SQL Server database to create or the SQL Server database to use when installing the central administration site database. You must specify the same database name that was used before the failure.  

        > [!IMPORTANT]  
        >  You must specify the instance name and site database name if you do not use the default instance.  

-   **Key Name:** SQLSSBPort  

    -   **Required:** Yes  

    -   **Values:** <*SSB port number*>  

    -   **Details:** Specifies the SSB port that SQL Server uses. SSB typically is configured to use TCP port 4022. You must specify the same SSB port that was used before the failure.  

-   **Key Name:** SQLDataFilePath  

    -   **Required:** No  

    -   **Values:** <*Path to database .mdb file*>  

    -   **Details:** Specifies an alternate location to create the database .mdb file.  

-   **Key Name:** SQLLogFilePath  

    -   **Required:** No  

    -   **Values:** <*Path to database .ldf file*>  

    -   **Details:** Specifies an alternate location to create the database .ldf file.  

**CloudConnectorOptions**  

-   **Key Name:** CloudConnector  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether to install a service connection point at this site. Because the service connection point can only be installed at the top-tier site of a hierarchy, this value must be **0** for a child primary site.  

-   **Key Name:** CloudConnectorServer  

    -   **Required:** Required when **CloudConnector** equals 1  

    -   **Values:** <*Service connection point server FQDN*>  

    -   **Details:** Specifies the FQDN of the server that will host the service connection point site system role.  

-   **Key Name:** UseProxy  

    -   **Required:** Required when **CloudConnector** equals 1  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether the service connection point will use a proxy server.  

-   **Key Name:** ProxyName  

    -   **Required:** Required when **CloudConnector** equals 1  

    -   **Values:** <*Proxy server FQDN*>  

    -   **Details:** Specifies the FQDN of the proxy server that will be used by the service connection point site system role.  

-   **Key Name:** ProxyPort  

    -   **Required:** Required when **CloudConnector** equals 1  

    -   **Values:** <*Port number*>  

    -   **Details:** Specifies the port number to use for the proxy port.  

### Unattended recovery for a primary site  
 Use the following details to recover a primary site by using an unattended Setup script file.  

**Identification**  

-   **Key Name:** Action  

    -   **Required:** Yes  

    -   **Values:** <*RecoverPrimarySite*>  

    -   **Details:** Recovers a primary site.  

-   **Key Name:** CDLatest  

    -   **Required:** Yes – Only when using media from the CD.Latest folder.    

    -   **Values:** 1
        Any value other than 1 is considered to not be using CD.Latest.

    -   **Details:** Your script must include this key and value when you run setup from media in a CD.Latest folder for the purpose of installing a primary or central administration site, or recovering a primary or central administration site. This value informs setup that media form CD.Latest is being used.    

**RecoveryOptions**  

-   **Key Name:** ServerRecoveryOptions  

    -   **Required:** Yes  

    -   **Values:** 1, 2, or 4  

         1 = Recover site server and SQL Server.  

         2 = Recover site server only.  

         4 = Recover SQL Server only.  

    -   **Details:** Specifies whether Setup will recover the site server, SQL Server, or both. The associated keys are required when you set the following value for the **ServerRecoveryOptions** setting:  

        -   Value = 1: You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

        -   Value = 2: You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

        -   Value = 4: The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.  

-   **Key Name:** DatabaseRecoveryOptions  

    -   **Required:** This key is required when the **ServerRecoveryOptions** setting has a value of **1** or **4**.  

    -   **Values:** 10, 20, 40, or 80  

         10 = Restore the site database from backup.  

         20 = Use a site database that has been manually recovered by using another method.  

         40 = Create a new database for the site. Use this option when there is no site database backup available. Global and site data is recovered through replication from other sites.  

         80 = Skip database recovery.  

    -   **Details:** Specifies how Setup recovers the site database in SQL Server.  

-   **Key Name:** SiteServerBackupLocation  

    -   **Required:** No  

    -   **Values:** <*Path to site server backup set*>  

    -   **Details:**  

         Specifies the path to the site server backup set. This key is optional when the **ServerRecoveryOptions** setting has a value of **1** or **2**. Specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

-   **Key Name:** BackupLocation  

    -   **Required:** This key is required when you configure a value of **1** or **4** for the **ServerRecoveryOptions** key, and configure a value of **10** for the **DatabaseRecoveryOptions** key.  

    -   **Values:** <*Path to site database backup set*>  

    -   **Details:** Specifies the path to the site database backup set.  

**Options**  

-   **Key Name:** ProductID  

    -   **Required:** Yes  

    -   **Values:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* or *Eval*  

    -   **Details:** Specifies the Configuration Manager installation product key, including the dashes. Enter **Eval** to install the evaluation version of Configuration Manager.  

-   **Key Name:** SiteCode  

    -   **Required:** Yes  

    -   **Values:** <*Site code*>  

    -   **Details:** Specifies three alphanumeric characters that uniquely identify the site in your hierarchy. You must specify the site code that the site used before the failure.

-   **Key Name:** SiteName  

    -   **Required:** No  

    -   **Values:** <*Site name*>  

    -   **Details:** Specifies the name for this site.  

-   **Key Name:** SMSInstallDir  

    -   **Required:** Yes  

    -   **Values:** <*Configuration Manager installation path*>  

    -   **Details:** Specifies the installation folder for the Configuration Manager program files.  

-   **Key Name:** SDKServer  

    -   **Required:** Yes  

    -   **Values:** <*SMS Provider FQDN*>  

    -   **Details:** Specifies the FQDN for the server that will host the SMS Provider. You must specify the server that hosted the SMS Provider before the failure. You can configure additional SMS Providers for the site after the initial installation. For more information about the SMS Provider, see [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Key Name:** PrerequisiteComp  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Download  

         1 = Already downloaded  

    -   **Details:** Specifies whether Setup prerequisite files have already been downloaded. For example, if you use a value of **0**, Setup downloads the files.  

-   **Key Name:** PrerequisitePath  

    -   **Required:** Yes  

    -   **Values:** <*Path to Setup prerequisite files*>  

    -   **Details:** Specifies the path to the Setup prerequisite files. Depending on the **PrerequisiteComp** value, Setup uses this path to store downloaded files or to locate previously downloaded files.  

-   **Key Name:** AdminConsole  

    -   **Required:** This key is required except when the **ServerRecoveryOptions** setting has a value of **4**.  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether to install the Configuration Manager console.  

-   **Key Name:** JoinCEIP  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not join  

         1 = Join  

    -   **Details:** Specifies whether to join the CEIP.  

**SQLConfigOptions**  

-   **Key Name:** SQLServerName  

    -   **Required:** Yes  

    -   **Values:** <*SQL server name*>  

    -   **Details:** Specifies the name of the server or clustered instance that is running SQL Server, and which will host the site database. You must specify the same server that hosted the site database before the failure.  

-   **Key Name:** DatabaseName  

    -   **Required:** Yes  

    -   **Values:**  <*Site database name*> or <*Instance name*>\\<*Site database name*>

    -   **Details:**  

         Specifies the name of the SQL Server database to create or the SQL Server database to use when installing the central administration site database. You must specify the same database name that was used before the failure.  

        > [!IMPORTANT]  
        >  You must specify the instance name and site database name if you do not use the default instance.  

-   **Key Name:** SQLSSBPort  

    -   **Required:** Yes  

    -   **Values:** <*SSB port number*>  

    -   **Details:** Specifies the SSB port that SQL Server uses. Typically, SSB is configured to use TCP port 4022. You must specify the same SSB port that was used before the failure.  

-   **Key Name:** SQLDataFilePath  

    -   **Required:** No  

    -   **Values:** <*Path to database .mdb file*>  

    -   **Details:** Specifies an alternate location to create the database .mdb file.  

-   **Key Name:** SQLLogFilePath  

    -   **Required:** No  

    -   **Values:** <*Path to database .ldf file*>  

    -   **Details:** Specifies an alternate location to create the database .ldf file.  

**HierarchyExpansionOptions**  

-   **Key Name:** CCARSiteServer  

    -   **Required:** See details.  

    -   **Values:** <*Site code for central administration site*>  

    -   **Details:** Specifies the central administration site to which a primary site attaches when it joins the Configuration Manager hierarchy. This setting is required if the primary site was attached to a central administration site before the failure. You must specify the site code that was used for the central administration site before the failure.  

-   **Key Name:** CASRetryInterval  

    -   **Required:** No  

    -   **Values:** <*Interval*>  

    -   **Details:** Specifies the retry interval (in minutes) to attempt a connection to the central administration site after the connection fails. For example, if the connection to the central administration site fails, the primary site waits the number of minutes that you specify for the **CASRetryInterval** value, and then attempts the connection again.  

-   **Key Name:** WaitForCASTimeout  

    -   **Required:** No  

    -   **Values:** <*Timeout*>  

    -   **Details:** Specifies the maximum timeout value (in minutes) for a primary site to connect to the central administration site. For example, if a primary site fails to connect to a central administration site, the primary site retries the connection to the central administration site based on the **CASRetryInterval** value until the **WaitForCASTimeout** period is reached. You can specify a value of **0** to **100**.  

**CloudConnectorOptions**  

-   **Key Name:** CloudConnector  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether to install a service connection point at this site. Because the service connection point can only be installed at the top-tier site of a hierarchy, this value must be **0** for a child primary site.  

-   **Key Name:** CloudConnectorServer  

    -   **Required:** Required when **CloudConnector** equals 1  

    -   **Values:** <*Service connection point server FQDN*>  

    -   **Details:** Specifies the FQDN of the server that will host the service connection point site system role.  

-   **Key Name:** UseProxy  

    -   **Required:** Required when **CloudConnector** equals 1  

    -   **Values:** 0 or 1  

         0 = Do not install  

         1 = Install  

    -   **Details:** Specifies whether the service connection point will use a proxy server.  

-   **Key Name:** ProxyName  

    -   **Required:** Required when **CloudConnector** equals 1  

    -   **Values:** <*Proxy server FQDN*>  

    -   **Details:** Specifies the FQDN of the proxy server that will be used by the service connection point site system role.  

-   **Key Name:** ProxyPort  

    -   **Required:** Required when **CloudConnector** equals 1  

    -   **Values:** <*Port number*>  

    -   **Details:** Specifies the port number to use for the proxy port.  
