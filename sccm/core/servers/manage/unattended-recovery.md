---
title: Unattended recovery
titleSuffix: Configuration Manager
description: Use a script to recover your sites in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Unattended site recovery for Configuration Manager   

*Applies to: System Center Configuration Manager (Current Branch)*

 To perform an [unattended recovery](/sccm/protect/understand/recover-sites#site-recovery-procedures) of a Configuration Manager central administration site or primary site, you can create an unattended installation script and then use setup with the **/script** command option. The script provides the same type of information that the setup wizard prompts for, except that there are no default settings. All values must be specified for the setup keys that apply to the type of recovery you are using.

 To use the /script setup command-line option, you must create an initialization file. Then specify this file name after the /script option. The name of the file is unimportant as long as it has the **.ini** file name extension. When you reference the setup initialization file from the command line, you must provide the full path to the file. For example, if your setup initialization file is named *setup.ini*, and it is stored in the *C:\setup folder*, your command line would be:

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  You must have Administrator rights to run setup. When you run setup with the unattended script, start the command prompt in an Administrator context by using **Run as administrator**.

 The script contains section names, key names, and values. Required section key names vary depending on the recovery type that you are scripting. The order of the keys within sections, and the order of sections within the file, is not important. The keys are not case-sensitive. When you provide values for keys, the name of the key must be followed by an equals sign (=) and the value for the key.

 Use the following sections to help you to create your script for unattended site recovery. The tables list the available setup script keys, their corresponding values, whether they are required, which type of installation they are used for, and a short description for the key.

## Recover a central administration site unattended
 Use the following information to configure an unattended setup script file to recover a central administration site.

 **Identification**

-   **Key name:** Action

    -   **Required:** Yes
    -   **Values:** RecoverCCAR
    -   **Details:** Recovers a central administration site


-   **Key Name:** CDLatest

    -   **Required:** Yes – Only when using media from the CD.Latest folder.
    -   **Values:** 1
        Any value other than 1 is considered to not be using CD.Latest.
    -   **Details:** Your script must include this key and value when you run setup from media in a CD.Latest folder for the purpose of installing a primary or central administration site, or recovering a primary or central administration site. This value informs setup that media form CD.Latest is being used.

**RecoveryOptions**   
-   **Key name:** ServerRecoveryOptions   

    -   **Required:** Yes
    -   **Values:** 1, 2, or 4  
         1 = Recovery site server and SQL Server.   
         2 = Recover site server only.  
         4 = Recover SQL Server only.
    -   **Details:** Specifies whether setup recovers the site server, SQL Server, or both. The associated keys are required when you set the following value for the ServerRecoveryOptions setting:  
        -   **Value = 1** You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.

             The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.

        -   **Value = 2** You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.

        -   **Value = 4** The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.

-   **Key name:** DatabaseRecoveryOptions

    -   **Required:** Maybe
    -   **Values:**   
         - **10** = Restore the site database from backup.  
         - **20** = Use a site database that has been manually recovered by using another method.   
         - **40** = Create a new database for the site. Use this option when there is no site database backup available. Global and site data is recovered through replication from other sites.  
         - **80** = skip database recovery.
    -   **Details:** Specifies how setup recovers the site database in SQL Server. This key is required when the **ServerRecoveryOptions** setting has a value of **1** or **4**.


-   **Key name:** ReferenceSite  

    -   **Required:** Maybe
    -   **Values:** &lt;ReferenceSiteFQDN\>
    -   **Details:** Specifies the reference primary site. If the database backup is older than the change tracking retention period, or you recover the site without a backup, the central administration site uses the reference site to recover global data.

         When you do not specify a reference site, and the backup is older than the change tracking retention period, all primary sites are reinitialized with the restored data from the central administration site.

         When you do not specify a reference site, and the backup is within the change tracking retention period, only changes since the backup are replicated from primary sites. When there are conflicting changes from different primary sites, the central administration site uses the first one that it receives.

         This key is required when the **DatabaseRecoveryOptions** setting has a value of **40**.

-   **Key name:** SiteServerBackupLocation

    -   **Required:** No
    -   **Values:** &lt;PathToSiteServerBackupSet\>
    -   **Details:** Specifies the path to the site server backup set. This key is optional when the **ServerRecoveryOptions** setting has a value of **1** or **2**. Specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.


-   **Key name:** BackupLocation

    -   **Required:** Maybe
    -   **Values:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Details:** Specifies the path to the site database backup set. The **BackupLocation** key is required when you configure a value of **1** or **4** for the **ServerRecoveryOptions** key, and configure a value of **10** for the **DatabaseRecoveryOptions** key.


**Options**

-   **Key name:** ProductID
    -   **Required:** Yes
    -   **Values:**   
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - Eval
    -   **Details:** The Configuration Manager installation product key, including the dashes. Enter **Eval** can install the evaluation version of Configuration Manager.  


-   **Key name:** SiteCode

    -   **Required:** Yes
    -   **Values:** &lt;Site code\>
    -   **Details:** Three alpha-numeric characters that uniquely identify the site in your hierarchy. Specify the site code that was used by the site before the failure.


-   **Key name:** SiteName

    -   **Required:** Yes
    -   **Values:** SiteName
    -   **Details:** Description for this site.


-   **Key name:** SMSInstallDir

    -   **Required:** Yes
    -   **Values:** &lt;*ConfigMgrInstallationPath*>
    -   **Details:** Specifies the installation folder for the Configuration Manager program files.
        > [!NOTE]   
        >  You can specify the original path or a new  path to use for the Configuration Manager installation.

-   **Key name:** SDKServer

    -   **Required:** Yes
    -   **Values:** &lt;*FQDN of SMS Provider*>
    -   **Details:** Specifies the FQDN for the server that hosts the SMS Provider. Specify the server that hosted the SMS Provider before the failure.

         You can configure additional SMS Providers for the site after the initial installation.

-   **Key name:** PrerequisiteComp

    -   **Required:** Yes
    -   **Values:** 0 or 1  
         0 = download   
         1 = already downloaded
    -   **Details:** Specifies whether setup prerequisite files have already been downloaded. For example, if you use a value of 0, setup downloads the files.  


-   **Key name:** PrerequisitePath

    -   **Required:** Yes
    -   **Values:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Details:** Specifies the path to the setup prerequisite files. Depending on the **PrerequisiteComp** value, setup uses this path to store downloaded files or to locate previously downloaded files.

-   **Key name:** AdminConsole

    -   **Required:** Maybe
    -   **Values:** 0 or 1
         0 = do not install   
         1 = install
    -   **Details:** Specifies whether to install the Configuration Manager console. This key is required except when the **ServerRecoveryOptions** setting has a value of **4**.


-   **Key name:** JoinCEIP   
    > [!Note]  
    > Starting in Configuration Manager version 1802 the CEIP feature is removed from the product.

    -   **Required:** Yes
    -   **Values:** 0 or 1  
         0 = do not join  
         1 = join
    -   **Details:** Specifies whether to join the Customer Experience Improvement Program.

**SQLConfigOptions**

-   **Key name:** SQLServerName

    -   **Required:** Yes
    -   **Values:** *&lt;SQLServerName\>*
    -   **Details:** The name of the server, or clustered instance name, running SQL Server that hosts the site database. Specify the same server that hosted the site database before the failure.


-   **Key name:** DatabaseName

    -   **Required:** Yes
    -   **Values:** *&lt;SiteDatabaseName\>* or *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **Details:** The name of the SQL Server database to create or use to install the central administration site database. Specify the same database name that was used before the failure.

        > [!IMPORTANT]  
        >  If you do not use the default instance, you must specify the instance name and site database name.

-   **Key name:** SQLSSBPort

    -   **Required:** No
    -   **Values:** &lt;*SSBPortNumber*>
    -   **Details:** Specify the SQL Server Service Broker (SSB) port used by SQL Server. Typically, SSB is configured to use TCP port 4022, but other ports are supported. Specify the same SSB port that was used before the failure.

## Recover a Primary Site Unattended
 Use the following information to configure an unattended setup script file to recover a central administration site.

 **Identification**

-   **Key name:** Action

    -   **Required:** Yes
    -   **Values:** RecoverPrimarySite
    -   **Details:** Recovers a primary site


-   **Key Name:** CDLatest

    -   **Required:** Yes – Only when using media from the CD.Latest folder.
    -   **Values:** 1
        Any value other than 1 is considered to not be using CD.Latest.
    -   **Details:** Your script must include this key and value when you run setup from media in a CD.Latest folder for the purpose of installing a primary or central administration site, or recovering a primary or central administration site. This value informs setup that media form CD.Latest is being used.

**RecoveryOptions**

-   **Key name:** ServerRecoveryOptions

    -   **Required:** Yes
    -   **Values:** 1, 2, or 4    
         1 = Recovery site server and SQL Server.   
         2 = Recover site server only.  
         4 = Recover SQL Server only.
    -   **Details:** Specifies whether setup recovers the site server, SQL Server, or both. The associated keys are required when you set the following value for the ServerRecoveryOptions setting:

        -   **Value = 1** You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.

             The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.

        -   **Value = 2** You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.

        -   **Value = 4** The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.

-   **Key name:** DatabaseRecoveryOptions

    -   **Required:** Maybe
    -   **Values:**   
         - **10** = Restore the site database from backup.  
         - **20** = Use a site database that has been manually recovered by using another method.     
         - **40** = Create a new database for the site. Use this option when there is no site database backup available. Global and site data is recovered through replication from other sites.  
         - **80** = skip database recovery.
    -   **Details:** Specifies how setup recovers the site database in SQL Server. This key is required when the **ServerRecoveryOptions** setting has a value of **1** or **4**.


-   **Key name:** SiteServerBackupLocation

    -   **Required:** No
    -   **Values:** &lt;PathToSiteServerBackupSet\>
    -   **Details:** Specifies the path to the site server backup set. This key is optional when the **ServerRecoveryOptions** setting has a value of **1** or **2**. Specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.     


-   **Key name:** BackupLocation

    -   **Required:** Maybe
    -   **Values:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Details:** Specifies the path to the site database backup set. The **BackupLocation** key is required when you configure a value of **1** or **4** for the **ServerRecoveryOptions** key, and configure a value of **10** for the **DatabaseRecoveryOptions** key.

**Options**

-   **Key name:** ProductID

    -   **Required:** Yes
    -   **Values:**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - Eval     
    -   **Details:** The Configuration Manager installation product key, including the dashes. Enter **Eval** can install the evaluation version of Configuration Manager.  


-   **Key name:** SiteCode

    -   **Required:** Yes
    -   **Values:** &lt;Site code\>
    -   **Details:** Three alpha-numeric characters that uniquely identify the site in your hierarchy. Specify the site code that was used by the site before the failure.


-   **Key name:** SiteName

    -   **Required:** Yes
    -   **Values:** SiteName
    -   **Details:** Description for this site.


-   **Key name:** SMSInstallDir

    -   **Required:** Yes
    -   **Values:** &lt;*ConfigMgrInstallationPath*>
    -   **Details:** Specifies the installation folder for the Configuration Manager program files.

        > [!NOTE]   
        >  You can specify the original path or a new  path to use for the Configuration Manager installation.

-   **Key name:** SDKServer

    -   **Required:** Yes
    -   **Values:** &lt;*FQDN of SMS Provider*>
    -   **Details:** Specifies the FQDN for the server that hosts the SMS Provider. Specify the server that hosted the SMS Provider before the failure.

         You can configure additional SMS Providers for the site after the initial installation.

-   **Key name:** PrerequisiteComp

    -   **Required:** Yes
    -   **Values:** 0 or 1    
         0 = download   
         1 = already downloaded   
    -   **Details:** Specifies whether setup prerequisite files have already been downloaded. For example, if you use a value of 0, setup downloads the files.


-   **Key name:** PrerequisitePath

    -   **Required:** Yes
    -   **Values:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Details:** Specifies the path to the setup prerequisite files. Depending on the **PrerequisiteComp** value, setup uses this path to store downloaded files or to locate previously downloaded files.


-   **Key name:** AdminConsole

    -   **Required:** Maybe
    -   **Values:** 0 or 1  
         0 = do not install   
         1 = install  
    -   **Details:** Specifies whether to install the Configuration Manager console. This key is required except when the **ServerRecoveryOptions** setting has a value of **4**.

-   **Key name:** JoinCEIP  
    > [!Note]  
    > Starting in Configuration Manager version 1802 the CEIP feature is removed from the product.

    -   **Required:** Yes
    -   **Values:** 0 or 1    
         0 = do not join  
         1 = join
    -   **Details:** Specifies whether to join the Customer Experience Improvement Program.


**SQLConfigOptions**

-   **Key name:** SQLServerName

    -   **Required:** Yes
    -   **Values:** *&lt;SQLServerName\>*
    -   **Details:** The name of the server, or clustered instance name, running SQL Server that hosts the site database. Specify the same server that hosted the site database before the failure.


-   **Key name:** DatabaseName

    -   **Required:** Yes
    -   **Values:** *&lt;SiteDatabaseName\>* or *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **Details:** The name of the SQL Server database to create or use to install the central administration site database. Specify the same database name that was used before the failure.

        > [!IMPORTANT]    
        >  If you do not use the default instance, you must specify the instance name and site database name.

-   **Key name:** SQLSSBPort

    -   **Required:** No
    -   **Values:** &lt;*SSBPortNumber*>
    -   **Details:** Specify the SQL Server Service Broker (SSB) port used by SQL Server. Typically, SSB is configured to use TCP port 4022, but other ports are supported. Specify the same SSB port that was used before the failure.

**Hierarchy ExpansionOption**

-   **Key name:** CCARSiteServer

    -   **Required:** Maybe
    -   **Values:** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **Details:** Specifies the central administration site that a primary site attaches to when it joins the Configuration Manager hierarchy. This setting is required if the primary site was attached to a central administration site before the failure. Specify the site code that was used for the central administration site before the failure.

-   **Key name:** CASRetryInterval

    -   **Required:** No
    -   **Values:** &lt;*Interval*>
    -   **Details:** Specifies the retry interval (in minutes) to attempt a connection to the central administration site after the connection fails. For example, if the connection to the central administration site fails, the primary site waits the number of minutes that you specify for CASRetryInterval, and then reattempts the connection.


-   **Key name:** WaitForCASTimeout

    -   **Required:** No
    -   **Values:** &lt;*Timeout*>
    -   **Details:** Specifies the maximum timeout value (in minutes) for a primary site to connect to the central administration site. For example, if a primary site fails to connect to a central administration site, the primary site retries the connection to the central administration site based on the CASRetryInterval until the WaitForCASTimeout period is reached. You can specify a value of 0 to 100.
