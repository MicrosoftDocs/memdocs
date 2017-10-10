---
title: "Management point database replicas"
titleSuffix: "Configuration Manager"
description: "Use a database replica to reduce the CPU load placed on the site database server by management points."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
caps.latest.revision: 9
author: Brendunsms.author: brendunsmanager: angrobe

---
# Database replicas for management points for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
System Center Configuration Manager primary sites can use a database replica to reduce the CPU load placed on the site database  server by management points as they service requests from clients.  

-   When a management point uses a database replica, that management point requests data from the SQL Server computer that hosts the database replica instead of from the site database server.  

-   This can help reduce the CPU processing requirements on the site database server by offloading frequent processing tasks related to clients.  An example of frequent processing tasks for clients includes sites where there are a large numbers of clients that make frequent requests for client policy  


##  <a name="bkmk_Prepare"></a> Prepare to use database replicas  
**About database replicas for management points:**  

-   Replicas are a partial copy of the site database that is replicated to a separate instance of  SQL Server:  

    -   Primary sites support a dedicated database replica for each management point at the site (Secondary sites do not support database replicas)  

    -   A single database replica can be used by more than a one management point from the same site  

    -   A SQL server can host multiple database replicas for use by different management points so long as each runs in a separate instance of SQL Server  

-   Replicas synchronize a copy of the site database on a fixed schedule  from data that is published by the sites database server for this purpose.  

-   Management points can be configured to use a replica when you install the management point, or at a later time by reconfiguring the previously installed management point to use the database replica  

-   Regularly monitor the site database server and each database replica server to ensure that replication occurs between them, and that the performance of the database replica server is sufficient for the site and client performance that you require  

**Prerequisites for database replicas:**  

