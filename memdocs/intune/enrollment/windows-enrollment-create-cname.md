---
# required metadata

title: Enable auto-discovery of Intune enrollment server
titleSuffix:
description: Simplify enrollment for users by enabling automatic discovery of the Intune enrollment server. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/04/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: f94dbc2e-a855-487e-af6e-8d08fabe6c3d

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Enable auto-discovery of Intune enrollment server     
*Applies to Windows 10, Windows 11*  

[!INCLUDE [azure_portal](../includes/azure_portal.md)]  

If you're not using automatic enrollment as part of your enrollment or provisioning solution, we recommend creating a domain name server (DNS) alias, called a *CNAME* record type, for your MDM servers. The CNAME redirects enrollment requests to Intune servers so that device users don't have to enter the server address during device enrollment. Although the CNAME configuration is optional, it makes enrollment easier for users by enabling automatic discovery of the Intune enrollment server and reducing the amount of user interaction required.  

If you're enrolling Windows 10/11 devices using [MDM automatic enrollment](windows-enroll.md), you don’t have to worry about configuring CNAME records for your MDM server. The MDM server is configured by default when you enable MDM automatic enrollment in your tenant.    

## Step 1: Create CNAME 

Create CNAME DNS resource records for your organization's domain. For example, if your organization's website is contoso.com, create a CNAME record in DNS that redirects *EnterpriseEnrollment.contoso.com* to *enterpriseenrollment-s.manage.microsoft.com*. 

If no enrollment CNAME record is found, users are prompted to manually enter the MDM server name: *enrollment.manage.microsoft.com*. 

| Type | Host name | Points to | TTL |
|----------|---------------|---------------|---|
| CNAME | EnterpriseEnrollment.company_domain.com | EnterpriseEnrollment-s.manage.microsoft.com | 1 hour |
| CNAME | EnterpriseRegistration.company_domain.com | EnterpriseRegistration.windows.net | 1 hour |

If your organization uses more than one UPN suffix, create one CNAME for each domain name and point each one to *EnterpriseEnrollment-s.manage.microsoft.com*. 

For example:

1. Contoso users use the following formats as their email address/UPN:  
    - name@contoso.com
    - name@us.contoso.com
    - name@eu.contoso.com

2. As the Contoso DNS admin, you should configure CNAME records as described in the following table:  

   | Type | Host name | Points to | TTL |  
   |----------|---------------|---------------|---|
   | CNAME | EnterpriseEnrollment.contoso.com | EnterpriseEnrollment-s.manage.microsoft.com | 1 hour |
   | CNAME | EnterpriseEnrollment.us.contoso.com | EnterpriseEnrollment-s.manage.microsoft.com | 1 hour |
   | CNAME | EnterpriseEnrollment.eu.contoso.com | EnterpriseEnrollment-s.manage.microsoft.com | 1 hour |

`EnterpriseEnrollment-s.manage.microsoft.com` – Supports a redirect to the Intune service with domain recognition from the email's domain name

Changes to DNS records might take up to 72 hours to propagate. You can't verify the DNS change in Intune until the DNS record propagates.

## Step 2: Verify CNAME 

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > **Windows** > **Windows enrollment**.  
2. Select **CNAME Validation**.  
2. For **Domain**, enter the company website, and then choose **Test**.

## Best practices and recommendations    

*EnterpriseEnrollment-s.manage.microsoft.com* is the preferred FQDN for enrollment. *EnterpriseEnrollment.manage.microsoft.com* (without the *-s*) and *manage.microsoft.com* both work as the target for the auto-discovery server, but require users to acknowledge a confirmation message. We recommend using *EnterpriseEnrollment-s.manage.microsoft.com* because there is no confirmation required, which means one less step for the device user.  

Alternate redirection methods aren't supported with Intune. For example, you can't use a proxy server to redirect *enterpriseenrollment.contoso.com/EnrollmentServer/Discovery.svc* to *enterpriseenrollment-s.manage.microsoft.com/EnrollmentServer/Discovery.svc* or *manage.microsoft.com/EnrollmentServer/Discovery.svc*.  

## Registration CNAME  

Azure Active Directory uses a different CNAME during device registration for iOS/iPadOS, Android, and Windows devices. Intune conditional access requires devices to be registered to Azure AD (also called *workplace joined*). If you plan to use conditional access, you should configure the *EnterpriseRegistration* CNAME for each company name you have.  

| Type | Host name | Points to | TTL |
| --- | --- | --- | --- |
| CNAME | EnterpriseRegistration.company_domain.com | EnterpriseRegistration.windows.net | 1 hour |

For more information about device registration, see
[Manage device identities using the Azure portal](/azure/active-directory/devices/device-management-azure-portal)

## Windows auto enrollment and device registration  

This section applies to US government cloud customers on devices running Windows 10 or Windows 11.  

Although creating CNAME DNS entries is optional, CNAME records make enrollment easier for users. If no enrollment CNAME record is found, users are prompted to manually enter the MDM server name, enrollment.manage.microsoft.us.

| Type | Host name | Points to | TTL |
| --- | --- | --- | --- |
|CNAME | EnterpriseEnrollment.company_domain.com | EnterpriseEnrollment-s.manage.microsoft.us | 1 hour |
|CNAME | EnterpriseRegistration.company_domain.com | EnterpriseRegistration.windows.net | 1 hour |  

For more information about automatic enrollment for Windows, see [Set up automatic enrollment](../enrollment/windows-enroll.md).  

## Next steps


