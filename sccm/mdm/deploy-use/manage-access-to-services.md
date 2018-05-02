---
title: "Conditional access"
titleSuffix: "Configuration Manager"
description: "Learn how to use conditional access in System Center Configuration Manager to help secure email and other services."
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Manage access to services in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


## Conditional access in System Center Configuration Manager
Use conditional access to specify conditions to help secure email and other services on devices enrolled with Microsoft Intune.  

 For information about conditional access on devices that are managed with the Configuration Manager client, see [Manage access to O365 services for PCs managed by System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


 A typical flow for conditional access might look as follows:  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 Use conditional access to manage access to the following services:  

-   Microsoft Exchange On-premises  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated  

-   SharePoint Online  

-   Skype for Business Online

-   Dynamics CRM Online

 To implement conditional access, you configure two policy types in Configuration Manager:  

-   **Compliance policies** are optional policies you can deploy to user collections and evaluate settings like:  

    -   Passcode  

    -   Encryption  

    -   Whether the device is jailbroken or rooted  

    -   Whether email on the device is managed by a Configuration Manager or Microsoft Intune policy  

     A device reports compliant for any applicable conditional access policies if you do not deploy any compliance policy to it.

-   **Conditional access policies** are for a particular service. These policies define rules such as which Azure Active Directory security user groups or Configuration Manager user collections to target or exclude.  

     You configure the on-premises Exchange conditional access policy from the Configuration Manager console. However, when you configure an Exchange Online or SharePoint Online policy, the Microsoft Intune console opens to configure the policy.  

     Unlike other Microsoft Intune or Configuration Manager policies, you do not deploy conditional access policies. Instead, you configure these policies once, and they apply to all targeted users.  

 When devices do not meet the configured conditions, the user is guided though enrolling the device and fixing the device compliance issue.  

Before you start using conditional access, ensure that you have the correct requirements in place:  

## Requirements for Exchange Online (using the shared multi-tenant environment)
Conditional access to Exchange Online supports devices that run:
-   Windows 8.1 and later (when enrolled with Intune)
-   Windows 7.0 or Windows 8.1 (when domain joined)
-   Windows Phone 8.1 and later
-   iOS 7.1 and later
-   Android 4.0 and later, Samsung KNOX Standard 4.0 and later

 **Additionally**:
-   Devices must be workplace joined, which registers the device with the Azure Active Directory Device Registration Service (AAD DRS).<br />     
- Domain joined PCs must be automatically registered with Azure Active Directory through group policy or MSI.

  The **Conditional access for PCs** section in this article describes all the requirements for enabling conditional access for a PC.<br />     
  AAD DRS activates automatically for Microsoft Intune and Office 365 customers. Customers who have already deployed the ADFS Device Registration Service do not see registered devices in their on-premises Active Directory.
-   Use an Office 365 subscription that includes Exchange Online (such as E3). Users must be licensed for Exchange Online.
-   The Exchange Server connector is optional and connects Configuration Manager to Microsoft Exchange Online. This connector helps you monitor device information through the Configuration Manager console. For more information, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
You do not need the connector to use compliance policies or conditional access policies. Running reports on the impact of conditional access requires the connector.

## Requirements for Exchange Online Dedicated
Conditional access to Exchange Online Dedicated supports devices that run:
-   Windows 8 and later (when enrolled with Intune)
-   Windows 7.0 or Windows 8.1 (when domain joined)

  Conditional access to domain joined PCs only to tenants in the new Exchange Online dedicated environment.
-   Windows Phone 8 and later
-   Any iOS device that uses an Exchange ActiveSync (EAS) email client
-   Android 4 and later.
-   For tenants in the legacy Exchange Online Dedicated environment:    

  Use the Exchange Server connector, which connects Configuration Manager to Microsoft Exchange on-premises. The connector lets you manage mobile devices and enables conditional access. For more information, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
-   For tenants in the new Exchange Online Dedicated environment:     
  The Exchange Server connector is optional, which connects Configuration Manager to Microsoft Exchange Online and helps you manage device information. For more information, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md). You do not need the connector to use compliance policies or conditional access policies. Running reports on the impact of conditional access requires the connector.  