-   **SQL Server requirements:**  

    -   The SQL Server that hosts the database replica must meet the same requirements as the site database server. However, the replica server does not need to run the same version or edition of SQL Server as the site database server, as long as it runs a supported version and edition of SQL Server. For information see [Support for SQL Server versions for System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md)  

    -   The SQL Server Service on the computer that hosts the replica database must run as the **System** account.  

    -   Both the SQL Server that hosts the site database and that hosts a database replica must have **SQL Server replication** installed.  

    -   The site database must **publish** the database replica, and each remote database replica server must **subscribe** to the published data.  

    -   Both the SQL Server that hosts the  site database and that hosts a database replica must be configured to support a **Max Text Repl Size** of 2 GB. For an example of how to configure this for SQL Server 2012, see [Configure the max text repl size Server Configuration Option](http://go.microsoft.com/fwlink/p/?LinkId=273960).  

-   **Self-signed certificate:** To configure a database replica, you must create a self-signed certificate on the database replica server and make this certificate available to each management point that will use that database replica server.  

    -   The certificate is automatically available to a management point that is installed on the database replica server.  

    -   To make this certificate available to remote management points, you must export the certificate and then add it to the **Trusted People** certificate store on the remote management point.  

-   **Client notification:** To support client notification with a database replica for a management point, you must configure communication between the site database server and the database replica server for the **SQL Server Service Broker**. This requires you to:  

    -   Configure each database with information about the other database  

    -   Exchange certificates between the two databases for secure communication  

**Limitations when you use database replicas:**  

-   When your site is configured to publish database replicas, the following procedures should be used in place of normal guidance:  

    -   [Uninstall a site server that publishes a database replica](#BKMK_DBReplicaOps_Uninstall)  

    -   [Move a site server database that publishes a database replica](#BKMK_DBReplicaOps_Move)  

-   **Upgrades to System Center Configuration Manager**: Before you upgrade a site from System Center 2012 Configuration Manager to System Center Configuration Manager, you must disable database replicas for management points.  After your site upgrades, you can reconfigure the database replicas for management points.  

-   **Multiple replicas on a single SQL Server:**  If you configure  a database replica server to host multiple database replicas for management points (each replica must be on a separate instance) you must use a modified configuration script (from Step 4 of the following section)  to prevent overwriting the self-signed certificate in use by previously configured database replicas on that server.  

##  <a name="BKMK_DBReplica_Config"></a> Configure database replicas  
To use configure a database replica, the following steps are required:  

-   [Step 1 - Configure the site database server to Publish the database replica](#BKMK_DBReplica_ConfigSiteDB)  

-   [Step 2 - Configuring the database replica server](#BKMK_DBReplica_ConfigSrv)  

-   [Step 3 - Configure management points to use the database replica](#BKMK_DBReplica_ConfigMP)  

-   [Step 4 -Configure a self-signed certificate for the database replica server](#BKMK_DBReplica_Cert)  

-   [Step 5 - Configure the SQL Server Service Broker for the database replica server](#BKMK_DBreplica_SSB)  

###  <a name="BKMK_DBReplica_ConfigSiteDB"></a> Step 1 - Configure the site database server to Publish the database replica  
 Use the following procedure as an example of how to configure the site database server on a Windows Server 2008 R2 computer to publish the database replica. If you have a different operating system version, refer to your operating system documentation and adjust the steps in this procedure as necessary.  

##### To configure the site database server  

1.  On the site database server, set the SQL Server Agent to automatically start.  

2.  On the site database server, create a local user group with the name **ConfigMgr_MPReplicaAccess**. You must add the computer account for each database replica server that you use at this site to this group to enable those database replica servers to synchronize with the published database replica.  

3.  On the site database server, configure a file share with the name **ConfigMgr_MPReplica**.  

4.  Add the following permissions to the **ConfigMgr_MPReplica** share:  

    > [!NOTE]  
    >  If the SQL Server Agent uses an account other than the local system account, replace SYSTEM with that account name in the following list.  

    -   **Share Permissions**:  

        -   SYSTEM: **Write**  

        -   ConfigMgr_MPReplicaAccess: **Read**  

    -   **NTFS Permissions**:  

        -   SYSTEM: **Full Control**  

        -   ConfigMgr_MPReplicaAccess: **Read**, **Read & execute**, **List folder contents**  

5.  Use **SQL Server Management Studio** to connect to the site database and run the following stored procedure as a query: **spCreateMPReplicaPublication**  

When the stored procedure completes, the site database server is configured to publish the database replica.  

###  <a name="BKMK_DBReplica_ConfigSrv"></a> Step 2 - Configuring the database replica server  
The database replica server is a computer that runs SQL Server and that hosts a replica of the site database for management points to use. On a fixed schedule, the database replica server synchronizes its copy of the database with the database replica that is published by the site database server.  

The database replica server must meet the same requirements as the site database server. However, the database replica server can run a different edition or version of SQL Server than the site database server uses. For information about the supported versions of SQL Server, see the [Support for SQL Server versions for System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md) topic.  

> [!IMPORTANT]  
>  The SQL Server Service on the computer that hosts the replica database must run as the System account.  

Use the following procedure as an example of how to configure a database replica server on a Windows Server 2008 R2 computer. If you have a different operating system version, refer to your operating system documentation and adjust the steps in this procedure as necessary.  

##### To configure the database replica server  

1.  On the database replica server, set the SQL Server Agent to automatic startup.  

2.  On the database replica server, use **SQL Server Management Studio** to connect to the local server, browse to the **Replication** folder, click Local Subscriptions, and select **New Subscriptions** to start the **New Subscription Wizard**:  

    1.  On the **Publication** page, in the **Publisher** list box, select **Find SQL Server Publisher**, enter the name of the sites database server, and then click **Connect**.  

    2.  Select **ConfigMgr_MPReplica**, and then click **Next**.  

    3.  On the **Distribution Agent Location** page, select **Run each agent at its Subscriber (pull subscriptions)**, and click **Next**.  

    4.  On the **Subscribers** page do one of the following:  

        -   Select an existing database from the database replica server to use for the database replica, and then click **OK**.  

        -   Select **New database** to create a new database for the database replica. On the **New Database** page, specify a database name, and then click **OK**.  

    5.  Click **Next** to continue.  

    6.  On the **Distribution Agent Security** page, click the properties button **(....)** in the Subscriber Connection row of the dialog box, and then configure the security settings for the connection.  

        > [!TIP]  
        >  The properties button, **(....)**, is in the fourth column of the display box.  

        **Security settings:**  

        -   Configure the account that runs the Distribution Agent process (the process account):  

            -   If the SQL Server Agent runs as local system, select **Run under the SQL Server Agent service account (This is not a recommended security best practice.)**  

            -   If the SQL Server Agent runs by using a different account, select **Run under the following Windows account**, and then configure that account. You can specify a Windows account or a SQL Server account.  

            > [!IMPORTANT]  
            >  You must grant the account that runs the Distribution Agent permissions to the publisher as a pull subscription. For information about configuring these permissions, see [Distribution Agent Security](http://go.microsoft.com/fwlink/p/?LinkId=238463) in the SQL Server TechNet Library.  

        -   For **Connect to the Distributor**, select **By impersonating the process account**.  

        -   For **Connect to the Subscriber**, select **By impersonating the process account**.  

         After you configure the connection security settings, click **OK** to save them, and then click **Next**.  

    7.  On the **Synchronization Schedule** page, in the **Agent Schedule** list box, select **Define schedule**, and then configure the **New Job Schedule**. Set the frequency to occur **Daily**, recur every **5 minute(s)**, and the duration to have **No end date**. Click **Next** to save the schedule, and then click **Next** again.  

    8.  On the **Wizard Actions** page, select the check box for **Create the subscriptions(s)**, and then click **Next**.  

    9. On the **Complete the Wizard** page, click **Finish**, and then click **Close** to complete the Wizard.  

3.  Immediately after completing the New Subscription Wizard, use **SQL Server Management Studio** to connect to the database replica server database and run the following query to enable the TRUSTWORTHY database property:  `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4.  Review the synchronization status to validate that the subscription is successful:  

    -   On the subscriber computer:  

        -   In **SQL Server Management Studio**, connect to the database replica server and expand **Replication**.  

        -   Expand **Local Subscriptions**, right-click the subscription to the site database publication, and then select **View Synchronization Status**.  

    -   On the publisher computer:  

        -   In **SQL Server Management Studio**, connect to the site database computer, right-click the **Replication** folder, and then select **Launch Replication Monitor**.  

5.  To enable common language runtime (CLR) integration for the database replica, use **SQL Server Management Studio** to connect to the database replica on the database replica server, and run the following stored procedure as a query: **exec sp_configure 'clr enabled', 1; RECONFIGURE WITH OVERRIDE**  

6.  For each management point that uses a database replica server, add that management points computer account to the local **Administrators** group on that database replica server.  

    > [!TIP]  
    >  This step is not necessary for a management point that runs on the database replica server.  

 The database replica is now ready for a management point to use.  

###  <a name="BKMK_DBReplica_ConfigMP"></a> Step 3 - Configure management points to use the database replica  
 You can configure a management point at a primary site to use a database replica when you install the management point role, or you can reconfigure an existing management point to use a database replica.  

 Use the following information to configure a management point to use a database replica:  

-   **To configure a new management point:** On the **Management Point Database** page of the wizard that you use to install the management point, select **Use a database replica**, and specify the FQDN of the computer that hosts the database replica. Next, for **ConfigMgr site database name**, specify the database name of the database replica on that computer.  

-   **To configure a previously installed management point**: Open the properties page of the management point, select the **Management Point Database** tab, select **Use a database replica**, and then specify the FQDN of the computer that hosts the database replica. Next, for **ConfigMgr site database name**, specify the database name of the database replica on that computer.  

-   **For each management point that uses a database replica**, you must manually add the computer account of the management point server to the **db_datareader** role for the database replica.  

In addition to configuring the management point to use the database replica server, you must enable **Windows Authentication** in **IIS** on the management point:  

1.  Open **Internet Information Services (IIS) Manager**.  

2.  Select the website used by the management point, and open **Authentication**.  

3.  Set **Windows Authentication** to **Enabled**, and then close **Internet Information Services (IIS) Manager**.  

###  <a name="BKMK_DBReplica_Cert"></a> Step 4 -Configure a self-signed certificate for the database replica server  
 You must create a self-signed certificate on the database replica server and make this certificate available to each management point that will use that database replica server.  

 The certificate is automatically available to a management point that is installed on the database replica server. However, to make this certificate available to remote management points, you must export the certificate and then add it to the Trusted People certificate store on the remote management point.  

 Use the following procedures as an example of how to configure the self-signed certificate on the database replica server for a Windows Server 2008 R2 computer. If you have a different operating system version, refer to your operating system documentation and adjust the steps in these procedures as necessary.  

##### To configure a self-signed certificate for the database replica server  

1.  On the database replica server, open a PowerShell command prompt with administrative privileges, and then run the following command: **set-executionpolicy UnRestricted**  

2.  Copy the following PowerShell script and save it as a file with the name **CreateMPReplicaCert.ps1**. Place a copy of this file in the root folder of the system partition of the database replica server.  

    > [!IMPORTANT]  
    >  If you are configuring more than one  database replica on a single SQL Server, for each subsequent replica you configure you must use a modified version of this script for this procedure. See  [Supplemental script for additional database replicas on a single SQL Server](#bkmk_supscript)  

    ```  
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
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

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  On the database replica server, run the following command that applies to the configuration of your SQL Server:  

    -   For a default instance of SQL Server: Right-click the file **CreateMPReplicaCert.ps1** and select **Run with PowerShell**. When the script runs, it creates the self-signed certificate and configures SQL Server to use the certificate.  

    -   For a named instance of SQL Server: Use PowerShell to run the command **%path%\CreateMPReplicaCert.ps1 xxxxxx** where **xxxxxx** is the name of the SQL Server instance.  

    -   After the script completes, verify that the SQL Server Agent is running. If not, restart the SQL Server Agent.  

##### To configure remote management points to use the self-signed certificate of the database replica server  

1.  Perform the following steps on the database replica server to export the server's self-signed certificate:  

    1.  Click **Start**, click **Run**, and type **mmc.exe**. In the empty console, click **File**, and then click **Add/Remove Snap-in**.  

    2.  In the **Add or Remove Snap-ins** dialog box, select **Certificates** from the list of **Available snap-ins**, and then click **Add**.  

    3.  In the **Certificate snap-in** dialog box, select **Computer account**, and then click **Next**.  

    4.  In the **Select Computer** dialog box, ensure that **Local computer: (the computer this console is running on)** is selected, and then click **Finish**.  

    5.  In the **Add or Remove Snap-ins** dialog box, click **OK**.  

    6.  In the console, expand **Certificates (Local Computer)**, expand **Personal**, and select **Certificates**.  

    7.  Right-click the certificate with the friendly name of **ConfigMgr SQL Server Identification Certificate**, click **All Tasks**, and then select **Export**.  

    8.  Complete the **Certificate Export Wizard** by using the default options and save the certificate with the **.cer** file name extension.  

2.  Perform the following steps on the management point computer to add the self-signed certificate for the database replica server to the Trusted People certificate store on the management point:  

    1.  Repeat the preceding steps 1.a through 1.e to configure the **Certificate** snap-in MMC on the management point computer.  

    2.  In the console, expand **Certificates (Local Computer)**, expand **Trusted People**, right-click **Certificates**, select **All Tasks**, and then select **Import** to start the **Certificate Import Wizard**.  

    3.  On the **File to Import** page, select the certificate saved in step 1.h, and then click **Next**.  

    4.  On the **Certificate Store** page, select **Place all certificates in the following store**, with the **Certificate store** set to **Trusted People**, and then click **Next**.  

    5.  Click **Finish** to close the wizard and complete the certificate configuration on the management point.  

###  <a name="BKMK_DBreplica_SSB"></a> Step 5 - Configure the SQL Server Service Broker for the database replica server  
To support client notification with a database replica for a management point, you must configure communication between the site database server and the database replica server for the SQL Server Service Broker. This requires you to configure each database with information about the other database, and to exchange certificates between the two databases for secure communication.  

> [!NOTE]  
>  Before you can use the following procedure, the database replica server must successfully complete the initial synchronization with the site database server.  

 The following procedure does not modify the Service Broker port that is configured in SQL Server for the site database server or the database replica server. Instead, this procedure configures each database to communicate with the other database by using the correct Service Broker port.  

 Use the following procedure to configure the Service Broker for the site database server and the database replica server.  

##### To configure the service broker for a database replica  

1.  Use **SQL Server Management Studio** to connect to database replica server database, and then run the following query to enable the Service Broker on the database replica server: **ALTER DATABASE &lt;Replica Database Name\> SET ENABLE_BROKER, HONOR_BROKER_PRIORITY ON WITH ROLLBACK IMMEDIATE**  

2.  Next, on the database replica server, configure the Service Broker for client notification and export the Service Broker certificate. To do this, run a SQL Server stored procedure that configures the Service Broker and exports the certificate as a single action. When you run the stored procedure, you must specify the FQDN of the database replica server, the name of the database replicas database, and specify a location for the export of the certificate file.  

     Run the following query to configure the required details on the database replica server, and to export the certificate for the database replica server: **EXEC sp_BgbConfigSSBForReplicaDB '&lt;Replica SQL Server FQDN\>', '&lt;Replica Database Name\>', '&lt;Certificate Backup File Path\>'**  

    > [!NOTE]  
    >  When the database replica server is not on the default instance of SQL Server, for this step you must specify the instance name in addition to the replica database name. To do so, replace **&lt;Replica Database Name\>** with **&lt;Instance name\\Replica Database Name\>**.  

     After you export the certificate from the database replica server, place a copy of the certificate on the primary sites database server.  

3.  Use **SQL Server Management Studio** to connect to the primary site database. After you connect to the primary sites database, run a query to import the certificate and specify the Service Broker port that is in use on the database replica server, the FQDN of the database replica server, and name of the database replicas database. This configures the primary sites database to use the Service Broker to communicate to the database of the database replica server.  

     Run the following query to import the certificate from the database replica server and specify the required details: **EXEC sp_BgbConfigSSBForRemoteService 'REPLICA', '&lt;SQL Service Broker Port\>', '&lt;Certificate File Path\>', '&lt;Replica SQL Server FQDN\>', '&lt;Replica Database Name\>'**  

    > [!NOTE]  
    >  When the database replica server is not on the default instance of SQL Server, for this step you must specify the instance name in addition to the replica database name. To do so, replace **&lt;Replica Database Name\>** with **\Instance name\\Replica Database Name\>**.  

4.  Next, on the site database server, run the following command to export the certificate for the site database server: **EXEC sp_BgbCreateAndBackupSQLCert '&lt;Certificate Backup File Path\>'**  

     After you export the certificate from the site database server, place a copy of the certificate on the database replica server.  

5.  Use **SQL Server Management Studio** to connect to the database replica server database. After you connect to the database replica server database, run a query to import the certificate and specify the site code of the primary site and the Service Broker port that is in use on the site database server. This configures the database replica server to use the Service Broker to communicate to the database of the primary site.  

     Run the following query to import the certificate from the site database server: **EXEC sp_BgbConfigSSBForRemoteService '&lt;Site Code\>', '&lt;SQL Service Broker Port\>', '&lt;Certificate File Path\>'**  

 A few minutes after you complete the configuration of the site database and the database replica database, the notification manager at the primary site sets up the Service Broker conversation for client notification from the primary site database to the database replica.  

###  <a name="bkmk_supscript"></a> Supplemental script for additional database replicas on a single SQL Server  
 When you use the script from step 4 to  configure a self-signed certificate for the database replica server on a SQL Server that already has a database replica you plan to continue using, you must use a modified version of the  original script. The following modifications prevent the script from deleting an existing certificate on the server, and create subsequent certificates with unique Friendly names.  Edit the original script as follows:  

-   Comment out (prevent from running) each line between the script entries **# Delete existing cert if one exists** and **# Create the new cert**. To do so, add a  **#**  as the first character of  each  applicable line.  

-   For each subsequent  database replica you use this script to configure, update the Friendly name for the certificate.  To do so, edit the line **$enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"** and replace **ConfigMgr SQL Server Identification Certificate** with a new name, like  **ConfigMgr SQL Server Identification Certificate1**.  

##  <a name="BKMK_DBReplicaOps"></a> Manage database replica configurations  
 When you use a database replica at a site, use the information in the following sections to supplement the process of uninstalling a database replica, uninstalling a site that uses a database replica, or moving the site database to a new installation of SQL Server. When you use information in the following sections to delete publications, use the guidance for deleting transactional replication for the version of SQL Server that you use for the database replica. For example, if you use SQL Server 2008 R2, see [How to: Delete a Publication (Replication Transact-SQL Programming)](http://go.microsoft.com/fwlink/p/?LinkId=273934).  

> [!NOTE]  
>  After you restore a site database that was configured for database replicas, before you can use the database replicas you must reconfigure each database replica, recreating both the publications and subscriptions.  

###  <a name="BKMK_UninstallDbReplica"></a> Uninstall a database replica  
 When you use a database replica for a management point, you might need to uninstall the database replica for a period of time, and then reconfigure it for use. For example, you must remove database replicas before you upgrade a Configuration Manager site to a new service pack. After the site upgrade completes, you can restore the database replica for use.  

 Use the following steps to uninstall a database replica.  

1.  In the **Administration** workspace of the Configuration Manager console, expand **Site Configuration**, then select **Servers and Site System Roles**, and then in the details pane select the site system server that hosts the management point that uses the database replica you will uninstall.  

2.  In the **Site System Roles** pane, right click **Management point** and select **Properties**.  

3.  On the **Management Point Database** tab, select **Use the site database** to configure the management point to use the site database instead of the database replica. Then, click **OK** to save the configuration.  

4.  Next, Use **SQL Server Management Studio** to perform the following tasks:  

    -   Delete the publication for the database replica from the site server database.  

    -   Delete the subscription for the database replica from the database replica server.  

    -   Delete the replica database from the database replica server.  

    -   Disable publishing and distribution on the site database server. To disable publishing and distribution, right-click the Replication folder and then click **Disable Publishing and Distribution**.  

5.  After you delete the publication, subscription, the replica database, and disable publishing on the site database server, the database replica is uninstalled.  

###  <a name="BKMK_DBReplicaOps_Uninstall"></a> Uninstall a site server that publishes a database replica  
 Before you uninstall a site that publishes a database replica, use the following steps to clean up the publication and any subscriptions.  

1.  Use **SQL Server Management Studio** to delete the database replica publication from the site server database.  

2.  Use **SQL Server Management Studio** to delete the database replica subscription from each remote SQL Server that hosts a database replica for this site.  

3.  Uninstall the site.  

###  <a name="BKMK_DBReplicaOps_Move"></a> Move a site server database that publishes a database replica  
 When you move the site database to a new computer, use the following steps:  

1.  Use **SQL Server Management Studio** to delete the publication for the database replica from the site server database.  

2.  Use **SQL Server Management Studio** to delete the subscription for the database replica from each database replica server for this site.  

3.  Move the database to the new SQL Server computer. For more information, see the [Modify the site database configuration](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) section in the [Modify your System Center Configuration Manager infrastructure](../../../../core/servers/manage/modify-your-infrastructure.md) topic.  

4.  Recreate the publication for the database replica on the site database server. For more information, see [Step 1 - Configure the site database server to Publish the database replica](#BKMK_DBReplica_ConfigSiteDB) in this topic.  

5.  Recreate the subscriptions for the database replica on each database replica server. For more information, see [Step 2 - Configuring the database replica server](#BKMK_DBReplica_ConfigSrv) in this topic.  
