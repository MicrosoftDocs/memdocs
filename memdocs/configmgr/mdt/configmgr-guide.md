---
title: Quickstart - ZTI
titleSuffix: Microsoft Deployment Toolkit
description: A quickstart guide for Microsoft Deployment Toolkit (MDT) with System Center 2012 R2 Configuration Manager for the zero-touch installation (ZTI)
ms.date: 09/09/2016
ms.subservice: mdt
ms.service: configuration-manager
ms.topic: quickstart
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: frankroj,mstewart,aaroncz
---

# Quick Start Guide for Microsoft System Center 2012 R2 Configuration Manager

Microsoft Deployment Toolkit (MDT) 2013 provides technology for deploying Windows operating systems, and Microsoft Office. This quick start guide helps you quickly evaluate MDT 2013 by providing condensed, step-by-step instructions for using it to install the Windows 8.1 operating system with Microsoft System Center 2012 R2 Configuration Manager. This quick start guide demonstrates how to perform the New Computer deployment scenario, which covers the deployment of Windows 8.1 to a new computer. This scenario assumes that there is no user data or profile to preserve.

> [!NOTE]
>
> In this document, *Windows* applies to the Windows 8.1, Windows 8, Windows 7, Windows Server® 2012 R2, Windows Server 2012, and Windows Server 2008 R2 operating systems unless otherwise noted. MDT does not support ARM processor-based versions of Windows. Similarly, *MDT* refers to MDT 2013 unless otherwise stated.

 After using this guide to evaluate MDT, review the rest of the MDT guidance to learn more about the technology's advanced features.

## Prerequisites

Zero Touch Installation installations using Configuration Manager have the following prerequisites.

### Required Software

To complete this guide, the following software is required:

- Windows Server 2008 R2

- Microsoft SQL Server 2008 R2

- SQL Server 2008 R2 Service Pack 1 (SP1)

- SQL Server 2008 R2 SP1 Cumulative Update 6 (CU6)

- Windows 8.1

- System Center 2012 R2 Configuration Manager

- Microsoft .NET Framework version 3.5 with SP1

- Windows PowerShell version 2.0

- Windows Preinstallation Environment (Windows PE), which is included in Configuration Manager

- Networking services, including Domain Name System (DNS) and Dynamic Host Configuration Protocol (DHCP)

- Active Directory Domain Services (AD DS)

  See the [Supported Configurations for Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg682077(v=technet.10)) for additional software combinations that can be used for installing Configuration Manager.

> [!NOTE]
>
> The Task Sequencer used in MDT deployments requires that the Create Global Object right be assigned to credentials used to access and run the Deployment Workbench and the deployment process. This right is normally available to accounts with Administrator-level permissions (unless explicitly removed). Also, the Specialized Security - Limited Functionality (SSLF) security profile removes the Create Global Object right and should not be applied to computers deployed using MDT.

### Computer Configuration

To complete this guide, set up the computers listed in the following table. These computers can be either physical computers or virtual machines (VMs) with the system resources designated.

|**Computer**|**Description and system resources**|
|-|-|
|WDG-MDT-01|This computer runs the MDT infrastructure and Configuration Manager. The computer runs Windows Server 2008 R2 with the following networking services installed:<br><br> -   AD DS<br>-   DNS Server<br>-   DHCP Server<br>-   Windows Deployment Services<br><br> The system resources of the computer are as follows:<br><br> -   Quad-core processor running at 2.66 gigahertz (GHz) or faster<br>-   4 gigabytes (GB) or more of physical memory<br>-   A disk partition that has 40 GB or more of available disk space; it will become the drive C partition<br>-   One CD-ROM or DVD-ROM drive that will be assigned the drive letter D<br>-   A disk partition that has 40 GB or more of available disk space; it will become partition E.|
|WDG-REF-01|This is the reference computer, which runs no current operating system. The system resources of the computer are as follows:<br><br> -   Processor running at 1.4 GHz or faster<br>-   1 GB or more of physical memory<br>-   16 GB or more of available disk space|
|WDG-CLI-01|This is the target computer, which runs no current operating system. The system resources of the computer are as follows:<br><br> -   Processor running at 1.4 GHz or faster<br>-   1 GB or more of physical memory<br>-   16 GB or more of available disk space|

 The resources listed in the preceding table reflect the system resources recommended to perform the steps in this guide. For information on the minimum system resource requirements for:

- Windows Server 2008 R2, see [Installing Windows Server 2008 R2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379511(v=ws.10))

- SQL Server 2008 R2, see [Hardware and Software Requirements for Installing SQL Server 2008 R2](/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server)

> [!NOTE]
>
> This guide assumes that MDT is being evaluated on 64-bit (x64) physical or virtual computers. If evaluating MDT on 32-bit (x86) platforms, download and install the x86 editions of MDT and the components that this guide describes.

## Step 1: Prepare the Prerequisite Infrastructure

For purposes of this guide, all the prerequisite infrastructure services run on the computer named *WDG-MDT-01*. Install the prerequisite software, server roles, and services on this computer before installing MDT.

