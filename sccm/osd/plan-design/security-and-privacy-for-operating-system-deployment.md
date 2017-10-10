---
title: Security and privacy for operating system deployment
description: "Learn about security and privacy best practices for operating system deployment in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
caps.latest.revision: 6
caps.handback.revision: 0
author: Dougebyms.author: dougebymanager: angrobe

---
# Security and privacy for operating system deployment in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
This topic contains security and privacy information for operating system deployment in System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Security best practices for operating system deployment  
 Use the following security best practices for when you deploy operating systems with Configuration Manager:  

-   **Implement access controls to protect bootable media**  

     When you create bootable media, always assign a password to help secure the media. However, even with a password, only files that contain sensitive information are encrypted and all files can be overwritten.  

     Control physical access to the media to prevent an attacker from using cryptographic attacks to obtain the client authentication certificate.  

     To help prevent a client from installing content or client policy that has been tampered with, the content is hashed and must be used with the original policy.  If the content hash fails or the check that the content matches the policy, the client will not use the bootable media. Only the content is hashed; the policy is not but it is encrypted and secured when you specify a password, which makes it more difficult for an attacker to successfully modify the policy.  

-   **Use a secured location when you create media for operating system images**  

     If unauthorized users have access to the location, they can tamper with the files that you create and also use all the available disk space so that the media creation fails.  

-   **Protect certificate files (.pfx) with a strong password and if you store them on the network, secure the network channel when you import them into Configuration Manager**  

     When you require a password to import the client authentication certificate that you use for bootable media, this helps to protect the certificate from an attacker.  

     Use SMB signing or IPsec between the network location and the site server to prevent an attacker from tampering with the certificate file.  

-   **If the client certificate is compromised, block the certificate from Configuration Manager and revoke it if it is a PKI certificate**  

     To deploy an operating system by using bootable media and PXE boot, you must have a client authentication certificate with a private key. If that certificate is compromised, block the certificate in the **Certificates** node in the **Administration** workspace, **Security** node.  

-   **When the SMS Provider is on a computer or computers other than the site server, secure the communication channel to protect boot images**  

     When boot images are modified and the SMS Provider is running on a server that is not the site server, the boot images are vulnerable to attack. Protect the network channel between these computers by using SMB signing or IPsec.  

-   **Enable distribution points for PXE client communication only on secure network segments**  

     When a client sends a PXE boot request, you have no way to ensure that the request is serviced by a valid PXE-enabled distribution point. This scenario has the following security risks:  

    -   A rogue distribution point that responds to PXE requests could provide a tampered image to clients.  

    -   An attacker could launch a man-in-the-middle attack against the TFTP protocol that is used by PXE and send malicious code with the operating system files, or she could create a rogue client to make TFTP requests directly to the distribution point.  

    -   An attacker could use a malicious client to launch a denial of service attack against the distribution point.  

     Use defense in depth to protect the network segments where clients will access distribution points for PXE requests.  

    > [!WARNING]  
    >  Because of these security risks, do not enable a distribution point for PXE communication when it is in an untrusted network, such as a perimeter network.  

-   **Configure PXE-enabled distribution points to respond to PXE requests only on specified network interfaces**  

     If you allow the distribution point to respond to PXE requests on all network interfaces, this configuration might expose the PXE service to untrusted networks  

-   **Require a password to PXE boot**  

     When you require a password for PXE boot, this configuration adds an extra level of security to the PXE boot process, to help safeguard against rogue clients joining the Configuration Manager hierarchy.  

-   **Do not include line of business applications or software that contains sensitive data into an image that will be used for PXE boot or multicast**  

     Because of the inherent security risks involved with PXE boot and multicast, reduce the risks if rogue computer downloads the operating system image.  

-   **Do not include line of business applications or software that contains sensitive data in software packages that are installed by using task sequences variables**  

     When you deploy software packages by using task sequences variables, software might be installed on computers and to users who are not authorized to receive that software.  

