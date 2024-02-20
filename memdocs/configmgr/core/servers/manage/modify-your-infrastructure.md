---
title: Modify infrastructure
titleSuffix: Configuration Manager
description: Make changes or take actions that affect your Configuration Manager infrastructure.
ms.date: 04/01/2020
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Modify your Configuration Manager infrastructure

*Applies to: Configuration Manager (current branch)*

After you install one or more sites, you might have need to modify configurations or take actions that affect your infrastructure.

## <a name="BKMK_ManageSMSprovider"></a> Manage the SMS provider

The SMS provider provides the point of administrative contact for one or more Configuration Manager consoles. When you install multiple SMS providers, you can provide redundancy for contact points to administer your site and hierarchy.

At each Configuration Manager site, you can rerun setup to:

- Add an additional instance of the SMS provider. Each additional instance of the SMS provider must be on a separate computer.

- Remove an instance of the SMS provider. To remove the last SMS provider for a site, you must uninstall the site.

Monitor the installation or removal of the SMS provider by viewing the **ConfigMgrSetup.log** in the root folder of the site server on which you run setup.

Before you modify the SMS provider at a site, see [Plan for the SMS provider](../../plan-design/hierarchy/plan-for-the-sms-provider.md).

### Manage the SMS provider configuration for a site  

1. Run **Configuration Manager Setup** from `\BIN\X64\setup.exe` in the Configuration Manager site installation folder.

1. On the **Getting Started** page, select **Perform site maintenance or reset this site**.

1. On the **Site Maintenance** page, select **Modify SMS provider configuration**.

1. On the **Manage SMS providers** page, select one of the following options:

    - **Add a new SMS provider**: Specify the FQDN for a computer to host the SMS provider that doesn't currently host it.

    - **Uninstall the specified SMS provider**: Select the name of the computer from which you want to remove the SMS provider.

    > [!TIP]  
    > To move the SMS provider between two computers, first install it to the new computer. Then remove it from the original location. There's no option to move the SMS provider between computers.

After the setup wizard finishes, the SMS provider configuration is complete. In the site **Properties**, on the **General** tab, verify the computers that have an SMS provider installed for a site.

## <a name="bkmk_Console"></a> Manage the Configuration Manager console

The following tasks help you manage the Configuration Manager console:

- To modify the language that displays in the Configuration Manager console, see the [Manage Configuration Manager console language](#BKMK_ManageConsoleLanguages) section.

- To install additional consoles, see [Install Configuration Manager consoles](../deploy/install/install-consoles.md).

- To configure DCOM permissions to enable consoles that are remote from the site server, see the [Configure DCOM permissions for remote Configuration Manager consoles](#BKMK_ConfigDCOMforRemoteConsole) section.

- To modify administrative permissions to limit what users can see and do in the console, see [Modify the administrative scope of an administrative user](../deploy/configure/configure-role-based-administration.md#modify-the-administrative-scope-of-an-administrative-user).

### <a name="BKMK_ManageConsoleLanguages"></a> Manage Configuration Manager console language

During site server installation, the Configuration Manager console installation files and supported language packs for the site are copied to the `\Tools\ConsoleSetup` subfolder of the Configuration Manager installation path on the site server.

- When you start the Configuration Manager console installation from this folder on the site server, it copies the Configuration Manager console and supported language pack files to the computer.

- When a language pack is available for the current language setting on the computer, the Configuration Manager console opens in that language.

- If the associated language pack isn't available for the Configuration Manager console, the console opens in English (United States).

For example, you install the Configuration Manager console from a site server that supports English, German, and French. If you open the Configuration Manager console on a computer with a configured language setting of French, the console opens in French. If you open the Configuration Manager console on a computer with a configured language of Japanese, the console opens in English because the Japanese language pack isn't available.  

Each time the Configuration Manager console opens:

- Tt determines the configured language settings for the computer
- Verifies whether an associated language pack is available for the Configuration Manager console
- Opens the console by using the appropriate language pack

When you want to open the Configuration Manager console in English regardless of the configured language settings on the computer, remove or rename the language pack files on the computer.

Use the following procedures to start the Configuration Manager console in English regardless of the configured locale setting on the computer.  

#### Install an English-only version of the Configuration Manager console on computers  

1. In Windows Explorer, browse to `\Tools\ConsoleSetup\LanguagePack` in the Configuration Manager installation path.

1. Rename the **.msp** and **.mst** files. For example, you could change **&lt;file name\>.MSP** to **&lt;file name\>.MSP.disabled**.

1. Install the Configuration Manager console on the computer.

    > [!IMPORTANT]
    > When new server languages are configured for the site server, the .msp and .mst files are recopied to the **LanguagePack** folder, and you must repeat this procedure to install new Configuration Manager consoles in only English.  

#### Temporarily disable a console language on an existing Configuration Manager console installation

1. On the computer that is running the Configuration Manager console, close the Configuration Manager console.

1. In Windows Explorer, browse to &lt;*ConsoleInstallationPath*>\Bin\ on the Configuration Manager console computer.  

1. Rename the appropriate language folder for the language that is configured on the computer. For example, if the language settings for the computer were set for German, you could rename the **de** folder to **de.disabled**.  

1. To open the Configuration Manager console in the language that is configured for the computer, rename the folder to the original name. For example, rename **de.disabled** to **de**.  

## <a name="BKMK_ConfigDCOMforRemoteConsole"></a> Configure DCOM permissions for remote consoles

The user account that runs the Configuration Manager console requires permission to access the site database by using the SMS provider. However, an administrative user who uses a remote Configuration Manager console also requires **Remote Activation** DCOM permissions on:

- The site server computer

- Each computer that hosts an instance of the SMS provider

The security group named **SMS Admins** grants access to the SMS provider on a computer, and can also be used to grant the required DCOM permissions. This group is local to the computer when the SMS provider runs on a member server. It's a domain local group when the SMS provider runs on a domain controller.

> [!IMPORTANT]
> The Configuration Manager console uses WMI to connect to the SMS provider, and WMI internally uses DCOM. If the Configuration Manager console runs on a computer other than the SMS provider computer, it requires permissions to activate a DCOM server on the SMS provider computer. By default, Remote Activation is granted only to the members of the built-in Administrators group.
>
> If you allow the SMS Admins group to have Remote Activation permission, a member of this group could attempt DCOM attacks against the SMS provider computer. This configuration also increases the attack surface of the computer. To mitigate this threat, carefully monitor the membership of the SMS Admins group.

Use the following procedure to configure each central administration site (CAS), primary site server, and each computer where the SMS provider is installed to grant remote Configuration Manager console access for administrative users.

### Configure DCOM permissions for remote Configuration Manager console connections

1. As an administrator on the target computer, run `Dcomcnfg.exe` to open **Component Services**.

1. Expand **Component Services**, expand **Computers**, and then select **My Computer**. On the **Action** menu, select **Properties**.

1. In the **My Computer Properties** window, switch to the **COM Security** tab. In the **Launch and Activation Permissions** section, select **Edit Limits**.

1. In the **Launch and Activation Permissions** window, select **Add**.

1. In the **Select Users, Computers, Service Accounts, or Groups** window, in the **Enter the object names to select** field, type `SMS Admins`, and then select **OK**.

   > [!TIP]
   > To locate the SMS Admins group, you might have to change the setting: **From this Location**. This group is local to the computer when the SMS provider runs on a member server, and is a domain local group when the SMS provider runs on a domain controller.

1. In the **Permissions for SMS Admins** section, to allow remote activation, select the **Allow** column for the **Remote Activation** row.

1. Select **OK** to save changes and close all windows.

Your computer is now configured to allow remote Configuration Manager console access to members of the SMS Admins group.

Repeat this procedure on each SMS provider computer that supports remote Configuration Manager consoles.

## <a name="bkmk_dbconfig"></a> Modify the site database configuration

After you install a site, you can modify the configuration of the site database and site database server. Run Configuration Manager setup on a CAS server or primary site server to make changes. You can move the site database to a new instance of SQL Server on the same computer, or to a different computer that runs a supported version of SQL Server. These changes aren't supported for the database configuration at secondary sites.

For more information about the limits of support, see [Support policy for manual database changes in a Configuration Manager environment](https://support.microsoft.com/kb/3106512).  

> [!NOTE]
> When you modify the database configuration for a site, Configuration Manager restarts or reinstalls Configuration Manager services on the site server and remote site system servers that communicate with the database.

### Modify the database configuration

Run Configuration Manager setup on the site server, and select the option **Perform site maintenance or reset this site**. Then select the **Modify SQL Server configuration** option. You can change the following site database configurations:

- The Windows-based server that hosts the database.

- The instance of SQL Server in use on a server that hosts the SQL Server database.

- The database name.

- SQL Server port in use by Configuration Manager.

- SQL Server Service Broker port in use by Configuration Manager.

### Move the site database

If you move the site database, also review the following configurations:

- When you move the site database to a new computer, add the computer account of the site server to the local **Administrators** group on the computer that runs SQL Server. If you use a SQL Server Always On failover cluster instance for the site database, add the computer account to the local **Administrators** group of each Windows Server cluster node computer.

- When you move the database to a new instance on SQL Server, or to a new SQL Server computer, enable common language runtime (CLR) integration. Use **SQL Server Management Studio** to connect to the instance of SQL Server that hosts the site database. Then run the following stored procedure as a query: `sp_configure 'clr enabled',1; reconfigure`

- Make sure the new SQL Server has access to the backup location. When you use a UNC for storing your site database backup, after moving the database to a new server, make sure the computer account of the new SQL Server has **write** permissions to the UNC location. This configuration includes when you move to a SQL Server Always On availability group or a failover cluster instance.

> [!IMPORTANT]
> Before you move a database that has one or more database replicas for management points, first remove the database replicas. After you complete the database move, you can reconfigure database replicas. For more information, see [Database replicas for management points](../deploy/configure/database-replicas-for-management-points.md).

## <a name="bkmk_SPN"></a> Manage the SPN for the site database server

You can choose the account that runs SQL Server services for the site database:

- When the services run with the computers system account, it automatically registers the service principal name (SPN) for you.

- When the services run with a domain local user account, manually register the SPN. The SPN allows SQL Server clients and other site systems to authenticate with Kerberos. Without Kerberos authentication, communication to the database might fail.

For more information about SPNs and Kerberos connections, see [Register a service principal name for Kerberos connections](/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections).

Register an SPN for the SQL Server service account of the site database server by using the **Setspn** tool. Run Setspn as a Domain Administrator on a computer in the same domain as the SQL Server.

The following procedures are examples of how to manage the SPN for the SQL Server service account. For more information about Setspn, see [Setspn Overview](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\)).

### Manually create a domain user SPN for the SQL Server service account

1. Open a command prompt as an administrator.

1. Enter a valid command to create the SPN for both the NetBIOS name and the FQDN:

    > [!IMPORTANT]
    > When you create an SPN for a SQL Server Always On failover cluster instance, specify the virtual name of the failover cluster instance as the SQL Server computer name.

    - NetBIOS name: `setspn -A MSSQLSvc/<SQL Server computer name>:<port> <Domain\Account>`

        For example: `setspn -A MSSQLSvc/sqlserver:1433 contoso\sqlservice`

    - FQDN: `setspn -A MSSQLSvc/<SQL Server FQDN>:<port> <Domain\Account>`

        For example: `setspn -A MSSQLSvc/sqlserver.contoso.com:1433 contoso\sqlservice`

    > [!NOTE]
    > The command to register an SPN for a SQL Server named instance is the same as that you use when you register an SPN for a default instance. The only exception is that the port number must match the port that the named instance uses.

### Verify the domain user SPN is registered correctly

1. Open a command prompt as an administrator.

1. Enter the following command: `setspn -L <domain\SQL Server service account>`

    For example: `setspn -L contoso\sqlservice`

1. Review the registered **ServicePrincipalName**. Make sure that you created a valid SPN for the SQL Server.

### Change the SQL Server service account from local system to a domain user account

1. Create or select a domain or local system user account that you want to use as the SQL Server service account.

1. Open **SQL Server Configuration Manager**.

1. Select **SQL Server Services**, and then open **SQL Server&lt;INSTANCE NAME\>**.

1. Switch to the **Log on** tab. Select **This account**, and then enter the user name and password for the domain user account from step 1.

1. Confirm the service account change and restart the SQL Server service.

## <a name="bkmk_reset"></a> Run a site reset

When a site reset runs at a CAS or primary site, the site:

- Reapplies the default Configuration Manager file and registry permissions

- Reinstalls all site components and all site system roles

Secondary sites don't support site reset.

You can manually reset a site. They can also run automatically after you modify the site configuration. For example:

- If there has been a change to the accounts used by Configuration Manager components, consider a manual site reset. This action makes sure the site components update to use the new account details.

- If you modify the client or server languages at a site, Configuration Manager automatically runs a site reset. The site requires a reset to use the new languages.

> [!NOTE]
> A site reset doesn't reset access permissions to non-Configuration Manager objects.

### What happens during a site reset

When a site reset runs:

1. Setup stops and restarts the **SMS_SITE_COMPONENT_MANAGER** service and the thread components of the **SMS_EXECUTIVE** service.

1. Setup removes and recreates the site system share folder and the **SMS Executive** component on the local computer and on remote site system computers.

1. Setup restarts the **SMS_SITE_COMPONENT_MANAGER** service, which installs the **SMS_EXECUTIVE** and the **SMS_SQL_MONITOR** services.

Site reset restores the following objects:

- The **SMS** or **NAL** registry keys, and any default subkeys under these keys.

- The Configuration Manager file directory tree, and any default files or subdirectories in this file directory tree.

### Prerequisites for site reset

The account that you use to reset a site must have the following permissions:

- To reset the CAS:

  - A local **Administrator** on the CAS server

  - Privileges that are equivalent to the **Full Administrator** role-based administration security role

- To reset a primary site:

  - A local **Administrator** on the primary site server

  - Privileges that are equivalent to the **Full Administrator** role-based administration security role
  
  - If the primary site is in a hierarchy with a CAS, this account must also be a local **Administrator** on the CAS server.

### Limitations for a site reset

If the hierarchy is configured to support [testing client upgrades in a pre-production collection](../../clients/manage/upgrade/test-client-upgrades.md), you can't use a site reset to change the server or client language packs at sites.

### Run a site reset

1. Start Configuration Manager setup on the site server by using one of the following methods:

    - On the **Start** menu, select **Configuration Manager Setup**.

    - In the directory for the Configuration Manager *installation media*, open `\SMSSETUP\BIN\X64\setup.exe`. Make sure this version is the same as the site version.

    - In the directory where Configuration Manager is *installed*, open `\BIN\X64\setup.exe`.

1. On the **Getting Started** page, select **Perform site maintenance or reset this site**.

1. On the **Site Maintenance** page, select **Reset site with no configuration changes**.

1. Select **Yes** to begin the site reset.

## <a name="bkmk_sitelang"></a> Manage language packs at a site

After a site installs, you can change the server and client language packs that are in use.

### Server language packs

*Applies to: Configuration Manager console installations, new installations of applicable site system roles*

After you update the server language packs at a site, you can add support for the language packs to Configuration Manager consoles.

To add support for a server language pack to a Configuration Manager console, install the Configuration Manager console from the **ConsoleSetup** folder on a site server that includes the language pack that you want to use. If the Configuration Manager console is already installed, you must first uninstall it to enable the new installation to identify the current list of supported language packs.

### Client language packs

Changes to the client language packs update the client installation source files. New client installations and upgrades add support for the updated list of client languages.

After you update the client language packs at a site, install each client that will use the language packs by using source files that include the client language packs.

For more information about the client and server languages that Configuration Manager supports, see [Language Packs](../deploy/install/language-packs.md).

### Modify the supported language packs at a site

1. Start Configuration Manager setup on the site server by using one of the following methods:

    - On the **Start** menu, select **Configuration Manager Setup**.

    - In the directory for the Configuration Manager *installation media*, open `\SMSSETUP\BIN\X64\setup.exe`. Make sure this version is the same as the site version.

    - In the directory where Configuration Manager is *installed*, open `\BIN\X64\setup.exe`.

1. On the **Getting Started** page, select **Perform site maintenance or reset this Site**.

1. On the **Site Maintenance** page, select **Modify language configuration**.

1. On the **Prerequisites Downloads** page, select one of the following options:

    - **Download required files**: Acquire updates to language packs.

    - **Use previously downloaded files**: Use previously downloaded files that include the language packs you want to add to the site.

1. On the **Server Language Selection** page, select the server languages this site supports.

1. On the **Client Language Selection** page, select the client languages that this site supports.

1. Complete the wizard to modify language support at the site.

    > [!NOTE]
    > Configuration Manager initiates a site reset which also reinstalls all site system roles at the site.

## <a name="BKMK_ModDBAlert"></a> Modify the database server alert threshold

By default, Configuration Manager generates alerts when free disk space on a site database server is low:

- Generate a warning when there's 10 GB or less of free disk space
- Generate a critical alert when there's 5 GB or less of free disk space

You can modify these values or disable alerts for each site:

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

1. Select the site that you want to configure. In the ribbon, select **Properties**.

1. Switch to the **Alert** tab, and then edit the settings.

## Uninstall sites and hierarchies

You may need to uninstall a Configuration Manager site system role, site, or hierarchy. For more information, see [Uninstall roles, sites, and hierarchies](../deploy/install/uninstall-sites-and-hierarchies.md).

Starting in version 2002, you can also remove the CAS from a hierarchy, but keep the primary site. For more information, see [Remove the CAS](../deploy/install/remove-central-administration-site.md).