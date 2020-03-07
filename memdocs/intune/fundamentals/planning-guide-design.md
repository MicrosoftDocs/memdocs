---
# required metadata

title: Create your Microsoft Intune design
titleSuffix: Microsoft Intune
description: This article helps you to create a design for a Microsoft Intune cloud-only design and implementation.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 3/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: a8e38e29-f5e3-4a71-a170-d3b1a06e37c6

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Create a design

Your Intune design is based on the information you collect and decisions you make when completing other [sections of this guide](planning-guide.md). It helps you bring together:

- The current environment

- Intune deployment options

- Identity requirements for external dependencies

- Device platform considerations

- Requirements to be delivered  

Although there's minimal on-premises infrastructure requirements, a design plan is still helpful to make sure you have the right mobile device management solution that meets your goals, objectives, and requirements.

Let's review each of these areas in more detail. 

## Record your current environment
Additionally, it's common to have design changes during the implementation and testing phases. Use your design plan to document these changes and the rationale behind them as they occur.

Your current environment can influence design decisions and should be documented and referenced when you make other Intune design decisions. Below are few examples of how to record the current environment:

- **Identity in the cloud**

  - Do you use DirSync or Azure Active Directory (Azure AD) Connect?

  - Is your environment federated?

  - Is multi-factor authentication (MFA) enabled?

- **Email environment**

  - Do you use Exchange? Is it on-premises or in the cloud?

  - Are you in the middle of a project to migrate Exchange to the cloud?

- **Current mobile device management (MDM) solution**

  - Are you currently using other MDM solutions?

  - What MDM solutions are you using for corporate and BYOD use-case scenarios?

  - What capabilities are you using (for example: app device settings, Wi-Fi configurations)?

  - What device platforms are supported?

  - What groups and how many users are using the MDM solution?

- **Certificate solution**

  - Have you implemented a certificate solution?

  - What type of certificates do you use?

- **Systems management**

  - How are you managing your PC and server environment?

  - Are you using Microsoft Endpoint Configuration Manager? Are you using a third-party system management platform?

- **VPN solution**

  - What is your VPN solution?

  - Do you use it for both corporate and BYOD use-case scenarios?

Make sure to note any projects or any other plans in place that could affect your environment when recording the current MDM environment. Below is an example of a way to record the current environment when creating your Intune design:

| **Solution area** | **Current environment** | **Comments** |
|---|---|---|
| **Identity** | Azure AD, Azure AD Connect, not federated, no MFA | Project in place to enable MFA by end of year |                 
| **Email environment** | Exchange on-premises, Exchange online | Currently migrating from Exchange on-premises to Exchange online. 75% of mailboxes migrated. Last 25% will be migrated before Intune Pilot begins. |                
| **SharePoint** | SharePoint on-premises | No plans to move to SharePoint online |  
| **Current MDM** | Exchange ActiveSync |  |
| **Certificate solution** | Microsoft Server 2012 R2, AD Certificate Services | Only use PKI for Web Site Servers |
| **System Management** | Configuration Manager current branch | Would like to investigate co-management solution |
| **VPN solution** | Cisco AnyConnect |  |


You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to develop your Intune design plan.

## Intune tenant location

If your organization has global presence, make sure to plan where your tenant resides when you subscribe to the service. The country/region is defined when you sign up for an Intune subscription for the first time, and map to countries/regions around the world, which are listed below:

- North America

- Europe, Middle East, and Africa

- Asia and Pacific

>[!IMPORTANT]
> It's not possible to change the country/region and tenant location later.

## External dependencies

External dependencies are services and products that are separate from Intune, but are either a requirement of Intune, or might integrate with Intune. It's important to identify requirements for any external dependencies and how to configure them. Some examples of common external dependencies are:

- Identity

- User and device groups

- Public key infrastructure (PKI)

In the following, we explore these common external dependencies in more detail.

### Identity

Identity is how we identify the users who belong to your organization and are enrolling a device. Intune requires Azure Active Directory (Azure AD) as the user identity provider. If you already use this service, you can use your existing identity already in the cloud. In addition, Azure AD Connect is the recommended tool to synchronize your on-premises user identities with Microsoft cloud services. If your organization is already using Office 365, it's important for Intune to use the same Azure AD environment.