-   **When you migrate user state, secure the network channel between the client and the state migration point by using SMB signing or IPsec**  

     After the initial connection over HTTP, user state migration data is transferred by using SMB.  If you do not secure the network channel, an attacker can read and modify this data.  

-   **Use the latest version of the User State Migration Tool (USMT) that Configuration Manager supports**  

     The latest version of USMT provides security enhancements and greater control for when you migrate user state data.  

-   **Manually delete folders on state migration point when they are decommissioned**  

     When you remove a state migration point folder in the Configuration Manager console on the state migration point properties, the physical folder is not deleted. To protect the user state migration data from information disclosure, you must manually remove the network share and delete the folder.  

-   **Do not configure the deletion policy to delete user state immediately**  

     If you configure the deletion policy on the state migration point to remove data that is marked for deletion immediately, and if an attacker manages to retrieve the user state data before the valid computer does, the user state data would be deleted immediately. Set the **Delete after** interval to be long enough to verify the successful restore of user state data.  

-   **Manually delete computer associations when the user state migration data restore is complete and verified**  

     Configuration Manager does not automatically remove computer associations. Help to protect the identify of user state data by manually deleting computer associations that are no longer required.  

-   **Manually back up the user state migration data on the state migration point**  

     Configuration Manager Backup does not include the user state migration data.  

-   **Remember to enable BitLocker after the operating system is installed**  

     If a computer supports BitLocker, you must disable it by using a task sequence step if you want to install the operating system unattended. Configuration Manager does not enable BitLocker after the operating system is installed, so you must manually re-enable BitLocker.  

-   **Implement access controls to protect the prestaged media**  

     Control physical access to the media to prevent an attacker from using cryptographic attacks to obtain the client authentication certificate and sensitive data.  

-   **Implement access controls to protect the reference computer imaging process**  

     Ensure that the reference computer that you use to capture operating system images is in a secure environment with appropriate access controls so that unexpected or malicious software cannot be installed and inadvertently included in the captured image. When you capture the image, ensure that the destination network file share location is secure so that the image cannot be tampered with after it is captured.  

-   **Always install the most recent security updates on the reference computer**  

     When the reference computer has current security updates, it helps to reduce the window of vulnerability for new computers when they first start up.  

-   **If you must deploy operating systems to an unknown computer, implement access controls to prevent unauthorized computers from connecting to the network**  

     Although provisioning unknown computers provides a convenient method to deploy new computers on demand, it can also allow an attacker to efficiently become a trusted client on your network. Restrict physical access to the network, and monitor clients to detect unauthorized computers. Also, computers responding to PXE-initiated operating system deployment might have all data destroyed during the operating system deployment, which could result in a loss of availability of systems that are inadvertently reformatted.  

-   **Enable encryption for multicast packages**  

     For every operating system deployment package, you have the option to enable encryption when Configuration Manager transfers the package by using multicast. This configuration helps prevent rogue computers from joining the multicast session and helps prevent attackers from tampering with the transmission.  

-   **Monitor for unauthorized multicast-enabled distribution points**  

     If attackers can gain access to your network, they can configure rogue multicast servers to spoof operating system deployment.  

-   **When you export task sequences to a network location, secure the location and secure the network channel**  

     Restrict who can access the network folder.  

     Use SMB signing or IPsec between the network location and the site server to prevent an attacker from tampering with the exported task sequence.  

-   **Secure the communication channel when you upload a virtual hard disk to Virtual Machine Manager.**  

     To prevent tampering of the data when it is transferred over the network, use Internet Protocol security (IPsec) or server message block (SMB) between the computer that runs the Configuration Manager console and the computer running Virtual Machine Manager.  

