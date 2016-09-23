---
title: "Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune"
ms.custom: na
ms.date: 2016-03-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1973f960-19c3-4b85-be71-063375357a5b
caps.latest.revision: 14
author: NathBarn

---
# Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune
Before you can manage Windows Phone 8.1 and later mobile devices with Configuration Manager using Intune,  users must install the Company Portal app from the Windows Phone Store and then enroll it.  To enroll the Windows Phone 8.0 and to deploy company apps, including the Company Portal app, to Windows Phone 8.1 and later devices, you must get a Symantec Enterprise Mobile Code Signing certificate. You cannot use a certificate issued by your own certification authority because only the Symantec certificate is trusted by Windows Phone devices.  

## Set up Windows Phone device enrollment  
 To enable Windows Phone mobile device management, you need to enable management for the platform and instruct users to install the Company Portal app.  

### Create DNS alias for device enrollment  
 A DNS alias (CNAME record type) makes it easier for users to enroll their devices by automatically populating the server name during device enrollment. If you do not create DNS aliases to support device enrollment, you will need to provide  To create a DNS alias (CNAME record type), you have to configure a CNAME in your company's DNS records that redirects requests sent to a URL in your company's domain to Microsoft's cloud service servers. *EnterpriseEnrollment.<company domain name\>.com* to manage.microsoft.com. For example, if your company's domain is contoso.com, you have to create a CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to EnterpriseEnrollment-s.manage.microsoft.com.  

|Type|Host name|Points to|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  

### Enable Windows Phone 8.1 and later devices  
 If your users will only enroll Windows Phone 8.1 and later devices and you won't deploy line-of-business apps to Windows Phone devices, no Symantec certificate is needed. After enabling Windows Phone enrollment, you should instruct users to install the Company Portal app from the Windows Phone Store to enroll their devices.  

 Complete the following steps for the Windows Phone devices you will manage.  

##### To enable enrollment for Windows Phone 8.1 and later devices  

1.  **Prerequisites** - Before you can set up enrollment for any platform, complete the prerequisites and procedures in [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../mdm/plan-design/hybrid-mobile-device-management.md).  

2.  In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services** > **Microsoft Intune Subscriptions**.  

    > [!WARNING]  
    >  If other Configuration Manager dialog boxes are open, close them before continuing with this procedure.  

3.  On the **Home** tab, click **Configure Platforms**, and then click **Windows Phone**.  

