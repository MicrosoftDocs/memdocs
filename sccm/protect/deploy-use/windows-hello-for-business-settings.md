---
title: "Windows Hello for Business settings | System Center Configuration Manager"
ms.custom: na
ms.date: 2016-07-22
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: 17
author: robstackmsft
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Windows Hello for Business settings in System Center Configuration Manager
System Center Configuration Manager lets you integrate with Windows Hello for Business, which is an alternative sign-in method for Windows 10 devices. Hello for Business uses Active Directory, or an Azure Active Directory account to replace a password, smart card, or virtual smart card.  
  
Hello for Business lets you use a **user gesture** to login, instead of a password. A user gesture might be a simple PIN, biometric authentication, or an external device such as a fingerprint reader.  
  
 Configuration Manager integrates with Windows Hello for Business in two ways:  
  
-   You can use Configuration Manager to control which gestures users can and cannot use to login  
  
-   You can store authentication certificates in the Windows Hello for Business key storage provider (KSP). For more information, see [Certificate profiles in System Center Configuration Manager](../Topic/Certificate%20profiles%20in%20System%20Center%20Configuration%20Manager.md).  
 
<!-- [cmshort](../../apps/deploy-use/includes/cmshort_md.md)] for domain-joined Windows 10 devices that run the Configuration Manager client. This configuration is described in [Configure Windows Hello for Business on domain-joined Windows 10 devices](#BKMK_Dom), below.!-->
<!-- When you are using Configuration Manager with Microsoft Intune (hybrid), you can configure these settings on Windows 10, and Windows 10 Mobile devices, but not on domain-joined devices that run the Configuration Manager client.-->    


  
  
## To configure Windows Hello for Business settings (hybrid)  
  
1.  In the Configuration Manager console, click **Administration**.  
  
2.  In the **Administration** workspace, expand **Cloud Services**, and then click **Microsoft Intune Subscriptions**.  
  
3.  From the list, select your Microsoft Intune subscription and then, in the **Home** tab, in the **Subscription** group, click **Configure Platforms** > **Windows (MDM)**.  
  
4.  On the **Windows Hello for Business** tab of the **Microsoft Intune Subscription Properties** dialog box, choose from the following values that will affect all enrolled Windows 10 and Windows 10 Mobile devices:  
  
    -   **Disable Windows Hello for Business on enrolled devices** or **Enable Windows Hello for Business on enrolled devices** - Enables or disables the use of Windows Hello for Business on all enrolled Windows 10 and Windows 10 Mobile devices.  
  
    -   **Use a Trusted Platform Module (TPM)** - A Trusted Platform Module (TPM) chip provides an additional layer of data security. Choose one of the following values:  
  
        -   **Required** (default) - Only devices with an accessible TPM can provision Windows Hello for Business.  
  
        -   **Preferred** - Devices first attempt to use a TPM. If this is not available, they can use software encryption  
  
    -   **Require minimum PIN length** - Specify the minimum number of characters required for the Windows Hello for Business PIN. You must use at least 4 characters (the default value is 6 characters).  
  
    -   **Require maximum PIN length** - Specify the maximum number of characters allowed for the Windows Hello for Business PIN. You can use up to 127 characters.  
  
    -   **Require lowercase letters in PIN** - Specifies whether lowercase letters must be used  in the Windows Hello for Business PIN. Choose from:  
  
        -   **Allowed** - Users can use lowercase characters in their PIN.  
  
        -   **Required** - Users must include at least one lowercase character in their PIN.  
  
        -   **Not allowed** (default) - Users must not use lowercase characters in their PIN.  
  
    -   **Require uppercase letters in PIN** - Specifies whether uppercase letters must be used  in the Windows Hello for Business PIN. Choose from:  
  
        -   **Allowed** - Users can use uppercase characters in their PIN.  
  
        -   **Required** - Users must include at least one uppercase character in their PIN.  
  
        -   **Not allowed** (default) - Users must not use uppercase characters in their PIN.  
  
    -   **Require special characters** - Specifies the use of special characters in the PIN. Choose from:  
  
        -   **Allowed** - Users can use special characters in their PIN.  
  
        -   **Required** - Users must include at least one special character in their PIN.  
  
        -   **Not allowed** (default) - Users must not use special characters in their PIN (this is also the behavior if the setting is not configured).  
  
         Special characters include: **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**.  
  
    -   **Require PIN expiration (days)** - Specifies the number of days before the device PIN must be changed. The default is 41 days.  
  
    -   **Prevent reuse of previous PINS** - Use this setting to restrict the re-use of previously used PINS. The default is the last 5 PINS used cannot be reused.  
  
    -   **Enable biometric gestures** - Enables biometric authentication such as facial recognition or fingerprint as an alternative to a PIN for Windows Hello for Business. Users must still configure a work PIN in case biometric authentication fails.  
  
         If set to **Enabled**, Windows Hello for Business allows biometric authentication.  If set to **Disabled**, Windows Hello for Business prevents biometric authentication (for all account types).  
  
    -   **Use enhanced anti-spoofing, when available** - Configures whether enhanced anti-spoofing is used on devices that support it.  
  
         If set to **Enabled**, Windows requires all users to use anti-spoofing for facial features when supported.  
  
    -   **Use Remote Passport** - If this option is set to **Enabled**, users can use a remote Hello for Business to serve as a portable companion device for desktop computer authentication. The desktop computer must be Azure Active Directory joined, and the companion device must be configured with a Windows Hello for Business PIN.  
  
5.  When you are finished, click **OK**.  
  
 
<!-- ##  <a name="BKMK_Dom"></a> Configure Windows Hello for Business on domain-joined Windows 10 devices    -->
<!--You can control Windows Hello for Business settings on domain-joined Windows 10 devices in three ways:  -->

<!--- You can create and deploy a Windows Hello for Business Profile. This is the recommended approach.  -->
<!--- You can use group policy.  -->
<!--- You can use a PowerShell script.  -->

<!--Note that in addition to this configuration, you must also deploy a certificate profile, as described in [Configure a certificate profile](#BKMK_step2).  -->
  
<!--### Recommended approach -  Configure a Windows Hello for Business profile  -->

<!--In the admin console, under **Company Resource Access**, right-click **Windows Hello for Business Profiles** and choose **New** to start the profile wizard. Provide the settings requested by the wizard, review and confirm the settings on the last page, and click **Close**. Here's an example of what your settings might look like:  -->

<!-- ![Hello for Business settings](../../protect/deploy-use/media/Hello-for-Business-settings.png)  -->
   
<!-- ### Configure Windows Hello for Business with Group Policy in Active Directory  -->

<!-- You can use an Active Directory Group Policy to configure your Windows 10 domain-joined devices to provision user Hello for Business credentials when a user logs to Windows:  -->  
   
<!--1.  On a Windows Server  computer, open Server Manager and navigate to **Tools** > **Group Policy Management**.    -->
  
<!--2.  In the **Group Policy Management** dialog box, expand the  domain in which you want to enable Automatic Workplace Join.    -->
  
<!--3.  Right-click **Group Policy Objects**, and then click **New**.  -->  
  
<!--4.  In the **New GPO** dialog box, enter a name for the new Group Policy object, such as **Enable Windows Hello for Business**, and then click **OK**.  -->  
  
<!--5.  In the **Group Policy Objects** node, right-click the object you just created, and then click **Edit**.    -->
  
<!--6.  In the **Group Policy Management Editor** dialog box, navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.    -->
  
<!--7.  Right-click **Enable Windows Hello for Business** and then click **Edit**.  -->  
  
<!--8.  Select **Enabled**, click **Apply**, and then click **OK**.  -->  
  
<!-- You can now link the Group Policy object you just created to a location of your choice. For example:    -->
  
<!---   A specific Organizational Unit (OU) in AD where Windows 10 domain-joined computers will be located.    -->
  
<!---   A specific security group containing Windows 10 domain-joined computers that will be automatically registered with Azure AD.  -->  
  
<!--#### Configure Windows Hello for Business by deploying a PowerShell script with Configuration Manager    -->
<!--You can create and deploy the following PowerShell script by using Configuration Manager application management.  -->  
  
<!--```    -->
<!--powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}"   --> 
<!--```  -->  
  
<!-- For more information about Configuration Manager application management, see [Deploy and manage applications with System Center Configuration Manager](../Topic/Deploy%20and%20manage%20applications%20with%20System%20Center%20Configuration%20Manager.md).  -->
  
## <a name="BKMK_step2"></a>Configure a certificate profile to enroll the Windows Hello for Business enrollment certificate in Configuration Manager  
 If you want to use Windows Hello for Business certificate-based logon, or Microsoft Hello, then configure the following:  
  
-   A Configuration Manager certificate profile.  
  
-   In the certificate profile, select a template that uses Smart Card logon EKU.  
  
 For more information, see [Certificate profiles in System Center Configuration Manager](../Topic/Certificate%20profiles%20in%20System%20Center%20Configuration%20Manager.md).  
  
### See also  
 [Protect data and site infrastructure with System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)
 
 [Manage identity verification using Microsoft Passport](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport).  
 