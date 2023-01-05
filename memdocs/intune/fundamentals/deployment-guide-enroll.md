---
# required metadata

title: Step 5 – Enroll devices in Microsoft Intune 
description: Enroll Android, Android Enterprise, iOS, iPadOS, Linux, macOS, and Windows devices in Intune. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 1/05/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: 
  - M365-identity-device-management
  - highpri
  - highseo
---

# Step 5 – Enroll devices in Microsoft Intune

In the final phase of deployment, devices are registered or joined in Azure Active Directory (Azure AD), enrolled in Microsoft Intune, and checked for compliance. 

Before enrollment begins, [a device identity](/azure/active-directory/devices/overview) needs to be established in your org's Azure AD. This step grants the user of the device single sign-on (SSO) access to cloud-based work apps and other resources. Registration in Azure AD is a required step for Intune management. 

* *Azure AD registration* is the device identity option available for personal and corporate-owned mobile devices. Users on these devices *sign in to work resources like apps and web browsers* using their Azure AD work account. 
* *Azure AD joined* is the device identity option available for corporate-owned Windows 10/11 devices utilizing co-management options. Users on these devices *sign in to the device* using their Azure AD work account.   

During enrollment, Microsoft Intune installs a mobile device management (MDM) certificate on the device, which enables Intune to enforce policies and profiles you created, such as:   

* Device enrollment restrictions
* Configuration profiles
* Compliance policies 
* Terms and conditions 
* Multifactor authentication 

After enrollment, the device user is immediately notified of your compliance policies, and must update their device settings to meet requirements. This is the last step before the device is granted access to work resources.  

## Create pilot groups  

If this is your first time deploying enrollment profiles with Intune, or you're trying a new configuration, start small and use a staged approach. Assign the enrollment profile to a pilot or test group. After initial testing, add more users to the pilot group. If everything is going well, assign the enrollment profile to more pilot groups.  

