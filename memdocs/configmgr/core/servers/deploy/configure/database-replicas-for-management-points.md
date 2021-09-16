---
title: Management point database replicas
titleSuffix: Configuration Manager
description: Use a database replica to reduce the CPU load placed on the site database server by management points.
ms.date: 04/27/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Database replicas for management points for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager primary sites can use a database replica to reduce the CPU load placed on the site database server by management points as they service requests from clients. When a management point uses a database replica, it requests data from the SQL Server computer that hosts the database replica instead of from the site database server.

This configuration can help reduce the CPU processing requirements on the site database server by offloading frequent processing tasks related to clients. An example of frequent processing tasks for clients includes sites where there are a large number of clients that make frequent requests for client policy.

## About

- Replicas are a partial copy of the site database that replicates to a separate instance of  SQL Server.

  - Primary sites support a dedicated database replica for each management point at the site.

  - Secondary sites don't support database replicas.

  - A single database replica can be used by more than a one management point from the same site.

  - A SQL Server can host multiple database replicas for use by different management points so long as each runs in a separate instance of SQL Server.

- Replicas synchronize a copy of the site database on a fixed schedule from data that the site's database server publishes for this purpose.

- You can configure management points to use a replica when you install it, or at a later time. For an existing management point, reconfigure it to use the database replica.

- Regularly monitor the site database server and each database replica server to make sure that replication occurs between them. Make sure that the performance of the database replica server is sufficient for the site and client performance that you require.

## Prerequisites

### SQL Server requirements

- The SQL Server that hosts the database replica has the same requirements as the site database server. The replica server doesn't need to run the same version or edition of SQL Server as the site database server, as long as it runs a supported version and edition of SQL Server. For more information, see [Support for SQL Server versions](../../../../core/plan-design/configs/support-for-sql-server-versions.md).

- The SQL Server service on the computer that hosts the replica database must run as the **System** account.

- Both the SQL Server that hosts the site database and that hosts a database replica must have **SQL Server replication** installed.

- The site database must *publish* the database replica, and each remote database replica server must *subscribe* to the published data.

- Configure both SQL Servers to support a **max text repl size** of 2 GB. For more information and how to configure this setting for SQL Server, see [Configure the max text repl size Server Configuration Option](/sql/database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option).

### Self-signed certificate

To configure a database replica, create a self-signed certificate on the database replica server. Make this certificate available to each management point that will use that database replica server.

- The certificate is automatically available to a management point that's installed on the database replica server.

- To make this certificate available to remote management points, first export the certificate. Then add it to the **Trusted People** certificate store on the remote management point.

### Client notification

To support client notification with a database replica for a management point, configure communication between the site database server and the database replica server for the **SQL Server Service Broker**:

- Configure each database with information about the other database.

- Exchange certificates between the two databases for secure communication.

## Limitations

