---
title: Set up your lab
titleSuffix: Configuration Manager
description: Set up a lab for evaluating Configuration Manager with simulated real-life activities.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
manager: apoorvseth
ms.author: banreetkaur
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Set up a Configuration Manager lab

*Applies to: Configuration Manager (current branch)*

Following the guidance in this topic will enable you to set up a lab for evaluating Configuration Manager with simulated real-life activities.  

> [!NOTE]
> Microsoft offers a pre-configured version of this lab using an evaluation version of Configuration Manager. For more information, see [Microsoft Intune and Configuration Manager evaluation lab kit](https://www.microsoft.com/evalcenter/evaluate-mem-evaluation-lab-kit). 

##  <a name="BKMK_LabCore"></a> Core components  
 Setting up your environment for Configuration Manager requires some core components to support the installation of Configuration Manager.    

-   **The lab environment uses Windows Server 2012 R2**, into which we will install Configuration Manager.  

     You can download an evaluation version of Windows Server 2012 R2 from the [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).  

    Consider modifying or disabling Internet Explorer Enhanced Security Configuration in order to more easily access some of the downloads referenced throughout the course of these exercises. For more information, see [Internet Explorer: Enhanced Security Configuration](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10)).  

-   **The lab environment uses SQL Server 2012 SP2** for the site database.  

     You can download an evaluation version of SQL Server 2012 from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=43340).  

     SQL Server has [Supported versions of SQL Server](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions) that must be met for use with Configuration Manager.  

    -   Configuration Manager requires a 64-bit version of SQL Server to host the site database.  

    -   **SQL_Latin1_General_CP1_CI_AS** as the **SQL Collation** class.  

    -   **Windows authentication**, [rather than SQL Server authentication](/sql/relational-databases/security/choose-an-authentication-mode), is required.  

    -   A dedicated **SQL Server instance** is required.  

    -   Do not limit the **system addressable memory** for SQL Server.  

    -   Configure the **SQL Server service account** to run using a low rights domain user account.  

    -   You must install **SQL Server reporting services**.  

    -   **Intersite communications** use the SQL Server Service Broker on default port TCP 4022.  

    -   **Intrasite communications** between the SQL Server database engine and select Configuration Manager site system roles  use default port TCP 1433.  

-   **The domain controller uses Windows Server 2008 R2** with Active Directory Domain Services installed. The domain controller also functions as the host for the DHCP and the DNS servers for use with a fully qualified domain name.  

     For more information, see [overview of Active Directory Domain Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831484(v=ws.11)).  

-   **Hyper-V is used with a few virtual machines** to verify that the management steps taken in these exercises are functioning as expected. A minimum of three virtual machines is recommended, with Windows 10 installed.  

     For more information, see [overview of Hyper-V](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).  

-   **Administrator permissions** will be required for all of these components.  

    -   Configuration Manager requires an administrator with local permissions within the Windows Server environment  

    -   Active Directory requires an administrator with permissions to modify the schema  

    -   Virtual machines require local permissions on the machines themselves  

Though not required for this lab, you can review [Supported configurations for Configuration Manager](../../core/plan-design/configs/supported-configurations.md) for additional information on requirements for implementing Configuration Manager. Refer to documentation for  software versions other than those referenced here.  

Once you have installed all of these components, there are additional steps you must take to configure your Windows environment for Configuration Manager:  

##  <a name="BKMK_LabADPrep"></a> Prepare Active Directory content for the lab  
 For this lab, you will create a security group, then add a domain user to it.  

-   Security group: **Evaluation**  

    -   Group scope: **Universal**  

    -   Group type: **Security**  

-   Domain user: **ConfigUser**  

     Under normal circumstances, you wouldn't grant universal access to all users within your environment. You are doing so with this user in order to streamline bringing your lab online.  

The next steps required to enable Configuration Manager clients to query Active Directory Domain Services to locate site resources are listed over the next procedures.  

##  <a name="BKMK_CreateSysMgmtLab"></a> Create the System Management container  
 Configuration Manager won't automatically create the required System Management container in Active Directory Domain Services when the schema is extended. Therefore, you will create this for your lab. This step will require you to [install ADSI Edit](/previous-versions/windows/it-pro/windows-server-2003/cc773354(v=ws.10)).

 Ensure that you are logged on as an account that has **Create All Child Objects** permission on the **System** Container in Active Directory Domain Services.  

