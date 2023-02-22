---
# required metadata

title: Create device platform restrictions  
titleSuffix: Microsoft Intune  
description: Restrict personally owned devices, and specific device platforms and OS versions from enrolling in Intune. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/08/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: 
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Create device platform restrictions   

[!INCLUDE [azure_portal](../includes/azure_portal.md)]  

*Applies to: Android, iOS/iPadOS, macOS, Windows 10, Windows 11*    

Create a device platform enrollment restriction policy to restrict devices from enrolling in Intune. Available restrictions include:  

* Device platform
* OS version
* Manufacturer
* Ownership (personally-owned)

 You can create a new device platform restriction policy in the Microsoft Endpoint Manager admin center or use the default policy that's already available. You can have up to 25 device platform restriction policies. 

This article describes the device platform restrictions supported in Microsoft Intune and how to configure them in the admin center.  

## Default policy 
Microsoft Intune provides one default policy for device platform restrictions that you can edit and customize as needed. Intune applies the default policy to all user and userless enrollments until you assign a higher-priority policy.  

## Best practice - Android platform restrictions          
Since Intune supports two Android platforms, it's important to understand how OS version restrictions work when used together with device platform restrictions:   
  * If you allow both platforms for the same group, and then refine it for specific and non-overlapping versions, devices are sent through the Android enrollment flow that's picked for their version.   
  * If you allow both platforms, but block the same versions, devices running blocked versions can't enroll. Users on these devices are sent through the Android device administrator enrollment flow before they're blocked and prompted to sign out. 

## Create a device platform restriction   

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Go to **Devices** > **Enroll devices** > **Enrollment device platform restrictions**.  
3. Select the tab along the top of the page that corresponds with the platform you're configuring. Your options:  

    * **Android restrictions**
    * **Windows restrictions**
    * **MacOS restrictions**
    * **iOS restrictions**  

4. Select **Create restriction**.  
5. On the **Basics** page, give the restriction a name and optional description. 
6. Select **Next**.  
7. On the **Platform settings** page, configure the restrictions for your selected platform. Your options:       
    - **Platform** (Android): Select **Allow** to permit a platform to enroll, and **Block** to restrict it.       
    - **MDM** (Windows, macOS, and iOS/iPadOS): Select **Allow** to permit a platform to enroll, and **Block** to restrict it.   
    - **Personally-owned**: Select **Allow** to permit devices to enroll and operate as personal devices.  
    - **Device manufacturer** (Android): Enter a comma-separated list of the manufacturers that you want to block. 
    - **Allow min/max range** (Android, Windows, iOS/iPadOS): Enter the minimum and maximum OS versions allowed to enroll. Supported version formats include:  
        - Windows supports major.minor.build.rev for Windows 10 and Windows 11.    
        - Android device administrator and Android Enterprise work profile support major.minor.rev.build.  
        - iOS/iPadOS supports major.minor.rev.  

             > [!TIP]
             > The min/max range isn't applicable to Apple devices that enroll with the Device Enrollment Program, Apple School Manager, or the Apple Configurator app. Although Intune doesn't block ADE enrollments that use Company Portal to authenticate, not meeting OS requirements impacts registration because devices can't create the Azure AD device record used to evaluate Conditional Access policies. You can tell that this is the case if a device user receives an error message that says "Couldn't map device record with a user" after they sign in to Company Portal.        

8. Select **Next**. 
9. Optionally, add scope tags to the restriction. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md). 

      > [!NOTE]
      >  If you apply scope tags to a restriction, only Intune users within scope can view and manage the policy. Only people in scope can view and reorder a restriction, or change its priority level. They can also see the relative priority of the restriction, even if they can't see all restrictions.  

10. Select **Next**. 
11. On the **Assignments** page, select **Add groups** and then use the search box to find and select groups. To assign the restriction to all device users, select **Add all users**. If you don't assign a restriction to at least one group, the restriction won't take effect.  
12. Optionally, after you assign groups, select **Edit filter** to restrict the policy assignment further with filters. Filters are available for macOS, iOS, and Windows policies. For more information, see [Apply assignment filters](create-device-platform-restrictions.md#apply-assignment-filters) (in this article).  
13. Select **Next**. 
14. Review your policy, and then select **Create** to create it. 

You can view the new restriction policy and access its properties in the **Enrollment device platform restrictions** > **Device type restrictions** table. Select and drag the restriction to reposition it in the table and change its priority.   

## Apply assignment filters 

You can use assignment filters to include and exclude additional devices from certain group-targeted policies. Enrollment restrictions and ESP policies both support the use of assignment filters.   

For example, you can use a filter to allow personal Windows devices to enroll while blocking devices that run a specific operating system SKU. To achieve this outcome, apply a preconfigured filter to your enrollment restriction assignments. The filter needs to have the `operatingSystemSKU` property in its rules. Example steps:  

  1. Create a platform enrollment restriction policy for Windows.  
  2. In the platform settings, select the option that allows personal devices to enroll. 
  3. In the assignments settings, select the groups you want to assign.
  4. Select **Edit filter** and then apply your preconfigured filter that contains the `operatingSystemSKU` property. The applied property blocks devices running Windows 10 Home edition. 

For more information about creating filters, see [Create a filter](../fundamentals/filters.md). 

### Supported filter properties  

Enrollment restrictions support fewer filter properties than other group-targeted policies. This is because devices aren't yet enrolled, so Intune doesn't have the device info to support all properties. You'll see the limited selection of properties when you:  

* Configure a device platform restriction policy for Apple and Windows devices. 
* Configure an enrollment status page (ESP) policy for Windows. 
* Edit a filter that's in-use in an enrollment restriction or ESP profile. 

The following filter properties are always available to use with enrollment policies:    

**Windows** 

* OS version 
* Operating System SKU 
* Enrollment profile name

**iOS/iPadOS and macOS**  
* Manufacturer 
* Model 
* OS version 
* Ownership 
* Enrollment profile name 

For more information about these properties, see [device properties](../fundamentals/filters-device-properties.md#device-properties). Filters can't be used with Android enrollment restrictions.  

## Edit enrollment restrictions  

Edits are applied to new enrollments and do not affect devices that are already enrolled.  

1. Go to **Enrollment device platform restrictions**.  
2. In the **Device type restrictions** table, select the name of the policy you want to change.
3. Select **Properties**.  
4. Select **Edit**.   
5. Make your changes and select **Review + save**. 
6. Review your changes and select **Save**.  

