---
title: "List of Prerequisite Checks for System Center Configuration Manager"
ms.custom: na
ms.date: 03/11/2016
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

---
# List of Prerequisite Checks for System Center Configuration Manager
The following sections detail the available prerequisite checks.  


 For  information about using the Prerequisite Checker, see the [Prerequisite Checker](../Topic/Site%20installation%20technical%20reference%20for%20System%20Center%20Configuration%20Manager.md#bkmk_PreqChk) section of the [Site installation technical reference for System Center Configuration Manager](../Topic/Site%20installation%20technical%20reference%20for%20System%20Center%20Configuration%20Manager.md) topic.  

##  <a name="BKMK_Security"></a> Prerequisite Checks for Security Rights  
 The followingare prerequisite checks that Prerequisite Checker performs for security rights.  

 **Administrator rights on central administration site** - Verifies the user account that runs Configuration Manager Setup has local **Administrator** rights on the central administration site computer.  

-   **Severity:** Error  

-   **Applicability:**  
      -   Primary site  

**Administrative rights on expand primary site** - Verifies that the user running Setup has local **Administrator** rights on the stand-alone primary site that will be expanded.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site  

**Administrative rights on site system** - Verifies the user account that runs Configuration Manager Setup has local **Administrator** rights on the site server computer.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site  
    -   Primary site  
    -   Secondary site  

**CAS Machine administrative rights on expand primary site** - Verifies that the computer account of the central administration site has local **Administrator** rights on the stand-alone primary site that will be expanded.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site  

**Connection to SQL Server on central administration site** - Verifies the user account that runs Configuration Manager Setup on the primary site to join an existing hierarchy has the **sysadmin** role on the instance of the SQL Server for the central administration site.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Primary site  

**Site server computer account administrative rights** - Verifies that the site server computer account has administrative rights on the SQL Server and management point computers.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Primary site  
    -   SQL Server  

**Site System to SQL Server Communication** - Verifies that a valid Service Principal Name (SPN) is registered in Active Directory Domain Services for the account configured to run the SQL Server service for the SQL Server instance used to host the Configuration Manager site database. A valid SPN must be registered in Active Directory Domain Services to support Kerberos authentication.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Secondary site  
    -   Management point  

**SQL Server security mode** - Verifies that SQL Server is configured for Windows authentication security.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   SQL Server  

**SQL Server sysadmin rights** - Verifies the user account that runs Configuration Manager Setup has the **sysadmin** role on the SQL Server instance selected for site database installation. This check also fails when Setup is unable to access the instance for the SQL Server to verify permissions.  

-   **Severity:** Error  

-   **Applicability:**  

    -   SQL Server  

**SQL Server sysadmin rights for reference site** - Verifies that the user account running Configuration Manager Setup has the **sysadmin** role on the SQL Server role instance selected as the reference site database.  SQL Server **sysadmin** role permissions are required in order to modify the site database.  

-   **Severity:** Error  

-   **Applicability:**  

    -   SQL Server  

##  <a name="BKMK_Dependencies"></a> Prerequisite Checks for Configuration Manager Dependencies  
 The following are prerequisite checks that Prerequisite Checker performs for Configuration Manager dependencies.  

**Active migration mappings on the target primary site**  

 Verifies that there are no active migration mappings to primary sites.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site  

**Active Replica MP** - Checks for an active management point replica.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Primary site  

**Administrative rights on distribution point** - Verifies that the user running Setup has local **Administrator** rights on the distribution point computer.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Distribution point  

**Administrative rights on management point** -  Verifies that the computer account of site server has **Administrator** rights on the management point and distribution point computer.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Management point  

**Administrative share (Site system)** - Verifies that the required administrative shares are present on the site system computer.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Management point  

**Application Compatibility** - Verifies that current applications are compliant with the application schema.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site  

**BITS enabled** - Verifies that Background Intelligent Transfer Service (BITS) is installed on the management point site system computer. When this check fails, BITS is not installed, IIS 6 WMI compatibility component for IIS7 is not installed on the computer or the remote IIS host, or Setup was unable to verify remote IIS settings because IIS common components were not installed on the site server computer.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Management point  

**BITS installed** - Verifies that Background Intelligent Transfer Service (BITS) is installed in Internet Information Services (IIS).  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Management point  

**Case-insensitive collation on SQL Server** - Verifies that the SQL Server installation uses a case-insensitive collation, such as SQL_Latin1_General_CP1_CI_AS.  

-   **Severity:** Error  

-   **Applicability:**  

    -   SQL Server  

**Check existing stand-alone primary site for version and sitecode** - Verify that the primary site you plan to expand is a standalone primary site, and has the same version of Configuration Manager, but a different sitecode than the central administration site to be installed.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site  

**Check for incompatible collection references** - During an upgrade, this check verifies that collections only reference other collections of the same type.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site  

**Client version on management point computer** - Verifies that you are installing the management point on a computer that does not have a different version of the Configuration Manager client installed.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Management point  

**Configuration for SQL Server memory usage** - Checks whether SQL Server is configured for unlimited memory usage. You should configure SQL Server memory to have a maximum limit.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   SQL Server  

**Dedicated SQL Server instance** - Checks whether a dedicated instance of the SQL Server is configured to host the Configuration Manager site database. If another site uses the instance, you must select a different instance for the new site to use. Alternatively, you can uninstall the other site or move its database to a different instance for the SQL Server.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  

**Existing Configuration Manager server components on server** - Verifies that a site server or site system role is not already installed on the computer selected for site installation.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  

**Firewall exception for SQL Server** - Checks whether the Windows Firewall is disabled or if a relevant Windows Firewall exception exists for SQL Server. You must allow sqlservr.exe or the required TCP ports to be accessed remotely. By default, SQL Server listens on TCP port 1433 and the SQL Broker Service uses TCP port 4022.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site    
    -   Management point  

**Firewall exception for SQL Server (stand-alone primary site)** - Checks whether the Windows Firewall is disabled or if a relevant Windows Firewall exception exists for SQL Server. You must allow sqlservr.exe or the required TCP ports to be accessed remotely. By default, SQL Server listens on TCP port 1433 and the SQL Broker Service uses TCP port 4022.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Primary site (stand-alone only)  

**Firewall exception for SQL Server for management point** - Checks whether the Windows Firewall is disabled or if a relevant Windows Firewall exception exists for SQL Server.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Management point  

**IIS HTTPS Configuration** - Verifies Internet Information Services (IIS) website bindings for HTTPS communication protocol. When you select to install site roles that require HTTPS, you must configure IIS site bindings on the specified server with a valid PKI certificate.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Management point    
    -   Distribution point  

**IIS service running** - Verifies Internet Information Services (IIS) is installed and running on the computer to install the management point or distribution point.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Management point    
    -   Distribution point  

**Match Collation of expand primary site** - Verify that the site database for the stand-alone primary site that you will expand has same collation as the site database at the central administration site.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site  

**Microsoft Remote Differential Compression (RDC) library registered** - Verifies that the Microsoft Remote Differential Compression (RDC) library is registered on the Configuration Manager site server.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  

**Microsoft Windows Installer** - Verifies the Windows Installer version. When this check fails, Setup was not able to verify the version or the installed version does not meet the minimum requirement of Windows Installer version 4.5.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  

**Microsoft XML Core Services 6.0 (MSXML60)** - Verifies that Microsoft Core XML Services (MSXML) 6.0, or a later version, is installed on the computer.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site    
    -   Configuration Manager console    
    -   Management point    
    -   Distribution point  

**Minimum .NET Framework version for Configuration Manager console** - Checks whether Microsoft .NET Framework version 4.0 is installed on the Configuration Manager console computer. You can download Microsoft .NET Framework version 4.0 from [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=189149).  

-   **Severity:** Error  

-   **Applicability:**  

    -   Configuration Manager console  

**Minimum .NET Framework version for Configuration Manager site server** - Checks whether Microsoft .NET Framework version 3.5 is installed on the Configuration Manager site server. For Windows Server 2008, you can download the Microsoft .NET Framework version 3.5 from [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=185604). For Windows Server 2008 R2, you can enable the Microsoft .NET Framework version 3.5 as a feature within Server Manager.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  

**Minimum .NET Framework version for SQL Server Express edition installation for Configuration Manager secondary site** - Verifies that the Microsoft .NET Framework version 4.0 is installed on Configuration Manager secondary site computers for installing SQL Server Express edition.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Secondary site  

**Parent/child database collation** - Verifies that the collation of the site database matches the collation of the parent site's database. All sites in a hierarchy must use the same database collation.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Primary site    
    -   Secondary site  

**PowerShell 2.0 on site server** - Verifies that Windows PowerShell version 2.0 or later is installed on the site server for the Configuration Manager Exchange Connector. For more information about PowerShell 2.0, see [Article 968930](http://go.microsoft.com/fwlink/p/?LinkId=226450) in the Microsoft Knowledge Base.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Primary site  

**Primary FQDN** - Verifies that the NetBIOS name of the computer matches the local hostname (first label of the FQDN) of the computer.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site    
    -   SQL Server  

**Remote Connection to WMI on Secondary Site** - Checks whether Setup is able to establish a remote connection to WMI on the secondary site server.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Secondary site  

**Required SQL Server Collation** - Verifies that the instance for SQL Server and the Configuration Manager site database, if installed, is configured to use the SQL_Latin1_General_CP1_CI_AS collation, unless you are using a Chinese operating system and require GB18030 support.  

 For information about changing your SQL Server instance and database collations, see [Setting and Changing Collations](http://go.microsoft.com/fwlink/p/?LinkID=234541) in the SQL Server 2008 R2 Books Online.  For information about enabling GB18030 support, see [International support in System Center Configuration Manager](../../../../core/plan-design/hierarchy/international-support.md).  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  

**Setup Source Folder** - Verifies that the computer account for the secondary site has **Read** NTFS file system permissions and **Read** share permissions to the Setup source folder and share.  

> [!NOTE]  
>  The secondary site computer account must be an administrator on the computer if you use administrative shares (for example, C$ and D$).  

-   **Severity:** Error  

-   **Applicability:**  

    -   Secondary site  

**Setup Source Version** - Verifies that the Configuration Manager version in the source folder that you specified for the secondary site installation must match the Configuration Manager version of the primary site.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Secondary site  

**Site code in use** - Checks that the site code that you specified is not already in use in the Configuration Manager hierarchy. You must specify a unique site code for this site.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Primary site  

**SMS Provider machine has same domain as site server** - Checks if a computer that runs an instance of the SMS Provider has same domain as the site server.  

-   **Severity:** Error  

-   **Applicability:**  

    -   SMS Provider  

**SQL Server Edition** - Checks that the edition of SQL Server at the site is not SQL Server Express.  

-   **Severity:** Error  

-   **Applicability:**  

    -   SQL Server  

**SQL Server Express on Secondary Site** - Checks that SQL Server Express can successfully install on the site server computer for a secondary site.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Secondary site  

**SQL Server on the Secondary Site Computer** - Checks that SQL Server is installed on the secondary site computer. It is not supported to install SQL Server on remote site system.  

> [!WARNING]  
>  This check applies only when you select to have Setup use an existing instance of SQL Server.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Secondary site  

**SQL Server process memory allocation** - Verifies that SQL Server reserves a minimum of 8 GB of memory for the central administration site and primary site, and a minimum of 4 GB of memory for the secondary site. For more information about how to set a fixed amount of memory by using SQL Server Management Studio, see [How to: Set a Fixed Amount of Memory (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

> [!NOTE]  
>  This check is not applicable to SQL Server Express on a secondary site, which is limited to 1 GB of reserved memory  

-   **Severity:** Warning  

-   **Applicability:**  

    -   SQL Server  

**SQL Server service running account** - Verifies that the logon account for the SQL Server service is not a local user account or LOCAL SERVICE. You must configure the SQL Server service to use a valid domain account, NETWORK SERVICE, or LOCAL SYSTEM.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  

**SQL Server TCP Port** - Checks that TCP is enabled for the SQL Server and is set to use a static port.  

-   **Severity:** Error  

-   **Applicability:**  

    -   SQL Server  

**SQL Server version** - Verifies that a supported version of SQL Server is installed on the specified site database server. For more information, see  [Support for SQL Server versions for System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   **Severity:** Error  

-   **Applicability:**  

    -   SQL Server  

**Unsupported site system operating system version for upgrade** - During an upgrade, this rule checks whether site system roles, other than distribution points, are installed on computers that run Windows Server 2008 or earlier.  

> [!NOTE]  
>  Because this check cannot resolve the status of site system roles that are installed in Azure or for the cloud storage used by Microsoft Intune when you integrate Intune with Configuration Manager, you can ignore  warnings for these roles as false positives.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Primary site    
    -   Secondary site  

**Unsupported site system role 'Asset Intelligence synchronization point' on the expanded primary site** - Checks that the Asset Intelligence synchronization point site system role is not on installed on the stand-alone primary site that you are expanding.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site  

**Unsupported site system role 'Endpoint Protection point' on the expanded primary site** - Checks that the Endpoint Protection point site system role is not installed on the stand-alone primary site that you are expanding.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site  


**Unsupported site system role Microsoft Intune Connector' on the expanded primary site** - Checks that the 'Microsoft Intune Connector' site system role is not installed on the stand-alone primary site that you are expanding.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site  

**User State Migration Tool (USMT) installed** - Checks whether the User State Migration Tool (USMT) component of Windows Assessment and Deployment Kit (ADK) for Windows 8.1 is installed.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site (stand-alone only)  

**Validate FQDN of SQL Server Computer** - Checks that the FQDN that you specified for the SQL Server computer is valid.  

-   **Severity:** Error  

-   **Applicability:**  

    -   SQL Server  

**Verify Central Administration Site Version** - Checks that the central administration site has the same version of Configuration Manager.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Primary site  

**Verify site server permissions to publish to Active Directory** - Verifies that the computer account for the site server has **Full Control** permissions to the **System Management** container in the Active Directory domain. For more information about your options to configure required permissions, see [Extend the Active Directory schema for System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md).  

> [!NOTE]  
>  You can ignore this warning if you have manually verified the permissions.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  

**Windows Deployment Tools installed** - Checks whether the Windows Deployment Tools component of Windows Assessment and Deployment Kit (ADK) for Windows 10 is installed.  

-   **Severity:** Error  

-   **Applicability:**  

    -   SMS Provider  

**Windows Failover Cluster** - Checks that computers that have a management point or distribution point are not part of a Windows Cluster.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Management point    
    -   Distribution point  

**Windows Preinstallation Environment installed** - Checks whether the Windows Preinstallation Environment component of the Windows Assessment and Deployment Kit (ADK) for Windows 10 is installed.  

-   **Severity:** Error  

-   **Applicability:**  

    -   SMS Provider  

**Windows Remote Management (WinRM) v1.1** - Verifies that WinRM v1.1 is installed on the primary site server or Configuration Manager console computer to run the out of band management console. For more information about how to download WinRM 1.1, see [Article 936059](http://go.microsoft.com/fwlink/p/?LinkId=247166) in the Microsoft Knowledge Base.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Primary site    
    -   Configuration Manager console  

**WSUS on site server** - Verifies that Windows Server Update Services (WSUS) version 3.0 Service Pack 2 is installed on the site server. When you use a software update point on a different computer than the site server, you must install the WSUS Administration Console on the site server. For more information about WSUS, see [Windows Server Update Services](http://go.microsoft.com/fwlink/p/?LinkID=79477) web page.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site  

##  <a name="BKMK_Requirements"></a> Prerequisite Checks for System Requirements  
 The following are prerequisite checks that Prerequisite Checker performs for system requirements.  

**Active Directory Domain Functional Level Check** - Verifies that the Active Directory domain functional level is a minimum of Windows Server 2008 R2.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site  

**Check Server Service is running** - Verifies that the Server Service is started.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  

**Domain membership** - Verifies that Configuration Manager the computer is a member of a Windows domain.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site    
    -   SMS Provider    
    -   SQL Server  

**Domain membership** - Verifies that Configuration Manager the computer is a member of a Windows domain.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Management point    
    -   Distribution point  

**FAT Drive on Site Server** - Checks whether the disk drive is formatted with the FAT file system. Install site server components on disk drives formatted with the NTFS file system for better security.  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Primary site  

**Free disk space on site server** - The site server computer must have at least 5 GB of free disk space to install the site server. You must have an additional 1 GB of free space if you install the SMS Provider site system role on the same computer.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  

**Pending system restart** - Checks whether another program requires the server to be restarted before you run Setup.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  
    -   Configuration Manager console    
    -   SMS Provider    
    -   SQL Server    
    -   Management point    
    -   Distribution point  

**Read-Only Domain Controller** - Site database servers and secondary site servers are not supported on a read-only domain controller (RODC). For more information, see [You may encounter problems when installing SQL Server on a domain controller](http://go.microsoft.com/fwlink/p/?LinkId=264856) in the Microsoft Knowledge Base.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  

**Schema extensions** - Determines whether the Active Directory Domain Services schema has been extended, and if so, the version of the schema extensions that were used. Configuration Manager Active Directory schema extensions are not required for site server installation, but are recommended to fully support the use of all Configuration Manager features. For more information about the advantages of extending the schema, see [Extend the Active Directory schema for System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md).  

-   **Severity:** Warning  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site  

**Site Server FQDN Length** - Checks the length of the FQDN of the site server computer.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site  

**Unsupported Configuration Manager console operating system** - Verifies that the Configuration Manager consoles can be installed on computers that run a supported operating system version. For more information, see the  [Supported operating systems for System Center Configuration Manager consoles](../Topic/Supported%20operating%20systems%20for%20sites%20and%20clients%20for%20System%20Center%20Configuration%20Manager.md#bkmk_ConsoleOS) section in the [Supported operating systems for sites and clients for System Center Configuration Manager](../Topic/Supported%20operating%20systems%20for%20sites%20and%20clients%20for%20System%20Center%20Configuration%20Manager.md) topic.  

-   **Severity:** Error  

-   **Applicability:**  

    -   Configuration Manager console  

**Unsupported site server operating system version for Setup** - Verifies that a supported operating system is running on the server. For more information, see  [Supported operating systems for sites and clients for System Center Configuration Manager](../Topic/Supported%20operating%20systems%20for%20sites%20and%20clients%20for%20System%20Center%20Configuration%20Manager.md).  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site    
    -   Secondary site    
    -   Configuration Manager console    
    -   Management point    
    -   Distribution point  

**Verify database consistency** - Beginning with version 1602, this check verifies database consistency  

-   **Severity:** Error  

-   **Applicability:**  

    -   Central administration site    
    -   Primary site  