#### To create the System Management container:  

1.  Run **ADSI Edit**, and connect to the domain in which the site server resides.  

2.  Expand **Domain&lt;computer fully qualified domain name\>**, expand **<distinguished name\>**, right-click **CN=System**, click **New**, and then click **Object**.  

3.  In the **Create Object** dialog box, select **Container**, and then click **Next**.  

4.  In the **Value** box, type **System Management**, and then click **Next**.  

5.  Click **Finish** to complete the procedure.  

##  <a name="BKMK_SetSecPermLab"></a> Set security permissions for the System Management container  
 Grant the site server's computer account the permissions that are required to publish site information to the container. You will use ADSI Edit for this task as well.  

> [!IMPORTANT]  
>  Confirm that you are connected to the site server's domain prior to beginning the following procedure.  

#### To set security permissions for the System Management container:  

1.  In the console pane, expand the **site server's domain**, expand **DC=&lt;server distinguished name\>**, and then expand **CN=System**. Right-click **CN=System Management**, and then click **Properties**.  

2.  In the **CN=System Management Properties** dialog box, click the **Security** tab, and then click **Add** to add the site server computer account. Grant the account **Full Control** permissions.  

3.  Click **Advanced**, select the site server's computer account, and then click **Edit**.  

4.  In the **Apply onto** list, select **This object and all descendant objects**.  

5.  Click **OK** to close the **ADSI Edit** console and complete the procedure.  

     For more information, see [Extend the Active Directory schema for Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md)  

##  <a name="BKMK_ExtADSchLab"></a> Extend the Active Directory schema using extadsch.exe  
 You will extend the Active Directory schema for this lab, as this allows you to use all Configuration Manager features and functionality with the least amount of administrative overhead. Extending the Active Directory schema is a forest-wide configuration that is done one time per forest. Extending the schema permanently modifies the set of classes and attributes in your base Active Directory configuration. This action is irreversible. Extending the schema allows Configuration Manager to access components that will allow it to function most effectively within your lab environment.  

> [!IMPORTANT]  
>  Ensure that you are logged on to the schema master domain controller with an account that is a member of the **Schema Admins** security group. Attempting to use alternate credentials will fail.  

#### To extend the Active Directory schema using extadsch.exe:  

1.  Create a backup of the schema master domain controller's system state. For more information about backing up master domain controller, see [Windows Server Backup](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770757(v=ws.11))  

2.  Navigate to **\SMSSETUP\BIN\X64** in the installation media.  

3.  Run **extadsch.exe**.  

4.  Verify that the schema extension was successful by reviewing the **extadsch.log** located in the root folder of the system drive.  

     For more information, see [Extend the Active Directory schema for Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

##  <a name="BKMK_OtherTasksLab"></a> Other required tasks  
 You will also need to complete the following tasks prior to installation.  

 **Create a folder for storing all  downloads**  

 There will be multiple downloads required for components of the installation media throughout this exercise. Before beginning any installation procedures, determine a location that will not require you to move these files until you wish to decommission your lab. A single folder with separate subfolders to store these downloads is recommended.  

 **Install .NET and activate Windows Communication Foundation**  

 You will need to install two .NET Frameworks: first, .NET 3.5.1 and then .NET 4.5.2+. You will also need to activate Windows Communication Foundation (WCF). WCF is designed to offer a manageable approach to distributed computing, broad interoperability, and direct support for service orientation, and simplifies development of connected applications through a service-oriented programming model. For more information, see [What Is Windows Communication Foundation?](/previous-versions/dotnet/netframework-3.5/ms731082(v=vs.90)).

#### To install .NET and activate Windows Communication Foundation:  

1.  Open **Server Manager**, then navigate to **Manage**. Click **Add Roles and Features** to open the **Add Roles and Features Wizard.**  

2.  Review the information provided in the **Before You Begin** panel, then click **Next**.  

3.  Select **Role-based or feature-based installation**, then click **Next**.  

4.  Select your server from the **Server Pool**, then click **Next**.  

5.  Review the **Server Roles** panel, then click **Next**.  

6.  Add the following **Features** by selecting them from the list:  

    -   **.NET Framework 3.5 Features**  

        -   **.NET Framework 3.5 (includes .NET 2.0 and 3.0)**  

    -   **.NET Framework 4.5 Features**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **WCF Services**  

            -   **HTTP Activation**  

            -   **TCP Port Sharing**  

7.  Review the **Web Server Role (IIS)** and **Role Services** screen, then click **Next**.  

8.  Review the **Confirmation** screen, then click **Next**.  

9. Click **Install** and verify that the installation completed properly in the **Notifications** pane of **Server Manager**.  

10. After the base installation of .NET completes, navigate to  the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=42643) to obtain the web installer for the .NET Framework 4.5.2. Click the **Download** button, then **Run** the installer. It will automatically detect and install the required components in your selected language.  

