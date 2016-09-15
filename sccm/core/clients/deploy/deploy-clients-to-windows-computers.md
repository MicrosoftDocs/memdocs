---
title: "How to deploy clients to Windows computers in System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
caps.latest.revision: 13
caps.handback.revision: 0
author: Mtillman
translation.priority.ht:
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to deploy clients to Windows computers in System Center Configuration Manager
You can use different client deployment methods to install the System Center Configuration Manager client software on computers. To help you decide which deployment method to use, see [Client installation methods in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

 Before you install Configuration Manager clients, ensure that all the prerequisites are in place and that you have completed all required deployment configurations. For more information, see [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md).  

 Use the following procedures to install clients in Configuration Manager.  

-   [How to Install Configuration Manager Clients by Using Client Push](#BKMK_ClientPush)  

-   [How to Install Configuration Manager Clients by Using Software Update-Based Installation](#BKMK_ClientSUP)  

-   [How to Install Configuration Manager Clients by Using Group Policy](#BKMK_ClientGP)  

-   [How to Install Configuration Manager Clients Manually](#BKMK_Manual)  

-   [How to Install Configuration Manager Clients by Using Logon Scripts](#BKMK_ClientLogonScript)  

-   [How to Install Configuration Manager Clients by Using a Package and Program](#BKMK_ClientApp)  

-   [How to Install Configuration Manager Clients by Using Computer Imaging](#BKMK_ClientImage)  

-   [How to Install Configuration Manager Clients on Workgroup Computers](#BKMK_ClientWorkgroup)  

-   [How to Install Configuration Manager Clients for Internet-based Client Management](#BKMK_ClientInternet)  

-   [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](#BKMK_Provision)  

##  <a name="BKMK_ClientPush"></a> How to Install Configuration Manager Clients by Using Client Push  
 Use client push installation to install the Configuration Manager client software on computers that Configuration Manager discovered. You can configure client push installation for a site, and client installation will automatically run on the computers that are discovered within the site's configured boundaries when those boundaries are configured as a boundary group. Or, you can initiate a client push installation by running the Client Push Installation Wizard for a specific collection or resource within a collection.  

 You can also use the Client Push Installation Wizard to install the Configuration Manager client to the results that are obtained from running a query. For installation to succeed in this scenario, one of the items returned by the selected query must be the attribute **ResourceID** from the attribute class **System Resource**. For more information about queries, see [Queries technical reference for System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md).  

 If the site server cannot contact the client computer or start the setup process, it automatically repeats the installation attempt every hour for up to 7 days until it succeeds.  

 To help track the client installation process, install a fallback status point site system before you install the clients. When a fallback status point is installed, it is automatically assigned to clients when they are installed by the client push installation method. View the client deployment and assignment reports to track client installation progress. Additionally, the client log files provide more detailed information for troubleshooting and do not require the installation of a fallback status point. For example, the CCM.log file on the site server records any problems that the site server has connecting to the computer, and the CCMSetup.log file on the client records the installation process.  

> [!IMPORTANT]  
>  For client push to succeed, ensure that all the prerequisites are in place. These are listed in the section “Installation Method Dependencies” in [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md).  

#### To configure the site to automatically use client push for discovered computers  

1.  In the Configuration Manager console, click **Administration.**  

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Sites**.  

3.  In the **Sites** list, select the site for which you want to configure automatic site-wide client push installation.  

4.  On the **Home** tab, in the **Settings** group, click **Client Installation Settings**, and then click **Client Push Installation**.  

5.  On the **General** tab of the **Client Push Installation Properties** dialog box, select **Enable automatic site-wide client push installation**. Select the system types to which Configuration Manager should push the client software by selecting **Servers**, **Workstations**, or **Configuration Manager site system servers**. The default selection is **Servers** and **Workstations**.  

6.  Select whether you want automatic site-wide client push installation to install the Configuration Manager client software on domain controllers.  

7.  On the **Accounts** tab, specify one or more accounts for Configuration Manager to use when connecting to the computer to install the client software. Click the **Create** icon, enter the **User name** and **Password**, confirm the password, and then click **OK**. You must specify at least one client push installation account, which must have local administrator rights on every computer on which you want to install the client. If you do not specify a client push installation account, Configuration Manager tries to use the site system computer account, which will cause cross-domain client push to fail.  

    > [!IMPORTANT]  
    >  The password for the client push installation account is limited to 38 characters or less.  

    > [!NOTE]  
    >  If you intend to use the client push installation method from a secondary site, the account must be specified at the secondary site that initiates the client push.  
    >   
    >  For more information about the client push installation account, see the next procedure,”To use the Client Push Installation Wizard”.  

8.  On the **Installation Properties** tab, specify any installation properties  to use when installing the Configuration Manager client. You can specify any installation properties of the Windows Installer package (Client.msi) and the following CCMSetup.exe properties:  

    -   /forcereboot  

    -   /skipprereq  

    -   /logon  

    -   /BITSPriority  

    -   /downloadtimeout  

    -   /forceinstall  

     Client installation properties that are specified in this tab are published to Active Directory Domain Services if the schema is extended for Configuration Manager and read by client installations where CCMSetup is run without installation properties. For more information about client installation properties, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!NOTE]  
    >  If you enable client push installation on a secondary site, ensure that the SMSSITECODE property is set to the Configuration Manager site name of its parent primary site. If the Active Directory schema is extended for Configuration Manager, you can also set this to AUTO to automatically find the correct site assignment.  

#### To use the Client Push Installation Wizard  

1.  In the Configuration Manager console, click **Administration.**  

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Sites**.  

3.  In the **Sites** list, select the site for which you want to configure automatic site-wide client push installation.  

4.  On the **Home** tab, in the **Settings** group, click **Client Installation Settings**, and then click **Client Push Installation**.  

5.  On the **Installation Properties** tab, specify any installation properties to use when installing the Configuration Manager client. You can specify any installation properties of the Windows Installer package (Client.msi) and the following CCMSetup.exe properties:  

    -   /forcereboot  

    -   /skipprereq  

    -   /logon  

    -   /BITSPriority  

    -   /downloadtimeout  

    -   /forceinstall  

     Client installation properties that are specified in this tab are published to Active Directory Domain Services if the schema is extended for Configuration Manager and read by client installations where CCMSetup is run without installation properties. For more information about client installation properties, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

6.  In the Configuration Manager console, click **Assets and Compliance**.  

7.  In the **Assets and Compliance** workspace, select one or more computers, or a collection of computers.  

8.  On the **Home** tab, choose one of the following:  

    -   If you want to install the client to a single computer or multiple computers, in the **Device** group, click **Install Client**.  

    -   If you want to install the client to a collection of computers, in the **Collection** group, click **Install Client**.  

9. On the **Before You Begin** page of the **Install Client Wizard**, review the information, and then click **Next**.  

10. On the **Installation options** page, configure whether the client can be installed on domain controllers, whether the client will be reinstalled, upgraded, or repaired on computers with an existing client, and the name of the site that will install the client software. Click **Next**.  

11. Review the installation settings, and then close the wizard.  

> [!NOTE]  
>  You can use the wizard to install clients even if the site is not configured for client push.  

##  <a name="BKMK_ClientSUP"></a> How to Install Configuration Manager Clients by Using Software Update-Based Installation  
 Software update-based client installation publishes the Configuration Manager client to a software update point as an additional software update. This method of client installation can be used to install the Configuration Manager client on computers that do not already have the client installed or to upgrade existing Configuration Manager clients.  

 If a computer has the Configuration Manager client installed, Configuration Manager provides the client with the software update point server name and port from which to obtain software updates. This information is included in the client policy.  

> [!IMPORTANT]  
>  To use software update-based installation, you must use the same Windows Server Update Services (WSUS) server for client installation and software updates. This server must be the active software update point in a primary site. For more information, see [Configure software updates in System Center Configuration Manager](../../../sum/deploy-use/configure-software-updates.md).  

 If a computer does not have the Configuration Manager client installed, you must configure and assign a Group Policy Object (GPO) in Active Directory Domain Services to specify the software update point server name from which the computer will obtain software updates.  

 You cannot add command-line properties to a software update-based client installation. If you have extended the Active Directory schema for Configuration Manager, client computers automatically query Active Directory Domain Services for installation properties when they install.  

 If you have not extended the Active Directory schema, you can use Group Policy to provision client installation settings to computers in your site. These settings are automatically applied to any software update-based client installations. For more information, see [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](#BKMK_Provision) and [How to assign clients to a site in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

 Use the following procedures to configure computers without a Configuration Manager client to use the software update point for client installation and software updates, and to publish the Configuration Manager client software to the software update point.  

> [!NOTE]  
>  If computers are in a pending restart state following a previous software installation, then a software update based client installation might cause the computer to restart.  

#### To configure a Group Policy Object in Active Directory Domain Services to specify the software update point for client installation and software updates  

1.  Use the Group Policy Management Console to open a new or existing Group Policy Object.  

2.  In the console, expand **Computer Configuration**, expand **Administrative Templates**, expand **Windows Components**, and then click **Windows Update**.  

3.  Open the properties of the setting **Specify intranet Microsoft update service location**, and then click **Enabled**.  

4.  In the box **Set the intranet update service for detecting updates**, specify the name of the software update point server that you want to use and the port. These must match exactly the server name format and the port being used by the software update point:  

    -   If the Configuration Manager site system is configured to use a fully qualified domain name (FQDN), specify the server name by using FQDN format.  

    -   If the Configuration Manager site system is not configured to use a fully qualified domain name (FQDN), specify the server name by using a short name format.  

    > [!NOTE]  
    >  To determine the port number that is being used by the software update point, see [How to determine the port settings used by WSUS in System Center Configuration Manager](../../../sum/plan-design/determine-wsus-port-settings.md).  

     Example: **http://server1.contoso.com:8530**  

5.  In the box **Set the intranet statistics server**, specify the name of the intranet statistics server that you want to use. There are no specific requirements for specifying this server. It does not have to be the same computer as the software update point server, and the format does not have to match if it is the same server.  

6.  Assign the Group Policy Object to the computers on which you want to install the Configuration Manager client and receive software updates.  

#### To publish the Configuration Manager client to the software update point  

1.  In the Configuration Manager console, click **Administration.**  

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Sites**.  

3.  In the **Sites** list, select the site for which you want to configure software update-based client installation.  

4.  On the **Home** tab, in the **Settings** group, click **Client Installation Settings**, and then click **Software Update-Based Client Installation**.  

5.  In the **Software Update Point Client Installation Properties** dialog box, select **Enable software update-based client installation** to enable this client installation method.  

6.  If the client software on the Configuration Manager site server is a later version than the client version stored on the software update point, the **Later Version of Client Package Detected** dialog box opens. Click **Yes** to publish the most recent version of the client software to the software update point.  

    > [!NOTE]  
    >  If the client software has not been previously published to the software update point, this box will be blank.  

7.  To finish configuring the software update point client installation, click **OK**.  

> [!NOTE]  
>  The software update for the Configuration Manager client is not automatically updated when there is a new version. If you upgrade the site, which includes a new client version, you must repeat this procedure and click **Yes** for step 6.  

##  <a name="BKMK_ClientGP"></a> How to Install Configuration Manager Clients by Using Group Policy  
 You can use Group Policy in Active Directory Domain Services to publish or assign the Configuration Manager client to install on computers in your enterprise. When you assign the Configuration Manager client to computers by using Group Policy, the client installs when the computer first starts. When you publish the Configuration Manager client to users by using Group Policy, the client displays in the Control Panel **Add or Remove Programs** for the computer for the user to install.  

 Use the Windows Installer package (CCMSetup.msi) for Group Policy-based installations. This file is found in the folder **<ConfigMgr installation directory\>\bin\i386** on the Configuration Manager site server. You cannot add properties to this file to modify installation behavior:  

> [!IMPORTANT]  
>  You must have Administrator permissions to the folder to access the client installation files.  

-   If the Active Directory schema is extended for Configuration Manager and **Publish this site in Active Directory Domain Services** is selected in the **Advanced** tab of the **Site Properties** dialog box, client computers automatically search Active Directory Domain Services for installation properties. For more information about the installation properties that are published, see [About client installation properties published to Active Directory Domain Services in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   If the Active Directory schema has not been extended, you can use the following procedure in this topic to store installation properties in the registry of computers: [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](#BKMK_Provision). These installation properties are then used when the Configuration Manager client is installed.  

 For information about how to use Group Policy in Active Directory Domain Services to install software, refer to your Windows Server documentation.  

##  <a name="BKMK_Manual"></a> How to Install Configuration Manager Clients Manually  
 You can manually install the Configuration Manager client software on computers in your enterprise by using the CCMSetup.exe program. This program and its supporting files can be found in the **Client** folder of the Configuration Manager installation folder on the site server and on management points in your site. This folder is shared to the network as  

 \\\\*<Site Server Name\>*\SMS_*<Site Code\>*\Client\  

 where *<Site Server Name\>* is the name of one of the servers hosting a management point and *<Site Code\>* is the code for primary site the client will belong to.  To run CCMSetup.exe from the command line on the client, you must map a network drive to this location, and then run the command.  

> [!IMPORTANT]  
>  You must have Administrator permissions to the folder to access the client installation files.  

 CCMSetup.exe copies all necessary installation prerequisites to the client computer and calls the Windows Installer package (Client.msi) to perform the client installation.  

> [!IMPORTANT]  
>  You cannot run Client.msi directly.  

 You can specify command-line properties for both CCMSetup.exe and Client.msi to modify the behavior of the client installation. Make sure that you specify CCMSetup properties (the properties that begin with “**/**” ) before you specify Client.msi properties.  

 For example, you could specify the following command:  

```  
CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01  
```  

 and the client installs by using the following properties:  

|Property|Description|  
|--------------|-----------------|  
|**/mp:SMSMP01**|This CCMSetup property specifies the management point SMSMP01 to download the required client installation files.|  
|**/logon**|This CCMSetup property specifies that the installation should stop if an existing Configuration Manager client is found on the computer.|  
|**SMSSITECODE=AUTO**|This Client.msi property specifies that the client tries to locate the Configuration Manager site code to use, for example, by using Active Directory Domain Services.|  
|**FSP=SMSFP01**|This Client.msi property specifies that the fallback status point named SMSFP01 will be used to receive state messages sent from the client computer.|  

 For details on all CCMSetup.exe properties, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md)  

### Examples for Installing Configuration Manager Clients Manually  
 These examples are for Active Directory clients on the intranet and  use  the following values to represent different aspects of the site:  

 **MPSERVER** = server hosting the management point   
**FSPSERVER** = server hosting the fallback status point  
**ABC** = site code  
**contoso.com** = domain name  

 All site system servers are configured with an intranet FQDN and the site is published to the client’s Active Directory forest.  

 On the client computer, you log on as a local administrator, map a drive (z:) to\\\MPSERVER\SMS_ABC\Client, switch the command prompt to the z drive, and then run one of the following commands.  

 **Example 1:**  

```  
CCMSetup.exe  
```  

> [!NOTE]  
>  This example installs the client with no additional properties so that the client is automatically configured by using the client installation properties published to Active Directory Domain Services. For example, the client is automatically configured for the site code (requires the client’s network location to be included in a boundary group that is configured for client assignment), a management point, the fallback status point, and whether the client must communicate by using HTTPS only. For more information about the client installation properties that can be automatically configured for Active Directory clients, see [About client installation properties published to Active Directory Domain Services in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Example 2:**  

```  
CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com  
```  

> [!NOTE]  
>  This example overrides the automatic configuration that Active Directory Domain Services can provide and does not require that the client’s network location is included in a boundary group that is configured for client assignment. Instead, the installation specifies the site, an intranet management point and an Internet-based management point, a fallback status point that accepts connections from the Internet, and to use a client PKI certificate (if available) that has the longest validity period.  

##  <a name="BKMK_ClientLogonScript"></a> How to Install Configuration Manager Clients by Using Logon Scripts  
 Configuration Manager supports logon scripts to install the Configuration Manager client software. You can use the program file **CCMSetup.exe** in a logon script to trigger the client installation.  

 Logon script installation uses the same methods as manual client installation. You can specify the **/logon** installation property for CCMSsetup.exe, which prevents the client from installing if any version of the client already exists on the computer. This prevents reinstallation of the client from taking place each time the logon script runs.  

 If no installation source is specified that is using the **/Source** property and no management point from which to obtain installation is specified by using the **/MP** property, CCMSetup.exe can locate the management point by searching Active Directory Domain Services if the schema has been extended for Configuration Manager and the site is published to Active Directory Domain Services. Alternatively, the client can use DNS or WINS to locate a management point.  

##  <a name="BKMK_ClientApp"></a> How to Install Configuration Manager Clients by Using a Package and Program  
 You can use Configuration Manager to create and deploy a package and program that upgrades the client software for selected computers in your hierarchy. A package definition file is supplied with Configuration Manager that populates the package properties with typically used values. You can customize the behavior of the client installation by specifying additional command line properties.  

> [!NOTE]  
>  You cannot upgrade  Configuration Manager 2007 clients by using this method. Instead, use automatic client upgrade, which automatically creates and deploys a package that contains the latest version of the client. For more information, see [Upgrade clients in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  For more information about how to migrate from older versions of the Configuration Manager client, see [Planning a client migration strategy in System Center Configuration Manager](../../../core/migration/planning-a-client-migration-strategy.md).  

 Use the following procedure to create a Configuration Manager package and program that you can deploy to Configuration Manager client computers to upgrade the client software.  

#### To create a package and program for the client software  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Application Management**, and then click **Packages**.  

3.  On the **Home** tab, in the **Create** group, click **Create Package from Definition**.  

4.  On the **Package Definition** page of the **Create Package from Definition Wizard**, select **Microsoft** from the **Publisher** drop-down list, select **Configuration Manager Client Upgrade** from the **Package definition** list, and then click **Next**.  

5.  On the **Source Files** page of the wizard, select **Always obtain files from a source folder**, and then click **Next**.  

6.  On the **Source Folder** page of the **Create Package from Definition Wizard**, select **Network path (UNC Name)** and enter the network path to the computer and folder that contains the Configuration Manager client installation files.  

    > [!NOTE]  
    >  The computer on which the Configuration Manager deployment runs must have access to the network folder that you specify. If the computer does not have access, the installation will fail.  

7.  Click **Next** and complete the wizard.  

8.  If you want to change any of the client installation properties, you can modify the CCMSetup.exe command line parameters on the **General** tab of the **Configuration Manager agent silent upgrade Properties** program dialog box. The default installation properties are **/noservice SMSSITECODE=AUTO**.  

9. Distribute the package to all distribution points that you want to host the client upgrade package. You can then deploy the package to computer collections that contain Configuration Manager clients that you want to upgrade.  

##  <a name="BKMK_ClientImage"></a> How to Install Configuration Manager Clients by Using Computer Imaging  
 You can preinstall the Configuration Manager client software on a master image computer that will be used to build computers in your enterprise. To install the client on a master computer, do not specify a site code for the client. When computers are imaged from this master image, they will contain the Configuration Manager client and must complete site assignment when installation is complete.  

> [!IMPORTANT]  
>  The imaged computers cannot function as Configuration Manager clients until the Configuration Manager clients are assigned to a Configuration Manager site.  

 You must remove any computer-specific certificates that are installed on the master image computer. For example, if you use public key infrastructure (PKI) certificates, you must remove the certificates in the **Personal** store for **Computer** and **User** before you image the computer.  

 If clients cannot query Active Directory Domain Services to locate a management point, they use the trusted root key to determine trusted management points. If all imaged clients will be deployed in the same hierarchy as the master computer, leave the trusted root key in place. If the clients will be deployed in different hierarchies, remove the trusted root key and as a best practice, preprovision these clients with the new trusted root key. For more information, see  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

#### To prepare the client computer for imaging  

1.  Manually install the Configuration Manager client software on the master image computer. For more information, see [How to Install Configuration Manager Clients Manually](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Do not specify a Configuration Manager site code for the client in the CCMSetup.exe command-line properties.  

2.  At a command prompt, type **net stop ccmexec** to ensure that the **SMS Agent Host** service (Ccmexec.exe) is not running on the master image computer.  

3.  Remove any certificates that are stored in the local computer store on the master image computer.  

4.  If the clients will be installed in a different Configuration Manager hierarchy than the master image computer, remove the Trusted Root Key from the master image computer.  

5.  Use your imaging software to capture the image of the master computer.  

6.  Deploy the image to destination computers.  

##  <a name="BKMK_ClientWorkgroup"></a> How to Install Configuration Manager Clients on Workgroup Computers  
 Configuration Manager supports client installation for computers in workgroups. Install the client on workgroup computers by using the method specified in [How to Install Configuration Manager Clients Manually](#BKMK_Manual).  

 The following prerequisites must be met in order to install the Configuration Manager client on workgroup computers:  

-   The client must be installed manually on each workgroup computer. During installation, the logged-on user must have local administrator rights on the workgroup computer.  

-   In order to access resources in the Configuration Manager site server domain, the Network Access Account must be configured for the site. You specify this account as a software distribution component property. For more information, see [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

 There are a number of limitations to supporting workgroup computers:  

-   Workgroup clients cannot locate management points from Active Directory Domain Services, and instead must use DNS, WINS, or another management point.  

-   Global roaming is not supported, because clients cannot query Active Directory Domain Services for site information.  

-   Active Directory discovery methods cannot discover computers in workgroups.  

-   You cannot deploy software to users of workgroup computers.  

-   You cannot use the client push installation method to install the client on workgroup computers.  

-   Workgroup clients cannot use Kerberos for authentication and so might require manual approval.  

-   A workgroup client cannot be configured as a distribution point. Configuration Manager requires that distribution point computers be members of a domain.  

#### To install the client on workgroup computers  

1.  Ensure that the computers on which you want to install the client meet the above prerequisites.  

2.  Follow the directions in the section [How to Install Configuration Manager Clients Manually](#BKMK_Manual).  

     Example 1: **CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com**  

    > [!NOTE]  
    >  This example installs the client for intranet client management and specifies the site code and DNS suffix to locate a management point.  

     Example 2: **CCMSetup.exe FSP=fspserver.constoso.com**  

    > [!NOTE]  
    >  This example requires the client to be on a network location that is configured in a boundary group so that automatic site assignment can succeed. The command includes a fallback status point on server FSPSERVER, to help track client deployment and to identify any client communication issues.  

##  <a name="BKMK_ClientInternet"></a> How to Install Configuration Manager Clients for Internet-based Client Management  
 When the Configuration Manager site supports Internet-based client management for clients that are sometimes on the intranet, and sometimes on the Internet, you have two options when you install clients on the intranet:  

-   You can include the Client.msi property of CCMHOSTNAME=*<Internet FQDN of the Internet-based management point\>* when you install the client, for example by using manual installation or client push. When you use this method, you must also directly assign the client to the site and cannot use automatic site assignment. The [How to Install Configuration Manager Clients Manually](#BKMK_Manual) section in this topic provides an example of this configuration method.  

-   You can install the client for intranet client management, and then assign an Internet-based client management point to the client by using the Configuration Manager client properties in Control Panel, or by using a script. When you use this method, you can use automatic client assignment. For more information, see the [How to Configure Clients for Internet-based Client Management after Client Installation](#BKMK_ConfigureIBCM_MP) section in this topic.  

 If you must install clients that are on the Internet either because they are Internet-only clients, or because you must install them before they come back into the intranet, choose one of the following supported methods:  

-   Provide a mechanism for these clients to temporarily connect to the intranet by using a virtual private network (VPN), and then install them by using any appropriate client installation method.  

-   Use an installation method that is independent from Configuration Manager, such as packaging the client installation source files onto removable media that you can send to users to install with instructions. The client installation source files are located in the *<InstallationPath\>*\Client folder on the Configuration Manager site server and management points. Include on the media a script to manually copy over the client folder and from this folder, install the client by using CCMSetup.exe and all the appropriate CCMSetup command-line properties.  

> [!NOTE]  
>  Configuration Manager does not support installing a client directly from the Internet-based management point or from the Internet-based software update point.  

 Because clients that are managed over the Internet must communicate with Internet-based site systems, ensure that these clients also have public key infrastructure (PKI) certificates installed before you install them. You must install these certificates independently from Configuration Manager. For more information about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

#### To install clients on the Internet by specifying CCMSetup command-line properties  

1.  Follow the directions in the section [How to Install Configuration Manager Clients Manually](#BKMK_Manual) and always include the following:  

    -   CCMSetup command-line property **/source:***<local path to the copied Client folder\>*  

    -   CCMSetup command-line property **/UsePKICert**  

    -   Client.msi property **CCMHOSTNAME=***<FQDN of Internet-based management point\>*  

    -   Client.msi property **SMSSIGNCERT=***<local path to exported site server signing certificate\>*  

    -   Client.msi property **SMSSITECODE=***<site code of Internet-based management point\>*  

    > [!NOTE]  
    >  If the site has more than one Internet-based management point, it does not matter which Internet-based management point you specify for the CCMHOSTNAME property. When a Configuration Manager client connects to the specified Internet-based management point, the management point sends the client a list of available Internet-based management points in the site, and the client selects one from the list. The selection is nondeterministic.  

2.  If you do not want the client to check the certificate revocation list (CRL), specify the CCMSetup command-line property **/NoCRLCheck**.  

3.  If you are using an Internet-based fallback status point, specify the Client.msi property **FSP=***<Internet FQDN of the Internet-based fallback status point\>*.  

4.  If you are installing the client for Internet-only client management, specify the Client.msi property **CCMALWAYSINF=1**.  

5.  Verify whether you have to specify any additional CCMSetup command-line properties. For example, you might have to specify a certificate selection criteria if the client has more than one valid PKI certificate. For a list of available properties, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

     Example: **CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1**  

    > [!NOTE]  
    >  This example installs the client source files from a folder on the D drive with settings to use a client PKI certificate and select the certificate with the longest validity period for Internet-only client management, assigns the client to use the Internet-based management point named SERVER1 and the Internet-based fallback status point in the contoso.com domain, and assigns the client to the ABC site.  

###  <a name="BKMK_ConfigureIBCM_MP"></a> How to Configure Clients for Internet-based Client Management after Client Installation  
 To assign the Internet-based management point after the client is installed, use one of the following procedures. The first procedure requires manual configuration so it is appropriate for a few clients, whereas the second procedure is more appropriate if you have many clients to configure.  

##### To configure clients for Internet-based client management after client installation by assigning the Internet-based management point in Configuration Manager Properties  

1.  Navigate to **Configuration Manager** in the Control Panel of the client computer, and then double-click to open its properties.  

2.  On the **Internet** tab, enter the fully qualified domain name of the Internet-based management point in the Internet FQDN text box.  

    > [!NOTE]  
    >  The **Internet** tab is only available if the client has a client PKI certificate.  

3.  Enter proxy server settings if the client will access the Internet by using a proxy server.  

4.  Click **OK**.  

##### To configure clients for Internet-based client management after client installation by using a script  

1.  Open a text editor, such as Notepad.  

2.  Copy and insert the following into the file:  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the Internet-Based Management Point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

3.  Replace *mp.contoso.com* with the Internet FQDN of your Internet-based management point.  

    > [!NOTE]  
    >  If you have to delete a specified Internet-based management point so that the client is not configured to use an Internet-based management point, remove the value inside the quotation marks so that this line becomes **newInternetBasedManagementPointFQDN = ""**.  

4.  Save the file with a .vbs extension.  

5.  Use cscript to run the script on client computers, by using one of the following methods:  

    -   Deploy the file to existing Configuration Manager clients by using a package and a program.  

    -   Run the file locally on existing Configuration Manager clients by double-clicking the script file in Windows Explorer.  

 You might have to restart the client for the new setting in this script to take effect.  

##  <a name="BKMK_Provision"></a> How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)  
 You can use Windows Group Policy to provision computers in your enterprise with Configuration Manager client installation properties. These properties are stored in the registry of the computer and read when the client software is installed. This procedure would not normally be required for Configuration Manager. However, this might be required for some client installation scenarios, such as the following:  

-   You are using the Group Policy settings or software update-based client installation methods, and you have not extended the Active Directory schema for Configuration Manager.  

-   You want to override client installation properties on specific computers.  

> [!NOTE]  
>  If any installation properties are supplied on the CCMSetup.exe command line, installation properties provisioned on computers will not be used.  

 A Group Policy administrative template named ConfigMgrInstallation.adm is supplied on the Configuration Manager installation media, which can be used to provision client computers with installation properties. Use the following procedure to configure and assign this template to computers in your organization.  

#### To configure and assign client installation properties by using a Group Policy Object  

1.  Import the administrative template ConfigMgrInstallation.adm into a new or existing Group Policy Object, by using an editor such as Windows Group Policy Object Editor.  

    > [!NOTE]  
    >  This file can be found in the folder **TOOLS\ConfigMgrADMTemplates** on the Configuration Manager installation media.  

2.  Open the properties of the imported setting **Configure Client Deployment Settings**.  

3.  Click **Enabled**.  

4.  In the **CCMSetup** box, enter the required CCMSetup command-line properties. For a list of all CCMSetup command-line properties and examples of their use, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Assign the Group Policy Object to the computers that you want to provision with Configuration Manager client installation properties.  

 For information about Windows Group Policy, refer to your Windows Server documentation.  
