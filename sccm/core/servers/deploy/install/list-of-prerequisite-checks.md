---
title: "Prerequisite checks"
description: "Review the available prerequisite checks for System Center Configuration Manager. Includes checks for security rights."
ms.custom: na
ms.date: 4/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# List of prerequisite checks for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The following sections detail the available prerequisite checks.

For information about using Prerequisite Checker, see [Prerequisite Checker](prerequisite-checker.md).  

##  <a name="BKMK_Security"></a> Prerequisite checks for security rights  
The following table lists checks that Prerequisite Checker performs for security rights.

|Check performed|Explanation|Severity|Site applicability|
|---|---|---|---|
|**Administrator rights on central administration site**|Verifies the user account that runs Configuration Manager Setup has **Administrator** rights on the central administration site computer. |Error|Primary site|
|**Administrative rights on expand primary site**|Verifies that the user account that runs Setup has **Administrator** rights on the standalone primary site that will be expanded.|Error|Central administration site|
|**Administrative rights on site system**|Verifies that the user account that runs Configuration Manager Setup has **Administrator** rights on the site server computer. |Error|Central administration site, <br>Primary site, <br>Secondary site|
|**CAS Machine administrative rights on expand primary site**|Verifies that the computer account of the central administration site has **Administrator** rights on the standalone primary site that will be expanded.|Error|Central administration site|
|**Connection to SQL Server on central administration site**|Verifies that the user account that runs Configuration Manager Setup on the primary site to join an existing hierarchy has the **sysadmin** role on the SQL Server instance for the central administration site.|Error|Primary site|
|**Site server computer account administrative rights**|Verifies that the site server computer account has **Administrator** rights on the SQL server and management point computers.|Error|Primary site, <br>SQL Server|
|**Site System to SQL Server Communication**| Verifies that a valid Service Principal Name (SPN) is registered in Active Directory Domain Services for the account configured to run the SQL Server service for the SQL Server instance that hosts the Configuration Manager site database. A valid SPN must be registered in Active Directory Domain Services to support Kerberos authentication.|Warning|Secondary site, <br>Management point|
|**SQL Server security mode**|Verifies that SQL Server is configured for Windows authentication security.|Warning|SQL Server|
|**SQL Server sysadmin rights**|Verifies that the user account that runs Configuration Manager Setup has the **sysadmin** role on the SQL Server instance selected for site database installation. This check also fails when Setup is unable to access the instance for the SQL Server to verify permissions.|Error|SQL Server|
|**SQL Server sysadmin rights for reference site**|Verifies that the user account that runs Configuration Manager Setup has the **sysadmin** role on the SQL Server role instance selected as the reference site database. SQL Server **sysadmin** role permissions are required to modify the site database.|Error|SQL Server|

##  <a name="BKMK_Dependencies"></a> Prerequisite checks for Configuration Manager dependencies
The following table lists checks that Prerequisite Checker performs for Configuration Manager dependencies.

