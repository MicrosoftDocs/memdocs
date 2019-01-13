---
title: Windows Autopilot with co-management
titleSuffix: Configuration Manager
description: Use Windows Autopilot with co-management in Configuration Manager to simplify the set up of new Windows 10 devices.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Windows Autopilot with co-management

Receiving a new Windows 10 device is exciting. However, it can take time to configure all your settings and apps so that you can be productive. Co-management solves this device provisioning problem with Windows Autopilot.

Autopilot provides a simplified experience for both you and your users in the following situations:
- Set up and preconfigure new Windows 10 devices  
- Reset, recycle, and recover existing devices  

Autopilot reduces the time, resources, and complexity associated with deploying, managing, and retiring devices. At the same time, the experience for your users is streamlined and easy from first boot.

Windows Autopilot supports several scenarios, all of which are maximized with co-management:

- Users can drive their own deployments of new devices into either Active Directory with hybrid Azure AD join, or Azure Active Directory (Azure AD)  

- You can set up self-deploying new device deployments into Azure AD for shared devices and kiosks  

- With Windows Autopilot for existing devices, use Configuration Manager to migrate an existing device from Windows 7 and Active Directory to Windows 10 and Azure AD  

<!--update with final video for this quickstart-->
In the following video, senior program manager Danny Guillory and principal program manager Andrew McMurray discuss and demo Windows Autopilot with co-management:

> [!VIDEO https://www.youtube.com/embed/gA5q0_3bxPs]



## Benefits

When you use co-management and Autopilot together, you make sure that new devices entering your network end up in the same state of management. In this setup, devices are enrolled in Intune and have a Configuration Manager client.  It allows you to use the new Windows 10 provisioning model, and helps you eliminate the need to create, maintain, and update custom OS images. 

In all of these scenarios, you can automatically [enable co-management](/sccm/comanage/how-to-prepare-win10) by Intune. This automation assists with the provisioning process, and for ongoing management of the device.

With Autopilot, you don't need to worry about images and drivers. Focus on provisioning devices by this automated process using Intune and Configuration Manager via co-management.


Here's how using co-management and Autopilot together can help you right now:

#### Reduce time, costs, and complexity
Windows Autopilot uses the OEM-optimized version of Windows 10 that's preinstalled on the device. This configuration saves organizations the effort of having to maintain custom images and drivers for every model of device in use. Instead of reimaging the device, transform the existing Windows 10 installation into a "business-ready" state. It applies settings and policies, installs apps, and changes the edition of Windows 10. For example, upgrading from Windows 10 Pro to Windows 10 Enterprise so that you can support advanced features.

#### Improve the user experience
The best user experience causes the least disruption and helps them get back to focusing on their work. Windows Autopilot offers a simple approach to help your users get set up quickly with a few simple clicks and their Azure AD credentials. For many organizations with a large field of remote employees, use Windows Autopilot to ship new devices straight from the manufacturer.

#### Use Autopilot and Configuration Manager to migrate existing Windows 7 devices to Windows 10
With Windows Autopilot for existing devices, you create a configuration file and deploy it with a Configuration Manager task sequence. This process easily migrates existing devices from Windows 7 to Windows 10. You use a signature Windows 10 image in Configuration Manager, and then apply it to the existing Windows 7 device with the Autopilot configuration. When the user starts the device, they use the Autopilot user-driven onboarding process.

Here are the steps for Autopilot for existing devices:

![Process overview for Windows Autopilot for existing devices](media/autopilot-for-existing-devices.png)

1. Deploy group policy to redirect known folders to OneDrive
2. Generate Autopilot configuration file
3. Deploy task sequence to upgrade to Windows 10
4. Windows 10 machine goes through Autopilot on first boot

#### Modernizing device provisioning for all types of workers
With Autopilot, you can now provide a hands-free OS deployment to unmanned devices or shared devices using the self-deploying mode. This setup meets the needs of all your different types of workers. Also, the Windows Autopilot Reset function makes sure that reprovisioning of a device to a new user is simple and easy. This process simplifies what has traditionally been a difficult task when you have seasonal or contract workers. 



## Case study

The German logistics and rail freight company DB Shenker uses Autopilot to increase employee productivity and free its IT teams from working on day-to-day support tasks. Shenker has moved away from traditional imaging and replaced it with provisioning via the cloud. They now use Azure AD-join and Intune to get new devices up and running quickly. 

Rather than have their remote workers waste time traveling to a location with IT services, Shenker now uses Windows Autopilot. They ship their workers hardware directly from the manufacturer to their local field office. The worker connects the new device to the internet, and they sign in with their Azure AD credentials. The device then connects to the applications and services that Schenker's IT department assigns to the user's individual profile.

For more information, see [Global logistics firm centralizes IT, unites employees with modern digital workplace](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10).



## Value proposition

Create satisfaction in your organization by creating a better user experience for your users. Use Windows Autopilot to drive down costs. Free up your time to focus on other projects to drive more value and impact for your organization.



## Configure

For more information, see [Enroll Windows devices in Intune by using the Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