## Requirements for Exchange on-premises
Conditional access to Exchange on-premises supports:
-   Windows 8 and later (when enrolled with Intune)
-   Windows Phone 8 and later
-   Native email app on iOS
-   Native email app on Android 4 or later
-   Microsoft Outlook app is not supported (Android and iOS)

**Additionally**:

- Exchange version must be Exchange 2010 or later
- Exchange server Client Access Server (CAS) array is supported

> [!TIP]
> If your Exchange environment is in a CAS server configuration, then you must configure the on-premises Exchange connector to point to one of the CAS servers.
- Use the Exchange Server connector, which connects Configuration Manager to Microsoft Exchange on-premises. The connector lets you manage mobile devices and enables conditional access. For more information, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - Make sure that you are using the latest version of the on-premises Exchange connector. Configure the on-premises Exchange connector through the Configuration Manager console. For a detailed walkthrough, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - Only configure the connector on the Configuration Manager primary site

- Exchange ActiveSync can be configured with certificate-based authentication, or user credential entry


## Requirements for Skype for Business Online
Conditional access to SharePoint Online supports devices that run:
 -   iOS 7.1 and later
 -   Android 4.0 and later
 -   Samsung KNOX Standard 4.0 or later

Enable [modern authentication](https://aka.ms/SkypeModernAuth) for Skype for Business Online. 

All of your users must use Skype for Business Online. If you have a deployment with both Skype for Business Online and Skype for Business on-premises, conditional access policy does not apply to on-premises users.

## Requirements for SharePoint Online
Conditional access to SharePoint Online supports devices that run:
 -   Windows 8.1 and later (when enrolled with Intune)
 -   Windows 7.0 or Windows 8.1 (when domain joined)
 -   Windows Phone 8.1 and later
 -   iOS 7.1 and later
 -   Android 4.0 and later, Samsung KNOX Standard 4.0 and later

 **Additionally**:
 -   Devices must be workplace joined, which registers the device with the Azure Active Directory Device Registration Service (AAD DRS).

 Domain joined PCs must be automatically registered with Azure Active Directory through group policy or MSI. The **Conditional access for PCs** section in this article describes all the requirements for enabling conditional access for a PC.

 AAD DRS activates automatically for Microsoft Intune and Office 365 customers. Customers who have already deployed the ADFS Device Registration Service do not see registered devices in their on-premises Active Directory.
 -   A SharePoint Online subscription is required and users must be licensed for SharePoint Online.

 ### Conditional access for PCs

 You can configure conditional access for PCs that run Office desktop applications, and access Exchange Online or SharePoint Online. The PCs must meet the following requirements:
 -   The PC must be running Windows 7.0 or Windows 8.1
 -   The PC must be either domain joined or compliant

 In order to be compliant, the PC must be enrolled in Microsoft Intune and comply with the policies.

 For domain joined PCs, you must  set it up to [automatically register the device](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/) with Azure Active Directory.
 -   [Office 365 modern authentication must be enabled](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/), and have all the latest Office updates.<br />     Modern authentication brings Active Directory Authentication Library (ADAL)-based sign-in to Office 2013 Windows clients and enables better security like multi-factor authentication and certificate-based authentication.
 -   Setup ADFS claims rules to block non-modern authentication protocols.  

## Next Steps  
 Read the following topics to learn how to configure compliance policies and conditional access policies for your required scenario:  

-   [Manage device compliance policies in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)  

-   [Manage email access in System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md)  

-   [Manage SharePoint Online access in System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Manage Skype for Business Online access](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### See also  

 [Get started with compliance settings in System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md)
