---
title: "Set up Windows hybrid device management with System Center Configuration Manager and Microsoft Intune"
description: "Set up Windows device management with System Center Configuration Manager and Microsoft Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: NathBarnms.author: nathbarnmanager: angrobe

---
# Set up Windows hybrid device management with System Center Configuration Manager and Microsoft Intune*Applies to: System Center Configuration Manager (Current Branch)*
You can use Configuration Manager with  Intune to manage desktops, laptops, and other devices running Windows as mobile devices. You can set up Azure Active Directory to allow automatic enrollment of Windows PCs. You can also configure Configuration Manager to simplify enrollment using the Company Portal app.

- [Enable automatic enrollment](#azure-active-directory-enrollment)
- [Enable Company Portal enrollment](#set-up-windows-device-enrollment)

## Azure Active Directory enrollment

Automatic enrollment lets users enroll either company-owned or personal Windows 10 PCs and Windows 10 Mobile devices in Intune by adding a work or school account and agreeing to be managed. Simple as that. In the background, the user's device registers and joins Azure Active Directory. Once registered, the device is managed with Intune.

**Prerequisites**
- Azure Active Directory Premium subscription ([trial subscription](http://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune subscription


### Configure automatic MDM enrollment

1. In the [Azure management portal](https://manage.windowsazure.com) (https://manage.windowsazure.com), navigate to the **Active Directory** node and select your directory.

2. Click the **Applications** tab and you should see **Microsoft Intune** in the list of applications.

    ![Azure AD apps with Microsoft Intune](../media/aad-intune-app.png)

3. Click on the arrow for **Microsoft Intune** and you should see a page that enables you to configure Microsoft Intune.

4. Click **Configure** to start configuring automatic MDM enrollment with Microsoft Intune.

5. Specify the URLs for Intune:

  - **MDM Enrollment URL** – Use `https://enterpriseenrollment-s.manage.microsoft.com/EnrollmentServer/Discovery.svc` for the MDM Enrollment URL.
  - **MDM Terms of Use URL** – Use the default value. This URL displays terms of use for users when enrolling devices.
  - **MDM Compliance URL** – Use the default value. If a device is found to be out of compliance, an **Access denied** message is displayed with this URL. The URL points to a page that helps users understand why their device is not compliant with policy and how they can bring it back into compliance.

6.  Specify which users’ devices should be managed by Microsoft Intune. These users’ Windows 10 devices will be automatically enrolled for management with Microsoft Intune.

  - **All**
  - **Groups**
  - **None**

7. Choose **Save**.

## Set up Windows device enrollment
 To enable Windows mobile device management, you need to enable management for the operating system.  

### Create DNS alias for device enrollment  
 A DNS alias (CNAME record type) makes it easier for users to enroll their devices by automatically populating the server name during device enrollment. To create a DNS alias (CNAME record type), you have to configure a CNAME in your company's DNS records that redirects requests sent to a URL in your company's domain to Microsoft's cloud service servers.  For example, if your company's domain is contoso.com, you should to create a CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to EnterpriseEnrollment-s.manage.microsoft.com.  

|Type|Host name|Points to|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  

### Enable enrollment for Windows devices  
 To support enrollment of Windows computers for management as mobile devices, complete the following steps.  

##### To enable enrollment for Windows devices  

1.  **Prerequisites** - Before you can set up enrollment for any platform, complete the prerequisites and procedures in [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../mdm/plan-design/hybrid-mobile-device-management.md).  

2.  In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services** > **Microsoft Intune Subscriptions**.  

    > [!WARNING]  
    >  If other Configuration Manager dialog boxes are open, close them before continuing with this procedure.  

3.  On the **Home** tab, click **Configure Platforms**, and then click **Windows**.  

4.  On the **General** tab, select **Enable Windows enrollment**.  

 Once you're set up, you'll need to let your users know how to enroll their devices. See [What to tell users about enrolling their devices](https://technet.microsoft.com/library/dn948527.aspx). This information applies to both Microsoft Intune and Configuration Manager-managed mobile devices.
