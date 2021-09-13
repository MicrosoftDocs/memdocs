---
# required metadata

title: Device management capabilities in Microsoft Intune 
description: Read this topic to find out how Intune can help you manage devices that you enroll.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/16/2019
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 
ROBOTS: NOINDEX,NOFOLLOW

# optional metadata

#audience:

ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---
# Enrolled device management capabilities of Microsoft Intune

Microsoft Intune lets you manage a range of devices by *enrolling* them into the service. You can enroll some device types yourself, or users can enroll using the *company portal* app. Enrolling lets them browse and install apps, make sure that their devices are compliant with company policies, and contact their IT support.

This article gives a full list of the capabilities that you get after devices are enrolled.

Management, inventory, app deployment, provisioning, and retirement are all handled through Intune in the Azure portal.

Users gain access to the company portal, which enables them to install apps, enroll and remove devices, and contact their IT department or helpdesk.



## Device security and configuration

|Capability|Details|More information|
|--------------|-----------|--------------------|
|Configuration policies<br><br>Custom policies| Lets you manage many settings and features on mobile devices in your organization. For example, you can  require a password, limit the number of failed attempts, limit the amount of time before the screen locks, set password expiration, and prevent previously used passwords. You can also control the use of hardware and software features such as the device camera or the web browser.<br><br>Use custom policies when configuration policies do not contain the settings that you require. For iOS/iPadOS devices, you can import settings that you exported from the Apple Configurator tool. For other devices, you can use Open Mobile Alliance Uniform Resource Identifier (OMA-URI) settings to configure settings and features on the device.|[Manage settings and features on your devices with Microsoft Intune policies](../protect/device-compliance-get-started.md)|
|Remote Wipe, Remote Lock, and Passcode Reset|Erases sensitive data when a device is lost or stolen. For example, you can remotely lock the device, restore it to factory settings, or wipe only corporate data.<br><br>You can reset passcodes if users lose access to their device, lock missing or stolen devices, or even wipe data off of missing or stolen devices.|Help protect your devices with [remote lock](../remote-actions/device-remote-lock.md) and [passcode reset](../remote-actions/device-passcode-reset.md)|
|Kiosk mode|Lets you lock down certain features of mobile devices such as screen captures and power switches. Also lets you restrict devices to run a single app that you specify. |[iOS configuration policy settings in Microsoft Intune](../configuration/device-restrictions-ios.md)|
|Autopilot Reset|Sends a task to the device to start the reset process remotely, avoiding the need for IT staff or other administrators to visit each machine to start the process. When Autopilot reset is used on a device, the device's primary user will be removed. The next user who signs in after the reset will be set as the primary user.|[Remote Windows Autopilot Reset](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)|

## App management

|Capability|Details|More information|
|--------------|-----------|--------------------|
|App deployment and management|Provides a range of tools to help you manage mobile apps through their lifecycle, including app deployment from installation files and app stores, detailed monitoring of app status, and app removal.|[Deploy apps in Microsoft Intune](../apps/apps-deploy.md)|
|Compliant and noncompliant apps|Lets you specify lists of compliant apps (that users are allowed to install) and noncompliant apps (that users aren't allowed to install).|[iOS policy settings in Microsoft Intune](../configuration/device-restrictions-ios.md)|
|Mobile application management|Configures restrictions for apps by using mobile application management for all devices that are both managed with Intune and not managed with Intune. You can increase the security of your company data by restricting operations such as copy and paste, external backup of data, and the transfer of data between apps.|[Configure and deploy mobile application management policies in the Microsoft Intune console](../developer/app-wrapper-prepare-android.md)|
|iOS mobile app configuration|Uses mobile app configuration policies to supply settings for iOS/iPadOS apps that might be required when the user runs the app. For example, an app might require the user to specify a port number or logon information. You can streamline app configuration and reduce the number of support calls.|[Configure iOS/iPadOS apps with mobile app configuration policies in Microsoft Intune](../apps/app-configuration-policies-use-ios.md)|
|iOS/iPadOS mobile app provisioning profiles|Helps you deploy provisioning profiles to iOS/iPadOS apps that are nearing expiration. |[Use iOS/iPadOS mobile provisioning profile policies to prevent your apps from expiring](../apps/app-provisioning-profile-ios.md)|
|Managed browser|Configures managed browser policies to control the websites that device users can visit. In addition, you can also apply mobile application management policies to the managed browser.|[Manage Internet access using managed browser policies with Microsoft Intune](../apps/manage-microsoft-edge.md)|
|Windows Hello for Business|Lets you integrate with Windows Hello for Business, which is an alternative sign-in method for Windows 10 that uses on-premises Active Directory or  Azure Active Directory to replace passwords, smart cards, or virtual smart cards.|[Control Windows Hello for Business settings on devices with Microsoft Intune](../protect/windows-hello.md)|
|Volume purchased apps|Helps you manage apps that you purchased through a volume-purchase program by importing the license information from the app store, tracking how many of the licenses you have used, and preventing you from installing more copies of the app than you own.|[Manage volume-purchased apps using Microsoft Intune](../apps/vpp-apps.md)|

## Company resource access

|Capability|Details|More information|
|--------------|-----------|--------------------|
|Certificate profiles|Creates and deploys trusted certificate profiles and Simple Certificate Enrollment Protocol (SCEP) certificates, which can be used to secure and authenticate Wi-Fi, VPN, and email profiles.|[Secure resource access with certificate profiles in Microsoft Intune](../protect/certificates-configure.md)|
|Wi-Fi profiles|Deploys wireless network settings to your users. By deploying these settings, you minimize the user effort that's required to connect to the corporate network.|[Wi-Fi connections in Microsoft Intune](../configuration/wi-fi-settings-configure.md)|
|Email profiles|Creates and deploys email settings to devices so that users can access corporate email on their personal devices without any required setup on their part.|[Configure access to corporate email using email profiles with Microsoft Intune](../configuration/email-settings-configure.md)|
|VPN profiles|Deploys VPN settings to users and devices in your organization. By deploying these settings, you minimize the user effort that's required to connect to resources on the company network.|[VPN connections in Microsoft Intune](../configuration/device-profiles.md#vpn)|
|Conditional Access policies|Manages access to Microsoft Exchange email and SharePoint Online from devices that are not managed by Intune.|[Restrict access to email and SharePoint with Microsoft Intune](../protect/app-based-conditional-access-intune.md)|

## Next steps

[See a list of devices that you can manage](../remote-actions/device-management.md).