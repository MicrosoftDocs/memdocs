---
title: "Client security and privacy | Microsoft Docs"
description: "Learn about security and privacy for clients in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
caps.latest.revision: 10
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# Security and privacy for clients in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article contains security and privacy information for clients in System Center Configuration Manager and for mobile devices that are managed by the Exchange Server connector:  

##  <a name="BKMK_Security_Cliients"></a> Security best practices for clients  
 When Configuration Manager accepts data from devices that run the Configuration Manager client, this introduces the risk that the clients could attack the site. For example, they could send malformed inventory, or attempt to overload the site systems. Deploy the Configuration Manager client only to devices that you trust. In addition, use the following security best practices to help protect the site from rogue or compromised devices:  

 **Use public key infrastructure (PKI) certificates for client communications with site systems that run IIS.**  

-   As a site property, configure **Site system settings** for **HTTPS only**.  

-   Install clients with the **/UsePKICert** CCMSetup property  

-   Use a certificate revocation list (CRL) and make sure that clients and communicating servers can always access it.  

 These certificates are required for mobile device clients and for client computer connections on the Internet, and, with the exception of distribution points, are recommended for all client connections on the intranet.  

 For more information about the PKI certificate requirements and how they are used to help protect Configuration Manager, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Automatically approve client computers from trusted domains and manually check and approve other computers**  

 You can configure approval for the hierarchy as manual, automatic for computers in trusted domains, or automatic for all computers. The most secure approval method is to automatically approve clients that are members of trusted domains, and then manually check and approve all other computers. Automatically approving all clients is not recommended unless you have other access controls to prevent untrustworthy computers from accessing your network.  

 Approval identifies a computer that you trust to be managed by Configuration Manager when you cannot use PKI authentication.  

 For more information about how to manually approve computers, see [Manage Clients from the Devices Node](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 **Do not rely on blocking to prevent clients from accessing the Configuration Manager hierarchy**  

 Blocked clients are rejected by the Configuration Manager infrastructure so that they cannot communicate with site systems to download policy, upload inventory data, or send state or status messages. However, do not rely on blocking to protect the Configuration Manager hierarchy from untrusted computers when site systems accept HTTP client connections. In this scenario, a blocked client could re-join the site with a new self-signed certificate and hardware ID. Blocking is designed to be used to block lost or compromised boot media when you deploy an operating system to clients and when all site systems accept HTTPS client connections. If you use a public key infrastructure (PKI) and it supports a certificate revocation list (CRL), always consider certificate revocation to be the primary line of defense against potentially compromised certificates. Blocking clients in Configuration Manager offers a second line of defense to protect your hierarchy.  

 For more information, see [Determine whether to block clients in System Center Configuration Manager](../../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

 **Use the most secure client installation methods that are practical for your environment:**  

-   For domain computers, Group Policy client installation and software update-based client installation methods are more secure than client push installation.  

-   Imaging and manual installation can be very secure if you apply access controls and change controls.  

 Of all the client installation methods, client push installation is the least secure because of the many dependencies it has, which includes local administrative permissions, the Admin$ share, and many firewall exceptions. These dependencies increase your attack surface.  

 For more information about the different client installation methods, see [Client installation methods in System Center Configuration Manager](../../../../core/clients/deploy/plan/client-installation-methods.md).  

 In addition, wherever possible, select a client installation method that requires the least security permissions in Configuration Manager, and restrict the administrative users that are assigned security roles that include permissions that can be used for purposes other than client deployment. For example, automatic client upgrade requires the **Full Administrator** security role, which grants an administrative user all security permissions.  

 For more information about the dependencies and security permissions required for each client installation method, see "Installation Method Dependencies" in [Prerequisites for Computer Clients](../../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

 **If you must use client push installation, take additional steps to secure the Client Push Installation Account**  

 Although this account must be a member of the local **Administrators** group on each computer that will install the Configuration Manager client software, never add the Client Push Installation Account to the **Domain Admins** group. Instead, create a global group and add that global group to the local **Administrators** group on your client computers. You can also create a Group Policy object to add a Restricted Group setting to add the Client Push Installation Account to the local **Administrators** group.  

 For additional security, create multiple Client Push Installation Accounts, each with administrative access to a limited number of computers so that if one account is compromised, only the client computers to which that account has access are compromised.  

 **Remove certificates prior to imaging client computer**  

 If you plan to deploy clients by using imaging technology, always remove certificates such as PKI certificates that include client authentication and self-signed certificates prior to capturing the image. If you do not remove these certificates, clients might impersonate each other and you would not be able to verify the data for each client.  

 For more information about using Sysprep to prepare a computer for imaging, see your Windows deployment documentation..  

 **Ensure that the Configuration Manager computer clients get an authorized copy of these certificates:**  

-   The Configuration Manager trusted root key  

     If you have not extended the Active Directory schema for Configuration Manager, and clients do not use PKI certificates when they communicate with management points, clients rely on the Configuration Manager trusted root key to authenticate valid management points. In this scenario, clients have no way to verify that the management point is a trusted management point for the hierarchy unless they use the trusted root key. Without the trusted root key, a skilled attacker could direct clients to a rogue management point.  

     When clients cannot download the Configuration Manager trusted root key from the Global Catalog or by using PKI certificates, pre-provision the clients with the trusted root key to make sure that they cannot be directed to a rogue management point. For more information, see [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

-   The site server signing certificate  

     Clients use the site server signing certificate to verify that the site server signed the client policy that they download from a management point. This certificate is self-signed by the site server and published to Active Directory Domain Services.  

     When clients cannot download the site server signing certificate from the Global Catalog, by default they download it from the management point. When the management point is exposed to an untrusted network (such as the Internet), manually install the site server signing certificate on clients to make sure that they cannot run client policies that have been tampered with from  a compromised management point.  

     To manually install the site server signing certificate, use the CCMSetup client.msi property **SMSSIGNCERT**. For more information, see [About client installation properties in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

 **Do not use automatic site assignment if the client will download the trusted root key from the first management point it contacts**  

 This security best practice is linked to the preceding entry. To avoid the risk of a new client downloading the trusted root key from a rogue management point, use automatic site assignment in the following scenarios only:  

-   The client can access Configuration Manager site information that is published to Active Directory Domain Services.  

-   You pre-provision the client with the trusted root key.  

-   You use PKI certificates from an enterprise certification authority to establish trust between the client and the management point.  

 For more information about the trusted root key, see [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 **Install client computers with the CCMSetup Client.msi option SMSDIRECTORYLOOKUP=NoWINS**  

 The most secure service location method for clients to find sites and management points is to use Active Directory Domain Services. If this is not possible, for example, because you cannot extend the Active Directory schema for Configuration Manager, or because clients are in an untrusted forest or a workgroup, you can use DNS publishing as an alternative service location method. If both these methods fail, clients can fall back to using WINS when the management point is not configured for HTTPS client connections.  

 Because publishing to WINS is less secure than the other publishing methods, configure client computers to not fall back to using WINS by specifying SMSDIRECTORYLOOKUP=NoWINS. If you must use WINS for service location, use SMSDIRECTORYLOOKUP=WINSSECURE (the default setting), which uses the Configuration Manager trusted root key to validate the self-signed certificate of the management point.  

> [!NOTE]  
>  When the client is configured for SMSDIRECTORYLOOKUP=WINSSECURE and finds a management point from WINS, the client checks its copy of the Configuration Manager trusted root key that is in WMI. If the signature on the management point certificate matches the client's copy of the trusted root key, the certificate is validated, and the client communicates with the management point that it found by using WINS. If the signature on the management point certificate does not match the client's copy of the trusted root key, the certificate is not valid and the client will not communicate with the management point that it found by using WINS.  

 **Make sure that maintenance windows are large enough to deploy critical software updates**  

 You can configure maintenance windows for device collections to restrict the times that Configuration Manager can install software on these devices. If you configure the maintenance window to be too small, the client might not be able to install critical software updates, which leaves the client vulnerable to the attack that is mitigated by the software update.  

 **For Windows embedded devices that have write filters, take additional security precautions to reduce the attack surface if Configuration Manager disables the write filters to persist software installations and changes**  

 When write filters are enabled on Windows Embedded devices, any software installations or changes are made to the overlay only and do not persist after the device restarts. If you use Configuration Manager to temporarily disable the write filters to persist software installations and changes, during this period, the embedded device is vulnerable to changes to all volumes, which includes shared folders.  

 Although Configuration Manager locks the computer during this period so that only local administrators can log on, whenever possible, take additional security precautions to help protect the computer. For example, enable additional restrictions on the firewall and disconnect the device from the network.  

 If you use maintenance windows to persist changes, plan these windows carefully to minimize the time that write filters might be disabled but long enough to allow software installations and restarts to complete.  

 **If you use software update-based client installation and install a later version of the client on the site, update the software update that is published on the software update point so that clients receive the latest version**  

 If you install a later version of the client on the site, for example, you upgrade the site, the software update for client deployment that is published to the software update point is not automatically updated. You must republish the Configuration Manager client to the software update point and click **Yes** to update the version number.  

 For more information, see the procedure "To publish the Configuration Manager client to the software update point" in [How to Install Configuration Manager Clients by Using Software Update-Based Installation](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

 **Configure the Computer Agent client device setting Suspend BitLocker PIN entry on restart to be Always only for computers that you trust and that have restricted physical access**  

 When you set this client setting to **Always**, Configuration Manager can complete the installation of software to help to ensure that critical software updates are installed and that services are resumed. However, if an attacker intercepts the restart process, she could take control of the computer. Use this setting only when you trust the computer and when physical access to the computer is restricted. As an example, this setting might be appropriate for servers in a data center.  

 **Do not configure the Computer Agent client device setting PowerShell execution policy to be Bypass.**  

 This client setting allows the Configuration Manager client to run unsigned PowerShell scripts, which could allow malware to run on client computers. If you must select this option, use a custom client setting and assign it to only the client computers that must run unsigned PowerShell scripts.  

##  <a name="bkmk_mobile"></a> Security best practices for mobile devices  
 **For mobile devices that you enroll with Configuration Manager and will supported on the Internet: Install the enrollment proxy point in a perimeter network and the enrollment point in the intranet**  

 This role separation helps to protect the enrollment point from attack. If the enrollment point is compromised, an attacker could obtain certificates for authentication and steal the credentials of users who enroll their mobile devices.  

 **For mobile devices: Configure the password settings to help protect mobile devices from unauthorized access**  

 For mobile devices that are enrolled by Configuration Manager: Use a mobile device configuration item to configure the password complexity to be the PIN and at least the default length for the minimum password length.  

 For mobile devices that do not have the Configuration Manager client installed but that are managed by the Exchange Server connector: Configure the **Password Settings** for the Exchange Server connector such that the password complexity is the PIN and specify at least the default length for the minimum password length.  

 **For mobile devices: Help prevent tampering of inventory information and status information by allowing applications to run only when they are signed by companies that you trust and do not allow unsigned files to be installed**  

 For more mobile devices that are enrolled by Configuration Manager: Use a mobile device configuration item to configure the security setting **Unsigned applications** as **Prohibited** and configure **Unsigned file installations** to be a trusted source.  

 For mobile devices that do not have the Configuration Manager client installed but that are managed by the Exchange Server connector: Configure the **Application Settings** for the Exchange Server connector such that **Unsigned file installation** and **Unsigned applications** are configured as **Prohibited**.  

 **For mobile devices: Help prevent elevation of privilege attacks by locking the mobile device when it is not used**  

 For more mobile devices that are enrolled by Configuration Manager: Use a mobile device configuration item to configure the password setting **Idle time in minutes before mobile device is locked**.  

 For mobile devices that do not have the Configuration Manager client installed but that are managed by the Exchange Server connector: Configure the **Password Settings** for the Exchange Server connector to configure **Idle time in minutes before mobile device is locked**.  

 **For mobile devices: Help prevent elevation of privileges by restricting the users who can enroll their mobile devices.**  

 Use a custom client setting rather than default client settings to allow only authorized users to enroll their mobile devices.  

 **For mobile devices: Do not deploy applications to users who have mobile devices enrolled by Configuration Manager or Microsoft Intune in the following scenarios:**  

-   When the mobile device is used by more than one person.  

-   When the device is enrolled by an administrator on behalf of a user.  

-   When the device is transferred to another person without retiring and then re-enrolling the device.  

 A user device affinity relationship is created during enrollment, which maps the user who performs enrollment to the mobile device. If another user uses the mobile device, they will be able to run the applications that you deploy to the original user, which might result in an elevation of privileges. Similarly, if an administrator enrolls the mobile device for a user, applications deployed to the user will not be installed on the mobile device and instead, applications that are deployed to the administrator might be installed.  

 Unlike user device affinity for Windows computers, you cannot manually define the user device affinity information for mobile devices that are enrolled by Microsoft Intune.  

 If you transfer ownership of a mobile device that is enrolled by Intune, retire the mobile device from Intune to remove the user device affinity, and then ask the current user to enroll the device again.  

 **For mobile devices: Make sure that users enroll their own mobile devices for Microsoft Intune**  

 Because a user device affinity relationship is created during enrollment, which maps the user who performs enrollment to the mobile device, if an administrator enrolls the mobile device for a user, applications deployed to the user will not be installed on the mobile device and instead, applications that are deployed to the administrator might be installed.  

 **For the Exchange Server connector: Make sure that the connection between the Configuration Manager site server and the Exchange Server computer is protected**  

 Use IPsec if the Exchange Server is on-premise; hosted Exchange automatically secures the connection by using SSL.  

 **For the Exchange Server connector: Use the principle of least privileges for the connector**  

 For a list of the minimum cmdlets that the Exchange Server connector requires, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

##  <a name="bkmk_macs"></a> Security best practices for Macs  
 **For Mac computers: Store and access the client source files from a secured location.**  

 Configuration Manager does not verify whether these client source files have been tampered with before installing or enrolling the client on Mac computer. Download these files from a trustworthy source and store and access them securely.  

 **For Mac computers: Independently from Configuration Manager, monitor and track the validity period of the certificate that enrolled to users.**  

 To ensure business continuity, monitor and track the validity period of the certificates that you use for Mac computers. Configuration Manager does not support automatic renewal of this certificate or warn you that the certificate is about to expire. A typical validity period is 1 year.  

 For information about how to renew the certificate, see  [Renewing the Mac Client Certificate Manually](../../../../core/clients/deploy/deploy-clients-to-macs.md#renewing-the-mac-client-certificate).  

 **For Mac computers: Consider configuring the trusted root CA certificate such that it is trusted for the SSL protocol only, to help protect against elevation of privileges.**  

 When you enroll Mac computers, a user certificate to manage the Configuration Manager client is automatically installed, together with the trusted root certificate that the user certificate chains to. If you want to restrict the trust of this root certificate to the SSL protocol only, you can use the following procedure.  

 After you complete this procedure, the root certificate would not be trusted to validate protocols other than SSL - for example, Secure Mail (S/MIME), Extensible Authentication (EAP), or code signing.  

> [!NOTE]  
>  You can also use this procedure if you installed the client certificate independently from Configuration Manager.  

 To restrict the root CA certificate to the SSL protocol only:  

1.  On the Mac computer, open a terminal window.  

2.  Enter the command **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

3.  In the **Keychain Access** dialog box, in the **Keychains** section, click **System**, and then, in the **Category** section, click **Certificates**.  

4.  Locate and then double-click the root CA certificate for the Mac client certificate.  

5.  In the dialog box for the root CA certificate, expand the **Trust** section, and then make the following changes:  

    1.  For the **When using this certificate** setting, change the **Always Trust** default setting to **Use System Defaults**.  

    2.  For the **Secure Sockets Layer (SSL)** setting, change the **no value specified** to **Always Trust**.  

6.  Close the dialog box, and when prompted, enter the administrator's password, and then click **Update Settings**.  

##  <a name="BKMK_SecurityIssues_Clients"></a> Security issues for Configuration Manager clients  
 The following security issues have no mitigation:  

-   Status messages are not authenticated  

     No authentication is performed on status messages. When a management point accepts HTTP client connections, any device can send status messages to the management point. If the management point accepts HTTPS client connections only, a device must obtain a valid client authentication certificate from a trusted root certification authority, but could also then send any status message. If a client sends an invalid status message it will be discarded.  

     There are a few potential attacks against this vulnerability. An attacker could send a bogus status message to gain membership in a collection that is based on status message queries. Any client could launch a denial of service against the management point by flooding it with status messages. If status messages are triggering actions in status message filter rules, an attacker could trigger the status message filter rule. An attacker could also send status message that would render reporting information inaccurate.  

-   Policies can be retargeted to non-targeted clients  

     There are several methods that attackers could use to make a policy targeted to one client apply to an entirely different client. For example, an attacker at a trusted client could send false inventory or discovery information to have the computer added to a collection it should not belong to, and then receive all the deployments to that collection. While controls exist to help prevent attackers from modifying policy directly, attackers could take an existing policy to reformat and redeploy an operating system and send it to a different computer, creating a denial of service. These types of attacks would require precise timing and extensive knowledge of the Configuration Manager infrastructure.  

-   Client logs allow user access  

     All the client log files allow users Read access and Interactive Users Write access. If you enable verbose logging, attackers might read the log files to look for information about compliance or system vulnerabilities. Processes such as software installation that are performed in a user's context must be able to write to logs with a low-rights user account. This means an attacker could also write to the logs with a low rights account.  

     The most serious risk is that an attacker could remove information in the log files that an administrator might need for auditing and intruder detection.  

-   A computer could be used to obtain a certificate that is designed for mobile device enrollment  

     When Configuration Manager process an enrollment request, it cannot verify that the request originated from a mobile device rather than from a computer. If the request is from a computer, it can install a PKI certificate that then allows it to register with Configuration Manager. To help prevent an elevation of privilege attack in this scenario, only allow trusted users to enroll their mobile devices and carefully monitor enrollment activities.  

-   The connection from a client to the management point is not dropped if you block a client and the blocked client could continue to send client notification packets to the management point, as keep-alive messages  

     When you block a client that you no longer trust, and it has established a client notification communication, Configuration Manager does not disconnect the session. The blocked client can continue to send packets to its management point until the client disconnects from the network. These packets are only small, keep-alive packets and these clients cannot be managed by Configuration Manager until they are unblocked.  

-   When you use automatic client upgrade and the client is directed to a management point to download the client source files, the management point is not verified as a trusted source  

-   When users first enroll Mac computers, they are at risk from DNS spoofing  

     When the Mac computer connects to the enrollment proxy point during enrollment, it is unlikely that the Mac computer will already have the root CA certificate. At this point, the server is untrusted by the Mac computer and prompts the user to continue. If the fully qualified name of the enrollment proxy point is resolved by a rogue DNS server, it could direct the Mac computer to a rogue enrollment proxy point, and install certificates from an untrusted source. To help reduce this risk, follow best practices to avoid DNS spoofing in your environment.  

-   Mac enrollment does not limit certificate requests  

     Users can re-enroll their Mac computers, each time requesting a new client certificate. Configuration Manager does not check for multiple requests or limit the number of certificates requested from a single computer. A rogue user could run a script that repeats the command-line enrollment request, causing a denial of service on the network or on the issuing certification authority (CA). To help reduce this risk, carefully monitor the issuing CA for this type of suspicious behavior. A computer that shows this pattern of behavior should be immediately blocked from the Configuration Manager hierarchy.  

-   A wipe acknowledgment does not verify that the device has been successfully wiped  

     When you initiate a wipe action for a mobile device and Configuration Manager displays the wipe status to be acknowledged, the verification is that Configuration Manager successfully sent the message and not that the device acted on it. In addition, for mobile devices that are managed by the Exchange Server connector, a wipe acknowledgment verifies that the command was received by Exchange, not by the device.  

-   If you use the options to commit changes on Windows Embedded devices , accounts might be locked out sooner than expected  

     If the Windows Embedded device is running an operating system that is prior to Windows 7 and a user attempts to log on while the write filters are disabled to commit changes made by Configuration Manager, the number of incorrect logon attempts that are allowed before the account is locked out is effectively halved. For example, if the **Account Lockout Threshhold** is configured as 6 and a user mistypes their password 3 times, the account is locked out, effectively creating a denial of service situation.  If users must log on to embedded devices in this scenario, caution them about the potential for a reduced lockout threshold.  

##  <a name="BKMK_Privacy_Cliients"></a> Privacy information for Configuration Manager clients  
 When you deploy the Configuration Manager client, you enable client settings so you can use Configuration Manager management features. The settings that you use to configure the features can apply to all clients in the Configuration Manager hierarchy, regardless of whether they are directly connected to the corporate network, connected through a remote session, or connected to the Internet but supported by Configuration Manager.  

 Client information is stored in the Configuration Manager database and is not sent to Microsoft. Information is retained in the database until it is deleted by the site maintenance tasks **Delete Aged Discovery Data** every 90 days. You can configure the deletion interval.  

 Before you configure the Configuration Manager client, consider your privacy requirements.  

### Privacy information for mobile devices that are enrolled by Configuration Manager  
 For privacy information for when you enroll a mobile device by Configuration Manager, see [System Center Configuration Manager privacy statement - Mobile device addendum](../../../../core/misc/privacy/privacy-statement-mobile-device-addendum.md).  

### Client status  
 Configuration Manager monitors the activity of clients and periodically evaluates and can remediate the Configuration Manager client and its dependencies. Client status is enabled by default, and it uses server-side metrics for the client activity checks, and client-side actions for self-checks, remediation, and for sending client status information to the Configuration Manager site. The client runs the self-checks according to a schedule that you can configure. The client sends the results of the checks to the Configuration Manager site. This information is encrypted during transfer.  

 Client status information is stored in the Configuration Manager database and is not sent to Microsoft. The information is not stored in encrypted format in the site database. This information is retained in the database until it is deleted according to the value that is configured for the **Retain client status history for the following number of days** client status setting. The default value for this setting is every 31 days.  

 Before you install the Configuration Manager client with client status checking, consider your privacy requirements.  

##  <a name="BKMK_Privacy_ExchangeConnector"></a> Privacy information for mobile devices that are managed with the Exchange Server Connector  
 The Exchange Server Connector finds and manages devices that connect to Exchange Server (on-premise or hosted) by using the ActiveSync protocol. The records found by the Exchange Server Connector are stored in the Configuration Manager database. The information is collected from Exchange Server. It does not contain any additional information from what the mobile devices send to Exchange Server.  

 The mobile device information is not sent to Microsoft. The mobile device information is stored in the Configuration Manager database. Information is retained in the database until it is deleted by the site maintenance tasks **Delete Aged Discovery Data** every 90 days. You can configure the deletion interval.  

 Before you install and configure the Exchange Server connector, consider your privacy requirements.  
