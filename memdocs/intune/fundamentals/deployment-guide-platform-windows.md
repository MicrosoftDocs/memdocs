---
# required metadata

title: Deployment guide for Windows device management | Microsoft Intune  
description: Use our platform deployment guide to set up Windows device management in Microsoft Intune.    
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 02/06/2023  
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience: 
#ms.devlang:
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection: M365-identity-device-management
---

# Deployment guide: Manage devices running Windows 10/11

This guide describes how to protect and manage Windows apps and endpoints using Microsoft Intune, and includes our setup recommendations and resources from prerequisites to enrollment.    

For each section in this guide, review the associated tasks. Some tasks are required and some, like setting up Azure AD conditional access, are optional. Select the provided links in each section to go to our recommended help docs on Microsoft Learn, where you can find more detailed information and how-to instructions.        
 
## Step 1: Prerequisites  

 Complete the following prerequisites to enable your tenant's endpoint management capabilities:   

* [Add users](users-add.md) and [groups](groups-add.md)
* [Assign licenses to users](licenses-assign.md) 
* [Set mobile device management authority](mdm-authority-set.md) 
* [Have Global Administrator or Intune administrator Azure Active Directory permissions](role-based-access-control.md)  

 For more details and recommendations about how to prepare your organization, onboard, or adopt Intune for mobile device management, see [Migration guide: Set up or move to Microsoft Intune](deployment-guide-intune-setup.md).    

## Step 2: Plan for your deployment  

Use the Microsoft Intune planning guide to define your device management goals, use-case scenarios, and requirements. Use the guide to plan for rollout, communication, support, testing, and validation. For example, in some cases you don't have to be present when employees and students are enrolling their devices. We recommend having a communication plan so that people know where to find information about installing and using Intune Company Portal.  

For more information, see [Microsoft Intune planning guide](intune-planning-guide.md).  

## Step 3: Create compliance policies    
Use compliance policies to ensure that devices accessing your data are secure and meet your organization's standards. The final stage of the enrollment process is the compliance evaluation, which verifies that the settings on the device meet your policies. Device users must resolve all compliance issues to get access to protected resources.  Intune marks devices that fall short of compliance requirements as *non-compliant* and takes additional action (such as sending the user a notification, restricting access, or wiping the device) according to your *action for noncompliance* configurations.  

You can use Azure AD conditional access policies in conjunction with device compliance policies to control access to Windows PCs, corporate email, and Microsoft 365 services. For example, you can create a policy that blocks employees from accessing Microsoft Teams in Edge without first enrolling or securing their device.    

