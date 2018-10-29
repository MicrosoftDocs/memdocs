---
title: Security and privacy for OS deployment
titleSuffix: Configuration Manager
description: Learn about security and privacy best practices for OS deployment in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Security and privacy for OS deployment in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article contains security and privacy information for the OS deployment feature in Configuration Manager.  



##  <a name="bkmk_security"></a> Security best practices for OS deployment  

 Use the following security best practices for when you deploy operating systems with Configuration Manager:  


### Implement access controls to protect bootable media

 When you create bootable media, always assign a password to help secure the media. Even with a password, it only encrypts files that contain sensitive information, and all files can be overwritten.  

 Control physical access to the media to prevent an attacker from using cryptographic attacks to obtain the client authentication certificate.  

 To help prevent a client from installing content or client policy that has been tampered with, the content is hashed and must be used with the original policy. If the content hash fails or the check that the content matches the policy, the client won't use the bootable media. Only the content is hashed. The policy isn't hashed, but it's encrypted and secured when you specify a password. This behavior makes it more difficult for an attacker to successfully modify the policy.  


### Use a secure location when you create media for OS images

 If unauthorized users have access to the location, they can tamper with the files that you create. They can also use all the available disk space so that the media creation fails.  


### Protect certificate files 

 Protect certificate files (.pfx) with a strong password. If you store them on the network, secure the network channel when you import them into Configuration Manager

 When you require a password to import the client authentication certificate that you use for bootable media, this configuration helps to protect the certificate from an attacker.  

 Use SMB signing or IPsec between the network location and the site server to prevent an attacker from tampering with the certificate file.  


### Block or revoke any compromised certificates 

 If the client certificate is compromised, block the certificate from Configuration Manager. If it's a PKI certificate, revoke it.  

 To deploy an OS by using bootable media and PXE boot, you must have a client authentication certificate with a private key. If that certificate is compromised, block the certificate in the **Certificates** node in the **Administration** workspace, **Security** node.  


### Secure the communication channel between the site server and the SMS Provider

 When the SMS Provider is remote from the site server, secure the communication channel to protect boot images.

 When you modify boot images and the SMS Provider is running on a server that isn't the site server, the boot images are vulnerable to attack. Protect the network channel between these computers by using SMB signing or IPsec.  


### Enable distribution points for PXE client communication only on secure network segments

 When a client sends a PXE boot request, you have no way to make sure that the request is serviced by a valid PXE-enabled distribution point. This scenario has the following security risks:  

 - A rogue distribution point that responds to PXE requests could provide a tampered image to clients.  

 - An attacker could launch a man-in-the-middle attack against the TFTP protocol that is used by PXE. This attack could send malicious code with the OS files. The attacker could also create a rogue client to make TFTP requests directly to the distribution point.  

 - An attacker could use a malicious client to launch a denial of service attack against the distribution point.  

 Use defense in depth to protect the network segments where clients access PXE-enabled distribution points.  

 > [!WARNING]  
 >  Because of these security risks, don't enable a distribution point for PXE communication when it's in an untrusted network, such as a perimeter network.  


### Configure PXE-enabled distribution points to respond to PXE requests only on specified network interfaces  

 If you allow the distribution point to respond to PXE requests on all network interfaces, this configuration might expose the PXE service to untrusted networks  


### Require a password to PXE boot

 When you require a password for PXE boot, this configuration adds an extra level of security to the PXE boot process. This configuration helps safeguard against rogue clients joining the Configuration Manager hierarchy.  


### Restrict content in OS images used for PXE boot or multicast

 Don't include line-of-business applications or software that contains sensitive data in an image that you use for PXE boot or multicast.  

 Because of the inherent security risks involved with PXE boot and multicast, reduce the risks if a rogue computer downloads the OS image.  


### Restrict content installed by task sequence variables

 Don't include line-of-business applications or software that contains sensitive data in packages of applications that you install by using task sequences variables.  

 When you deploy software by using task sequences variables, it might be installed on computers and to users who aren't authorized to receive that software.  


### Secure the network channel when migrating user state

 When you migrate user state, secure the network channel between the client and the state migration point by using SMB signing or IPsec.  

 After the initial connection over HTTP, user state migration data is transferred by using SMB. If you don't secure the network channel, an attacker can read and modify this data.  


### Use the latest version of USMT

 Use the latest version of the User State Migration Tool (USMT) that Configuration Manager supports.  

 The latest version of USMT provides security enhancements and greater control for when you migrate user state data.  


### Manually delete folders on state migration points when you decommission them  

 When you remove a state migration point folder in the Configuration Manager console on the state migration point properties, the site doesn't delete the physical folder. To protect the user state migration data from information disclosure, manually remove the network share and delete the folder.  


### Don't configure the deletion policy to immediately delete user state  

 If you configure the deletion policy on the state migration point to immediately remove data that's marked for deletion, and if an attacker manages to retrieve the user state data before the valid computer does, the site immediately deletes the user state data. Set the **Delete after** interval to be long enough to verify the successful restore of user state data.  


### Manually delete computer associations 

 Manually delete computer associations when the user state migration data restore is complete and verified.

 Configuration Manager doesn't automatically remove computer associations. Help to protect the identity of user state data by manually deleting computer associations that are no longer required.  


### Manually back up the user state migration data on the state migration point  

 Configuration Manager Backup doesn't include the user state migration data in the site backup.  


### Implement access controls to protect the prestaged media  

 Control physical access to the media to prevent an attacker from using cryptographic attacks to obtain the client authentication certificate and sensitive data.  


