---
title: "Introduction to certificate profiles | Microsoft Docs"
description: "Learn how certificate profiles in System Center Configuration Manager work with Active Directory Certificate Services."
ms.custom: na
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: 7
author: lleonard-msft
ms.author: alleonar
manager: angrobe

---

# Introduction to certificate profiles in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


Certificate profiles work with Active Directory Certificate Services and the Network Device Enrollment Service role to provision authentication certificates for managed devices so that users can seamlessly access company resources. For example, you can create and deploy certificate profiles to provide the necessary certificates for users to initiate VPN and wireless connections.

Certificate profiles can automatically configure user devices so that company resources such as Wi-Fi networks and VPN servers can be accessed without having to install certificates manually or use an out of band process. Certificate profiles can also help to keep company resources secure because you can use more secure settings that are supported by your enterprise public key infrastructure (PKI). For example, you can require server authentication for all Wi-Fi and VPN connections because you have provisioned the required certificates on the managed devices.   

Certificate profiles provide the following management capabilities:  

-   Certificate enrollment and renewal from an enterprise certification authority (CA) for devices that run iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop and Mobile, and Android. These certificates can then be used for Wi-Fi and VPN connections.  

-   Deployment of trusted root CA certificates and intermediate CA certificates to configure a chain of trust on devices for VPN and Wi-Fi connections when server authentication is required.  

-   Monitor and report about the installed certificates.  

**Example:** All employees must be able to connect to Wi-Fi hotspots in multiple corporate locations. Deploy the certificates needed to connect to Wi-Fi, and deploy Wi-Fi profiles that reference the certificate to enable seamless user connection.  

**Example:** You have a PKI in place and want to move to a more flexible, secure method of provisioning certificates that lets users access company resources from their personal devices without compromising security. Configure certificate profiles with settings and protocols that are supported for the specific device platform. The devices can then automatically request these certificates from an Internet-facing enrollment server. Then, configure VPN profiles to use these certificates so that the device can access company resources.  

## Types of certificate profiles  
 There are three types of certificate profiles:  

-   **Trusted CA certificate** - Lets you deploy a trusted root CA or intermediate CA certificate to form a certificate chain of trust when the device must authenticate a server.  

-   **Simple Certificate Enrollment Protocol (SCEP)** - Lets you request a certificate for a device or user by using the SCEP protocol and the Network Device Enrollment Service on a server running Windows Server 2012 R2.

    To create a **Simple Certificate Enrollment Protocol (SCEP)** certificate profile, first create a **Trusted CA certificate** certificate profile.

-   **Personal information exchange (.pfx)** - Lets you request a .pfx (also known as PKCS #12) certificate for a device or user.

    You may create PFX certificate profiles by ether [importing credentials](/sccm/mdm/deploy-use/import-pfx-certificate-profiles) from existing certificates or by [defining a certificate](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) authority to process requests.

    Starting with release 1706, you can use Microsoft or Entrust as certificate authorities for **Personal information exchange (.pfx)** certificates.


## Requirements and supported platforms  
To deploy certificate profiles that use SCEP, you must install the certificate registration point on a site system server in the central administration site, or in a primary site. You must also install a policy module for NDES, the Configuration Manager Policy Module, on a server that runs Windows Server 2012 R2 with the Active Directory Certificate Services role and a working NDES that is accessible to the devices that require the certificates. For the devices that are enrolled by Microsoft Intune, this requires the NDES to be accessible from the Internet, for example, in a screened subnet (also known as a DMZ).  

PFX certificates also require a certificate registration point on a site system server in the central administration site or in a primary site.  You must also specify the Certificate authority (CA) for the certificate and specify relevant access credentials.  Starting with version 1706, you may specify either Microsoft or Entrust as certificate authorities.  

For more information about how the Network Device Enrollment Service supports a policy module so that Configuration Manager can deploy certificates, see [Using a Policy Module with the Network Device Enrollment Service](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

Configuration Manager supports deploying certificates to different certificate stores, depending on the requirements, the device type, and the operating system. The following devices and operating systems are supported:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop and Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  To deploy profiles to Android, iOS, Windows Phone, and enrolled Windows 8.1 or later devices, these devices must be [enrolled in Microsoft Intune](/intune-classic/deploy-use/enroll-devices-in-microsoft-intune).   

A typical scenario for System Center Configuration Manager is to install trusted root CA certificates to authenticate Wi-Fi and VPN servers when the connection uses EAP-TLS, EAP-TTLS, and PEAP authentication protocols, and IKEv2, L2TP/IPsec, and Cisco IPsec VPN tunneling protocols.  

You must ensure that an enterprise root CA certificate is installed on the device before the device can request certificates by using a SCEP certificate profile.  

You can specify a variety of settings in a SCEP certificate profile to request customized certificates for different environments or connectivity requirements. The **Create Certificate Profile Wizard** contains two pages for enrollment parameters. The first, **SCEP Enrollment**, contains settings for the enrollment request and where to install the certificate. The second, **Certificate Properties**, describes the requested certificate itself.  

## Deploying certificate profiles  
 When you deploy a certificate profile, the certificate files within the profile are installed on client devices. Any SCEP parameters will also be deployed, and the SCEP requests will be processed on the client device. You can deploy certificate profiles to user or device collections and specify the destination store for each certificate. Applicability rules determine whether the certificates can be installed on the device. When certificate profiles are deployed to user collections, user device affinity determines which of the users' devices will install the certificates. When certificate profiles that contain user certificates are deployed to device collections, by default, the certificates will be installed on each of the users' primary devices. You can modify this behavior to install the certificate on any of the users' devices on the **SCEP Enrollment** page of the **Create Certificate Profile Wizard**. In addition, user certificates will not be deployed to devices if they are workgroup computers.  

## Monitoring certificate profiles  

You can monitor certificate profile deployments by viewing compliance results or reports. These approaches are described in [How to monitor certificate profiles](/sccm/protect/deploy-use/monitor-certificate-profiles).


## Automatic revocation of certificates  
 System Center Configuration Manager automatically revokes user and computer certificates that were deployed by using certificate profiles in the following circumstances:  

-   The device is retired from System Center Configuration Manager management.  

-   The device is selectively wiped.  

-   The device is blocked from the System Center Configuration Manager hierarchy.  

 To revoke the certificates, the site server sends a revocation command to the issuing certification authority. The reason for the revocation is **Cease of Operation**.  
