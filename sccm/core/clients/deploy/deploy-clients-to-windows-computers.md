---
title: "Deploy Windows clients| Microsoft Docs"
description: "Learn how to deploy clients to Windows computers in System Center Configuration Manager."
ms.custom: na
ms.date: 08/20/2017
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
author: robstackmsft
ms.author: robstack
manager: angrobe

---
# How to deploy clients to Windows computers in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Before you install Configuration Manager clients, ensure that all the [prerequisites](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) are in place and that you have completed all required deployment configurations.   

##  <a name="BKMK_ClientPush"></a> How to install clients with client push  

You can configure client push installation for a site, and client installation will automatically run on the computers that are discovered within the site's configured boundaries when those boundaries are configured as a boundary group. Or, you can initiate a client push installation by running the Client Push Installation Wizard for a specific collection or resource within a collection.  

You can also use the Client Push Installation Wizard to install the Configuration Manager client to [query](../../../core/servers/manage/queries-technical-reference.md) results. For installation to succeed, one of the items returned by the query must be the attribute **ResourceID** from the class **System Resource**.   

If the site server cannot contact the client computer or start the setup process, it automatically repeats the installation attempt every hour for up to 7 days.  

To help track the client installation process, install a fallback status point site system before you install the clients. When a fallback status point is installed, it is automatically assigned to clients when they are installed by the client push installation method. View the client deployment and assignment reports to track client installation progress. 

Client log files provide more detailed information for troubleshooting and do not require a fallback status point. For example, the CCM.log file on the site server records any problems that the site server has connecting to the computer, and the CCMSetup.log file on the client records the installation process.  

> [!IMPORTANT]  
>  For client push to succeed, ensure that all the prerequisites are in place. These are listed in the section "Installation Method Dependencies" in [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md).  

### To configure the site to automatically use client push for discovered computers

1.  In the Configuration Manager console, choose **Administration** > **Site Configuration** > **Sites**.  

3.  Select the site for which you want to configure automatic site-wide client push installation.  

4.  On the **Home** tab, in the **Settings** group, choose **Client Installation Settings** > **Client Push Installation**.  

5.  On the **General** tab of the **Client Push Installation Properties** dialog, select **Enable automatic site-wide client push installation**. Select the system types to which Configuration Manager should push the client software.  

6.  Select whether you want to install the client on domain controllers.  

7.  On the **Accounts** tab, specify one or more accounts for Configuration Manager to use when connecting to the computer to install the client software. Click the **Create** icon, enter the **User name** and **Password** (no more than 38 characters), confirm the password, and then click **OK**. You must specify at least one client push installation account, which must have local administrator rights on every computer on which you want to install the client. If you do not specify a client push installation account, Configuration Manager tries to use the site system computer account, which will cause cross-domain client push to fail.  
    > [!NOTE]  
    >  If you intend to use the client push installation method from a secondary site, the account must be specified at the secondary site that initiates the client push.  
    >   
    >  For more information about the client push installation account, see the next procedure, "To use the Client Push Installation Wizard".  
8.  Complete the **Installation Properties** tab.

     [Client installation properties](../../../core/clients/deploy/about-client-installation-properties.md) that are specified in this tab are published to Active Directory Domain Services if the schema is extended for Configuration Manager and read by client installations where CCMSetup is run without installation properties.  

    > [!NOTE]  
    >  If you enable client push installation on a secondary site, ensure that the SMSSITECODE property is set to the Configuration Manager site name of its parent primary site. If the Active Directory schema is extended for Configuration Manager, you can also set this to AUTO to automatically find the correct site assignment.  

### To use the Client Push Installation Wizard

1.  In the Configuration Manager console, choose **Administration** >  **Site Configuration** > **Sites**.  

3.  Select the site for which you want to configure automatic site-wide client push installation.  

4.  On the **Home** tab > **Settings** group, choose **Client Installation Settings** > **Client Push Installation**.  

5.  Complete the **Installation Properties** tab.  

     [Client installation properties](../../../core/clients/deploy/about-client-installation-properties.md) that are specified in this tab are published to Active Directory Domain Services if the schema is extended for Configuration Manager and read by client installations where CCMSetup is run without installation properties.  