-   **If you must use the Task Sequence Run As Account, take additional security precautions**  

     Take the following precautionary steps if you use the Task Sequence Run As Account:  

    -   Use an account with the least possible permissions.  

    -   Do not use the Network Access account for this account.  

    -   Never make the account a domain administrator.  

     In addition:  

    -   Never configure roaming profiles for this account. When the task sequence runs, it will download the roaming profile for the account, which leaves the profile vulnerable to access on the local computer.  

    -   Limit the scope of the account. For example, create different Task Sequence Run As Accounts for each task sequence, so that if one account is compromised, only the client computers to which that account has access are compromised. If the command line requires administrative access on the computer, consider creating a local administrator account solely for the Task Sequence Run As Account on all computers that will run the task sequence, and delete the account as soon as it is no longer required.  

-   **Restrict and monitor the administrative users who are granted the Operating System Deployment Manager security role**  

     Administrative users who are granted the Operating System Deployment Manager security role can create self-signed certificates that can then be used to impersonate a client and obtain client policy from Configuration Manager.  

### Security issues for operating system deployment  
 Although operating system deployment can be a convenient way to deploy the most secure operating systems and configurations for computers on your network, it does have the following security risks:  

-   Information disclosure and denial of service  

     If an attacker can obtain control of your Configuration Manager infrastructure, she could run any task sequences, which might include formatting the hard drives of all client computers. Task sequences can be configured to contain sensitive information, such as accounts that have permissions to join the domain and volume licensing keys.  

-   Impersonation and elevation of privileges  

     Task sequences can join a computer to domain, which can provide a rogue computer with authenticated network access. Another important security consideration for operating system deployment is to protect the client authentication certificate that is used for bootable task sequence media and for PXE boot deployment. When you capture a client authentication certificate, this gives an attacker an opportunity to obtain the private key in the certificate and then impersonate a valid client on the network.  

     If an attacker obtains the client certificate that is used for bootable task sequence media and for PXE boot deployment, this certificate can be used to impersonate a valid client to Configuration Manager. In this scenario, the rogue computer can download policy, which can contain sensitive data.  

     If clients use the Network Access Account to access data stored on the state migration point, these clients effectively share the same identity and could access state migration data from another client that uses the Network Access Account. The data is encrypted so only the original client can read it, but the data could be tampered with or deleted.  

-   Client authentication to the state migration point is achieved by using a Configuration Manager token that is issued by the management point.  

     In addition, Configuration Manager does not limit or manage the amount of data that is stored on the state migration point and an attacker could fill up the available disk space and cause a denial of service.  

-   If you use collection variables, local administrators can read potentially sensitive information  

     Although collection variables offer a flexible method to deploy operating systems, this might result in information disclosure.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Privacy information for operating system deployment  
 In addition to deploying operating systems to computers with no operating system, Configuration Manager can be used to migrate users' files and settings from one computer to another. The administrator configures which information to transfer, including personal data files, configuration settings, and browser cookies.  

 The information is stored on a state migration point and is encrypted during transmission and storage. The information is allowed to be retrieved by the new computer associated with the state information. If the new computer loses the key to retrieve the information, a Configuration Manager administrator with the View Recovery Information right on computer association instance objects can access the information and associate it with a new computer. After the new computer restores the state information, it deletes the data after one day by default. You can configure when the state migration point removes data marked for deletion. The state migration information is not stored in the site database and is not sent to Microsoft.  

 If you use boot media to deploy operating system images, always use the default option to password-protect the boot media. The password encrypts any variables stored in the task sequence, but any information not stored in a variable might be vulnerable to disclosure.  

 Operating system deployment can use task sequences to perform many different tasks during the deployment process, which includes installing applications and software updates. When you configure task sequences, you should also be aware of the privacy implications of installing software.  

 If you upload a virtual hard disk to Virtual Machine Manager without first using Sysprep to clean the image, the uploaded virtual hard disk could contain personal data from the original image.  

 Configuration Manager does not implement operating system deployment by default and requires several configuration steps before you collect user state information or create task sequences or boot images.  

 Before you configure operating system deployment, consider your privacy requirements.  
