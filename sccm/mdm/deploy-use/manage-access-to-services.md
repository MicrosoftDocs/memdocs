---
title: "Conditional access"
titleSuffix: "Configuration Manager"
description: "Learn how to use conditional access in System Center Configuration Manager to help secure email and other services."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: 26
author: andredm7
ms.author: andredm
manager: angrobe

---

# Manage access to services in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


## Conditional access in System Center Configuration Manager
Use **conditional access**  to help secure email and other services on devices that are enrolled with Microsoft Intune, depending on conditions you specify.  

 For information about **conditional access on PCs that are managed with System Center Configuration Manager** and evaluated for compliance, see [Manage access to O365 services for PCs managed by System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


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

    -   Whether email on the device is managed by a Configuration Manager or Intune policy  

     **If no compliance policy is deployed to a device, then any applicable conditional access policies will treat the device as compliant**.  

-   **Conditional access policies** are configured for a particular service, and define rules such as which Azure Active Directory security user groups or Configuration Manager user collections will be targeted, or exempt.  

     You configure the On-Premises Exchange conditional access policy from the Configuration Manager console. However, when you configure an Exchange Online or SharePoint Online policy, this opens the Intune admin console where you configure the policy.  

     Unlike other Intune or Configuration Manager policies, you do not deploy conditional access policies. Instead, you configure these once, and they apply to all targeted users.  

 When devices do not meet the conditions you configure, the user is guided though the process of enrolling the device and fixing the issue that prevents the device from being compliant.  

**Before** you start using conditional access, ensure that you have the correct **requirements** in place:  

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

  The **Conditional access for PCs** section in this topic describes all the requirements for enabling conditional access for a PC.<br />     
  AAD DRS will be activated automatically for Intune and Office 365 customers. Customers who have already deployed the ADFS Device Registration Service will not see registered devices in their on-premises Active Directory.
-   You must use an Office 365 subscription that includes Exchange Online (such as E3) and users must be licensed for Exchange Online.
-   The optional **Exchange Server connector** is optional and connects Configuration Manager to Microsoft Exchange Online and helps you monitor device information through the Configuration Manager console (see [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
You do not need to use the connector to use compliance policies or conditional access policies, but is required to run reports that help evaluate the impact of conditional access.

## Requirements for Exchange Online Dedicated
Conditional access to Exchange Online Dedicated supports devices that run:
-   Windows 8 and later (when enrolled with Intune)
-   Windows 7.0 or Windows 8.1 (when domain joined)

  Conditional access to domain joined PCs only to tenants in the new Exchange Online dedicated environment.
-   Windows Phone 8 and later
-   Any iOS device that uses an Exchange ActiveSync (EAS) email client
-   Android 4 and later.
-   For tenants in the **legacy Exchange Online Dedicated environment**:    

  You must use the  **Exchange Server connector** which connects Configuration Manager to Microsoft Exchange On-premises. This lets you manage mobile devices and enables conditional access (see [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
-   For tenants in the **new Exchange Online Dedicated environment**:     
  The optional **Exchange Server connector** connects Configuration Manager to Microsoft Exchange Online and helps you manage device information (see [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)). You do not need to use the connector to use compliance policies or conditional access policies, but is required to run reports that help evaluate the impact of conditional access.  

## Requirements for Exchange On-premises
Conditional access to Exchange On-premises supports:
-   Windows 8 and later (when enrolled with Intune)
-   Windows Phone 8 and later
-   Native email app on iOS
-   Native email app on Android 4 or later
-   Microsoft Outlook app is not supported (Android and iOS).

**Additionally**:

-  Exchange version must be Exchange 2010 or later. Exchange server Client Access Server (CAS) array is supported.

> [!TIP]
> If your Exchange environment is in a CAS server configuration, then you must configure the on-premises Exchange connector to point to one of the CAS servers.
- You must use the **Exchange Server connector** which connects Configuration Manager to Microsoft Exchange On-premises. This lets you manage mobile devices  and enables conditional access (see [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
  - Make sure that you are using the latest version of the **on-premises Exchange connector**. The on-premises Exchange connector should be configured through the Configuration Manager console. For a detailed walkthrough, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - The connector must  be configured only on the System Center Configuration Manager Primary Site.</li><li>This connector  supports Exchange CAS environment. <br />        When configuring the connector, you must set it so it talk to the one of the Exchange CAS servers.

- Exchange ActiveSync can be configured with certificate based authentication, or user credential entry


## Requirements for Skype for Business Online
Conditional access to SharePoint Online supports devices that run:
 -   iOS 7.1 and later
 -   Android 4.0 and later
 -   Samsung KNOX Standard 4.0 or later

**Additionally,** you must enable modern authentication for Skype for Business Online. Fill this [connect form](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) to be enrolled in the modern authentication program.

All your end-users must be using the Skype for Business Online. If you have a deployment with both Skype for Business Online and Skype for Business on-premises, conditional access policy will not be applied to end-users who are in the on-premises deployment.

## Requirements for SharePoint Online
Conditional access to SharePoint Online supports devices that run:
 -   Windows 8.1 and later (when enrolled with Intune)
 -   Windows 7.0 or Windows 8.1 (when domain joined)
 -   Windows Phone 8.1 and later
 -   iOS 7.1 and later
 -   Android 4.0 and later, Samsung KNOX Standard 4.0 and later

 **Additionally**:
 -   Devices must be workplace joined, which registers the device with the Azure Active Directory Device Registration Service (AAD DRS).

 Domain joined PCs must be automatically registered with Azure Active Directory through group policy or MSI. The **Conditional access for PCs** section in this topic describes all the requirements for enabling conditional access for a PC.

 AAD DRS will be activated automatically for Intune and Office 365 customers. Customers who have already deployed the ADFS Device Registration Service will not see registered devices in their on-premises Active Directory.
 -   A SharePoint Online subscription is required and users must be licensed for SharePoint Online.

 ### Conditional access for PCs

 You can setup conditional access for PCs that run Office desktop applications to access **Exchange Online** and **SharePoint Online** for PCs that meet the following requirements:
 -   The PC must be running Windows 7.0 or Windows 8.1.
 -   The PC must either be domain joined or compliant.

 In order to be compliant, the PC must be enrolled in Intune and comply with the policies.

 For domain joined PCs, you must  set it up to [automatically register the device](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) with Azure Active Directory.
 -   [Office 365 modern authentication must be enabled](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/), and have all the latest Office updates.<br />     Modern authentication brings Active Directory Authentication Library (ADAL) based sign-in to Office 2013 Windows clients and enables better security like **multi-factor authentication**, and **certificate-based authentication**.
 -   Setup ADFS claims rules to block non-modern authentication protocols.  

## Next Steps  
 Read the following topics to learn how to configure compliance policies and conditional access policies for your required scenario:  

-   [Manage device compliance policies in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)  

-   [Manage email access in System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md)  

-   [Manage SharePoint Online access in System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Manage Skype for Business Online access](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### See also  

 [Get started with compliance settings in System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md)
