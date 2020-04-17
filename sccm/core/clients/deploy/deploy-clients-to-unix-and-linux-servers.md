---
title: Deploy UNIX/Linux clients
titleSuffix: Configuration Manager
description: Learn how to deploy a client to a UNIX or Linux server in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# How to deploy clients to UNIX and Linux servers in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!Important]  
> Starting in version 1902, Configuration Manager doesn't support Linux or UNIX clients. 
> 
> Consider Microsoft Azure Management for managing Linux servers. Azure solutions have extensive Linux support that in most cases exceed Configuration Manager functionality, including end-to-end patch management for Linux.


Before you can manage a Linux or UNIX server with Configuration Manager, you must install the Configuration Manager client for Linux and UNIX on each Linux or UNIX server. You can accomplish the installation of the client manually on each computer, or use a shell script that installs the client remotely. Configuration Manager doesn't support the use of client push installation for Linux or UNIX servers. Optionally you can configure a Runbook for System Center Orchestrator to automate the install of the client on the Linux or UNIX server.  

 Regardless of the installation method you use, the install process requires the use of a script named **install** to manage the install process. This script is included when you download the Client for Linux and UNIX.  

 The install script for the Configuration Manager client for Linux and UNIX supports command-line properties. Some command-line properties are required, while others are optional. For example, when you install the client, you must specify a management point from the site that is used by the Linux or UNIX server for its initial contact with the site. For the complete list of command-line properties, see [Command-line properties for installing the client on Linux and UNIX servers](#BKMK_CmdLineInstallLnUClient).  

 After you install the client, you specify Client Settings in the Configuration Manager console to configure the client agent in the same way you would Windows-based clients. For more information, see  [Client settings for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="BKMK_AboutInstallPackages"></a> About client installation packages and the universal agent  
 To install the client for Linux and UNIX on a specific platform, you must use the applicable client installation package for the computer where you install the client. Applicable client installation packages are included as part of each client download from the [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=525184). In addition to client installation packages, the client download includes the **install** script that manages the installation of the client on each computer.  

 When you install a client, you can use the same process and command-line properties regardless of the client installation package you use.  

 For information about the operating systems, platforms, and client installation packages that are supported by each release of the Configuration Manager client for Linux and UNIX, see [Linux and UNIX servers](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#linux-and-unix-servers).  

##  <a name="BKMK_InstallLnUClient"></a> Install the client on Linux and UNIX servers  
 To install the client for Linux and UNIX, you run a script on each Linux or UNIX computer. The script is named **install** and supports command-line properties that modify the installation behavior and reference the client installation package. The install script and client installation package must be located on the client. The client installation package contains the Configuration Manager client files for a specific Linux or UNIX operating system and platform.
 Each client installation package contains all the necessary files to complete the client installation and unlike Windows-based computers, doesn't download additional files from a management point or other source location.  

 After you install the Configuration Manager client for Linux and UNIX, you don't need to reboot the computer. As soon as the software installation is complete, the client is operational. If you reboot the computer, the Configuration Manager client restarts automatically.  

 The installed client runs with root credentials. Root credentials are required to collect hardware inventory and do software deployments.  

 Use the following command format:  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install` is the name of the script file that installs the client for Linux and UNIX. This file is provided with the client software.  

-   `-mp <computer>` specifies the initial management point that is used by the client. Example: `smsmp.contoso.com`  

-   `-sitecode <site code>` specifies the site code that  the client is assigned to. Example: `S01`  

-   `<property #1> <property #2>` specifies the command-line properties to use with the installation script.  

    > [!NOTE]  
    >  For more information, see [Command-line properties for installing the client on Linux and UNIX servers](#BKMK_CmdLineInstallLnUClient).  

-   **client installation package** is the name of the client installation .tar package for this computer operating system, version, and CPU architecture. The client installation .tar file must be specified last. Example: `ccm-Universal-x64.<build>.tar`  

###  <a name="BKMK_ToInstallLnUClinent"></a> To install the Configuration Manager client on Linux and UNIX servers  

1.  On a Windows computer, [download the appropriate client file for the Linux or UNIX server](https://go.microsoft.com/fwlink/?LinkID=525184) you want to manage.  

2.  Run the self-extracting .exe file on the Windows computer to extract the install script and the client installation .tar file.  

3.  Copy the **install** script and the .tar file to a folder on the server you want to manage.  

4.  On the UNIX or Linux server, run the following command to enable the script to run as a program: `chmod +x install`  

    > [!IMPORTANT]  
    >  You must use root credentials to install the client.  

5.  Next, run the following command to install the Configuration Manager client: `./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     When you enter this command, use additional command-line properties you require. For the list of command-line properties, see [Command-line properties for installing the client on Linux and UNIX servers](#BKMK_CmdLineInstallLnUClient)  

6.  After the script runs, validate the install by reviewing the **/var/opt/microsoft/scxcm.log** file. Additionally, you can confirm that the client is installed and communicating with the site by viewing details for the client in the **Devices** node of the **Assets and Compliance** workspace in the Configuration Manager console.  

###  <a name="BKMK_CmdLineInstallLnUClient"></a> Command-line properties for installing the client on Linux and UNIX servers  
 The following properties are available to modify the behavior of the install script:  

> [!NOTE]  
>  Use the property `-h` to display this list of supported properties.  

-   `-mp <server FQDN>`  

     Required. Specifies by FQDN, the management point server that the client uses as an initial point of contact.  

    > [!IMPORTANT]  
    >  This property doesn't specify the management point to which the client is assigned after installation.  

    > [!NOTE]  
    >  When you use the `-mp` property to specify a management point that's configured to accept only HTTPS client connections, you must also use the `-UsePKICert` property.  

-   `-sitecode <sitecode>`  

     Required. Specifies the Configuration Manager primary site to assign the Configuration Manager client to. Example: `-sitecode S01`  

-   `-fsp <server_FQDN>`  

     Optional. Specifies by FQDN, the fallback status point server that the client uses to submit state messages. For more information, see [Determine whether you require a fallback status point](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

-   `-dir <directory>`  

     Optional. Specifies an alternate location to install the Configuration Manager client files. By default, the client installs to the following location: `/opt/microsoft`  

-   `-nostart`  

     Optional. Prevents the automatic start of the Configuration Manager client service, **ccmexec.bin**, after the client installation completes.  

     After the client installs, you must start the client service manually.  

     By default, the client service starts after the client installation completes, and each time the computer restarts.  

-   `-clean`  

     Optional. Specifies the removal of all client files and data from a previously installed client for Linux and UNIX, before the new installation starts. This action removes the client's database and certificate store.  

-   `-keepdb`  

     Optional. Specifies that the local client database is kept, and reused when you reinstall a client. By default, when you reinstall a client this database is deleted.  

-   `-UsePKICert <parameter>`  

     Optional. Specifies the full path and file name to a X.509 PKI certificate in the Public Key Certificate Standard (PKCS#12) format. This certificate is used for client authentication. If a certificate is not specified during installation and you need to add or change a certificate, use the **certutil** utility. For more information, see [How to manage certificates on the client for Linux and UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     When you use `-UsePKICert`, you must also supply the password associated with the PKCS#12 file by use of the `-certpw` command-line parameter.  

     If you don't use this property to specify a PKI certificate, the client uses a self-signed certificate and all communications to site systems are over HTTP.  

     If you specify an invalid certificate on the client install command line, no errors are returned. Certificate validation occurs after the client installs. When the client starts, certificates are validated with the management point. If a certificate fails validation, the following message appears in **scxcm.log**: **Failed validate the certificate for Management Point**. The default log file location is:  **/var/opt/microsoft/scxcm.log**.  

     > [!NOTE]  
     > You must specify this property when you install a client and use the `-mp` property to specify a management point that is configured to accept only HTTPS client connections.  

     Example: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     Optional. Specifies the password associated with the PKCS#12 file that you specified by use of the `-UsePKICert` property.  

     Example: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     Optional. Specifies that a client shouldn't check the certificate revocation list (CRL) when it communicates over HTTPS by use of a PKI certificate. When this option isn't specified, the client checks the CRL before establishing an HTTPS connection by use of PKI certificates. For more information about client CRL checking, see Planning for PKI Certificate Revocation.  

     Example: `-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     Optional. Specifies the full path and file name to the Configuration Manager trusted root key. The Configuration Manager trusted root key provides a mechanism that Linux and UNIX clients use to verify that they're connected to a site system that belongs to the correct hierarchy.  

     If you don't specify the trusted root key on the command line, the client will trust the first management point it communicates with and will automatically retrieve the trusted root key from that management point.  

     For more information, see  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Example: `-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     Optional. Specifies the port that is configured on management points that the client uses when communicating to management points over HTTP. If the port isn't specified, the default value of 80 is used.  

     Example: `-httpport 80`  

-   `-httpsport <port>`  

     Optional. Specifies the port that is configured on management points that the client uses when communicating to management points over HTTPS. If the port isn't specified, the default value of 443 is used.  

     Example: `-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     Optional. Specifies that client installation skips SHA-256 validation. Use this option when installing the client on operating systems that didn't release with a version of OpenSSL that supports SHA-256. For more information, see [About Linux and UNIX operating systems that don't support SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   `-signcertpath <file location>`  

     Optional. Specifies the full path and **.cer** file name of the exported self-signed certificate on the site server. If PKI certificates aren't available, the Configuration Manager site server automatically generates self-signed certificates.  

     These certificates are used to validate that the client policies downloaded from the management point were sent from the intended site. If a self-signed certificate is not specified during installation, or you need to change the certificate, use the **certutil** utility. For more information, see [How to manage certificates on the client for Linux and UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     This certificate can be retrieved through the **SMS** certificate store and has the Subject name **Site Server** and the friendly name **Site Server Signing Certificate**.  

     If this option isn't specified during installation, Linux and UNIX clients trust the first management point they communicate with. They automatically retrieve the signing certificate from that management point.  

     Example: `-signcertpath <full path and file name>`  

-   `-rootcerts`  

     Optional. Specifies additional PKI certificates to import that aren't part of a management points certification authority (CA) hierarchy. If you specify multiple certificates in the command line, they should be comma delimited.  

     Use this option if you use PKI client certificates that don't chain to a root CA certificate that is trusted by your sites management points. Management points will reject the client if the client certificate doesn't chain to a trusted root certificate in the site's certificate issuers list.  

     If you don't use this option, the Linux and UNIX client will verify the trust hierarchy using only the certificate in the `-UsePKICert` option.  

     Example: `-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="BKMK_UninstallLnUClient"></a> Uninstalling the client from Linux and UNIX servers  
 To uninstall the Configuration Manager client for Linux and UNIX you use the uninstall utility, **uninstall**. By default, this file is located in the **/opt/microsoft/configmgr/bin/** folder on the client computer. This uninstall command doesn't support any command-line parameters and will remove all files related to the client software from the server.  

 To uninstall the client, use the following command line: **/opt/microsoft/configmgr/bin/uninstall**  

 You don't have to reboot the computer after you uninstall the Configuration Manager client for Linux and UNIX.  

##  <a name="BKMK_ConfigLnUClientCommuincations"></a> Configure Request Ports for the Client for Linux and UNIX  
 Similar to Windows-based clients, the Configuration Manager client for Linux and UNIX uses HTTP and HTTPS to communicate with Configuration Manager site systems. The ports that the Configuration Manager client uses to communicate are referred to as a request ports.  

 When you install the Configuration Manager client for Linux and UNIX, you can change the clients default request ports by specifying the **-httpport** and **-httpsport** installation properties. When you don't specify the installation property and a custom value, the client uses the default values. The default values are **80** for HTTP traffic and **443** for HTTPS traffic.  

 After you install the client, you can't change its request port configuration. Instead, to change the port configuration you must reinstall the client and specify the new port configuration. When you reinstall the client to change the request port numbers, run the **install** command similar to the new client install, but use the additional command-line property of **-keepdb**. This switch instructs the installation to keep the client database and files including the clients GUID and certificate store.  

 For more information about client communication port numbers, see [How to configure client communication ports](../../../core/clients/deploy/configure-client-communication-ports.md).  

##  <a name="BKMK_ConfigClientMP"></a> Configure the Client for Linux and UNIX to Locate Management Points  
 When you install the Configuration Manager client for Linux and UNIX, you must specify a management point to use as an initial point of contact.  

 The Configuration Manager client for Linux and UNIX contacts this management point at the time the client installs. If the client fails to contact the management point, the client software continues to retry until successful.  

 For more information about how clients locate management points, see [Locating Management Points](assign-clients-to-a-site.md#locating-management-points).