|Check performed|Explanation|Severity|Site applicability|
|---|---|---|---|
|**Active migration mappings on the target primary site**|Verifies that there are no active migration mappings to primary sites.|Error|Central administration site|
|**Active Replica MP**|Checks for an active management point replica.|Error|Primary site|
|**Administrative rights on distribution point**|Verifies that the user account running Setup has **Administrator** rights on the distribution point computer.|Warning|Distribution point|
|**Administrative rights on management point**|Verifies that the computer account of the site server has **Administrator** rights on the management point and distribution point computer.|Warning|Management point|
|**Administrative share (Site system)**|Verifies that the required administrative shares are present on the site system computer.|Warning|Management point|
|**Application Compatibility**|Verifies that current applications are compliant with the application schema.|Warning|Central administration site, <br>Primary site|
|**BITS enabled**|Verifies that Background Intelligent Transfer Service (BITS) is installed on the management point site system computer. When this check fails, BITS is not installed, the Internet Information Services (IIS) 6.0 Windows Management Instrumentation (WMI) compatibility component for IIS 7.0 is not installed on the computer or on the remote IIS host, or Setup was unable to verify remote IIS settings because IIS common components were not installed on the site server computer.|Error|Management point|
|**BITS installed**|Verifies that BITS is installed in IIS.|Warning|Management point|
|**Case-insensitive collation on SQL Server**|Verifies that the SQL Server installation uses a case-insensitive collation, such as SQL_Latin1_General_CP1_CI_AS.|Error|SQL Server|
|**Check existing stand-alone primary site for version and sitecode**|Verifies that the primary site you plan to expand is a standalone primary site, and that it has the same version of Configuration Manager, but a different site code than the central administration site to be installed.|Error|Central administration site, <br>Primary site|
|**Check for incompatible collection references**|During an upgrade, this check verifies that collections reference only other collections of the same type.|Error|Central administration site|  
|**Client version on management point computer**|Verifies that you are installing the management point on a computer that does not have a different version of the Configuration Manager client installed.|Error|Management point|
|**Configuration for SQL Server memory usage**|Checks whether SQL Server is configured for unlimited memory use. You should configure SQL Server memory to have a maximum limit.|Warning|SQL Server|
|**Dedicated SQL Server instance**|Checks whether a dedicated instance of the SQL server is configured to host the Configuration Manager site database. If another site uses the instance, you must select a different instance for the new site to use. Alternatively, you can uninstall the other site or move its database to a different instance for the SQL server.|Error|Central administration site, <br>Primary site, <br>Secondary site|
|**Existing Configuration Manager server components on server**|Verifies that a site server or site system role is not already installed on the computer selected for site installation.|Error|Central administration site, <br>Primary site, <br>Secondary site|
|**Firewall exception for SQL Server**|Checks whether the Windows Firewall is disabled or whether a relevant Windows Firewall exception exists for SQL Server. You must allow Sqlservr.exe or the required TCP ports to be accessed remotely. By default, SQL Server listens on TCP port 1433, and the SQL Server Service Broker (SSB) uses TCP port 4022.|Error|Central administration site, <br>Primary site, <br>Secondary site, <br>Management point|
|**Firewall exception for SQL Server (stand-alone primary site)**|Checks whether the Windows Firewall is disabled or whether a relevant Windows Firewall exception exists for SQL Server. You must allow Sqlservr.exe or the required TCP ports to be accessed remotely. By default, SQL Server listens on TCP port 1433, and the SSB uses TCP port 4022.|Warning|Primary site (standalone only)|
|**Firewall exception for SQL Server for management point**|Checks whether the Windows Firewall is disabled or whether a relevant Windows Firewall exception exists for SQL Server.|Warning|Management point|
|**IIS HTTPS Configuration**|Verifies IIS website bindings for the HTTPS communication protocol. When you install site roles that require HTTPS, you must configure IIS site bindings on the specified server with a valid public key infrastructure (PKI) certificate.|Warning|Management point, <br>Distribution point|
|**IIS service running**|Verifies IIS is installed and running on the computer to install the management point or distribution point.|Error|Management point, <br> Distribution point|
|**Match Collation of expand primary site**|Verifies that the site database for the standalone primary site that you will expand has same collation as the site database at the central administration site.|Error|Central administration site|
|**Microsoft Remote Differential Compression (RDC) library registered**|Verifies that the RDC library is registered on the Configuration Manager site server.|Error|Central administration site, <br>Primary site, <br>Secondary site|
|**Microsoft Windows Installer**|Verifies the Windows Installer version. When this check fails, Setup was not able to verify the version, or the installed version does not meet the minimum requirements of Windows Installer 4.5.|Error|Central administration site, <br>Primary site, <br>Secondary site|
|**Microsoft XML Core Services 6.0 (MSXML60)**|Verifies that MSXML 6.0 or a later version is installed on the computer.|Warning|Central administration site, <br>Primary site, <br>Secondary site, <br>Configuration Manager console, <br>Management point, <br>Distribution point|
|**Minimum .NET Framework version for Configuration Manager console**|Checks whether Microsoft .NET Framework 4.0 is installed on the Configuration Manager console computer. You can download .NET Framework 4.0 from [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=189149).|Error|Configuration Manager console|
|**Minimum .NET Framework version for Configuration Manager site server**|Checks whether .NET Framework 3.5 is installed on the Configuration Manager site server. For Windows Server 2008, you can download the Microsoft .NET Framework 3.5 from [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=185604). For Windows Server 2008 R2, you can enable the .NET Framework 3.5 as a feature within Server Manager.|Error|Central administration site, <br>Primary site, <br>Secondary site|
|**Minimum .NET Framework version for SQL Server Express edition installation for Configuration Manager secondary site**|Verifies that .NET Framework 4.0 is installed on Configuration Manager secondary site computers for installing SQL Server Express.|Error|Secondary site|
|**Parent/child database collation**|Verifies that the collation of the site database matches the collation of the parent site's database. All sites in a hierarchy must use the same database collation.|Error|Primary site, <br>Secondary site|
|**PowerShell 2.0 on site server**|Verifies that Windows PowerShell 2.0 or a later version is installed on the site server for the Configuration Manager Exchange Connector. For more information about PowerShell 2.0, see [Article 968930](http://go.microsoft.com/fwlink/p/?LinkId=226450) in the Microsoft Knowledge Base.|Warning|Primary site|
|**Primary FQDN**|Using a fully qualified domain name (FQDN), verifies that the NetBIOS name of the computer matches the local hostname (first label of the FQDN) of the computer.|Error|Central administration site, <br>Primary site, <br>Secondary site, <br>SQL Server|
|**Remote Connection to WMI on Secondary Site**|Checks whether Setup is able to establish a remote connection to WMI on the secondary site server.|Warning|Secondary site|
|**Required SQL Server Collation**|Verifies that the instance for SQL Server and the Configuration Manager site database, if installed, is configured to use the SQL_Latin1_General_CP1_CI_AS collation, unless you are using a Chinese operating system and require GB18030 support.<br><br>For information about changing your SQL Server instance and database collations, see [Setting and changing collations](http://go.microsoft.com/fwlink/p/?LinkID=234541) in the SQL Server 2008 R2 Books Online.  For information about enabling GB18030 support, see [International support in System Center Configuration Manager](../../../../core/plan-design/hierarchy/international-support.md).|Error|Central administration site, <br>Primary site, <br>Secondary site|
|**Setup Source Folder**|Verifies that the computer account for the secondary site has **Read** NTFS file system permissions and **Read** share permissions to the Setup source folder and share.<br><br>**NOTE**: The secondary site computer account must be an **Administrator** user on the computer if you use administrative shares (for example, C$ and D$).|Error|Secondary site|
|**Setup Source Version**|Verifies that the Configuration Manager version in the source folder that you specified for the secondary site installation matches the Configuration Manager version of the primary site.|Error|Secondary site|
|**Site code in use**|Checks that the site code that you specified is not already in use in the Configuration Manager hierarchy. You must specify a unique site code for this site.|Error|Primary site|
|**SMS Provider machine has same domain as site server**|Checks whether a computer that runs an instance of the SMS Provider has the same domain as the site server.|Error|SMS Provider|
|**SQL Server Edition**|Checks that the edition of SQL Server at the site is not SQL Server Express.|Error|SQL Server|
|**SQL Server Express on Secondary Site**|Checks that SQL Server Express can successfully install on the site server computer for a secondary site.|Error|Secondary site|
|**SQL Server on the Secondary Site Computer**|Checks that SQL Server is installed on the secondary site computer. You cannot install SQL Server on a remote site system.<br><br>**WARNING**: This check applies only when you select to have Setup use an existing instance of SQL Server.|Error|Secondary site|
|**SQL Server process memory allocation**|Verifies that SQL Server reserves a minimum of 8 GB of memory for the central administration site and primary site, and a minimum of 4 GB of memory for the secondary site. For more information about how to set a fixed amount of memory by using SQL Server Management Studio, see [How to set a fixed amount of memory (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).<br><br>**NOTE**: This check is not applicable to SQL Server Express on a secondary site, which is limited to 1 GB of reserved memory.|Warning|SQL Server|
|**SQL Server service running account**|Verifies that the logon account for the SQL Server service is not a local user account or LOCAL SERVICE. You must configure the SQL Server service to use a valid domain account, NETWORK SERVICE, or LOCAL SYSTEM.|Error|Central administration site, <br>Primary site, <br>Secondary site|
|**SQL Server TCP Port**|Checks that TCP is enabled for the SQL Server instance and is set to use a static port.|Error|SQL Server|
|**SQL Server version**|Verifies that a supported version of SQL Server is installed on the specified site database server. For more information, see [Support for SQL Server versions for System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).|Error|SQL Server|
|**Unsupported site system operating system version for upgrade**|During an upgrade, this rule checks whether site system roles, other than distribution points, are installed on computers that run Windows Server 2008 or earlier versions.<br><br>**NOTE**: Because this check cannot resolve the status of site system roles that are installed in Azure or for the cloud storage used by Microsoft Intune, when you integrate Intune with Configuration Manager, you can ignore warnings for these roles as false positives.|Warning|Primary site, <br>Secondary site|
|**Unsupported site system role 'Asset Intelligence synchronization point' on the expanded primary site**|Checks that the Asset Intelligence sync point site system role is not installed on the standalone primary site that you are expanding.|Error|Central administration site|
|**Unsupported site system role 'Endpoint Protection point' on the expanded primary site**|Checks that the Endpoint Protection point site system role is not installed on the standalone primary site that you are expanding.|Error|Central administration site|
|**Unsupported site system role 'Microsoft Intune Connector' on the expanded primary site**|Checks that the Microsoft Intune Connector site system role is not installed on the standalone primary site that you are expanding.|Error|Central administration site|
|**User State Migration Tool (USMT) installed**|Checks whether the User State Migration Tool (USMT) component of Windows Assessment and Deployment Kit (ADK) for Windows 8.1 is installed.|Error|Central administration site, <br>Primary site (standalone only)|  
|**Validate FQDN of SQL Server Computer**|Checks that the FQDN that you specified for the SQL Server computer is valid.|Error|SQL Server|
|**Verify Central Administration Site Version**|Checks that the central administration site has the same version of Configuration Manager.|Error|Primary site|
|**Verify site server permissions to publish to Active Directory**|Verifies that the computer account for the site server has **Full Control** permissions to the **System Management** container in the Active Directory domain. For more information about your options to configure required permissions, see [Prepare Active Directory for site publishing](../../../../core/plan-design/network/extend-the-active-directory-schema.md).<br><br>**NOTE**: You can ignore this warning if you have manually verified the permissions.|Warning|Central administration site, <br>Primary site, <br>Secondary site|
|**Windows Deployment Tools installed**|Checks whether the Windows Deployment Tools component of Windows ADK for Windows 10 is installed.|Error|SMS Provider|
|**Windows Failover Cluster**|Checks that computers that have a management point or distribution point are not part of a Windows Cluster.|Error|Management point<br>Distribution point|
|**Windows Preinstallation Environment installed**|Checks whether the Windows Preinstallation Environment component of the Windows ADK for Windows 10 is installed.|Error|SMS Provider|
|**Windows Remote Management (WinRM) v1.1**|Verifies that WinRM 1.1 is installed on the primary site server or the Configuration Manager console computer to run the out-of-band management console. For more information about how to download WinRM 1.1, see [Article 936059](https://support.microsoft.com/en-us/kb/936059) in the Microsoft Knowledge Base.|Warning|Primary site, <br>Configuration Manager console|
|**WSUS on site server**|Verifies that Windows Server Update Services (WSUS) 3.0 Service Pack 2 (SP2) is installed on the site server. When you use a software update point on a computer that is not the site server, you must install the WSUS Administration Console on the site server. For more information about WSUS, see [Windows Server Update Services](http://go.microsoft.com/fwlink/p/?LinkID=79477).|Warning|Central administration site, <br>Primary site|  

##  <a name="BKMK_Requirements"></a> Prerequisite checks for system requirements  
The following table lists checks that Prerequisite Checker performs for system requirements.  

|Check performed|Explanation|Severity|Site applicability|
|---|---|---|---|
|**Active Directory Domain Functional Level Check**|Verifies that the Active Directory domain functional level is a minimum of Windows Server 2008 R2.|Warning|Central administration site, <br>Primary site|
|**Check Server Service is running**|Verifies that the Server Service is started.|Error|Central administration site, <br>Primary site, <br>Secondary site|  
|**Domain membership**|Verifies that the Configuration Manager computer is a member of a Windows domain.|Error|Central administration site, <br>Primary site, <br>Secondary site, <br>SMS Provider, <br>SQL Server|
|**Domain membership**|Verifies that the Configuration Manager computer is a member of a Windows domain.|Warning|Management point, <br>Distribution point|
|**FAT Drive on Site Server**|Checks whether the disk drive is formatted with the FAT file system. For better security, install site server components on disk drives formatted with the NTFS file system.|Warning|Primary site|
|**Free disk space on site server**|To install the site server, the site server computer must have at least 15 GB of free disk space. You must have an additional 1 GB of free space if you install the SMS Provider site system role on the same computer.|Error|Central administration site, <br>Primary site, <br>Secondary site|
|**Pending system restart**|Checks whether another program requires the server to be restarted before you run Setup.|Error|Central administration site, <br>Primary site, <br>Secondary site, <br>Configuration Manager console, <br>SMS Provider, <br>SQL Server, <br>Management point, <br>Distribution point|
|**Read-Only Domain Controller**|Site database servers and secondary site servers are not supported on a read-only domain controller (RODC). For more information, see [Problems when installing SQL Server on a domain controller](http://go.microsoft.com/fwlink/p/?LinkId=264856) in the Microsoft Knowledge Base.|Error|Central administration site, <br>Primary site, <br>Secondary site|
|**Schema extensions**|Determines whether the Active Directory Domain Services schema has been extended, and if so, the version of the schema extensions that were used. Configuration Manager Active Directory schema extensions are not required for site server installation, but we recommend them for the full use of all Configuration Manager features. For more information about the advantages of extending the schema, see [Prepare Active Directory for site publishing](../../../../core/plan-design/network/extend-the-active-directory-schema.md).|Warning|Central administration site, <br>Primary site|
|**Site Server FQDN Length**|Checks the length of the FQDN of the site server computer.|Error|Central administration site, <br>Primary site, <br>Secondary site|
|**Unsupported Configuration Manager console operating system**|Verifies that the Configuration Manager console can be installed on computers that run a supported operating system version. For more information, see the  [Supported operating systems for the System Center Configuration Manager console](/sccm/core/plan-design/configs/supported-operating-systems-consoles).|Error|Configuration Manager console|
|**Unsupported site server operating system version for Setup**|Verifies that a supported operating system is running on the server. For more information, see [Supported operating systems for System Center Configuration Manager site system servers](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).|Error|Central administration site, <br>Primary site, <br>Secondary site, <br>Configuration Manager console, <br>Management point, <br>Distribution point|
|**Verify database consistency**|Beginning with version 1602, this check verifies database consistency.|Error|Central administration site, <br>Primary site|  