6.  In the Configuration Manager console, choose **Assets and Compliance**.  

7.  In the **Assets and Compliance** workspace, select one or more computers, or a collection of computers.  

8.  On the **Home** tab, choose one of the following:  

    -   If you want to install the client to a single computer or multiple computers, in the **Device** group, choose **Install Client**.  

    -   If you want to install the client to a collection of computers, in the **Collection** group, choose **Install Client**.  

9. On the **Before You Begin** page of the **Install Client Wizard**, review the information, and then choose **Next**.  

10. Complete the **Installation options** page.  

11. Review the installation settings, and then close the wizard.  

> [!NOTE]  
>  You can use the wizard to install clients even if the site is not configured for client push.  

##  <a name="BKMK_ClientSUP"></a> How to install clients with software update-based installation  
 Software update-based client installation publishes the client to a software update point as a software update. Use this method for a first-time installation or upgrade.  

 If a computer has the client installed, Configuration Manager provides the client with the client policy, which includes the software update point server name and port from which to obtain software updates.   

> [!IMPORTANT]  
>  To use software update-based installation, you must use the same Windows Server Update Services (WSUS) server for client installation and software updates. This server must be the active software update point in a primary site. For more information, see [Install a software update point](../../../sum/get-started/install-a-software-update-point.md).  

If a computer does not have the Configuration Manager client installed, you must configure and assign a Group Policy Object (GPO) in Active Directory Domain Services to specify the software update point server name.  

You cannot add command-line properties to a software update-based client installation. If you have extended the Active Directory schema for Configuration Manager, client computers automatically query Active Directory Domain Services for installation properties when they install.  