For more information and suggestions, see the [Planning guide: Step 5 - Create a rollout plan](intune-planning-guide.md#step-5---create-a-rollout-plan).  

## Pre-enrollment configurations  
This section describes the general enrollment features and profiles available in Microsoft Intune. Configure these settings prior to enrollment.   

### Unenroll and reset existing devices  

If devices are currently enrolled in another MDM provider, unenroll the devices from the existing MDM provider before enrolling them in Intune. The following table shows the devices that require a factory reset before enrolling in Intune. 

-----
| Platform | Factory reset required? |
| --- | --- |
| Android Enterprise personally owned devices with a work profile (BYOD) | No |
| Android Enterprise corporate-owned work profile (COPE) | Yes |
| Android Enterprise fully managed (COBO) | Yes |
| Android Enterprise dedicated devices (COSU) | Yes |
| Android device administrator (DA) | No |
| iOS/iPadOS | Yes |
| Linux | No |
| macOS | Yes |
| Windows | No |

-----  

Devices that don't require a reset begin installing Intune profiles as soon as they enroll. Previously configured settings may remain on devices if you don't change them in Intune prior to enrollment.   

### Add device enrollment managers     
We recommend utilizing device enrollment managers when you need to enroll and prepare a large number of devices for distribution. A DEM account can enroll and manage up to 1,000 devices, while a standard non-admin account can only enroll 15 devices. A device enrollment manager (DEM) is a non-administrator Azure AD user who can:

* Enroll up to 1000 corporate-owned devices in Intune
* Sign in to Intune Company Portal to get company apps
* Configure access to corporate data by deploying role-specific apps to devices  

For more information and limitations, see [Add device enrollment managers](../enrollment/device-enrollment-manager-enroll.md).  

### Create device enrollment restrictions  
Use this feature in the Microsoft Endpoint Manager admin center to restrict certain devices from enrolling in Intune. There are two types of device enrollment restrictions you can configure in Microsoft Intune:

* Device platform restrictions: Restrict devices based on device platform, version, manufacturer, or ownership type.
* Device limit restrictions: Restrict the number of devices a user can enroll in Intune. 

Enrollment restrictions aren't available for Linux and some Windows enrollment scenarios. When you're setting up restrictions for Android Enterprise personal devices, we recommend leveraging our Android security configuration framework. It includes the device restrictions needed for basic security (level 1), which is the minimum security configuration we recommend having on personal devices, and high security (level 3), which is for devices used by specific users or groups who are uniquely high risk.   

For more information, see:  

* [What are enrollment restrictions?](../enrollment/enrollment-restrictions-set.md) 
* [Recommended device restrictions](../enrollment/device-enrollment-restrictions.md)

### Create terms and conditions policy    
Use an Intune terms and conditions policy to disclose legal disclaimers and compliance requirements to device users before enrollment. This policy requires a person to accept your org's terms and conditions before they enroll their device or access protected resources. The terms and conditions are shown to targeted users in the Intune Company Portal app. 

For more control over where your terms appear, configure Azure Active Directory terms of use. These terms are shown to users when they sign in to targeted apps and resources and offer more granular settings than Intune terms and conditions.   

For more information, see [Terms and conditions for user access](../enrollment/terms-and-conditions-create.md).  

### Require multifactor authentication  
Require multifactor authentication (MFA) during Microsoft Intune enrollment. This feature is available for all platforms except Linux. 

If you require MFA, people wanting to enroll devices must authenticate with a second device and two forms of credentials. This is a one-time conditional step, and ensures that the person on the device is who they say they are. For this feature to take effect, the user must be assigned an Azure AD Premium license. 

For more information, see [Require multifactor authentication for Intune device enrollments](../enrollment/multi-factor-authentication.md).   

### Categorize devices into groups  
Device categories make it easier to manage and group devices in Microsoft Intune by job title, department, or role. Create a category, such as *nursing* or *marketing*, and Intune will automatically add all devices that fall within that category to the corresponding device group in Intune. This feature is available for all platforms except Linux.  

For more information, see [Categorize devices into groups](../enrollment/device-group-mapping.md).  

## Enrollment for Android devices  
You can enroll personal or corporate-owned Android devices in Intune. We recommend the Android Enterprise enrollment methods for personal and corporate-owned devices that have Google Mobile Services. For corporate-owned devices that don't have Google Mobile Services, and are built from the Android Open Source Project (AOSP), use the AOSP enrollment methods.   

### Prerequisites   
[Connect Intune to your managed Google Play account](../enrollment/connect-intune-android-enterprise.md) to enable access to Android Enterprise device management features and managed Google Play. The connection is required for all Android Enterprise management options, including:  

* Android Enterprise personally owned work profile  
* Android Enterprise corporate-owned work profile  
* Android Enterprise fully managed  
* Android Enterprise dedicated devices  

### Android enrollment options      
These are the enrollment options available for Android devices in Intune. 

You can enroll Android Enterprise devices as:   
* [Personally owned devices with a work profile](../enrollment/android-work-profile-enroll.md): Enroll personal devices in bring-your-own-device (BYOD) scenarios. This method creates a separate work profile on the personal device so that a person can switch between their personal apps and work apps easily and securely. The device owner enrolls their device through the Intune Company Portal app. As an admin, you can manage the apps and data in the work profile. This method aligns with the *Android Enterprise personally owned work profile* solution.    
* [Corporate-owned devices with a work profile](../enrollment/android-corporate-owned-work-profile-enroll.md): Enroll corporate-owned devices that are also approved for personal use. This method creates a separate work profile on the device so that the user can switch between their personal apps and work apps easily and securely. The device user enrolls the device through the Microsoft Intune app. As an admin, you can manage the apps and data in the work profile.  This method aligns with the *Android Enterprise corporate-owned work profile* solution.   
* [Corporate-owned, fully managed devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md): Enroll corporate-owned devices exclusively for work and not personal use. There's one user associated with the device, which they enroll via user-associated devices. You can manage the entire device and enforce policy controls unavailable with the Android Enterprise work profile method. This method aligns with the *Android Enterprise fully managed* solution.   
* [Corporate-owned, dedicated devices](../enrollment/android-kiosk-enroll.md): Enroll corporate-owned, single use or kiosk devices used for things like digital signage, ticket printing, or inventory management. With Intune, you can limit use on these devices to select apps and web links, and prevent people from using the device outside of the intended scope. This method aligns with the *Android Enterprise dedicated devices* solution.   

You can enroll AOSP devices as:    
* [Corporate-owned, userless devices](../enrollment/android-aosp-corporate-owned-userless-enroll.md): Enroll corporate-owned, userless devices that are built from AOSP and absent of Google Mobile services. These devices don't have a user associated with them and are intended to be shared, like in a library or lab.  
* [Corporate-owned, user associated devices](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md): Enroll corporate-owned, user-associated devices that are built from AOSP and absent of Google Mobile services. These devices are associated with a single user and intended to be exclusively for work use.  

We recommend using zero-touch enrollment for bulk enrollments and to simplify enrollment for remote workers:  
* [Zero-touch enrollment](../enrollment/android-dedicated-devices-fully-managed-enroll.md#enroll-by-using-google-zero-touch): Prepare corporate-owned devices ahead of time so that they automatically provision and enroll as fully manged devices when users turn them on. To use Android zero-touch enrollment, link your zero-touch account to Intune in the Microsoft Endpoint Manager admin center. Zero-touch enrollment must be supported on your devices and affiliated with a supplier that is part of the Android zero-touch enrollment service.  

> [!TIP]
> Android Enterprise device management capabilities supersede Android device administrator. We only recommend the Android device administrator enrollment method in these scenarios:  
> * For Microsoft Teams certified Android devices.
> * When the device is in an area where Android Enterprise is unavailable.  
> * When devices are incapable of integrating with Google Mobile Services, and the AOSP enrollment options won't work with them. For more information about using Android device administrator when Google Mobile Services is unavailable, see [How to use Intune in environments without Google Mobile Services](../apps/manage-without-gms.md).  

## Enrollment for Apple devices 
This section describes the enrollment options available for iOS/iPadOS and Mac devices in Intune.  

### Prerequisites  
* [Get an Apple MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md) from the Apple Push Certificates Portal and upload it to the admin center. Without the certificate, Intune enrollment features appear unavailable and you can't enroll any devices. 

* Get an Apple ADE token for [iOS/iPadOS](../enrollment/device-enrollment-program-enroll-ios.md#get-an-apple-automated-device-enrollment-token) or [Mac](../enrollment/device-enrollment-program-enroll-macos.md#get-an-apple-ade-token): If you plan to enroll devices via Apple automated device enrollment, download an enrollment token (.p7m) file from Apple. This token allows Intune, Apple Business Manager, and Apple School Manager to sync with each other about the devices that your organization owns.  

### iOS/iPadOS enrollment options   
These are the enrollment options available for iOS/iPadOS devices in Intune.     

* [Apple automated device enrollment](../enrollment/device-enrollment-program-enroll-ios.md): Enroll new or wiped devices purchased from Apple Business Manager or Apple School Manager. This automated enrollment method for corporate-owned devices applies your organization's settings from Apple Business Manager and Apple School Manager, supports supervision mode, and enrolls devices without you needing to touch them.  When people turn on their devices, Apple Setup Assistant guides them through setup and enrollment. 

   This method requires that you pick an enrollment authentication method before creating the enrollment profile; we recommend selecting a modern authentication option such as Intune Company Portal, Setup Assistant with modern authentication, or Just in Time Registration for Setup Assistant. 

* [Enrollment with Apple Configurator](): Manually enroll new or existing devices via Apple Configurator. This method is ideal for bulk enrollments and when you don't have access to Apple School Manager, Apple Business Manager, or when you require a wired network connection. You must have physical access to the devices because this method requires you to connect and configure devices on a Mac. There are two different paths you can take:  

   * Setup Assistant enrollment: This method wipes the device and prepares it for enrollment in Apple Configurator. When users turn on their devices, Setup Assistant begins and devices enroll in Intune. This method requires you to have access to the device serial numbers because you need to input them into the admin center. 
   * Direct enrollment: This method lets you enroll the device prior to distribution, and doesn't wipe the device. Devices enrolled this way aren't associated with a user so we recommend this option for shared or kiosk devices. You don't need to have the serial numbers for this method.  

 * [User and device enrollment](../enrollment/ios-user-enrollment.md): Enable enrollment for personal-owned devices in BYOD scenarios. This method gives device owners the option to secure the entire device or just work-related apps and data. Enrollment takes place in the Company Portal app. This enrollment profile is in public preview in the admin center and is called **Enrollment types (preview)**.  

 ### macOS enrollment options  
These are the enrollment options available for Mac devices in Intune.   

 * [Device enrollment](../enrollment/macos-enroll.md): Enable enrollment for personal-owned Macs in BYOD scenarios. Licensed users can initialize enrollment on their personal devices by signing into the Company Portal app. 

* [Apple automated device enrollment](../enrollment/device-enrollment-program-enroll-macos.md): Enroll new or wiped Macs purchased from Apple Business Manager or Apple School Manager. This automated enrollment method for corporate-owned devices applies your organization's settings from Apple Business Manager and Apple School Manager, supports supervision mode, and enrolls devices without you needing to touch them.  When people turn on their devices, Apple Setup Assistant guides them through setup and enrollment.   

 * [Direct enrollment](../enrollment/device-enrollment-direct-enroll-macos.md): This method lets you enroll a corporate-owned Mac prior to distribution, and doesn't wipe the device. Devices enrolled this way aren't associated with a user so we recommend this option for shared or kiosk devices. You don't need to have the serial numbers for this method, but you must have physical access to the device to transfer and install the management profile on it. This method is similar to the Apple Configurator direct enrollment option for iOS/iPadOS but doesn't utilize Apple Configurator as much, so be sure to follow the instructions for macOS.   

## Enrollment for Windows    
This section describes the enrollment methods and configurations available for Windows 10/11 personal and corporate-owned devices. Microsoft Intune enrollment is supported in cloud environments and with co-management in on-premises environments.

As a reminder, devices must be registered or joined to Azure AD to enroll in Intune. The following table shows our recommended management strategy for each device identity option. 
 
 | Identity | Management | Provisioning| Cloud modernization   
 | --- | --- | ---| --- |
 | Active Directory domain services | Configuration Manager + tenant attach |Operating system deployment |Low|
 | Hybrid Azure AD joined | Tenant attach + co-management |Operating system Deployment | Medium|
 | Azure Active Directory | Co-management or Microsoft Intune |Windows Autopilot | High    

### Windows enrollment options  

These are the enrollment scenarios supported in Intune for devices running Windows 10/11.  

> [!IMPORTANT]
> Make enrollment in Intune easier for employees and students by [enabling automatic enrollment](../enrollment/windows-enroll.md#enable-windows-automatic-enrollment) in the admin center. Where supported, it automatically enrolls the device in Microsoft Intune after the Intune-licensed user registers or joins the device to Azure AD. 

* Bring your own device (BYOD):  Automatic enrollment is available for personal-owned devices in BYOD scenarios. Intune-licensed device users initialize registration and enrollment by signing into the Company Portal app. We recommend enabling automatic enrollment so that your employees only have to enter their credentials once to start enrollment.  

* Azure Active Directory Join: Automatic enrollment is supported on devices that are procured by you or an employee for work use. Enrollment occurs during the out-of-box-experience, after the user signs in with their work account and joins Azure AD.  This method is useful when you don't have access to the device, such as in remote work environments. When these devices enroll, their device ownership changes to *corporate-owned*, and you get access to management features that aren't available for personal ownership. 

* [Windows Autopilot out-of-box-experience](): Automatic enrollment is supported during the user-driven or self-deploying Windows Autopilot out-of-box-experience (OOBE). This method is for corporate-owned desktops, laptops, and kiosks. Device users get desktop access after required software and policies are installed. An Azure AD Premium license is required for automatic enrollment.   

* [Windows Autopilot for Hybrid Azure AD join](/autopilot/windows-autopilot-hybrid): Automatic enrollment is supported with Windows Autopilot for hybrid Azure AD-joined devices. During the Windows Autopilot out-of-box-experience, the Intune connector for Active Directory enables devices in Active Directory domain services to join to Azure AD, and then automatically enroll in Intune. This method requires you to install the Intune connector for Active Directory on an on-premises server and register devices in Windows Autopilot.  We recommend this method for on-premises environments that use Active Directory domain services and can't currently move their identities to Azure AD. 

* [Co-management with Configuration Manager](/configmgr/comanage/autopilot-enrollment): Enable co-management settings in Intune to use Intune features on devices you manage with Configuration Manager. Co-management gives you the option to use both Intune and Configuration Manager features.  For example, you can manage devices with compliance policies and device configuration workloads in Intune, and utilize Configuration Manager for all other features, like app deployment and security policies.   

* [Bulk enrollment](../enrollment/windows-bulk-enroll.md):  Set up and enroll a large number of devices in Azure AD and Intune without needing to reimage them. This process requires you to create a provisioning package using the Windows Configuration Designer app, and then apply the package during the OOBE, or run it on the device in the Settings app.   

There are other enrollment options in Intune to help improve or simplify the Windows enrollment experience for you and your employees:     

* [CNAME validation](../enrollment/windows-enroll.md#simplify-windows-enrollment-without-azure-ad-premium): Create a domain name server (DNS) alias (CNAME record type) that redirects enrollment requests to Intune servers, so that people enrolling their devices don't have to manually enter the server address. This option simplifies enrollment in the absence of Azure AD Premium.   
* [Enrollment Status Page](../enrollment/windows-enrollment-status.md): Enable the Enrollment Status Page so that people going through device setup can view and track installation progress.  

To access these options in the admin center, go to **Devices** > **Windows** > **Windows enrollment**. 

## Report and troubleshoot  
Track [incomplete and abandoned user enrollments](../enrollment/enrollment-report-company-portal-abandon.md). This Microsoft Intune report tells you where where in the Company Portal users failed to complete the enrollment process.  

For troubleshooting docs, see [Troubleshoot device enrollment](/troubleshoot/mem/intune/troubleshoot-device-enrollment-in-intune).    

## Additional resources 
Additional resources for enrollment are available throughout the Microsoft Intune documentation, and include visual comparisons, how-to steps, tips, and best practices.  

There's an enrollment guide for every platform. 

- [Application management without enrollment (MAM-WE)](deployment-guide-enrollment-mamwe.md)
- [Android device management](deployment-guide-enrollment-android.md)
- [iOS/iPadOS device management](deployment-guide-enrollment-ios-ipados.md)
- [Linux device management](deployment-guide-enrollment-linux.md)
- [macOS device management](deployment-guide-enrollment-macos.md)
- [Windows device management](deployment-guide-enrollment-windows.md)

Download our visual guide to compare enrollment options and capabilities.   

[![A visual representation of Intune enrollment options by platform](./media/deployment-guide-enrollment/msft-intune-enrollment-options-thumb-landscape.png)](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) <br/> [Download PDF version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.pdf) | [Download Visio version](https://download.microsoft.com/download/e/6/2/e6233fdd-a956-4f77-93a5-1aa254ee2917/msft-intune-enrollment-options.vsdx)  