- When you configure the site to publish database replicas, use the following procedures instead of the normal guidance:

  - [Uninstall a site server that publishes a database replica](#BKMK_DBReplicaOps_Uninstall)

  - [Move a site server database that publishes a database replica](#BKMK_DBReplicaOps_Move)

- User deployments in Software Center won't work against a management point using a SQL Server replica. <!--sccmdocs-1011-->

- Upgrades to Configuration Manager current branch: Before you upgrade a site, either from System Center 2012 Configuration Manager to Configuration Manager current branch or updating Configuration Manager current branch to the latest release, disable database replicas for management points. After your site upgrades, you can reconfigure the database replicas for management points.

- Multiple replicas on a single SQL Server: If you configure separate instances of a database replica server to host multiple database replicas for management points, use a modified configuration script. As noted in step 4 of the process to [Configure database replicas](#BKMK_DBReplica_Cert), this action prevents overwriting the self-signed certificate in use by previously configured database replicas on that server.

## <a name="BKMK_DBReplica_Config"></a> Configure

To configure a database replica, the following steps are required:

- [Step 1 - Configure the site database server to Publish the database replica](#BKMK_DBReplica_ConfigSiteDB)

- [Step 2 - Configuring the database replica server](#BKMK_DBReplica_ConfigSrv)

- [Step 3 - Configure management points to use the database replica](#BKMK_DBReplica_ConfigMP)

- [Step 4 -Configure a self-signed certificate for the database replica server](#BKMK_DBReplica_Cert)

- [Step 5 - Configure the SQL Server Service Broker for the database replica server](#BKMK_DBreplica_SSB)

### <a name="BKMK_DBReplica_ConfigSiteDB"></a> Step 1 - Configure the site database server to publish the database replica

Use the following procedure as an example of how to configure the site database server to publish the database replica. The specific steps might vary depending upon the version of Windows Server.

Do the following steps on the site database server:

1. Set the SQL Server Agent to automatically start.

1. Create a local user group with the name **ConfigMgr_MPReplicaAccess**. For each database replica server that you use at this site, add its computer account to this group. This action enables those database replica servers to synchronize with the published database replica.

    > [!NOTE]
    > You can also create a domain group for this purpose.

1. Configure a file share with the name **ConfigMgr_MPReplica**.

1. Add the following permissions to the **ConfigMgr_MPReplica** share:

    > [!NOTE]
    > If the SQL Server Agent uses an account other than the local system account, replace SYSTEM with that account name in the following list.

    - Share permissions:

      - SYSTEM: **Change**

      - ConfigMgr_MPReplicaAccess: **Read**

    - NTFS permissions:

      - SYSTEM: **Full Control**

      - ConfigMgr_MPReplicaAccess: **Read**, **Read & execute**, and **List folder contents**

1. Use **SQL Server Management Studio** to connect to the site database and run the following stored procedure as a query: `spCreateMPReplicaPublication`

    > [!NOTE]
    > If you're using a domain group instead of a local group, change this SQL statement to: `EXEC spCreateMPReplicaPublication N'<DomainName>\ConfigMgr_MPReplicaAccess'`<!-- MEMDocs#527 -->

When the stored procedure completes, the site database server is configured to publish the database replica.

### <a name="BKMK_DBReplica_ConfigSrv"></a> Step 2 - Configure the database replica server

Use the following procedure as an example of how to configure a database replica server. The specific steps might vary depending upon the version of Windows Server.

Do the following steps on the database replica server:

1. Set the SQL Server Agent to automatic startup.

1. Use **SQL Server Management Studio** to connect to the local server. Browse to the **Replication** folder, select **Local Subscriptions**, and then select **New Subscriptions**. This action starts the **New Subscription Wizard**.

    1. On the **Publication** page, select **Find SQL Server Publisher**. Enter the name of the site database server, and then select **Connect**.

    1. Select **ConfigMgr_MPReplica**, and then select **Next**.

    1. On the **Distribution Agent Location** page, select **Run each agent at its Subscriber (pull subscriptions)**, and then select **Next**.

    1. On the **Subscribers** page, do one of the following actions:

        - Select an existing database from the database replica server to use for the database replica, and then select **OK**.

        - Select **New database** to create a new database for the database replica. On the **New Database** page, specify a database name, and then select **OK**.

    1. Select **Next** to continue.

    1. On the **Distribution Agent Security** page, select the properties button **(...)** in the Subscriber Connection row of the dialog box. Then configure the security settings for the connection.

        > [!TIP]
        > The properties button, **(...)**, is in the fourth column of the display box.

      - Configure the account that runs the Distribution Agent process (*process account*):

        - If the SQL Server Agent runs as local system, select **Run under the SQL Server Agent service account (This is not a recommended security best practice.)**

        - If the SQL Server Agent runs by using a different account, select **Run under the following Windows account**, and then configure that account. You can specify a Windows account or a SQL Server account.

        > [!IMPORTANT]
        > Grant the account that runs the Distribution Agent permissions to the publisher as a pull subscription. For more information about configuring these permissions, see [Distribution agent security](/sql/relational-databases/replication/distribution-agent-security).

      - For **Connect to the Distributor**, select **By impersonating the process account**.

      - For **Connect to the Subscriber**, select **By impersonating the process account**.

        After you configure the connection security settings, select **OK** to save them, and then select **Next**.

    1. On the **Synchronization Schedule** page, select **Define schedule**, and then configure the **New Job Schedule**. Set the frequency to occur **Daily**, recur every **5 minute(s)**, and the duration to have **No end date**. Select **Next** to save the schedule, and then select **Next** again.

    1. On the **Wizard Actions** page, enable the option to **Create the subscriptions(s)**, and then select **Next**.

    1. Complete the wizard.

1. Immediately after completing the New Subscription Wizard, use **SQL Server Management Studio** to connect to the database replica server database. Run the following query to enable the TRUSTWORTHY database property: `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`

1. Review the synchronization status to validate that the subscription is successful:

    - On the subscriber computer:

      - In **SQL Server Management Studio**, connect to the database replica server, and expand **Replication**.

      - Expand **Local Subscriptions**, right-click the subscription to the site database publication, and then select **View Synchronization Status**.

    - On the publisher computer:

      - In **SQL Server Management Studio**, connect to the site database computer, right-click the **Replication** folder, and then select **Launch Replication Monitor**.

1. To enable common language runtime (CLR) integration for the database replica, use **SQL Server Management Studio** to connect to the database replica on the database replica server. Run the following stored procedure as a query: `exec sp_configure 'clr enabled', 1; RECONFIGURE WITH OVERRIDE`

1. For each management point that uses a database replica server, add that management points computer account to the local **Administrators** group on that database replica server.

    > [!TIP]
    > This step isn't necessary for a management point that runs on the database replica server.

The database replica is now ready for a management point to use.

### <a name="BKMK_DBReplica_ConfigMP"></a> Step 3 - Configure management points to use the database replica

You can configure a management point at a primary site to use a database replica when you install the management point role, or you can reconfigure an existing management point to use a database replica.

Use the following information to configure a management point to use a database replica:

- To configure a new management point:

    1. On the **Management Point Database** page of the wizard to install the management point, select **Use a database replica**.
    1. Specify the FQDN of the computer that hosts the database replica.
    1. For the **ConfigMgr site database name**, specify the database name of the database replica on that computer.

- To configure a previously installed management point:

    1. Open the properties page of the management point, and switch to the **Management Point Database** tab.
    1. Select **Use a database replica**, and then specify the FQDN of the computer that hosts the database replica.
    1. Next, for **ConfigMgr site database name**, specify the database name of the database replica on that computer.

For each management point that uses a database replica, manually add the computer account of the management point server to the **db_datareader** role for the database replica.

In addition to configuring the management point to use the database replica server, enable **Windows Authentication** in **IIS** on the management point:

1. Open **Internet Information Services (IIS) Manager**.

1. Select the website used by the management point, and open **Authentication**.

1. Set **Windows Authentication** to **Enabled**, and then close **Internet Information Services (IIS) Manager**.

###  <a name="BKMK_DBReplica_Cert"></a> Step 4 -Configure a self-signed certificate for the database replica server

Use the following procedures as an example of how to configure the self-signed certificate on the database replica server. The specific steps might vary depending upon the version of Windows Server.

#### Configure a self-signed certificate for the database replica server

1. On the database replica server, open a PowerShell command prompt with administrative privileges, and then run the following command: `Set-ExecutionPolicy Unrestricted`

1. Copy the following PowerShell script and save it as a file with the name **CreateMPReplicaCert.ps1**. Place a copy of this file in the root folder of the system partition of the database replica server.

    > [!IMPORTANT]
    > If you're configuring more than one database replica on a single SQL Server, for each subsequent replica you configure, use a modified version of this script for this procedure. For more information, see [Supplemental script for additional database replicas on a single SQL Server](#bkmk_supscript).

    ``` PowerShell
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the SQL Server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL Server needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL Server to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart SQL Server service  
    Restart-Service $SQLServiceName -Force  
    ```  

1. On the database replica server, run the following command that applies to the configuration of your SQL Server:

    - For a default instance of SQL Server: Enter the following command in the PowerShell session: `.\CreateMPReplicaCert.ps1`. When the script runs, it creates the self-signed certificate and configures SQL Server to use the certificate.

    - For a named instance of SQL Server: Use PowerShell to run the following command: `.\CreateMPReplicaCert.ps1 <SQL Server instance name>`

    After the script completes, verify that the SQL Server Agent is running. If not, restart the SQL Server Agent.

#### Configure remote management points to use the self-signed certificate of the database replica server

Do the following steps on the *database replica server* to export the server's self-signed certificate:

1. Go to the **Start** menu, select **Run**, and type `mmc.exe`. In the empty console, select **File**, and then select **Add/Remove Snap-in**.

1. In the **Add or Remove Snap-ins** dialog box, select **Certificates** from the list of **Available snap-ins**, and then select **Add**.

1. In the **Certificate snap-in** dialog box, select **Computer account**, and then select **Next**.

1. In the **Select Computer** dialog box, make sure that **Local computer: (the computer this console is running on)** is selected, and then select **Finish**.

1. In the **Add or Remove Snap-ins** dialog box, select **OK**.

1. In the console, expand **Certificates (Local Computer)**, expand **Personal**, and select **Certificates**.

1. Right-click the certificate with the friendly name of **ConfigMgr SQL Server Identification Certificate**, select **All Tasks**, and then select **Export**.

1. Complete the **Certificate Export Wizard** with the default options. Save the certificate with the **.cer** file name extension.


Do the following steps on the *management point* server to add the self-signed certificate for the database replica server to the Trusted People certificate store:

1. Repeat the preceding steps to open the **Certificate** snap-in MMC on the management point computer.

1. In the Certificates console, expand **Certificates (Local Computer)**, expand **Trusted People**, right-click **Certificates**, select **All Tasks**, and then select **Import**. This action starts the **Certificate Import Wizard**.

1. On the **File to Import** page, select the saved certificate, and then select **Next**.

1. On the **Certificate Store** page, select **Place all certificates in the following store**, with the **Certificate store** set to **Trusted People**, and then select **Next**.

1. Select **Finish** to close the wizard and complete the certificate configuration on the management point.

### <a name="BKMK_DBreplica_SSB"></a> Step 5 - Configure the SQL Server Service Broker for the database replica server

To support client notification with a database replica for a management point, configure communication between the site database server and the database replica server for the SQL Server Service Broker. Configure each database with information about the other database, and to exchange certificates between the two databases for secure communication.

> [!NOTE]
> Before you can use the following procedure, the database replica server must successfully complete the initial synchronization with the site database server.

The following procedure doesn't modify the Service Broker port that's configured in SQL Server for the site database server or the database replica server. This procedure configures each database to communicate with the other database by using the correct Service Broker port.

Use the following procedure to configure the Service Broker for the site database server and the database replica server:

1. Use **SQL Server Management Studio** to connect to the *replica server database*. Then run the following query to enable the Service Broker on the database replica server: `ALTER DATABASE <Replica Database Name> SET ENABLE_BROKER, HONOR_BROKER_PRIORITY ON WITH ROLLBACK IMMEDIATE`

1. On the *database replica server*, configure the Service Broker for client notification and export the Service Broker certificate. Run a SQL Server stored procedure that configures the Service Broker and exports the certificate as a single action. When you run the stored procedure, specify the FQDN of the database replica server, the name of the database replicas database, and specify a location for the export of the certificate file.

    Run the following query to configure the required details on the database replica server, and to export the certificate for the database replica server: `EXEC sp_BgbConfigSSBForReplicaDB '<Replica SQL Server FQDN>', '<Replica Database Name>', '<Certificate Backup File Path>'`

    > [!NOTE]
    > When the database replica server isn't on the default instance of SQL Server, also specify the instance name with the replica database name. In the example command, replace `<Replica Database Name>` with `<Instance name>\<Replica Database Name>`.

    After you export the certificate from the database replica server, place a copy of the certificate on the primary site database server.

1. Use **SQL Server Management Studio** to connect to the *primary site database*. After you connect to the primary sites database, run a query to import the certificate and specify the Service Broker port that's in use on the database replica server, the FQDN of the database replica server, and name of the database replicas database. This action configures the primary sites database to use the Service Broker to communicate to the database of the database replica server.

    Run the following query to import the certificate from the database replica server and specify the required details: `EXEC sp_BgbConfigSSBForRemoteService 'REPLICA', '<SQL Service Broker Port>', '<Certificate File Path>', '<Replica SQL Server FQDN>', '<Replica Database Name>'`

    > [!NOTE]
    > When the database replica server isn't on the default instance of SQL Server, also specify the instance name with the replica database name. In the example command, replace `<Replica Database Name>` with `<Instance name>\<Replica Database Name>`.

1. On the *site database server*, run the following command to export the certificate for the site database server: `EXEC sp_BgbCreateAndBackupSQLCert '<Certificate Backup File Path>'`

    After you export the certificate from the site database server, place a copy of the certificate on the database replica server.

1. Use **SQL Server Management Studio** to connect to the *replica server database*. After you connect to the replica server database, run a query to import the certificate and specify the site code of the primary site and the Service Broker port that's in use on the site database server. This action configures the database replica server to use the Service Broker to communicate to the database of the primary site.

    Run the following query to import the certificate from the site database server: `EXEC sp_BgbConfigSSBForRemoteService '<Site Code>', '<SQL Service Broker Port>', '<Certificate File Path>'`

A few minutes after you complete the configuration of the site database and the database replica database, the notification manager at the primary site sets up the Service Broker conversation for client notification from the primary site database to the database replica.

### <a name="bkmk_supscript"></a> Supplemental script for other database replicas on a single SQL Server

When you use the script from step 4 to configure a self-signed certificate for the database replica server on a SQL Server that already has a database replica you plan to continue using, use a modified version of the original script. The following modifications prevent the script from deleting an existing certificate on the server, and create subsequent certificates with unique friendly names. Edit the original script as follows:

- Comment out each line between the script entries `# Delete existing cert if one exists` and `# Create the new cert`. Add a pound sign (`#`) as the first character of each applicable line.

- For each subsequent database replica you use this script to configure, update the friendly name for the certificate. Edit the line `$enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"` and replace `ConfigMgr SQL Server Identification Certificate` with a new name. For example, `ConfigMgr SQL Server Identification Certificate1`.

## <a name="BKMK_DBReplicaOps"></a> Manage database replica configurations

When you use a database replica at a site, use the information in the following sections to supplement the process of uninstalling a database replica, uninstalling a site that uses a database replica, or moving the site database to a new installation of SQL Server. When delete publications, use the guidance for deleting transactional replication for the version of SQL Server that you use for the database replica. For more information, see [Delete a Publication](/sql/relational-databases/replication/publish/delete-a-publication).

> [!NOTE]
> After you restore a site database that was configured for database replicas, before you can use the database replicas, reconfigure each database replica and recreate both the publications and subscriptions.

### <a name="BKMK_UninstallDbReplica"></a> Uninstall a database replica

When you use a database replica for a management point, you might need to uninstall it and then reconfigure it for use. For example, remove database replicas before you update Configuration Manager to the latest version. After the site update completes, restore the database replica for use.

Use the following steps to uninstall a database replica.

1. In the **Administration** workspace of the Configuration Manager console, expand **Site Configuration**, then select **Servers and Site System Roles**. In the details pane, select the site system server that hosts the management point that uses the database replica you will uninstall.

1. In the **Site System Roles** pane, select the **Management point** role. In the ribbon, on the **Site Role** tab, select **Properties**.

1. Switch to the **Management Point Database** tab. Select **Use the site database** to configure the management point to use the site database instead of the database replica. Select **OK** to save the configuration.

1. Use **SQL Server Management Studio** to do the following tasks:

    - Delete the publication for the database replica from the site server database.

    - Delete the subscription for the database replica from the database replica server.

    - Delete the replica database from the database replica server.

    - Disable publishing and distribution on the site database server. To disable publishing and distribution, right-click the **Replication** folder and select **Disable Publishing and Distribution**.

After you delete the publication, subscription, the replica database, and disable publishing on the site database server, the database replica is uninstalled.

### <a name="BKMK_DBReplicaOps_Uninstall"></a> Uninstall a site server that publishes a database replica

Before you uninstall a site that publishes a database replica, use the following steps to clean up the publication and any subscriptions.

1. Use **SQL Server Management Studio** to delete the database replica publication from the site server database.

1. Use **SQL Server Management Studio** to delete the database replica subscription from each remote SQL Server that hosts a database replica for this site.

1. Uninstall the site.

### <a name="BKMK_DBReplicaOps_Move"></a> Move a site server database that publishes a database replica

When you move the site database to a new computer, use the following steps:

1. Use **SQL Server Management Studio** to delete the publication for the database replica from the site server database.

1. Use **SQL Server Management Studio** to delete the subscription for the database replica from each database replica server for this site.

1. Move the database to the new SQL Server computer. For more information, see [Modify the site database configuration](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig).

1. Recreate the publication for the database replica on the site database server. For more information, see [Step 1 - Configure the site database server to Publish the database replica](#BKMK_DBReplica_ConfigSiteDB).

1. Recreate the subscriptions for the database replica on each database replica server. For more information, see [Step 2 - Configuring the database replica server](#BKMK_DBReplica_ConfigSrv).