If you have not extended the Active Directory schema, you can use Group Policy to provision client installation settings to computers in your site. These settings are automatically applied to any software update-based client installations. For more information, see [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](#BKMK_Provision) and [How to assign clients to a site in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

Use the following procedures to configure computers without a Configuration Manager client to use the software update point for client installation and software updates, and to publish the client software to the software update point.  

> [!NOTE]  
>  If computers are in a pending restart state following a previous software installation, then a software update based client installation might cause the computer to restart.  

### Configure a Group Policy Object in Active Directory Domain Services to specify the software update point for client installation and software updates:  

1.  Use the Group Policy Management Console to open a new or existing Group Policy Object.  

2.  In the console, expand **Computer Configuration**, expand **Administrative Templates**, expand **Windows Components**, and then choose **Windows Update**.  

3.  Open the properties of the setting **Specify intranet Microsoft update service location**, and then choose **Enabled**.  

4.  In the box **Set the intranet update service for detecting updates**, specify the name and port of the software update point server:  

    -   If the Configuration Manager site system is configured to use a fully qualified domain name (FQDN), use the FQDN format.  

    -   If the Configuration Manager site system is not configured to use a FQDN, use a short name format.  

    > [!NOTE]  
    >  To determine the port number, see [How to determine the port settings used by WSUS in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

     Example: **http://server1.contoso.com:8530**  

5.  In the box **Set the intranet statistics server**, specify the name of the intranet statistics server. It does not have to be the same as the software update point server, and the format does not have to match if it is the same server.  

6.  Assign the Group Policy Object to the computers on which you want to install the client and receive software updates.  

### To publish the Configuration Manager client to the software update point  

1.  In the Configuration Manager console, click **Administration** > **Site Configuration** > **Sites**.  

3.  Select the site for which you want to configure software update-based client installation.  

4.  On the **Home** tab, in the **Settings** group, choose **Client Installation Settings**, and then choose **Software Update-Based Client Installation**.  

5.  Select **Enable software update-based client installation**.  

6.  If the client software on the Configuration Manager site server is a later version than that on the software update point, the **Later Version of Client Package Detected** dialog box opens. Click **Yes** to publish the most recent version.  

    > [!NOTE]  
    >  If the client software wasn't previously published to the software update point, this box will be blank.  

The software update for the Configuration Manager client is not automatically updated when there is a new version. If you upgrade the site, which includes a new client version, you must repeat this procedure and click **Yes** for step 6.  

##  <a name="BKMK_ClientGP"></a> How to install clients with group policy  
 You can use Group Policy in Active Directory Domain Services to publish or assign the Configuration Manager client to install on computers in your enterprise. The client will install when the computer starts. When you use Group Policy, the client displays in the Control Panel **Add or Remove Programs** for the user to install.  

 Use the Windows Installer package (CCMSetup.msi) for Group Policy-based installations. This file is found in the folder **&lt;ConfigMgr installation directory\>\bin\i386** on the Configuration Manager site server. You cannot add properties to this file to modify installation behavior.  

> [!IMPORTANT]  
>  You must have Administrator permissions to access the client installation files.  

-   If the Active Directory schema is extended for Configuration Manager and **Publish this site in Active Directory Domain Services** is selected in the **Advanced** tab of the **Site Properties** dialog box, client computers automatically search Active Directory Domain Services for installation properties. For more information about the installation properties that are published, see [About client installation properties published to Active Directory Domain Services in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   If the Active Directory schema has not been extended, you can use the  procedure in this topic to store installation properties in the registry of computers: [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](#BKMK_Provision). These installation properties will be used when the client is installed.  

For information about how to use Group Policy in Active Directory Domain Services to install software, refer to your Windows Server documentation.  

##  <a name="BKMK_Manual"></a> How to install clients manually  
 You can manually install the client software on computers in your enterprise by using the CCMSetup.exe program. This program and its supporting files can be found in the **Client** folder of the Configuration Manager installation folder on the site server and on management points in your site. This folder is shared to the network as  

 \\\\*&lt;Site Server Name\>*\SMS_*&lt;Site Code\>*\Client\  

 where *&lt;Site Server Name\>* is the name of one of the servers hosting a management point and *&lt;Site Code\>* is the code for primary site the client will belong to.  To run CCMSetup.exe from the command line on the client, you must map a network drive to this location, and then run the command.  

> [!IMPORTANT]  
>  You must have Administrator permissions to access the client installation files.  

 CCMSetup.exe copies all necessary prerequisites to the client computer and calls the Windows Installer package (Client.msi) to install the client. You cannot run Client.msi directly.  

 You can specify command-line properties for both CCMSetup.exe and Client.msi to modify the behavior of the client installation. Make sure that you specify CCMSetup properties (the properties that begin with **/**) before you specify Client.msi properties. For example:  

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

### Examples
 These examples are for Active Directory clients on the intranet and  use  the following values to represent different aspects of the site:  

 **MPSERVER** = server hosting the management point   
**FSPSERVER** = server hosting the fallback status point  
**ABC** = site code  
**contoso.com** = domain name  

 All site system servers are configured with an intranet FQDN and the site is published to the client's Active Directory forest.  

 On the client computer, log on as a local administrator, map a drive (z:) to\\\MPSERVER\SMS_ABC\Client, switch the command prompt to the z drive, and then run one of the following commands.  

 **Example 1:**  

```  
CCMSetup.exe  
```  
This example installs the client with no additional properties so that the client is automatically configured with the client installation properties published to Active Directory Domain Services. For example, the client is automatically configured for the site code (requires the client's network location to be included in a boundary group that is configured for client assignment), a management point, the fallback status point, and whether the client must communicate by using HTTPS only. For more information about the client installation properties that can be automatically configured for Active Directory clients, see [About client installation properties published to Active Directory Domain Services in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Example 2:**  

```  
CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com  
```  
This example overrides the automatic configuration that Active Directory Domain Services can provide and does not require that the client's network location is included in a boundary group that is configured for client assignment. Instead, the installation specifies the site, an intranet management point and an Internet-based management point, a fallback status point that accepts connections from the Internet, and to use a client PKI certificate (if available) that has the longest validity period.  

##  <a name="BKMK_ClientLogonScript"></a> How to install clients with logon scripts  
 Configuration Manager supports logon scripts to install the Configuration Manager client software. You can use the program file **CCMSetup.exe** in a logon script to trigger the client installation.  

 Logon script installation uses the same methods as manual client installation. You can specify the **/logon** installation property for CCMSsetup.exe, which prevents the client from installing if any version of the client already exists on the computer. This prevents reinstallation of the client from taking place each time the logon script runs.  

 If no installation source is specified that is using the **/Source** property and no management point from which to obtain installation is specified by using the **/MP** property, CCMSetup.exe can locate the management point by searching Active Directory Domain Services if the schema has been extended for Configuration Manager and the site is published to Active Directory Domain Services. Alternatively, the client can use DNS or WINS to locate a management point.  

##  <a name="BKMK_ClientApp"></a> How to install clients with a package and program  
 You can use Configuration Manager to create and deploy a package and program that upgrades the client software for selected computers in your hierarchy. A package definition file that populates the package properties with typically used values is supplied with Configuration Manager. You can customize the behavior of the client installation by specifying additional command line properties.  

> [!NOTE]  
>  You cannot upgrade  Configuration Manager 2007 clients with this method. Instead, use automatic client upgrade, which automatically creates and deploys a package that contains the latest version of the client. For more information, see [Upgrade clients in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  For more information about how to migrate from older versions of the Configuration Manager client, see [Planning a client migration strategy in System Center Configuration Manager](../../../core/migration/planning-a-client-migration-strategy.md).  

 
###To create a package and program for the client software  

Use the following procedure to create a Configuration Manager package and program that you can deploy to Configuration Manager client computers to upgrade the client software.  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Packages**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Package from Definition**.  

4.  On the **Package Definition** page of the wizard, select **Microsoft** from the **Publisher** drop-down list, and select **Configuration Manager Client Upgrade** from the **Package definition** list.  

5.  On the **Source Files** page, select **Always obtain files from a source folder**.  

6.  On the **Source Folder** page, select **Network path (UNC Name)** and enter the network path to the computer and folder that contains the client installation files.  

    > [!NOTE]  
    >  The computer on which the Configuration Manager deployment runs must have access to the network folder that you specify, otherwise, the installation will fail.  

    If you want to change any of the client installation properties, you can modify the CCMSetup.exe command line parameters on the **General** tab of the **Configuration Manager agent silent upgrade Properties** program dialog box. The default installation properties are **/noservice SMSSITECODE=AUTO**.  

9. Distribute the package to all distribution points that you want to host the client upgrade package. You can then deploy the package to computer collections that contain clients that you want to upgrade.  

## How to install clients to Intune MDM-managed Windows devices

You can deploy the client installation files to computers that are enrolled with Microsoft Intune. 

To ensure the device remains in a managed state after the client software is installed, the device must be on the corporate network and within a Configuration Manager site boundary. 

> [!NOTE]
> Once the client software is installed, the device will be unenrolled from Intune.

### To install clients with Intune:

1. In Intune, [create an app](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune) containing the Configuration Manager client installation file **ccmsetup.msi**.

2. In the Intune Software Publisher, use the following command line parameters:

  **CCMSETUPCMD="/MP:&lt;FQDN of management point> SMSMP=&lt;FQDN of management point> SMSSITECODE=&lt;Your site code> DNSSUFFIX=&lt;DNS Suffix of management point>"**

3. [Deploy the app](/intune/deploy-use/deploy-apps-in-microsoft-intune) to the enrolled Windows computers.

##  <a name="BKMK_ClientImage"></a> How to install clients with a computer image  
You can preinstall the Configuration Manager client software on a master image computer that you will use to image other computers.   

### To prepare the client computer for imaging  

1.  Manually install the Configuration Manager client software on the master image computer. For more information, see [How to Install Configuration Manager Clients Manually](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Do not specify a Configuration Manager site code for the client in the CCMSetup.exe command-line properties.  

2.  At a command prompt, type **net stop ccmexec** to ensure that the **SMS Agent Host** service (Ccmexec.exe) is not running on the master image computer.
3.  Delete the file **SMSCFG.INI** from the **Windows** folder on the reference computer.  
3.  Remove any certificates that are stored in the local computer store on the master image computer.  For example, if you use public key infrastructure (PKI) certificates, you must remove the certificates in the **Personal** store for **Computer** and **User** before you image the computer.

4.  If the clients will be installed in a different Configuration Manager hierarchy than the master image computer, remove the Trusted Root Key from the master image computer.  
    > [!NOTE]  
    >  If clients cannot query Active Directory Domain Services to locate a management point, they use the trusted root key to determine trusted management points. If all imaged clients will be deployed in the same hierarchy as the master computer, leave the trusted root key in place. If the clients will be deployed in different hierarchies, remove the trusted root key and as a best practice, preprovision these clients with the new trusted root key. For more information, see  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK). 

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

### To install the client on workgroup computers  

Check the prerequisites, then follow the directions in the section [How to Install Configuration Manager Clients Manually](#BKMK_Manual).  

   This example installs the client for intranet client management and specifies the site code and DNS suffix to locate a management point: `**CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com**`  

     

   This example requires the client to be on a network location that is configured in a boundary group so that automatic site assignment can succeed. The command includes a fallback status point on server FSPSERVER, to help track client deployment and to identify any client communication issues: `**CCMSetup.exe FSP=fspserver.constoso.com**`  

      

##  <a name="BKMK_ClientInternet"></a> How to install clients for Internet-based client management  
 When the Configuration Manager site supports Internet-based client management for clients that are sometimes on the intranet, and sometimes on the Internet, you have two options when you install clients on the intranet:  

-   You can include the Client.msi property of CCMHOSTNAME=*&lt;Internet FQDN of the Internet-based management point\>* when you install the client, for example by using manual installation or client push. When you use this method, you must also directly assign the client to the site and cannot use automatic site assignment. The [How to Install Configuration Manager Clients Manually](#BKMK_Manual) section in this topic provides an example of this configuration method.  

-   You can install the client for intranet client management, and then assign an Internet-based client management point to the client by using the Configuration Manager client properties in Control Panel, or by using a script. When you use this method, you can use automatic client assignment. For more information, see the [How to Configure Clients for Internet-based Client Management after Client Installation](#BKMK_ConfigureIBCM_MP) section in this topic.  

 If you must install clients that are on the Internet either because they are Internet-only clients, or because you must install them before they come back into the intranet, choose one of the following supported methods:  

-   Provide a mechanism for these clients to temporarily connect to the intranet with a virtual private network (VPN), and then install them by using any appropriate client installation method.  

-   Use an installation method that is independent from Configuration Manager, such as packaging the client installation source files onto removable media that you can send to users to install with instructions. The client installation source files are located in the *&lt;InstallationPath\>*\Client folder on the Configuration Manager site server and management points. Include on the media a script to manually copy over the client folder and from this folder, install the client by using CCMSetup.exe and all the appropriate CCMSetup command-line properties.  

> [!NOTE]  
>  Configuration Manager does not support installing a client directly from the Internet-based management point or from the Internet-based software update point.  

 Because clients that are managed over the Internet must communicate with Internet-based site systems, ensure that these clients also have public key infrastructure (PKI) certificates installed before you install them. You must install these certificates independently from Configuration Manager. For more information about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

### To install clients on the Internet by specifying CCMSetup command-line properties  

1.  Follow the directions in the section [How to Install Configuration Manager Clients Manually](#BKMK_Manual) and always include the following:  

    -   CCMSetup command-line property **/source:***&lt;local path to the copied Client folder\>*  

    -   CCMSetup command-line property **/UsePKICert**  

    -   Client.msi property **CCMHOSTNAME=***&lt;FQDN of Internet-based management point\>*  

    -   Client.msi property **SMSSIGNCERT=***&lt;local path to exported site server signing certificate\>*  

    -   Client.msi property **SMSSITECODE=***&lt;site code of Internet-based management point\>*  

    > [!NOTE]  
    >  If the site has more than one Internet-based management point, it does not matter which Internet-based management point you specify for the CCMHOSTNAME property. When a Configuration Manager client connects to the specified Internet-based management point, the management point sends the client a list of available Internet-based management points in the site, and the client randomly selects one from the list.  

2.  If you do not want the client to check the certificate revocation list (CRL), specify the CCMSetup command-line property **/NoCRLCheck**.  

3.  If you are using an Internet-based fallback status point, specify the Client.msi property **FSP=***&lt;Internet FQDN of the Internet-based fallback status point\>*.  

4.  If you are installing the client for Internet-only client management, specify the Client.msi property **CCMALWAYSINF=1**.  

5.  Verify whether you have to specify additional CCMSetup command-line properties. For example, you might have to specify a certificate selection criterion if the client has more than one valid PKI certificate. For a list of available properties, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

   Example: `**CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1**`  

   This example installs the client source files from a folder on the D drive with settings to use a client PKI certificate and select the certificate with the longest validity period for Internet-only client management, assigns the client to use the Internet-based management point named SERVER1 and the Internet-based fallback status point in the contoso.com domain, and assigns the client to the ABC site.  

###  <a name="BKMK_ConfigureIBCM_MP"></a>To configure clients for Internet-based Client Management after client installation  
 To assign the Internet-based management point after the client is installed, use one of the following procedures. The first requires manual configuration and is appropriate for a few clients. The second is more appropriate for configuring many clients.  

#### To configure clients for Internet-based client management after client installation by assigning the Internet-based management point in Configuration Manager Properties  

1.  Navigate to **Configuration Manager** in the Control Panel of the client computer, and then double-click to open its properties.  

2.  On the **Internet** tab, enter the fully qualified domain name of the Internet-based management point in the Internet FQDN text box.  

    > [!NOTE]  
    >  The **Internet** tab is only available if the client has a client PKI certificate.  

3.  Enter proxy server settings if the client will access the Internet by using a proxy server.  

#### To configure clients for Internet-based client management after client installation by using a script  

1.  Open a text editor, such as Notepad.  

2.  Copy and insert the following into the file. Replace *mp.contoso.com* with the Internet FQDN of your Internet-based management point.  

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

    > [!NOTE]  
    >  If you have to delete a specified Internet-based management point so that the client is not configured to use an Internet-based management point, remove the value inside the quotation marks so that this line becomes **newInternetBasedManagementPointFQDN = ""**.  

4.  Save the file with a .vbs extension.  

5.  Use cscript to run the script on client computers, by using one of the following methods:  

    -   Deploy the file to existing Configuration Manager clients by using a package and a program.  

    -   Run the file locally on existing Configuration Manager clients by double-clicking the script file in Windows Explorer.  

 You might have to restart the client for the changes to take effect.  

##  <a name="BKMK_Provision"></a> How to provision client installation properties (group policy and software update-based client installation)  
 You can use Windows Group Policy to provision computers with Configuration Manager client installation properties. These properties are stored in the registry of the computer and are read when the client software is installed. This procedure would not normally be required, but might be needed for some client installation scenarios, such as:  

-   You are using the Group Policy settings or software update-based client installation methods, and you have not extended the Active Directory schema for Configuration Manager.  

-   You want to override client installation properties on specific computers.  

> [!NOTE]  
>  If any installation properties are supplied on the CCMSetup.exe command line, installation properties provisioned on computers will not be used.  

 A Group Policy administrative template named ConfigMgrInstallation.adm is supplied on the Configuration Manager installation media, which can be used to provision client computers with installation properties.   

### To configure and assign client installation properties by using a Group Policy Object  

1.  Import the administrative template ConfigMgrInstallation.adm into a new or existing Group Policy Object, by using an editor such as Windows Group Policy Object Editor. The file can be found in the folder **TOOLS\ConfigMgrADMTemplates** on the Configuration Manager installation media.  

2.  Open the properties of the imported setting **Configure Client Deployment Settings**.  

3.  Choose **Enabled**.  

4.  In the **CCMSetup** box, enter the required CCMSetup command-line properties. For a list of all CCMSetup command-line properties and examples of their use, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Assign the Group Policy Object to the computers that you want to provision with Configuration Manager client installation properties.  

For information about Windows Group Policy, refer to your Windows Server documentation.  

## Next steps
For more help installing the Configuration Manager client, see [Client installation methods in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).