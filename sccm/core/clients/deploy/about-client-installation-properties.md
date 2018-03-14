---
title: Client installation properties
titleSuffix: Configuration Manager
description: Learn about the ccmsetup command-line properties for installing the Configuration Manager client.
ms.custom: na
ms.date: 03/16/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: 15
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# About client installation properties in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the CCMSetup.exe command to install the Configuration Manager client. If you provide these client installation properties on the command line, they modify the installation behavior.



##  <a name="aboutCCMSetup"></a> About CCMSetup.exe  
 The CCMSetup.exe command downloads needed files to install the client from a management point or a source location. These files might include:  

-   The Windows Installer package client.msi that installs the client software.  

-   Microsoft Background Intelligent Transfer Service (BITS) installation files.  

-   Windows Installer installation files.  

-   Updates and fixes for the Configuration Manager client.  

> [!NOTE]  
>  In Configuration Manager, you can't run the Client.msi file directly.  

 CCMSetup.exe provides [command-line properties](#ccmsetup-exe-command-line-properties) to customize the installation. You can also specify properties to modify the behavior of client.msi at the CCMSetup.exe command line.  

> [!IMPORTANT]  
>  Specify CCMSetup properties before you specify properties for client.msi.  

 CCMSetup.exe and the supporting files are located on the site server in the **Client** folder of the Configuration Manager installation folder. This folder is shared to the network as **&lt;Site Server Name\>\SMS_&lt;Site Code\>\Client**.  

 At the command prompt, the CCMSetup.exe command uses the following format:  

 `CCMSetup.exe [<Ccmsetup properties>] [<client.msi setup properties>]`  

 For example:  

   `CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

 This example does the following things:  

-   Specifies the management point named SMSMP01 to request a list of distribution points to download the client installation files.  

-   Specifies that installation should stop if a version of the client already exists on the computer.  

-   Instructs client.msi to assign the client to the site code S01.  

-   Instructs client.msi to use the fallback status point named SMSFP01.  

> [!NOTE]  
>  If a property has spaces, surround it with quotation marks.  


> [!IMPORTANT]  
>  If you extended the Active Directory schema for Configuration Manager, the site publishes many client installation properties in Active Directory Domain Services. The Configuration Manager client automatically reads these properties. For more information, see [About client installation properties published to Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md)  



##  CCMSetup.exe Command-Line Properties  

### /?  

Opens the **CCMSetup** dialog box showing command-line properties for ccmsetup.exe.  

Example: **ccmsetup.exe /?**  

### /source:&lt;Path\>  

 Specifies the  file download location. Use a local or UNC path. Files are downloaded using the server message block (SMB) protocol. To use  **/source**, the Windows user account for client installation must have Read permissions to the location.

> [!NOTE]  
>  You can use the **/source** property more than once in a command line to specify alternative download locations.  

 Example: **ccmsetup.exe /source:"\\\computer\folder"**  

### /mp:&lt;Server\>

 Specifies a source management point for computers to connect to. Computers use this management point to find the nearest distribution point for the installation files. If there are no distribution points, or computers can't download the files from the distribution points after four hours, they download the files from the specified management point.  

> [!IMPORTANT]  
>  This property is used to specify an initial management point for computers to find a download source, and can be any management point in any site. It doesn't *assign* the client to a management point.   

 Computers download the files over an HTTP or HTTPS connection, depending on the site system role configuration for client connections. If configured, the download uses BITS throttling. If all distribution points and management points are configured for HTTPS client connections only, verify that the client computer has a valid client certificate.  

You can use the **/mp** command-line property to specify more than one management point. If the computer fails to connect to the first one, it tries the next in the specified list. When you specify multiple management points, separate the values by semicolons.

If the client connects to a management point using HTTPS, typically, you must specify the FQDN, not the computer name. The value must match the management point’s PKI certificate Subject or Subject Alternative Name. Although Configuration Manager supports using a computer name in the certificate for connections on the intranet, an FQDN is the recommended security best practice.

Example for when you use the computer name: `ccmsetup.exe /mp:SMSMP01`  

Example for when you use the FQDN: `ccmsetup.exe /mp:smsmp01.contoso.com`  

This property can specify the URL of a cloud management gateway. Use this URL to install the client on an internet-based device. To get the value for this property, use the following steps:
- Create a cloud management gateway.
- On an active client, open a Windows PowerShell command prompt as an administrator. 
- Run the following command: `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
- Append the "https://" prefix to use with the **/mp** property.

Example for when you use the cloud management gateway URL: `ccmsetup.exe /mp: https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > When specifying the URL of a cloud management gateway for the **/mp** property, it must start with **https://**.


### /retry:&lt;Minutes\>

The retry interval if CCMSetup.exe fails to download installation files. CCMSetup continues to retry until it reaches the limit specified in the **downloadtimeout** property.  

Example: `ccmsetup.exe /retry:20`  

### /noservice

Prevents CCMSetup from running as a service, which is the default. When CCMSetup runs as a service, it runs in the context of the Local System account of the computer. This account might not have sufficient rights to access required network resources for the installation. With **/noservice**, CCMSetup.exe runs in the context of the user account that you use to start the installation. Also, if you're using a script to run CCMSetup.exe with the **/service** property, CCMSetup.exe exits after the service starts and might not report installation details correctly.   

Example: `ccmsetup.exe /noservice`  

### /service

Specifies that CCMSetup should run as a service that uses the local system account.  

Example: `ccmsetup.exe /service`  

### /uninstall

Specifies that the client software should be uninstalled. For more information, see [How to manage clients](../manage/manage-clients.md).  

Example: `ccmsetup.exe /uninstall`  

### /logon

If any version of the client is already installed, this property specifies that the client installation should stop.  

Example: `ccmsetup.exe /logon`  

### /forcereboot

 Specifies that CCMSetup should force the client computer to restart if necessary to complete the installation. If this property isn't specified, CCMSetup exits when a restart is necessary. It then continues after the next manual restart.  

 Example: `CCMSetup.exe /forcereboot`  

### /BITSPriority:&lt;Priority\>

 Specifies the download priority when client installation files are downloaded over an HTTP connection. Possible values are as follows:  

-   FOREGROUND  

-   HIGH  

-   NORMAL  

-   LOW  

 The default value is NORMAL.  

 Example: `ccmsetup.exe /BITSPriority:HIGH`  

### /downloadtimeout:&lt;Minutes\>

The length of time in minutes that CCMSetup tries to download the installation files before stopping. The default value is **1440** minutes (one day).  

Example: `ccmsetup.exe /downloadtimeout:100`  

### /UsePKICert

 When specified, the client uses a PKI certificate that includes client authentication, if available. If the client can't find a valid certificate, it uses an HTTP connection with a self-signed certificate. This behavior is the same when you don't use this property.

> [!NOTE]  
>  In some scenarios, you do not have to specify this property when you are installing a client, and still use a client certificate. These scenarios include installing a client by using client push, and software update point–based client installation. However, you must specify this property whenever you manually install a client and use the **/mp** property to specify a management point that is configured to accept only HTTPS client connections. You also must specify this property when you install a client for internet-only communication. Use the CCMALWAYSINF=1 property together with the properties for the internet-based management point and the site code. For more information about internet-based client management, see [Considerations for client communications from the internet or an untrusted forest](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

 Example: `CCMSetup.exe /UsePKICert`  

### /NoCRLCheck

 Specifies that a client shouldn't check the certificate revocation list (CRL) when it communicates over HTTPS with a PKI certificate.  

 When not specified, the client checks the CRL before establishing an HTTPS connection.  

 For more information about client CRL checking, see [Planning for PKI certificate revocation](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

 Example: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### /config:&lt;configuration file\>

Specifies the name of a text file that lists client installation properties.

- If you don't specify the **/noservice** CCMSetup property, this file must be located in the CCMSetup folder, which is %Windir%\\Ccmsetup for 32-bit and 64-bit operating systems.
- If you specify the **/noservice** property, this file must be located in the same folder from which you run CCMSetup.exe.  

Example: `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

To provide the correct file format, use the mobileclienttemplate.tcf file in the &lt;Configuration Manager directory\>\\bin\\&lt;platform\> folder on the site server. This file also has comments about the sections and how they're used. Specify the client installation properties in the [Client Install] section, after the following text: **Install=INSTALL=ALL**.  

Example [Client Install] section entry: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### /skipprereq:&lt;filename\>

 Specifies that CCMSetup.exe must not install the specified prerequisite program when installing the Configuration Manager client. This property supports entering more than one value. Use the semicolon character (;) to separate each value.  


 Examples: `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe` or `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`  

### /forceinstall

 Specify that CCMSetup.exe uninstalls any existing client, and installs a new client.  

### /ExcludeFeatures:&lt;feature\>

Specifies that CCMSetup.exe doesn't install the specified feature when it installs the client.  

Example: `CCMSetup.exe /ExcludeFeatures:ClientUI` doesn't install Software Center on the client.  

> [!NOTE]  
>  **ClientUI** is the only value supported with the **/ExcludeFeatures** property.  



##  <a name="ccmsetupReturnCodes"></a> CCMSetup.exe return codes  
 The CCMSetup.exe command provides the following return codes completed. To troubleshoot, review the ccmsetup.log file on the client computer for context and additional detail about return codes.  

|Return code|Meaning|  
|-----------------|-------------|  
|0|Success|  
|6|Error|  
|7|Reboot required|  
|8|Setup already running|  
|9|Prerequisite evaluation failure|  
|10|Setup manifest hash validation failure|  



##  <a name="clientMsiProps"></a> Client.msi Properties  
 The following properties can modify the installation behavior of client.msi. If you use the client push installation method, you can also specify the properties in the **Client** tab of the **Client Push Installation Properties** dialog box.  


### AADCLIENTAPPID

Specifies the Azure Active Directory (Azure AD) client app identifier. The client app is created or imported when you [configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) for Cloud Management. An Azure administrator can obtain the value for this property from the Azure portal. For more information, see [get application ID](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key). For the **AADCLIENTAPPID** property, this application ID is for the "Native" application type.

Example: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`


### AADRESOURCEURI

Specifies the Azure AD server app identifier. The server app is created or imported when you [configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) for Cloud Management. When creating the server app, in the Create Server Application dialog, this property is the **App ID URI**. 

Example: `ccmsetup.exe AADRESOURCEURI=https://contososerver`


### AADTENANTID

Specifies the Azure AD tenant identifier. This tenant is linked to Configuration Manager when you [configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantId** value. For example, `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

 > [!Note]
 > An Azure administrator can also obtain this value in the Azure portal. For more information, see [get tenant ID](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-tenant-id)

Example: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`


### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`


### CCMADMINS  

Specifies one or more Windows user accounts or groups to be given access to client settings and policies. This property is useful where the Configuration Manager admin doesn't have local administrative credentials on the client computer. Specify a list of accounts that are separated by semi-colons.  

Example: `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### CCMALLOWSILENTREBOOT

Specifies that the computer is allowed to restart following the client installation if necessary.  

> [!IMPORTANT]  
>  The computer restarts without warning even if a user is logged on.  

Example: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### CCMALWAYSINF

 Set to **1** to specify that the client is always internet-based and never connects to the intranet. The client's connection type displays **Always Internet**.  

 Use this property in conjunction with CCMHOSTNAME, which specifies the FQDN of the internet-based management point. Also use it with the CCMSetup property /UsePKICert, and with the site code.  

 For more information about internet-based client management, see [Considerations for client communications from the internet or an untrusted forest](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

 Example: `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### CCMCERTISSUERS

 Specifies the certificate issuers list, which is a list of trusted root certification (CA) certificates that the Configuration Manager site trusts.  

 For more information about the certificate issuers list and how clients use it during the certificate selection process, see [Planning for PKI client certificate selection](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

 This value is a case-sensitive match for subject attributes that are in the root CA certificate. Attributes can be separated by a comma (,) or semi-colon (;). Specify more than one root CA certificates by using a separator bar. Example:  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  To copy the **CertificateIssuers=&lt;string\>** for the site, reference the mobileclient.tcf file in the &lt;Configuration Manager directory\>\bin\\&lt;platform\> folder on the site server.  

### CCMCERTSEL

 Specifies the certificate selection criteria if the client has more than one certificate for HTTPS communication. This certificate is a valid certificate that includes the client authentication capability.  

 You can search for an exact match (use **Subject:**) or a partial match (use **SubjectStr:)** in the Subject Name or Subject Alternative Name. Examples:  

 `CCMCERTSEL="Subject:computer1.contoso.com"` searches for a certificate with an exact match to the computer name "computer1.contoso.com" in the Subject Name or the Subject Alternative Name.  

 `CCMCERTSEL="SubjectStr:contoso.com"` searches for a certificate that contains "contoso.com" in the Subject Name or the Subject Alternative Name.  

 You can also use Object Identifier (OID) or distinguished name attributes in the Subject Name or Subject Alternative Name attributes, for example:  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` searches for the organizational unit attribute expressed as an object identifier, and named Computers.  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` searches for the organizational unit attribute expressed as a distinguished name, and named Computers.  

> [!IMPORTANT]  
>  If you use the Subject Name box, the **Subject:** is case-sensitive, and the  **SubjectStr:** is case-insensitive.  
>   
>  If you use the Subject Alternative Name box, the **Subject:**and the **SubjectStr:** are case-insensitive.  

 The complete list of attributes that you can use for certificate selection is listed in [Supported attribute values for the PKI certificate selection criteria](#BKMK_attributevalues).  

 If more than one certificate matches the search, and the property CCMFIRSTCERT has been set to 1, the certificate with the longest validity period is selected.  

### CCMCERTSTORE

 Specifies an alternate certificate store name if the client certificate for HTTPS isn't located in the default certificate store of **Personal** in the Computer store.  

 Example: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### CCMDEBUGLOGGING

  Enables debug logging. Values can be set to 0 (off, default) or 1 (on). This property causes the client to log low-level information for troubleshooting. As a best practice, avoid using this property in production sites. Excessive logging can occur, which might make it difficult to find relevant information in the log files. Also set CCMENABLELOGGING to TRUE to enable debug logging.  

  Example: `CCMSetup.exe CCMDEBUGLOGGING=1`  

### CCMENABLELOGGING

  By default, this property is set to TRUE to enable logging. The log files are stored in the **Logs** folder in the Configuration Manager client installation folder. By default, this folder is %Windir%\CCM\Logs.  

  Example: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### CCMEVALINTERVAL  

 The frequency at which client health evaluation tool (ccmeval.exe) runs. Can be **1** to **1440** minutes. By default, runs once a day.  

### CCMEVALHOUR

 The hour when the client health evaluation tool (ccmeval.exe) runs,  between **0** (midnight) and **23** (11pm). Runs at midnight by default.  

### CCMFIRSTCERT

 If set to 1, this property specifies that the client should select the PKI certificate with the longest validity period. This setting might be required if you're using Network Access Protection with IPsec enforcement.  

 Example: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  


### CCMHOSTNAME

 If the client is managed over the internet, this property specifies the FQDN of the internet-based management point.  

 Don't specify this option with the installation property of SMSSITECODE=AUTO. Internet-based clients must be directly assigned to their internet-based site.  

 Example: `CCMSetup.exe  /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

This property can specify the address of a cloud management gateway. To get the value for this property, use the following steps:
- Create a cloud management gateway.
- On an active client, open a Windows PowerShell command prompt as an administrator. 
- Run the following command: `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
- Use the returned value as-is with the **CCMHOSTNAME** property.

For example: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > When specifying the address of a cloud management gateway for the **CCMHOSTNAME** property, do *not* append a prefix such as **https://**. This prefix is only used with the **/mp** URL of a cloud management gateway.



### CCMHTTPPORT

 Specifies the port that the client should use when communicating over HTTP to site system servers. Set to Port 80 by default.  

 Example: `CCMSetup.exe CCMHTTPPORT=80`  

### CCMHTTPSPORT

Specifies the port that the client should use when communicating over HTTPS to site system servers. Set to Port 443 by default.  

Example: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### CCMINSTALLDIR

 Identifies the folder where the Configuration Manager client files are installed, *%Windir%*\CCM by default. Regardless of where these files are installed, the Ccmcore.dll file is always installed in the *%Windir%\System32* folder. Also, on a 64-bit OS, a copy of the Ccmcore.dll file is always installed in the *%Windir%*\SysWOW64 folder. This file supports 32-bit applications that use the 32-bit version of the client APIs from the Configuration Manager SDK.  

 Example: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### CCMLOGLEVEL

Specifies the level of detail to write to Configuration Manager log files. Specify an integer from 0 to 3, where 0 is the most verbose logging and 3 logs only errors. The default is 1.  

Example: `CCMSetup.exe CCMLOGLEVEL=3`  

### CCMLOGMAXHISTORY

When a Configuration Manager log file reaches the maximum size, the client renames it as a backup and creates a new log file. The maximum size is 250,000 bytes by default, or the value specified by the property CCMLOGMAXSIZE.

This property specifies how many previous versions of the log file to keep. The default value is 1. If the value is set to 0, no old log files are kept.  

Example: `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### CCMLOGMAXSIZE

The maximum log file size in bytes. When a log grows to the specified size, the client renames it as a history file, and creates a new file. This property must be set to at least 10,000 bytes. The default value is 250,000 bytes.  

Example: `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### DISABLESITEOPT

 If set to TRUE, this property disables the ability of administrative users from changing the assigned site in the **Configuration Manager** control panel.  

 Example: **CCMSetup.exe DISABLESITEOPT=TRUE**  

### DISABLECACHEOPT

If set to TRUE, this property disables the ability of administrative users from changing the client cache folder settings in the **Configuration Manager** control panel.  

Example: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### DNSSUFFIX

 Specifies a DNS domain for clients to locate management points that are published in DNS. When a management point is located, it informs the client about other management points in the hierarchy. This behavior means that the management point that is located by using DNS publishing doesn't have to be from the client’s site, but can be any management point in the hierarchy.  

> [!NOTE]  
>  You don't have to specify this property if the client is in the same domain as a published management point. In that case, the client’s domain is automatically used to search DNS for management points.  

 For more information about DNS publishing as a service location method for Configuration Manager clients, see [Service location and how clients determine their assigned management point](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

> [!NOTE]  
>  By default, DNS publishing isn't enabled in Configuration Manager.  

 Example: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### FSP

Specifies the fallback status point that receives and processes state messages sent by Configuration Manager client computers.  

For more information about the fallback status point, see [Determine if you need a fallback status point](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point).  

Example: `CCMSetup.exe FSP=SMSFP01`  

### IGNOREAPPVVERSIONCHECK

 Specifies that the presence of the minimum required version of Microsoft Application Virtualization (App-V) isn't checked before the client is installed.  

> [!IMPORTANT]  
>  If you install the Configuration Manager client without installing App-V, you can't deploy virtual applications.  

 Example: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### NOTIFYONLY

Specifies that the client reports status, but doesn't remediate problems that it finds.  

Example: `CCMSetup.exe NOTIFYONLY=TRUE`  

For more information, see [How to configure client status](configure-client-status.md).  

### RESETKEYINFORMATION

 If a client has the wrong Configuration Manager trusted root key and can't contact a trusted management point to receive the new trusted root key, use this property to manually remove the old trusted root key. This situation may occur when you move a client from one site hierarchy to another. This property applies to clients that use HTTP and HTTPS client communication.  

 Example: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### SITEREASSIGN

Enables automatic site reassignment for client upgrades when used with [SMSSITECODE](#smssitecode)=AUTO.

Example: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### SMSCACHEDIR

Specifies the location of the client cache folder on the client computer, which stores temporary files. By default, the location is *%Windir%\ccmcache*.  

Example: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

This property can be used in conjunction with the SMSCACHEFLAGS property to control the client cache folder location.  

Example: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` installs the client cache folder on the largest available client disk drive.  

### SMSCACHEFLAGS

Specifies further installation details for the client cache folder. You can use SMSCACHEFLAGS properties individually or in combination, separated by semicolons. If this property isn't specified, the client cache folder is installed according to the SMSCACHEDIR property, the folder isn't compressed, and the SMSCACHESIZE value is used as the size in MB of the folder.  

This setting is ignored when you upgrade an existing client.  

Properties:  

-   PERCENTDISKSPACE: Specifies the folder size as a percentage of the total disk space. If you specify this property, you must also specify the property SMSCACHESIZE as the percentage value to use.  

-   PERCENTFREEDISKSPACE: Specifies the folder size as a percentage of the free disk space. If you specify this property, you must also specify the property SMSCACHESIZE as the percentage value to use. For example, if the disk has 10 MB free and SMSCACHESIZE is specified as 50, the folder size is set to 5 MB. You cannot use this property with the PERCENTDISKSPACE property.  

-   MAXDRIVE: Specifies that the folder should be installed on the largest available disk. This value is ignored if a path has been specified with the SMSCACHEDIR property.  

-   MAXDRIVESPACE: Specifies that the folder should be installed on the disk drive that has the most free space. This value is ignored if a path has been specified with the SMSCACHEDIR property.  

-   NTFSONLY: Specifies that the folder can be installed only on NTFS disk drives. This value is ignored if a path has been specified with the SMSCACHEDIR property.  

-   COMPRESS: Specifies that the folder should be stored in a compressed form.  

-   FAILIFNOSPACE: Specifies that the client software should be removed if there is insufficient space to install the folder.  

Example: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### SMSCACHESIZE

> [!IMPORTANT]
> Client settings are available for specifying the client cache folder size. The addition of those client settings effectively replaces using SMSCACHESIZE as a client.msi property to specify the size of the client cache. For more information, see the [client settings for cache size](about-client-settings.md#client-cache-settings).  

<!-- For 1602 and earlier, SMSCACHESIZE specifies the size of the client cache folder in megabyte (MB) or as a percentage when used with the PERCENTDISKSPACE or PERCENTFREEDISKSPACE property. If this property isn't set, the folder defaults to a maximum size of 5120 MB. The lowest value that you can specify is 1 MB.  -->

> [!NOTE]  
>  If a new package that must be downloaded would cause the folder to exceed the maximum size, and if the folder can't be purged to make sufficient space available, the package download fails, and the program or application doesn't run.  

This setting is ignored when you upgrade an existing client, and when the client downloads software updates.  

Example: `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  If you reinstall a client, you can't use the SMSCACHESIZE or SMSCACHEFLAGS installation properties to set the cache size to be smaller than it was previously. If you try to do this action, your value is ignored. The cache size is automatically set to the previous size.  

### SMSCONFIGSOURCE

Specifies the location and order that the Configuration Manager Installer checks for configuration settings. The property is a string of one or more characters, each defining a specific configuration source. Use the character values R, P, M, and U, alone or in combination:  

-   R: Check for configuration settings in the registry.  

   For more information, see [information about storing client installation properties in the registry](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

-   P: Check for configuration settings in the installation properties provided at the command prompt.  

-   M: Check for existing settings when upgrading an older client with the Configuration Manager client software.  

-   U: Upgrade the installed client to a newer version (and use  the assigned site code).  

 By default, the client installation uses `PU` to check first the installation properties and then the existing settings.  

 Example: `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### SMSDIRECTORYLOOKUP

 Specifies whether the client can use Windows Internet Name Service (WINS) to find a management point that accepts HTTP connections. Clients use this method when they can't find a management point in Active Directory Domain Services or in DNS.  

 This property doesn't affect whether the client uses WINS for name resolution.  

 You can configure two different modes for this property:  

-   NOWINS: This value is the most secure setting for this property and prevents clients from finding a management point in WINS. When you use this setting, clients must have an alternative method to locate a management point on the intranet, such as Active Directory Domain Services or by using DNS publishing.  

-   WINSSECURE (default): In this mode, a client that uses HTTP communication can use WINS to find a management point. However, the client must have a copy of the trusted root key before it can successfully connect to the management point. For more information, see [Planning for the trusted root key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  


 Example: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### SMSMP

Specifies an initial management point for the Configuration Manager client to use.  

> [!IMPORTANT]  
>  If the management point only accepts client connections over HTTPS, you must prefix the management point name with https://.  

Example: `CCMSetup.exe SMSMP=smsmp01.contoso.com`

Example: `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  


### SMSPUBLICROOTKEY

 Specifies the Configuration Manager trusted root key when it cannot be retrieved from Active Directory Domain Services. This property applies to clients that use HTTP and HTTPS client communication. For more information, see [Planning for the trusted root key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 Example: `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### SMSROOTKEYPATH

 Used to reinstall the Configuration Manager trusted root key. Specifies the full path and file name to a file containing the trusted root key. This property applies to clients that use HTTP and HTTPS client communication. For more information, see [Planning for the trusted root key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 Example: 'CCMSetup.exe SMSROOTKEYPATH=&lt;Full path and filename\>`  

### SMSSIGNCERT

 Specifies the full path and .cer file name of the exported self-signed certificate on the site server.  

 This certificate is stored in the **SMS** certificate store and has the Subject name **Site Server** and the friendly name **Site Server Signing Certificate**.  

 Example: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;Full path and file name\>**  

### SMSSITECODE

 Specifies the Configuration Manager site to assign the client to. This value can either be a three-character site code or the word AUTO. If you specify AUTO, or do not specify this property, the client attempts to determine its site assignment from Active Directory Domain Services or from a specified management point. To enable AUTO for client upgrades, you must also set [SITEREASSIGN](#sitereassign) to TRUE.    

> [!NOTE]  
>  Don't use AUTO if you also specify the Internet-based management point (CCMHOSTNAME). In that case, you must directly assign the client to its site.  

 Example: `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> Supported Attribute Values for the PKI Certificate Selection Criteria  
 Configuration Manager supports the following attribute values for the PKI certificate selection criteria:  

|OID attribute|Distinguished Name attribute|Attribute definition|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Domain component|  
|1.2.840.113549.1.9.1|E or E-mail|Email address|  
|2.5.4.3|CN|Common name|  
|2.5.4.4|SN|Subject name|  
|2.5.4.5|SERIALNUMBER|Serial number|  
|2.5.4.6|C|Country code|  
|2.5.4.7|L|Locality|  
|2.5.4.8|S or ST|State or province name|  
|2.5.4.9|STREET|Street address|  
|2.5.4.10|O|Organization name|  
|2.5.4.11|OU|Organizational unit|  
|2.5.4.12|T or Title|Title|  
|2.5.4.42|G or GN or GivenName|Given name|  
|2.5.4.43|I or Initials|Initials|  
|2.5.29.17|(no value)|Subject Alternative Name|  
