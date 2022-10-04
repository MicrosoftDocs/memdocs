---
title: Client security and privacy
titleSuffix: Configuration Manager
description: Learn about security and privacy for Configuration Manager clients.
ms.date: 05/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Security and privacy for Configuration Manager clients

*Applies to: Configuration Manager (current branch)*

This article describes security and privacy information for Configuration Manager clients. It also includes information for mobile devices that are managed by the [Exchange Server connector](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

## Security guidance for clients

The Configuration Manager site accepts data from devices that run the Configuration Manager client. This behavior introduces the risk that the clients could attack the site. For example, they could send malformed inventory, or attempt to overload the site systems. Deploy the Configuration Manager client only to devices that you trust.

Use the following security guidance to help protect the site from rogue or compromised devices.

### Use public key infrastructure (PKI) certificates for client communications with site systems that run IIS

- As a site property, configure **Site system settings** for **HTTPS only**. For more information, see [Configure security](../../../plan-design/security/configure-security.md#client-pki-certificates).

- Install clients with the [UsePKICert](../about-client-installation-properties.md#usepkicert) CCMSetup property.

- Use a [certificate revocation list](../../../plan-design/security/plan-for-certificates.md#pki-certificate-revocation) (CRL). Make sure that clients and communicating servers can always access it.

Mobile device clients and some internet-based clients require these certificates. Microsoft recommends these certificates for all client connections on the intranet.  

For more information on the use of certificates in Configuration Manager, see [Plan for certificates](../../../plan-design/security/plan-for-certificates.md).

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

### Automatically approve client computers from trusted domains and manually check and approve other computers

When you can't use PKI authentication, approval identifies a computer that you trust to be managed by Configuration Manager. The hierarchy has the following options to configure client approval:

- Manual
- Automatic for computers in trusted domains
- Automatic for all computers

The most secure approval method is to automatically approve clients that are members of trusted domains. This option includes cloud-domain joined clients from connected Azure Active Directory (Azure AD) tenants.<!-- MEMDocs#318 --> Then manually check and approve all other computers. Automatically approving all clients isn't recommended, unless you have other access controls to prevent untrustworthy computers from accessing your network.

For more information about how to manually approve computers, see [Manage clients from the devices node](../../manage/manage-clients.md#manage-clients-from-the-devices-node).

### Don't rely on blocking to prevent clients from accessing the Configuration Manager hierarchy  

Blocked clients are rejected by the Configuration Manager infrastructure. If clients are blocked, they can't communicate with site systems to download policy, upload inventory data, or send state or status messages.

Blocking is designed for the following scenarios:

- To block lost or compromised boot media when you deploy an OS to clients
- When all site systems accept HTTPS client connections

When site systems accept HTTP client connections, don't rely on blocking to protect the Configuration Manager hierarchy from untrusted computers. In this scenario, a blocked client could rejoin the site with a new self-signed certificate and hardware ID.

Certificate revocation is the primary line of defense against potentially compromised certificates. A certificate revocation list (CRL) is only available from a supported public key infrastructure (PKI). Blocking clients in Configuration Manager offers a second line of defense to protect your hierarchy.

For more information, see [Determine whether to block clients](determine-whether-to-block-clients.md).

### Use the most secure client installation methods that are practical for your environment

- For domain computers, _group policy_ client installation and _software update-based_ client installation methods are more secure than _client push_ installation.

- If you apply access controls and change controls, use imaging and manual installation methods.

- Use Kerberos mutual authentication with client push installation.

Of all the client installation methods, client push installation is the least secure because of the many dependencies it has. These dependencies include local administrative permissions, the `Admin$` share, and firewall exceptions. The number and type of these dependencies increase your attack surface.

When using client push, the site can require Kerberos mutual authentication by not allowing fallback to NTLM before establishing the connection. This enhancement helps to secure the communication between the server and the client. For more information, see [How to install clients with client push](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!--1358204-->

For more information about the different client installation methods, see [Client installation methods](client-installation-methods.md).

Wherever possible, select a client installation method that requires the least security permissions in Configuration Manager. Restrict the administrative users that are assigned security roles with permissions that can be used for purposes other than client deployment. For example, configuring automatic client upgrade requires the **Full Administrator** security role, which grants an administrative user all security permissions.

For more information about the dependencies and security permissions required for each client installation method, see [Prerequisites for computer clients](../prerequisites-for-deploying-clients-to-windows-computers.md#installation-method-dependencies).

### If you must use client push installation, secure the client push installation account

The [client push installation account](../../../plan-design/hierarchy/accounts.md#client-push-installation-account) must be a member of the local **Administrators** group on each computer that installs the Configuration Manager client. Never add the client push installation account to the **Domain Admins** group. Instead, create a global group, and then add that global group to the local **Administrators** group on your clients. Create a group policy object to add a **Restricted Group** setting to add the client push installation account to the local **Administrators** group.

For greater security, create multiple client push installation accounts, each with administrative access to a limited number of computers. If one account is compromised, only the client computers to which that account has access are compromised.

### Remove certificates before imaging clients

When you deploy clients by using OS images, always remove certificates before capturing the image. These certificates include PKI certificates for client authentication, and self-signed certificates. If you don't remove these certificates, clients might impersonate each other. You can't verify the data for each client.

For more information, see [Create a task sequence to capture an OS](../../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).

### Make sure that Configuration Manager client gets an authorized copy of certificates

#### The Configuration Manager trusted root key certificate

When both of the following statements are true, clients rely on the Configuration Manager trusted root key to authenticate valid management points:

- You haven't extended the Active Directory schema for Configuration Manager
- Clients don't use PKI certificates when they communicate with management points

In this scenario, clients have no way to verify that the management point is trusted for the hierarchy unless they use the trusted root key. Without the trusted root key, a skilled attacker could direct clients to a rogue management point.

When clients don't use PKI certificates and can't download the trusted root key from the Active Directory global catalog, pre-provision the clients with the trusted root key. This action makes sure that they can't be directed to a rogue management point. For more information, see [Planning for the trusted root key](../../../plan-design/security/plan-for-security.md#the-trusted-root-key).

#### The site server signing certificate

Clients use the site server signing certificate to verify that the site server signed the policy downloaded from a management point. This certificate is self-signed by the site server and published to Active Directory Domain Services.

When clients can't download this certificate from the Active Directory global catalog, by default they download it from the management point. If the management point is exposed to an untrusted network like the internet, manually install the site server signing certificate on clients. This action makes sure that they can't download tampered client policies from a compromised management point.

To manually install the site server signing certificate, use the CCMSetup client.msi property [SMSSIGNCERT](../about-client-installation-properties.md#smssigncert).

### If the client downloads the trusted root key from the first management point it contacts, don't use automatic site assignment

To avoid the risk of a new client downloading the trusted root key from a rogue management point, only use automatic site assignment in the following scenarios:

- The client can access Configuration Manager site information that's published to Active Directory Domain Services.

- You pre-provision the client with the trusted root key.

- You use PKI certificates from an enterprise certification authority to establish trust between the client and the management point.

For more information about the trusted root key, see [Planning for the trusted root key](../../../plan-design/security/plan-for-security.md#the-trusted-root-key).

### Make sure that maintenance windows are large enough to deploy critical software updates

Maintenance windows for device collections restrict the times that Configuration Manager can install software on these devices. If you configure the maintenance window to be too small, the client may not install critical software updates. This behavior leaves the client vulnerable to any attack that the software update mitigates.

### Take security precautions to reduce the attack surface on Windows Embedded devices with write filters

When you enable write filters on Windows Embedded devices, any software installations or changes are only made to the overlay. These changes don't persist after the device restarts. If you use Configuration Manager to disable the write filters, during this period the embedded device is vulnerable to changes to all volumes. These volumes include shared folders.

Configuration Manager locks the computer during this period so that only local administrators can sign in. Whenever possible, take other security precautions to help protect the computer. For example, enable restrictions on the firewall.

If you use maintenance windows to persist changes, plan these windows carefully. Minimize the time that write filters are disabled, but make them long enough to allow software installations and restarts to complete.

### Use the latest client version with software update-based client installation

If you use software update-based client installation, and install a later version of the client on the site, update the published software update. Then clients receive the latest version from the software update point.

When you update the site, the software update for client deployment that's published to the software update point isn't automatically updated. Republish the Configuration Manager client to the software update point and update the version number.

For more information, see [How to install Configuration Manager clients by using software update-based installation](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).

### Only suspend BitLocker PIN entry on trusted and restricted-access devices

Only configure the client setting to **Suspend BitLocker PIN entry on restart** to **Always** for computers that you trust and that have restricted physical access.

When you set this client setting to **Always**, Configuration Manager can complete the installation of software. This behavior helps install critical software updates and resume services. If an attacker intercepts the restart process, they could take control of the computer. Use this setting only when you trust the computer, and when physical access to the computer is restricted. For example, this setting might be appropriate for servers in a data center.

For more information on this client setting, see [About client settings](../about-client-settings.md#suspend-bitlocker-pin-entry-on-restart).

### Don't bypass PowerShell execution policy

If you configure the Configuration Manager client setting for **PowerShell execution policy** to **Bypass**, then Windows allows unsigned PowerShell scripts to run. This behavior could allow malware to run on client computers. When your organization requires this option, use a custom client setting. Assign it to only the client computers that must run unsigned PowerShell scripts.

For more information on this client setting, see [About client settings](../about-client-settings.md#powershell-execution-policy).

## Security guidance for mobile devices

### Install the enrollment proxy point in a perimeter network and the enrollment point in the intranet

For internet-based mobile devices that you enroll with Configuration Manager, install the enrollment proxy point in a perimeter network and the enrollment point in the intranet. This role separation helps to protect the enrollment point from attack. If an attacker compromises the enrollment point, they could obtain certificates for authentication. They can also steal the credentials of users who enroll their mobile devices.

### Configure the password settings to help protect mobile devices from unauthorized access

*For mobile devices that are enrolled by Configuration Manager*: Use a mobile device configuration item to configure the password complexity as the PIN. Specify at least the default minimum password length.

*For mobile devices that don't have the Configuration Manager client installed but are managed by the Exchange Server connector*: Configure the **Password Settings** for the Exchange Server connector such that the password complexity is the PIN. Specify at least the default minimum password length.

### Only allow applications to run that are signed by companies that you trust

Help prevent tampering of inventory information and status information by allowing applications to run only when they're signed by companies that you trust. Don't allow devices to install unsigned files.

*For mobile devices that are enrolled by Configuration Manager*: Use a mobile device configuration item to configure the security setting **Unsigned applications** as **Prohibited**. Configure **Unsigned file installations** to be a trusted source.

*For mobile devices that don't have the Configuration Manager client installed but are managed by the Exchange Server connector*: Configure the **Application Settings** for the Exchange Server connector such that **Unsigned file installation** and **Unsigned applications** are **Prohibited**.

### Lock mobile devices when not in use

Help prevent elevation of privilege attacks by locking the mobile device when it isn't used.

*For mobile devices that are enrolled by Configuration Manager*: Use a mobile device configuration item to configure the password setting **Idle time in minutes before mobile device is locked**.

*For mobile devices that don't have the Configuration Manager client installed but are managed by the Exchange Server connector*: Configure the **Password Settings** for the Exchange Server connector to set the **Idle time in minutes before mobile device is locked**.

### Restrict the users who can enroll their mobile devices

Help prevent elevation of privileges by restricting the users who can enroll their mobile devices. Use a custom client setting rather than default client settings to allow only authorized users to enroll their mobile devices.

### User device affinity guidance for mobile devices

Don't deploy applications to users who have mobile devices enrolled by Configuration Manager in the following scenarios:

- The mobile device is used by more than one person.

- The device is enrolled by an administrator on behalf of a user.

- The device is transferred to another person without retiring and then re-enrolling the device.

Device enrollment creates a user device affinity relationship. This relationship maps the user who does enrollment to the mobile device. If another user uses the mobile device, they can run the applications deployed to the original user, which might result in an elevation of privileges. Similarly, if an administrator enrolls the mobile device for a user, applications deployed to the user aren't installed on the mobile device. Instead, applications deployed to the administrator might be installed.

### Protect the connection between the Configuration Manager site server and the Exchange Server

If the Exchange Server is on-premises, use IPsec. Hosted Exchange automatically secures the connection with HTTPS.

### Use the principle of least privileges for the Exchange connector

For a list of the minimum cmdlets that the Exchange Server connector requires, see [Manage mobile devices with Configuration Manager and Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

## Security guidance for macOS devices

### Store and access the client source files from a secured location

Before installing or enrolling the client on a macOS computer, Configuration Manager doesn't verify whether these client source files have been tampered with. Download these files from a trustworthy source. Securely store and access them.

### Monitor and track the validity period of the certificate

Monitor and track the validity period of the certificates that you use for macOS computers. Configuration Manager doesn't support automatic renewal of this certificate, or warn you that the certificate is about to expire. A typical validity period is one year.

For more information about how to renew the certificate, see [Renewing the macOS client certificate manually](../deploy-clients-to-macs.md#renew-the-mac-client-certificate).

### Configure the trusted root certificate for SSL only

To help protect against elevation of privileges, configure the certificate for the trusted root certificate authority so that it's only trusted for the SSL protocol.

When you enroll Mac computers, a user certificate to manage the Configuration Manager client is automatically installed. This user certificate includes the trusted root certificates in its trust chain. To restrict the trust of this root certificate to the SSL protocol only, use the following procedure:  

1. On the Mac computer, open a terminal window.  

2. Enter the following command: `sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3. In the **Keychain Access** dialog box, in the **Keychains** section, select **System**. Then in the **Category** section, select **Certificates**.  

4. Locate and open the root CA certificate for the Mac client certificate.  

5. In the dialog box for the root CA certificate, expand the **Trust** section, and then make the following changes:  

    1. **When using this certificate**: Change the **Always Trust** setting to **Use System Defaults**.  

    2. **Secure Sockets Layer (SSL)**: Change **no value specified** to **Always Trust**.  

6. Close the dialog box. When prompted, enter the administrator's password, and then select **Update Settings**.  

After you complete this procedure, the root certificate is only trusted to validate the SSL protocol. Other protocols that are now untrusted with this root certificate include Secure Mail (S/MIME), Extensible Authentication (EAP), or code signing.  

> [!NOTE]  
> Also use this procedure if you installed the client certificate independently from Configuration Manager.

## Security issues for clients

The following security issues have no mitigation:

### Status messages aren't authenticated

The management point doesn't authenticate status messages. When a management point accepts HTTP client connections, any device can send status messages to the management point. If the management point accepts HTTPS client connections only, a device must have a valid client authentication certificate, but could also send any status message. The management point discards any invalid status message received from a client.

There are a few potential attacks against this vulnerability:

- An attacker could send a bogus status message to gain membership in a collection that's based on status message queries.
- Any client could launch a denial of service against the management point by flooding it with status messages.
- If status messages are triggering actions in status message filter rules, an attacker could trigger the status message filter rule.
- An attacker could send status message that would render reporting information inaccurate.

### Policies can be retargeted to non-targeted clients

There are several methods that attackers could use to make a policy targeted to one client apply to an entirely different client. For example, an attacker at a trusted client could send false inventory or discovery information to have the computer added to a collection to which it shouldn't belong. That client then receives all the deployments to that collection.

Controls exist to help prevent attackers from directly modifying policy. However, attackers could take an existing policy that reformats and redeploys an OS and send it to a different computer. This redirected policy could create a denial of service. These types of attacks would require precise timing and extensive knowledge of the Configuration Manager infrastructure.

### Client logs allow user access

All the client log files allow the **Users** group with **Read** access, and the special **Interactive** user with access to write data. If you enable verbose logging, attackers might read the log files to look for information about compliance or system vulnerabilities. Processes such as software that the client installs in a user's context must write to logs with a low-rights user account. This behavior means an attacker could also write to the logs with a low-rights account.

The most serious risk is that an attacker could remove information in the log files. An administrator might need this information for auditing and intrusion detection.

### A computer could be used to obtain a certificate that's designed for mobile device enrollment

When Configuration Manager processes an enrollment request, it can't verify the request originated from a mobile device rather than from a computer. If the request is from a computer, it can install a PKI certificate that then allows it to register with Configuration Manager.

To help prevent an elevation of privilege attack in this scenario, only allow trusted users to enroll their mobile devices. Carefully monitor device enrollment activities in the site.

### A blocked client can still send messages to the management point

When you block a client that you no longer trust, but it established a network connection for client notification, Configuration Manager doesn't disconnect the session. The blocked client can continue to send packets to its management point until the client disconnects from the network. These packets are only small, keep-alive packets. This client can't be managed by Configuration Manager until it's unblocked.

### Automatic client upgrade doesn't verify the management point

When you use automatic client upgrade, the client can be directed to a management point to download the client source files. In this scenario, the client doesn't verify the management point as a trusted source.

### When users first enroll macOS computers, they're at risk from DNS spoofing

When the macOS computer connects to the enrollment proxy point during enrollment, it's unlikely that the macOS computer already has the trusted root CA certificate. At this point, the macOS computer doesn't trust the server, and prompts the user to continue. If a rogue DNS server resolves the fully qualified domain name (FQDN) of the enrollment proxy point, it could direct the macOS computer to a rogue enrollment proxy point to install certificates from an untrusted source. To help reduce this risk, follow DNS guidance to avoid spoofing in your environment.

### macOS enrollment doesn't limit certificate requests

Users can re-enroll their macOS computers, each time requesting a new client certificate. Configuration Manager doesn't check for multiple requests or limit the number of certificates requested from a single computer. A rogue user could run a script that repeats the command-line enrollment request. This attack could cause a denial of service on the network or on the issuing certificate authority (CA). To help reduce this risk, carefully monitor the issuing CA for this type of suspicious behavior. Immediately block from the Configuration Manager hierarchy any computer that shows this pattern of behavior.

### A wipe acknowledgment doesn't verify that the device has been successfully wiped

When you start a wipe action for a mobile device, and Configuration Manager acknowledges the wipe, the verification is that Configuration Manager successfully *sent* the message. It doesn't verify that the device *acted* on the request.

For mobile devices managed by the Exchange Server connector, a wipe acknowledgment verifies that the command was received by Exchange, not by the device.

### If you use the options to commit changes on Windows Embedded devices, accounts might be locked out sooner than expected

If the Windows Embedded device is running an OS version earlier than Windows 7, and a user attempts to sign in while the write filters are disabled by Configuration Manager, Windows allows only half of the configured number of incorrect attempts before the account is locked out.

For example, you configure the domain policy for **Account lockout threshold** to six attempts. A user mistypes their password three times, and the account is locked out. This behavior effectively creates a denial of service. If users must sign in to embedded devices in this scenario, caution them about the potential for a reduced lockout threshold.

## Privacy information for clients

When you deploy the Configuration Manager client, you enable [client settings](../configure-client-settings.md) for Configuration Manager features. The settings that you use to configure the features can apply to all clients in the Configuration Manager hierarchy. This behavior is the same whether they're directly connected to the internal network, connected through a remote session, or connected to the internet.

Client information is stored in the Configuration Manager site database in your SQL Server, and isn't sent to Microsoft. Information is kept in the database until it's deleted by the site maintenance task [Delete Aged Discovery Data](../../../servers/manage/reference-for-maintenance-tasks.md#delete-aged-discovery-data) every 90 days. You can configure the deletion interval.

Some summarized or aggregate diagnostics and usage data is sent to Microsoft. For more information, see [Diagnostics and usage data](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).

You can learn more about Microsoft's data collection and use in the [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement).

### Client status

Configuration Manager monitors the activity of clients. It periodically evaluates the Configuration Manager client and can remediate issues with the client and its dependencies. Client status is enabled by default. It uses server-side metrics for the client activity checks. Client status uses client-side actions for self-checks, remediation, and for sending client status information to the site. The client runs the self-checks according to a schedule that you configure. The client sends the results of the checks to the Configuration Manager site. This information is encrypted during transfer.

Client status information is stored in the Configuration Manager database in your SQL Server, and isn't sent to Microsoft. The information isn't stored in encrypted format in the site database. This information is kept in the database until it's deleted according to the value configured for the **Retain client status history for the following number of days** client status setting. The default value for this setting is every 31 days.

## Privacy information for the Exchange Server Connector

The Exchange Server Connector finds and manages devices that connect to an on-premises or hosted Exchange Server by using the ActiveSync protocol. The records found by the Exchange Server Connector are stored in the Configuration Manager database in your SQL Server. The information is collected from the Exchange Server. It doesn't contain any additional information from what the mobile devices send to Exchange Server.

The mobile device information isn't sent to Microsoft. The mobile device information is stored in the Configuration Manager database in your SQL Server. Information is kept in the database until it's deleted by the site maintenance task [Delete Aged Discovery Data](../../../servers/manage/reference-for-maintenance-tasks.md#delete-aged-discovery-data) every 90 days. You configure the deletion interval.

You can learn more about Microsoft's data collection and use in the [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement).
