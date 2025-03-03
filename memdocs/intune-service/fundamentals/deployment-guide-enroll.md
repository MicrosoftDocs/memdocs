---
# required metadata

title: Step 5 – Enroll devices in Microsoft Intune 
description: Enroll Android, Android Enterprise, iOS, iPadOS, Linux, macOS, and Windows devices in Intune. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 4/3/2024
ms.topic: how-to
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
- tier1
---

# Step 5 – Enroll devices in Microsoft Intune

In the final phase of deployment, devices are registered or joined in Microsoft Entra ID, enrolled in Microsoft Intune, and checked for compliance.

:::image type="content" source="./media/deployment-guide-enroll/deployment-plan-enroll.png" alt-text="Diagram that shows getting started with Microsoft Intune with step 5, which is enrolling devices to be managed by Intune.":::

During enrollment, Microsoft Intune installs a mobile device management (MDM) certificate on the device, which enables Intune to enforce enrollment profiles, enrollment restrictions, and the policies and profiles you created earlier in this guide.  

This article describes:

* How-to prepare enrollment in Microsoft Intune for corporate-owned and user-owned devices. 
* Enrollment options for each OS platform.  
* Post-enrollment monitoring, troubleshooting, and resources.  

## Getting started       
If this is your first time deploying enrollment profiles with Intune, or you're trying a new configuration, start small and use a staged approach. Assign the enrollment profile to a pilot or test group. After initial testing, add more users to the pilot group. If everything is going well, assign the enrollment profile to more pilot groups. For more information and suggestions, see the [Planning guide: Step 5 - Create a rollout plan](intune-planning-guide.md#step-5---create-a-rollout-plan).  

Registration in Microsoft Entra ID is a required step for Intune management. Before a device can enroll in Intune, the user of the device must authenticate and establish a device identity in your org's Microsoft Entra ID. This step grants the user single sign-on access to cloud-based work apps and other resources. It's important to know which identity option you're utilizing because it determines the enrollment methods you can use, and also determines the sign-in experience for the device user. Identity options include:       
   * *Microsoft Entra registration* is the device identity option available for personal and corporate-owned mobile devices. Users on these devices authenticate by signing in to work resources, like apps and web browsers, using their Microsoft Entra ID work account. 
   * *Microsoft Entra joined* is the device identity option available for corporate-owned Windows 10/11 devices utilizing co-management options. Users on these devices authenticate by signing in to the device using their Microsoft Entra ID work account.  

## Pre-enrollment configurations  
Prepare devices for enrollment by configuring enrollment features, such as enrollment restrictions, device categorization, and device enrollment managers. These configurations help improve and simplify the enrollment experience for you and device users, and help you stay organized in the admin center.  Configure them before you create the enrollment profile. 

Setting availability varies by OS platform.       

### Unenroll and reset existing devices  

If devices are currently enrolled in another MDM provider, unenroll the devices from the existing MDM provider before enrolling them in Intune. The following table shows the devices that require a factory reset before enrolling in Intune.  

| Platform | Factory reset required? |
| --- | --- |
| Android Enterprise personally owned devices with a work profile (BYOD) | No |
| Android Enterprise corporate-owned work profile (COPE) | Yes |
| Android Enterprise fully managed (COBO) | Yes |
| Android Enterprise dedicated devices (COSU) | Yes |
| Android device administrator (DA) | No |
| iOS/iPadOS (BYOD) | No |
| iOS/iPadOS (ADE) | Yes |
| Linux | No |
| macOS (BYOD) | No |
| macOS (ADE) | Yes |
| Windows | No |

-----  

Devices that don't require a reset begin installing Intune profiles as soon as they enroll. Previously configured settings may remain on devices if you don't change them in Intune prior to enrollment.   

### Add device enrollment managers     
We recommend utilizing device enrollment managers when you need to enroll and prepare a large number of devices for distribution. A device enrollment manager account can enroll and manage up to 1,000 devices, while a standard non-admin account can only enroll 15 devices. A device enrollment manager is a non-administrator Microsoft Entra user who can:

* Enroll up to 1000 corporate-owned devices in Intune
* Sign in to Intune Company Portal to get company apps
* Configure access to corporate data by deploying role-specific apps to devices  