**Enable BITS, IIS, and RDC**  

The [Background Intelligent Transfer Service (BITS)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282296(v=ws.11)) is used for applications that need to transfer files asynchronously between a client and a server. By metering the flow of the transfers in the foreground and background, BITS preserves the responsiveness of other network applications. It will also automatically resume file transfers if a transfer session is interrupted.  

You will install BITS for this lab, as this site server will also be used as a management point.  

Internet Information Services (IIS) is a flexible, scalable web server that can be used to host anything on the web. It is used by Configuration Manager for a number of site system roles. For additional information on IIS, review [Websites for site system servers](../../core/plan-design/network/websites-for-site-system-servers.md).  

[Remote Differential Compression (RDC)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754372(v=ws.11)) is a set of APIs that applications can use to determine if any changes have been made to a set of files. RDC enables the application to replicate only the changed portions of a file, keeping network traffic to a minimum.  

#### To enable BITS, IIS, and RDC site server roles:  

1.  On your site server, open **Server Manager**. Navigate to **Manage**. Click **Add Roles and Features** to open the **Add Roles and Features Wizard**.  

2.  Review the information provided in the **Before You Begin** panel, then click **Next**.  

3.  Select **Role-based or feature-based installation**, then click **Next**.  

4.  Select your server from the **Server Pool**, then click **Next**.  

5.  Add the following **Server Roles** by selecting them from the list:  

    -   **Web Server (IIS)**  

        -   **Common HTTP Features**  

            -   **Default Document**  

            -   **Directory Browsing**  

            -   **HTTP Errors**  

            -   **Static Content**  

            -   **HTTP Redirection**  

        -   **Health and Diagnostics**  

            -   **HTTP Logging**  

            -   **Logging Tools**  

            -   **Request Monitor**  

            -   **Tracing**  

    -   **Performance**  

        -   **Static Content Compression**  

        -   **Dynamic Content Compression**  

    -   **Security**  

        -   **Request Filtering**  

        -   **Basic Authentication**  

        -   **Client Certificate Mapping Authentication**  

        -   **IP and Domain Restrictions**  

        -   **URL Authorization**  

        -   **Windows Authentication**  

    -   **Application Development**  

        -   **.NET Extensibility 3.5**  

        -   **.NET Extensibility 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **ISAPI Extensions**  

        -   **ISAPI Filters**  

        -   **Server Side Includes**  

    -   **FTP Server**  

        -   **FTP Service**  

    -   **Management Tools**  

        -   **IIS Management Console**  

        -   **IIS 6 Management Compatibility**  

            -   **IIS 6 Metabase Compatibility**  

            -   **IIS 6 Management Console**  

            -   **IIS 6 Scripting Tools**  

            -   **IIS 6 WMI Compatibility**  

        -   **IIS 6 Management Scripts and Tools**  

        -   **Management Service**  

6.  Add the following **Features** by selecting them from the list:  

    -   **Background Intelligent Transfer Service (BITS)**  

          -   **IIS Server Extension**  

    -   **Remote Server Administration Tools**  

          -   **Feature Administration Tools**  

          -   **BITS Server Extensions Tools**  

7.  Click **Install** and verify that the installation completed properly in the **Notifications** pane of **Server Manager**.  

