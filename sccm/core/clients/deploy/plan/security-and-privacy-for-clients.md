---
title: Client security and privacy
titleSuffix: Configuration Manager
description: Learn about security and privacy for Configuration Manager clients.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Security and privacy for Configuration Manager clients

*Applies to: System Center Configuration Manager (Current Branch)*

This article describes security and privacy information for Configuration Manager clients. It also includes information for mobile devices that are managed by the [Exchange Server connector](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



##  <a name="BKMK_Security_Clients"></a> Security best practices for clients  

The Configuration Manager site accepts data from devices that run the Configuration Manager client. This behavior introduces the risk that the clients could attack the site. For example, they could send malformed inventory, or attempt to overload the site systems. Deploy the Configuration Manager client only to devices that you trust. In addition, use the following security best practices to help protect the site from rogue or compromised devices:  

#### Use public key infrastructure (PKI) certificates for client communications with site systems that run IIS  

-   As a site property, configure **Site system settings** for **HTTPS only**.  

-   Install clients with the `UsePKICert` CCMSetup property.  

-   Use a certificate revocation list (CRL) and make sure that clients and communicating servers can always access it.  

Mobile device clients and some internet-based clients require these certificates. Microsoft recommends these certificates for all client connections on the intranet.  

For more information about the PKI certificate requirements and how they're used to help protect Configuration Manager, see [PKI certificate requirements](/sccm/core/plan-design/network/pki-certificate-requirements).  


#### Automatically approve client computers from trusted domains and manually check and approve other computers  

When you can't use PKI authentication, approval identifies a computer that you trust to be managed by Configuration Manager. The hierarchy has the following options to configure client approval:  
- Manual
- Automatic for computers in trusted domains
- Automatic for all computers  

The most secure approval method is to automatically approve clients that are members of trusted domains. Then manually check and approve all other computers. Automatically approving all clients isn't recommended, unless you have other access controls to prevent untrustworthy computers from accessing your network.  

For more information about how to manually approve computers, see [Manage clients from the devices node](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode).  


#### Don't rely on blocking to prevent clients from accessing the Configuration Manager hierarchy  

Blocked clients are rejected by the Configuration Manager infrastructure. If clients are blocked, they can't communicate with site systems to download policy, upload inventory data, or send state or status messages. 

Blocking is designed for the following scenarios: 
- To block lost or compromised boot media when you deploy an OS to clients
- When all site systems accept HTTPS client connections 

When site systems accept HTTP client connections, don't rely on blocking to protect the Configuration Manager hierarchy from untrusted computers. In this scenario, a blocked client could rejoin the site with a new self-signed certificate and hardware ID. 

Certificate revocation is the primary line of defense against potentially compromised certificates. A certificate revocation list (CRL) is only available from a supported public key infrastructure (PKI). Blocking clients in Configuration Manager offers a second line of defense to protect your hierarchy.  

For more information, see [Determine whether to block clients](/sccm/core/clients/deploy/plan/determine-whether-to-block-clients).  


#### Use the most secure client installation methods that are practical for your environment  

-   For domain computers, Group Policy client installation and software update-based client installation methods are more secure than client push installation.  

-   If you apply access controls and change controls, use imaging and manual installation methods.  

-   In version 1806 or later, use Kerberos mutual authentication with client push installation.  

Of all the client installation methods, client push installation is the least secure because of the many dependencies it has. These dependencies include local administrative permissions, the Admin$ share, and firewall exceptions. The number and type of these dependencies increase your attack surface.  

Starting in version 1806, when using client push, the site can require Kerberos mutual authentication by not allowing fallback to NTLM before establishing the connection. This enhancement helps to secure the communication between the server and the client. For more information, see [How to install clients with client push](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).<!--1358204-->  

For more information about the different client installation methods, see [Client installation methods](/sccm/core/clients/deploy/plan/client-installation-methods).  

Wherever possible, select a client installation method that requires the least security permissions in Configuration Manager. Restrict the administrative users that are assigned security roles with permissions that can be used for purposes other than client deployment. For example, configuring automatic client upgrade requires the **Full Administrator** security role, which grants an administrative user all security permissions.  

For more information about the dependencies and security permissions required for each client installation method, see "Installation method dependencies" in [Prerequisites for computer clients](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#BKMK_prereqs_computers).  


#### If you must use client push installation, take additional steps to secure the Client Push Installation Account  

This account must be a member of the local **Administrators** group on each computer that installs the Configuration Manager client. Never add the Client Push Installation Account to the **Domain Admins** group. Instead, create a global group, and then add that global group to the local **Administrators** group on your clients. Create a group policy object to add a Restricted Group setting to add the Client Push Installation Account to the local **Administrators** group.  

For additional security, create multiple Client Push Installation Accounts, each with administrative access to a limited number of computers. If one account is compromised, only the client computers to which that account has access are compromised.  


#### Remove certificates before imaging clients  

When you deploy clients by using OS images, always remove certificates before capturing the image. These certificates include PKI certificates for client authentication, and self-signed certificates. If you don't remove these certificates, clients might impersonate each other. You can't verify the data for each client.  

For more information, see [Create a task sequence to capture an operating system](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).  


#### Ensure that the Configuration Manager computer clients get an authorized copy of these certificates  

-   The Configuration Manager trusted root key certificate  

    When both of the following statements are true, clients rely on the Configuration Manager trusted root key to authenticate valid management points:  

      - You haven't extended the Active Directory schema for Configuration Manager
      - Clients don't use PKI certificates when they communicate with management points  

    In this scenario, clients have no way to verify that the management point is trusted for the hierarchy unless they use the trusted root key. Without the trusted root key, a skilled attacker could direct clients to a rogue management point.  

    When clients can't download the Configuration Manager trusted root key from the Global Catalog or by using PKI certificates, pre-provision the clients with the trusted root key. This action makes sure that they can't be directed to a rogue management point. For more information, see [Planning for the trusted root key](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  

-   The site server signing certificate  

     Clients use this certificate to verify that the site server signed the policy downloaded from a management point. This certificate is self-signed by the site server and published to Active Directory Domain Services.  

     When clients can't download the site server signing certificate from the Global Catalog, by default they download it from the management point. If the management point is exposed to an untrusted network like the internet, manually install the site server signing certificate on clients. This action makes sure that they can't download tampered client policies from a compromised management point.  

     To manually install the site server signing certificate, use the CCMSetup client.msi property **SMSSIGNCERT**. For more information, see [About client installation properties](/sccm/core/clients/deploy/about-client-installation-properties).  


#### Don't use automatic site assignment if the client downloads the trusted root key from the first management point it contacts  

To avoid the risk of a new client downloading the trusted root key from a rogue management point, only use automatic site assignment in the following scenarios:  

-   The client can access Configuration Manager site information that's published to Active Directory Domain Services.  

-   You pre-provision the client with the trusted root key.  

-   You use PKI certificates from an enterprise certification authority to establish trust between the client and the management point.  

For more information about the trusted root key, see [Planning for the trusted root key](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  


#### Install client computers with the CCMSetup Client.msi option SMSDIRECTORYLOOKUP=NoWINS  

The most secure service location method for clients to find sites and management points is to use Active Directory Domain Services. Sometimes this method isn't possible for some environments. For example, because you can't extend the Active Directory schema for Configuration Manager, or because clients are in an untrusted forest or a workgroup. If this method isn't possible, use DNS publishing as an alternative service location method. If both these methods fail, and when the management point isn't configured for HTTPS client connections, clients can fall back to using WINS.  

Publishing to WINS is less secure than the other publishing methods. Configure client computers to not fall back to using WINS by specifying **SMSDIRECTORYLOOKUP=NoWINS**. If you must use WINS for service location, use **SMSDIRECTORYLOOKUP=WINSSECURE**. This setting is the default. It uses the Configuration Manager trusted root key to validate the self-signed certificate of the management point.  

> [!NOTE]  
>  When you configure the client for **SMSDIRECTORYLOOKUP=WINSSECURE** and it finds a management point from WINS, the client checks its copy of the Configuration Manager trusted root key that's in WMI.  
> 
> If the signature on the management point certificate matches the client's copy of the trusted root key, the certificate is validated. After validating the certificate, the client starts communicates with the management point that it found by using WINS.  
> 
> If the signature on the management point certificate doesn't match the client's copy of the trusted root key, the certificate isn't valid. In this scenario, the client doesn't communicate with the management point that it found by using WINS.  


#### Make sure that maintenance windows are large enough to deploy critical software updates  

Maintenance windows for device collections restrict the times that Configuration Manager can install software on these devices. If you configure the maintenance window to be too small, the client may not install critical software updates. This behavior leaves the client vulnerable to any attack that the software update mitigates.  


#### Take additional security precautions to reduce the attack surface on Windows embedded devices with write filters  

When you enable write filters on Windows Embedded devices, any software installations or changes are only made to the overlay. These changes don't persist after the device restarts. If you use Configuration Manager to disable the write filters, during this period the embedded device is vulnerable to changes to all volumes. These volumes include shared folders.  

Configuration Manager locks the computer during this period so that only local administrators can sign in. Whenever possible, take additional security precautions to help protect the computer. For example, enable additional restrictions on the firewall.  

If you use maintenance windows to persist changes, plan these windows carefully. Minimize the time that write filters are disabled, but make them long enough to allow software installations and restarts to complete.  


#### Use the latest client version with software update-based client installation

If you use software update-based client installation, and install a later version of the client on the site, update the published software update. Then clients receive the latest version from the software update point.  

When you update the site, the software update for client deployment that's published to the software update point isn't automatically updated. Republish the Configuration Manager client to the software update point and update the version number.  

For more information, see [How to install Configuration Manager clients by using software update-based installation](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientSUP).  


#### Only suspend BitLocker PIN entry on trusted and restricted-access devices  

Only configure the client setting to **Suspend BitLocker PIN entry on restart** to **Always** for computers that you trust and that have restricted physical access.

When you set this client setting to **Always**, Configuration Manager can complete the installation of software. This behavior helps install critical software updates and resume services. If an attacker intercepts the restart process, they could take control of the computer. Use this setting only when you trust the computer, and when physical access to the computer is restricted. For example, this setting might be appropriate for servers in a data center.  

For more information on this client setting, see [About client settings](/sccm/core/clients/deploy/about-client-settings#suspend-bitlocker-pin-entry-on-restart).  


#### Don't bypass PowerShell execution policy   

If you configure the Configuration Manager client setting for **PowerShell execution policy** to **Bypass**, then Windows allows unsigned PowerShell scripts to run. This behavior could allow malware to run on client computers. When your organization requires this option, use a custom client setting. Assign it to only the client computers that must run unsigned PowerShell scripts.  

For more information on this client setting, see [About client settings](/sccm/core/clients/deploy/about-client-settings#powershell-execution-policy).  



##  <a name="bkmk_mobile"></a> Security best practices for mobile devices  


#### Install the enrollment proxy point in a perimeter network and the enrollment point in the intranet  

For internet-based mobile devices that you enroll with Configuration Manager, install the enrollment proxy point in a perimeter network and the enrollment point in the intranet. This role separation helps to protect the enrollment point from attack. If an attacker compromises the enrollment point, they could obtain certificates for authentication. They can also steal the credentials of users who enroll their mobile devices.  


#### Configure the password settings to help protect mobile devices from unauthorized access  

*For mobile devices that are enrolled by Configuration Manager*: Use a mobile device configuration item to configure the password complexity as the PIN. Specify at least the default minimum password length.  

*For mobile devices that don't have the Configuration Manager client installed but are managed by the Exchange Server connector*: Configure the **Password Settings** for the Exchange Server connector such that the password complexity is the PIN. Specify at least the default minimum password length.  


#### Only allow applications to run that are signed by companies that you trust  

Help prevent tampering of inventory information and status information by allowing applications to run only when they're signed by companies that you trust. Don't allow devices to install unsigned files.  

*For mobile devices that are enrolled by Configuration Manager*: Use a mobile device configuration item to configure the security setting **Unsigned applications** as **Prohibited**. Configure **Unsigned file installations** to be a trusted source.  

*For mobile devices that don't have the Configuration Manager client installed but are managed by the Exchange Server connector*: Configure the **Application Settings** for the Exchange Server connector such that **Unsigned file installation** and **Unsigned applications** are **Prohibited**.  


#### Lock mobile devices when not in use  

Help prevent elevation of privilege attacks by locking the mobile device when it isn't used.

*For mobile devices that are enrolled by Configuration Manager*: Use a mobile device configuration item to configure the password setting **Idle time in minutes before mobile device is locked**.  

*For mobile devices that don't have the Configuration Manager client installed but are managed by the Exchange Server connector*: Configure the **Password Settings** for the Exchange Server connector to set the **Idle time in minutes before mobile device is locked**.  


#### Restrict the users who can enroll their mobile devices  

Help prevent elevation of privileges by restricting the users who can enroll their mobile devices. Use a custom client setting rather than default client settings to allow only authorized users to enroll their mobile devices.  


#### User device affinity guidance for mobile devices  

Don't deploy applications to users who have mobile devices enrolled by Configuration Manager or Microsoft Intune in the following scenarios:  

-   The mobile device is used by more than one person.  

-   The device is enrolled by an administrator on behalf of a user.  

-   The device is transferred to another person without retiring and then re-enrolling the device.  

Device enrollment creates a user device affinity relationship. This relationship maps the user who performs enrollment to the mobile device. If another user uses the mobile device, they can run the applications deployed to the original user, which might result in an elevation of privileges. Similarly, if an administrator enrolls the mobile device for a user, applications deployed to the user aren't installed on the mobile device. Instead, applications deployed to the administrator might be installed.  

Unlike user device affinity for Windows computers, you can't manually define the user device affinity information for mobile devices enrolled by Microsoft Intune.  

If you transfer ownership of a mobile device that's enrolled by Intune, first retire the mobile device from Intune. This action removes the user device affinity relationship. Then ask the current user to enroll the device again.  


#### Make sure that users enroll their own mobile devices for Microsoft Intune  

A user device affinity relationship is created during enrollment. This action maps the user who performs enrollment to the mobile device. If an administrator enrolls the mobile device for a user, applications deployed to the user aren't installed on the mobile device. Instead, applications deployed to the administrator might be installed.  


#### Protect the connection between the Configuration Manager site server and the Exchange Server   

If the Exchange Server is on-premise, use IPsec. Hosted Exchange automatically secures the connection by using SSL.  


#### Use the principle of least privileges for the connector  

For a list of the minimum cmdlets that the Exchange Server connector requires, see [Manage mobile devices with Configuration Manager and Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



##  <a name="bkmk_macs"></a> Security best practices for Macs  


#### Store and access the client source files from a secured location  

Before installing or enrolling the client on Mac computer, Configuration Manager doesn't verify whether these client source files have been tampered with. Download these files from a trustworthy source. Securely store and access them.  


#### Monitor and track the validity period of the certificate  

To ensure business continuity, monitor and track the validity period of the certificates that you use for Mac computers. Configuration Manager doesn't support automatic renewal of this certificate, or warn you that the certificate is about to expire. A typical validity period is one year.  

For more information about how to renew the certificate, see [Renewing the Mac client certificate manually](/sccm/core/clients/deploy/deploy-clients-to-macs#renewing-the-mac-client-certificate).  


#### Configure the trusted root certificate for SSL only  

To help protect against elevation of privileges, configure the certificate for the trusted root certificate authority so that it's only trusted for the SSL protocol.

When you enroll Mac computers, a user certificate to manage the Configuration Manager client is automatically installed. This user certificate includes the trusted root certificates in its trust chain. To restrict the trust of this root certificate to the SSL protocol only, use the following procedure:  

1.  On the Mac computer, open a terminal window.  

2.  Enter the following command: `sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3.  In the **Keychain Access** dialog box, in the **Keychains** section, click **System**. Then in the **Category** section, click **Certificates**.  

4.  Locate and double-click the root CA certificate for the Mac client certificate.  

5.  In the dialog box for the root CA certificate, expand the **Trust** section, and then make the following changes:  

    1.  **When using this certificate**: Change the **Always Trust** setting to **Use System Defaults**.  

    2.  **Secure Sockets Layer (SSL)**: Change **no value specified** to **Always Trust**.  

6.  Close the dialog box. When prompted, enter the administrator's password, and then click **Update Settings**.  

After you complete this procedure, the root certificate is only trusted to validate the SSL protocol. Other protocols that are now untrusted with this root certificate include Secure Mail (S/MIME), Extensible Authentication (EAP), or code signing.  

> [!NOTE]  
>  Also use this procedure if you installed the client certificate independently from Configuration Manager.  



##  <a name="BKMK_SecurityIssues_Clients"></a> Security issues for Configuration Manager clients  

The following security issues have no mitigation:  


#### Status messages aren't authenticated  

No authentication is performed on status messages. When a management point accepts HTTP client connections, any device can send status messages to the management point. If the management point accepts HTTPS client connections only, a device must have a valid client authentication certificate, but could also send any status message. The management point discards any invalid status message received from a client.  

There are a few potential attacks against this vulnerability: 
- An attacker could send a bogus status message to gain membership in a collection that's based on status message queries. 
- Any client could launch a denial of service against the management point by flooding it with status messages. 
- If status messages are triggering actions in status message filter rules, an attacker could trigger the status message filter rule. 
- An attacker could send status message that would render reporting information inaccurate.  


#### Policies can be retargeted to non-targeted clients  

There are several methods that attackers could use to make a policy targeted to one client apply to an entirely different client. For example, an attacker at a trusted client could send false inventory or discovery information to have the computer added to a collection to which it shouldn't belong. That client then receives all the deployments to that collection. 

Controls exist to help prevent attackers from directly modifying policy. However, attackers could take an existing policy that reformats and redeploys an OS and send it to a different computer. This redirected policy could create a denial of service. These types of attacks would require precise timing and extensive knowledge of the Configuration Manager infrastructure.  


#### Client logs allow user access  

All the client log files allow the **Users** group with *Read* access, and the special **Interactive** user with *Write* access. If you enable verbose logging, attackers might read the log files to look for information about compliance or system vulnerabilities. Processes such as software that the client installs in a user's context must write to logs with a low-rights user account. This behavior means an attacker could also write to the logs with a low-rights account.  

The most serious risk is that an attacker could remove information in the log files. An administrator might need this information for auditing and intrusion detection.  


#### A computer could be used to obtain a certificate that's designed for mobile device enrollment  

When Configuration Manager processes an enrollment request, it can't verify the request originated from a mobile device rather than from a computer. If the request is from a computer, it can install a PKI certificate that then allows it to register with Configuration Manager. 

To help prevent an elevation of privilege attack in this scenario, only allow trusted users to enroll their mobile devices. Carefully monitor device enrollment activities in the site.  


#### A blocked client can still send messages to the management point

When you block a client that you no longer trust, but it established a network connection for client notification, Configuration Manager doesn't disconnect the session. The blocked client can continue to send packets to its management point until the client disconnects from the network. These packets are only small, keep-alive packets. This client can't be managed by Configuration Manager until it's unblocked.  


#### Automatic client upgrade doesn't verify the management point

When you use automatic client upgrade, the client can be directed to a management point to download the client source files. In this scenario, the client doesn't verify the management point as a trusted source.  


#### When users first enroll Mac computers, they're at risk from DNS spoofing  

When the Mac computer connects to the enrollment proxy point during enrollment, it's unlikely that the Mac computer already has the trusted root CA certificate. At this point, the Mac computer doesn't trust the server, and prompts the user to continue. If a rogue DNS server resolves the fully qualified domain name (FQDN) of the enrollment proxy point, it could direct the Mac computer to a rogue enrollment proxy point to install certificates from an untrusted source. To help reduce this risk, follow best practices to avoid DNS spoofing in your environment.  


#### Mac enrollment doesn't limit certificate requests  

Users can re-enroll their Mac computers, each time requesting a new client certificate. Configuration Manager doesn't check for multiple requests or limit the number of certificates requested from a single computer. A rogue user could run a script that repeats the command-line enrollment request. This attack could cause a denial of service on the network or on the issuing certificate authority (CA). To help reduce this risk, carefully monitor the issuing CA for this type of suspicious behavior. Immediately block from the Configuration Manager hierarchy any computer that shows this pattern of behavior.  


#### A wipe acknowledgment doesn't verify that the device has been successfully wiped  

When you initiate a wipe action for a mobile device, and Configuration Manager acknowledges the wipe, the verification is that Configuration Manager successfully *sent* the message. It doesn't verify that the device *acted* on the request. 

For mobile devices managed by the Exchange Server connector, a wipe acknowledgment verifies that the command was received by Exchange, not by the device.  


#### If you use the options to commit changes on Windows Embedded devices, accounts might be locked out sooner than expected  

If the Windows Embedded device is running an OS version prior to Windows 7, and a user attempts to sign in while the write filters are disabled by Configuration Manager, Windows allows only half of the configured number of incorrect attempts before the account is locked out. 

For example, you configure the domain policy for **Account lockout threshold** to six attempts. A user mistypes their password three times, and the account is locked out. This behavior effectively creates a denial of service. If users must sign in to embedded devices in this scenario, caution them about the potential for a reduced lockout threshold.  



##  <a name="BKMK_Privacy_Clients"></a> Privacy information for Configuration Manager clients  

When you deploy the Configuration Manager client, you enable client settings for Configuration Manager features. The settings that you use to configure the features can apply to all clients in the Configuration Manager hierarchy. This behavior is the same whether they're directly connected to the internal network, connected through a remote session, or connected to the internet.  

Client information is stored in the Configuration Manager database in your SQL server, and isn't sent to Microsoft. Information is retained in the database until it's deleted by the site maintenance tasks **Delete Aged Discovery Data** every 90 days. You can configure the deletion interval. 

Some summarized or aggregate diagnostics and usage data is sent to Microsoft. For more information, see [Diagnostics and usage data](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  

Before you configure the Configuration Manager client, consider your privacy requirements.  


### Privacy information for mobile devices that are enrolled by Configuration Manager  

For privacy information when you enroll a mobile device by Configuration Manager, see [System Center Configuration Manager privacy statement - Mobile device addendum](/sccm/core/misc/privacy/privacy-statement-mobile-device-addendum).  


### Client status  

Configuration Manager monitors the activity of clients. It periodically evaluates the Configuration Manager client and can remediate issues with the client and its dependencies. Client status is enabled by default. It uses server-side metrics for the client activity checks. Client status uses client-side actions for self-checks, remediation, and for sending client status information to the site. The client runs the self-checks according to a schedule that you configure. The client sends the results of the checks to the Configuration Manager site. This information is encrypted during transfer.  

Client status information is stored in the Configuration Manager database in your SQL server, and isn't sent to Microsoft. The information isn't stored in encrypted format in the site database. This information is retained in the database until it's deleted according to the value configured for the **Retain client status history for the following number of days** client status setting. The default value for this setting is every 31 days.  

Before you install the Configuration Manager client with client status checking, consider your privacy requirements.  



##  <a name="BKMK_Privacy_ExchangeConnector"></a> Privacy information for mobile devices that are managed with the Exchange Server Connector  

The Exchange Server Connector finds and manages devices that connect to an on-premises or hosted Exchange Server by using the ActiveSync protocol. The records found by the Exchange Server Connector are stored in the Configuration Manager database in your SQL server. The information is collected from the Exchange Server. It doesn't contain any additional information from what the mobile devices send to Exchange Server.  

The mobile device information isn't sent to Microsoft. The mobile device information is stored in the Configuration Manager database in your SQL server. Information is retained in the database until it's deleted by the site maintenance task **Delete Aged Discovery Data** every 90 days. You configure the deletion interval.  

Before you install and configure the Exchange Server connector, consider your privacy requirements.  