Some enrollment methods, such as Apple automated device enrollment, aren't compatible with the device enrollment manager account, so be sure that the method you choose is supported before you begin setup. 

For more information and limitations, see [Add device enrollment managers](../enrollment/device-enrollment-manager-enroll.md).  

### Create device enrollment restrictions  
Use this feature in the Microsoft Intune admin center to restrict certain devices from enrolling in Intune. There are two types of device enrollment restrictions you can configure in Microsoft Intune:

* Device platform restrictions: Restrict devices based on device platform, version, manufacturer, or ownership type.
* Device limit restrictions: Restrict the number of devices a user can enroll in Intune. 

Enrollment restrictions aren't available for Linux and some Windows enrollment scenarios. For more information, see [Overview of enrollment restrictions ](../enrollment/enrollment-restrictions-set.md).  <!-- Removing until PM updates framework docs. When you're setting up restrictions for Android Enterprise personal devices, we recommend leveraging our Android security configuration framework. It includes the device restrictions needed for basic security (level 1), which is the minimum security configuration we recommend having on personal devices, and high security (level 3), which is for devices used by specific users or groups who are uniquely high risk. -->     

### Create terms and conditions policy    
You can use an Intune terms and conditions policy to disclose legal disclaimers and compliance requirements to device users before enrollment. This policy requires the devices user to accept your org's terms and conditions before they enroll their device or access protected resources. The terms and conditions are shown to targeted users in the Intune Company Portal app. 

If you're looking for more control, including where the terms appear, consider configuring *Microsoft Entra terms of use*. Microsoft Entra terms are shown to users when they sign in to targeted apps and resources and offer more granular settings than Intune terms and conditions.   

For more information, see [Terms and conditions for user access](../enrollment/terms-and-conditions-create.md).  

### Require multifactor authentication  
Require users to authenticate via multi-factor authentication (MFA) during enrollment. If you require MFA, people wanting to enroll devices must authenticate with a second device and two forms of credentials before they can enroll their device. This is a one-time conditional step, and ensures that the person on the device is who they say they are.  You can enable this behavior for all platforms except Linux by using a Conditional Access policy with an MFA policy. Microsoft Entra ID P1 or P2 is required.  

For more information, see [Require multifactor authentication for Intune device enrollments](../enrollment/multi-factor-authentication.md).   

### Categorize devices into groups  
Create a device category in Intune, such as *nursing* or *marketing*, and Intune will automatically add all devices that fall within that category to the corresponding device group in Intune. 

This feature is available for all platforms except Linux. For more information, see [Categorize devices into groups](../enrollment/device-group-mapping.md).  

## Enrollment for Android devices  
You can enroll personal or corporate-owned Android devices in Intune. We recommend Android Enterprise enrollment solutions for personal and corporate-owned devices that use Google Mobile Services. For corporate-owned devices that don't have Google Mobile Services and are built from the Android Open Source Project (AOSP), use the AOSP enrollment methods. 

### Prerequisites 

 [Connect Intune to your managed Google Play account](../enrollment/connect-intune-android-enterprise.md). The connection is required for all Android Enterprise management options, including:  

* Android Enterprise personally owned work profile  
* Android Enterprise corporate-owned work profile  
* Android Enterprise fully managed  
* Android Enterprise dedicated  

### Android enrollment methods  

The following tabs describe the Intune-supported Android and AOSP enrollment options.  

# [Corporate owned](#tab/work-profile)  

* [Corporate-owned devices with a work profile](../enrollment/android-corporate-owned-work-profile-enroll.md): Enroll corporate-owned devices that are also approved for personal use. This method creates a separate work profile on the device so that the user can switch between their personal apps and work apps easily and securely. The device user enrolls the device through the Microsoft Intune app. As an admin, you can manage the apps and data in the work profile.  This method aligns with the *Android Enterprise corporate-owned work profile* management solution.  
 
* [Fully managed](../enrollment/android-dedicated-devices-fully-managed-enroll.md): Enroll corporate-owned devices exclusively for work and not personal use. There's one user associated with the enrolled device. You can manage the entire device and enforce policy controls not available with the Android Enterprise work profile method. This method aligns with the *Android Enterprise fully managed* management solution.  