By default, IIS blocks several types of file extensions and locations from access by HTTP or HTTPS communication. To enable these files to be distributed to client systems, you will need to configure request filtering for IIS on your distribution point. For more information, see [IIS Request Filtering for distribution points](../../core/plan-design/network/prepare-windows-servers.md#iis-request-filtering-for-distribution-points).  

#### To configure IIS filtering on distribution points:  

1.  Open **IIS Manager** and select the name of your server in the sidebar. This will take you to the **Home** screen.  

2.  Verify that **Features View** is selected at the bottom of the **Home** screen. Navigate to **IIS** and open **Request Filtering**.  

3.  In the **Actions** pane, click **Allow File Name Extension...**  

4.  Type **.msi** into the dialog box and click **OK**.  

##  <a name="BKMK_InstallCMLab"></a> Installing Configuration Manager  
You will create a [Determine when to use a primary site](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary) to manage clients directly. This will allow your lab environment to support management for [Site system scale](../plan-design/configs/size-and-scale-numbers.md) of potential devices.  
During this process, you will also install the Configuration Manager console, which will be used to manage your evaluation devices going forward.  

Before you begin the installation, launch the  [Prerequisite Checker](../servers/deploy/install/prerequisite-checker.md) on the server using Windows Server 2012 to confirm that all settings have been correctly enabled.  

#### To download and install Configuration Manager:  

1. Navigate to the [Evaluation Center](https://www.microsoft.com/evalcenter/download-microsoft-endpoint-configuration-manager) page to download the newest evaluation version of Configuration Manager.  

<!--
> [!NOTE]
> The Evaluation Center is currently unavailable. As a workaround you can download the ConfigMgr 2203 Current Branch Eval exe here : ( https://aka.ms/MECM2203CB-Eval).
-->

2.  Decompress the download media into your predefined location.  

3.  Follow the installation procedure listed at [Install a site using the Configuration Manager Setup Wizard](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md). Within that procedure, you will input the following:  

    |Step in site installation procedure|Selection|  
    |-----------------------------------------|---------------|  
    |Step 4: the **Product Key** page|Select **Evaluation**.|  
    |Step 7:  **Prerequisite Downloads**|Select **Download required files** and specify your predefined location.|  
    |Step 10: **Site and Installation Settings**|-   **Site code:LAB**<br />-   **Site name:Evaluation**<br />-   **Installation folder:** specify your predefined location.|  
    |Step 11: **Primary Site Installation**|Select **Install the primary site as a stand-alone site**, then click **Next**.|  
    |Step 12: **Database Installation**|-   **SQL Server name (FQDN):** input your FQDN here.<br />-   **Instance name:** leave this blank, as you will use the default instance of SQL Server that you previously installed.<br />-   **Service Broker Port:** leave as default port of 4022.|  
    |Step 13: **Database Installation**|Leave these settings as default.|  
    |Step 14: **SMS Provider**|Leave these settings as default.|  
    |Step 15: **Client Communication Settings**|Confirm that **All site system roles accept only HTTPS communication from clients** is not selected|  
    |Step 16: **Site System Roles**|Input your FQDN and confirm that your selection of **All site system roles accept only HTTPS communication from clients** is still deselected.|  

##  <a name="BKMK_EnablePubLab"></a> Enable publishing for the Configuration Manager site  
Each Configuration Manager site publishes its own site-specific information to the System Management container within its domain partition in the Active Directory schema. Bidirectional channels for communication between Active Directory and Configuration Manager must be opened to handle this traffic. You will also additionally enable Forest Discovery to determine certain components of your Active Directory and network infrastructure.  

#### To configure Active Directory forests for publishing:  

1.  In the bottom-left corner of the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Hierarchy Configuration**, then click **Discovery Methods**.  

3.  Select **Active Directory Forest Discovery** and click **Properties**.  

4.  In the **Properties** dialog box, select **Enable Active Directory Forest Discovery**. Once this is active, select **Automatically create Active Directory site boundaries when they are discovered**. A dialog box will appear that states **Do you want to run full discovery as soon as possible?** Click **Yes**.  

5.  In the **Discovery Method** group at the top of the screen, click **Run Forest Discovery Now**, then navigate to **Active Directory Forests** in the sidebar. Your Active Directory forest should be shown in the list of discovered forests.  

6.  Navigate to the top of the screen, to the **General** tab.  

7.  In the **Administration** workspace, expand **Hierarchy Configuration**, then click **Active Directory Forests**.  

#### To enable a Configuration Manager site to publish site information to your Active Directory forest:  

1.  In the Configuration Manager console, click **Administration**.  

2.  You will configure a new forest that has not yet been discovered.  

3.  In the **Administration** workspace, click **Active Directory Forests**.  

4.  On the **Publishing** tab of the site properties, select your connected forest, then click **Ok** to save the configuration.
