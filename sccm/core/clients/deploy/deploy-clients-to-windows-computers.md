---
title: Deploy clients to Windows
titleSuffix: Configuration Manager
description: Learn how to deploy the Configuration Manager client to Windows computers.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to deploy clients to Windows computers in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article provides details on how to deploy the Configuration Manager client to Windows computers. For more information on planning and preparing for client deployment, see the following articles:
- [Client installation methods](/sccm/core/clients/deploy/plan/client-installation-methods)  
- [Prerequisites for deploying clients to Windows computers](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers)   
- [Security and privacy for Configuration Manager clients](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  
- [Best practices for client deployment](/sccm/core/clients/deploy/plan/best-practices-for-client-deployment)  



##  <a name="BKMK_ClientPush"></a> Client push installation 

There are three main ways to use client push:  

- When you configure client push installation for a site, client installation automatically runs on computers that the site discovers. This method is scoped to the site's configured boundaries when those boundaries are configured as a boundary group.  

- Start client push installation by running the Client Push Installation Wizard for a specific collection or resource within a collection.  

- Use the Client Push Installation Wizard to install the Configuration Manager client to [query](/sccm/core/servers/manage/queries-technical-reference) results. For installation to succeed, one of the items returned by the query must be the **ResourceID** attribute from the **System Resource** class.   

If the site server can't contact the client computer or start the setup process, it automatically retries the installation every hour. The server continues to retry for up to seven days.  

To help track the client installation process, install a fallback status point before you install the clients. When you install a fallback status point, it's automatically assigned to clients when they're installed by the client push installation method. To track client installation progress, view the client deployment and assignment reports. 

Client log files provide more detailed information for troubleshooting. The log files don't require a fallback status point. For example, the **CCM.log** file on the site server records any problems from the site server when connecting to the computer. The **CCMSetup.log** file on the client records the installation process.  

> [!IMPORTANT]  
>  For client push to succeed, make sure that all the prerequisites are in place. For more information, see [Installation method dependencies](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies).  


### Configure the site to automatically use client push for discovered computers

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.  

2.  Select the site for which you want to configure automatic site-wide client push installation.  

3.  On the **Home** tab of the ribbon, in the **Settings** group, choose **Client Installation Settings**, and select **Client Push Installation**.  

4.  On the **General** tab of the Client Push Installation Properties window, select **Enable automatic site-wide client push installation**.   

5. Starting in version 1806, when you update the site, it enables a Kerberos check for client push. The option to **Allow connection fallback to NTLM** is enabled by default, which is consistent with previous behavior. If the site can't authenticate the client using Kerberos, it retries the connection using NTLM. The recommended configuration for improved security is to disable this setting, which requires Kerberos without NTLM fallback.<!--1358204-->  

    > [!Note]  
    > When using client push to install the Configuration Manager client, the site server creates a remote connection to the client. Starting in version 1806, the site can require Kerberos mutual authentication by not allowing fallback to NTLM before establishing the connection. This enhancement helps to secure the communication between the server and the client.  
    > 
    > Depending on your security policies, your environment may already prefer or require Kerberos over older NTLM authentication. For more information on the security considerations of these authentication protocols, see the [Windows security policy setting to restrict NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).  
    > 
    > To use this feature, clients must be in a trusted Active Directory forest. Kerberos in Windows relies upon Active Directory for mutual authentication.  

6.  Select the system types to which Configuration Manager should push the client software. Select whether you want to install the client on domain controllers.  

7.  On the **Accounts** tab, specify one or more accounts for Configuration Manager to use when connecting to the target computer. Click the **Create** icon, enter the **User name** and **Password** (no more than 38 characters), confirm the password, and then click **OK**. Specify at least one client push installation account. This account must have local Administrator rights on the target computer to install the client. If you don't specify a client push installation account, Configuration Manager tries to use the site system computer account. Cross-domain client push fails when using the site system computer account.  

    > [!NOTE]  
    >  To use client push from a secondary site, specify the account at the secondary site that initiates the client push.  
    >   
    >  For more information about the client push installation account, see the next procedure, [Use the Client Push Installation Wizard](#use-the-client-push-installation-wizard).  

8.  Complete the **Installation Properties** tab.

     If you've extended the Active Directory schema for Configuration Manager, the site publishes the specified [Client installation properties](/sccm/core/clients/deploy/about-client-installation-properties) to Active Directory Domain Services. When CCMSetup runs without installation properties, it reads these properties from Active Directory.  

    > [!NOTE]  
    >  If you enable client push installation on a secondary site, set the **SMSSITECODE** property to the Configuration Manager site code of its parent primary site. If you've extended the Active Directory schema for Configuration Manager, to automatically find the correct site assignment, set this property to **AUTO**.  


### Use the client push installation wizard

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.  

2.  Select the site for which you want to configure automatic site-wide client push installation.  

3.  On the **Home** tab of the ribbon, in the **Settings** group, choose **Client Installation Settings**, and select **Client Push Installation**.  

4.  Complete the **Installation Properties** tab.  

    If you've extended the Active Directory schema for Configuration Manager, the site publishes the specified [Client installation properties](/sccm/core/clients/deploy/about-client-installation-properties) to Active Directory Domain Services. When CCMSetup runs without installation properties, it reads these properties from Active Directory.   

5.  In the Configuration Manager console, go to the **Assets and Compliance** workspace.  

6.  In the **Devices** node, select one or more computers. Or select a collection of computers in the **Device Collections** node.  

7.  On the **Home** tab of the ribbon, choose one of the following options:  

    -   To push the client to one or more devices, in the **Device** group, choose **Install Client**.  

    -   To push the client to a collection of devices, in the **Collection** group, choose **Install Client**.  

8. On the **Before You Begin** page of the Install Client Wizard, review the information, and then choose **Next**.  

9. Complete the **Installation options** page.  

10. Review the installation settings, and then complete the wizard.  

> [!NOTE]  
> Use this wizard to install clients even if the site isn't configured for client push.  



##  <a name="BKMK_ClientSUP"></a> Software update-based installation  

Software update-based client installation publishes the client to a software update point as a software update. Use this method for a first-time installation or upgrade.  

If a computer has the Configuration Manager client installed, it receives client policy from the site. This policy includes the software update point server name and port from which to get software updates.   

> [!IMPORTANT]  
>  For software update-based installation, use the same Windows Server Update Services (WSUS) server for client installation and software updates. This server must be the active software update point in a primary site. For more information, see [Install a software update point](/sccm/sum/get-started/install-a-software-update-point).  

If a computer doesn't have the Configuration Manager client installed, configure and assign a group policy object. This group policy specifies the server name of the software update point.  

You can't add command-line properties to a software update-based client installation. If you've extended the Active Directory schema for Configuration Manager, the client install automatically queries Active Directory Domain Services for the installation properties.  

If you haven't extended the Active Directory schema, use group policy to provision client installation settings. These settings are automatically applied to any software update-based client installation. For more information, see the section on [How to provision client installation properties](#BKMK_Provision) and the article on [How to assign clients to a site](/sccm/core/clients/deploy/assign-clients-to-a-site).  

Use the following procedures to configure computers without a Configuration Manager client to use the software update point. There's also a procedure to publish the client software to the software update point.  

> [!Tip]  
>  If computers are in a pending restart state following a previous software installation, then a software update-based client installation might cause the computer to restart.  


### Configure a group policy object to specify the software update point  

1.  Use the **Group Policy Management Console** to open a new or existing group policy object.  

2.  Expand **Computer Configuration**, expand **Administrative Templates**, expand **Windows Components**, and then choose **Windows Update**.  

3.  Open the properties of the setting **Specify intranet Microsoft update service location**, and then choose **Enabled**.  

4.  **Set the intranet update service for detecting updates**: Specify the name and port of the software update point server.  

    -   If you've configured the Configuration Manager site system to use a fully qualified domain name (FQDN), use this format.  

    -   If the Configuration Manager site system isn't configured to use an FQDN, use a short name format.   

    > [!Tip]  
    >  To determine the port number, see [How to determine the port settings used by WSUS](/sccm/sum/plan-design/plan-for-software-updates).  

     Example with FQDN format: `http://server1.contoso.com:8530`  

5.  **Set the intranet statistics server**: This setting is typically the same server name.   

6.  Assign the group policy object to the computers on which you want to install the client and receive software updates.  


### Publish the Configuration Manager client to the software update point  

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.  

2.  Select the site for which you want to configure software update-based client installation.  

3.  On the **Home** tab of the ribbon, in the **Settings** group, choose **Client Installation Settings**, and then choose **Software Update-Based Client Installation**.  

4.  Select **Enable software update-based client installation**.  

5.  If the site's client version is more recent than the version on the software update point, the **Later Version of Client Package Detected** dialog box opens. Click **Yes** to publish the most recent version.  

    > [!NOTE]  
    >  If you haven't already published the client software to the software update point, this box is blank.  

The software update for the Configuration Manager client isn't automatically updated when there's a new version. When you update the site, repeat this procedure to update the client.  



##  <a name="BKMK_ClientGP"></a> Group policy installation 

Use group policy in Active Directory Domain Services to publish or assign the Configuration Manager client. The client installs when the computer starts. When you use group policy, the client displays in the **Add or Remove Programs** control panel for the user to install.  

Use the Windows Installer package **CCMSetup.msi** for group policy-based installations. This file is found in the folder `<ConfigMgr installation directory>\bin\i386` on the site server. You can't add properties to this file to modify installation behavior.  

> [!IMPORTANT]  
>  You must have **Administrator** permissions to access the client installation files.  

-   If you've extended the Active Directory schema for Configuration Manager, and you selected **Publish this site in Active Directory Domain Services** in the **Advanced** tab of the **Site Properties** dialog box, client computers automatically search Active Directory Domain Services for installation properties. For more information, see [About client installation properties published to Active Directory Domain Services](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services).  

-   If you haven't extended the Active Directory schema, to store installation properties in the Windows registry of computers, see the section on [How to provision client installation properties](#BKMK_Provision). The client uses these installation properties when it installs.  

For more information about how to use group policy in Active Directory Domain Services to install software, see [How to use group policy to remotely install software](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server).  



##  <a name="BKMK_Manual"></a> Manual installation

Manually install the client software on computers by using **CCMSetup.exe**. Find this program and its supporting files in the **Client** folder of the Configuration Manager installation folder on the site server. The site shares this folder to the network as:  

 `\\<Site Server Name>\SMS_<Site Code>\Client\`  

 where `<Site Server Name>` is the primary site server name, and `<Site Code>` is the primary site code to which the client is assigned. To run CCMSetup.exe from the command line on the client, connect to this network location, and then run the command.  

> [!IMPORTANT]  
>  You must have **Administrator** permissions to access the client installation files.  

CCMSetup.exe copies all necessary prerequisites to the client computer and calls the Windows Installer package (Client.msi) to install the client. You can't run Client.msi directly.  

To modify the behavior of the client installation, specify command-line options for both CCMSetup.exe and Client.msi. Make sure that you specify CCMSetup parameters that begin with `/` before you specify Client.msi properties. For example:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`    

The client installs in this example by using the following options:  

|Option|Description|  
|--------------|-----------------|  
|`/mp:SMSMP01`|This CCMSetup parameter specifies the management point SMSMP01 to download the required client installation files.|  
|`/logon`|This CCMSetup parameter specifies that the installation should stop if an existing Configuration Manager client is found on the computer.|  
|`SMSSITECODE=AUTO`|This Client.msi property specifies that the client tries to locate the Configuration Manager site code to use. For example, by using Active Directory Domain Services.|  
|`FSP=SMSFP01`|This Client.msi property specifies that the fallback status point named SMSFP01 is used to receive state messages sent from the client computer.|  

 For more information, see [About client installation parameters and properties](/sccm/core/clients/deploy/about-client-installation-properties).  

> [!Tip]  
> For the procedure to install the Configuration Manager client on a modern Windows 10 device using Azure AD identity, see [Install and assign Configuration Manager Windows 10 clients using Azure AD for authentication](/sccm/core/clients/deploy/deploy-clients-cmg-azure). That procedure is for clients on the intranet or the internet.  


### Manual installation examples

These examples are for Active Directory-joined clients on the intranet. They use the following values:  

- **MPSERVER**: server hosting the management point   
- **FSPSERVER**: server hosting the fallback status point  
- **ABC**: site code  
- **contoso.com**: domain name  

You've configured all site system servers with an intranet FQDN. You've published the site information to Active Directory.  

Start with the following steps on the client computer:  
1. Sign in as a local administrator  
2. Map drive Z: to `\\MPSERVER\SMS_ABC\Client`  
3. Switch the command prompt to the Z: drive  

Then run one of the following commands:  


#### Manual example 1  

`CCMSetup.exe`  

This example installs the client with no additional parameters or properties. The client automatically configures with the client installation properties published to Active Directory Domain Services, including the following settings:  

- Site code: This setting requires the client's network location to be included in a boundary group that you've configured for client assignment.  
- Management point
- Fallback status point
- Communicate using HTTPS only  

For more information, see [About client installation properties published to Active Directory Domain Services](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services).  


#### Manual example 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
This example overrides the automatic configuration that Active Directory Domain Services provides. It doesn't require that the client's network location is included in a boundary group that is configured for client assignment. Instead, the installation specifies the following settings:
- Site code
- Intranet management point 
- Internet-based management point
- Fallback status point that accepts connections from the internet
- Use a client PKI certificate (if available) that has the longest validity period  



##  <a name="BKMK_ClientLogonScript"></a> Logon script installation

Configuration Manager supports logon scripts to install the Configuration Manager client software. Use the program file **CCMSetup.exe** in a logon script to trigger the client installation.  

Logon script installation uses the same methods as manual client installation. Specify the `/logon` installation parameter for CCMSsetup.exe. If any version of the client already exists on the computer, this parameter prevents the client from installing. This behavior prevents reinstallation of the client each time the logon script runs.  

If you don't specify an installation source by the `/Source` parameter, and no management point from which to obtain installation is specified by the `/MP` parameter, CCMSetup.exe locates the management point by searching Active Directory Domain Services. This behavior only occurs if you've extended the schema for Configuration Manager, and you've published the site to Active Directory Domain Services. Alternatively, the client can use DNS or WINS to locate a management point.  



##  <a name="BKMK_ClientApp"></a> Package and program installation  

Use Configuration Manager to create and deploy a package and program that upgrades the client software for selected devices. Configuration Manager supplies a package definition file that populates the package properties with typically used values. Customize the behavior of the client installation by specifying additional command-line parameters and properties.  

> [!NOTE]  
>  You can't upgrade Configuration Manager 2007 clients with this method. Instead, use automatic client upgrade, which automatically creates and deploys a package that contains the latest version of the client. For more information, see [Upgrade clients](/sccm/core/clients/manage/upgrade/upgrade-clients).  
>   
>  For more information about how to migrate from older versions of the Configuration Manager client, see [Planning a client migration strategy](/sccm/core/migration/planning-a-client-migration-strategy).  

 
### Create a package and program for the client software  

Use the following procedure to create a Configuration Manager package and program that you can deploy to Configuration Manager client computers to upgrade the client software.  

1.  In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Packages** node.  

2.  On the **Home** tab of the ribbon, in the **Create** group, choose **Create Package from Definition**.  

3.  On the **Package Definition** page of the wizard, select **Microsoft** from the **Publisher** drop-down list, and select **Configuration Manager Client Upgrade** from the **Package definition** list.  

4.  On the **Source Files** page, select **Always obtain files from a source folder**.  

5.  On the **Source Folder** page, select **Network path (UNC Name)**. Then enter the network path to the server and share that contains the client installation files.  

    > [!NOTE]  
    >  The computer on which the Configuration Manager deployment runs must have access to the specified network folder. Otherwise, the client installation fails.  

    To change any of the client installation properties, modify the CCMSetup.exe command line on the **General** tab of the **Configuration Manager agent silent upgrade Properties** program dialog box. The default installation properties are `/noservice SMSSITECODE=AUTO`.  

6. Distribute the package to all distribution points that you want to host the client upgrade package. Then deploy the package to device collections that contain clients that you want to upgrade.  



## <a name="bkmk_mdm"></a> Intune MDM-managed Windows devices

Deploy the Configuration Manager client to devices that are enrolled with Microsoft Intune. 

This procedure is for a traditional client that is connected to the intranet. It uses traditional client authentication methods. To ensure the device remains in a managed state after it installs the client, it must be on the intranet and within a Configuration Manager site boundary.  

For the procedure to install the Configuration Manager client on a modern Windows 10 device using Azure AD identity, see [Install and assign Configuration Manager Windows 10 clients using Azure AD for authentication](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

> [!NOTE]  
> By default, once the client software is installed, the device unenrolls from Intune.
> 
> Starting in version 1710, clients don't unenroll from Intune. They can have both the Configuration Manager client and MDM enrollment at the same time. For more information, see [Co-management overview](/sccm/comanage/overview).  


###  Install clients with Intune  

1. In Intune, [Add a Windows line-of-business app](https://docs.microsoft.com/intune/lob-apps-windows) containing the Configuration Manager client installation file **ccmsetup.msi**. This file is found in the following folder on the site server: `<ConfigMgr installation directory>\bin\i386`  

2. In the Intune Software Publisher, enter command-line parameters. For example, use the following command line with a traditional client on the intranet:  

   `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<Your site code> DNSSUFFIX=<DNS Suffix of management point>"`  

   > [!Note]  
   > For an example command line to use with a modern Windows 10 client using Azure AD authentication, see [How to prepare internet-based devices for co-management](/sccm/comanage/how-to-prepare-win10#install-the-configuration-manager-client).  

3. [Assign the app](https://docs.microsoft.com/intune/deploy-use/deploy-apps-in-microsoft-intune) to a group of the enrolled Windows computers.  



##  <a name="BKMK_ClientImage"></a> OS image installation

Preinstall the Configuration Manager client on a reference computer that you use to create an OS image.   

> [!Important]  
> When using the Configuration Manager task sequence to deploy the OS image, the [Prepare ConfigMgr Client](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) task sequence step completely removes the Configuration Manager client.  


### Prepare the client computer for imaging  

1.  Manually install the Configuration Manager client software on the reference computer. For more information, see [How to install Configuration Manager clients manually](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Don't specify a Configuration Manager site code for the client in the CCMSetup.exe command-line properties.  

2.  At a command prompt, type `net stop ccmexec` to stop the **SMS Agent Host** service (Ccmexec.exe) on the reference computer.  

3.  Delete the file **SMSCFG.INI** from the **Windows** folder on the reference computer.  

4.  Remove any certificates that are stored in the local computer store on the reference computer. For example, if you use public key infrastructure (PKI) certificates, before you image the computer, remove the certificates in the **Personal** store for **Computer** and **User**.  

5.  If the clients are installed in a different Configuration Manager hierarchy than the reference computer, remove the trusted root key from the reference computer.  

    > [!NOTE]  
    >  If clients can't query Active Directory Domain Services to locate a management point, they use the trusted root key to determine trusted management points. If you deploy all imaged clients in the same hierarchy as the master computer, leave the trusted root key in place. 
    > 
    > If you deploy the clients in different hierarchies, remove the trusted root key. Also provision these clients with the new trusted root key. For more information, see [Planning for the trusted root key](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  

6.  Use your imaging software to capture an image of the reference computer.  

7.  Deploy the image to destination computers.  



##  <a name="BKMK_ClientWorkgroup"></a> Workgroup computers  

Configuration Manager supports client installation for computers in workgroups. Install the client on workgroup computers by using the method specified in [How to install Configuration Manager clients manually](#BKMK_Manual).  


### Prerequisites  

-   Manually install the client on each workgroup computer. During installation, the interactive user must have local administrator rights.  

-   To access resources in the Configuration Manager site server domain, configure the Network Access Account for the site. Specify this account in the software distribution site component. For more information, see [Site components](/sccm/core/servers/deploy/configure/site-components).  


### Limitations  

-   Workgroup clients can't locate management points from Active Directory Domain Services. Instead they use DNS, WINS, or another management point.  

-   Global roaming isn't supported. Workgroup clients can't query Active Directory Domain Services for site information.  

-   Active Directory discovery methods can't discover computers in workgroups.  

-   You can't deploy software to users of workgroup computers.  

-   You can't use the client push installation method to install the client on workgroup computers.  

-   Workgroup clients can't use Kerberos for authentication, and might require manual approval.  

-   You can't configure a workgroup client as a distribution point. Configuration Manager requires that distribution point computers be members of a domain.  


### Install the client on workgroup computers  

Check the prerequisites, then follow the directions in the section [How to install Configuration Manager clients manually](#BKMK_Manual).  


#### Workgroup example 1

This example does the following actions: 
- Installs the client for intranet client management
- Specifies the site code 
- Specifies the DNS suffix to locate a management point  

   `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     
#### Workgroup example 2

This example requires the client to be on a network location that's configured in a boundary group. This requirement is for automatic site assignment to succeed. The command includes a fallback status point on server FSPSERVER. This property helps track client deployment, and to identify any client communication issues. 

   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> Internet-based client management  
 
> [!Note]  
> This section doesn't apply to clients using a [cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway). To install internet-based clients using a cloud management gateway, see [Install and assign Configuration Manager Windows 10 clients using Azure AD for authentication](/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

When the Configuration Manager site supports [internet-based client management](/sccm/core/clients/manage/plan-internet-based-client-management) for clients that are sometimes on the intranet, and sometimes on the internet, you have two options when you install clients on the intranet:  

-   Include the Client.msi property `CCMHOSTNAME=<internet FQDN of the internet-based management point>` when you install the client. For example, by using manual installation or client push. When you use this method, directly assign the client to the site. You can't use automatic site assignment. See the [How to install Configuration Manager clients manually](#BKMK_Manual) section, which provides an example of this configuration method.  

-   Install the client for intranet client management, and then assign an internet-based client management point to the client. Change the management point by using the client properties in the Configuration Manager control panel, or by using a script. When you use this method, you can use automatic client assignment. For more information, see the [How to configure clients for internet-based client management after client installation](#BKMK_ConfigureIBCM_MP) section.  

To install clients that are on the internet, choose one of the following supported methods:  

-   Provide a mechanism for these clients to temporarily connect to the intranet with a VPN. Then install the client by using any appropriate client installation method.  

-   Use an installation method that is independent from Configuration Manager. For example, package the client installation source files onto removable media and send to users to install. The client installation source files are located in the `<InstallationPath>\Client` folder on the Configuration Manager site server. Include on the media a script to manually copy over the client folder. From this folder, install the client by using CCMSetup.exe and all the appropriate CCMSetup command-line properties.  

> [!NOTE]  
>  Configuration Manager doesn't support installing a client directly from the internet-based management point or from the internet-based software update point.  

Clients that are managed over the internet must communicate with internet-based site systems. Ensure that these clients also have public key infrastructure (PKI) certificates before you install the client. Install these certificates independently from Configuration Manager. For more information about the certificate requirements, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements).  


### Install clients on the internet by specifying CCMSetup command-line properties  

1.  Follow the directions in the section [How to install Configuration Manager clients manually](#BKMK_Manual). Always include the following options:  

    -   CCMSetup command-line parameter `/source:<local path to the copied Client folder>`  

    -   CCMSetup command-line parameter `/UsePKICert`  

    -   Client.msi property `CCMHOSTNAME=<FQDN of internet-based management point>`  

    -   Client.msi property `SMSSIGNCERT=<local path to exported site server signing certificate>`  

    -   Client.msi property `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    >  If the site has more than one internet-based management point, it doesn't matter which internet-based management point you specify for the CCMHOSTNAME property. When a Configuration Manager client connects to the specified internet-based management point, it sends the client a list of available internet-based management points in the site. The client randomly selects one from the list.  

2.  If you don't want the client to check the certificate revocation list (CRL), specify the CCMSetup command-line parameter `/NoCRLCheck`.  

3.  If you're using an internet-based fallback status point, specify the Client.msi property `FSP=<internet FQDN of the internet-based fallback status point>`.  

4.  If you're installing the client for internet-only client management, specify the Client.msi property `CCMALWAYSINF=1`.  

5.  Verify whether you have to specify additional CCMSetup command-line parameters. For example, if the client has more than one valid PKI certificate, you might have to specify a certificate selection criterion. For a list of available properties, see [About client installation parameters and properties](/sccm/core/clients/deploy/about-client-installation-properties).  


#### Internet-based example:  

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

This example installs the client with the following behaviors:
  - Use source files from a folder on the D drive
  - Use a client PKI certificate 
  - Select the certificate with the longest validity period 
  - Internet-only client management
  - Assign the client to use the internet-based management point named SERVER1
  - Assign the internet-based fallback status point in the contoso.com domain
  - Assign the client to the ABC site  


###  <a name="BKMK_ConfigureIBCM_MP"></a> To configure clients for internet-based client management after client installation  

To assign the internet-based management point after you install the client, use one of these procedures. The first requires manual configuration, and is appropriate for a few clients. The second is more appropriate for configuring many clients.  


#### Configure clients for internet-based client management after client installation from the Configuration Manager control panel  

1.  Open the **Configuration Manager** control panel on the client.  

2.  On the **Internet** tab, enter the fully qualified domain name (FQDN) of the internet-based management point as the **Internet FQDN**.  

    > [!NOTE]  
    >  The **Internet** tab is only available if the client has a client PKI certificate.  

3.  If the client accesses the internet by using a proxy server, enter the proxy server settings.  


#### Configure clients for internet-based client management after client installation by using a script  

1.  Open a text editor, such as Notepad.  

2.  Copy and insert the following VBScript sample into the file. Replace *mp.contoso.com* with the internet FQDN of your internet-based management point.  

    ``` VBScript 
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
    >  To delete a specified internet-based management point, remove the server FQDN value inside the quotation marks. This line becomes: `newInternetBasedManagementPointFQDN = ""`  

4.  Save the file with a .vbs extension.  

5.  Use cscript.exe to run the script on client computers, by using one of the following methods:  

    -   Deploy the file to existing Configuration Manager clients by using a package and a program.  

    -   Run the file locally on existing Configuration Manager clients by double-clicking the script file in Windows Explorer.  

You might have to restart the client for the changes to take effect.  



##  <a name="BKMK_Provision"></a> Provision client installation properties for group policy and software update-based client installations

Use Windows group policy to provision computers with Configuration Manager client installation properties. These properties are stored in the registry of the computer. The client reads them when it installs. This procedure isn't normally required, but might be needed for some client installation scenarios, such as:  

-   You're using the group policy settings or software update-based client installation methods. You haven't extended the Active Directory schema for Configuration Manager.  

-   You want to override client installation properties on specific computers.  

> [!NOTE]  
>  If any installation properties are supplied on the CCMSetup.exe command line, installation properties provisioned on computers aren't used.  

A group policy administrative template named **ConfigMgrInstallation.adm** is supplied on the Configuration Manager installation media. Use this template to provision client computers with installation properties.   


### Configure and assign client installation properties by using a group policy object  

1.  Import the administrative template **ConfigMgrInstallation.adm** into a new or existing group policy object, by using an editor such as Windows Group Policy Object Editor. Find this file in the folder `TOOLS\ConfigMgrADMTemplates` on the Configuration Manager installation media.  

2.  Open the properties of the imported setting **Configure Client Deployment Settings**.  

3.  Choose **Enabled**.  

4.  In the **CCMSetup** box, enter the required CCMSetup command-line properties. For a list of all CCMSetup command-line properties and examples of their use, see [About client installation parameters and properties](/sccm/core/clients/deploy/about-client-installation-properties).  

5.  Assign the group policy object to the computers that you want to provision with Configuration Manager client installation properties.  