* [Dedicated device](../enrollment/android-kiosk-enroll.md): Enroll corporate-owned, single use or kiosk devices used for things like digital signage, ticket printing, or inventory management. With this method, you can limit the apps and web links available on the device, and prevent people from using the device outside of the intended scope. This method aligns with the *Android Enterprise dedicated devices* management solution.    

* [Corporate-owned, userless devices](../enrollment/android-aosp-corporate-owned-userless-enroll.md): Enroll devices that are built from the Android Open Source Project (AOSP) and absent of Google Mobile services as *corporate-owned, userless devices*. These devices don't have a user associated with them and are intended to be shared, like in a library or lab.  
* [Corporate-owned, user associated devices](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md): Enroll devices that are built from AOSP and absent of Google Mobile services as *corporate-owned, user-associated devices*. These devices are associated with a single user and intended to be exclusively for work use.  

* [Zero-touch enrollment](../enrollment/android-dedicated-devices-fully-managed-enroll.md#enroll-by-using-google-zero-touch): We recommend using zero-touch enrollment for bulk enrollments and to simplify enrollment for remote workers. This method lets you prepare corporate-owned devices ahead of time so that they automatically provision and enroll as fully managed devices when users turn them on.     

# [User owned](#tab/user-owned-android)  

[Personally owned devices with a work profile](../enrollment/android-work-profile-enroll.md): Support enrollment for personal devices in BYOD scenarios. During enrollment, a separate work profile is created on the device so that people can switch between their personal apps and work apps easily and securely. The device owner enrolls their device through the Intune Company Portal app. As an admin, you can manage the apps and data in the work profile. This method aligns with the *Android Enterprise work profile for personally owned devices* management solution.    


---

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)] 

## Enrollment for Apple devices 
This section describes the enrollment options available for iOS/iPadOS and Mac devices in Intune. 

### Prerequisites  
Complete the following prerequisites before you create the enrollment profile for Apple devices:  

