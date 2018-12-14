---
title: Introduction to certificate profiles
titleSuffix: Configuration Manager
description: Learn how certificate profiles in System Center Configuration Manager work with Active Directory Certificate Services.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Introduction to certificate profiles in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


Certificate profiles work with Active Directory Certificate Services and the Network Device Enrollment Service (NDES) role. Create and deploy authentication certificates for managed devices so that users can easily access company resources. For example, you can create and deploy certificate profiles to provide the necessary certificates for users to connect to VPN and wireless connections.

Certificate profiles can automatically configure user devices. Users access company resources such as Wi-Fi networks and VPN servers without manually installing certificates or using an out-of-band process. Certificate profiles help to keep company resources secure because you can use more secure settings that are supported by your enterprise public key infrastructure (PKI). For example, require server authentication for all Wi-Fi and VPN connections because you've deployed the required certificates on the managed devices.   

Certificate profiles provide the following management capabilities:  

-   Certificate enrollment and renewal from an enterprise certification authority (CA) for devices that run iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop and Mobile, and Android. These certificates can then be used for Wi-Fi and VPN connections.  

-   Deployment of trusted root CA certificates and intermediate CA certificates. These certificates configure a chain of trust on devices for VPN and Wi-Fi connections when server authentication is required.  

-   Monitor and report about the installed certificates.  

**Example:** All employees must be able to connect to Wi-Fi hotspots in multiple corporate locations. To enable easy user connection, first deploy the certificates needed to connect to Wi-Fi. Then deploy Wi-Fi profiles that reference the certificate.  

**Example:** You have a PKI in place. You want to move to a more flexible, secure method of deploying certificates. Users should be able to access company resources from their personal devices without compromising security. Configure certificate profiles with settings and protocols that are supported for the specific device platform. The devices can then automatically request these certificates from an Internet-facing enrollment server. Then, configure VPN profiles to use these certificates so that the device can access company resources.  



## Types of certificate profiles  
 There are three types of certificate profiles:  

-   **Trusted CA certificate** - Deploy a trusted root CA or intermediate CA certificate. These certificates form a chain of trust when the device must authenticate a server.  

-   **Simple Certificate Enrollment Protocol (SCEP)** - Request a certificate for a device or user by using the SCEP protocol. This type requires the Network Device Enrollment Service (NDES) role on a server running Windows Server 2012 R2 or later.

    To create a **Simple Certificate Enrollment Protocol (SCEP)** certificate profile, first create a **Trusted CA certificate** profile.

-   **Personal information exchange (.pfx)** - Request a .pfx (also known as PKCS #12) certificate for a device or user.<!--1321368-->  

    You may create PFX certificate profiles by either [importing credentials](/sccm/mdm/deploy-use/import-pfx-certificate-profiles) from existing certificates or by [defining a certificate](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) authority to process requests.

    > [!Note]  
    > Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

    Starting with version 1706, you can use Microsoft or Entrust as certificate authorities for **Personal information exchange (.pfx)** certificates.


## Requirements and supported platforms  
To deploy certificate profiles that use SCEP, install the certificate registration point on a site system server. Also install a policy module for NDES, the Configuration Manager Policy Module, on a server that runs Windows Server 2012 R2 or later. This server requires the Active Directory Certificate Services role and a working NDES that is accessible to the devices that require the certificates. For the devices that are enrolled by Microsoft Intune, the NDES must be accessible from the Internet. For example, in a screened subnet, also known as a DMZ.  

PFX certificates also require a certificate registration point. Also specify the certificate authority (CA) for the certificate and the relevant access credentials. Starting with version 1706, you may specify either Microsoft or Entrust as certificate authorities.  

For more information about how the Network Device Enrollment Service supports a policy module so that Configuration Manager can deploy certificates, see [Using a Policy Module with the Network Device Enrollment Service](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

Depending on the requirements, Configuration Manager supports deploying certificates to different certificate stores on various device types and operating systems. The following devices and operating systems are supported:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop and Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  To deploy profiles to Android, iOS, Windows Phone, and enrolled Windows 8.1 or later devices, these devices must be [enrolled in Microsoft Intune](/intune/device-enrollment).   

A typical scenario for Configuration Manager is to install trusted root CA certificates to authenticate Wi-Fi and VPN servers when the connection uses EAP-TLS, EAP-TTLS, and PEAP authentication protocols, and IKEv2, L2TP/IPsec, and Cisco IPsec VPN tunneling protocols.  

An enterprise root CA certificate must be installed on the device before the device can request certificates by using a SCEP certificate profile.  

You can specify settings in a SCEP certificate profile to request customized certificates for different environments or connectivity requirements. The **Create Certificate Profile Wizard** has two pages for enrollment parameters. The first, **SCEP Enrollment**, includes settings for the enrollment request and where to install the certificate. The second, **Certificate Properties**, describes the requested certificate itself.  

## Deploying certificate profiles  
 When you deploy a certificate profile, the certificate files within the profile are installed on client devices. Any SCEP parameters are also deployed, and the SCEP requests are processed on the client device. You can deploy certificate profiles to user or device collections and specify the destination store for each certificate. Applicability rules determine whether the certificates can be installed on the device. When certificate profiles are deployed to user collections, user device affinity determines which of the users' devices install the certificates. When certificate profiles that include user certificates are deployed to device collections, by default the certificates are installed on each of the users' primary devices. You can modify this behavior to install the certificate on any of the users' devices on the **SCEP Enrollment** page of the **Create Certificate Profile Wizard**. If the devices are workgroup computers, user certificates are not deployed.  

## Monitoring certificate profiles  

You can monitor certificate profile deployments by viewing compliance results or reports. These approaches are described in [How to monitor certificate profiles](/sccm/protect/deploy-use/monitor-certificate-profiles).


## Automatic revocation of certificates  
 System Center Configuration Manager automatically revokes user and computer certificates that were deployed by using certificate profiles in the following circumstances:  

- The device is retired from System Center Configuration Manager management.  

- The device is selectively wiped.  

- The device is blocked from the System Center Configuration Manager hierarchy.  

  To revoke the certificates, the site server sends a revocation command to the issuing certification authority. The reason for the revocation is **Cease of Operation**.  
