---
# required metadata

title: Set the mobile device management authority
titleSuffix: Microsoft Intune
description: Set the mobile device management authority in Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/16/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 8deff871-5dff-4767-9484-647428998d82

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Set the mobile device management authority

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

The mobile device management (MDM) authority setting determines how you manage your devices. As an IT admin, you must set an MDM authority before users can enroll devices for management.

Possible configurations are:

- **Intune Standalone** - cloud-only management, which you configure by using the Azure portal. Includes the full set of capabilities that Intune offers. [Set the MDM authority in the Intune console](#set-mdm-authority-to-intune).

- **Intune co-management** - integration of the Intune cloud solution with Configuration Manager for Windows 10 devices. You configure Intune by using the Configuration Manager console. [Configure auto-enrollment of devices to Intune](https://docs.microsoft.com/configmgr/comanage/tutorial-co-manage-clients#configure-auto-enrollment-of-devices-to-intune). 

- **Mobile Device Management for Office 365** - integration of Office 365 with the Intune cloud solution. You configure Intune from your Microsoft 365 admin center. Includes a subset of the capabilities that are available with Intune Standalone. Set the MDM authority in Microsoft 365 admin center.

- **Office 365 MDM Coexistence** You can activate and use both MDM for Office 365 and Intune concurrently on your tenant and set the management authority to either Intune or MDM for Office 365 for each user to dictate which service will be used to manage their mobile devices. User’s management authority is defined based on the license assigned to the user. For more information, see [Microsoft Intune Co-existence with MDM for Office 365](https://blogs.technet.microsoft.com/configmgrdogs/2016/01/04/microsoft-intune-co-existence-with-mdm-for-office-365)

## Set MDM authority to Intune

If you haven't yet set the MDM authority, follow the steps below.

1. In the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), select the orange banner to open the **Mobile Device Management Authority** setting. The orange banner is only displayed if you haven't yet set the MDM authority.
2. Under **Mobile Device Management Authority**, choose your MDM authority from the following options:
   - **Intune MDM Authority**
   - **None**

   ![Screenshot of Intune set mobile device management authority screen](./media/mdm-authority-set/set-mdm-auth.png)

   A message indicates that you have successfully set your MDM authority to Intune.

### Workflow of Intune Administration UI
When Android or Apple device management is enabled, Intune sends device and user information to integrate with these third-party services to manage their respective devices.

Scenarios that add a consent to share data are included when:
- You enable Android work profiles.
- You enable and upload Apple MDM push certificates.
- You Enable any of the Apple services, such as Device Enrollment Program, School Manager, or Volume Purchasing Program.

In each case, the consent is strictly related to running a mobile device management service. For example, confirming that an IT Admin has authorized Google or Apple devices to enroll. Documentation to address what information is shared when the new workflows go live is available from the following locations:
- [Data Intune sends to Google](https://aka.ms/Data-intune-sends-to-google)
- [Data Intune sends to Apple](https://aka.ms/data-intune-sends-to-apple)

## Key Considerations
After you switch to the new MDM authority, there will likely be transition time (up to eight hours) before the device checks in and synchronizes with the service. You're required to configure settings in the new MDM authority to make sure that enrolled devices will continue to be managed and protected after the change. 
- Devices must connect with the service after the change so that the settings from the new MDM authority (Intune standalone) replace the existing settings on the device.
- After you change the MDM authority, some of the basic settings (such as profiles) from the previous MDM authority will remain on the device for up to seven days or until the device connects to the service for the first time. It's recommended that you configure apps and settings (policies, profiles, apps, etc.) in the new MDM authority as soon as possible and deploy the setting to the user groups that contains users who have existing enrolled devices. As soon as a device connects to the service after the change in MDM authority, it will receive the new settings from the new MDM authority and prevent gaps in management and protection.
- Devices that don't have associated users (typically when you have iOS/iPadOS Device Enrollment Program or bulk enrollment scenarios) are not migrated to the new MDM authority. For those devices, you need to call support for assistance to move them to the new MDM authority.

## Change MDM authority to Office 365

To activate Office 365 MDM (or to enable MDM coexistence in addition to your existing Intune Service), go to [https://protection.office.com](https://protection.office.com), choose **Data Loss Prevention** > **Device Security Policies** > **View list of Managed Devices** > **Let's get started**.

For more information, see [Set up Mobile Device Management (MDM) in Office 365](https://support.office.com/en-us/article/Set-up-Mobile-Device-Management-MDM-in-Office-365-dd892318-bc44-4eb1-af00-9db5430be3cd).

If you want the end users to only be managed by Office 365 MDM, then remove any assigned Intune and/or EMS licenses after activating Office 365 MDM.

## Mobile device cleanup after MDM certificate expiration

The MDM certificate is renewed automatically when mobile devices are communicating with the Intune service. If mobile devices are wiped, or they fail to communicate with the Intune service for some period of time, the MDM certificate will not get renewed. The device is removed from the Azure portal 180 days after the MDM certificate expires.

## Remove MDM authority

The MDM authority can't be changed back to Unknown. The MDM authority is used by the service to determine which portal enrolled devices report to (Microsoft Intune or Office 365 MDM).

## What to expect after changing the MDM authority

- When the Intune service detects that a tenant’s MDM authority has changed, it sends out a notification message to all the enrolled devices to check in and synchronize with the service (this notification is outside of the regularly scheduled check-in). Therefore, after the MDM authority for the tenant has been changed from Intune standalone, all the devices that are powered on and online will connect with the service, receive the new MDM authority, and be managed by the new MDM authority. There is no interruption to the management and protection of these devices.
- Even for devices that are powered on and online during (or shortly after) the change in MDM authority, there will be a delay of up to eight hours (depending on the timing of the next scheduled regular check-in) before devices are registered with the service under the new MDM authority.    

  > [!IMPORTANT]    
  > Between the time when you change the MDM authority and when the renewed APNs certificate is uploaded to the new authority, new device enrollments and device check-in for iOS/iPadOS devices fail. Therefore, it's important that you review and upload the APNs certificate to the new authority as soon as possible after the change in MDM authority.

- Users can quickly change to the new MDM authority by manually starting a check-in from the device to the service. Users can easily make this change by using the Company Portal app and initiating a device compliance check.
- To validate that things are working correctly after devices have checked-in and synchronized with the service after the change in MDM authority, look for the devices in the new MDM authority.
- There is an interim period when a device is offline during the change in MDM authority and when that device checks in to the service. To help ensure that the device remains protected and functional during this interim period, the following profiles remain on the device for up to seven days (or until the device connects with the new MDM authority and receives new settings that overwrite the existing ones):
  - E-mail profile
  - VPN profile
  - Cert profile
  - Wi-Fi profile
  - Configuration profiles
- After you change to the new MDM authority, the compliance data in the Microsoft Intune administration console can take up to a week to accurately report. However, the compliance states in Azure Active Directory and on the device will be accurate so the device is still be protected.
- Make sure the new settings that are intended to overwrite existing settings have the same name as the previous ones to ensure that the old settings are overwritten. Otherwise, the devices might end up with redundant profiles and policies.    

  > [!TIP]    
  > As a best practice, you should create all management settings and configurations, as well as deployments, shortly after the change to the MDM authority has completed. This helps ensure that devices are protected and actively managed during the interim period.

- After you change the MDM authority, perform the following steps to validate that new devices are enrolled successfully to the new authority:   
  - Enroll a new device
  - Make sure the newly enrolled device shows up in the new MDM authority.
  - Perform an action, such as Remote Lock, from the administration console to the device. If it's successful, the device is being managed by the new MDM authority.
- If you have issues with specific devices, you can unenroll and reenroll the devices to get them connected to the new authority and managed as quickly as possible.

## Next steps

With the MDM authority set, you can start [enrolling devices](../enrollment/device-enrollment.md).