* Upload an Apple MDM push certificate to Intune. For more information, see [Get MDM push certificate](../enrollment/apple-mdm-push-certificate-get.md).  
* Get an Apple enrollment program token  if you plan to enroll devices via Apple automated device enrollment.    For more information, see: 
  * [Get Apple enrollment program token for iOS/iPadOS](../enrollment/device-enrollment-program-enroll-ios.md#get-an-apple-automated-device-enrollment-token)
  * [Get Apple enrollment program token for macOS](../enrollment/device-enrollment-program-enroll-macos.md#create-enrollment-program-token)

### Apple enrollment solutions  
The following table describes the enrollment solutions for devices running iOS/iPadOS and macOS.     

# [Corporate owned](#tab/corporate-owned-apple) 
* Automated device enrollment [for iOS/iPadOS](../enrollment/device-enrollment-program-enroll-ios.md) and [for Mac devices](../enrollment/device-enrollment-program-enroll-macos.md): 
Enroll new or wiped devices purchased from Apple Business Manager or Apple School Manager with automated device enrollment. This automated enrollment method for corporate-owned devices applies your organization's settings from Apple Business Manager and Apple School Manager, supports supervision mode, and enrolls devices without you needing to touch them.  When people turn on their devices, Apple Setup Assistant guides them through setup and enrollment.  

* Apple Configurator [for iOS/iPadOS](../enrollment/apple-configurator-enroll-ios.md) and [for Mac devices](../enrollment/device-enrollment-direct-enroll-macos.md): Manually enroll new or existing corporate-owned devices via Apple Configurator. This option is ideal for bulk enrollments and when you don't have access to Apple School Manager, Apple Business Manager, or when you require a wired network connection. You must have physical access to the devices because you have to connect to and configure devices on a Mac. There are two different paths you can take:  
  * Setup Assistant enrollment: This method wipes the device and prepares it for enrollment in Apple Configurator. When users turn on their devices, Setup Assistant begins, and then devices enroll in Intune. You must have access to the device serial numbers, because you need to input them into the admin center. 
  * Direct enrollment: This method lets you enroll the device prior to distribution, and doesn't wipe the device. Devices enrolled this way aren't associated with a user so we recommend this option for shared or kiosk devices. The instructions are different for macOS and iOS devices, so be sure to use the correct how-to documentation for devices.  

# [User owned](#tab/user-owned-apple)

* [BYOD enrollment for Macs](../enrollment/macos-enroll.md): Enable enrollment in Intune for personally owned Macs in bring-your-own-device (BYOD) scenarios. Intune-licensed device users initialize enrollment by signing into the Company Portal app on their device.  

* [Apple User Enrollment](../enrollment/apple-user-enrollment-with-company-portal.md): Enable Apple User Enrollment for personally owned iOS/iPadOS devices in BYOD scenarios. This option gives device owners the option to secure the entire device or just work-related apps and data, and keeps managed data and apps on a separate volume away from the user's personal data. Enrollment takes place in the Company Portal app.   

* [Apple Device Enrollment](../enrollment/apple-user-enrollment-with-company-portal.md): Enable Apple Device Enrollment for personally owned iOS/iPadOS devices in BYOD scenarios. This method gives you more control over device configuration settings than User Enrollment. For example, you can apply more granular requirements for passcodes. 

--- 
## Enrollment for Linux  
Employees and students in BYOD scenarios can [enroll personal Linux devices](../user-help/enroll-device-linux.md) in Microsoft Intune. Enrollment enables them to access work resources in Microsoft Edge.  

As an Intune admin, you don't need to do anything to enable Linux enrollment in the admin center. It's automatically enabled. When users enroll their Linux devices, you'll see them in the admin center. For more information, see [Enroll Linux desktop devices in Microsoft Intune](deployment-guide-enrollment-linux.md). 

## Enrollment for Windows    
This section describes the enrollment solutions available for personal and corporate-owned devices running Windows 10 or Windows 11. 

>[!NOTE]
> Microsoft Intune enrollment is supported on devices in cloud environments. Co-management with Configuration Manager is supported in on-premises environments. 

### Windows enrollment methods   
The following table describes the supported enrollment methods for devices running Windows 10 and Windows 11.   

# [Automatic enrollment](#tab/automatic-enrollment)
Make enrollment in Intune easier for employees and students by enabling automatic enrollment for Windows. For more information, see [Enable automatic enrollment](../enrollment/windows-enroll.md#enable-windows-automatic-enrollment). 

* [Microsoft Entra join with automatic enrollment](/azure/active-directory/devices/concept-azure-ad-join): This option is supported on devices that are procured by you or the device user for work use. Enrollment occurs during the out-of-box-experience, after the user signs in with their work account and joins Microsoft Entra ID or by choosing to join the device in Microsoft Entra ID when connecting a work or school account from the Settings app ([as described in Windows device enrollment guide - End user tasks](./deployment-guide-enrollment-windows.md#automatic-enrollment-end-user-tasks)). This solution is for when you don't have access to the device, such as in remote work environments. When these devices enroll, their device ownership changes to corporate-owned and you get access to management features that aren't available on devices marked as personal-owned. 

* [Windows Autopilot user-driven or self-deploying mode](/autopilot/tutorial/autopilot-scenarios): Automatic enrollment is supported with the Windows Autopilot user-driven (for both the Microsoft Entra hybrid join and Microsoft Entra join scenarios) or self-deploying (Microsoft Entra join only) profiles and can be used for corporate-owned desktops, laptops, and kiosks. Device users get desktop access after required software and policies are installed. A Microsoft Entra ID P1 or P2 license is required. We recommend using only Microsoft Entra join, which provides the best user experience and is easier to configure. In scenarios where on-premises Active Directory is still needed, Microsoft Entra hybrid join can be used but you have to [install the Intune connector for Active Directory](/autopilot/windows-autopilot-hybrid), and your devices must be able to connect to a domain controller via either an on-premises network or VPN connection. 

* [Co-management with Configuration Manager](../../configmgr/comanage/quickstart-paths.md): Co-management is best for environments that already manage devices with Configuration Manager, and want to integrate Microsoft Intune workloads. Co-management is the act of moving workloads from Configuration Manager to Intune and telling the Windows client who the management authority is for that particular workload. For example, you can manage devices with compliance policies and device configuration workloads in Intune, and utilize Configuration Manager for all other features, like app deployment and security policies.

* [Enrollment using Group Policy](/windows/client-management/enroll-a-windows-10-device-automatically-using-group-policy): A Group Policy can be used to trigger the automatic enrollment of Microsoft Entra hybrid joined devices without any user interaction. The enrollment process starts in the background (via a scheduled task) after a Microsoft Entra ID-synced user signs in on the device. We recommend this method in environments where devices are Microsoft Entra hybrid joined and not managed using Configuration Manager. 

# [BYOD enrollment](#tab/byod-enrollment) 
These options can be used by users in BYOD scenarios who want to enroll their personal devices without joining them to a domain.
* [Connect a work or school account](./deployment-guide-enrollment-windows.md#automatic-enrollment-end-user-tasks): Users go to the Settings app on their device and add their work or school account. They add their work email address without selecting a domain joining option. 
* [Enrollment using the Intune Company Portal app](../user-help/enroll-windows-10-device.md): Users sign in to the Intune Company Portal app with their work account to enroll their devices. They can install Company Portal from Microsoft Store. 
* Enrollment via a Microsoft 365 app sign-in: Users sign into a Microsoft 365 app or service, such as Exchange Online, from an unmanaged and unregistered device with their work account. On the sign-in prompt, they select **Allow my organization to manage my device**.   

In all of these BYOD scenarios, the devices are Microsoft Entra registered and managed by Intune. If both the MDM and MAM user scopes are enabled for a user in the [Intune automatic enrollment configuration](../enrollment/windows-enroll.md), then the MAM user scope will take precedence and the device will not be enrolled and managed by Intune.  

# [Bulk enrollment via provisioning package](#tab/bulk-enrollment)
Workplace join and enroll a large number of corporate-owned devices in Microsoft Entra ID and Intune without needing to reimage them. This process requires you to create a provisioning package using the Windows Configuration Designer app. You can apply the package during the device OOBE, or upload it on the device in the Settings app.   

---   

### More Windows enrollment features   
There are other Windows enrollment options in Intune to help improve or simplify the device management experience for you and your employees:     

* [Co-management settings](../../configmgr/comanage/autopilot-enrollment.md#configure): Enable co-management settings to integrate Configuration Manager workloads with Intune. Co-management enables you to use both Intune and Configuration Manager features to manage devices.  
* [CNAME validation](../enrollment/windows-enrollment-create-cname.md): Validate a domain name server (DNS) alias (CNAME record type) you created to redirect enrollment requests to Intune servers. The alias simplifies enrollment for users in the absence of Microsoft Entra ID P1 or P2 and automatic enrollment.    
* [Enrollment Status Page](../enrollment/windows-enrollment-status.md): Enable the Enrollment Status Page so that people going through device setup can view and track installation progress.  

## Report and troubleshoot  
Track [incomplete and abandoned user enrollments](../enrollment/enrollment-report-company-portal-abandon.md). This Microsoft Intune report tells you where in the Company Portal users failed to complete the enrollment process.  

For troubleshooting docs, see [Troubleshoot device enrollment](/troubleshoot/mem/intune/troubleshoot-device-enrollment-in-intune).    

## Resources 
Additional enrollment guides are available throughout the Microsoft Intune documentation. These guides include visual comparisons, how-to steps, tips, and enrollment best practices for each supported platform.   

- [Android enrollment guide](deployment-guide-enrollment-android.md)
- [iOS/iPadOS enrollment guide](deployment-guide-enrollment-ios-ipados.md)
- [Linux enrollment guide](deployment-guide-enrollment-linux.md)
- [macOS enrollment guide](deployment-guide-enrollment-macos.md)
- [Windows enrollment guide](deployment-guide-enrollment-windows.md)    

## Next steps  

1. [Set up Microsoft Intune](deployment-plan-setup.md)
2. [Add, configure, and protect apps](deployment-plan-protect-apps.md)
3. [Plan for compliance policies](deployment-plan-compliance-policies.md)
4. [Create device configuration profiles](deployment-plan-configuration-profile.md)
5. 🡺 **Enroll devices** (*You are here*)  