### Implement access controls to protect the reference computer imaging process  

 Make sure the reference computer you use to capture OS images is in a secure environment. Use appropriate access controls so that unexpected or malicious software can't be installed and inadvertently included in the captured image. When you capture the image, make sure the destination network location is secure. This process helps make sure the image can't be tampered with after you capture it.  


### Always install the most recent security updates on the reference computer  

 When the reference computer has current security updates, it helps to reduce the window of vulnerability for new computers when they first start up.  


### Implement access controls when deploying an OS to an unknown computer

 If you must deploy an OS to an unknown computer, implement access controls to prevent unauthorized computers from connecting to the network.  

 Provisioning unknown computers provides a convenient method to deploy new computers on demand. But it can also allow an attacker to efficiently become a trusted client on your network. Restrict physical access to the network, and monitor clients to detect unauthorized computers. 

 Computers responding to a PXE-initiated OS deployment might have all data destroyed during the process. This behavior could result in a loss of availability of systems that are inadvertently reformatted.  


### Enable encryption for multicast packages  

 For every OS deployment package, you can enable encryption when Configuration Manager transfers the package by using multicast. This configuration helps prevent rogue computers from joining the multicast session. It also helps prevent attackers from tampering with the transmission.  


### Monitor for unauthorized multicast-enabled distribution points  

 If attackers can gain access to your network, they can configure rogue multicast servers to spoof OS deployment.  


### When you export task sequences to a network location, secure the location and secure the network channel

 Restrict who can access the network folder.  

 Use SMB signing or IPsec between the network location and the site server to prevent an attacker from tampering with the exported task sequence.  


### If you use the task sequence run as account, take additional security precautions

 If you use the [task sequence run as account](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account), take the following precautionary steps:  

 - Use an account with the least possible permissions.  

 - Don't use the network access account for this account.  

 - Never make the account a domain administrator.  

 - Never configure roaming profiles for this account. When the task sequence runs, it downloads the roaming profile for the account, which leaves the profile vulnerable to access on the local computer.  

 - Limit the scope of the account. For example, create different task sequence run as accounts for each task sequence. If one account is compromised, only the client computers to which that account has access are compromised. If the command line requires administrative access on the computer, consider creating a local administrator account solely for the task sequence run as account. Create this local account on all computers that run the task sequence, and delete the account as soon as it's no longer required.  


### Restrict and monitor the administrative users who are granted the OS deployment manager security role

 Administrative users who are granted the **OS deployment manager** security role can create self-signed certificates. These certificates can then be used to impersonate a client and obtain client policy from Configuration Manager.  


### Use Enhanced HTTP to reduce the need for a network access account

Starting in version 1806, when you enable [Enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http), several OS deployment scenarios don't require a network access account to download content from a distribution point. For more information, see [Task sequences and the network access account](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSNetworkAccessAccount).<!--1358278--> 



## Security issues for OS deployment  

 Although OS deployment can be a convenient way to deploy the most secure operating systems and configurations for computers on your network, it does have the following security risks:  


### Information disclosure and denial of service  

 If an attacker can obtain control of your Configuration Manager infrastructure, they could run any task sequences. This process might include formatting the hard drives of all client computers. Task sequences can be configured to contain sensitive information, such as accounts that have permissions to join the domain and volume licensing keys.  


### Impersonation and elevation of privileges  

 Task sequences can join a computer to domain, which can provide a rogue computer with authenticated network access. 

 Protect the client authentication certificate that's used for bootable task sequence media and for PXE boot deployment. When you capture a client authentication certificate, this process gives an attacker an opportunity to obtain the private key in the certificate. This certificate lets them impersonate a valid client on the network. In this scenario, the rogue computer can download policy, which can contain sensitive data.  

 If clients use the network access account to access data stored on the state migration point, these clients effectively share the same identity. They could access state migration data from another client that uses the network access account. The data is encrypted so only the original client can read it, but the data could be tampered with or deleted.  


### Client authentication to the state migration point is achieved by using a Configuration Manager token that is issued by the management point.  

 Configuration Manager doesn't limit or manage the amount of data that's stored on the state migration point. An attacker could fill up the available disk space and cause a denial of service.  


### If you use collection variables, local administrators can read potentially sensitive information  

 Although collection variables offer a flexible method to deploy operating systems, this feature might result in information disclosure.  



##  <a name="bkmk_privacy"></a> Privacy information for OS deployment  

 In addition to deploying an OS to computers without one, Configuration Manager can be used to migrate users' files and settings from one computer to another. The administrator configures which information to transfer, including personal data files, configuration settings, and browser cookies.  

 Configuration Manager stores the information on a state migration point, and encrypts it during transmission and storage. Only the new computer associated with the state information can retrieve the stored information. If the new computer loses the key to retrieve the information, a Configuration Manager administrator with the **View Recovery Information** right on computer association instance objects can access the information and associate it with a new computer. After the new computer restores the state information, it deletes the data after one day, by default. You can configure when the state migration point removes data marked for deletion. Configuration Manager doesn't store the state migration information in the site database, and doesn't send it to Microsoft.  

 If you use boot media to deploy OS images, always use the default option to password-protect the boot media. The password encrypts any variables stored in the task sequence, but any information not stored in a variable might be vulnerable to disclosure.  

 OS deployment can use task sequences to perform many different tasks during the deployment process, which includes installing applications and software updates. When you configure task sequences, you should also be aware of the privacy implications of installing software.  

 Configuration Manager doesn't implement OS deployment by default. It requires several configuration steps before you collect user state information or create task sequences or boot images.  

 Before you configure OS deployment, consider your privacy requirements.  



## See also

[Diagnostics and usage data](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)

[Security and privacy for Configuration Manager](/sccm/core/plan-design/security/security-and-privacy)