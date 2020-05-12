---
# required metadata

title: Set up enrollment for Windows devices by using Microsoft Intune
titleSuffix:
description: Set up enrollment for Windows devices.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/05/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: f94dbc2e-a855-487e-af6e-8d08fabe6c3d

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Set up enrollment for Windows devices

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

This article helps IT administrators simplify Windows enrollment for their users. Once you've [set up Intune](../fundamentals/setup-steps.md), users enroll Windows devices by [signing in](https://docs.microsoft.com/mem/intune/user-help/windows-enrollment-company-portal) with their work or school account.  

As an Intune admin, you can simplify enrollment in the following ways:

- [Enable automatic enrollment](#enable-windows-10-automatic-enrollment) (Azure AD Premium required)
- [CNAME registration](#simplify-windows-enrollment-without-azure-ad-premium)
- [Enable bulk enrollment](windows-bulk-enroll.md) (Azure AD Premium and Windows Configuration Designer required)

Two factors determine how you can simplify Windows device enrollment:

- **Do you use Azure Active Directory Premium?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) is included with Enterprise Mobility + Security and other licensing plans.
- **What versions of Windows clients will users enroll?** <br>Windows 10 devices can automatically enroll by adding a work or school account. Earlier versions must enroll using the Company Portal app.

||**Azure AD Premium**|**Other AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Automatic enrollment](#enable-windows-10-automatic-enrollment) |User enrollment|
|**Earlier Windows versions**|User enrollment|User enrollment|

Organizations that can use automatic enrollment can also configure [bulk enroll devices](windows-bulk-enroll.md) by using the Windows Configuration Designer app.

## Device enrollment prerequisites

Before an administrator can enroll devices to Intune for management, licenses should have already been assigned to the administrator's account. [Read about assigning licenses for device enrollment](../fundamentals/licenses-assign.md)

## Multi-user support

Intune supports multiple users on devices that both:

- run the Windows 10 Creator's update
- are Azure Active Directory domain-joined.

When standard users sign in with their Azure AD credentials, they receive apps and policies assigned to their user name. Only the device's [Primary user](../remote-actions/find-primary-user.md) can use the Company Portal for self-service scenarios like installing apps and performing device actions (Remove, Reset). For shared Windows 10 devices that do not have a primary user assigned, the Company Portal can still be used to install Available apps.

[!INCLUDE [AAD-enrollment](../includes/win10-automatic-enrollment-aad.md)]

## Simplify Windows enrollment without Azure AD Premium
To simplify enrollment, create a domain name server (DNS) alias (CNAME record type) that redirects enrollment requests to Intune servers. Otherwise, users trying to connect to Intune must enter the Intune server name during enrollment.

**Step 1: Create CNAME** (optional)<br>
Create CNAME DNS resource records for your company's domain. For example, if your company's website is contoso.com, you would create a CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to enterpriseenrollment-s.manage.microsoft.com.

Although creating CNAME DNS entries is optional, CNAME records make enrollment easier for users. If no enrollment CNAME record is found, users are prompted to manually enter the MDM server name, enrollment.manage.microsoft.com.

|Type|Host name|Points to|TTL|
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hour|
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|1 hour|

If the company uses more than one UPN suffix, you need to create one CNAME for each domain name and point each one to EnterpriseEnrollment-s.manage.microsoft.com. For example, users at Contoso use the following formats as their email/UPN:

- name@contoso.com
- name@us.contoso.com
- name@eu.contoso.com

The Contoso DNS admin should create the following CNAMEs:

|Type|Host name|Points to|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hour|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hour|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hour|

`EnterpriseEnrollment-s.manage.microsoft.com` – Supports a redirect to the Intune service with domain recognition from the email's domain name

Changes to DNS records might take up to 72 hours to propagate. You can't verify the DNS change in Intune until the DNS record propagates.

## Additional Endpoints Are Supported but Not Recommended
EnterpriseEnrollment-s.manage.microsoft.com is the preferred FQDN for enrollment, but there are two other endpoints that have been used by customers in the past and are supported. EnterpriseEnrollment.manage.microsoft.com (without the -s) and manage.microsoft.com both work as the target for the auto-discovery server, but the user will have to touch OK on a confirmation message. If you point to EnterpriseEnrollment-s.manage.microsoft.com, the user won't have to do the additional confirmation step, so this is the recommended configuration

## Alternate Methods of Redirection Are Not Supported
Using a method other than the CNAME configuration is not supported. For example, using a proxy server to redirect enterpriseenrollment.contoso.com/EnrollmentServer/Discovery.svc to either enterpriseenrollment-s.manage.microsoft.com/EnrollmentServer/Discovery.svc or manage.microsoft.com/EnrollmentServer/Discovery.svc is not supported.

**Step 2: Verify CNAME** (optional)<br>
1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Windows** > **Windows enrollment** > **CNAME Validation**.
2. In the **Domain** box, enter the company website and then choose **Test**.

## Tell users how to enroll Windows devices
Tell your users how to enroll their Windows devices and what to expect after they're brought into management.

> [!NOTE]
> End users must access the Company Portal website through Microsoft Edge to view Windows apps that you've assigned for specific versions of Windows. Other browsers, including Google Chrome, Mozilla Firefox, and Internet Explorer do not support this type of filtering.

For end-user enrollment instructions, see [Enroll your Windows device in Intune](../user-help/windows-enrollment-company-portal.md). You can also tell users to review [What can my IT admin see on my device](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md).

>[!IMPORTANT]
> If you do not have Auto-MDM enrollment enabled, but you have Windows 10 devices that have been joined to Azure AD, two records will be visible in the Intune console after enrollment. You can stop this by making sure that users with Azure AD joined devices go to **Accounts** > **Access work or school** and **Connect** using the same account. 

For more information about end-user tasks, see [Resources about the end-user experience with Microsoft Intune](../fundamentals/end-user-educate.md).

## Registration and Enrollment CNAMEs
Azure Active Directory has a different CNAME that it uses for device registration for iOS/iPadOS, Android, and Windows devices. Intune conditional access requires devices to be registered, also called "workplace joined". If you plan to use conditional access, you should also configure the EnterpriseRegistration CNAME for each company name you have.

| Type | Host name | Points to | TTL |
| --- | --- | --- | --- |
| NAME | EnterpriseRegistration. company_domain.com | EnterpriseRegistration.windows.net | 1 hour|

For more information about device registration, see
[Manage device identities using the Azure portal](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal)

## Windows 10 auto enrollment and device registration

This section applies to US government cloud customers.

Although creating CNAME DNS entries is optional, CNAME records make enrollment easier for users. If no enrollment CNAME record is found, users are prompted to manually enter the MDM server name, enrollment.manage.microsoft.us.

| Type | Host name | Points to | TTL |
| --- | --- | --- | --- |
| CNAME | EnterpriseEnrollment.company_domain.com | EnterpriseEnrollment-s.manage.microsoft.us | 1 hour|
|CNAME | EnterpriseRegistration.company_domain.com | EnterpriseRegistration.windows.net | 1 hour |


## Next steps

- [Considerations when managing Windows devices using Intune on Azure](../fundamentals/intune-legacy-pc-client.md).
