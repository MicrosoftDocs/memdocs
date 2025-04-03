---
title: Plan on-premises MDM
titleSuffix: Configuration Manager
description: Plan for on-premises mobile device management to manage mobile devices in Configuration Manager
ms.date: 01/09/2020
ms.subservice: mdm
ms.service: configuration-manager
ms.topic: article
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Plan for on-premises MDM in Configuration Manager

*Applies to: Configuration Manager (current branch)*

There are several key areas to review when you're planning to implement on-premises mobile device management (MDM) in Configuration Manager:

- Supported devices and OS versions
- Required site system roles
- Secure communication
- Device enrollment

> [!IMPORTANT]
> While the site or any mobile device doesn't connect to Microsoft Intune, your organization still requires Intune licenses to use this feature. For more information, see [Microsoft Intune licensing](/mem/intune-service/fundamentals/licenses).

Consider the following requirements before preparing the Configuration Manager infrastructure to handle on-premises MDM.

## <a name="bkmk_devices"></a> Supported devices  

The current branch of Configuration Manager supports enrollment in on-premises mobile device management for devices running Windows 10. These device types primarily include laptops, IoT, and Surface Hub. For more information and the list of specific editions, see [Supported OS versions for clients and devices](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

## <a name="bkmk_roles"></a> Site system roles

On-premises MDM requires at least one of the following site system roles:

- **Enrollment proxy point** to support enrollment requests.

- **Enrollment point** to support device enrollment.

- **Device management point** for policy delivery. This role is a variation of the management point, but allows for mobile device management.

- **Distribution point** for content delivery.

Depending on the needs of your organization, you can install these roles on the single server or separately on different servers.

> [!NOTE]
> You need to configure each role used for on-premises MDM as an HTTPS endpoint for communicating with trusted devices. For more information, see [Required trusted communications](#bkmk_trustedComs).

For more general information, see [Plan for site system servers and roles](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="bkmk_trustedComs"></a> Trusted communications

On-premises MDM requires that you enable site system roles for HTTPS communications. Depending on your needs, you can use your organization's certificate authority (CA) to establish the trusted connections between servers and devices. You can also use a publicly available CA to be the trusted authority. Either way, you need to configure the following certificates:

- A **web server certificate** in IIS on the servers hosting the required site system roles. If one server hosts multiple site system roles, then you only need one certificate for that server. If each role is on a separate server, each server needs a separate certificate.

- The **trusted root certificate** of the CA that issues the web server certificates. Install this root certificate on all devices that need to connect to the site system roles.

For more information, see [Set up certificates for trusted communications in on-premises MDM](../get-started/set-up-certificates-on-premises-mdm.md).

## <a name="bkmk_enrollment"></a> Device enrollment

To enable device enrollment for on-premises MDM:

- Grant users permission to enroll via client settings

- Configure devices for trusted communications with the site system servers hosting the required roles

As an alternative to user-initiated enrollment, you can set up a bulk enrollment package. This package allows the device to enroll without user intervention. Deliver the package to the device before it's provisioned for use or after it goes through its OOBE process.

For more information, see [Set up device enrollment for on-premises MDM](../get-started/set-up-device-enrollment-on-premises-mdm.md).

## Next step

> [!div class="nextstepaction"]
> [Install site system roles](../get-started/install-site-system-roles-for-on-premises-mdm.md)