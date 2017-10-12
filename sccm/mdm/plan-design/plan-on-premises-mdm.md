---
title: "Plan On-premises MDM"
titleSuffix: "Configuration Manager"
description: "Plan for On-premises Mobile Device Management to manage mobile devices in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
caps.latest.revision: 9
caps.handback.revision: 0
author: dougeby
ms.author: dougeby
manager: angrobe

---
# Plan for On-premises Mobile Device Management in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Consider the following requirements before preparing the Configuration Manager infrastructure to handle On\-premises Mobile Device Management.

##  <a name="bkmk_devices"></a> Supported devices  
 On-premises Mobile Device Management allows you to manage mobile devices using the management capabilities built into the device operating systems.  The management capability is based on the Open Mobile Alliance (OMA) Device Management (DM) standard, and many device platforms use this standard to allow the devices to be managed.  We call these **modern devices** (in the documentation and the Configuration Manager console user interface) to distinguish them from other devices that require the Configuration Manager client to manage them.  

 > [!NOTE]  
>  The current branch of Configuration Manager supports enrollment in On-premises Mobile Device Management for devices running the following operating systems:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(beginning in Configuration Manager version 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

##  <a name="bkmk_intune"></a> Use of the  Microsoft Intune subscription  
 To start using On\-premises Mobile Device Management, you will need a Microsoft Intune subscription. The subscription is only required to track licensing of the devices and is not used to manage or store management information for the devices. All management is handled in your organization's enterprise using the on-premises Configuration Manager infrastructure.  

 > [!NOTE]  
 > Beginning in version 1610, Configuration Manager supports managing mobile devices using both Microsoft Intune and on-premises Configuration Manager infrastructure at the same time.   

 If your site has devices with internet connectivity, the Intune service can be used to notify devices to  check the device management point for policy updates. This use of  Intune is strictly for notification only of internet-facing devices. Devices without internet connections (and cannot be contacted by Intune) rely on the configured polling interval to check in with site system roles for management functions.  

> [!TIP]  
>  We recommend that you set up the Intune before you set up the required site system roles to minimize the time required for the site system roles to become functional.  

 For information on how to set up the Intune subscription, see [Set up a Microsoft Intune subscription for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md).  

##  <a name="bkmk_roles"></a> Required site system roles  
 On\-premises Mobile Device Management requires at least one of each of the following site system roles:  

-   **Enrollment proxy point** to support enrollment requests.  

-   **Enrollment point** to support device enrollment.  

-   **Device management point** for policy delivery. This site system role is a variation of the management point role that has been configured to allow for mobile device management.  

-   **Distribution point** for content delivery.  

-   **Service connection point** for connecting to Intune to notify devices outside the firewall.  

 These site system roles can be installed on the single site system server or can be run separately on different servers depending the needs of your organization. Each site system server used for On\-premises Mobile Device Management must be configured as an HTTPS endpoint for communicating with trusted devices. For more information, see [Required trusted communications](#bkmk_trustedComs).  

 For more information on planning for site system roles, see [Plan for site system servers and site system roles for System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 For more information on how to add the required site system roles, see [Install site system roles for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).  

##  <a name="bkmk_trustedComs"></a> Required trusted communications  
 On\-premises Mobile Device Management requires site system roles to be enabled for HTTPS communications. Depending on your needs, you can use your enterprise's certificate authority (CA) to establish the trusted connections between servers and devices or you could use a publicly available CA to be the trusted authority.  Either way, you will need a web server certificate to be configured with IIS on the site system servers hosting the required site system roles, and you will need the root certificate of that CA installed on the devices that need to connect to those servers.  

 If you use your enterprise's CA to establish trusted communications, you need to do the following tasks:  

-   Create and issue the web server certificate template on the CA.  

-   Request a web server certificate for each site system server hosting a required site system role.  

-   Configure IIS on the site system server to use the requested web server certificate.  

 For devices joined to the corporate Active Directory domain, the root certificate of the enterprise CA is already available on the device for trusted connections. This means that domain-joined devices (like desktop computers) will automatically be trusted for HTTPS connections with the site system servers. However, non-domain-joined devices (typically mobile) will not have the required root certificate installed. Those devices will require the root certificate to be manually installed on them to successfully communicate with site system servers supporting On\-premises Mobile Device Management.  

 You must export the root certificate of the issuing CA for use by individual devices. To get the root certificate file, you can export it using the CA, or a simpler method is to use the web server certificate issued by the CA to extract the root and create a root certificate file.   Then, the root certificate must be delivered to the device.  Some example delivery methods include  

-   File system  

-   Email attachment  

-   Memory card  

-   Tethered device  

-   Cloud storage (such as OneDrive)  

-   Near field communication (NFC) connection  

-   Barcode scanner  

-   Out of box experience (OOBE) provisioning package  

 For more information, see [Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

##  <a name="bkmk_enrollment"></a> Enrollment considerations  
 To enable device enrollment for On\-premises Mobile Device Management, users must be granted permission to enroll and their devices must be able to have trusted communications with the site system servers hosting the required site system roles.  

 Granting user enrollment permission can be accomplished through setting up an enrollment profile in Configuration Manager client settings. You can use the default client settings to push the enrollment profile to all discovered users or you can set up the enrollment profile in custom client settings and push the settings to one or more user collections.  

 With user enrollment permission granted, users can enroll their own devices. To get enrolled, the user's device must have the root certificate of the certification authority (CA) that issued the web server certificate used on the site system servers hosting the required site system roles.  

 As an alternative to user-initiated enrollment, you can set up a bulk enrollment package that allows the device to be enrolled without user intervention. This package can be delivered to the device before it is initially provisioned for use or after the device goes through its OOBE process.  

 For more information on how to set up and enroll devices, see  

-   [Set up device enrollment for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

-   [Enroll devices for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md)  
