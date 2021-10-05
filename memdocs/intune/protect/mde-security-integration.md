---
# required metadata

title: Use MDE Security Configuration Management in Microsoft Endpoint manager
description: Use Intune profiles to manage security settings for Microsoft Defender for Endpoint on devices that register in your Azure Active Directory. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/16/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata
 
#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattcall


---
<!-- Release branch: release-mde-integration. Draft and scope in progress. Place images in ./media/mde-security-integration folder.  -->


# Manage Microsoft Defender for Endpoint on devices with Microsoft Endpoint Manager

With Security configuration management for Microsoft Defender for Endpoint (MDE), you use the Microsoft Endpoint Manager admin center to configure and monitor MDE security configurations on devices that aren’t’ managed by an MDM solution. This scenario isn’t about device management, but security management. Security management for MDE assists you on your journey towards Zero Trust by helping you secure the devices that aren’t managed through dedicated device management like Intune or Configuration Manager.

You configure security management within the Microsoft Endpoint Manager admin center using the same policies you use to configure security for enrolled and managed devices. On supported devices, the MDE Sense agent reads the security configuration policy, configures the device, and then reports back on its status and security configuration. Then, within the Microsoft Endpoint Manager you can view the security status of all your devices in one location.

This scenario supports devices that aren’t enrolled with a product like Intune or Configuration Manager. If a device is managed through Intune or Configuration Manager, you use those channels to manage MDE on the device instead.

<!-- Placeholder image follows -->
:::image type="content" source="./media/mde-security-integration/endpoint-security-overview.png" alt-text="Conceptual diagram of the MDE-Attach solution.":::

## Overview

To use Security management for MDE, you connect your MDE subscription to MEM. After they’re connected you can enroll devices with MDE. Enrollment installs the MDE Sense agent on the device and registers it with your Azure AD if the device doesn’t already have a registration. It’s through the Azure AD registration that the Sense agent receives policies for the MDE configuration and reports back the device status.

The broad strokes to use Security management for MDE include:

- In a single Azure tenant, connect Microsoft Defender for Endpoint to Microsoft Endpoint Manager.
- Identify supported devices that aren’t enrolled with Intune or managed by Configuration Manager, and onboard them to MDE. Onboarding also ensures the device is registered in Azure AD.
- Use the Endpoint security node in the Microsoft Endpoint Manager admin center to create and deploy policy to manage MDE and view reports.

> [!TIP]
> You can use Security management for MDE to manage MDE on devices that are enrolled with a third-party non-Microsoft MDM.  

## Architecture

<!-- Placeholder image follows. Use of AAD and MEM for Azure AD and Microsoft Endpoint Manager must be fixed for use in docs -->
:::image type="content" source="./media/mde-security-integration/pending-mde-attach-architecture.png" alt-text="Conceptual representation of the MDE-Attach solution.":::

1. Blah
2. Blah
<!-- for Localization, the more text we can add outside the image, the better -->

## Which solution should I use?



## Prerequisites

### Environment

Your environment must use Azure AD or Hybrid Azure AD. When a device enrolls with MDE, the device is registered automatically:

- New devices are registered in Azure AD at the time they onboard to MDE.
- Existing registrations are used when the device is already present in Azure AD.
- Devices without a domain relationship (workgroup devices) are registered in Azure AD without user interaction.

Devices must have access to the following endpoints:

- `enterpriseregistration.windows.net` – For Azure AD registration.
- `login.microsoftonline.com` – For Azure AD registration.
- `*.dm.microsoft.com` -  The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting,and which can change as the service scales.

### Supported platforms

<!-- Owned by MDE?  possibly and Include?     What' about Windows 10? -->
Security management for MDE policies are supported for the following device platforms:

- Windows 11
- Windows Server 2012 R2
- Windows Server 2016

### Licensing and subscriptions

To use security management for MDE, you need only a subscription for Microsoft Defender for Endpoint. The source of that license doesn’t matter and might be provided through Microsoft 365, an E5, or a license for only Microsoft Defender for Endpoint.

*Any subscription* that grants MDE licenses also grants your tenant access to the Endpoint security node of the Microsoft Endpoint Manager admin center. The Endpoint security node is where you’ll configure and deploy policies to manage MDE for your devices and monitor device status.

## Configure your tenant

<!--  Rough notes:

1.	Configure your Tenant.
IDENTITY
a.	Azure AD Connect:  Ensure Sync Scope is setup properly for AAD Connect.
b.	If you use ADFS:  Federation Claims must be configured properly for ADFS scenarios. (Does hybrid join work correctly? Your probably good to go). 
c.	If Enterprise DRS (Device registration service), take caution. This requires some extra configuration and care. (Should be rare… Escalate that to devs for support…)

FLIP TOGGLES: 
- In MDE: 
  - Enable MDE-attach for security settings management in MEM (This will change, MDE-attach isn’t usable).
- In Microsoft Endpoint Manager: 
  - Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations

*** Any supported device not managed by Microsoft Endpoint Manager, will be queued up to onboard!
-->

## Onboard devices

<!-- Owned by MDE?  possibly and Include?  -->

## Deploy policy

Use the following endpoint security policies and profiles for security configuration management:

- Antivirus
- Firewall


## Monitor status


## Next steps