>[!TIP]
> For an overview of device compliance policies, see [Compliance overview](../protect/device-compliance-get-started.md#device-compliance-policies).     

| Task | Detail | 
| ---- | ------ | 
| [Create a compliance policy](../protect/create-compliance-policy.md)|Get step-by-step guidance on how to create and assign a compliance policy to user and device groups.   |       
| [Add actions for noncompliance](../protect/actions-for-noncompliance.md) |Choose what happens when devices no longer meet the conditions of your compliance policy. Examples of actions include sending alerts, remotely locking devices, or retiring devices. You can add actions for noncompliance when you configure a device compliance policy, or later by editing the policy. |  
| Create [a device-based](../protect/create-conditional-access-intune.md) or [app-based](../protect/app-based-conditional-access-intune-create.md) conditional access policy| Select the apps or services you want to protect and define the conditions for access. |   
|[Block access to apps that don't use modern authentication](../protect/app-modern-authentication-block.md)  | Create an app-based Conditional Access policy to block apps that use authentication methods other than OAuth2; for example, those apps that use basic and form-based authentication. Before you block access, however, sign in to Azure AD and review the [authentication methods activity report](/azure/active-directory/authentication/howto-authentication-methods-activity) to see if users are using basic authentication to access essential things you forgot about or are unaware of. For example, things like meeting room calendar kiosks use basic authentication.  | 
| [Add custom compliance settings](../protect/compliance-use-custom-settings.md) | With custom compliance settings, you can write your own Bash scripts to address compliance scenarios not yet included in the device compliance options built into Microsoft Intune. This article describes how to create, monitor, and troubleshoot custom compliance policies for Windows devices. Custom compliance settings require you to [create a custom script](../protect/compliance-custom-json.md) that identifies the settings and value pairs.| 


## Step 4: Configure endpoint security  

Use Intune endpoint security features to configure device security and to manage security tasks for devices at risk. 

| Task | Detail | 
| ---- | ------ | 
|[Manage devices with endpoint security features](../protect/endpoint-security-manage-devices.md)|Use the endpoint security settings in Intune to effectively manage device security and remediate issues for devices.|
|[Add endpoint protection settings](../protect/endpoint-protection-configure.md)| Configure common endpoint protection security features, such as firewall, BitLocker, and Microsoft Defender. For a description of the settings in this area, see the [endpoint protection settings reference](../protect/endpoint-protection-windows-10.md).   | 
|[Configure Microsoft Defender for Endpoint in Intune](../protect/advanced-threat-protection-configure.md)|When you integrate Intune with Microsoft Defender for Endpoint, you not only help prevent security breaches, but you can take advantage of Microsoft Defender for Endpoints Threat & Vulnerability Management (TVM) and use Intune to remediate endpoint weakness identified by TVM.| 
|[Manage BitLocker policy](../protect/encrypt-devices.md)| Ensure that devices are encrypted upon enrollment by creating a policy that configures BitLocker on managed devices. | 
|[Manage security baseline profiles](../protect/security-baselines-configure.md)| Use the security baselines in Intune to help you secure and protect your users and devices. A security baseline includes the best practices and recommendations for settings that impact security.  | 
|[Use Windows Update for Business for software updates](/windows/deployment/update/waas-configure-wufb)|Configure a Windows Update rollout strategy with Windows Update for Business. This article introduces you to the policy types you can use to manage Windows 10/11 software updates, and how to transition from update ring deferrals to a feature updates policy. |   

## Step 5: Configure device settings     

Use Microsoft Intune to enable or disable Windows settings and features on devices. To configure and enforce these settings, create a device configuration profile and then assign the profile to groups in your organization. Devices receive the profile once they enroll.        

| Task | Detail | 
| ---- | ------ | 
|[Create a device profile](../configuration/device-profile-create.md) |Create a device profile in Microsoft Intune and find resources about all device profile types. You can also use the [settings catalog](../configuration/settings-catalog.md) to create a policy from scratch.|  
|[Configure group policy settings](../configuration/administrative-templates-windows.md) |Use Windows 10 templates to configure group policy settings in Microsoft Intune. Administrative templates include hundreds of settings that you can configure for Internet Explorer, Microsoft Edge, OneDrive, remote desktop, Word, Excel, and other Office programs. These templates give administrators a simplified view of settings similar to group policy, and they're 100% cloud-based.|  
|[Configure Wi-Fi profile](../configuration/wi-fi-settings-configure.md)|This profile enables people to find and connect to your organization's Wi-Fi network. For a description of the settings in this area, see the [Wi-Fi settings reference for Windows 10 and later](../configuration/wi-fi-settings-windows.md).|
|[Configure VPN profile](../configuration/vpn-settings-configure.md)|Set up a secure VPN option, such as Microsoft Tunnel, for people connecting to your organization's network.  For a description of the settings in this area, see the [VPN settings reference](../configuration/vpn-settings-windows-10.md). |  
|[Configure email profile](../configuration/email-settings-configure.md)|Configure email settings so that people can connect to a mail server and access their work or school email. For a description of the settings in this area, see the [email settings reference](../configuration/email-settings-windows-10.md).|
|[Restrict device features](../configuration/device-restrictions-configure.md)|Protect users from unauthorized access and distractions by limiting the device features they can use at work or school. For a description of the settings in this area, see the [device restrictions reference for Windows 10/11](../configuration/device-restrictions-windows-10.md) and [Windows 10 Teams](../configuration/device-restrictions-windows-10-teams.md). |
|[Configure custom profile](../configuration/custom-settings-configure.md)|Add and assign device settings and features that aren't built into Intune. For a description of the settings in this area, see the [custom settings reference](../configuration/custom-settings-windows-10.md).|
|[Configure BIOS settings](../configuration/device-firmware-configuration-interface-windows.md)|Set up Intune so that you can control UEFI (BIOS) settings on enrolled devices, using the Device Firmware Configuration Interface (DFCI)|  
|[Configure Domain Join](../configuration/domain-join-configure.md)|If you're planning to enroll Azure AD joined devices, be sure to create a domain join profile so that Intune knows which on-premises domain to join.|  
|[Configure delivery optimization settings](../configuration/delivery-optimization-windows.md)|Use these settings to reduce bandwidth consumption on devices downloading apps and updates.|  
|[Customize branding and enrollment experience](../apps/company-portal-app.md)|Customize the Intune Company Portal and Microsoft Intune app experience with your organization's own words, branding, screen preferences, and contact information.|
|[Configure kiosks and dedicated devices](../configuration/kiosk-settings.md)|Create a kiosk profile to manage devices running in kiosk mode. |  
|[Customize shared devices](../configuration/shared-user-device-settings.md)|Control access, accounts, and power features on shared or multi-user devices.|  
|[Configure network boundary](../configuration/network-boundary-windows.md)|Create a network boundary profile to protect your environment from sites you don't trust.  | 
|[Configure Windows health monitoring](../configuration/windows-health-monitoring.md)|Create a Windows health monitoring profile to permit Microsoft to collect data about performance and provide recommendations for improvements. Creating a profile enables the endpoint analytics feature in Microsoft Endpoint Manager, which analyzes collected data, recommends software, helps improve startup performance, and fixes common support issues. |  
|[Configure Take a Test app for students](../configuration/education-settings-configure.md)| Configure the Take a Test app for students taking tests or exams on enrolled devices. |  
|[Configure eSim cellular profile](../configuration/esim-device-configuration.md)| You can configure eSIM for ESIM-capable devices, such as the Surface LTE Pro, to connect to the internet over a cellular data connection. This configuration is ideal for global travelers who need to stay connected and flexible while traveling, and eliminates the need for a SIM card. | 


## Step 6: Set up secure authentication methods   
Set up authentication methods in Intune to ensure that only authorized people access your internal resources. Intune supports multi-factor authentication, certificates, and derived credentials. Certificates can also be used for signing and encryption of email using S/MIME. 

| Task | Detail | 
| ---- | ------ | 
|[Require multi-factor authentication (MFA)](../enrollment/multi-factor-authentication.md)| Require people to supply two forms of credentials at time of device enrollment. This policy works in conjunction with Azure AD conditional access policies.| 
|[Create a trusted certificate profile](../protect/certificates-trusted-root.md)|Create and deploy a trusted certificate profile before you create a SCEP, PKCS, or PKCS imported certificate profile. The trusted certificate profile deploys the trusted root certificate to devices and users using SCEP, PKCS, and PKCS imported certificates. |
|[Use SCEP certificates with Intune ](../protect/certificates-scep-configure.md)| Learn what’s needed to use SCEP certificates with Intune, and configure the required infrastructure. Then you can [create a SCEP certificate profile](../protect/certificates-profile-scep.md) or [set up a third-party certification authority with SCEP](../protect/certificate-authority-add-scep-overview.md).|  
|[Use PKCS certificates with Intune](../protect/certificates-pfx-configure.md)|Configure required infrastructure (such as on-premises certificate connectors), export a PKCS certificate, and add the certificate to an Intune device configuration profile. | 
|[Use imported PKCS certificates with Intune](../protect/certificates-imported-pfx-configure.md)|Set up imported PKCS certificates, which enable you to [set up and use S/MIME to encrypt email](../protect/certificates-s-mime-encryption-sign.md). 
|[Set up a derived credentials issuer](../protect/derived-credentials.md)| Provision Windows devices with certificates that are derived from user smart cards.  
|[Integrate Windows Hello for Business with Microsoft Intune](../protect/windows-hello.md)| Create a Windows Hello for Business policy to enable or disable Windows Hello for Business during device enrollment. Hello for Business is an alternative sign-in method that uses Active Directory or an Azure Active Directory account to replace a password, smart card, or a virtual smart card. | 

## Step 7: Deploy apps  

As you set up apps and app policies, think about your organization's requirements, such as the platforms you'll support, the tasks people do, the type of apps they need to complete those tasks, and who needs them. You can use Intune to manage the whole device (including apps) or use Intune to manage apps only.  

| Task | Detail | 
| ---- | ------ | 
|[Add line-of-business apps ](../apps/lob-apps-windows.md)|Add macOS line-of-business (LOB) apps to Intune and assign to groups.| 
|[Add Microsoft Edge](../apps/apps-windows-edge.md) | Add and assign Microsoft Edge for Windows. | 
|[Add Intune Company Portal app ](../apps/store-apps-company-portal-download.md)|Add and assign the Intune Company Portal app as a required app for personal devices.    | 
|[Add Intune Company Portal app for Autopilot ](../apps/store-apps-company-portal-autopilot.md)|Add the Company Portal app to devices provisioned by Windows Autopilot. |
|[Add Microsoft 365 apps](../apps/apps-add-office365.md) |Add Microsoft 365 Apps for enterprise. | 
|[Assign apps to groups ](../apps/apps-deploy.md)|After you add apps to Intune, assign them to users and devices.|
|[Include and exclude app assignments ](../apps/apps-inc-exl-assignments.md)|Control access and availability to an app by including and excluding selected groups from assignment.| 
|[Use PowerShell scripts](../apps/intune-management-extension.md)|Upload PowerShell scripts to extend Windows device management capabilities in Intune and make it easier to move to modern management.| 

## Step 8: Enroll devices  

During enrollment, the device is registered with Azure AD and evaluated for compliance. For information about each enrollment method and how to choose one that's right for your organization, see [Windows device enrollment guide for Microsoft Intune](../fundamentals/deployment-guide-platform-windows.md).   

| Task | Detail |
| ---- | ------ |
|[Enable MDM automatic enrollment](../enrollment/windows-enroll.md)|Simplify enrollment by enabling automatic enrollment, which automatically enrolls devices in Intune that join or register with your Azure AD. Automatic enrollment simplifies Windows Autopilot deployment, BYOD enrollment, enrollment using Group Policy, and bulk enrollment via a provisioning package.  |  
|[Enable automatic discovery of MDM server](../enrollment/windows-enrollment-create-cname.md)| If you don't have Azure AD Premium, we recommend creating a CNAME record type for Intune enrollment servers. The CNAME record redirects enrollment requests to the right server so that enrolling users don't have to type the server name in manually. |
|[Tutorial: Use Windows Autopilot to enroll devices](../enrollment/tutorial-use-autopilot-enroll-devices.md)| Simplify device provisioning for you and your users by setting up Microsoft Intune device enrollment to occur automatically during [Windows Autopilot](../../autopilot/windows-autopilot.md). | 
|[Enroll devices using Group Policy](/windows/client-management/enroll-a-windows-10-device-automatically-using-group-policy)| Trigger automatic enrollment into Intune using a group policy.   | 
|[Bulk enroll devices](../enrollment/windows-bulk-enroll.md)| Create a provisioning package in Windows Configuration Designer that both joins large numbers of new Windows devices to Azure AD and enrolls them in Intune. |  
|[Set up the enrollment status page (ESP)](../enrollment/windows-enrollment-status.md)| Create an enrollment status page profile with custom settings to guide users through device setup and enrollment.   |  
|[Change device ownership label](../enrollment/corporate-identifiers-add.md#change-device-ownership)|After a device has been enrolled, you can change its ownership label in Intune to corporate-owned or personal-owned. This adjustment changes the way you manage the device, and can enable more management and identification capabilities in Intune, or limit them.|   
|[Configure proxy for Intune Active Directory Connector](../enrollment/autopilot-hybrid-connector-proxy.md)| Configure the Intune Connector for Active Directory to work with your existing outbound proxy servers.   | 
|[Troubleshoot enrollment problems](/troubleshoot/mem/intune/troubleshoot-device-enrollment-in-intune)|Troubleshoot and find resolutions to problems that occur during enrollment. |


## Step 9: Run remote actions  

After devices are set up, you can use supported remote actions to manage and troubleshoot devices from a distance. The following articles introduce you to the remote actions for Windows. If an action is absent or disabled in the portal, then it isn't supported for Windows.  

| Task | Detail | 
| ---- | ------ | 
|[Take remote action on devices](../remote-actions/device-management.md)|Learn how to drill down and remotely manage and troubleshoot individual devices in Intune. This article lists all remote actions available in Intune and links to those procedures.   |
|[Use TeamViewer to remotely administer Intune devices](../remote-actions/teamviewer-support.md)|Configure TeamViewer within Intune, and learn how to remotely administer a device.  |  
|[Use security tasks to view threats and vulnerabilities](../protect/atp-manage-vulnerabilities.md)|Use Intune to remediate endpoint weakness identified by Microsoft Defender for Endpoint. Before you can work with security tasks, you must integrate Microsoft Defender for Endpoint with Intune. |  
|[Use organizational messages](../remote-actions/organizational-messages-overview.md)|Use organizational messages to send important messages to employees on Intune-managed devices running Windows 11. Organizational messages can be used to communicate in remote and hybrid work scenarios.|

## Step 10: Help employees and students   

The resources in this section are in the Microsoft Intune User Help documentation. This documentation is meant for employees, students, and other Intune-licensed device users who are enrolling a personal or company-provided device. Documentation links are available throughout the Intune Company Portal app and point to information about: 

* Enrollment methods, with walkthroughs of how to enroll 
* Company Portal settings and features  
* How to unenroll and remove stored data
* Updating device settings for compliance requirements 
* How to report app problems    

>[!TIP]
> Make your organization's operating system requirements and device password requirements easy to find on your website or in an onboarding email so that employees don't have to delay enrollment to seek out that information. 

| Task | Detail | 
| ---- | ------ | 
|[Install Intune Company Portal app for Windows](../user-help/sign-in-to-the-company-portal.md)| Learn where to get the Company Portal app and how to sign in. | 
|[Update Company Portal app](../user-help/install-a-new-version-of-the-company-portal-app.md)| This article describes how to install the latest version of Company Portal and how to turn on automatic app updates. | 
|[Enroll a device](../user-help/enroll-windows-10-device.md)| This article describes how to enroll personal devices running Windows 10 or Windows 11. | 
|[Unenroll a device](../user-help/unenroll-your-device-from-intune-windows.md)| This article describes how to unenroll a device from Intune and delete the stored cache and logs for Company Portal. | 

## Next steps  

* For an overview of the Microsoft Intune admin center and how to navigate it, see [Tutorial: Walkthrough the Microsoft Intune admin center](tutorial-walkthrough-endpoint-manager.md). Tutorials are 100 – 200 level content for people new to Intune or a specific scenario.   

* For other versions of this guide, see:   

    * [Deployment guide: Manage Android devices in Microsoft Intune](deployment-guide-platform-android.md)  
    * [Deployment guide: Manage iOS devices in Microsoft Intune](deployment-guide-platform-ios-ipados.md)
    * [Deployment guide: Manage macOS devices in Microsoft Intune](deployment-guide-platform-macos.md)  
    * [Deployment guide: Managed Linux devices in Microsoft Intune](deployment-guide-platform-linux.md)