---
title: "Introduction to certificate profiles | System Center Configuration Manager"
description: "Learn how certificate profiles in System Center Configuration Manager work with Active Directory Certificate Services."
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: 7
author: Nbigmanms.author: nbigmanmanager: angrobe

---
# Introduction to certificate profiles in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*

Certificate profiles in System Center Configuration Manager works with Active Directory Certificate Services and the Network Device Enrollment Service role to provision authentication certificates for managed devices so that users can seamlessly access company resources. For example, you can create and deploy certificate profiles to provide the necessary certificates for users to initiate VPN and wireless connections.  

 Certificate profiles in System Center Configuration Manager provide the following management capabilities:  

-   Certificate enrollment and renewal from an enterprise certification authority (CA) for devices that run iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop and Mobile, and Android, These certificates can then be used for Wi-Fi and VPN connections.  

-   Deployment of trusted root CA certificates and intermediate CA certificates to configure a chain of trust on devices for VPN and Wi-Fi connections when server authentication is required.  

-   Monitor and report about the installed certificates.  

 Certificate profiles can automatically configure user devices so that company resources such as Wi-Fi networks and VPN servers can be accessed without having to install certificates manually or use an out of band process. Certificate profiles can also help to keep company resources secure because you can use more secure settings that are supported by your enterprise public key infrastructure (PKI). For example, you can require server authentication for all Wi-Fi and VPN connections because you have provisioned the required certificates on the managed devices.  

 **Example:** All employees must be able to connect to Wi-Fi hotspots in multiple corporate locations. To accomplish this, you can deploy the certificates required to make the Wi-Fi connection and also deploy Wi-Fi profiles in System Center Configuration Manager that reference the correct certificate to use so that the Wi-Fi connection happens seamlessly for users.  

 **Example:** You have a PKI in place and want to move to a more flexible, secure method of provisioning certificates that lets users access company resources from their personal devices without compromising security. To accomplish this, you can configure certificate profiles with settings and protocols that are supported for the specific device platform. The devices can then automatically request these certificates from an Internet-facing enrollment server. You can then configure VPN profiles to use these certificates so that the device can access company resources.  

## Types of Certificate Profile  
 You can create three types of certificate profiles in System Center Configuration Manager:  

-   **Trusted CA certificate** - Allows you to deploy a trusted root CA or intermediate CA certificate to form a certificate chain of trust when the device must authenticate a server.  

-   **Simple Certificate Enrollment Protocol (SCEP)** - Allows you to request a certificate for a device or user, by using the SCEP protocol and the Network Device Enrollment Service on a server running Windows Server 2012 R2.
-   -   **Personal information exchange (.pfx)** - Allows you to request a certificate for a device or user, by using the SCEP protocol and the Network Device Enrollment Service on a server running Windows Server 2012 R2.

    > [!NOTE]  
    >  You must create a certificate profile of the type **Trusted CA certificate** before you can create a certificate profile of the type **Simple Certificate Enrollment Protocol (SCEP) settings**.  

## Requirements and Supported Platforms  
 To deploy certificate profiles that use the Simple Certificate Enrollment Protocol, you must install the certificate registration point on a site system server in the central administration site, or in a primary site. You must also install a policy module for the Network Device Enrollment Service, the Configuration Manager Policy Module, on a server that runs Windows Server 2012 R2 with the Active Directory Certificate Services role and a working Network Device Enrollment Service that is accessible to the devices that require the certificates. For the devices that are enrolled by Microsoft Intune, this requires the Network Device Enrollment Service to be accessible from the Internet, for example, in a screened subnet (also known as a DMZ).  

 For more information about how the Network Device Enrollment Service supports a policy module so that System Center Configuration Manager can deploy certificates, see [Using a Policy Module with the Network Device Enrollment Service](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

 System Center Configuration Manager supports deploying certificates to different certificate stores, depending on the requirement, and also on the device type and operating system. The following devices and operating systems are supported:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop and Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  To deploy profiles to Android, iOS, Windows Phone, and enrolled Windows 8.1 or later devices, these devices must be enrolled into Microsoft Intune. For information about how to get your devices enrolled, see [Manage mobile devices with Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 A typical scenario for System Center Configuration Manager is to install trusted root CA certificates to authenticate Wi-Fi and VPN servers when the connection uses EAP-TLS, EAP-TTLS, and PEAP authentication protocols, and IKEv2, L2TP/IPsec, and Cisco IPsec VPN tunneling protocols.  

 You must ensure that an enterprise root CA certificate is installed on the device before the device can request certificates by using a SCEP certificate profile.  

 You can specify a variety of settings in a SCEP certificate profile to request customized certificates for different environments or connectivity requirements. The **Create Certificate Profile Wizard** contains two pages for enrollment parameters. The first, **SCEP Enrollment**, contains settings for the enrollment request and where to install the certificate. The second, **Certificate Properties**, describes the requested certificate itself.  

## Deploying Certificate Profiles  
 When you deploy a certificate profile, the certificate files within the profile are installed on client devices. Any SCEP parameters will also be deployed, and the SCEP requests will be processed on the client device. You can deploy certificate profiles to user collections or device collections and specify the destination store for each certificate. Applicability rules determine whether the certificates can be installed on the device. When certificate profiles are deployed to user collections, user device affinity determines which of the usersâ€™ devices will install the certificates. When certificate profiles that contain user certificates are deployed to device collections, by default, the certificates will be installed on each of the usersâ€™ primary devices. You can modify this behavior to install the certificate on any of the usersâ€™ devices on the **SCEP Enrollment** page of the **Create Certificate Profile Wizard**. In addition, user certificates will not be deployed to devices if they are workgroup computers.  

## Monitoring Certificate Profiles  
 You can monitor certificate profile deployments from the **Deployments** node of the **Monitoring** workspace in the System Center Configuration Manager console.  

 You can also use one of the following System Center Configuration Manager reports to monitor certificate profiles:  

-   **History of certificates that are issued by the certificate registration point**  

-   **List of assets by certificate issuance state for certificates enrolled by the certificate registration point**  

-   **List of assets with certificates that are close to the expiry date**  

## Automatic Revocation of Certificates  
 System Center Configuration Manager automatically revokes user and computer certificates that were deployed by using certificate profiles in the following circumstances:  

-   The device is retired from System Center Configuration Manager management.  

-   The device is selectively wiped.  

-   The device is blocked from the System Center Configuration Manager hierarchy.  

 To revoke the certificates, the site server sends a revocation command to the issuing certification authority. The reason for the revocation is **Cease of Operation**.  
