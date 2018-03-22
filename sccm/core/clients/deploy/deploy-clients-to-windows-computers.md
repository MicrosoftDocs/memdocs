---
title: Deploy clients to Windows
titleSuffix: Configuration Manager
description: Learn how to deploy the Configuration Manager client to Windows computers.
ms.custom: na
ms.date: 03/22/2018
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
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# How to deploy clients to Windows computers in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Before you install Configuration Manager clients, ensure that all the [prerequisites](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) are in place and that you have completed all required deployment configurations.   



##  <a name="BKMK_ClientPush"></a> How to install clients with client push  

You can configure client push installation for a site. Client installation automatically runs on the computers that are discovered within the site's configured boundaries when those boundaries are configured as a boundary group. Or, you can initiate a client push installation by running the Client Push Installation Wizard for a specific collection or resource within a collection.  

You can also use the Client Push Installation Wizard to install the Configuration Manager client to [query](../../../core/servers/manage/queries-technical-reference.md) results. For installation to succeed, one of the items returned by the query must be the attribute **ResourceID** from the class **System Resource**.   

If the site server can't contact the client computer or start the setup process, it automatically retries the installation every hour. The server continues to retry for up to seven days.  

To help track the client installation process, install a fallback status point before you install the clients. When a fallback status point is installed, it's automatically assigned to clients when they're installed by the client push installation method. To track client installation progress, view the client deployment and assignment reports. 

Client log files provide more detailed information for troubleshooting. The log files don't require a fallback status point. For example, the **CCM.log** file on the site server records any problems from the site server when connecting to the computer. The **CCMSetup.log** file on the client records the installation process.  

> [!IMPORTANT]  
>  For client push to succeed, ensure that all the prerequisites are in place. For more information, see [Installation method dependencies](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies).  

### Configure the site to automatically use client push for discovered computers

1.  In the Configuration Manager console, choose **Administration** > **Site Configuration** > **Sites**.  

3.  Select the site for which you want to configure automatic site-wide client push installation.  

4.  On the **Home** tab, in the **Settings** group, choose **Client Installation Settings** > **Client Push Installation**.  

5.  On the **General** tab of the **Client Push Installation Properties** dialog, select **Enable automatic site-wide client push installation**. Select the system types to which Configuration Manager should push the client software.  

6.  Select whether you want to install the client on domain controllers.  

