---
title: "Set up Windows hybrid device management with System Center Configuration Manager and Microsoft Intune | Microsoft Docs"
description: "Set up Windows device management with System Center Configuration Manager and Microsoft Intune."
ms.custom: na
ms.date: 03/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: nathbarn
ms.author: nathbarn
manager: angrobe

---
# Set up Windows hybrid device management with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

This topic tells IT admins how they can enable their users to bring Windows PCs and mobile devices into management using Configuration Manager and Microsoft Intune. Two enrollment methods are available:
- Azure Active Directory (AD) automatic enrollment
- Enrollment by installing and signing in with the Company Portal app

## Choose how to enroll Windows devices

Two factors determine how you'll enroll Windows devices:
- **Do you use Azure Active Directory Premium?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) is included with Enterprise Mobility + Security and other licensing plans.
- **What versions of Windows will enroll?** <br>Windows 10 devices can automatically enroll when users sign-in to devices with a work or school account. Earlier versions must enroll using the Company Portal app.

||**Azure AD Premium**|**Other AD **|
|----------|---------------|---------------|  
|**Windows 10**|[Automatic enrollment](#automatic-enrollment) |[Company Portal enrollment](#company-portal-enrollment)|
|**Earlier Windows versions**|[Company Portal enrollment](#company-portal-enrollment)|[Company Portal enrollment](#company-portal-enrollment)|

## Automatic enrollment

Automatic enrollment lets users enroll either company-owned or personal Windows 10 devices by adding a work or school account to the device and agreeing to be managed. In the background, the user's device registers and connects with Azure Active Directory. Once registered, the device can be managed with Intune. Managed devices can still use the Company Portal for tasks, but don't have to install it to become enrolled.

**Prerequisites**
- Azure Active Directory Premium subscription (If you don't have one, get a [trial subscription](https://go.microsoft.com/fwlink/?linkid=845167).)
- Microsoft Intune subscription

### Configure automatic enrollment

1. Sign in to the [Azure portal](https://manage.windowsazure.com), navigate to the **Active Directory** node in the left pane, and select your directory.
2. Select the **Configure** tab and scroll to the section called **Devices**.
3. Select **All** for **Users may workplace join devices**.
4. Select the maximum number of devices you want to authorize per user.

By default, two-factor authentication is not enabled for the service. However, two-factor authentication is recommended when registering a device. Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for multi-factor authentication. See [Getting started with the Azure Multi-Factor Authentication Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## Company Portal enrollment
Your end users or a [device enrollment manager](enroll-devices-with-device-enrollment-manager.md) can enroll Windows devices by installing the Company Portal app and then signing in with their work credentials. To simplify enrollment for your end users, you should [add a CNAME to your DNS registration](#create-dns-alias-for-device-enrollment).

### Enable Windows device management
To enable Windows device management for either PCs or mobile devices, use the following steps:

1.  Before you set up enrollment for any platform, complete the prerequisites and procedures in [Setup hybrid MDM](setup-hybrid-mdm.md).  
2.  In the Configuration Manager console in the **Administration** workspace, go to **Overview** > **Cloud Services** > **Microsoft Intune Subscriptions**.  
3.  In the ribbon, click **Configure Platforms**, and then select the platform:
    - **Windows** for Windows PCs and laptops, then perform the following steps:
      1. In the **General** tab, select **Enable Windows enrollment**.
      2. If you use a certificate to code-sign and deploy the Company Portal app, browse to the **Code-signing certificate**. Device users can also install the Company Portal app from the Windows Store or you can deploy the app from the Windows Store for Business without code-signing.
      3. You can also configure [Windows Hello for Business settings](windows-hello-for-business-settings.md).
    - **Windows Phone** for phones and tablets. Perform the following steps:
      1. In the **General** tab, select the **Windows Phone 8.1 and Windows 10 Mobile**. Windows Phone 8.0 is no longer supported.
      2. Users can enroll and then install the Company Portal app from the Windows Store. If your organization needs to sideload company apps or you need to deploy the Company Portal app using Intune, you can upload the required token or file.
        - **Application enrollment token**
        - **.pfx file**
        - **None**
      If you use a Symantec certificate, you can specify **Show an alert before Symantec certificates expire**.

      For more information about sideloading apps, see [Creat Windows apps](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
4. Click **OK** to close the dialog box.  To simplify the enrollment process using the Company Portal, you should [create a DNS alias](#create-dns-alias-for-device-enrollment) for device enrollment.
5. Tell users how to enroll devices. Now that you're set up, you'll need to let your users know how to enroll their devices. See [What to tell users about enrolling their devices](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) for guidance. You can direct users to [Enroll your Windows device in Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). This information applies to both Microsoft Intune and Configuration Manager-managed mobile devices.

### Create DNS alias for device enrollment  
A DNS alias (CNAME record type) makes it easier for users to enroll their devices by connecting to the Intune service without requiring the user to enter a server address. To create a DNS alias (CNAME record type), you have to configure a CNAME in your company's DNS records that redirects requests sent to a URL in your company's domain to Microsoft's cloud service servers.  For example, if your company's domain is contoso.com, you should to create a CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to EnterpriseEnrollment-s.manage.microsoft.com.  

 Although creating CNAME DNS entries is optional, CNAME records make enrollment easier for users. If no enrollment CNAME record is found, users are prompted to manually enter the MDM server name, enrollment.manage.microsoft.com.

|Type|Host name|Points to|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hour|

If you have more than one UPN suffix, you need to create one CNAME for each domain name and point each one to EnterpriseEnrollment-s.manage.microsoft.com. For example if users at Contoso use name@contoso.com, but also use name@us.contoso.com, and name@eu.constoso.com as their email/UPN, the Contoso DNS admin would need to create the following CNAMEs.

|Type|Host name|Points to|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hour|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hour|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hour|

## Tell users how to enroll devices  

 Once you're set up, you'll need to let your users know how to enroll their devices. See [What to tell users about enrolling their devices](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) for guidance. You can direct users to [Enroll your Windows device in Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). This information applies to both Microsoft Intune and Configuration Manager-managed mobile devices.

> [!div class="button"]
[< Previous step](create-service-connection-point.md)  [Next step >](set-up-additional-management.md)