4.  On the **General** tab, choose  **Windows Phone 8.1 and Windows 10 Mobile**. You can upload AET .xml file data or a .pfx file to support deployment of the Company Portal or instruct users to download the Company Portal from the Windows Phone Store.  

     Click **OK**.  

 Once you're set up, you'll need to let your users know how to enroll their devices. See [What to tell users about enrolling their devices](https://technet.microsoft.com/library/dn948527.aspx). This information applies to both Microsoft Intune and Configuration Manager-managed mobile devices.  

## Enable Windows Phone 8.0 enrollment and company app deployment for later devices  
 Before you can enable management for Windows Phone 8.0 devices or to sign and deploy line-of-business apps with Intune, you must acquire a Symantec Enterprise Mobile Code Signing certificate. This certificate is required to sign Windows Phone apps not installed from the Windows Phone Store, and any apps installed on Windows Phone 8.0 devices.  

 The steps below will help you get the required Symantec certificate and sign the Company Portal app (Windows Phone 8.0 only). You will need a Windows Phone Dev Center account, and then you will need to purchase a Symantec certificate.  

 For more information about the Symantec certificate requirement, see [Why does Windows Phone require a Symantec certificate for management?](https://technet.microsoft.com/en-us/library/dn764959.aspx)  

#### To prepare to enroll Windows Phone 8.0  

1.  **Prerequisites** - Before you can set up enrollment for any platform, you must complete the prerequisites listed in [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../mdm/plan-design/hybrid-mobile-device-management.md).  

2.  **Join the Windows Phone Dev Center**   
    Join the [Windows Phone Dev Center](http://go.microsoft.com/fwlink/?LinkId=268442) using corporate account information when logging in to purchase your company account. This request will need to be authorized by a company officer before you receive a code-signing certificate.  

3.  **Get a company Symantec certificate**   
    Purchase a certificate from the [Symantec website](http://go.microsoft.com/fwlink/?LinkId=268441) using your Symantec ID. After you purchase the certificate, the corporate approver who you designated in your Windows Phone Dev Center account will receive an email asking for approval of the certificate request.  

4.  **Import certificates**   
    Once the request has been approved, you will receive an email containing instructions for importing certificates. Follow the instructions in the email to import the certificates.  

5.  **Verify certificates imported**   
    To verify that the certificates have been imported correctly, go to the **Certificates** snap-in, right-click **Certificates**, and select **Find Certificates**. In the **Contains** field, enter "Symantec", and click **Find Now**. The certificates you imported should appear in the results.  

     ![certmgr&#45;WinPhone&#95;cert](../../mdm/deploy-use/media/certmgr-WinPhone_cert.jpg "certmgr-WinPhone_cert")  

6.  **Export a signing certificate**   
    Having verified that the certificates are present, you can export the .pfx file to sign the company portal. Select the Symantec certificate with **Intended purpose** "code-signing." Right-click the code-signing certificate and select **Export**.  

     ![certExport&#45;WinPhone](../../mdm/deploy-use/media/certExport-WinPhone.jpg "certExport-WinPhone")  

     In the **Certificate Export Wizard**, select **Yes, export the private key**, and then click **Next**. Select **Personal Information Exchange -PKCS #12 (.PFX)**, and check **Include all the certificates in the certification path if possible**. Complete the wizard. For more information, see how to [export a certificate with the private key](http://go.microsoft.com/fwlink/?LinkID=203031).  

7.  **Download the Company Portal**   
    Download the [Intune Company Portal for Windows Phone 8.0](http://go.microsoft.com/fwlink/?LinkId=268440) from the Download Center . The default installation location is `C:\Program Files (x86)\Microsoft Corporation\Windows Intune Company Portal for Windows Phone`.  

8.  **Download the SDK**   
    Download the [Windows Phone SDK](http://go.microsoft.com/fwlink/?LinkId=268439).  

9. **Code-sign the Company Portal app**   
    Use the XAPSignTool app downloaded with the SDK to sign the company portal with the .pfx file you created from the Symantec certificate. For more information, see [How to sign a company app by using XapSignTool](http://go.microsoft.com/fwlink/?LinkID=280195).  

10. **Create an application for distribution**   
    Create an application to deploy that contains the signed company portal app. Select **Automatically detect information about this application from installation files**. In **Type**, select **Windows Phone app package (\*.xap) file**. In **Location**, browse to a network share where you have copied the ssp.xap. On the **General Information** page, enter a name that will show up in the Configuration Manager console, but note that the application will always be displayed as Company Portal in the app list on Windows Phones.  

11. **Enable management by Configuration Manager**   
     In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services** > **Microsoft Intune Subscriptions**.  I the ribbon, select **Configure Platforms**, and then click **Windows Phone**.  

     On the **General** tab, choose the Windows Phone platforms that you will use. The **Windows Phone 8.0** and **Windows Phone 8.1 and Windows 10 Mobile** options determine the requirements needed for those platforms. For example, when you select **Windows Phone 8.0**, you are required to specify the Company Portal app on the **Company Portal App** tab. If you only select **Windows Phone 8.1 and Windows 10 Mobile**, the options are disabled on the **Company Portal App** tab because the Company Portal app installation is not associated with device enrollment with Windows Phone 8.1 or later devices.  

     Add the certificate (.pfx) file that you exported to .pfx file. Or choose Application enrollment token and browse to the location of the files. Then on the **Company Portal App** tab, click **Browse** and select the application package that contains the signed Company Portal app. This option is only available when you select Windows Phone 8.0 on the **General** tab. For Windows Phone 8.1 and later, deploy the application that contains the Company Portal app with a deployment purpose of **Required**.  

12. In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services** > **Microsoft Intune Subscriptions**.  

    > [!WARNING]  
    >  If other Configuration Manager dialog boxes are open, close them before continuing with this procedure.  

13. On the **Home** tab, click **Configure Platforms**, and then click **Windows Phone**.  

14. On the **General** tab, choose the Windows Phone platforms that you will use, and then click **Next**. The **Windows Phone 8.0** and **Windows Phone 8.1 and later** options are used to determine the requirements that are needed for those platforms. For example, when you select **Windows Phone 8.0**, you are required to specify the Company Portal app on the **Company Portal App** tab. If you only select **Windows Phone 8.1 and later**, the options are disabled on the **Company Portal App** tab because the Company Portal app installation is not associated with device enrollment with Windows Phone 8.1 or later devices.  

15. Add the certificate (.pfx) file that you exported to **.pfx file**. Or choose **Application enrollment token** and browse to the location of the files.  

16. On the **Company Portal App** tab, click **Browse** and select the application package that contains the signed Company Portal app. This option is only available when you select **Windows Phone 8.0** on the **General** tab. For Windows Phone 8.1 and later, deploy the application that contains the Company Portal app with a deployment purpose of **Required**. For details, see [Creating Windows Phone applications with System Center Configuration Manager](../../apps/get-started/creating-windows-phone-applications.md).  

17. **Distribute the application**   
    Use the Distribute Content wizard to distribute the Microsoft Intune company portal application to the manage.microsoft.com distribution point.  

    > [!IMPORTANT]  
    >  Do not create a deployment for this application - the deployment will be automatically created when you complete the Microsoft Intune Subscription Wizard.  

 Once you're set up, you'll need to let your users know how to enroll their devices. See [What to tell users about enrolling their devices](https://technet.microsoft.com/library/dn948527.aspx). This information applies to both Microsoft Intune and Configuration Manager-managed mobile devices.
