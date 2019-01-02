---
title: "Modify infrastructure"
titleSuffix: "Configuration Manager"
description: "Learn how to make changes or take actions that affect the Configuration Manager infrastructure you have deployed."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Modify your System Center Configuration Manager infrastructure

*Applies to: System Center Configuration Manager (Current Branch)*

After you install one or more sites, you might have need to modify configurations or take actions that affect the infrastructure you have deployed.  


##  <a name="BKMK_ManageSMSprovider"></a> Manage the SMS Provider  
 The SMS Provider (a dynamic-link library file: smsprov.dll) provides the point of administrative contact for one or more Configuration Manager consoles. When you install multiple SMS Providers, you can provide redundancy for contact points to administer your site and hierarchy.  

 At each Configuration Manager site, you can re-run Setup to:  

- Add an additional instance of the SMS Provider (Each additional instance of the SMS Provider must be on a separate computer)  

- Remove an instance of the SMS Provider (To remove the last SMS Provider for a site, you must uninstall the site)  

  You can monitor the installation or removal of the SMS Provider by viewing the **ConfigMgrSetup.log** in the root folder of the site server on which you run Setup.  

  Before modifying the SMS Provider at a site, be familiar with the information in [Plan for the SMS Provider for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### To manage the SMS Provider configuration for a site  

1. Run **Configuration Manager Setup** from **&lt;Configuration Manager site installation folder\>\BIN\X64\setup.exe**.  

2. On the **Getting Started** page, select **Perform site maintenance or reset this site**, and then click **Next**  

3. On the **Site Maintenance** page, select **Modify SMS Provider configuration**, and then click **Next**.  

4. On the **Manage SMS Providers** page, select one of the following options and complete the wizard by using one of the following options:  

   -   To add an additional SMS Provider at this site:  

        Select **Add a new SMS Provider**, specify the FQDN for a computer that will host the SMS Provider and does not currently host a SMS Provider, and then click **Next**.  

   -   To remove an SMS Provider from a server:  

        Select **Uninstall the specified SMS Provider**, select the name of the computer from which you want to remove the SMS Provider, click **Next**, and then confirm the action.  

       > [!TIP]  
       >  To move the SMS Provider between two computers, you must install the SMS Provider to the new computer, and remove the SMS Provider from the original location. There is no dedicated option to move the SMS Provider between computers in a single process.  

   After the Setup Wizard finishes, the SMS Provider configuration is completed. On the **General** tab in the site **Properties** dialog box, you can verify the computers that have an SMS Provider installed for a site.  

##  <a name="bkmk_Console"></a> Manage the Configuration Manager console  
 The following are tasks you can do to manage the Configuration Manager console:  

-   **Modify the language that displays in the Configuration Manager console** - To modify the installed languages   see [Manage Configuration Manager console language](#BKMK_ManageConsoleLanguages) in this topic.  

-   **Install additional consoles** - To install additional consoles, see  [Install System Center Configuration Manager consoles](/sccm/core/servers/deploy/install/install-consoles).  

-   **Configure DCOM** - To configure DCOM permission to enable consoles that are remote from the site server to connect, see  [Configure DCOM permissions for remote Configuration Manager consoles](#BKMK_ConfigDCOMforRemoteConsole) in this topic.  

-   **Modify permissions to limit what administrative users can see in the console** - To modify administrative permission, which limit what users can see and do in the console,  see [Modify the administrative scope of an administrative user](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_ModAdminUser).     

###  <a name="BKMK_ManageConsoleLanguages"></a> Manage Configuration Manager console language  
 During site server installation, the Configuration Manager console installation files and supported language packs for the site are copied to the **&lt;ConfigMgrInstallationPath\>\Tools\ConsoleSetup** subfolder on the site server.  

-   When you start the Configuration Manager console installation from this folder on the site server, the Configuration Manager console and supported language pack files are copied to the computer  

-   When a language pack is available for the current language setting on the computer, the Configuration Manager console opens in that language  

-   If the associated language pack is not available for the Configuration Manager console, the console opens in English  

For example, consider a scenario where you install the Configuration Manager console from a site server that supports English, German, and French. If you open the Configuration Manager console on a computer with a configured language setting of French, the console opens in French. If you open the Configuration Manager console on a computer with a configured language of Japanese, the console opens in English because the Japanese language pack is not available.  

 Each time the Configuration Manager console opens, it determines the configured language settings for the computer, verifies whether an associated language pack is available for the Configuration Manager console, and then opens the console by using the appropriate language pack. When you want to open the Configuration Manager console in English regardless of the configured language settings on the computer, you must manually remove or rename the language pack files on the computer.  

 Use the following procedures to start the Configuration Manager console in English regardless of the configured locale setting on the computer.  

##### To install an English-only version of the Configuration Manager console on computers  

1.  In Windows Explorer, browse to **&lt;ConfigMgrInstallationPath\>\Tools\ConsoleSetup\LanguagePack**  

2.  Rename the **.msp** and **.mst** files. For example, you could change **&lt;file name\>.MSP** to **&lt;file name\>.MSP.disabled**.  

3.  Install the Configuration Manager console on the computer.  

    > [!IMPORTANT]  
    >  When new server languages are configured for the site server, the .msp and .mst files are recopied to the **LanguagePack** folder, and you must repeat this procedure to install new Configuration Manager consoles in only English.  

##### To temporarily disable a console language on an existing Configuration Manager console installation  

1.  On the computer that is running the Configuration Manager console, close the Configuration Manager console.  

2.  In Windows Explorer, browse to &lt;*ConsoleInstallationPath*>\Bin\ on the Configuration Manager console computer.  

3.  Rename the appropriate language folder for the language that is configured on the computer. For example, if the language settings for the computer were set for German, you could rename the **de** folder to **de.disabled**.  

4.  To open the Configuration Manager console in the language that is configured for the computer, rename the folder to the original name. For example, rename **de.disabled** to **de**.  

##  <a name="BKMK_ConfigDCOMforRemoteConsole"></a> Configure DCOM permissions for remote Configuration Manager consoles  
 The user account that runs the Configuration Manager console requires permission to access the site database by using the SMS Provider. However, an administrative user who uses a remote Configuration Manager console also requires **Remote Activation** DCOM permissions on:  

- The site server computer  

- Each computer that hosts an instance of the SMS Provider  

  The  security group named **SMS Admins** grants access to the SMS Provider on a computer, and can also be used to grant the required DCOM permissions. (This group is local to the computer when the SMS Provider runs on a member server, and is a domain local group when the SMS Provider runs on a domain controller.)  

> [!IMPORTANT]  
>  The Configuration Manager console uses Windows Management Instrumentation (WMI) to connect to the SMS Provider, and WMI internally uses DCOM. Therefore, Configuration Manager requires permissions to activate a DCOM server on the SMS Provider computer if the Configuration Manager console is running on a computer other than the SMS Provider computer. By default, Remote Activation is granted only to the members of the built-in Administrators group. If you allow the SMS Admins group to have Remote Activation permission, a member of this group could attempt DCOM attacks against the SMS Provider computer. This configuration also increases the attack surface of the computer. To mitigate this threat, carefully monitor the membership of the SMS Admins group.  

 Use the following procedure to configure each central administration site, primary site server, and each computer where the SMS Provider is installed to grant remote Configuration Manager console access for administrative users.  

#### To configure DCOM permissions for remote Configuration Manager console connections  

1. Open  **Component Services** by running **Dcomcnfg.exe**.  

2. In **Component Services**, click **Console root** >  **Component Services** > **Computers**, and then click **My Computer**. On the **Action** menu, click **Properties**.  

3. In the **My Computer Properties** dialog box, on the **COM Security** tab, in the **Launch and Activation Permissions** section, click **Edit Limits**.  

4. In the **Launch and Activation Permissions** dialog box, click **Add**.  

5. In the **Select User, Computers, Service Accounts, or Groups** dialog box, in the **Enter the object names to select (examples)** box, type **SMS Admins**, and then click **OK**.  

   > [!NOTE]  
   >  You might have to change the setting for **From this Location** to locate the SMS Admins group. This group is local to the computer when the SMS Provider runs on a member server, and is a domain local group when the SMS Provider runs on a domain controller.  

6. In the **Permissions for SMS Admins** section, to allow remote activation, select the **Remote Activation** check box.  

7. Click **OK** and click **OK** again, and then close **Computer Management**. Your computer is now configured to allow remote Configuration Manager console access to members of the SMS Admins group.  

   Repeat this procedure on each SMS Provider computer that might support remote Configuration Manager consoles.  

##  <a name="bkmk_dbconfig"></a> Modify the site database configuration  
 After you install a site, you can modify the configuration of the site database and site database server by running Setup on a central administration site server or primary site server. You can move the site database to a new instance of SQL Server on the same computer, or to a different computer that runs a supported version of SQL Server. These and related changes are not supported for the database configuration at secondary sites.  

 For more information about the limits of support, see [Support policy for manual database changes in a Configuration Manager environment](https://support.microsoft.com/kb/3106512).  

> [!NOTE]  
>  When you modify the database configuration for a site, Configuration Manager restarts or reinstalls Configuration Manager services on the site server and remote site system servers that communicate with the database.  

**To modify the database configuration**, you must run Setup on the site server and select the option **Perform site maintenance or reset this site**. Next, select the **Modify SQL Server configuration** option. You can change the following site database configurations:  

-   The Windows-based server that hosts the database.  

-   The instance of SQL Server in use on a server that hosts the SQL Server database.  

-   The database name.  

-   SQL Server Port in use by Configuration Manager  

-   SQL Server Service Broker port in use by Configuration Manager  

**If you move the site database, you must configure the following:**  

-   **Configure access:** When you move the site database to a new computer, add the computer account of the site server to the **Local Administrators** group on the computer that runs SQL Server. If you use a SQL Server cluster for the site database, you must add the computer account to the **Local Administrators** group of each Windows Server cluster node computer.  

-   **Enable common language runtime (CLR) integration:**  When you move the database to a new instance on SQL Server, or to a new SQL Server computer, you must enable common language runtime (CLR) integration. To enable CLR, use **SQL Server Management Studio** to connect to the instance of SQL Server that hosts the site database and run the following stored procedure as a query: **sp_configure 'clr enabled',1; reconfigure**.  
-  **Ensure the new SQL Server has access to the backup location:** When you use a UNC for storing your site database backup, after moving the database to a new server, including a move a SQL Server AlwaysOn availability group or to a SQL Server cluster, ensure the computer account of the new SQL Server has **write** permissions to the UNC location.  


> [!IMPORTANT]  
>  Before you move a database that has one or more database replicas for management points, you must first remove the database replicas. After you complete the database move, you can reconfigure database replicas. For more information see [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

##  <a name="bkmk_SPN"></a> Manage the SPN for the site database server  
You can choose the account that runs  SQL Services for the site database:  

-   When the services run with the computers system account, the SPN is automatically registered for you.  

-   When the services run with a domain local user account, you must manually register the SPN to ensure SQL clients and other site system can perform Kerberos authentication. Without Kerberos authentication, communication to the database might fail.  

SQL Server documentation can help you [manually register the SPN](https://technet.microsoft.com/library/ms191153\(v=sql.120\).aspx), and provide additional background about SPNs and Kerberos connections.  

> [!IMPORTANT]
> - When you create an SPN for a clustered SQL Server, you must specify the virtual name of the SQL Server Cluster as the SQL Server computer name  
>   -   The command to register an SPN for a SQL Server named instance is the same as that you use when you register an SPN for a default instance except that the port number must match the port that is used by the named instance  

You can register an SPN for the SQL Server service account of the site database server by using the **Setspn** tool. You must run the Setspn tool on a computer that resides in the domain of SQL Server, and it must use Domain Administrator credentials to run.  

 Use the following procedures as examples of how to manage the SPN for the SQL Server service account that uses the Setspn tool on Windows Server 2008 R2. For specific guidance about Setspn, see [Setspn Overview](http://go.microsoft.com/fwlink/p/?LinkId=226343), or similar documentation specific to your operating system.  

> [!NOTE]  
>  The following procedures reference the Setspn command-line tool. The Setspn command-line tool is included when you install Windows Server 2003 Support Tools from the product CD or from the [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=100114). For more information about how to install Windows Support Tools from the product CD, see [Install Windows Support Tools](http://go.microsoft.com/fwlink/p/?LinkId=62270).  

#### To manually create a domain user Service Principal Name (SPN) for the SQL Server service account  

1.  On the **Start** menu, click **Run**, and then enter **cmd** in the Run dialog box.  

2.  At the command line, navigate to the Windows Server support tools installation directory. By default, these tools are located in the **C:\Program Files\Support Tools** directory.  

3.  Enter a valid command to create the SPN. To create the SPN, you can use the NetBIOS name or the fully qualified domain name (FQDN) of the computer running SQL Server. However, you must create an SPN for both the NetBIOS name and the FQDN.  

    > [!IMPORTANT]  
    >  When you create an SPN for a clustered SQL Server, you must specify the virtual name of the SQL Server Cluster as the SQL Server computer name.  

    -   To create an SPN for the NetBIOS name of the SQL Server computer, type the following command: **setspn -A MSSQLSvc/&lt;SQL Server computer name\>:1433 &lt;Domain\Account>**  

    -   To create an SPN for the FQDN of the SQL Server computer, type the following command: **setspn -A MSSQLSvc/&lt;SQL Server FQDN\>:1433 &lt;Domain\Account>**  

    > [!NOTE]  
    >  The command to register an SPN for a SQL Server named instance is the same as that you use when you register an SPN for a default instance except that the port number must match the port that is used by the named instance.  

#### To verify the domain user SPN is registered correctly by using the Setspn command  

1.  On the **Start** menu, click **Run**, and then enter **cmd** in the **Run** dialog box.  

2.  At the command prompt, enter the following command: **setspn -L &lt;domain\SQL Service Account>**.  

3.  Review the registered **ServicePrincipalName** to ensure that a valid SPN has been created for the SQL Server.  

#### To verify the domain user SPN is registered correctly when using the ADSIEdit MMC console  

1.  On the **Start** menu, click **Run**, and then enter **adsiedit.msc** to start the ADSIEdit MMC console.  

2.  If necessary, connect to the domain of the site server.  

3.  In the console pane, expand the site server's domain, expand **DC=&lt;server distinguished name\>**, expand **CN=Users**, right-click **CN=&lt;Service Account User\>**, and then click **Properties**.  

4.  In the **CN=&lt;Service Account User\> Properties** dialog box, review the **servicePrincipalName** value to ensure that a valid SPN has been created and associated with the correct SQL Server computer.  

#### To change the SQL Server service account from local system to a domain user account  

1.  Create or select a domain or local system user account that you want to use as the SQL Server service account.  

2.  Open **SQL Server Configuration Manager**.  

3.  Click **SQL Server Services**, and then double-click **SQL Server&lt;INSTANCE NAME\>**.  

4.  On the **Log on** tab, select **This account**, and then enter the user name and password for the domain user account created in step 1, or click **Browse** to find the user account in Active Directory Domain Services, and then click **Apply**.  

5.  Click **Yes** in the **Confirm Account Change** dialog box to confirm the service account change and restart the SQL Server Service.  

6.  Click **OK** after the service account has been successfully changed.  

##  <a name="bkmk_reset"></a> Run a site reset  
 When a site reset runs at a central administration site or primary site, the  site:  

-   Reapplies the default Configuration Manager file and registry permissions  

-   Reinstalls all site components and all site system roles at the site  

Secondary sites do not support a site reset.  

Site resets can be run manually, when you choose, but can also run automatically after you modify the site configuration.  

For example, if there has been a change to the accounts used by Configuration Manager components, you should consider a manual site reset to ensure the site  components update to use the new account details. However, if you modify the client or server languages at a site, Configuration Manager automatically runs a site reset because the reset is required before a site can use this change.  

> [!NOTE]  
>  A site reset does not reset access permissions to non-Configuration Manager objects.  

When a site reset runs:  

1.  Setup stops and restarts the **SMS_SITE_COMPONENT_MANAGER** service and the thread components of the **SMS_EXECUTIVE** service.  

2.  Setup removes, and then re-creates, the site system share folder and the **SMS Executive** component on the local computer and on remote site system computers.  

3.  Setup restarts the **SMS_SITE_COMPONENT_MANAGER** service, this service installs the **SMS_EXECUTIVE** and the **SMS_SQL_MONITOR** services.  

In addition, a site reset restores the following objects:  

-   The **SMS** or **NAL** registry keys, and any default subkeys under these keys.  

-   The Configuration Manager file directory tree, and any default files or subdirectories in this file directory tree.  

**Prerequisites to run a site reset**  

The account that you use to perform a site reset must have the following permissions:  

-   The account that you use to perform a site reset must have the following permissions:  

    -   **Central administration site**: The account that you use to run a site reset at this site must be a local administrator on the central administration site server and must have privileges that are equivalent to the **Full Administrator** role-based administration security role.  

    -   **Primary site**: The account that you use to run a site reset at this site must be a local administrator on the primary site server and must have privileges that are equivalent to the **Full Administrator** role-based administration security role. If the primary site is in a hierarchy with a central administration site, this account must also be a local administrator on the central administration site server.  

**Limitations for a site reset**
  -	Beginning with version 1602, you cannot use a site reset to change the Server or Client language packs that installed at sites so long as the hierarchy is configured to support [testing client upgrades in a pre-production collection](/sccm/core/clients/manage/upgrade/test-client-upgrades).

#### To perform a site reset  

1.  Run **Configuration Manager Setup** from **&lt;Configuration Manager site installation folder\>\BIN\X64\setup.exe**.  

    > [!TIP]  
    >  You can also run a site reset by starting Configuration Manager Setup on the **Start** menu of the site server computer or from the Configuration Manager source media.  

2.  On the **Getting Started** page, select **Perform site maintenance or reset this site**, and then click **Next**.  

3.  On the **Site Maintenance** page, select **Reset site with no configuration changes**, and then click **Next**.  

4.  Click **Yes** to begin the site reset.  

When the site reset is finished, click **Close** to complete this procedure.  

##  <a name="bkmk_sitelang"></a> Manage language packs at a site  
After a site installs,  you can change the server and client language packs that are in use:  

**Server language packs:**  

-   **Applies to:**  

     Configuration Manager console installations  

     New installations of applicable site system roles  

-   **Details:**  

     After you update the server language packs at a site, you can add support for the language packs to Configuration Manager consoles.  

     To add support for a server language pack to a Configuration Manager console, you must install the Configuration Manager console from the **ConsoleSetup** folder on a site server that includes the language pack that you want to use. If the Configuration Manager console is already installed, you must first uninstall it to enable the new installation to identify the current list of supported language packs.  

**Client language packs:**  

-   **Applies to:**  

     Changes to the client language packs update the client installation source files so that new client installations and upgrades  add support for the updated list of client languages.  

-   **Details:**  

     After you update the client language packs at a site, you must install each client that will use the language packs by using source files that include the client language packs.  

For information about the client and server languages that are supported by Configuration Manager, see [Language Packs in System Center Configuration Manager](../../../core/servers/deploy/install/language-packs.md)  

#### To modify the language packs that are supported at a site  

1.  On the site server, run Configuration Manager Setup from **&lt;Configuration Manager site installation folder\>\BIN\X64\setup.exe.**  

2.  On the **Getting Started** page, select **Perform site maintenance or reset this Site**, and then click **Next**.  

3.  On the **Site Maintenance** page, select **Modify language configuration**, and then click **Next**.  

4.  On the **Prerequisites Downloads** page, select **Download required files** to acquire updates to language packs, or select **Use previously downloaded files** to use previously downloaded files that include the language packs you want to add to the site. Click **Next** to validate the files and continue.  

5.  On the **Server Language Selection** page, select the check box for server languages this site supports, and then click **Next**.  

6.  On the **Client Language Selection** page, select the check box for client languages that this site supports, and then click **Next**.  

7.  Click **Next**, to modify language support at the site.  

    > [!NOTE]  
    >  Configuration Manager initiates a site reset which also reinstalls all site system roles at the site.  

8.  Click **Close** to complete this procedure.  

##  <a name="BKMK_ModDBAlert"></a> Modify the database server alert threshold  
 By default, Configuration Manager generates alerts when free disk space on a site database server is low. The defaults are set to generate a warning when there is 10 GB or less of free disk space, and a critical alert when there is 5 GB or less of free disk space. You can modify these values or disable alerts for each site.  

 To change these settings:  

1.  In the **Administration** workspace, expand **Site Configuration**, and then click **Sites**.  

2.  Select the site that you want to configure and open that site's **Properties**.  

3.  In the site's **Properties** dialog box, select the **Alert** tab, and then edit the settings.  

4.  Click **OK** to close the site properties dialog box.  
