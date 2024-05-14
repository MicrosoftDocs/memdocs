---
# required metadata

title: Device staging overview   
titleSuffix: Microsoft Intune
description: An overview of the device staging enrollment feature in Microsoft Intune. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/14/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

## Device staging for Android Enterprise enrollment  

**Applies to Android**  

Enable device staging during enrollment to reduce end user steps for frontline workers and optimize devices for immediate productivity. During device staging, you or a third-party vendor can complete both the admin and end user stages of preprovisioning. Minimal interaction is required of the user when they receive their device.

Device staging uses a *staging* token during the enrollment process rather than the *default* token type. Microsoft Intune supports device staging for Android Enterprise devices running Android 8 or later. You can enable device staging in these enrollment profiles:   

* Android Enterprise corporate-owned fully managed  

* Android Enterprise corporate-owned work profile  

This article provides an overview of device staging and token management in the Microsoft Intune admin center. 

## Token types     

When you create an enrollment profile in the admin center, you have to select a token type. There is a default token and a staging token. Each type enables a different enrollment experience. 

### Staging token  

The *staging* token enables a staged version of the enrollment flow so that you or a third-party vendor can complete the admin *and* end user steps. This process requires more work from the admin or third party vendor than the end user.

There are three stages during this process:  

-  Admin 
-  Third party vendor 
-  End user  

The device remains userless throughout the admin and vendor stage. It becomes user affiliated and ready for use at the last step when the user signs in with their credentials. 

If you're not using a third party vendor to provision devices, you can continue in the admin stage until it's time to distribute devices to the end user. End users complete the last stage by signing into devices with their work or school account. Devices are ready to use upon sign-in.  

<screenshot> 

The admin stage of this flow requires you to:
1. Create the enrollment token and initiate the enrollment process for the device. 
1. Scan the QR code and follow the on-screen prompts to complete enrollment. 

>[!IMPORTANT] If a third-party is doing the provisioning for you, share the device staging token with them now so they can continue with the steps.    

1. Complete the provisioning steps. 
1. For a device enrolling with a newly-created enrollment token, create a dynamic device group or an assignment filter to assign policies and apps in the user stage. 
1. Distribute the device to the end user.   

### Default token   

The *default* token enables the standard enrollment flow, with two stages of pre-provisioning: 

- Admin stage  
- End user stage  

You complete a portion of the pre-provisioning steps before you distribute the devices. Then end users complete the remaining steps when they sign in with their work or school account. With this token, end users complete the majority of the pre-provisioning steps.  

<screenshot> 

The admin stage of this flow requires you to:  
1. Create the default enrollment token and initiate the enrollment process for the device.  
1. Scan the QR code and follow the on-screen prompts to complete enrollment. 
1. For a device enrolling with a newly-created enrollment token, create a dynamic device group or an assignment filter to assign policies and apps in the user stage. 
1. Distribute the device to the end user.   

The end user stage of this flow requires end users to: 

1. Unbox the device and connect to Wi-Fi 
1. Sign in to work or school account, and then follow the on-screen prompts.  
1. Complete the pre-provisioning steps. If they're going through work profile enrollment, for example, they create and install the work profile.  
1. Grant permissions or accept terms wherever required. 

For detailed steps, see:
- [Set up enrollment for Android Enterprise fully managed devices]()
- [Set up enrollment for corporate-owned work profile devices]()    

## Replace, remove, or export token  
Select a token in the admin center to access these management options:   

- **Replace token**: Generate a new token that's nearing expiration. 

- **Revoke token**: Immediately expire the token. After you revoke it, the token is no longer usable. This option is useful if you: 

  - Accidentally share the token with an unauthorized party. 

  - Complete all enrollments and no longer need the token. 

- **Export token**: Export the JSON content of the token. You can use this option to get the JSON content required for Google Zero Touch or Knox Mobile Enrollment configuration.  

When applied, these actions don't have any effect on devices that are already enrolled.   

## Next steps  



