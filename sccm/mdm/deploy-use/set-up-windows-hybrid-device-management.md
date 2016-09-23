---
title: "Set up Windows hybrid device management with System Center Configuration Manager and Microsoft Intune"
ms.custom: na
ms.date: 03/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: NathBarn

---
# Set up Windows hybrid device management with System Center Configuration Manager and Microsoft Intune
You can use Configuration Manager with  Intune to manage desktops, laptops, and other devices running Windows as mobile devices. Before you can manage Windows devices as mobile devices, you must enable mobile device enrollment for those operating systems.  
  
## Set up Windows  device enrollment  
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

