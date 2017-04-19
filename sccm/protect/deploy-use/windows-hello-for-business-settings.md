---
title: "Windows Hello for Business settings | Microsoft Docs"
description: "Learn how to integrate Windows Hello for Business with System Center Configuration Manager."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: 17
author: robstackmsftms.author: robstackmanager: angrobe

---
# Windows Hello for Business settings in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
System Center Configuration Manager lets you integrate with Windows Hello for Business (formerly Microsoft Passport for Windows), which is an alternative sign-in method for Windows 10 devices. Hello for Business uses Active Directory, or an Azure Active Directory account to replace a password, smart card, or virtual smart card.  

Hello for Business lets you use a **user gesture** to login, instead of a password. A user gesture might be a simple PIN, biometric authentication, or an external device such as a fingerprint reader.  

 Configuration Manager integrates with Windows Hello for Business in two ways:  

-   You can use Configuration Manager to control which gestures users can and cannot use to sign in.  

-   You can store authentication certificates in the Windows Hello for Business key storage provider (KSP). For more information, see [Certificate profiles](introduction-to-certificate-profiles.md).  

- You can deploy Windows Hello for Business policies to domain-joined Windows 10 devices that run the Configuration Manager client. This configuration is described in [Configure Windows Hello for Business on domain-joined Windows 10 devices](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices), below. When you are using Configuration Manager with Intune (hybrid), you can configure these settings on Windows 10, and Windows 10 Mobile devices, but not on domain-joined devices that run the Configuration Manager client. See [Configure Windows Hello for Business settings (hybrid)](../../mdm/deploy-use/windows-hello-for-business-settings.md) for more information.

## Configure Windows Hello for Business on domain-joined Windows 10 devices
You can control Windows Hello for Business settings on domain-joined Windows 10 devices in three ways:

- You can create and deploy a Windows Hello for Business Profile. This is the recommended approach.
- You can use group policy.  
- You can use a PowerShell script.

Note that in addition to this configuration, you must also deploy a certificate profile, as described in [Configure a certificate profile](#configure-a-certificate-profile).

## Recommended approach -  Configure a Windows Hello for Business profile  

In the Configuration Manager console, under **Company Resource Access**, right-click **Windows Hello for Business Profiles** and choose **New** to start the profile wizard. Provide the settings requested by the wizard, review and confirm the settings on the last page, and click **Close**. Here's an example of what your settings might look like:  

![Windows Hello for Business settings](../media/Hello-for-Business-settings.png)

## Configure Windows Hello for Business with Group Policy in Active Directory  

You can use an Active Directory Group Policy to configure your Windows 10 domain-joined devices to provision user Hello for Business credentials when a user logs to Windows:

1.  On a Windows Server  computer, open Server Manager and navigate to **Tools** > **Group Policy Management**.    

2.  In the **Group Policy Management** dialog box, expand the  domain in which you want to enable Automatic Workplace Join.    

3.  Right-click **Group Policy Objects**, and then click **New**.  

4.  In the **New GPO** dialog box, enter a name for the new Group Policy object, such as **Enable Windows Hello for Business**, and then click **OK**.  

5.  In the **Group Policy Objects** node, right-click the object you just created, and then click **Edit**.  

6.  In the **Group Policy Management Editor** dialog box, navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.  

7.  Right-click **Enable Windows Hello for Business** and then click **Edit**.   

8.  Select **Enabled**, click **Apply**, and then click **OK**.

You can now link the Group Policy object you just created to a location of your choice. For example:    

   A specific Organizational Unit (OU) in AD where Windows 10 domain-joined computers will be located.    

   A specific security group containing Windows 10 domain-joined computers that will be automatically registered with Azure AD.    

## Configure Windows Hello for Business by deploying a PowerShell script with Configuration Manager    
You can create and deploy the following PowerShell script by using Configuration Manager application management.    

**powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}" ** 

For more information about Configuration Manager application management, see [Introduction to application management in System Center Configuration Manager](/sccm/apps/understand/introduction-to-application-management).  

## Configure a certificate profile to enroll the Windows Hello for Business enrollment certificate in Configuration Manager  
 If you want to use Windows Hello for Business certificate-based logon, or Microsoft Hello, then configure the following:  

-   A Configuration Manager certificate profile.  

-   In the certificate profile, select a template that uses Smart Card logon EKU.  

-	If you intend to store certificate profiles in the Windows Hello for Business key container, and the certificate profile uses the **Smart Card Logon** EKU, you must configure the following permissions for key registration to ensure the certificate is validated correctly.
You must first have created the **Key Admins** group and added all Configuration Manager management point computers as members to this group.

	1.	Login to a domain controller or management workstations with Domain Admin, or equivalent credentials.
	2.	Open **Active Directory Users and Computers**.
	3.	From the navigation pane, right-click your domain name, and then click **Properties**.
	4.	On the **Security** tab of the *<domain name>* **Properties** dialog box, click **Advanced**. 
if the **Security** tab is not displayed, turn on **Advanced Features** from the **View** menu of **Active Directory Users and Computers**.
	5.	Click **Add**.
	6.	In the **Permission Entry for** *<domain name>* dialog box, click **Select a principal**.
	7.	In the **Select User, Computer, Service Account, or Group** dialog box, type **Key Admins** in the **Enter the object name to select** text box.  Click **OK**.
	8.	From the **Applies to** list, select **Descendant User objects**.
	9.	Scroll to the bottom of the page and click **Clear all**.
	10.	In the **Properties** section, select **Read msDS-KeyCredentialLink**.
	11.	Click **OK** three times to complete the task.


 For more information, see [Certificate profiles](introduction-to-certificate-profiles.md).  

## See also  
 [Protect data and site infrastructure with System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)

 [Manage identity verification using Windows Hello for Business](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport).  