7.  On the **Accounts** tab, specify one or more accounts for Configuration Manager to use when connecting to the target computer. Click the **Create** icon, enter the **User name** and **Password** (no more than 38 characters), confirm the password, and then click **OK**. Specify at least one client push installation account. This account must have local Administrator rights on the target computer to install the client. If you do not specify a client push installation account, Configuration Manager tries to use the site system computer account. Cross-domain client push fails when using the site system computer account.  
    > [!NOTE]  
    >  To use client push from a secondary site, specify the account at the secondary site that initiates the client push.  
    >   
    >  For more information about the client push installation account, see the next procedure, [Use the Client Push Installation Wizard](#use-the-client-push-installation-wizard).  

8.  Complete the **Installation Properties** tab.

     If the schema is extended for Configuration Manager, the site publishes to Active Directory Domain Services the [Client installation properties](../../../core/clients/deploy/about-client-installation-properties.md) that you specify in this tab. These properties are read by client installations where CCMSetup is run without installation properties.  

    > [!NOTE]  
    >  If you enable client push installation on a secondary site, ensure that the **SMSSITECODE** property is set to the Configuration Manager site name of its parent primary site. If the Active Directory schema is extended for Configuration Manager, you can also set this property to AUTO to automatically find the correct site assignment.  

### Use the Client Push Installation Wizard

1.  In the Configuration Manager console, choose **Administration** >  **Site Configuration** > **Sites**.  

3.  Select the site for which you want to configure automatic site-wide client push installation.  

4.  On the **Home** tab > **Settings** group, choose **Client Installation Settings** > **Client Push Installation**.  

5.  Complete the **Installation Properties** tab.  

     If the schema is extended for Configuration Manager, the site publishes to Active Directory Domain Services the [Client installation properties](../../../core/clients/deploy/about-client-installation-properties.md) that you specify in this tab. These properties are read by client installations where CCMSetup is run without installation properties.   

6.  In the Configuration Manager console, choose **Assets and Compliance**.  

7.  In the **Assets and Compliance** workspace, select one or more computers, or a collection of computers.  

8.  On the **Home** tab, choose one of the following options:  

    -   If you want to install the client to a single computer or multiple computers, in the **Device** group, choose **Install Client**.  

    -   If you want to install the client to a collection of computers, in the **Collection** group, choose **Install Client**.  

9. On the **Before You Begin** page of the **Install Client Wizard**, review the information, and then choose **Next**.  

10. Complete the **Installation options** page.  

11. Review the installation settings, and then close the wizard.  

> [!NOTE]  
>  You can use the wizard to install clients even if the site isn't configured for client push.  



##  <a name="BKMK_ClientSUP"></a> How to install clients with software update-based installation  
 Software update-based client installation publishes the client to a software update point as a software update. Use this method for a first-time installation or upgrade.  

 If a computer has the Configuration Manager client installed, it receives client policy from the site. This policy includes the software update point server name and port from which to get software updates.   

> [!IMPORTANT]  
>  To use software update-based installation, you must use the same Windows Server Update Services (WSUS) server for client installation and software updates. This server must be the active software update point in a primary site. For more information, see [Install a software update point](../../../sum/get-started/install-a-software-update-point.md).  

If a computer doesn't have the Configuration Manager client installed, configure and assign a group policy object in Active Directory Domain Services to specify the server name of the software update point.  

You can't add command-line properties to a software update-based client installation. If you've extended the Active Directory schema for Configuration Manager, client computers automatically query Active Directory Domain Services for installation properties when they install.  

If you have not extended the Active Directory schema, you can use group policy to provision client installation settings to computers in your site. These settings are automatically applied to any software update-based client installations. For more information, see [How to provision client installation properties (group policy and software update-based client installation)](#BKMK_Provision) and [How to assign clients to a site](../../../core/clients/deploy/assign-clients-to-a-site.md).  

Use the following procedures to configure computers without a Configuration Manager client to use the software update point for client installation and software updates, and to publish the client software to the software update point.  

> [!NOTE]  
>  If computers are in a pending restart state following a previous software installation, then a software update based client installation might cause the computer to restart.  

### Configure a group policy object in Active Directory Domain Services to specify the software update point for client installation and software updates:  

1.  Use the Group Policy Management Console to open a new or existing group policy object.  

2.  In the console, expand **Computer Configuration**, expand **Administrative Templates**, expand **Windows Components**, and then choose **Windows Update**.  

3.  Open the properties of the setting **Specify intranet Microsoft update service location**, and then choose **Enabled**.  

4.  In the box **Set the intranet update service for detecting updates**, specify the name and port of the software update point server:  

    -   If the Configuration Manager site system is configured to use a fully qualified domain name (FQDN), use the FQDN format.  

    -   If the Configuration Manager site system is not configured to use an FQDN, use a short name format.  

    > [!NOTE]  
    >  To determine the port number, see [How to determine the port settings used by WSUS](../../../sum/plan-design/plan-for-software-updates.md).  

     Example: **http://server1.contoso.com:8530**  

5.  In the box **Set the intranet statistics server**, specify the name of the intranet statistics server. It doesn't have to be the same as the software update point server. If it's the same server, the format doesn't have to match.  

6.  Assign the group policy object to the computers on which you want to install the client and receive software updates.  

### Publish the Configuration Manager client to the software update point  

1.  In the Configuration Manager console, click **Administration** > **Site Configuration** > **Sites**.  

3.  Select the site for which you want to configure software update-based client installation.  

4.  On the **Home** tab, in the **Settings** group, choose **Client Installation Settings**, and then choose **Software Update-Based Client Installation**.  

5.  Select **Enable software update-based client installation**.  

6.  If the client software on the Configuration Manager site server is a later version than the version on the software update point, the **Later Version of Client Package Detected** dialog box opens. Click **Yes** to publish the most recent version.  

    > [!NOTE]  
    >  If the client software wasn't previously published to the software update point, this box is blank.  

The software update for the Configuration Manager client isn't automatically updated when there's a new version. If you upgrade the site, which includes a new client version, repeat this procedure and click **Yes** for step 6.  



##  <a name="BKMK_ClientGP"></a> How to install clients with group policy  
 You can use group policy in Active Directory Domain Services to publish or assign the Configuration Manager client to install on computers in your enterprise. The client installs when the computer starts. When you use group policy, the client displays in the Control Panel **Add or Remove Programs** for the user to install.  

 Use the Windows Installer package (CCMSetup.msi) for group policy-based installations. This file is found in the folder **&lt;ConfigMgr installation directory\>\bin\i386** on the Configuration Manager site server. You can't add properties to this file to modify installation behavior.  

> [!IMPORTANT]  
>  You must have Administrator permissions to access the client installation files.  

-   If the Active Directory schema is extended for Configuration Manager and **Publish this site in Active Directory Domain Services** is selected in the **Advanced** tab of the **Site Properties** dialog box, client computers automatically search Active Directory Domain Services for installation properties. For more information about the installation properties that are published, see [About client installation properties published to Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   If the Active Directory schema has not been extended, you can use the  procedure in this topic to store installation properties in the registry of computers: [How to provision client installation properties (group policy and software update-based client installation)](#BKMK_Provision). These installation properties are used when the client is installed.  

For information about how to use group policy in Active Directory Domain Services to install software, refer to your Windows Server documentation.  



##  <a name="BKMK_Manual"></a> How to install clients manually  
 You can manually install the client software on computers in your enterprise by using the CCMSetup.exe program. This program and its supporting files can be found in the **Client** folder of the Configuration Manager installation folder on the site server and on management points in your site. This folder is shared to the network as  

 \\\\*&lt;Site Server Name\>*\SMS_*&lt;Site Code\>*\Client\  

 where *&lt;Site Server Name\>* is the name of one of the servers hosting a management point, and *&lt;Site Code\>* is the primary site code to which the client is assigned. To run CCMSetup.exe from the command line on the client, you must map a network drive to this location, and then run the command.  

> [!IMPORTANT]  
>  You must have Administrator permissions to access the client installation files.  

 CCMSetup.exe copies all necessary prerequisites to the client computer and calls the Windows Installer package (Client.msi) to install the client. You can't run Client.msi directly.  

 You can specify command-line properties for both CCMSetup.exe and Client.msi to modify the behavior of the client installation. Make sure that you specify CCMSetup properties (the properties that begin with **/**) before you specify Client.msi properties. For example:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`    

and the client installs by using the following properties:  

|Property|Description|  
|--------------|-----------------|  
|**/mp:SMSMP01**|This CCMSetup property specifies the management point SMSMP01 to download the required client installation files.|  
|**/logon**|This CCMSetup property specifies that the installation should stop if an existing Configuration Manager client is found on the computer.|  
|**SMSSITECODE=AUTO**|This Client.msi property specifies that the client tries to locate the Configuration Manager site code to use, for example, by using Active Directory Domain Services.|  
|**FSP=SMSFP01**|This Client.msi property specifies that the fallback status point named SMSFP01 is used to receive state messages sent from the client computer.|  

 For details on all CCMSetup.exe properties, see [About client installation properties](../../../core/clients/deploy/about-client-installation-properties.md)  

> [!Tip]  
> For the procedure to install the Configuration Manager client on a modern Windows 10 device using Azure AD identity, see [Install and assign Configuration Manager Windows 10 clients using Azure AD for authentication](/sccm/core/clients/deploy/deploy-clients-cmg-azure). That procedure is for clients on the intranet or the internet.  


### Examples
 These examples are for Active Directory clients on the intranet. They use the following values to represent different aspects of the site:  

 **MPSERVER** = server hosting the management point   
**FSPSERVER** = server hosting the fallback status point  
**ABC** = site code  
**contoso.com** = domain name  

 All site system servers are configured with an intranet FQDN. The site is published to the client's Active Directory forest.  

 On the client computer, log on as a local administrator, map a drive (z:) to\\\MPSERVER\SMS_ABC\Client, switch the command prompt to the z drive, and then run one of the following commands:  

 **Example 1:**  

`CCMSetup.exe`  

This example installs the client with no additional properties. The client is automatically configured with the client installation properties published to Active Directory Domain Services. It is automatically configured for the following settings: 
- Site code. This setting requires the client's network location to be included in a boundary group that is configured for client assignment. 
- Management point
- Fallback status point
- Communicate using HTTPS only  
  
For more information, see [About client installation properties published to Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Example 2:**  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
This example overrides the automatic configuration that Active Directory Domain Services provides. It doesn't require that the client's network location is included in a boundary group that is configured for client assignment. Instead, the installation specifies the following settings:
- Site code
- Intranet management point 
- Internet-based management point
- Fallback status point that accepts connections from the internet
- Use a client PKI certificate (if available) that has the longest validity period  



##  <a name="BKMK_ClientLogonScript"></a> How to install clients with logon scripts  
 Configuration Manager supports logon scripts to install the Configuration Manager client software. You can use the program file **CCMSetup.exe** in a logon script to trigger the client installation.  

 Logon script installation uses the same methods as manual client installation. You can specify the **/logon** installation property for CCMSsetup.exe. If any version of the client already exists on the computer, this property prevents the client from installing. This behavior prevents reinstallation of the client from taking place each time the logon script runs.  

 If no installation source is specified by the **/Source** property, and no management point from which to obtain installation is specified by the **/MP** property, CCMSetup.exe locates the management point by searching Active Directory Domain Services. This behavior only occurs if the schema has been extended for Configuration Manager, and the site is published to Active Directory Domain Services. Alternatively, the client can use DNS or WINS to locate a management point.  



##  <a name="BKMK_ClientApp"></a> How to install clients with a package and program  
 You can use Configuration Manager to create and deploy a package and program that upgrades the client software for selected computers in your hierarchy. A package definition file that populates the package properties with typically used values is supplied with Configuration Manager. You can customize the behavior of the client installation by specifying additional command-line properties.  

> [!NOTE]  
>  You cannot upgrade  Configuration Manager 2007 clients with this method. Instead, use automatic client upgrade, which automatically creates and deploys a package that contains the latest version of the client. For more information, see [Upgrade clients](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  For more information about how to migrate from older versions of the Configuration Manager client, see [Planning a client migration strategy](../../../core/migration/planning-a-client-migration-strategy.md).  

 
### Create a package and program for the client software  

Use the following procedure to create a Configuration Manager package and program that you can deploy to Configuration Manager client computers to upgrade the client software.  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Packages**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Package from Definition**.  

4.  On the **Package Definition** page of the wizard, select **Microsoft** from the **Publisher** drop-down list, and select **Configuration Manager Client Upgrade** from the **Package definition** list.  

5.  On the **Source Files** page, select **Always obtain files from a source folder**.  

6.  On the **Source Folder** page, select **Network path (UNC Name)**. Then enter the network path to the computer and folder that contains the client installation files.  

    > [!NOTE]  
    >  The computer on which the Configuration Manager deployment runs must have access to the network folder that you specify, otherwise, the installation fails.  

    To change any of the client installation properties, modify the CCMSetup.exe command-line parameters on the **General** tab of the **Configuration Manager agent silent upgrade Properties** program dialog box. The default installation properties are **/noservice SMSSITECODE=AUTO**.  

9. Distribute the package to all distribution points that you want to host the client upgrade package. You can then deploy the package to computer collections that contain clients that you want to upgrade.  



## <a name="bkmk_mdm"></a>How to install clients to Intune MDM-managed Windows devices

You can deploy the client installation files to computers that are enrolled with Microsoft Intune. 

This procedure is for a traditional client that is connected to the intranet. It uses traditional client authentication methods. To ensure the device remains in a managed state after the client software is installed, the device must be on the intranet and within a Configuration Manager site boundary.  

For the procedure to install the Configuration Manager client on a modern Windows 10 device using Azure AD identity, see [Install and assign Configuration Manager Windows 10 clients using Azure AD for authentication](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

> [!NOTE]
> Once the client software is installed, the device unenrolls from Intune.
> 
> Starting in version 1710, clients do not unenroll from Intune. They can have both the Configuration Manager client and MDM enrollment at the same time. For more information, see [Co-management](/sccm/core/clients/manage/co-management-overview).

###  Install clients with Intune:

1. In Intune, [create an app](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune) containing the Configuration Manager client installation file **ccmsetup.msi**. This file is found in the folder **&lt;ConfigMgr installation directory\>\bin\i386** on the Configuration Manager site server.

2. In the Intune Software Publisher, enter command-line parameters. For example, use the following command line with a traditional client on the intranet:

  `CCMSETUPCMD="/MP:&lt;FQDN of management point> SMSMP=&lt;FQDN of management point> SMSSITECODE=&lt;Your site code> DNSSUFFIX=&lt;DNS Suffix of management point>"`  

   > [!Note]  
   > For an example command line to use with a modern Windows 10 client using Azure AD authentication, see [Prepare Windows 10 devices for co-management](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).

3. [Deploy the app](/intune/deploy-use/deploy-apps-in-microsoft-intune) to the enrolled Windows computers.



##  <a name="BKMK_ClientImage"></a> How to install clients with a computer image  
You can preinstall the Configuration Manager client software on a reference computer that you use to create an OS image.   

> [!Important]
> When using the Configuration Manager task sequence to deploy the OS image, the [Prepare ConfigMgr Client](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) task sequence step completely removes the Configuration Manager client. 

### Prepare the client computer for imaging  

1.  Manually install the Configuration Manager client software on the reference computer. For more information, see [How to Install Configuration Manager Clients Manually](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Don't specify a Configuration Manager site code for the client in the CCMSetup.exe command-line properties.  

2.  At a command prompt, type `net stop ccmexec` to ensure that the **SMS Agent Host** service (Ccmexec.exe) is not running on the reference computer.
3.  Delete the file **SMSCFG.INI** from the **Windows** folder on the reference computer.  
3.  Remove any certificates that are stored in the local computer store on the reference computer. For example, if you use public key infrastructure (PKI) certificates, you must remove the certificates in the **Personal** store for **Computer** and **User** before you image the computer.

4.  If the clients are installed in a different Configuration Manager hierarchy than the reference computer, remove the trusted root key from the reference computer.  
    > [!NOTE]  
    >  If clients cannot query Active Directory Domain Services to locate a management point, they use the trusted root key to determine trusted management points. If all imaged clients are deployed in the same hierarchy as the master computer, leave the trusted root key in place. If the clients are deployed in different hierarchies, remove the trusted root key. Also provision these clients with the new trusted root key. For more information, see [Planning for the trusted root key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK). 

5.  Use your imaging software to capture the image of the master computer.  

6.  Deploy the image to destination computers.  



##  <a name="BKMK_ClientWorkgroup"></a> How to install clients on workgroup computers  
 Configuration Manager supports client installation for computers in workgroups. Install the client on workgroup computers by using the method specified in [How to Install Configuration Manager Clients Manually](#BKMK_Manual).  

 Prerequisites:  

-   The client must be installed manually on each workgroup computer. During installation, the logged-on user must have local administrator rights.  

-   In order to access resources in the Configuration Manager site server domain, the Network Access Account must be configured for the site. Specify this account as a software distribution component property. For more information, see [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

 Limitations:  

-   Workgroup clients cannot locate management points from Active Directory Domain Services, and instead must use DNS, WINS, or another management point.  

-   Global roaming is not supported, because clients cannot query Active Directory Domain Services for site information.  

-   Active Directory discovery methods cannot discover computers in workgroups.  

-   You cannot deploy software to users of workgroup computers.  

-   You cannot use the client push installation method to install the client on workgroup computers.  

-   Workgroup clients cannot use Kerberos for authentication and might require manual approval.  

-   A workgroup client cannot be configured as a distribution point. Configuration Manager requires that distribution point computers be members of a domain.  

### Install the client on workgroup computers  

Check the prerequisites, then follow the directions in the section [How to install Configuration Manager clients manually](#BKMK_Manual).  

   This example installs the client for intranet client management and specifies the site code and DNS suffix to locate a management point. `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     

   This example requires the client to be on a network location that is configured in a boundary group. This requirement is for automatic site assignment to succeed. The command includes a fallback status point on server FSPSERVER. This property helps track client deployment, and to identify any client communication issues. 
   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> How to install clients for internet-based client management  
 
> [!Note]
> This section doesn't apply to clients using a [cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway). To install internet-based clients using a cloud management gateway, see [Install and assign Configuration Manager Windows 10 clients using Azure AD for authentication](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

When the Configuration Manager site supports [internet-based client management](/sccm/core/clients/manage/plan-internet-based-client-management) for clients that are sometimes on the intranet, and sometimes on the internet, you have two options when you install clients on the intranet:  

-   You can include the Client.msi property of CCMHOSTNAME=*&lt;internet FQDN of the internet-based management point\>* when you install the client, for example by using manual installation or client push. When you use this method, you must also directly assign the client to the site and cannot use automatic site assignment. The [How to install Configuration Manager clients manually](#BKMK_Manual) section in this topic provides an example of this configuration method.  

-   You can install the client for intranet client management, and then assign an internet-based client management point to the client. Change the management point by using the Configuration Manager client properties in Control Panel, or by using a script. When you use this method, you can use automatic client assignment. For more information, see the [How to configure clients for internet-based client management after client installation](#BKMK_ConfigureIBCM_MP) section in this topic.  

 If you must install clients that are on the internet, choose one of the following supported methods:  

-   Provide a mechanism for these clients to temporarily connect to the intranet with a VPN. Then install the client by using any appropriate client installation method.  

-   Use an installation method that is independent from Configuration Manager. For example, package the client installation source files onto removable media that you can send to users to install with instructions. The client installation source files are located in the *&lt;InstallationPath\>*\Client folder on the Configuration Manager site server and management points. Include on the media a script to manually copy over the client folder and from this folder, install the client by using CCMSetup.exe and all the appropriate CCMSetup command-line properties.  

> [!NOTE]  
>  Configuration Manager doesn't support installing a client directly from the internet-based management point or from the internet-based software update point.  

 Clients that are managed over the internet must communicate with internet-based site systems. Ensure that these clients also have public key infrastructure (PKI) certificates before you install the client. Install these certificates independently from Configuration Manager. For more information about the certificate requirements, see [PKI certificate requirements](../../../core/plan-design/network/pki-certificate-requirements.md).  

### Install clients on the internet by specifying CCMSetup command-line properties  

1.  Follow the directions in the section [How to install Configuration Manager clients manually](#BKMK_Manual) and always include the following:  

    -   CCMSetup command-line property **/source:***&lt;local path to the copied Client folder\>*  

    -   CCMSetup command-line property **/UsePKICert**  

    -   Client.msi property **CCMHOSTNAME=***&lt;FQDN of internet-based management point\>*  

    -   Client.msi property **SMSSIGNCERT=***&lt;local path to exported site server signing certificate\>*  

    -   Client.msi property **SMSSITECODE=***&lt;site code of internet-based management point\>*  

    > [!NOTE]  
    >  If the site has more than one internet-based management point, it doesn't matter which internet-based management point you specify for the CCMHOSTNAME property. When a Configuration Manager client connects to the specified internet-based management point, the management point sends the client a list of available internet-based management points in the site. The client randomly selects one from the list.  

2.  If you do not want the client to check the certificate revocation list (CRL), specify the CCMSetup command-line property **/NoCRLCheck**.  

3.  If you are using an internet-based fallback status point, specify the Client.msi property **FSP=***&lt;internet FQDN of the internet-based fallback status point\>*.  

4.  If you are installing the client for internet-only client management, specify the Client.msi property **CCMALWAYSINF=1**.  

5.  Verify whether you have to specify additional CCMSetup command-line properties. For example, you might have to specify a certificate selection criterion if the client has more than one valid PKI certificate. For a list of available properties, see [About client installation properties](../../../core/clients/deploy/about-client-installation-properties.md).  

   Example:  
   `CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

   This example installs the client with the following behaviors:
   - Use source files from a folder on the D drive
   - Use a client PKI certificate 
   - Select the certificate with the longest validity period 
   - Internet-only client management
   - Assign the client to use the internet-based management point named SERVER1
   - Assign the internet-based fallback status point in the contoso.com domain
   - Assign the client to the ABC site  

###  <a name="BKMK_ConfigureIBCM_MP"></a>To configure clients for internet-based client management after client installation  
 To assign the internet-based management point after the client is installed, use one of these procedures. The first requires manual configuration and is appropriate for a few clients. The second is more appropriate for configuring many clients.  

#### Configure clients for internet-based client management after client installation by assigning the internet-based management point in Configuration Manager properties  

1.  Navigate to **Configuration Manager** in the Control Panel of the client computer, and then double-click to open its properties.  

2.  On the **Internet** tab, enter the fully qualified domain name of the internet-based management point in the internet FQDN text box.  

    > [!NOTE]  
    >  The **Internet** tab is only available if the client has a client PKI certificate.  

3.  If the client accesses the internet by using a proxy server, enter the proxy server settings.  

#### Configure clients for internet-based client management after client installation by using a script  

1.  Open a text editor, such as Notepad.  

2.  Copy and insert the following VBScript sample into the file. Replace *mp.contoso.com* with the internet FQDN of your internet-based management point.  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the internet-based management point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  If you have to delete a specified internet-based management point so that the client isn't configured to use an internet-based management point, remove the value inside the quotation marks so that this line becomes: `newInternetBasedManagementPointFQDN = ""`  

4.  Save the file with a .vbs extension.  

5.  Use cscript.exe to run the script on client computers, by using one of the following methods:  

    -   Deploy the file to existing Configuration Manager clients by using a package and a program.  

    -   Run the file locally on existing Configuration Manager clients by double-clicking the script file in Windows Explorer.  

 You might have to restart the client for the changes to take effect.  



##  <a name="BKMK_Provision"></a> How to provision client installation properties (group policy and software update-based client installation)  
 You can use Windows group policy to provision computers with Configuration Manager client installation properties. These properties are stored in the registry of the computer and are read when the client software is installed. This procedure isn't normally required, but might be needed for some client installation scenarios, such as:  

-   You're using the group policy settings or software update-based client installation methods. You haven't extended the Active Directory schema for Configuration Manager.  

-   You want to override client installation properties on specific computers.  

> [!NOTE]  
>  If any installation properties are supplied on the CCMSetup.exe command line, installation properties provisioned on computers aren't used.  

 A group policy administrative template named ConfigMgrInstallation.adm is supplied on the Configuration Manager installation media. This template can be used to provision client computers with installation properties.   

### Configure and assign client installation properties by using a group policy Object  

1.  Import the administrative template ConfigMgrInstallation.adm into a new or existing group policy object, by using an editor such as Windows Group Policy Object Editor. The file can be found in the folder **TOOLS\ConfigMgrADMTemplates** on the Configuration Manager installation media.  

2.  Open the properties of the imported setting **Configure Client Deployment Settings**.  

3.  Choose **Enabled**.  

4.  In the **CCMSetup** box, enter the required CCMSetup command-line properties. For a list of all CCMSetup command-line properties and examples of their use, see [About client installation properties](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Assign the group policy object to the computers that you want to provision with Configuration Manager client installation properties.  

For information about Windows group policy, refer to your Windows Server documentation.  



## Next steps
For more help installing the Configuration Manager client, see [Client installation methods](../../../core/clients/deploy/plan/client-installation-methods.md).