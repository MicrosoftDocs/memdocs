---
title: Setup command-line options
titleSuffix: Configuration Manager
description: Create automation scripts to install Configuration Manager from a command line.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# Command-line options for Configuration Manager setup

*Applies to: System Center Configuration Manager (Current Branch)*

Use the following information to configure scripts or to install Configuration Manager from a command line.  

## <a name="bkmk_setup"></a> Command-line options for setup

Run setup from the `\BIN\X64` directory of the Configuration Manager installation path on the site server.

### `/DEINSTALL`

Uninstall the site. Run setup from the site server computer.  

### `/DONTSTARTSITECOMP`

Install a site, but prevents the Site Component Manager service from starting. Until the Site Component Manager service starts, the site isn't active. The Site Component Manager is responsible for installing and starting the SMS_Executive service, and for additional processes at the site. After the site install is finished, when you start the Site Component Manager service, it installs the SMS_Executive service and additional processes that are necessary for the site to operate.  

### `/HIDDEN`

Hide the user interface during setup. Use this option only in conjunction with the **/SCRIPT** option. The unattended script file must provide all required options or setup fails.  

### `/NOUSERINPUT`

Disable user input during setup, but displays the setup wizard. Use this option only in conjunction with the **/SCRIPT** option. The unattended script file must provide all required options or setup fails.  

### `/RESETSITE`

Run a site reset that resets the database and service accounts for the site.

For more information, see [Run a site reset](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset).  

### `/TESTDBUPGRADE`

Run a test on a backup of the site database to make sure that the database can upgrade.

> [!IMPORTANT]  
> Don't run this command-line option on your production site database. Running this command-line option on your production site database upgrades the site database and could render your site inoperable.

#### Usage

Provide the instance name and database name for the site database. If you specify only the database name, setup uses the default instance name.  

`/TESTDBUPGRADE <Instance name>\<Database name>`

`/TESTDBUPGRADE CM_ABC`

`/TESTDBUPGRADE Named\CM_ABC`

### `/UPGRADE`

Run an unattended upgrade of a site. Specify the product key including the dashes (`-`). Also specify the path to the previously downloaded setup prerequisite files.  

For more information about setup prerequisite files, see [Setup Downloader](/sccm/core/servers/deploy/install/setup-downloader).  

#### Usage

`setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

### `/SCRIPT`

Run an unattended installation. Use a setup initialization file with this option. For more information about how to run setup unattended, see [Install sites using a command line](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites).  

#### Usage

`/SCRIPT <setup script path>`

### `/SDKINST`

Install the SMS Provider on the specified computer. Provide the fully qualified domain name (FQDN) for the SMS Provider computer. For more information about the SMS Provider, see [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).  

#### Usage

`/SDKINST <SMS Provider FQDN>`

### `/SDKDEINST`

Uninstall the SMS Provider on the specified computer. Provide the FQDN for the SMS Provider computer.  

#### Usage

`/SDKDEINST <SMS Provider FQDN>`

### `/MANAGELANGS`

Manage the languages that are installed at a previously installed site. Provide the location for the language script file that contains the language settings. For more information, see the [Command-line options to manage languages](#bkmk_Lang) section.  

#### Usage

`/MANAGELANGS <Language script path>`


## <a name="bkmk_Lang"></a> Command-line options to manage languages

### Identification

- **Key name:** Action  

    - **Required:** Yes  

    - **Values:** `ManageLanguages`  

    - **Details:** Manages the server, client, and mobile client language support at a site.  

### Options

- **Key name:** AddServerLanguages  

    - **Required:** No  

    - **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    - **Details:** Specifies the server languages that will be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default.  

- **Key name:** AddClientLanguages  

    - **Required:** No  

    - **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    - **Details:** Specifies the languages that will be available to client computers. English is available by default.  

- **Key name:** DeleteServerLanguages  

    - **Required:** No  

    - **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    - **Details:** Specifies the languages to remove, and which will no longer be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default, you can't remove it.  

- **Key name:** DeleteClientLanguages  

    - **Required:** No  

    - **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    - **Details:** Specifies the languages to remove, and which will no longer be available to client computers. English is available by default, you can't remove it.  

- **Key name:** MobileDeviceLanguage  

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether the mobile device client languages are installed.  

- **Key name:** PrerequisiteComp  

    - **Required:** Yes  

    - **Values:**

        - `0` = Download  

        - `1` = Already downloaded  

    - **Details:** Specifies whether setup prerequisite files have already been downloaded. For example, if you use a value of `0`, setup downloads the files.  

- **Key name:** PrerequisitePath  

    - **Required:** Yes  

    - **Values:** <*Path to setup prerequisite files*>  

    - **Details:** Specifies the path to the setup prerequisite files. Depending on the **PrerequisiteComp** value, setup uses this path to store downloaded files or to locate previously downloaded files.  


## <a name="bkmk_Unattended"></a> Unattended setup script file keys

Use the following sections to help you create your script for unattended setup. The lists show:

- The available setup script keys and their corresponding values
- If they're required
- Which type of installation they're used for
- A short description of the key

### Unattended install for a central administration site (CAS)

Use the following details to install a CAS by using an unattended setup script file.  

#### Identification

- **Key name:** Action  

    - **Required:** Yes  

    - **Values:** `InstallCAS`  

    - **Details:** Installs a CAS.  

- **Key name:** CDLatest  

    - **Required:** Yes, only when using media from the CD.Latest folder.

    - **Values:**

        - `1` = you're using media from CD.Latest

        - Any value other than 1 = you're not using CD.Latest media

    - **Details:** When you install or recover a primary site or CAS, and you run setup from the CD.Latest folder, include this key and value. This value informs setup that you're using media from CD.Latest.

#### Options

- **Key name:** ProductID  

    - **Required:** Yes  

    - **Values:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = a valid product key with dashes

        - `Eval` = install the evaluation version of Configuration Manager

    - **Details:** Specifies the Configuration Manager installation product key, including the dashes.

- **Key name:** SiteCode  

    - **Required:** Yes  

    - **Values:** <*Site code*>, for example, `ABC`

    - **Details:** Specifies three alphanumeric characters that uniquely identify the site in your hierarchy.  

- **Key name:** Site name  

    - **Required:** Yes  

    - **Values:** <*Site name*>  

    - **Details:** Specifies the name for this site.  

- **Key name:** SMSInstallDir  

    - **Required:** Yes  

    - **Values:** <*Configuration Manager installation path*>  

    - **Details:** Specifies the installation folder for the Configuration Manager program files.  

- **Key name:** SDKServer  

    - **Required:** Yes  

    - **Values:** <*SMS Provider FQDN*>  

    - **Details:** Specifies the FQDN for the server that will host the SMS Provider. You can configure additional SMS Providers for the site after the initial installation.  

- **Key name:** PrerequisiteComp  

    - **Required:** Yes  

    - **Values:**

        - `0` = Download  

        - `1` = Already downloaded  

    - **Details:** Specifies whether setup prerequisite files have already been downloaded. For example, if you use a value of `0`, setup downloads the files.  

- **Key name:** PrerequisitePath  

    - **Required:** Yes  

    - **Values:** <*Path to setup prerequisite files*>  

    - **Details:** Specifies the path to the setup prerequisite files. Depending on the **PrerequisiteComp** value, setup uses this path to store downloaded files or to locate previously downloaded files.  

- **Key name:** AdminConsole  

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether to install the Configuration Manager console.  

- **Key name:** JoinCEIP  

    > [!Note]  
    > Starting in Configuration Manager version 1802 the CEIP feature is removed from the product.

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't join  

        - `1` = Join  

    - **Details:** Specifies whether to join the Customer Experience Improvement Program (CEIP).  

- **Key name:** AddServerLanguages  

    - **Required:** No  

    - **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    - **Details:** Specifies the server languages that will be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default.  

- **Key name:** AddClientLanguages  

    - **Required:** No  

    - **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    - **Details:** Specifies the languages that will be available to client computers. English is available by default.  

- **Key name:** DeleteServerLanguages  

    - **Required:** No  

    - **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    - **Details:** Modifies a site after it's installed. Specifies the languages to remove, and which will no longer be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default, you can't remove it.  

- **Key name:** DeleteClientLanguages  

    - **Required:** No  

    - **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    - **Details:** Modifies a site after it's installed. Specifies the languages to remove, and which will no longer be available to client computers. English is available by default, you can't remove it.  

- **Key name:** MobileDeviceLanguage  

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether the mobile device client languages are installed.  

#### SQLConfigOptions

- **Key name:** SQLServerName  

    - **Required:** Yes  

    - **Values:** <*SQL server name*>  

    - **Details:** Specifies the name of the server or clustered instance that's running SQL Server to host the site database.  

- **Key name:** DatabaseName  

    - **Required:** Yes  

    - **Values:** <*Site database name*> or <*Instance name*>\\<*Site database name*>  

    - **Details:** Specifies the name of the SQL Server database to create, or the SQL Server database to use, when setup installs the CAS database.  

        > [!IMPORTANT]  
        > If you don't use the default instance, specify the instance name and site database name.  

- **Key name:** SQLSSBPort  

    - **Required:** No  

    - **Values:** <*SSB port number*>  

    - **Details:** Specifies the SQL Server Service Broker (SSB) port that SQL Server uses. By default, SSB uses TCP port 4022, but you can use a different port.  

- **Key name:** SQLDataFilePath  

    - **Required:** No  

    - **Values:** <*Path to database .mdb file*>  

    - **Details:** Specifies an alternate location to create the database .mdb file.  

- **Key name:** SQLLogFilePath  

    - **Required:** No  

    - **Values:** <*Path to database .ldf file*>  

    - **Details:** Specifies an alternate location to create the database .ldf file.  

#### CloudConnectorOptions

- **Key name:** CloudConnector  

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether to install a service connection point at this site. Because you can only install the service connection point at the top-tier site of a hierarchy, set this value to `1` for a child primary site.  

- **Key name:** CloudConnectorServer  

    - **Required:** Required when **CloudConnector** equals 1  

    - **Values:** <*Service connection point server FQDN*>  

    - **Details:** Specifies the FQDN of the server that will host the service connection point site system role.  

- **Key name:** UseProxy  

    - **Required:** Required when **CloudConnector** equals 1  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether the service connection point uses a proxy server.  

- **Key name:** ProxyName  

    - **Required:** Required when **UseProxy** equals 1  

    - **Values:** <*Proxy server FQDN*>  

    - **Details:** Specifies the FQDN of the proxy server that the service connection point uses.  

- **Key name:** ProxyPort  

    - **Required:** Required when **UseProxy** equals 1  

    - **Values:** <*Port number*>  

    - **Details:** Specifies the port number to use for the proxy port.  

### Unattended install for a primary site

Use the following details to install a primary site by using an unattended setup script file.  

#### Identification

- **Key name:** Action  

    - **Required:** Yes  

    - **Values:** `InstallPrimarySite`  

    - **Details:** Installs a primary site.  

- **Key name:** CDLatest  

    - **Required:** Yes, only when using media from the CD.Latest folder.

    - **Values:**

        - `1` = you're using media from CD.Latest

        - Any value other than 1 = you're not using CD.Latest media

    - **Details:** When you install or recover a primary site or CAS, and you run setup from the CD.Latest folder, include this key and value. This value informs setup that you're using media from CD.Latest.

#### Options

- **Key name:** ProductID  

    - **Required:** Yes  

    - **Values:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = a valid product key with dashes

        - `Eval` = install the evaluation version of Configuration Manager

    - **Details:** Specifies the Configuration Manager installation product key, including the dashes.

- **Key name:** SiteCode  

    - **Required:** Yes  

    - **Values:** <*Site code*>  

    - **Details:** Specifies three alphanumeric characters that uniquely identify the site in your hierarchy.  

- **Key name:** SiteName  

    - **Required:** Yes  

    - **Values:** <*Site name*>  

    - **Details:** Specifies the name for this site.  

- **Key name:** SMSInstallDir  

    - **Required:** Yes  

    - **Values:** <*Configuration Manager installation path*>

    - **Details:** Specifies the installation folder for the Configuration Manager program files.  

- **Key name:** SDKServer  

    - **Required:** Yes  

    - **Values:** <*SMS Provider FQDN*>  

    - **Details:** Specifies the FQDN for the server that will host the SMS Provider. You can configure additional SMS Providers for the site after the initial installation.  

- **Key name:** PrerequisiteComp  

    - **Required:** Yes  

    - **Values:**

        - `0` = Download  

        - `1` = Already downloaded  

    - **Details:** Specifies whether setup prerequisite files have already been downloaded. For example, if you use a value of `0`, setup downloads the files.  

- **Key name:** PrerequisitePath  

    - **Required:** Yes  

    - **Values:** <*Path to setup prerequisite files*>  

    - **Details:** Specifies the path to the setup prerequisite files. Depending on the **PrerequisiteComp** value, setup uses this path to store downloaded files or to locate previously downloaded files.  

- **Key name:** AdminConsole  

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether to install the Configuration Manager console.  

- **Key name:** JoinCEIP  

    > [!Note]  
    > Starting in Configuration Manager version 1802 the CEIP feature is removed from the product.

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't join  

        - `1` = Join  

    - **Details:** Specifies whether to join the CEIP.  

- **Key name:** ManagementPoint  

    - **Required:** No  

    - **Values:** <*Management point site server FQDN*>  

    - **Details:** Specifies the FQDN of the server that will host the management point site system role.  

- **Key name:** ManagementPointProtocol  

    - **Required:** No  

    - **Values:** `HTTPS` or `HTTP`  

    - **Details:** Specifies the protocol to use for the management point.  

- **Key name:** DistributionPoint  

    - **Required:** No  

    - **Values:** <*Distribution point site server FQDN*>  

    - **Details:** Specifies the FQDN of the server that will host the distribution point site system role.  

- **Key name:** DistributionPointProtocol  

    - **Required:** No  

    - **Values:** `HTTPS` or `HTTP`  

    - **Details:** Specifies the protocol to use for the distribution point.  

- **Key name:** RoleCommunicationProtocol  

    - **Required:** Yes  

    - **Values:** `EnforceHTTPS` or `HTTPorHTTPS`  

    - **Details:** Specifies whether to configure all site systems to accept only HTTPS communication from clients, or to configure the communication method for each site system role. When you select `EnforceHTTPS`, clients must have a valid public key infrastructure (PKI) certificate for client authentication.  

- **Key name:** ClientsUsePKICertificate  

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't use  

        - `1` = Use  

    - **Details:** Specifies whether clients will use a client PKI certificate to communicate with site system roles.  

- **Key name:** AddServerLanguages  

    - **Required:** No  

    - **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    - **Details:** Specifies the server languages that will be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default.  

- **Key name:** AddClientLanguages  

    - **Required:** No  

    - **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    - **Details:** Specifies the languages that will be available to client computers. English is available by default.  

- **Key name:** DeleteServerLanguages  

    - **Required:** No  

    - **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    - **Details:** Modifies a site after it's installed. Specifies the languages to remove, and which will no longer be available for the Configuration Manager console, reports, and Configuration Manager objects. English is available by default, you can't remove it.  

- **Key name:** DeleteClientLanguages  

    - **Required:** No  

    - **Values:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    - **Details:** Modifies a site after it's installed. Specifies the languages to remove, and which will no longer be available to client computers. English is available by default, you can't remove it.  

- **Key name:** MobileDeviceLanguage  

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether the mobile device client languages are installed.  

#### SQLConfigOptions

- **Key name:** SQLServerName  

    - **Required:** Yes  

    - **Values:** <*SQL server name*>  

    - **Details:** Specifies the name of the server or clustered instance that runs SQL Server to host the site database.  

- **Key name:** DatabaseName  

    - **Required:** Yes  

    - **Values:** <*Site database name*> or <*Instance name*>\\<*Site database name*>  

    - **Details:** Specifies the name of the SQL Server database to create or the SQL Server database to use when installing the primary site database.  

        > [!IMPORTANT]  
        > If you don't use the default instance, specify the instance name and site database name.  

- **Key name:** SQLSSBPort  

    - **Required:** No  

    - **Values:** <*SSB port number*>  

    - **Details:** Specifies the SSB port that SQL Server uses. By default, SSB uses TCP port 4022, but you can use a different port.  

- **Key name:** SQLDataFilePath  

    - **Required:** No  

    - **Values:** <*Path to database .mdb file*>  

    - **Details:** Specifies an alternate location to create the database .mdb file.  

- **Key name:** SQLLogFilePath  

    - **Required:** No  

    - **Values:** <*Path to database .ldf file*>  

    - **Details:** Specifies an alternate location to create the database .ldf file.  

#### HierarchyExpansionOption

- **Key name:** CCARSiteServer  

    - **Required:** No  

    - **Values:** <*Central administration site FQDN*>  

    - **Details:** Specifies the CAS that a primary site attaches to when it joins the Configuration Manager hierarchy. Specify the CAS during setup.  

- **Key name:** CASRetryInterval  

    - **Required:** No  

    - **Values:** <*Interval in minutes*>  

    - **Details:** Specifies the retry interval in minutes to attempt a connection to the CAS after the connection fails. For example, if the connection to the CAS fails, the primary site waits the number of minutes that you specify for the **CASRetryInterval** value, and then reattempts the connection.  

- **Key name:** WaitForCASTimeout  

    - **Required:** No  

    - **Values:** <*Timeout in minutes from 0 to 100*>  

    - **Details:** Specifies the maximum timeout value in minutes for a primary site to connect to the CAS. For example, if a primary site fails to connect to a CAS, the primary site retries the connection to the CAS based on the **CASRetryInterval** value until the **WaitForCASTimeout** period is reached. You can specify a value from `0` to `100`.  

#### CloudConnectorOptions

- **Key name:** CloudConnector  

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether to install a service connection point at this site. Because you can only install the service connection point at the top-tier site of a hierarchy, set this value to `0` for a child primary site.  

- **Key name:** CloudConnectorServer  

    - **Required:** Required when **CloudConnector** equals 1  

    - **Values:** <*Service connection point server FQDN*\>  

    - **Details:** Specifies the FQDN of the server that will host the service connection point site system role.  

- **Key name:** UseProxy  

    - **Required:** Required when **CloudConnector** equals 1  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether the service connection point uses a proxy server.  

- **Key name:** ProxyName  

    - **Required:** Required when **UseProxy** equals 1  

    - **Values:** <*Proxy server FQDN*>  

    - **Details:** Specifies the FQDN of the proxy server that the service connection point uses.  

- **Key name:** ProxyPort  

    - **Required:** Required when **UseProxy** equals 1  

    - **Values:** <*Port number*>  

    - **Details:** Specifies the port number to use for the proxy port.  

### Unattended recovery for a CAS

Use the following details to recover a CAS by using an unattended setup script file.  

#### Identification

- **Key name:** Action  

    - **Required:** Yes  

    - **Values:** `RecoverCCAR`  

    - **Details:** Recovers a CAS.  

- **Key name:** CDLatest  

    - **Required:** Yes, only when using media from the CD.Latest folder.

    - **Values:**

        - `1` = you're using media from CD.Latest

        - Any value other than 1 = you're not using CD.Latest media

    - **Details:** When you install or recover a primary site or CAS, and you run setup from the CD.Latest folder, include this key and value. This value informs setup that you're using media from CD.Latest.

#### RecoveryOptions

- **Key name:** ServerRecoveryOptions  

    - **Required:** Yes  

    - **Values:**

        - `1` = Recover site server and SQL Server

        - `2` = Recover site server only

        - `4` = Recover SQL Server only  

    - **Details:** Specifies whether setup recovers the site server, SQL Server, or both. The following options are also required based on the specified value:  

        - **1** or **2**: To recover the site by using a site backup, specify a value for **SiteServerBackupLocation**. If you don't specify a value, setup reinstalls the site without restoring it from a backup set.  

        - **4**: The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.  

- **Key name:** DatabaseRecoveryOptions  

    - **Required:** This key is required when the **ServerRecoveryOptions** setting has a value of **1** or **4**.  

    - **Values:**

        - `10` = Restore the site database from backup.  

        - `20` = Use a site database that you manually recovered with another method.  

        - `40` = Create a new database for the site. Use this option when there's no site database backup available. The site recovers global and site data through replication from other sites.  

        - `80` = Skip database recovery.  

    - **Details:** Specifies how setup recovers the site database in SQL Server.  

- **Key name:** ReferenceSite  

    - **Required:** This key is required when the **DatabaseRecoveryOptions** setting has a value of **40**.  

    - **Values:** <*Reference site FQDN*>  

    - **Details:** If the database backup is older than the change-tracking retention period, or when you recover the site without a backup, specify the reference primary site that the CAS uses to recover global data.  

        When you don't specify a reference site, and the backup is older than the change-tracking retention period, all primary sites are reinitialized with the restored data from the CAS.  

        When you don't specify a reference site, and the backup is within the change-tracking retention period, only changes that are made after the backup are replicated from primary sites. When there are conflicting changes from different primary sites, the CAS uses the first one that it receives.  

- **Key name:** SiteServerBackupLocation  

    - **Required:** No  

    - **Values:** <*Path to site server backup set*>  

    - **Details:** Specifies the path to the site server backup set. This key is optional when the **ServerRecoveryOptions** setting has a value of **1** or **2**. Specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you don't specify a value, setup reinstalls the site without restoring it from a backup set.  

- **Key name:** BackupLocation  

    - **Required:** This key is required when you configure a value of **1** or **4** for the **ServerRecoveryOptions** key, and you configure a value of **10** for the **DatabaseRecoveryOptions** key.  

    - **Values:** <*Path to site database backup set*>  

    - **Details:** Specifies the path to the site database backup set.  

#### Options

- **Key name:** ProductID  

    - **Required:** Yes  

    - **Values:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = a valid product key with dashes

        - `Eval` = install the evaluation version of Configuration Manager

    - **Details:** Specifies the Configuration Manager installation product key, including the dashes.

- **Key name:** SiteCode  

    - **Required:** Yes  

    - **Values:** <*Site code*>  

    - **Details:** Specifies three alphanumeric characters that uniquely identify the site in your hierarchy. Specify the site code that the site used before the failure.

- **Key name:** SiteName  

    - **Required:** No  

    - **Values:** <*Site name*>  

    - **Details:** Specifies the name for this site.  

- **Key name:** SMSInstallDir  

    - **Required:** Yes  

    - **Values:** <*Configuration Manager installation path*>  

    - **Details:** Specifies the installation folder for the Configuration Manager program files.  

- **Key name:** SDKServer  

    - **Required:** Yes  

    - **Values:** <*SMS Provider FQDN*>  

    - **Details:** Specifies the FQDN for the server that hosts the SMS Provider. Specify the server that hosted the SMS Provider before the failure.  

        After the initial installation, you can configure additional SMS Providers for the site. For more information about the SMS Provider, see [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).  

- **Key name:** PrerequisiteComp  

    - **Required:** Yes  

    - **Values:**

        - `0` = Download  

        - `1` = Already downloaded  

    - **Details:** Specifies whether setup prerequisite files have already been downloaded. For example, if you use a value of **0**, setup downloads the files.  

- **Key name:** PrerequisitePath  

    - **Required:** Yes  

    - **Values:** <*Path to setup prerequisite files*>  

    - **Details:** Specifies the path to the setup prerequisite files. Depending on the **PrerequisiteComp** value, setup uses this path to store downloaded files or to locate previously downloaded files.  

- **Key name:** AdminConsole  

    - **Required:** This key is required except when the **ServerRecoveryOptions** setting has a value of **4**.  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether to install the Configuration Manager console.  

- **Key name:** JoinCEIP  

    > [!Note]  
    > Starting in Configuration Manager version 1802 the CEIP feature is removed from the product.

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't join  

        - `1` = Join  

    - **Details:** Specifies whether to join the CEIP.  

#### SQLConfigOptions

- **Key name:** SQLServerName  

    - **Required:** Yes  

    - **Values:** <*SQL server name*>  

    - **Details:** Specifies the name of the server or clustered instance that is running SQL Server, and which hosts the site database. Specify the same server that hosted the site database before the failure.  

- **Key name:** DatabaseName  

    - **Required:** Yes  

    - **Values:** <*Site database name*> or <*Instance name*>\\<*Site database name*>  

    - **Details:** Specifies the name of the SQL Server database to create or the SQL Server database to use when installing the CAS database. Specify the same database name that was used before the failure.  

        > [!IMPORTANT]  
        > If you don't use the default instance, specify the instance name and site database name.  

- **Key name:** SQLSSBPort  

    - **Required:** Yes  

    - **Values:** <*SSB port number*>  

    - **Details:** Specifies the SSB port that SQL Server uses. By default, SSB uses TCP port 4022. Specify the same SSB port that was used before the failure.  

- **Key name:** SQLDataFilePath  

    - **Required:** No  

    - **Values:** <*Path to database .mdb file*>  

    - **Details:** Specifies an alternate location to create the database .mdb file.  

- **Key name:** SQLLogFilePath  

    - **Required:** No  

    - **Values:** <*Path to database .ldf file*>  

    - **Details:** Specifies an alternate location to create the database .ldf file.  

#### CloudConnectorOptions

- **Key name:** CloudConnector  

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether to install a service connection point at this site. Because you can only install the service connection point at the top-tier site of a hierarchy, this value must be **0** for a child primary site.  

- **Key name:** CloudConnectorServer  

    - **Required:** Required when **CloudConnector** equals 1  

    - **Values:** <*Service connection point server FQDN*>  

    - **Details:** Specifies the FQDN of the server that will host the service connection point site system role.  

- **Key name:** UseProxy  

    - **Required:** Required when **CloudConnector** equals 1  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether the service connection point uses a proxy server.  

- **Key name:** ProxyName  

    - **Required:** Required when **CloudConnector** equals 1  

    - **Values:** <*Proxy server FQDN*>  

    - **Details:** Specifies the FQDN of the proxy server that the service connection point uses.  

- **Key name:** ProxyPort  

    - **Required:** Required when **CloudConnector** equals 1  

    - **Values:** <*Port number*>  

    - **Details:** Specifies the port number to use for the proxy port.  

### Unattended recovery for a primary site

Use the following details to recover a primary site by using an unattended setup script file.  

#### Identification

- **Key name:** Action  

    - **Required:** Yes  

    - **Values:** `RecoverPrimarySite`  

    - **Details:** Recovers a primary site.  

- **Key name:** CDLatest  

    - **Required:** Yes, only when using media from the CD.Latest folder.

    - **Values:**

        - `1` = you're using media from CD.Latest

        - Any value other than 1 = you're not using CD.Latest media

    - **Details:** When you install or recover a primary site or CAS, and you run setup from the CD.Latest folder, include this key and value. This value informs setup that you're using media from CD.Latest.

#### RecoveryOptions

- **Key name:** ServerRecoveryOptions  

    - **Required:** Yes  

    - **Values:**

        - `1` = Recover site server and SQL Server

        - `2` = Recover site server only

        - `4` = Recover SQL Server only  

    - **Details:** Specifies whether setup recovers the site server, SQL Server, or both. The following options are also required based on the specified value:  

        - **1** or **2**: To recover the site by using a site backup, specify a value for **SiteServerBackupLocation**. If you don't specify a value, setup reinstalls the site without restoring it from a backup set.  

        - **4**: The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.  

- **Key name:** DatabaseRecoveryOptions  

    - **Required:** This key is required when the **ServerRecoveryOptions** setting has a value of **1** or **4**.  

    - **Values:**

        - `10` = Restore the site database from backup.  

        - `20` = Use a site database that you manually recovered with another method.  

        - `40` = Create a new database for the site. Use this option when there's no site database backup available. The site recovers global and site data through replication from other sites.  

        - `80` = Skip database recovery.  

    - **Details:** Specifies how setup recovers the site database in SQL Server.  

- **Key name:** SiteServerBackupLocation  

    - **Required:** No  

    - **Values:** <*Path to site server backup set*>  

    - **Details:** Specifies the path to the site server backup set. This key is optional when the **ServerRecoveryOptions** setting has a value of **1** or **2**. Specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you don't specify a value, setup reinstalls the site without restoring it from a backup set.  

- **Key name:** BackupLocation  

    - **Required:** This key is required when you configure a value of **1** or **4** for the **ServerRecoveryOptions** key, and configure a value of **10** for the **DatabaseRecoveryOptions** key.  

    - **Values:** <*Path to site database backup set*>  

    - **Details:** Specifies the path to the site database backup set.  

#### Options

- **Key name:** ProductID  

    - **Required:** Yes  

    - **Values:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = a valid product key with dashes

        - `Eval` = install the evaluation version of Configuration Manager

    - **Details:** Specifies the Configuration Manager installation product key, including the dashes.

- **Key name:** SiteCode  

    - **Required:** Yes  

    - **Values:** <*Site code*>  

    - **Details:** Specifies three alphanumeric characters that uniquely identify the site in your hierarchy. Specify the site code that the site used before the failure.

- **Key name:** SiteName  

    - **Required:** No  

    - **Values:** <*Site name*>  

    - **Details:** Specifies the name for this site.  

- **Key name:** SMSInstallDir  

    - **Required:** Yes  

    - **Values:** <*Configuration Manager installation path*>  

    - **Details:** Specifies the installation folder for the Configuration Manager program files.  

- **Key name:** SDKServer  

    - **Required:** Yes  

    - **Values:** <*SMS Provider FQDN*>  

    - **Details:** Specifies the FQDN for the server that hosts the SMS Provider. Specify the server that hosted the SMS Provider before the failure. After the initial installation, you can configure additional SMS Providers for the site. For more information about the SMS Provider, see [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).  

- **Key name:** PrerequisiteComp  

    - **Required:** Yes  

    - **Values:**

        - `0` = Download  

        - `1` = Already downloaded  

    - **Details:** Specifies whether setup prerequisite files have already been downloaded. For example, if you use a value of **0**, setup downloads the files.  

- **Key name:** PrerequisitePath  

    - **Required:** Yes  

    - **Values:** <*Path to setup prerequisite files*>  

    - **Details:** Specifies the path to the setup prerequisite files. Depending on the **PrerequisiteComp** value, setup uses this path to store downloaded files or to locate previously downloaded files.  

- **Key name:** AdminConsole  

    - **Required:** This key is required except when the **ServerRecoveryOptions** setting has a value of **4**.  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether to install the Configuration Manager console.  

- **Key name:** JoinCEIP  

    > [!Note]  
    > Starting in Configuration Manager version 1802 the CEIP feature is removed from the product.

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't join  

        - `1` = Join  

    - **Details:** Specifies whether to join the CEIP.  

#### SQLConfigOptions

- **Key name:** SQLServerName  

    - **Required:** Yes  

    - **Values:** <*SQL server name*>  

    - **Details:** Specifies the name of the server or clustered instance that runs SQL Server to host the site database. Specify the same server that hosted the site database before the failure.  

- **Key name:** DatabaseName  

    - **Required:** Yes  

    - **Values:** <*Site database name*> or <*Instance name*>\\<*Site database name*>

    - **Details:** Specifies the name of the SQL Server database to create or the SQL Server database to use when installing the CAS database. Specify the same database name that was used before the failure.  

        > [!IMPORTANT]  
        > If you don't use the default instance, specify the instance name and site database name.  

- **Key name:** SQLSSBPort  

    - **Required:** Yes  

    - **Values:** <*SSB port number*>  

    - **Details:** Specifies the SSB port that SQL Server uses. By default, SSB uses TCP port 4022. Specify the same SSB port that was used before the failure.  

- **Key name:** SQLDataFilePath  

    - **Required:** No  

    - **Values:** <*Path to database .mdb file*>  

    - **Details:** Specifies an alternate location to create the database .mdb file.  

- **Key name:** SQLLogFilePath  

    - **Required:** No  

    - **Values:** <*Path to database .ldf file*>  

    - **Details:** Specifies an alternate location to create the database .ldf file.  

#### HierarchyExpansionOptions

- **Key name:** CCARSiteServer  

    - **Required:** See details.  

    - **Values:** <*Site code for CAS*>  

    - **Details:** Specifies the CAS to which a primary site attaches when it joins the Configuration Manager hierarchy. This setting is required if the primary site was attached to a CAS before the failure. Specify the site code that was used for the CAS before the failure.  

- **Key name:** CASRetryInterval  

    - **Required:** No  

    - **Values:** <*Interval in minutes*>  

    - **Details:** Specifies the retry interval in minutes to attempt a connection to the CAS after the connection fails. For example, if the connection to the CAS fails, the primary site waits the number of minutes that you specify for the **CASRetryInterval** value, and then attempts the connection again.  

- **Key name:** WaitForCASTimeout  

    - **Required:** No  

    - **Values:** <*Timeout in minutes*>  

    - **Details:** Specifies the maximum timeout value in minutes for a primary site to connect to the CAS. For example, if a primary site fails to connect to a CAS, the primary site retries the connection to the CAS based on the **CASRetryInterval** value until the **WaitForCASTimeout** period is reached. You can specify a value of `0` to `100`.  

#### CloudConnectorOptions

- **Key name:** CloudConnector  

    - **Required:** Yes  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether to install a service connection point at this site. Because you can only install the service connection point at the top-tier site of a hierarchy, this value must be `0` for a child primary site.  

- **Key name:** CloudConnectorServer  

    - **Required:** Required when **CloudConnector** equals 1  

    - **Values:** <*Service connection point server FQDN*>  

    - **Details:** Specifies the FQDN of the server that will host the service connection point site system role.  

- **Key name:** UseProxy  

    - **Required:** Required when **CloudConnector** equals 1  

    - **Values:**

        - `0` = Don't install  

        - `1` = Install  

    - **Details:** Specifies whether the service connection point uses a proxy server.  

- **Key name:** ProxyName  

    - **Required:** Required when **CloudConnector** equals 1  

    - **Values:** <*Proxy server FQDN*>  

    - **Details:** Specifies the FQDN of the proxy server that the service connection point uses.  

- **Key name:** ProxyPort  

    - **Required:** Required when **CloudConnector** equals 1  

    - **Values:** <*Port number*>  

    - **Details:** Specifies the port number to use for the proxy port.  
