---
title: Plan on-premises MDM
titleSuffix: Configuration Manager
description: Plan for on-premises mobile device management to manage mobile devices in Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Plan for on-premises MDM in Configuration Manager

*Applies to: Configuration Manager (current branch)*

On-premises mobile device management (MDM) allows you to manage mobile devices using the management capabilities built into the device OS. The management capability is based on the Open Mobile Alliance (OMA) Device Management (DM) standard, and many device platforms use this standard to allow the devices to be managed. These devices are called *modern devices* in the documentation and the Configuration Manager console. This term distinguishes them from other devices that require the Configuration Manager client to manage them.  

Consider the following requirements before preparing the Configuration Manager infrastructure to handle on-premises MDM.



## <a name="bkmk_devices"></a> Supported devices  

The current branch of Configuration Manager supports enrollment in On-premises Mobile Device Management for devices running the following operating systems:  
  
- Windows 10 Enterprise  
- Windows 10 Pro  
- Windows 10 Team   
- Windows 10 Mobile  
- Windows 10 Mobile Enterprise
- Windows 10 IoT Enterprise   



##  <a name="bkmk_intune"></a> The Microsoft Intune subscription  

To start using on-premises MDM, you need a Microsoft Intune subscription. The subscription is only required to track licensing of the devices and isn't used to manage or store management information for the devices. All management data is stored in your organization using the on-premises Configuration Manager infrastructure.  

> [!Note]  
> Starting in version 1810, an Intune connection is no longer required for new on-premises MDM deployments.<!--3607730, fka 1359124--> Your organization still requires Intune licenses to use this feature. You can't currently remove the Intune connection from existing on-premises MDM deployments. For more information, see the [Intune support blog post](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

If your site has devices with internet connectivity, the Intune service can be used to notify devices to check the device management point for policy updates. This behavior uses Intune strictly for notification of internet-facing devices. Devices without internet connections and that can't be contacted by Intune rely on the configured polling interval to check in with site system roles for management functions.  

> [!TIP]  
> Before you set up the required site system roles, set up the Intune subscription. This action minimizes the time required for the roles to become functional.  

For information on how to set up the Intune subscription, see [Set up a Microsoft Intune subscription for on-premises MDM](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm).  



##  <a name="bkmk_roles"></a> Site system roles  

On-premises MDM requires at least one of each of the following site system roles:  

- **Enrollment proxy point** to support enrollment requests.  

- **Enrollment point** to support device enrollment.  

- **Device management point** for policy delivery. This site system role is a variation of the management point role that has been configured to allow for mobile device management.  

- **Distribution point** for content delivery.  

- **Service connection point** for connecting to Intune to notify devices outside the firewall.  

These site system roles can be installed on the single site system server or can be run separately on different servers depending on the needs of your organization. Each site system server used for on-premises MDM must be configured as an HTTPS endpoint for communicating with trusted devices. For more information, see [Required trusted communications](#bkmk_trustedComs).  

For more information on planning for site system roles, see [Plan for site system servers and roles for Configuration Manager](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).  

For more information on how to add the required site system roles, see [Install site system roles for on-premises MDM](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm).  



##  <a name="bkmk_trustedComs"></a> Trusted communications  

On-premises MDM requires site system roles to be enabled for HTTPS communications. Depending on your needs, you can use your enterprise's certificate authority (CA) to establish the trusted connections between servers and devices. You could also use a publicly available CA to be the trusted authority. Either way, you need a web server certificate to be configured in IIS on the site system servers hosting the required site system roles. You also need the root certificate of that CA installed on the devices that need to connect to those servers.  

If you use your enterprise's CA to establish trusted communications, do the following tasks:  

- Create and issue the web server certificate template on the CA.  

- Request a web server certificate for each site system server hosting a required site system role.  

- Configure IIS on the site system server to use the requested web server certificate.  

For devices joined to the corporate Active Directory domain, the root certificate of the enterprise CA is already available on the device for trusted connections. This behavior means that domain-joined devices are automatically trusted for HTTPS connections with the site system servers. However, non-domain-joined devices don't automatically get the required root certificate installed. To successfully communicate with site system servers supporting on-premises MDM, non-domain-joined devices such as mobile devices require you to manually install the root certificate on them.  

Export the root certificate of the issuing CA for use by individual devices. To get the root certificate file, you can export it using the CA. Another method is to use the web server certificate issued by the CA to extract the root, and create a root certificate file. Then the root certificate must be delivered to the device. Some example delivery methods include:

- File system  

- Email attachment  

- Memory card  

- Tethered device  

- Cloud storage (such as OneDrive)  

- Near field communication (NFC) connection  

- Barcode scanner  

- Out of box experience (OOBE) provisioning package  

For more information, see [Set up certificates for trusted communications in on-premises MDM](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  



##  <a name="bkmk_enrollment"></a> Device enrollment

To enable device enrollment for on-premises MDM,
- Users must be granted permission to enroll 
- Devices must be configured for trusted communications with the site system servers hosting the required roles  

Grant users permission to enroll devices by setting up an enrollment profile in Configuration Manager client settings. You can use the default client settings to push the enrollment profile to all discovered users. You can also set up the enrollment profile in custom client settings and push the settings to one or more user collections.  

Once users are granted permission, they can enroll their own devices. To get enrolled, the user's device must have the root certificate of the certification authority (CA) that issued the web server certificate used on the site system servers hosting the required roles.  

As an alternative to user-initiated enrollment, you can set up a bulk enrollment package. This package allows the device to be enrolled without user intervention. It can be delivered to the device before it's provisioned for use or after the device goes through its OOBE process.  

For more information on how to set up and enroll devices, see the following articles: 

- [Set up device enrollment for on-premises MDM](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

- [Enroll devices for on-premises MDM](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