> [!NOTE]
>
> This section assumes that you are creating a new Configuration Manager infrastructure for MDT. If you are using an existing Configuration Manager infrastructure, review the steps in this section and substitute existing resource names for the resources created in this section (such as the computer name and shared network folders). After reviewing this section, proceed to [Step 2: Prepare the MDT Environment](#PrepareMDTEnvironment).

 Prepare the prerequisite infrastructure before installing MDT by:

- Installing Windows Server 2008 R2 as described in [Step 1-1: Install Windows Server 2008 R2](#InstallWindowsServer)

- Creating the required folders and network shares as described in [Step 1-2: Create the Required Folders and Network Shares](#CreateRequiredFolders)

- Obtaining the software required to perform the steps in this guide as described in [Step 1-3: Obtain the Required Software](#ObtainRequiredSoftware)

- Installing the AD DS server role as described in [Step 1-4: Install the AD DS Server Role](#InstallADDSRole)

- Installing the DHCP Server server role as described in [Step 1-5: Install the DHCP Server Server Role](#InstallDHCPServerRole)

- Installing the Web Services (IIS) server role as described in [Step 1-6: Install the Web Services (IIS) Server Role](#InstallIISRole)

- Adding the required Windows Server 2008 R2 features as described in [Step 1-7: Add the Required Windows Server 2008 R2 Features](#AddRequiredServerFeatures)

- Creating the user and service accounts required to perform the steps in this guide as described in [Step 1-8: Create the Required User and Service Accounts](#CreateRequiredUserAccounts)

- Installing SQL Server 2008 R2 for Configuration Manager to use as described in [Step 1-9: Install SQL Server 2008 R2](#InstallSQLServer)

- Adding the site server to the Administrators security group as described in [Step 1-10: Add the Site Server to the Administrators Security Group](#AddSiteSecuritytoAdminGroup)

- Installing Configuration Manager as described in [Step 1-11: Install Configuration Manager](#InstallConfigManager)

- Configuring the network access account that Configuration Manager clients use to access Configuration Manager distribution points as described in [Step 1-12: Configure the Network Access Account](#ConfigureNetworkAccessAccount)

- Configuring the Configuration Manager site boundaries  and boundary groups as described in [Step 1-13: Configure the Configuration Manager Site Boundaries and Boundary Groups](#ConfigurationManagerSiteBoundaries)

- Configuring the publishing of site information in AD DS and DNS as described in [Step 1-14: Configure the Publishing of Site Information in AD DS and DNS](#ConfigurePublishingSiteInfo)

###  <a name="InstallWindowsServer"></a> Step 1-1: Install Windows Server 2008 R2

 Information for Installing Windows Server 2008 R2. Accept default values unless otherwise specified.

|When prompted for| Provide these values|
|-|-|
|**Where do you want to install Windows?**|**Disk 0 Unallocated Space**|
|**Password**|Any strong password|
|**Computer name**|**WDG-MDT-01**|
|**Format for volumes C and E**|**NTFS**|
|**TCP/IP configuration**|Configure with a static IP address configuration, with the other TCP/IP configuration options as appropriate for the environment|

###  <a name="CreateRequiredFolders"></a> Step 1-2: Create the Required Folders and Network Shares

The MDT deployment process requires additional folders that are used as the source for files or to store files created during the MDT deployment process. Some of these folders need to be shared so that they can be accessed from other computers.

#### To create the required folders and share
1. The MDT Deployment Process Requires several folders. Create the following folders and shares with the specified permissions for each share.

   | Create this folder | With this share name |                With these share permissions                 |
   |--------------------|----------------------|-------------------------------------------------------------|
   |     E:\Source$     |       Source$        | **Administrators:** Co-owner<br><br> **Everyone:** Read |
   |     E:\Images$     |       Images$        | **Administrators:** Co-owner<br><br> **Everyone:** Read |
   |    E:\Capture$     |       Capture$       | **Administrators:** Co-owner<br><br> **Everyone:** Read |
   |    E:\Packages$    |      Packages$       | **Administrators:** Co-owner<br><br> **Everyone:** Read |

2. Create the following folders:

    - E:\CMDownloads

    - E:\Source$\CustomSettings

    - E:\Source$\Drivers

    - E:\Source$\Windows_8-1

    - E:\Source$\MDT_2013

    - E:\Source$\SQL2008R2

    - E:\Source$\SQL2008R2SP1

    - E:\Source$\SQL2008R2CU6

    - E:\Source$\ConfigMgr

    - E:\Packages$\Drivers

3. Copy the device drivers for the reference computer (WDG-REF-01) and the target computer (WDG-CLI-01) to E:\Source$\Drivers.

> [!NOTE]
>
> The processes in this guide assume that the reference computer and target computer have the same devices and do not require different devices drivers.

###  <a name="ObtainRequiredSoftware"></a> Step 1-3: Obtain the Required Software

Besides Windows Server 2008 R2, Windows 8.1, and Configuration Manager, certain software is required to evaluate MDT based on the processes in this guide.  The following table lists the software required to perform deployments using MDT, where to obtain the software, and where to place the software on WDG-MDT-01.

 |**Obtain this software**|**Place in this folder**|
 |-|-|
 |MDT 2013|E:\Source$\MDT_2013|
 |Windows 8.1 distribution files from the product media|E:\Source$\Windows_8-1|
 |Device drivers required for the reference and target computers (WDG-REF-01 and WDG-CLI-01)|E:\Source$\Drivers|
 |SQL Server 2008 R2 from the product media|E:\Source$\SQL2008R2|
 |SQL Server 2008 R2 SP1, available at [https://www.microsoft.com/download/details.aspx?id=26113](https://www.microsoft.com/download/details.aspx?id=26113)|E:\Source$\SQL2008R2SP1|
 |SQL Server 2008 R2 SP1 CU6, available at [https://support.microsoft.com/kb/2679367](https://support.microsoft.com/kb/2679367)|E:\Source$\SQL2008R2SP1CU6|
 |Configuration Manager from the product media|E:\Source$\ConfigMgr|

###  <a name="InstallADDSRole"></a> Step 1-4: Install the AD DS Server Role

AD DS is required to provide authentication and act as a repository for configuration values for the Microsoft products and technologies that MDT uses, such as SQL Server 2008 R2 and Configuration Manager.

 To install AD DS, run the DCPROMO Wizard to configure the computer as a domain controller. Install AD DS using the following information, accepting any defaults unless otherwise specified.

|**When prompted**|**Do this**|
|-|-|
|For the domain type|Create a new domain in a new forest.|
|For the fully qualified domain name|Type **mdt2013.corp.woodgrovebank.com**.|
|For the forest functional level|Select **Windows Server 2008 R2**.|
|To install the DNS Server service as part of the domain controller installation process|Select **Yes**.|

###  <a name="InstallDHCPServerRole"></a> Step 1-5: Install the DHCP Server Server Role

The DHCP Server server role is required to provide automatic IP configuration for the target computers. Install DHCP Server using the following information, accepting any defaults unless otherwise specified.

> [!NOTE]
>
> If you are using a virtualized environment, disable any DHCP configuration that the computer-virtualization software provides. Ensure that the DHCP Server service running WDG-MDT-01 is the only provider of IP configuration using DHCP.

|**On this wizard page**|**Do this**|
|-|-|
|**Authorize DHCP server in Active Directory**|Authorize WDG-MDT-01 to provide client IP configuration.|
|**DHCP scopes**|Create an appropriate scope that can be used to automatically configure TCP/IP for WDG-REF-01 and WDG-CLI-01.|
|**DHCPv6 stateless mode configuration**|Disable DHCPv6 stateless mode for this server.|

###  <a name="InstallIISRole"></a> Step 1-6: Install the Web Services (IIS) Server Role

Install the Web Services (IIS) server role with the role services listed in the following table.  These role services are required for SQL Server 2008 R2 and Configuration Manager. Unless otherwise specified, use the default values.

|Role service|Status|
|-|-|
|Web Server|Installed|
|Common HTTP Features|Installed|
|Static Content|Installed|
|Default Document|Installed|
|Directory Browsing|Installed|
|HTTP Errors|Installed|
|HTTP Redirection|Installed|
|WebDAV Publishing|Installed|
|Application Development|Installed|
|ASP.NET|Installed|
|.NET Extensibility|Installed|
|ASP|Not installed|
|CGI|Not installed|
|ISAPI Extensions|Installed|
|ISAPI Filters|Installed|
|Server Side Includes|Not installed|
|Health and Diagnostics|Installed|
|HTTP Logging|Installed|
|Logging Tools|Installed|
|Request Monitor|Installed|
|Tracing|Installed|
|Custom Logging|Not installed|
|ODBC Logging|Not installed|
|Security|Installed|
|Basic Authentication|Not installed|
|Windows Authentication|Installed|
|Digest Authentication|Not installed|
|Client Certificate Mapping Authentication|Not installed|
|IIS Client Certificate Mapping Authentication|Not installed|
|URL Authorization|Not installed|
|Request Filtering|Installed|
|IP and Domain Restriction|Not installed|
|Performance|Installed|
|Static Content Compression|Installed|
|Dynamic Content Compression|Not installed|
|Management Tools|Installed|
|IIS Management Console|Installed|
|IIS Management Scripts and Tools|Not installed|
|Management Service|Not installed|
|IIS 6 Management Compatibility|Installed|
|IIS 6 Metabase Compatibility|Installed|
|IIS 6 WMI Compatibility|Installed|
|IIS 6 Scripting Tools|Not installed|
|IIS 6 Management Console|Not installed|
|FTP Publishing Service|Not installed|
|FTP Server|Not installed|
|FTP Management Console|Not installed|
|IIS Hostable Web Core|Not installed|

###  <a name="AddRequiredServerFeatures"></a> Step 1-7: Add the Required Windows Server 2008 R2 Features

In addition to installing the required Windows Server 2008 R2 server roles, add the following required features in Server Manager in the **Features Summary** section:

- Background Intelligent Transfer Service

- Remote Differential Compression

###  <a name="CreateRequiredUserAccounts"></a> Step 1-8: Create the Required User and Service Accounts

Configuration Manager and SQL Server 2008 R2 require user accounts during the installation process.  Use the following information for creating these accounts.

|                      **Create this account**                      |                                                                                                                                                                                                                                                                     **With these settings**                                                                                                                                                                                                                                                                      |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                 SQL Server Agent service account                  |      1. In **First name**, type **SQL Agent**.<br>2. In **Last name**, type **Service Account**.<br>3. In **User logon name**, type **SQLAgent**.<br>4. In **Password** and **Confirm password**, type **P@ssw0rd**.<br>5. Clear the **User must change password at next logon** check box.<br>6. Select the **Password never expires** check box.<br>7. Make the account a member of the Domain Admins security group.<br>8. In **Description**, type **Service account used to run SQL Server 2008 R2 Agent service**.      |
|            SQL Server Database Engine service account             | 1. In **First name**, type **SQL DB Engine**.<br>2. In **Last name**, type **Service Account**.<br>3. In **User logon name**, type **SQLDBEngine**.<br>4. In **Password** and **Confirm password**, type **P@ssw0rd**.<br>5. Clear the **User must change password at next logon** check box.<br>6. Select the **Password never expires** check box.<br>7. Make the account a member of the Domain Admins security group.<br>8. In **Description**, type **Service account used to run SQL Server 2008 R2 database engine**.  |
|           SQL Server Reporting Services service account           | 1. In **First name**, type **SQL Reporting**.<br>2. In **Last name**, type **Service Account**.<br>3. In **User logon name**, type **SQLReport**.<br>4. In **Password** and **Confirm password**, type **P@ssw0rd**.<br>5. Clear the **User must change password at next logon** check box.<br>6. Select the **Password never expires** check box.<br>7. Make the account a member of the Domain Admins security group.<br>8. In **Description**, type **Service account used to run SQL Server 2008 R2 reporting services**. |
| Configuration Manager Client Network Access account |                           1. In **First name**, type **CM 2012**.<br>2. In **Last name**, type **Client Network Access**.<br>3. In **User logon name**, type **CMNetAccess**.<br>4. In **Password** and **Confirm password**, type **P@ssw0rd**.<br>5. Clear the **User must change password at next logon** check box.<br>6. Select the **Password never expires** check box.<br>7. In **Description**, type **Service account used as the network access account for Configuration Manager Client**.                           |

###  <a name="InstallSQLServer"></a> Step 1-9: Install SQL Server 2008 R2

Before installing Configuration Manager, install SQL Server 2008 R2 with SP1 and CU6 for SP1.

> [!NOTE]
>
> To enable all SQL Server 2008 R2 features, install the Web Services (IIS) server role before installing SQL Server 2008 R2.

#### To install SQL Server 2008 R2
1. Start the SQL Server Installation Center.

2. In the SQL Server Installation Center, in the navigation pane, select **Installation**.

3. In the details pane, select **New installation or add features to an existing installation**.

    SQL Server 2008 R2 Setup Wizard starts.

4. Install SQL Server 2008 R2 using the following information, accepting the defaults unless otherwise specified.

   |       **On this wizard page**        |                                                                                                                                                                                                                          **Do this**                                                                                                                                                                                                                           |
   |--------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |       **Setup Support Rules**        |                                                                                                                                                                                                                         Select **OK**.                                                                                                                                                                                                                          |
   |           **Product Key**            |                                                                                                                                                                                                                        Select **Next**.                                                                                                                                                                                                                         |
   |          **License Terms**           |                                                                                                                                                                                         Select the **I accept the license terms** check box, and then select **Next**.                                                                                                                                                                                          |
   |       **Setup Support Files**        |                                                                                                                                                                                                                       Select **Install**.                                                                                                                                                                                                                       |
   |       **Setup Support Rules**        |                                                                                                                                                                                         Ensure that no critical results exist for the rules, and then select **Next**.                                                                                                                                                                                          |
   |            **Setup Role**            |                                                                                                                                                                                                 Select **SQL Server Feature Installation**, and select **Next**.                                                                                                                                                                                                 |
   |        **Feature Selection**         |                                                                                                            1. Select **Database Engine Services** check box.<br>2. Select **Reporting Services** check box.<br>3. Select **Full-Text Search** check box.<br>4. Select **Management Tools - Complete** check box.<br>5. Select **Next**.                                                                                                            |
   |        **Installation Rules**        |                                                                                                                                                                                                                        Select **Next**.                                                                                                                                                                                                                         |
   |      **Instance Configuration**      |                                                                                                                                                                                                                        Select **Next**.                                                                                                                                                                                                                         |
   |     **Disk Space Requirements**      |                                                                                                                                                                                                                        Select **Next**.                                                                                                                                                                                                                         |
   |       **Server Configuration**       | 1. For **SQL Server Agent**, in **Account Name**, type **MDT2013\SQLAgent**, and in **Password**, type **P@ssw0rd**.<br>2. For **SQL Server Database Engine**, in **Account Name**, type **MDT2013\SQLDBEngine**, in **Password**, type **P@ssw0rd**.<br>3. For **SQL Server Reporting Services**, in **Account Name**, type **MDT2013\SQLReport**, in **Password**, type **P@ssw0rd**.<br>4. Select **Next**. |
   |  **Database Engine Configuration**   |                                                                                                                                                                                                        Select **Add Current User**, and select **Next**.                                                                                                                                                                                                         |
   | **Reporting Services Configuration** |                                                                                                                                                                                                                        Select **Next**.                                                                                                                                                                                                                         |
   |         **Error Reporting**          |                                                                                                                                                                                                                        Select **Next**.                                                                                                                                                                                                                         |
   | **Installation Configuration Rules** |                                                                                                                                                                                                                        Select **Next**.                                                                                                                                                                                                                         |
   |         **Ready to Install**         |                                                                                                                                                                                                                       Select **Install**.                                                                                                                                                                                                                       |
   |             **Complete**             |                                                                                                                                                                                                                        Select **Close**.                                                                                                                                                                                                                        |

5. Close the SQL Server Installation Center.

#### To install SQL Server 2008 R2 SP1
1. In Windows Explorer, go to E:\Source$\SQL2008R2SP1, and double-click **SQLServer2008R2SP1-KB2528583-x64-ENU.exe**.

    The **Extracting Files** dialog box displays the file-extraction process. When the process is complete, the SQL Server 2008 R2 Service Pack 1 Update Setup Wizard starts.

2. Install SQL Server 2008 R2 SP1 using the following information, accepting the defaults unless otherwise specified.

   |**On this wizard page**|**Do this**|
   |-|-|
   |**SQL Server 2008 R2 update**|Select **Next**.|
   |**License Terms**|Select the **I accept the license terms** check box, and then select **Next**.|
   |**Select Features**|Select **Next**.|
   |**Check Files In Use**|Select **Next**.|
   |**Ready to update**|Select **Update**.|
   |**Update Progress**|The progress is displayed on the wizard page as the update is performed and completes.|
   |**Complete**|Select **Close**.|

#### To install SQL Server 2008 R2 SP1 CU6
1. In Windows Explorer, go to E:\Source$\SQL2008R2SP1CU6, and double-click **446622_intl_x64_zip.exe**.

    The **Microsoft Self-Extractor** dialog box appears.

2. In the **Microsoft Self-Extractor** dialog box, select **Continue**.

3. In the **Microsoft Self-Extractor** dialog box, in **Select the folder where you want to unzip the files to**, type **E:\Source$\SQL2008R2SP1CU6**, and then select **OK**.

   > [!NOTE]
   >  You can select the ellipsis (**...**) to browse for the E:\Source$\SQL2008R2SP1CU6 folder.

    The extraction process is displayed. When the process is complete, the completion status is displayed.

4. In the **Microsoft Self-Extractor** dialog box, select **OK**.

5. In Windows Explorer, go to E:\Source$\SQL2008R2SP1CU6, and double-click **SQLServer2008R2-KB2679367-x64.exe**.

    The **Extracting Files** dialog box displays the file-extraction process. When the process is complete, the SQL Server 2008 R2 Service Pack 1 CU6 Update Setup Wizard starts.

6. Install SQL Server 2008 R2 SP1 CU6 using the following information, accepting the defaults unless otherwise specified.

   |**On this wizard page**|**Do this**|
   |-|-|
   |**SQL Server 2008 R2 update**|Select **Next**.|
   |**License Terms**|Select the **I accept the license terms** check box, and then select **Next**.|
   |**Select Features**|Select **Next**.|
   |**Check Files In Use**|Select **Next**.|
   |**Ready to update**|Select **Update**.|
   |**Update Progress**|The progress is displayed on the wizard page as the update is performed.|
   |**Complete**|Select **Close**.|

   The **Install a SQL Server 2008 R2 Update** dialog box appears prompting you to restart the computer to complete the setup.

7. In the **Install a SQL Server 2008 R2 update** dialog box, select **OK**.

8. Restart the computer.

9. After installing SQL Server 2008 R2 SP1 CU6, the SQL Server build number should be 10.51.2811.0.

    > [!TIP]
    >
    > You can verify the SQL Server build number by viewing the SQL Server updates applied in the Programs and Features Control Panel item by selecting **View installed updates**.

###  <a name="AddSiteSecuritytoAdminGroup"></a> Step 1-10: Add the Site Server to the Administrators Security Group

When all computers are in the same forest, manually add the site server computer account to the local Administrators group on each computer. Complete this step before configuring the computer as a site system.

 **To add the site server to the Administrators security group**

1. Select **Start**, point to **Administrative Tools**, and then select **Active Directory Users and Computers**.

2. In the Active Directory Users and Computers console tree, go to mdt2013.corp.woodgrovebank.com/Builtin.

3. In the preview pane, right-click **Administrators**, and then select **Properties**.

4. In the **Administrators Properties** dialog box, select the **Members** tab, and then select **Add**.

5. In the **Select Users, Contacts, Computers, or Groups** dialog box, select **Object Types**.

6. In the **Object Types** dialog box, in **Object types**, select **Computers**, and then select **OK**.

7. In the **Select Users, Contacts, Computers, or Groups** dialog box, in **Enter the object names to select**, type **WDG-MDT-01**. Select **Check Names**, and then select **OK**.

8. Close any open windows.

###  <a name="InstallConfigManager"></a> Step 1-11: Install Configuration Manager

When the other products and technologies have been installed, install Configuration Manager. Before doing so, however, extend the Active Directory schema so that computers can locate the distribution points, service locator points, and other server roles. Also, you can extend the schema after you have installed Configuration Manager. For more information about how to extend the Active Directory schema for Configuration Manager, see the section, "Extend the Active Directory Schema," in the Configuration Manager Documentation Library, which is installed with Configuration Manager.

 After extending the Active Directory schema, install Configuration Manager. The configuration of WDG-MDT-01 supports Configuration Manager for this sample. The configuration of computers in the production network may vary. To find out more about the prerequisites for installing Configuration Manager, see [Supported Configurations for Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg682077(v=technet.10)).

#### To install Configuration Manager
1. Start the System Center 2012 R2 Configuration Manager Setup splash screen.

2. On the System Center 2012 R2 Configuration Manager Setup splash screen, select the **Install** link.

    The Microsoft System Center 2012 R2 Configuration Manager Setup Wizard starts.

3. Complete the Microsoft System Center 2012 R2 Configuration Manager Setup Wizard using the following information, accepting the defaults unless otherwise specified.

   |                  **On this wizard page**                  |                                                                                                                                                                                                        **Do this**                                                                                                                                                                                                        |
   |-----------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |                   **Before You Begin**                    |                                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                                      |
   |                    **Getting Started**                    |                                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                                      |
   |                      **Product Key**                      |                                                                                                                                          In **Enter your 25-character product key**, type ***product_key*** (where *product_key* is your product key for Configuration Manager).                                                                                                                                          |
   |           **Microsoft Software License Terms**            |                                                                                                                                                                      Select the **I accept these license terms** check box, and then select **Next**.                                                                                                                                                                      |
   |                 **Prerequisite Licenses**                 | 1. In the **Microsoft SQL Server 2008 R2 Express** section, select the **I accept these License Terms** check box.<br>2. In the **Microsoft SQL Server 2008 Native Client** section, select the **I accept these License Terms** check box.<br>3. In the **Microsoft Silverlight 4** section, select the **I accept these License Terms and automatic updates of Silverlight** check box.<br>4. Select **Next**. |
   |            **Update Prerequisite Components**             |                                                                                                                                      In **Download and use the latest updates. Updates will be saved to the following location**, type **E:\CMDownloads**, and then select **Next**.                                                                                                                                       |
   |               **Server Language Selection**               |                                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                                      |
   |               **Client Language Selection**               |                                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                                      |
   |            **Site and Installation Settings**             |                                                                                                                                                   1. In **Site code**, type **NYC**.<br>2. In **Site name**, type **New York City Site**.<br>3. Select **Next**.                                                                                                                                                    |
   |               **Primary Site Installation**               |                                                               1. Select **Install the primary site as a stand-alone site**.<br>2. Select **Next**.<br>     The **Configuration Manager** dialog box appears, confirming that you want to install this site as a stand-alone site.<br>3. In the **Configuration Manager** dialog box, select **Yes**.                                                                |
   |                 **Database Information**                  |                                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                                      |
   |                 **SMS Provider Settings**                 |                                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                                      |
   |        **Client Computer Communication Settings**         |                                                                                                                                                              Select **Configure the communication method on each site system role**, and then select **Next**.                                                                                                                                                              |
   |                   **Site System Roles**                   |                                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                                      |
   | **Customer Experience Improvement Program Configuration** |                                                                                                                                          1. Select the appropriate participation in the Customer Experience Improvement program for your organization.<br>2. Select **Next**.                                                                                                                                          |
   |                   **Settings Summary**                    |                                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                                      |
   |                  **Prerequisite Check**                   |                                                                                                                                                                                                 Select **Begin Install**.                                                                                                                                                                                                  |
   |                        **Install**                        |                                                                                                                                                                   1. Monitor the installation process until it is complete.<br>2. Select **Close**.                                                                                                                                                                    |

4. Close all open windows and dialog boxes.

   When the wizard is complete, Configuration Manager is installed.

###  <a name="ConfigureNetworkAccessAccount"></a> Step 1-12: Configure the Network Access Account

The Configuration Manager client needs an account to provide credentials when accessing the Configuration Manager distribution points, MDT deployment shares, and shared folders. This account is called the *Network Access account*. The CMNetAccess account was created earlier in the process to use as the Network Access account.

#### To configure the Network Access account
1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Administration**.

3. In the Administration workspace, go to Overview/Site Configuration/Sites.

4. In the preview pane, select **NYC - New York City Site**.

5. On the Ribbon, select **Settings**, select **Configure Site Components**, and then select **Software Distribution**.

6. In the **Software Distribution Component Properties** dialog box, select the **Network Access Account** tab.

7. In **Network Access Account**, select **Specify the account that accessed network locations**, select **Set**, and then select **New Account**.

    The **Windows User Account** dialog box appears.

8. Complete the **Windows User Account** dialog box using the following information, and then select **OK**.

   |     **For this**     |           **Do this**           |
   |----------------------|---------------------------------|
   |    **User name**     |  Type **MDT2013\CMNetAccess**.  |
   |     **Password**     | Type **P@ssw0rd**. |
   | **Confirm password** | Type **P@ssw0rd**. |

9. In the **Software Distribution Component Properties** dialog box, select **OK**.

10. Close any open windows.

###  <a name="ConfigurationManagerSiteBoundaries"></a> Step 1-13: Configure the Configuration Manager Site Boundaries and Boundary Groups

The Configuration Manager client needs to know the boundaries for the site. Unless the site boundaries are specified, the client assumes that the computer running Configuration Manager is in a remote site. Add a site boundary based on the IP subnet that WDG-MDT-01, WDG-REF-01, and WDG-CLI-01 use. Then add the site boundary to a site boundary group.

#### To create a Configuration Manager site boundary
1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Administration**.

3. In the Administration workspace, go to Overview/Hierarchy Configuration/Boundaries.

4. On the Ribbon, select **Create Boundary**.

    The **Create Boundary** dialog box opens.

5. Complete the **Create Boundary** dialog box using the following information, and then select **OK**.

   > [!NOTE]
   >  For this sample, the site boundary is specified by network address. However, you can also specify site boundaries using an AD DS site name or an IP address range.

   |**For this**|**Do this**|
   |-|-|
   |**Description**|Type **IP Subnet Boundary**.|
   |**Type**|Select **IP subnet**.|
   |**Network**|Type ***network_address*** (where *network_address* is the network address of the subnet where the computers are installed).|
   |**Subnet mask**|Type ***subnet_mask*** (where *subnet_mask* is the subnet mask of the subnet where the computers are installed).|

#### To add the Configuration Manager site boundary to a site boundary group
1. In the Configuration Manager console, in the navigation pane, select **Administration**.

2. In the Administration workspace, go to Overview/Hierarchy Configuration/Boundary Groups.

3. On the Ribbon, select **Create Boundary Group**.

    The **Create Boundary Group** dialog box opens.

4. Complete the **General** tab of the **Create Boundary Group** dialog box using the following information.

   |  **For this**   |                                                                                                                                                       **Do this**                                                                                                                                                        |
   |-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    **Name**     |                                                                                                                                          Type **New York City Boundary Group**.                                                                                                                                          |
   | **Description** |                                                                                                                  Type **This is the boundary group for the site boundaries at the New York City site**.                                                                                                                  |
   |   Boundaries    | 1. Select **Add**.<br>     The **Add Boundaries** dialog box appears.<br>2. In the **Add Boundaries** dialog box, select ***site_boundary*** (where *site_boundary* is the site boundary you created earlier in the process), and then select **OK**.<br>     The site boundary appears in the list of boundaries. |

5. Complete the **References** tab of the **Create Boundary Group** dialog box using the following information, and then select **OK**.

   |     **For this**     |                                                                                                                                       **Do this**                                                                                                                                       |
   |----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | **Site assignment**  |                                                                                                          Select the **Use this boundary group for site assignment** check box.                                                                                                          |
   | **Content location** | 1. Select **Add**.<br>     The **Add Site Systems** dialog box appears.<br>2. In the **Add Site Systems** dialog box, select **\\\WDG-MDT-01.mdt2013.corp.woodgrovebank.com**, and then select **OK**.<br>     The site system server appears in the list of site system servers. |

6. Close any open windows.

###  <a name="ConfigurePublishingSiteInfo"></a> Step 1-14: Configure the Publishing of Site Information in AD DS and DNS

The Configuration Manager client needs to locate the various Configuration Manager server roles. Modify the site properties to publish the site information in AD DS and in DNS.

 **To configure the publishing of site information in AD DS and in DNS**

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Administration**.

3. In the Administration workspace, go to Overview/Site Configuration/Sites.

4. In the preview pane, select **NYC - New York City Site**.

5. On the Ribbon, select **Properties**.

6. In the **New York City Site Properties** dialog box, on the **Publishing** tab, verify that the **mdt2013.corp.woodgrovebank.com** Active Directory forest is listed, and then select **Cancel**.

7. Close any open windows.

##  <a name="PrepareMDTEnvironment"></a> Step 2: Prepare the MDT Environment

The first step in the deployment process is to prepare the MDT environment. When this step is complete, you can create the reference computer and deploy a captured image of it to the target computer (WDG-CLI-01) using Configuration Manager integration with MDT.

 Prepare the MDT environment by:

- Installing MDT as described in [Step 2-1: Install MDT](#InstallMDT)

- Enabling Configuration Manager console integration by running the Configure ConfigMgr Integration script as described in [Step 2-2: Enable Configuration Manager Console Integration](#EnableConfigManagerConsole)

###  <a name="InstallMDT"></a> Step 2-1: Install MDT

To install MDT, complete the following steps:

1. In Windows Explorer, go to E:\Source$\MDT_2013.

2. Double-click **MicrosoftDeploymentToolkit2013_x64.msi** (for 64-bit operating systems) or **MicrosoftDeploymentToolkit2013_x86.msi** (for 32-bit operating systems), and then select **Install**.

    The Microsoft Deployment Toolkit 2013 Setup Wizard starts.

3. Complete the Microsoft Deployment Toolkit 2013 Setup Wizard using the information in  the following table.  Accept the default values unless otherwise specified.

   |**On this wizard page**|**Do this**|
   |-|-|
   |**Welcome to the Microsoft Deployment Toolkit 2013 Setup Wizard**|Select **Next**.|
   |**End-User License Agreement**|Select **I accept the terms in the License Agreement**, and then select **Next**.|
   |**Custom Setup**|Select **Next**.|
   |**Ready to install Microsoft Deployment Toolkit 2013**|Select **Install**.|
   |**Installing Microsoft Deployment Toolkit 2013**|The progress for installing MDT is displayed.|
   |**Completing the Microsoft Deployment Toolkit 2013 Setup Wizard**|Select **Finish**.|

   The Microsoft Deployment Toolkit 2013 Setup Wizard finishes, and MDT is installed on WDG-MDT-01.

###  <a name="EnableConfigManagerConsole"></a> Step 2-2: Enable Configuration Manager Console Integration

Before you can use the Configuration Manager integration features of MDT, run the Configure ConfigMgr Integration script. This script copies the appropriate integration files to the folder in which Configuration Manager is installed. The script also adds Windows Management Instrumentation (WMI) classes for the new MDT custom actions. The classes are added by compiling a new Managed Object Format (.mof) file that contains the new class definitions.

 **To enable Configuration Manager console integration**

> [!NOTE]
>
> Ensure that the Configuration Manager console is closed while performing these steps.

1. Select **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then select **Configure ConfigMgr Integration**.

    The Configure ConfigMgr Integration Wizard starts.

2. Complete the Configure ConfigMgr Integration Wizard using the information in the following table. Accept the default values unless otherwise specified.

   |**On this wizard page**|**Do this**|
   |-|-|
   |**Options**|1. Verify that the **Install the MDT console extensions for System Center 2012 R2 Configuration Manager** check box is selected.<br>2. Verify that the **Add the MDT task sequence actions to a System Center 2012 R2 Configuration Manager server** check box is selected.<br>3. In **Site server name**, verify that the value is **WDG-MDT-01.mdt2013.corp.woodgrovebank.com**.<br>4. In **Site code**, verify that the value is **NYC**.<br>5. Select **Next**.|
   |**Confirmation**|Select **Finish**.|

   The Configure ConfigMgr Integration Wizard finishes, and MDT is integrated with Configuration Manager.

## Step 3: Create and Configure a Task Sequence to Create a Reference Computer

When you have prepared the MDT environment, create the reference computer. The reference computer is the template for deploying new images to the target computers. Configure this computer (WDG-REF-01) exactly as you will configure the target computers. You will then capture an image of the reference computer and deploy the image to the target computers.

 Create the reference computer, WDG-REF-01, by:

- Creating an MDT task sequence to deploy Windows 8.1 to the reference computer as described in [Step 3-1: Create an MDT Task Sequence for Deploying the Reference Computer](#CreateMDTTaskSequence)

- Selecting the distribution points for the new packages and images that the Create MDT Task Sequence Wizard creates as described in [Step 3-2: Select the Distribution Points for the New Packages and Images](#SelectDistroPoints)

- Adding the necessary device drivers to a new drive package and to the appropriate boot images as described in [Step 3-3: Add the Necessary Device Drivers](#AddDeviceDrivers)

- Enable monitoring of the MDT deployment process as described in [Step 3-4: Enable MDT Deployment Process Monitoring](#EnableMDTDeployProcess)

- Configuring the MDT configuration files for the reference computer—specifically, the CustomSettings.ini file—as described in [Step 3-5: Customize the MDT Configuration Files for the Reference Computer](#CustomizeMDTConfigFiles)

- Updating the Configuration Manager distribution points for the Custom Settings Files package as described in [Step 3-6: Update the Distribution Points for the Custom Settings Files Package](#UpdateDistroPoint)

- Customizing the task sequence for the reference computer as described in [Step 3-7: Customize the Task Sequence for the Reference Computer](#CustomizeTaskSequence)

###  <a name="CreateMDTTaskSequence"></a> Step 3-1: Create an MDT Task Sequence for Deploying the Reference Computer

Use the Create MDT Task Sequence Wizard in the Configuration Manager console to create task sequences in Configuration Manager that are integrated with MDT. MDT includes the Standard Client Task Sequence template, which you can use to deploy the reference computer.

 The Create MDT Task Sequence Wizard substitutes the packages and images selected for the placeholders in the task sequence templates. After completing the wizard, the new task sequence references the appropriate packages and images.

> [!NOTE]
>
> Always use the Create MDT Task Sequence Wizard to create task sequences based on the MDT task sequence templates. Although you can manually import the task sequence templates, Microsoft does not recommend this process.

#### To create a task sequence for deploying the reference computer

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Operating Systems/Task Sequences.

4. On the Ribbon, on the **Home** tab, in the **Task Sequences** group, select **Create MDT Task Sequence**.

    The Create MDT Task Sequence Wizard starts.

5. Complete the Create MDT Task Sequence Wizard using the information in the following table. Accept the default values unless otherwise specified.

   |        **On this wizard page**         |                                                                                                                                                                                                                                                                                                                                         **Do this**                                                                                                                                                                                                                                                                                                                                         |
   |----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |          **Choose Template**           |                                                                                                                                                                                                                                                                                                                  Select **Client Task Sequence**, and then select **Next**.                                                                                                                                                                                                                                                                                                                  |
   |      **Choose Template: General**      |                                                                                                                                                                                                                             1. In **Task sequence name**, type **Windows 8.1 Reference Deployment**.<br>2. In **Task sequence comments**, type **Task sequence for deploying Windows 8.1 to the reference computer (WDG-REF-01)**, and then select **Next**.                                                                                                                                                                                                                             |
   |      **Choose Template: Details**      |                                                                                                                                                                       1. Select **Join a workgroup**.<br>2. In **Workgroup**, type **WORKGROUP**.<br>3. In **User name**, type **Woodgrove Bank Employee**.<br>4. In **Organization name**, type **Woodgrove Bank**.<br>5. In **Product key**, type ***product_key*** (where *product_key* is the product key for Windows 8.1).<br>6. Select **Next**.                                                                                                                                                                        |
   | **Choose Template: Capture Settings**  | <ol><li>Select **This task sequence may be used to capture and image**.</li><li>In **Capture destination**, type **\\\WDG-MDT-01\Capture$\WDG-REF-01.wim**.</li><li>In **Capture account**, select **Set**.</li><li>Complete the **Windows User Account** dialog box by performing the following steps:<br><br> <ol><li>In **User name**, type **MDT2013\Administrator**.</li><li>In **Password** and **Confirm password**, type **P@ssw0rd**.</li></ol></li><li>Select **OK**.</li><li>Select **Next**.</li></ol> |
   |             **Boot Image**             |                                                                                                                                                                                                                                                         1. Select **Create a new boot image package**.<br>2. In **Package source folder to be created**, type **\\\WDG-MDT-01\Packages$\WINPE_Custom**, and then select **Next**.                                                                                                                                                                                                                                                         |
   |    **Boot Image: General Settings**    |                                                                                                                                                                                                                        1. In **Name**, type **Windows PE Custom**.<br>2. In **Version**, type **1.00**.<br>3. In **Comments**, type **Customized version of Windows PE to be used in deployment of reference and target computers**, and then select **Next**.                                                                                                                                                                                                                        |
   |        **Boot Image: Options**         |                                                                                                                                                                                                                                                                                                                 Under **Platform**, select **x64**, and then select **Next**.                                                                                                                                                                                                                                                                                                                 |
   |       **Boot Image: Components**       |                                                                                                                                                                                                                                                                                                                                       Select **Next**.                                                                                                                                                                                                                                                                                                                                       |
   |     **Boot Image: Customization**      |                                                                                                                                                                                                                                                                                                                                       Select **Next**.                                                                                                                                                                                                                                                                                                                                       |
   |            **MDT Package**             |                                                                                                                                                                                                                                              1. Select **Create a new Microsoft Deployment Toolkit Files package**.<br>2. In **Package source folder to be created**, type **\\\WDG-MDT-01\Packages$\MDT_Files**, and then select **Next**.                                                                                                                                                                                                                                               |
   |      **MDT Package: MDT Details**      |                                                                                                                                                                                                                                   1. In **Name**, type **MDT Files**.<br>2. In **Version**, type **1.00**.<br>3. In **Comments**, type **Provides access to MDT files during Configuration Manager deployment process**, and then select **Next**.                                                                                                                                                                                                                                    |
   |              **OS Image**              |                                                                                                                                                                                                             1. Select **Create a new OS install package**.<br>2. In **OS installation folder location**, type **\\\WDG-MDT-01\Source$\Windows_7**.<br>3. In **Package source folder to be created**, type **\\\WDG-MDT-01\Packages$\Windows_7**, and then select **Next**.                                                                                                                                                                                                             |
   |      **OS Image: Image Details**       |                                                                                                                                                                                                                                            1. In **Name**, type **Windows 8.1**.<br>2. In **Version**, type **1.00**.<br>3. In **Comments**, type **Windows 8.1 package used to deploy to reference computers**, and then select **Next**.                                                                                                                                                                                                                                            |
   |         **Deployment Method**          |                                                                                                                                                                                                                                                                                                                                       Select **Next**.                                                                                                                                                                                                                                                                                                                                       |
   |           **Client Package**           |                                                                                                                                                                                                                                                                                                          Select **Create a new ConfigMgr client package**, and then select **Next**.                                                                                                                                                                                                                                                                                                          |
   |            **USMT Package**            |                                                                                                                                                                                                                                                                1. Select **Create a new USMT package**.<br>2. In **Package source folder to be created**, type **\\\WDG-MDT-01\Packages$\USMT**, and then select **Next**.                                                                                                                                                                                                                                                                |
   |     **USMT Package: USMT Details**     |                                                                                                                                                                                                                                        1. In **Name**, type **USMT**.<br>2. In **Version**, type **1.00**.<br>3. In **Comments**, type **USMT files used to capture and restore user state migration information**, and then select **Next**.                                                                                                                                                                                                                                         |
   |          **Settings Package**          |                                                                                                                                                                                                                                                    1. Select **Create a new settings package**.<br>2. In **Package source folder to be created**, type **\\\WDG-MDT-01\Packages$\CustomSettings_Reference**, and then select **Next**.                                                                                                                                                                                                                                                    |
   | **Settings Package: Settings Details** |                                                                                                                                                                                                      1. In **Name**, type **MDT Reference Computer Custom Settings**.<br>2. In **Version**, type **1.00**.<br>3. In **Comments**, type **Configuration settings for MDT deployment process (such as CustomSettings.ini) for the reference computer**, and then select **Next**.                                                                                                                                                                                                       |
   |          **Sysprep Package**           |                                                                                                                                                                                                                                                                                                                                       Select **Next**.                                                                                                                                                                                                                                                                                                                                       |
   |              **Summary**               |                                                                                                                                                                                                                                                                          1. Review the information in the **Details** box that you provided while completing the previous wizard pages.<br>2. Select **Next**.                                                                                                                                                                                                                                                                           |
   |              **Progress**              |                                                                                                                                                                                                                                                                                                                  The progress for creating the task sequence is displayed.                                                                                                                                                                                                                                                                                                                  |
   |            **Confirmation**            |                                                                                                                                                                                                                                                                                                                                      Select **Finish**.                                                                                                                                                                                                                                                                                                                                      |

   The new task sequence appears in the preview pane.

###  <a name="SelectDistroPoints"></a> Step 3-2: Select the Distribution Points for the New Packages and Images

The Create MDT Task Sequence Wizard creates a number of packages and images. After these packages and images are created, select the distribution points from which the packages and images will be copied and available to target computers.

> [!NOTE]
>
> In this sample, there is only one distribution point (WDG-MDT-01). However, most production networks have multiple distribution points. When performing this step in a production environment, select the appropriate distribution points for the network.

#### To select the distribution points for software distribution packages
1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Operating Systems/Task Sequences.

4. In the preview pane, select **Windows 8.1 Reference Deployment**.

5. On the Ribbon, on the **Home** tab, in the **Deployment** group, select **Distribute Content**.

    The Distribute Content Wizard starts.

6. Complete the Distribute Content Wizard using the information in the following table. Accept default values unless otherwise specified.

   |     **On this wizard page**      |                                                                                                                                                                                  **Do this**                                                                                                                                                                                   |
   |----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |           **General**            |                                                                                                                                                                                Select **Next**.                                                                                                                                                                                 |
   |       **General: Content**       |                                                                                                                                                                                Select **Next**.                                                                                                                                                                                 |
   | **General: Content Destination** | 1. Select **Add**, and then select **Distribution Point**.<br>     The **Add Distribution Points** dialog box appears.<br>2. In the **Add Distribution Points** dialog box, select **WDG-MDT-01.mdt2013.corp.woodgrovebank.com**, and then select **OK**.<br>     WDG-MDT-01.corp.woodgrovebank.com appears in the **Content destination** list.<br>3. Select **Next**. |
   |           **Summary**            |                                                                                                                    1. Review the information in the **Details** box that you provided while completing the previous wizard pages.<br>2. Select **Next**.                                                                                                                    |
   |           **Progress**           |                                                                                                                                                            The progress for distributing the software is displayed.                                                                                                                                                            |
   |          **Completion**          |                                                                                                                                                                                Select **Close**.                                                                                                                                                                                |

7. Close all open windows and dialog boxes.

###  <a name="AddDeviceDrivers"></a> Step 3-3: Add the Necessary Device Drivers

When the MDT task sequence has been created, add any device drivers required for the reference computer (WDG-REF-01) to the Windows PE boot image and to the Windows 8.1 image. Add the device drivers in the Drivers node in the Configuration Manager console. Create a package that contains the device drivers, and inject the drivers into the custom Windows PE image created earlier in the process.

 After creating the package that contains the device drivers, select the distribution point to which the package will be deployed.

#### To add the necessary device drivers
1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Operating Systems/Drivers.

4. On the Ribbon, on the **Home** tab, in the **Create** group, select **Import Driver**.

    The Import New Driver Wizard starts.

5. Complete the Import New Driver Wizard using the information in the following table.  Accept the default values unless otherwise specified.

   |**On this wizard page**|**Do this**|
   |-|-|
   |**Locate Driver**|In **Source folder**, type **\\\WDG-MDT-01\Source$\Drivers**, and then select **Next**.|
   |**Locate Driver: Driver Details**|Select **Next**.|
   |**Locate Driver: Add Driver to Package**|<ol><li>Select **New Package**.</li><li>Complete the **New Driver Package** dialog box by performing the following steps:<br><br> <ol><li>In **Name**, type ***device_driver_name*** Package (where *device_driver_name* is a descriptive name for the device drivers).</li><li>In **Comment**, type **Device drivers that are necessary for the reference and target computers**.</li></ol></li><li>In **Driver package source**, type **\\\WDG-MDT-01\Packages$\Drivers**, and then select **OK**.</li><li>Select **Next**.</li></ol>|
   |**Locate Driver: Add Driver to Boot Images**|1. In the list of images, select the **Windows PE Custom** check box.<br>2. Select the **Update distribution points when finished** check box, and then select **Next**.|
   |**Summary**|1. Review the information in the **Details** box that you provided while completing the previous wizard pages.<br>2. Select **Next**.|
   |**Progress**|The progress for importing the device drivers is displayed.|
   |**Confirmation**|Select **Close**.|

#### To select the distribution points for the driver package
1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Operating Systems/Driver Packages.

4. In the preview pane, select ***device_driver_name*** **Package** (where *device_driver_name* is a descriptive name for the device drivers).

5. On the Ribbon, on the **Home** tab, in the **Deployment** group, select **Distribute Content**.

    The Distribute Content Wizard starts.

6. Complete the Distribute Content Wizard using the following information. Accept the default values unless otherwise specified.

   |     **On this wizard page**      |                                                                                                                                                                                        **Do this**                                                                                                                                                                                         |
   |----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |           **General**            |                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                       |
   |       **General: Content**       |                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                       |
   | **General: Content Destination** | 1. Select **Add**, and then select **Distribution Point**.<br>     The **Add Distribution Points** dialog box appears.<br>2. In the **Add Distribution Points** dialog box, select **\\\WDG-MDT-01.mdt2013.corp.woodgrovebank.com**, and then select **OK**.<br>     \\\WDGMDT01.mdt2013.corp.woodgrovebank.com appears in the **Content destination** list.<br>3. Select **Next**. |
   |           **Summary**            |                                                                                                                         1. Review the information in the **Details** box  that you provided while completing the previous wizard pages.<br>2. Select **Next**.                                                                                                                          |
   |           **Progress**           |                                                                                                                                                                  The progress for distributing the software is displayed.                                                                                                                                                                  |
   |          **Completion**          |                                                                                                                                                                                      Select **Close**.                                                                                                                                                                                      |

7. Close all open windows and dialog boxes.

###  <a name="EnableMDTDeployProcess"></a> Step 3-4: Enable MDT Deployment Process Monitoring

Prior to deploying the reference computer (WDG-REF-01) with the task sequence bootable media, enable MDT monitoring of the ZTI deployment process. You enable monitoring on the **Monitoring** tab on the deployment share **Properties** dialog box. Later in the process, you will monitor the ZTI deployment process using the Deployment Workbench or the **Get-MDTMonitorData** cmdlet.

 **To enable MDT monitoring of the ZTI deployment process**

1. Select **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then select **Deployment Workbench**.

2. In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares.

3. In the Actions pane, select **New Deployment Shares**.

    The New Deployment Share Wizard starts.

4. Complete the New Deployment Share Wizard using the following information

   |**On this wizard page**|**Do this**|
   |-|-|
   |**On this wizard page**|**Do this**|
   |**Path**|In **Deployment share path**, type **C:\DeploymentShare$**, and then select **Next**.|
   |**Share**|Select **Next**.|
   |**Descriptive Name**|Select **Next**.|
   |**Options**|Select **Next**.|
   |**Summary**|Select **Next**.|
   |**Progress**|The progress for creating the deployment share is displayed.|
   |**Confirmation**|Select **Finish**.|

   The New Deployment Share Wizard finishes, and the new deployment share—MDT Deployment Share (C:\DeploymentShare$)—appears in the details pane.

5. In the details pane, select **MDT Deployment Share (C:\DeploymentShare$)**.

6. In the Actions pane, select **Properties**.

    The **MDT Deployment Share (C:\DeploymentShare$) Properties** dialog box opens.

7. In the **MDT Deployment Share (C:\DeploymentShare$) Properties** dialog box, on the **Monitoring** tab, select the **Enable monitoring for this deployment share** check box, and then select **Apply**.

8. In the **MDT Deployment Share (C:\DeploymentShare$) Properties** dialog box, on the **Rules** tab, notice that the **EventService** property has been added to the CustomSettings.ini file, and then select **OK**.

   The **EventService** property is as follows:

   ```ini
   EventService=http://WDG-MDT-01:9800
   ```

9. Close all open windows and dialog boxes.

###  <a name="CustomizeMDTConfigFiles"></a> Step 3-5: Customize the MDT Configuration Files for the Reference Computer

When the MDT task sequence has been created, customize the MDT configuration files that provide the configuration settings for deploying Windows 8.1 to the target computer. Specifically, customize the CustomSettings.ini file.

 When the CustomSettings.ini file customization is finished, save the updated files to the source folder for the MDT Reference Computer Custom Settings package created earlier in the process (E:\Packages$\CustomSettings_Reference). Then, add the **DoCapture** and **EventService** properties and corresponding values to the CustomSettings.ini file so that the MDT deployment process captures an image of the reference computer (WDG-REF-01) after deploying Windows 8.1.

#### To customize the MDT configuration files for the reference computer

1. In Windows Explorer, go to E:\Packages$\CustomSettings_Reference, and then double-click **CustomSettings.ini**.

2. Open Microsoft Notepad, and then add the following lines to the end of the CustomSettings.ini file:

    ```ini
    DoCapture=YES
    EventService=http://WDG-MDT-01:9800
    ```

    Example of CustomSettings.ini file after adding the DoCapture property:

    ```ini
    [Settings]
    Priority=Default
    Properties=MyCustomProperty

    [Default]
    OSInstall=Y
    SkipCapture=YES
    SkipAdminPassword=NO
    SkipProductKey=YES
    DoCapture=YES
    EventService=http://WDG-MDT-01:9800
    ```

3. In Notepad, save the file, and then exit Notepad.

###  <a name="UpdateDistroPoint"></a> Step 3-6: Update the Distribution Points for the Custom Settings Files Package

When the source folder has been updated for the MDT Reference Computer Custom Settings package in Configuration Manager, update the distribution points for the MDT Reference Computer Custom Settings Files package. Updating the distribution points copies the updated version of the CustomSettings.ini file to the deployment shares specified in the package.

 **To update the distribution points for the Custom Settings package**

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Application Management/Packages.

4. In the preview pane, select **MDT Reference Computer Custom Settings**.

5. On the Ribbon, on the **Home** tab, in the **Deployment** group, select **Update Distribution Points**.

    The **Configuration Manager** dialog box opens, notifying you that you are going to update the package on all distribution points.

6. In the **Configuration Manager** dialog box, select **OK**.

7. Close all open windows and dialog boxes.

   Configuration Manager starts updating the distribution points with the latest versions of the CustomSettings.ini file. This process could take several minutes. Check the status of the package until the **Last Update** value of the package status has been updated to a recent date and time.

###  <a name="CustomizeTaskSequence"></a> Step 3-7: Customize the Task Sequence for the Reference Computer

For most deployments, the **Windows 8.1 Reference Deployment** task sequence created earlier in the process performs all the necessary steps without modification. In this sample, modify the task sequence to set the password for the local Administrator account to a known value. By default, the task sequence sets the password for the local Administrator account to a random value. Further customization of the task sequence may be required depending on the environment.

 **To customize the Windows 8.1 Reference Deployment task sequence**

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Operating Systems/Task Sequences.

4. In the preview pane, select **Windows 8.1 Reference Deployment**.

5. On the Ribbon, on the **Home** tab, in the **Task Sequence** group, select **Edit**.

    The **Windows 8.1 Reference Deployment Task Sequence Editor** dialog box opens.

6. In the **Windows 8.1 Reference Deployment Task Sequence Editor** dialog box, go to PostInstall/Apply Windows Settings.

7. On the **Properties** tab, select **Enable the account and specify the local administrator password**.

8. On the **Properties** tab, in **Password** and **Confirm Password**, type **P@ssw0rd**, and then select **Apply**.

9. Make any additional modifications to the task sequence that the environment requires, and then select **OK**.

10. Close all open windows and dialog boxes.

## Step 4: Deploy Windows 8.1 and Capture an Image of the Reference Computer

When you have created the task sequence to deploy Windows 8.1 to the reference computer and captured an image of the reference computer, start the task sequence. Create the operating system capture by using the Task Sequence Media Wizard in the Configuration Manager console.

 Deploy Windows 8.1 and capture an image of the reference computer by:

- Adding the reference computer to the Configuration Manager site database as described in [Step 4-1: Add the Reference Computer to the Configuration Manager Site Database](#AddRefComptoConfigDB)

- Creating a collection that contains the reference computer you just added as described in [Step 4-2: Create a Collection That Contains the Reference Computer](#CreateCollectionContainRefComp)

- Deploy the reference computer task sequence as described in [Step 4-3: Deploy the Reference Computer Task Sequence](#DeployRefCompTaskSeq)

- Using the Task Sequence Media Wizard to create a task sequence bootable media disk as described in [Step 4-4: Create the Task Sequence Bootable Media](#CreateTaskSeqBootMedia)

- Starting the reference computer with the task sequence bootable media disk as described in [Step 4-5: Start the Reference Computer with the Task Sequence Bootable Media](#StartRefCompwithTaskSeqBootMedia)

###  <a name="AddRefComptoConfigDB"></a> Step 4-1: Add the Reference Computer to the Configuration Manager Site Database

To deploy an operating system without stand-alone media to a new computer that Configuration Manager does not currently manage, add the new computer to the Configuration Manager site database prior to initiating the operating system deployment process. Configuration Manager can automatically discover computers on the network that have a Windows operating system installed; however, if the computer has no operating system installed, use the Import Computer Information Wizard to import the new computer information.

#### To add the reference computer to the Configuration Manager site database

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Assets and Compliance**.

3. In the Assets and Compliance workspace, go to Overview/Devices.

4. On the Ribbon, on the **Home** tab, in the **Create** group, select **Import Computer Information**.

    The Import Computer Information Wizard starts.

5. Complete the Import Computer Information Wizard using the following information. Accept the default values unless otherwise specified.

   |**On this wizard page**|**Do this**|
   |-|-|
   |**Select Source**|Select **Import single computer**, and then select **Next**.|
   |**Select Source: Single Computer**|1. In **Computer Name**, type **WDG-REF-01**.<br>2. In **MAC address**, type ***mac_address*** (where *mac_address* is the media access control [MAC] address of the primary network adapter for the reference computer, WDG-REF-01).<br>3. Select **Next**.|
   |**Select Source: Data Preview**|Select **Next**.|
   |**Select Source: Choose Target Collection**|Select **Next**.|
   |**Summary**|1. Review the information in the **Details** box  that you provided while completing the previous wizard pages.<br>2. Select **Next**.|
   |**Progress**|The progress for importing the computer is displayed.|
   |**Confirmation**|Select **Close**.|

   For more information on adding a new computer to the Configuration Manager site database, see the section, "To import computer information for a single computer," in the section "How to Deploy Operating Systems in Configuration Manager," in the Configuration Manager Documentation Library, which is installed with Configuration Manager.

###  <a name="CreateCollectionContainRefComp"></a> Step 4-2: Create a Collection That Contains the Reference Computer

In the Configuration Manager console, create a collection that includes the reference computer (WDG-REF-01). This computer collection is used later when advertising the task sequence created earlier in the process.

 **To create a collection that includes the reference computer**

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Assets and Compliance**.

3. In the Assets and Compliance workspace, go to Overview/Device Collections.

4. On the Ribbon, on the **Home** tab, in the **Create** group, select **Create**, and then select Create Device **Collection**.

    The Create Device Collection Wizard starts.

5. Complete the Create Device Collection Wizard using the following information. Accept the default values unless otherwise specified.

   |**On this wizard page**|**Do this**|
   |-|-|
   |**General**|<ol><li>In **Name**, type **Microsoft Deployment - Reference Computer**.</li><li>In **Comment**, type **Computer that is to be the reference computer for the target computers to be deployed**.</li><li>In **Limited Collection**, select **Browse**.<br><br>     The **Select Collection** dialog box appears. Complete the dialog box by performing the following steps:<br><br> <ol><li>In **Name**, select **All Systems**.</li><li>Select **OK**.</li></ol></li><li>Select **Next**.</li></ol>|
   |**Membership Rules**|<ol><li>Select **Add Rule**, and then select **Direct Rule**.<br><br>     The Create Direct Membership Rule Wizard starts.</li><li>Complete the Create Direct Membership Rule Wizard by performing the following steps:<br><br> <ol><li>On the **Welcome** page, select **Next**.</li><li>On the **Search for Resources** page, in **Resource class**, select **System Resource**; in **Attribute name**, select **Name**; in **Value**, type **WDG-REF-01**; and then select **Next**.</li><li>On the **Select Resources** page, select **WDG-REF-01**, and then select **Next**.</li><li>On the **Summary** page, select **Next**.</li><li>On the **Progress** page, view the progress for creating the new membership rule.</li><li>On the **Completion** page, select **Close**.</li></ol></li><li>Select **Next**.</li></ol>|
   |**Summary**|1. Review the information in the **Details** box  that you provided while completing the previous wizard pages.<br>2. Select **Next**.|
   |**Progress**|The progress for creating the device collection is displayed.|
   |**Completion**|Select **Close**.|

   For more information, see the section, "How to Create Collections in Configuration Manager," in the Configuration manager Documentation Library, which is installed with Configuration Manager.

###  <a name="DeployRefCompTaskSeq"></a> Step 4-3: Deploy the Reference Computer Task Sequence

In the Configuration Manager console, deploy the task sequence created earlier in the process to the device collection that includes the reference computer created earlier in the process.

#### To deploy the task sequence
1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Operating Systems/Task Sequences.

4. In the preview pane, select **Windows 8.1 Reference Deployment**.

5. On the Ribbon, on the **Home** tab, in the **Deployment** group, select **Deploy**.

    The Deploy Software Wizard starts.

6. Complete the Deploy Software Wizard using the following information. Accept the default values unless otherwise specified.

   |**On this wizard page**|**Do this**|
   |-|-|
   |**General**|1. In **Collection**, select **Browse**.<br>2. In the **Browse Collection** dialog box, select **Microsoft Deployment - Reference Computer**, and then select **OK**.<br>3. In **Comment**, type **Deploy Windows 8.1 to the reference computer and then capture an image of the reference computer**.<br>4. Select **Next**.|
   |**Deployment Settings**|1. In **Purpose**, select **Available**.<br>2. Select the **Make available to boot media and PXE** check box.<br>3. Select **Next**.|
   |**Deployment Settings: Schedule**|Select **Next**.|
   |**Deployment Settings: User Experience**|Select **Next**.|
   |**Deployment Settings: Alerts**|Select **Next**.|
   |**Deployment Settings: Distribution Points**|Select **Next**.|
   |**Summary**|1. Review the information in the **Details** box  that you provided while completing the previous wizard pages.<br>2. Select **Next**.|
   |**Progress**|The progress for deploying the task sequence is displayed.|
   |**Completion**|Select **Close**.|

   For more information, see the section, "How to Deploy a Task Sequence," in the Configuration manager Documentation Library, which is installed with Configuration Manager.

###  <a name="CreateTaskSeqBootMedia"></a> Step 4-4: Create the Task Sequence Bootable Media

To initiate the MDT process, provide a method for starting the computer with Windows PE and the necessary software by creating the task sequence bootable media disk. Use the Task Sequence Media Wizard in the Configuration Manager console to create bootable media for storage on a USB flash drive, CD, or DVD.

#### To create a task sequence bootable media disk

1. Select **Start**, point to **All Programs**, and then point to Microsoft System Center 2012. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Operating Systems/Task Sequences.

4. On the Ribbon, on the **Home** tab, in the **Create** group, select **Create Task Sequence Media**.

    The Create Task Sequence Media Wizard starts.

5. Complete the Create Task Sequence Media Wizard using the following information. Accept the default values unless otherwise specified.

   |         **On this wizard page**         |                                                                                                                                                                                                  **Do this**                                                                                                                                                                                                  |
   |-----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |          **Select Media Type**          |                                                                                                                                     1. Select **Bootable media**.<br>2. Clear the **Allow unattended operating system deployment** check box.<br>3. Select **Next**.                                                                                                                                     |
   | **Select Media Type: Media Management** |                                                                                                                                                                             Select **Site-based media**, and then select **Next**.                                                                                                                                                                              |
   |    **Select Media Type: Media Type**    |                                                                                                                                                     In **Media file**, type **\\\WDG-MDT-01\Capture$\CM2012_TS_Boot_Media.iso**, and then select **Next**.                                                                                                                                                     |
   |     **Select Media Type: Security**     |                                                                                                                                                      In **Password** and **Confirm password**, type **P@ssw0rd**, and then select **Next**.                                                                                                                                                       |
   |    **Select Media Type: Boot Image**    | 1. In **Boot image**, select **Browse**.<br>2. In the **Select a Boot Image** dialog box, select **Windows PE Custom**, and then select **OK**.<br>3. In **Distribution point**, select **\\\WDG-MDT-01.mdt2013.corp.woodgrovebank.com**, and then select **OK**.<br>4. In **Management point**, select **\\\WDG-MDT-01.mdt2013.corp.woodgrovebank.com**, and then select **OK**.<br>5. Select **Next**. |
   |  **Select Media Type: Customization**   |                                                                                                                                                                                                Select **Next**.                                                                                                                                                                                                |
   |               **Summary**               |                                                                                                                                   1. Review the information in the **Details** box  that you provided while completing the previous wizard pages.<br>2. Select **Next**.                                                                                                                                   |
   |              **Progress**               |                                                                                                                                                                        The progress for creating the task sequence media is displayed.                                                                                                                                                                        |
   |             **Completion**              |                                                                                                                                                                                               Select **Close**.                                                                                                                                                                                                |

   The wizard creates the CM2012_TS_Boot_Media.iso file in the WDG-MDT-01Capture$ shared folder.

6. If WDG-REF-01 is a physical computer, create a CD or DVD of the International Organization for Standardization (ISO) file. If WDG-REF-01 is a VM, start the VM directly from the ISO file.

   For more information on creating the task sequence bootable media disk, see the section, "How to Create Bootable Media," in the Configuration manager Documentation Library, which is installed with Configuration Manager.

###  <a name="StartRefCompwithTaskSeqBootMedia"></a> Step 4-5: Start the Reference Computer with the Task Sequence Bootable Media

Start the reference computer (WDG-REF-01) with the task sequence bootable media disk created earlier in the process. This medium starts Windows PE on the reference computer and initiates the MDT process. At the end of the MDT process, Windows 8.1 is deployed on the reference computer and an image of the reference computer is saved to \WDG-MDT-01\Capture$\WDG-REF-01.wim.

> [!NOTE]
>
> You can also initiate the MDT process by starting the target computer from Windows Deployment Services.

#### To start the reference computer with the task sequence bootable media

1. Start WDG-REF-01 with the task sequence bootable media created earlier in the process.

    Windows PE starts, and then the Task Sequence Wizard starts.

2. Complete the Task Sequence Wizard using the following information. Accept the default values unless otherwise specified.

   |         **On this wizard page**         |                                      **Do this**                                       |
   |-----------------------------------------|----------------------------------------------------------------------------------------|
   | **Welcome to the Task Sequence Wizard** |       In **Password**, type **P@ssw0rd**, and then select **Next**.        |
   |       **Select a Task Sequence**        | In the list box, select **Windows 8.1 Reference Deployment**, and then select **Next**. |

#### To monitor the reference computer deployment process using the Deployment Workbench, complete the following steps on WDG-MDT-01

1. On WDG-MDT-01, select **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then select **Deployment Workbench**.

2. In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares/MDT Deployment Share (C:\DeploymentShare$)/Monitoring.

3. In the details pane, view the deployment process for **WDG-REF-01**.

4. In the Actions pane, periodically select **Refresh**.

     The status of the deployment process is updated in the details pane. Continue to monitor the deployment process until the process is complete.

5. In the details pane, select **WDG-REF-01**.

6. In the Actions pane, select **Properties**.

     The **WDG-REF-01 Properties** dialog box is displayed.

7. In the **WDG-REF-01 Properties** dialog box, on the **Identity** tab, view the monitoring information provided about the deployment process as follows:

    |**Information**|**Description**|
    |-|-|
    |**ID**|Unique identifier for the computer being deployed.|
    |**Computer Name**|The name of the computer being deployed.|
    |**Deployment status**|The current status of the computer being deployed; the status can be one of the following:<br><br> -   **Running**. The task sequence is healthy and running.<br>-   **Failed**. The task sequence failed, and the deployment process was unsuccessful.<br>-   **Completed**. The task sequence has finished.<br>-   **Unresponsive**. The task sequence has not updated its status in the past four hours and is assumed to be nonresponsive.|
    |**Step**|The current task sequence step being run.|
    |**Progress**|The overall progress of the task sequence. The progress bar indicates how many task sequence steps have been run out of the total number of task sequence steps.|
    |**Start**|The time the deployment process started.|
    |**End**|The time the deployment process ended.|
    |**Elapsed**|The length of time the deployment process has been running or took to run if the deployment process has finished.|
    |**Errors**|The number of errors encountered during the deployment process.|
    |**Warnings**|The number of warnings encountered during the deployment process.|
    |**Remote Desktop**|This button allows you to establish a remote desktop connection with the computer being deployed using the Windows Remote Desktop feature. This method assumes that:<br><br> -   The target operating system is running and has remote desktop support enabled<br>-   **mstsc.exe** is in the path **Note:**  This button is always visible but may not be able to establish a remote desktop session if the monitored computer is running Windows PE, has not completed installation of the target operating system, or does not have the Remote Desktop feature enabled.|
    |**VM Connection**|This button allows you to establish a remote desktop connection to a VM running in HyperV®. This method assumes that:<br><br> -   The deployment is being performed to a VM running on Hyper-V<br>-   **vmconnect.exe** is located in the %ProgramFiles%\Hyper-V folder **Note:**  This button appears when ZTIGather.wsf detects that Hyper-V integration components are running on the monitored computer. Otherwise, this button will not be visible.|
    |**DaRT Remote Control**|This button allows you to establish a remote control session using the remote viewer feature in the Diagnostics and Recovery Toolkit (DaRT).<br><br> This method assumes that:<br><br> -   DaRT has been deployed to the target computer and is currently running<br>-   **DartRemoteViewer.exe** is located in the %ProgramFiles%\Microsoft DaRT 7\v7 folder **Note:**  This button appears when ZTIGather.wsf detects that DaRT is running on the monitored computer. Otherwise, this button will not be visible.|
    |**Automatically refresh this information every 10 seconds**|Check box that controls whether the information in the dialog box is automatically refreshed. If the check box is:<br><br> -   Selected, the information is refreshed every 10 seconds<br>-   Cleared, the information is not automatically refreshed and must be manually refreshed using the **Refresh Now** button|
    |**Refresh Now**|This button immediately refreshes the information displayed in the dialog box.|

8. In the **WDG-REF-01 Properties** dialog box, select **OK**.

9. Close the Deployment Workbench.

#### To monitor the reference computer deployment process using the Get-MDTMonitorData cmdlet, complete the following steps on WDG-MDT-01

1. On WDG-MDT-01, select **Start**, the select **Administrative Tools**, and then select **Windows PowerShell Modules**.

    The Windows PowerShell Modules command prompt opens.

2. Create a PowerShell drive that uses the MDT PowerShell provider by running the [New-PSDrive](/powershell/module/microsoft.powershell.management/new-psdrive) cmdlet as shown in the following example:

   ```powershell
   New-PSDrive -Name DS001 -PSProvider mdtprovider -Root d:\DeploymentShare$
   ```

3. View the MDT monitoring process by running the **Get-MDTMonitorData** cmdlet as shown in the following example:

   ```powershell
   Get-MDTMonitorData -Path DS001:
   ```

    This command returns the monitoring data collected by the MDT monitoring service running on the same computer that hosts the deployment share, as shown in the following example output:

   ```powershell
   Name               : WDG-REF-01
   PercentComplete    : 96
   Settings           :
   Warnings           : 0
   Errors             : 0
   DeploymentStatus   : 1
   StartTime          : 6/7/2012 6:45:39 PM
   EndTime            :
   ID                 : 1
   UniqueID           : 94a0830e-f2bb-421c-b1e0-6f86f9eb9fa1
   CurrentStep        : 130
   TotalSteps         : 134
   StepName           : Gather
   LastTime           : 6/7/2012 8:46:32 PM
   DartIP             :
   DartPort           :
   DartTicket         :
   VMHost             : XYL-DC-02
   VMName             : WDG-REF-01
   ComputerIdentities : {}
   ```

4. Close the Windows PowerShell console.

   If any problems occur during the deployment, consult the MDT document *Troubleshooting Reference*. When completed, a captured image of the reference computer should exist in \\\WDG-MDT-01\Capture$\WDG-REF-01.wim.

## Step 5: Create and Configure a Task Sequence to Deploy the Target Computer

After the task sequence to deploy the reference computer (WDG-REF-01) finishes, a captured image of the reference computer is stored in \\\WDG-MDT-01\Capture$\WDG-REF-01.wim. Now, create a task sequence that will deploy the captured image of the reference computer to the target computer (WDG-CLI-01). When this step is complete, you can deploy the captured image of the reference computer to the target computer.

 Create and configure a task sequence to deploy the target computer by:

- Importing the .wim file captured in the previous step into Configuration Manager using the Add Operating System Image Wizard as described in [Step 5-1: Import the Captured .wim File into Configuration Manager](#ImportCapturedwimFile)

- Using the Create MDT Task Sequence Wizard to create an MDT task sequence template to deploy the captured image of the reference computer to the target computer as described in [Step 5-2: Create an MDT Task Sequence to Deploy the Captured Image](#CreateMDTTaskSeqDeployCapturedImage)

- Selecting the distribution points for the new packages and images that the Create MDT Task Sequence Wizard creates as described in [Step 5-3: Select the Distribution Points for the New Packages and Images](#SelectDistroPointsNewPackagesImages)

- Customizing the MDT configuration files for the target computer—specifically, the CustomSettings.ini file—as described in [Step 5-4: Customize the MDT Configuration Files](#CustomizetheMDTConfigFiles)

- Updating the Configuration Manager distribution points for the Custom Settings package as described in [Step 5-5: Update the Distribution Points for the Custom Settings Package](#UpdateDistroPointsforCustomSettings)

- Customizing the task sequence for the target computer as described in [Step 5-6: Customize the Task Sequence for the Target Computer](#CustomizeTaskSequenceTargetComputer)

###  <a name="ImportCapturedwimFile"></a> Step 5-1: Import the Captured .wim File into Configuration Manager

After the image of the reference computer (WDG-REF-01) is captured in to the .wim file, import the captured .wim file into Configuration Manager. Import the captured .wim file into the Operating System Images node using the Add Operating System Image Wizard.

 The captured .wim contains two images, one for each partition on the reference computer. Identify which of the images has the captured Windows 8.1 operating system by checking the image description containing *Windows 8.1*. You will use the image index when you create the task sequence for deploying the captured image to the target computer.

 **To import the captured .wim file into Configuration Manager**

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Operating Systems/Operating System Images.

4. On the Ribbon, in the **Create** group, select **Add Operating System Image**.

     The Add Operating System Image Wizard starts.

5. Complete the Add Operating System Image Wizard using the following information. Accept the default values unless otherwise specified.

    |**On this wizard page**|**Do this**|
    |-|-|
    |**On this wizard page**|**Do this**|
    |**Data Source**|In **Path**, type **\\\WDG-MDT-01\Capture$\WDG-REF-01.wim**, and then select **Next**.|
    |**General**|1. In **Name**, type **Windows 8.1 Reference Image**.<br><br> 1. In **Version**, type **1.00**.<br><br> 1. In **Comments**, type **Windows 8.1 captured image of reference computer (WDG-REF-01) used to deploy to target computers**, and then select **Next**.|
    |**Summary**|1. Review the information in the **Details** box  that you provided while completing the previous wizard pages.<br>2. Select **Next**.|
    |**Progress**|The progress for importing the operating system image is displayed.|
    |**Completion**|Select **Close**.|

6. In the preview pane, select **Windows 8.1 Reference Image**.

7. In the preview pane, select the **Details** tab.

     The list of operating system partitions captured in the .wim is displayed. The image index that contains Windows 8.1 is the image index you will specify later during the Create MDT Task Sequence Wizard.

8. Record the image index that contains Windows 8.1.

    > [!TIP]
    >
    > For the purposes of this example, image index 2 should have the Windows 8.1 operating system.

###  <a name="CreateMDTTaskSeqDeployCapturedImage"></a> Step 5-2: Create an MDT Task Sequence to Deploy the Captured Image

After the image is captured, create a task sequence to deploy the captured image of the reference computer (WDG-REF-01) to the target computer (WDG-CLI-01). Most of the packages needed for this task sequence were created earlier in the process. However, you must create a new MDT Custom Settings package that has the proper configuration settings for the target computer and creates an operating system image of the captured image of the reference computer.

#### To create a task sequence template to deploy the captured image to the target computer

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Operating Systems/Task Sequences.

4. On the Ribbon, on the **Home** tab, in the **Task Sequences** group, select **Create MDT Task Sequence**.

    The Create MDT Task Sequence Wizard starts.

5. Complete the Create MDT Task Sequence Wizard using the following information. Accept the default values unless otherwise specified.

   |        **On this wizard page**         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                        **Do this**                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |          **Choose Template**           |                                                                                                                                                                                                                                                                                                                                                                                                                                                 Select **Client Task Sequence**, and then select **Next**.                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |      **Choose Template: General**      |                                                                                                                                                                                                                                                                                                                                                    1. In **Task sequence name**, type **Windows 8.1 Target Deployment**.<br>2. In **Task sequence comments**, type **Task sequence for deploying captured reference computer image to the target computer (WDG-CLI-01)**, and then select **Next**.                                                                                                                                                                                                                                                                                                                                                     |
   |      **Choose Template: Details**      | <ol><li>Select **Join a domain**.</li><li>In **Domain**, type **mdt2013.corp.woodgrovebank.com**.</li><li>In **Account**, select **Set**, and then complete the **Windows User Account** dialog box by performing the following steps:<br><br> <ol><li>In **User name**, type **MDT2013\Administrator**.</li><li>In **Password** and **Confirm password**, type **P@ssw0rd**.</li><li>Select **OK**.</li></ol></li><li>In **User name**, type **Woodgrove Bank Employee**.</li><li>In **Organization name**, type **Woodgrove Bank**.</li><li>In **Product key**, type **<em>product_key</em>** (where <em>product_key</em> is the product key for Windows 8.1).</li><li>Select **Next**.</li></ol> |
   | **Choose Template: Capture Settings**  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   |             **Boot Image**             |                                                                                                                                                                                                                                                                                                                                                                               1. In **Specify an existing boot image package**, select **Browse**.<br>2. In **Select a Package** dialog box, select **Windows PE Custom**, and then select **OK**.<br>3. Select **Next**.                                                                                                                                                                                                                                                                                                                                                                               |
   |            **MDT Package**             |                                                                                                                                                                                                                                                                                                                                                                     1. In **Specify an existing Microsoft Deployment Toolkit Files package**, select **Browse**.<br>2. In the **Select a Package** dialog box, select **MDT Files**, and then select **OK**.<br>3. Select **Next**.                                                                                                                                                                                                                                                                                                                                                                     |
   |              **OS Image**              |                                                                                                                                                                                                                                                                                                                                                    1. Select **Specify an existing OS image**.<br>2. In **Specify an existing OS image**, select **Browse**.<br>3. In the **Select a Package** dialog box, select **Windows 8.1 Reference Image**, and then select **OK**.<br>4. Select **Next**.                                                                                                                                                                                                                                                                                                                                                     |
   |      **OS Image: OS Image Index**      |                                                                                                                                                                                                                                                  1. In **The selected operating system image (WIM) file contains multiple images**. **Specify which image you would like to deploy**, select ***image_index*** (where *image_index* is the image index of the image that contains Windows 8.1, which was identified in the section [Step 5-1: Import the Captured .wim File into Configuration Manager](#ImportCapturedwimFile); for the purposes of this guide, select **2**).<br>2. Select **Next**.                                                                                                                                                                                                                                                  |
   |         **Deployment Method**          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   |           **Client Package**           |                                                                                                                                                                                                                                                                                                                                                           1. In **Specify an existing ConfigMgr client package**, select **Browse**.<br>2. In the **Select a Package** dialog box, select **Microsoft Configuration Manager Client Upgrade**, and then select **OK**.<br>3. Select **Next**.                                                                                                                                                                                                                                                                                                                                                            |
   |            **USMT Package**            |                                                                                                                                                                                                                                                                                                                                                                                      1. In **Specify an existing USMT package**, select **Browse**.<br>2. In the **Select a Package** dialog box, select **USMT**, and then select **OK**.<br>3. Select **Next**.                                                                                                                                                                                                                                                                                                                                                                                       |
   |          **Settings Package**          |                                                                                                                                                                                                                                                                                                                                                                                     1. Select **Create a new settings package**.<br>2. In **Package source folder to be created**, type **\\\WDG-MDT-01\Packages$\CustomSettings_Target**, and then select **Next**.                                                                                                                                                                                                                                                                                                                                                                                     |
   | **Settings Package: Settings Details** |                                                                                                                                                                                                                                                                                                                                         1. In **Name**, type **MDT Target Computer Custom Settings**.<br>2. In **Version**, type **1.00**.<br>3. In **Comments**, type **Configuration settings for MDT deployment process (such as CustomSettings.ini) for the target computer**, and then select **Next**.                                                                                                                                                                                                                                                                                                                                         |
   |          **Sysprep Package**           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                      Select **Next**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   |              **Summary**               |                                                                                                                                                                                                                                                                                                                                                                                                         1. Review the information in the **Details** box  that you provided while completing the previous wizard pages.<br>2. Select **Next**.                                                                                                                                                                                                                                                                                                                                                                                                          |
   |              **Progress**              |                                                                                                                                                                                                                                                                                                                                                                                                                                                 The progress for creating the task sequence is displayed.                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |            **Confirmation**            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                     Select **Finish**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

   The list of task sequences is displayed. The task sequence that you just created (Windows 8.1 Target Deployment) is listed in the list of task sequences.

###  <a name="SelectDistroPointsNewPackagesImages"></a> Step 5-3: Select the Distribution Points for the New Packages and Images

The Create MDT Task Sequence Wizard creates a number of packages and images. After these packages and images are created, select the distribution points from which the packages and images will be copied and available to target computers.

> [!NOTE]
>
> In this sample, there is only one distribution point (WDG-MDT-01). However, most production networks have multiple distribution points. When performing this step in a production environment, select the appropriate distribution points for the network.

#### To select the distribution points for software distribution packages

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Operating Systems/Task Sequences.

4. In the preview pane, select **Windows 8.1 Target Deployment**.

5. On the Ribbon, on the **Home** tab, in the **Deployment** group, select **Distribute Content**.

     The Distribute Content Wizard starts.

6. Complete the Distribute Content Wizard using the following information. Accept default values unless otherwise specified.

    |**On this wizard page**|**Do this**|
    |-|-|
    |**General**|Select **Next**.|
    |**Content**|Select **Next**.|
    |**General: Content**|Select **Next**.|
    |**General: Content Destination**|1. Select **Add**, and then select **Distribution Point**.<br>     The **Add Distribution Points** dialog box appears.<br>2. In the **Add Distribution Points** dialog box, select **\\\WDGMDT01.mdt2013.corp.woodgrovebank.com**, and then select **OK**.<br>     \\\WDGMDT01.mdt2013.corp.woodgrovebank.com appears in the **Content destination** list.<br>3. Select **Next**.|
    |**Summary**|1. Review the information in the **Details** box  that you provided while completing the previous wizard pages.<br>2. Select **Next**.|
    |**Progress**|The progress for distributing the software is displayed.|
    |**Completion**|Select **Close**.|

7. Close all open windows and dialog boxes.

###  <a name="CustomizetheMDTConfigFiles"></a> Step 5-4: Customize the MDT Configuration Files

When the task sequence for the target computer has been created, customize the MDT configuration files that provide the configuration settings for deploying Windows 8.1 to the target computer—specifically, CustomSettings.ini.

 When the CustomSettings.ini file has been customized, save the updated files to the source folder for the MDT Custom Settings package created earlier in the process (E:\Packages$\CustomSettings_Target).

#### To customize the MDT configuration files for the target computer

1. In Windows Explorer, go to E:\Packages$\CustomSettings_Target folder, and then double-click **CustomSettings.ini**.

2. Open Notepad, and then add the following lines to the CustomSettings.ini file:

    ```ini
    EventService=http://WDG-MDT-01:9800
    ```

     This setting will configure monitoring of the target computer deployment.

    > [!NOTE]
    >
    > Make any other changes that are required by your environment.

     **Example of the edited CustomSettings.ini File:**

    ```ini
    [Settings]
    Priority=Default
    Properties=MyCustomProperty

    [Default]
    OSInstall=Y
    SkipCapture=YES
    SkipAdminPassword=NO
    SkipProductKey=YES
    EventService=http://WDG-MDT-01:9800

    ```

3. Save the file, and then close Notepad.

###  <a name="UpdateDistroPointsforCustomSettings"></a> Step 5-5: Update the Distribution Points for the Custom Settings Package

When the source folder has been updated for the MDT Target Computer Custom Settings package in Configuration Manager, update the distribution points for the MDT Target Computer Custom Settings package. Updating the distribution points copies the updated version of the CustomSettings.ini file to the deployment shares specified in the package.

#### To update the distribution points for the Custom Settings package

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Application Management/Packages.

4. In the preview pane, select **MDT Target Computer Custom Settings**.

5. On the Ribbon, on the **Home** tab, in the **Deployment** group, select **Update Distribution Points**.

     The **Configuration Manager** dialog box opens, notifying you that you are going to update the package on all distribution points.

6. In the **Configuration Manager** dialog box, select **OK**.

7. Close all open windows and dialog boxes.

###  <a name="CustomizeTaskSequenceTargetComputer"></a> Step 5-6: Customize the Task Sequence for the Target Computer

For most deployments, the Windows 8.1 Target Deployment task sequence created earlier in the process performs all the necessary steps without modification. In this sample, modify the task sequence template to set the password for the local Administrator account to a known value. (By default, the task sequence sets the password for the local Administrator account to a random value.) The task sequence may require further customization depending on the environment.

#### To customize the Windows 8.1 Target Deployment task sequence

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Operating Systems/Task Sequences.

4. In the preview pane, select **Windows 8.1 Reference Deployment**.

5. On the Ribbon, on the **Home** tab, in the **Task Sequence** group, select **Edit**.

    The **Windows 8.1 Reference Deployment Task Sequence Editor** dialog box opens.

6. In the **Windows 8.1 Reference Deployment Task Sequence Editor** dialog box, go to PostInstall/Apply Windows Settings.

7. On the **Properties** tab, select **Enable the account and specify the local administrator password**.

8. On the **Properties** tab, in **Password** and **Confirm Password**, type **P@ssw0rd**, and then select **Apply**.

9. Make any additional modifications to the task sequence that the environment requires, and then select **OK**.

10. Close all open windows and dialog boxes.


## Step 6: Deploy the Captured Image of the Reference Computer to the Target Computer

When you have captured the image of the reference computer and created and configured the task sequence, deploy the captured image. Configure MDT to provide all the necessary configuration settings to deploy to the target computer. After initiating the deployment process, the image of the reference computer running Windows 8.1 is automatically deployed to the target computer and configured with the settings defined.

 Deploy the captured image by:

- Adding the target computer to the Configuration Manager site database as described in [Step 6-1: Add the Target Computer to the Configuration Manager Site Database](#AddTargetComptoConfigManager)

- Creating a computer collection that includes the target computer as described in [Step 6-2: Create a Computer Collection That Includes the Target Computer](#CreateComputerCollectionIncludesTarget)

- Deploying the task sequence created earlier in the process as described in [Step 6-3: Deploy the Target Computer Task Sequence](#DeployTargetComputerTaskSequence)

- Starting the target computer with the task sequence bootable media as described in [Step 6-4: Start the Target Computer with the Task Sequence Bootable Media](#StartTargetComputerTaskSequenceMedia)

###  <a name="AddTargetComptoConfigManager"></a> Step 6-1: Add the Target Computer to the Configuration Manager Site Database

To deploy an operating system without stand-alone media to a new computer that Configuration Manager does not currently manage, add the new computer to the Configuration Manager site database prior to initiating the operating system deployment process. Configuration Manager can automatically discover computers on the network that have a Windows operating system installed; however, if the computer has no operating system installed, use the Import Computer Information Wizard to import the new computer information.

#### To add the target computer to the Configuration Manager site database

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Assets and Compliance**.

3. In the Assets and Compliance workspace, go to Overview/Devices.

4. On the Ribbon, on the **Home** tab, in the **Create** group, select **Import Computer Information**.

    The Import Computer Information Wizard starts.

5. Complete the Import Computer Information Wizard using the following information. Accept the default values unless otherwise specified.

   |**On this wizard page**|**Do this**|
   |-|-|
   |**Select Source**|Select **Import single computer**, and then select **Next**.|
   |**Select Source: Single Computer**|1. In **Computer Name**, type **WDG-CLI-01**.<br>2. In **MAC address**, type ***mac_address*** (where *mac_address* is the MAC address of the primary network adapter for the target computer, WDG-CLI-01).<br>3. Select **Next**.|
   |**Select Source: Data Preview**|Select **Next**.|
   |**Select Source: Choose Target Collection**|Select **Next**.|
   |**Summary**|1. Review the information in the **Details** box  that you provided while completing the previous wizard pages.<br>2. Select **Next**.|
   |**Progress**|The progress for importing the computer is displayed.|
   |**Confirmation**|Select **Close**.|

   For more information on adding a new computer to the Configuration Manager site database, see the section, "To import computer information for a single computer," in the section, "How to Deploy Operating Systems in Configuration Manager," in the Configuration manager Documentation Library, which is installed with Configuration Manager.

###  <a name="CreateComputerCollectionIncludesTarget"></a> Step 6-2: Create a Computer Collection That Includes the Target Computer

In the Configuration Manager console, create a collection that includes the target computer (WDG-CLI-01). You use this computer collection later when advertising the task sequence created earlier in the process.

#### To create a computer collection that includes the target computer

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Assets and Compliance**.

3. In the Assets and Compliance workspace, go to Overview/Device Collections.

4. On the Ribbon, on the **Home** tab, in the **Create** group, select **Create Device Collection**.

    The Create Device Collection Wizard starts.

5. Complete the Create Device Collection Wizard using the following information. Accept the default values unless otherwise specified.

   |**On this wizard page**|**Do this**|
   |-|-|
   |**On this wizard page**|**Do this**|
   |**General**|<ol><li>In **Name**, type **Microsoft Deployment - Batch 01**.</li><li>In **Comment**, type **Computers that are to be included in the first batch of computers deployed**.</li><li>In **Limited Collection**, select **Browse**.<br><br>     The **Select Collection** dialog box appears. Complete the dialog box by performing the following steps:<br><br> <ol><li>In the **Select Collection** dialog box, in **Name**, select **All Systems**.</li><li>Select **OK**.</li></ol></li><li>Select **Next**.</li></ol>|
   |**Membership Rules**|<ol><li>Select **Add Rule**, and then select **Direct Rule**.<br><br>     The Create Direct Membership Rule Wizard starts.</li><li>Complete the Create Direct Membership Rule Wizard by performing the following steps:<br><br> <ol><li>On the **Welcome** page, select **Next**.</li><li>On the **Search for Resources** page, in **Resource class**, select **System Resource**; in **Attribute name**, select **Name**; in **Value**, type **WDG-CLI-01**; and then select **Next**.</li><li>On the **Select Resources** page, select **WDG-CLI-01**, and then select **Next**. **Note:**          The process for adding the target computer (WDG-CLI-01) to All Systems can take a few minutes to complete. If WDG-CLI-01 does not appear in the list, repeat steps b and c until WDGCLI01 appears.</li><li>On the **Summary** page, select **Next**.</li><li>On the **Completion** page, select **Close**.</li></ol></li><li>Select **Next**.</li></ol>|
   |**Summary**|1. Review the information in the **Details** box  that you provided while completing the previous wizard pages.<br>2. Select **Next**.|
   |**Progress**|The progress for creating the device collection is displayed.|
   |**Completion**|Select **Close**.|

   For more information, see the section, "How to Create Collections in Configuration Manager," in the Configuration manager Documentation Library, which is installed with Configuration Manager.

###  <a name="DeployTargetComputerTaskSequence"></a> Step 6-3: Deploy the Target Computer Task Sequence

In the Configuration Manager console, deploy the task sequence created earlier in the process for the target computers. Deploy the task sequence to the collection of target computers created earlier in the process.

#### To deploy the task sequence

1. Select **Start**, point to **All Programs**, and then point to **Microsoft System Center 2012**. Point to **Configuration Manager**, and then select **Configuration Manager Console**.

2. In the Configuration Manager console, in the navigation pane, select **Software Library**.

3. In the Software Library workspace, go to Overview/Operating Systems/Task Sequences.

4. In the preview pane, select **Windows 8.1 Target Deployment**.

5. On the Ribbon, on the **Home** tab, in the **Deployment** group, select **Deploy**.

    The Deploy Software Wizard starts.

6. Complete the Deploy Software Wizard using the following information.  Accept the default values unless otherwise specified.

   |**On this wizard page**|**Do this**|
   |-|-|
   |**General**|1. In **Collection**, select **Browse**.<br>2. In the **Browse Collection** dialog box, select **Microsoft Deployment - Batch 01**, and then select **OK**.<br>3. In **Comment**, type **Deploy Windows 8.1 to the first batch of target computers**.<br>4. Select **Next**.|
   |**Deployment Settings**|1. In **Purpose**, select **Available**.<br>2. Select the **Make available to boot media and PXE** check box.<br>3. Select **Next**.|
   |**Deployment Settings: Schedule**|Select **Next**.|
   |**Deployment Settings: User Experience**|Select **Next**.|
   |**Deployment Settings: Alerts**|Select **Next**.|
   |**Deployment Settings: Distribution Points**|Select **Next**.|
   |**Summary**|1. Review the information in the **Details** box  that you provided while completing the previous wizard pages.<br>2. Select **Next**.|
   |**Progress**|The progress for deploying the task sequence is displayed.|
   |**Completion**|Select **Close**.|

   For more information, see the section, "How to Deploy a Task Sequence," in the Configuration manager Documentation Library, which is installed with Configuration Manager.

###  <a name="StartTargetComputerTaskSequenceMedia"></a> Step 6-4: Start the Target Computer with the Task Sequence Bootable Media

Start the target computer (WDG-CLI-01) with the task sequence bootable media created earlier in the process. This medium starts Windows PE on the reference computer and initiates the MDT process. At the end of the MDT process, Windows 8.1 is deployed on the target computer.

> [!NOTE]
>
> You can also initiate the MDT process by starting the target computer from Windows Deployment Services.

#### To start the target computer with the task sequence bootable media

1. Start WDG-CLI-01 with the task sequence bootable media created earlier in the process.

    Windows PE starts, and then the Task Sequence Wizard starts.

2. Complete the Task Sequence Wizard using the following information. Accept the default values unless otherwise specified.

   |         **On this wizard page**         |                                     **Do this**                                     |
   |-----------------------------------------|-------------------------------------------------------------------------------------|
   | **Welcome to the Task Sequence Wizard** |      In **Password**, type **P@ssw0rd**, and then select **Next**.      |
   |       **Select a Task Sequence**        | In the list box, select **Windows 8.1 Target Deployment**, and then select **Next**. |

#### To monitor the reference computer deployment process using the Deployment Workbench

1. On WDG-MDT-01, select **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then select **Deployment Workbench**.

2. In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares/MDT Deployment Share (C:\DeploymentShare$)/Monitoring.

3. In the details pane, view the deployment process for **WDG-CLI-01**.

4. In the Actions pane, periodically select **Refresh**.

     The status of the deployment process is updated in the details pane. Continue to monitor the deployment process until the process is complete.

5. In the details pane, select **WDG-CLI-01**.

6. In the Actions pane, select **Properties**.

     The **WDG-CLI-01 Properties** dialog box is displayed.

7. In the **WDG-CLI-01 Properties** dialog box, on the **Identity** tab, view the monitoring information provided about the deployment process as described in the following table:

    |**Information**|**Description**|
    |-|-|
    |**ID**|Unique identifier for the computer being deployed.|
    |**Computer Name**|The name of the computer being deployed.|
    |**Deployment status**|The current status of the computer being deployed; the status can be one of the following:<br><br> -   **Running**. The task sequence is healthy and running.<br>-   **Failed**. The task sequence failed, and the deployment process was unsuccessful.<br>-   **Completed**. The task sequence has finished.<br>-   **Unresponsive**. The task sequence has not updated its status in the past four hours and is assumed to be nonresponsive.|
    |**Step**|The current task sequence step being run.|
    |**Progress**|The overall progress of the task sequence. The progress bar indicates how many task sequence steps have been run out of the total number of task sequence steps.|
    |**Start**|The time the deployment process started.|
    |**End**|The time the deployment process ended.|
    |**Elapsed**|The length of time the deployment process has been running or took to run if the deployment process has finished.|
    |**Errors**|The number of errors encountered during the deployment process.|
    |**Warnings**|The number of warnings encountered during the deployment process.|
    |**Remote Desktop**|This button allows you to establish a remote desktop connection with the computer being deployed using the Windows Remote Desktop feature. This method assumes that:<br><br> -   The target operating system is running and has remote desktop support enabled<br>-   **mstsc.exe** is in the path **Note:**  This button is always visible but may not be able to establish a remote desktop session if the monitored computer is running Windows PE, has not completed installation of the target operating system, or does not have the Remote Desktop feature enabled.|
    |**VM Connection**|This button allows you to establish a remote desktop connection to a VM running in Hyper-V. This method assumes that:<br><br> -   The deployment is being performed to a VM running on Hyper-V<br>-   **vmconnect.exe** is located in the %ProgramFiles%\Hyper-V folder **Note:**  This button appears when ZTIGather.wsf detects that Hyper-V integration components are running on the monitored computer. Otherwise, this button will not be visible.|
    |**DaRT Remote Control**|This button allows you to establish a remote control session using the remote viewer feature in the Diagnostics and Recovery Toolkit (DaRT).<br><br> This method assumes that:<br><br> -   DaRT has been deployed to the target computer and is currently running<br>-   **DartRemoteViewer.exe** is located in the %ProgramFiles%\Microsoft DaRT 7\v7 folder **Note:**  This button appears when ZTIGather.wsf detects that DaRT is running on the monitored computer. Otherwise, this button will not be visible.|
    |**Automatically refresh this information every 10 seconds**|Check box that controls whether the information in the dialog box is automatically refreshed. If the check box is:<br><br> -   Selected, the information is refreshed every 10 seconds<br>-   Cleared, the information is not automatically refreshed and must be manually refreshed using the **Refresh Now** button|
    |**Refresh Now**|This button immediately refreshes the information displayed in the dialog box.|

8. In the **WDG-REF-01 Properties** dialog box, select **OK**.

9. Close the Deployment Workbench.

#### To monitor the reference computer deployment process using the Get-MDTMonitorData cmdlet

1. On WDG-MDT-01, select **Start**, point to **Administrative Tools**, and then select **Windows PowerShell Modules**.The Windows PowerShell Modules command prompt opens.

2. Create a PowerShell drive that uses the MDT PowerShell provider by running the [New-PSDrive](/powershell/module/microsoft.powershell.management/new-psdrive) cmdlet as shown in the following example:

   ```powershell
   New-PSDrive -Name DS001 -PSProvider mdtprovider -Root d:\DeploymentShare$
   ```

3. View the MDT monitoring process by running the **Get-MDTMonitorData** cmdlet as shown in the following example:

   ```powershell
   Get-MDTMonitorData -Path DS001:
   ```

    This command returns the monitoring data collected by the MDT monitoring service running on the same computer that hosts the deployment share as shown in the following example output:

   ```powershell
   Name               : WDG-REF-01
   PercentComplete    : 96
   Settings           :
   Warnings           : 0
   Errors             : 0
   DeploymentStatus   : 1
   StartTime          : 6/7/2012 6:45:39 PM
   EndTime            :
   ID                 : 1
   UniqueID           : 94a0830e-f2bb-421c-b1e0-6f86f9eb9fa1
   CurrentStep        : 130
   TotalSteps         : 134
   StepName           : Gather
   LastTime           : 6/7/2012 8:46:32 PM
   DartIP             :
   DartPort           :
   DartTicket         :
   VMHost             : XYL-DC-02
   VMName             : WDG-REF-01
   ComputerIdentities : {}

   Name               : WDG-CLI-01
   PercentComplete    : 26
   Settings           :
   Warnings           : 0
   Errors             : 0
   DeploymentStatus   : 1
   StartTime          : 6/7/2012 3:07:13 AM
   EndTime            :
   ID                 : 2
   UniqueID           : 94a0830e-f2bb-421c-b1e0-6f86f9eb9fa1
   CurrentStep        : 49
   TotalSteps         : 134
   StepName           : Capture Network Settings using MDT
   LastTime           : 6/7/2012 3:08:32 AM
   DartIP             :
   DartPort           :
   DartTicket         :
   VMHost             :
   VMName             :
   ComputerIdentities : {}
   ```

4. Close the Windows PowerShell console.

   If any problems occur during the deployment, consult the MDT document *Troubleshooting Reference*. When successfully completed, the target computer is running a Windows 8.1 operating system configured like the reference computer.