Learn more about the following Intune identity requirements:

- [Identity requirements](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions).

- [Directory synchronization requirements](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

- [Multi-factor authentication requirements](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

### User and device groups

User and device groups determine the target of a deployment, including policies, applications, and profiles. You need to determine what user and device groups will be required.

We recommend that you create all groups in the on-premises Active Directory, then synchronize to Azure AD. Learn more about user and device group planning and creation:

- [Plan your user and device groups](users-add.md).

- [Create user and device groups](groups-add.md).

### Public key infrastructure (PKI)
Public key infrastructure supplies certificates to devices or users to securely authenticate to a service. Intune supports a Microsoft PKI infrastructure. Device and user certificates can be issued to a mobile device to satisfy certificate-based authentication requirements. Before you use certificates, you need to determine if you need them, if the network infrastructure can support certificate-based authentication, and if certificates are currently used in the existing environment.

If you're planning to use certificates with VPN, Wi-Fi, or e-mail profiles with Intune, make sure you have a supported [PKI infrastructure in place](../protect/certificates-configure.md), ready to create and deploy certificate profiles.

In addition, if SCEP certificate profiles will be used, you need to determine which server will host the Network Device Enrollment Service (NDES) feature, and how the communication will happen.

Learn more about:

- [How to configure Intune certificate profiles](../protect/certificates-configure.md)

- [How to configure the certificate infrastructure for SCEP](../protect/certificates-scep-configure.md)

- [How to configure the certificate infrastructure for PFX](../protect/certficates-pfx-configure.md)




## Device platform considerations

Take a closer look at the following aspects of your devices to understand how to manage them correctly.

- Supported device platforms

- Devices

- Device ownership

- Bulk enrollment

Let's review these areas in more detail.

### Determine supported device platforms

You need to know what devices will be in the environment and verify whether they are supported or not by Intune when creating your design. Intune supports iOS/iPadOS, Android, and Windows platforms.

[Complete list of Intune supported devices](supported-devices-browsers.md).

### Devices

Intune manages mobile devices to secure corporate data and allow end users to work from more locations. Intune supports many device platforms, so we recommend that you document the devices and the OS platforms and the versions that will be supported in your organization's design. For example:

| **Device platform** | **OS Versions** |
|:---:|:---:|
| iOS - iPhone | 10.0+ |                
| iOS - iPad | 10.0+ |               
| Android – Samsung Knox Standard | 4.0+ |
| Windows 10 tablet | 10+ |


You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to develop your list of devices.
### Device ownership

Intune supports both corporate-owned devices and personal devices. A device is considered corporate-owned if your enroll it by a device enrollment manager, or device enrollment program. For example, a device is enrolled with the Apple Device Enrollment Program (DEP), marked as corporate, and placed in a device group that receives targeted corporate policies and apps.

Refer to [Section 3: Determine use case scenario requirements](planning-guide-requirements.md) for more information about corporate and BYOD use cases.

### Bulk enrollment

 You can enroll devices in bulk in different ways depending on the platform. If you require bulk enrollment, first [determine the bulk enrollment method](../enrollment/device-enrollment.md) and incorporate it in to your design.

## Feature requirements

In these sections, we review the following features and capabilities that are aligned with your use case scenario requirements:

- Terms and conditions policies

- Configuration policies

- Resource profiles

- Apps

- Compliance policy

- Conditional Access

Let's review each of these areas in more detail.

### Terms and conditions policies

You can use [terms and conditions](../enrollment/terms-and-conditions-create.md) to explain policies or conditions that an end user must accept before they can enroll their device. Intune supports the ability to add and deploy multiple terms and conditions policies to user groups.

You need to determine if terms and condition policies are needed. If so, who will be responsible for providing this information in the organization. An example of how to document the terms and conditions policy is below.

| **Terms and Conditions name** | **Use case** | **Targeted group** |
|:---:|:---:|:---:|
| Corporate T&C | Corporate | Corporate users |                 
| BYOD T&C | BYOD | BYOD users |                


You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to map your terms and conditions to your user groups.

### Configuration policies

Use configuration policies to manage security settings and features on a device. When designing your configuration policies, refer to the use case requirements section to determine the configurations required for Intune devices. Document the settings and how they should be configured. Also document which user or device groups they will be targeted to.

You should create at least one configuration policy per platform. You can create several configuration policies per platform if needed. Below is an example of designing four different configuration policies for different platforms and use-case scenarios.

| **Policy name** | **Device platform** | **Settings** | **Target group** |   
|:---:|:---:|:---:|:---:|
| Corporate - iOS | iOS | PIN is required, Length: 6, Restrict Cloud Backup | Corporate Devices |                                                           
| Corporate - Android | Android | PIN is required, Length: 6, Restrict Cloud Backup | Corporate Devices |                                                           
| BYOD – iOS  | iOS | PIN is required, Length: 4 | BYOD devices |
| BYOD – Android  | Android | PIN is required, Length: 4 | BYOD devices |


You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to identify your configuration policy needs.

### Profiles

Use profiles to help the end user connect to company data. Intune supports many types of profiles. Refer to the use cases and requirements to determine when the profiles will be configured. All device profiles are categorized by platform type and should be included in the design documentation.

- Certificate profiles

- Wi-Fi profile

- VPN profile

- Email profile

Let's review each type of profile in more detail.

#### Certificate profiles

Certificate profiles allow Intune to issue a certificate to a user or device. Intune supports the following:

- Simple Certificate Enrollment Protocol (SCEP)

- Trusted Root Certificate

- PFX certificate.

We recommend that you document which user group needs a certificate, how many certificate profiles you need, and which user groups to deploy them to.

>[!NOTE]
> Remember that the trusted root certificate is required for the SCEP certificate profile, so make sure all users targeted for the SCEP certificate profile also receive a trusted root certificate. If you need SCEP certificates, design and document what SCEP certificate templates you need.

Here's an example how you can document the certificates during the design:

| **Type** | **Profile name** | **Device platform** | **Use cases** |   
|:---:|:---:|:---:|:---:|
| Root CA | Corporate Root CA | Android, iOS/iPadOS, Windows mobile | Corporate, BYOD  |                                                           
| SCEP | User Certificate | Android, iOS/iPadOS, Windows mobile | Corporate, BYOD |                                                           


You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to identify your certificate profile needs.

#### Wi-Fi profile

Wi-Fi profiles are used to automatically connect a mobile device to a wireless network. Intune supports deploying Wi-Fi profiles to all supported platforms. Learn more about [how Intune supports Wi-Fi profiles.](../configuration/wi-fi-settings-configure.md)

Below is an example of a design for a Wi-Fi profile:

| **Type** | **Profile name** | **Device platform** | **Use cases** |
|:---:|:---:|:---:|:---:|
| Wi-Fi | Asia Wi-Fi profile | Android | Corporate, BYOD Asia region|
| Wi-Fi | North America Wi-Fi profile | Android, iOS/iPadOS, Windows 10 Mobile | Corporate, BYOD North America region |

You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to identify your Wi-Fi profile needs.

#### VPN profile

VPN profiles let users securely access your network from remote locations. Intune supports VPN profiles from native mobile VPN connections and third-party vendors. Learn more about [VPN profiles and vendors supported by Intune](../configuration/vpn-settings-configure.md).

Below is an example of documenting the design of a VPN profile.

| **Type** | **Profile name** | **Device platform** | **Use cases** |
|:---:|:---:|:---:|:---:|
| VPN | VPN Cisco any connect Profile | Android, iOS/iPadOS, Windows 10 Mobile | Corporate, BYOD North America and Germany|
| VPN | Pulse Secure | Android | Corporate, BYOD Asia region |

You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to identify your VPN profile needs.

#### Email profile

Email profiles allow an email client to be automatically set up with connection information and email configuration. Intune supports email profiles on some devices. Learn more about [email profiles and what platforms are supported](../configuration/email-settings-configure.md).

Below is an example of documenting the design of email profiles:

| **Type** | **Profile name** | **Device platform** | **Use cases** |
|:---:|:---:|:---:|:---:|
| Email profile | iOS email profile | iOS | Corporate – Information worker BYOD |
| Email profile | Android Knox email profile | Android Knox | BYOD |

You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to identify your email profile needs.
### Apps

You can use Intune to deliver apps to the users or devices in several ways. The type of application includes software installer apps, apps from a public app store, external links, or managed iOS apps. In addition to individual app deployments, you can manage and deploy volume-purchased apps obtained through the volume-purchase programs for iOS and Windows. Learn more about:

- [The types of apps you can deliver](../apps/app-management.md)

- [iOS Volume Purchase Program for Business (VPP)](../apps/vpp-apps-ios.md)

- [Microsoft Store for Business apps](../apps/windows-store-for-business.md)

#### App type requirements

Since apps can be deployed to users and devices, we recommend that you decide which applications will be managed by Intune. While gathering the list, try to answer the following questions:

- Do the apps require integration with cloud services?

- Will all apps be available to BYOD users?

- What are the deployment options available for these apps?

- Does your company need to provide access to Software-as-a-service (SaaS) apps data for their partners?

- Do the apps require internet access from user's devices?

- Are the apps publicly available in an app store, or are they custom line-of-business (LOB) apps?


#### App protection policies

App protection policies minimize data loss by defining how the application manages the corporate data. Intune supports app protection policies for any application built to function with mobile app management. When you design the app protection policy, you need to decide what restrictions you want to place on corporate data in a given app. We recommend that you review how [app protection policies](../apps/app-protection-policy.md) work. Below is an example of how to document the existing applications and what protection is needed.

| **Application** | **Purpose** | **Platforms** | **Use case** | **App protection policy** |
|:---:|:---:|:---:|:---:|:---:|
| Outlook mobile  | Available | iOS | Corporate - Executives | Cannot be jail broken, encrypt files |                                                         
| Word | Available | iOS/iPadOS, Android - Samsung Knox, non-Knox, Windows 10 mobile | Corporate, BYOD | Cannot be jail broken, encrypt files |                                                         


You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to identify your app protection policy needs.
#### Compliance policies

Compliance policies determine whether a device conforms to certain requirements. Intune uses compliance policies to determine if a device is considered compliant or noncompliant. The compliance status can then be used to restrict or allow access to company resources. If Conditional Access is required, we recommend that you design a [device compliance policy](../protect/device-compliance-get-started.md).

Refer to requirements and use cases to determine how many device compliance policies you need and which user groups are the target user groups. Additionally, you need to decide how long a device can be offline without checking in before it's considered noncompliant.

Below is an example of how to design a compliance policy:

| **Policy name** | **Device platform** | **Settings** | **Target group** |
|:---:|:---:|:---:|:---:|
| Compliance policy | iOS/iPadOS, Android - Samsung Knox, non-Knox, Windows 10 mobile | PIN - required, cannot be jail broken | Corporate, BYOD |


You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to identify your compliance policy needs.
#### Conditional Access policies

Conditional Access is used to allow only compliant devices to access email and other company resources. Intune works with Enterprise Mobility + Security (EMS) to control access to company resources. Decide if you require Conditional Access, and what must be secured. Learn more about [Conditional Access](../protect/conditional-access.md).

For online access, decide what platforms and user groups you'll target by Conditional Access policies. Also, determine whether you need to install or configure the Intune connector for Exchange on-premises: 

- [Exchange on-premises](../protect/exchange-connector-install.md)

Here's an example of how to document Conditional Access policies:

| **Service** | **Platforms for Modern Authentication** | **Basic Authentication** | **Use cases** |
|:---:|:---:|:---:|:---:|
| Exchange online | iOS/iPadOS, Android | Block noncompliant devices on platforms supported by Intune | Corporate, BYOD |
| SharePoint online | iOS/iPadOS, Android |  | Corporate, BYOD |

You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to identify your Conditional Access policy needs.

## Next steps

The next section provides guidance on the [Intune implementation process](planning-guide-onboarding.md).
