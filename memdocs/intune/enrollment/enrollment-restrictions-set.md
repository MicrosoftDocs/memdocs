---
# required metadata

title: Set enrollment restrictions in Microsoft Intune
titleSuffix:
description: Restrict enrollment by platform and set a device enrollment limit in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/20/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 9691982c-1a03-4ac1-b7c5-73087be8c5f2

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Set enrollment restrictions  

**Applies to**
* Android  
* iOS
* macOS 
* Windows 10
* Windows 11 


[!INCLUDE [azure_portal](../includes/azure_portal.md)]  

Enrollment restrictions block Intune enrollment on devices that fall short of your device requirements. Enrollment restriction configurations are available in the Microsoft Endpoint Manager admin center and includes the following types of restrictions:   

- Device platform restrictions, which let you restrict device platforms, OS versions, and personally owned devices.  
- Device limit restrictions, which let you restrict the number of devices allowed to enroll. 

You can create new restrictions or use the Intune defaults. Each type of restriction comes with one default policy that you can edit and customize as needed. Intune will apply the default to all user and userless enrollments until you assign a higher-priority restriction.   

You can have up to 25 restrictions per type.  

## Device platform restrictions  
Use device platform restrictions to restrict enrollment by device platform and OS version. You can also use platform restrictions to block personally-owned devices from enrolling. This section describes the available restriction options in Intune and how to create a restriction policy.     

### Restrict device platform  
Restrict devices running on the following platforms: 

   * Android device administrator
   * Android Enterprise work profile
   * iOS/iPadOS
   * macOS
   * Windows 

 > [!TIP] 
 >  If you allow both Android platforms for the same group, devices that support work profile will enroll with a work profile. Devices that don't support it will enroll on the Android device administrator platform. Neither work profile nor device administrator enrollment will work until you complete all prerequisites for Android enrollment.   

### Restrict OS version  
Restrict device versions by setting a maximum and minimum OS version. Devices running earlier or later versions will not be allowed to enroll. You can apply this type of restriction to the following operating systems: 

   * Android device administrator
   * Android Enterprise work profile  
   * iOS/iPadOS
   * Windows  

> [!NOTE] 
> For Android and iOS/iPadOS, version restrictions are only supported on devices that enrolled via Intune Company Portal.    

#### Android version restrictions    
Since there are two Android platforms, it's important to understand how version restrictions work in conjunction with platform restrictions: 
  * If you allow both platforms for the same group, and then refine it for specific and non-overlapping versions, devices are sent through the Android enrollment flow that's picked for their version.   
  * If you allow both platforms, but block the same versions, devices running blocked versions cannot enroll. Users on these devices are sent through the Android device administrator enrollment flow before they are blocked and prompted to sign out. 

### Restrict personally-owned devices  
Restrict personal devices from enrolling in Intune. This restriction helps prevent device users from accidentally enrolling their personal devices.  

#### Blocking personal Android devices
By default, until you manually make changes in the admin center, your Android Enterprise work profile device settings and Android device administrator device settings are the same. 

If you block Android Enterprise work profile enrollment on personal devices, only corporate-owned devices can enroll with [personally-owned work profiles](../apps/android-deployment-scenarios-app-protection-work-profiles.md#android-enterprise-personally-owned-work-profiles).  


#### Blocking personal iOS/iPadOS devices
By default, Intune classifies iOS/iPadOS devices as personally-owned. To be classified as corporate-owned, an iOS/iPadOS device must fulfill one of the following conditions:
- [Registered with a serial number](corporate-identifiers-add.md).
- Enrolled by using Automated Device Enrollment (formerly Device Enrollment Program)

> [!NOTE]
> An iOS User Enrollment profile overrides an enrollment restriction policy. For more information, see [Set up iOS/iPadOS and iPadOS User Enrollment (preview)](ios-user-enrollment.md).  

### Blocking personal Windows devices
If you block personally owned Windows devices from enrollment, Intune checks to make sure that each new Windows enrollment request has been authorized for corporate enrollment. Unauthorized enrollments are blocked.  

The following enrollment methods are authorized for corporate enrollment:  
- The enrolling user is using a [device enrollment manager account]( device-enrollment-manager-enroll.md).
- The device enrolls through [Windows Autopilot](../../autopilot/enrollment-autopilot.md).
- The device is registered with Windows Autopilot but isn't an MDM enrollment only option from Windows Settings.
- The device enrolls through a [bulk provisioning package](windows-bulk-enroll.md).
- The device enrolls through GPO, or [automatic enrollment from Configuration Manager for co-management](/configmgr/comanage/quickstart-paths#bkmk_path1).
 
Intune marks devices going through the following types of enrollments as corporate-owned. But Intune blocks devices enrolling  since they don't offer the Intune administrator per-device control, they are blocked:  
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with [Azure Active Directory join during Windows setup](/azure/active-directory/device-management-azuread-joined-devices-frx)\*.
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with [Azure Active Directory join from Windows Settings](/azure/active-directory/user-help/user-help-register-device-on-network)\*.
 
Intune also blocks personal devices using these enrollment methods:  
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with [Add Work Account from Windows Settings](/azure/active-directory/user-help/user-help-join-device-on-network)\*.
- [MDM enrollment only]( /windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device) option from Windows Settings.

\* These won't be blocked if registered with Autopilot.  

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
    - **Platform** (Android only): Select **Allow** next to permitted platforms.    
    - **MDM** (Windows, macOS, and iOS/iPadOS): Select **Allow** next to permitted platforms.   
    - **Allow min/max range** (Android, Windows, iOS/iPadOS only): Enter the minimum and maximum OS versions allowed to enroll. Supported version formats include:  
        - Android device administrator and Android Enterprise work profile support major.minor.rev.build.
        - iOS/iPadOS supports major.minor.rev. Operating system versions don't apply to Apple devices that enroll with the Device Enrollment Program, Apple School Manager, or the Apple Configurator app.
        - Windows supports major.minor.build.rev for Windows 10 and Windows 11 only.
    - **Personally-owned**: Select **Allow** to permit devices to enroll and operate as personal devices.  
    - **Device manufacturer**: Enter a comma-separated list of the manufacturers that you want to block.  

8. Select **Next**. 
9. Optionally, add scope tags to the restriction. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md). 

      > [!NOTE]
      >  If you apply scope tags to a restriction, only Intune users within scope can view and manage the policy. Only people in scope can view and reorder a restriction, or change its priorty level. They can also see the relative priority of the restrictions, even if they can't see all restrictions.  

10. Select **Next**. 
11. On the **Assignments** page, select **Add groups** and then use the search box to find and select groups. To assign the restriction to all device users, select **Add all users**. If you don't assign a restriction to at least one group, the restriction won't take effect.  
12. Optionally, after you assign groups, select **Edit filter** to restrict the policy assignment further with filters. Filters are available for macOS, iOS, and Windows policies. For more information, see [Using filters with enrollment restriction and ESP policies](enrollment-restrictions-set.md#apply-filters-to-enrollment-restriction-and-esp-policies) (in this article).  
13. Select **Next**. 
14. On the **Review + create** page, select **Create** to save and create your restriction.  

You can view the new restriction and access its properties from the **Device type restrictions** table. Select and drag the restriction to reposition it in the table and change its priority.   

## Device limit restrictions  
You can enforce device limit restrictions on devices that meet the following criteria:  

  * Intune-managed  
  * Established contact with Intune within last 90 days  
  * Not in a registration-pending state for more than 24 hours  
  * Hasn't failed Apple enrollment  
  * Hasn't been deleted from Intune  
  * Enrollment type is not in shared mode (check DeviceCountsForDeviceCap for detail)  

 Device limit restrictions cannot be applied to devices in the following Windows enrollment scenarios, because these scenarios utilize shared device mode:  

  * Co-managed enrollments  
  * Group Policy (GPO) enrollments  
  * Azure Active Directory (Azure AD) joined enrollments, including bulk enrollments  
  * Windows Autopilot enrollments  
  * Device enrollment manager enrollments

Instead, you can configure a hard limit for these enrollment types in Azure AD. For more information, see [Manage device identities by using the Azure portal](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings).  

### What device users see during enrollment     

If restrictions are applied, BYOD users who reach their device limit receive a message during enrollment explaining the limitation. To continue enrolling, the device user must unenroll an existing device. Alternatively, you can increase the device limit in the admin center. For more information about troubleshooting enrollment errors such as this one, see [Troubleshoot device enrollment](/troubleshoot/mem/intune/troubleshoot-device-enrollment-in-intune#device-cap-reached).  

![Example image of device limit notification which reads, "Couldn't add your device. You have added the maximum number of devices allowed by your IT support. You must remove a device before you can add a new one.](./media/enrollment-restrictions-set/enrollment-restrictions-ios-set-limit-notification.png)  


## Create a device limit restriction  

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Enrollment restrictions** > **Create restriction** > **Device limit restriction**.
2. On the **Basics** page, give the restriction a **Name** and optional **Description**.
3. Choose **Next** to go to the **Device limit** page.
4. For **Device limit**, select the maximum number of devices that a user can enroll.
    ![Screen cap for choosing device limit](./media/enrollment-restrictions-set/choose-device-limit.png)
5. Choose **Next** to go to the **Scope tags** page.
6. On the **Scope tags** page, optionally add the scope tags you want to apply to this restriction. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md). 
7. Choose **Next** to go to the **Assignments** page.
8. Choose **Select groups to include** and then use the search box to find groups that you want to include in this restriction. The restriction applies only to groups to which it's assigned. If you don't assign a restriction to at least one group, it won't have any effect. Then choose **Select**. 
    ![Screen cap for selecting groups](./media/enrollment-restrictions-set/select-groups-device-limit.png)
9. Select **Next** to go to the **Review + create** page.
10. Select **Create** to create the restriction. The new restriction is appears in your list of restrictions and is given a higher priority than the default policy. For information about changing the priority level, see [Change restriction priority](enrollment-restrictions-set.md#change-restriction-policy)(in this article).  

## Apply filters to enrollment restriction and ESP policies 

You can use assignment filters to include and exclude additional devices from certain group-targeted policies. Enrollment restrictions and ESP policies both support the use of assignment filters.   

For example, you can use a filter to allow personal Windows devices to enroll while blocking devices that run a specific operating system SKU. To achieve this outcome, apply a preconfigured filter to your enrollment restiction assignments. The filter needs to have the `operatingSystemSKU` property in its rules. Example steps:  

  1. Create a platform enrollment restriction policy for Windows.  
  2. In the platform settings, select the option that allows personally-owned devices to enroll. 
  3. In the assignments settings, select the groups you want to assign.
  4. Select **Edit filter** and then apply your preconfigured filter that contains the `operatingSystemSKU` property. The applied property blocks devices running Windows 10 Home edition. 

For more information about creating filters, see [Create a filter](../fundamentals/filters.md). 

### Supported filter properties  

Enrollment restrictions support fewer filter properties than other group-targeted policies. This is because devices are not yet enrolled, so Intune doesn't have the device info to support all properties. You'll see the limited selection of properties when you:  

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

For more information about these properties, see [device properties](../fundamentals/filters-device-properties.md#device-properties). Filters cannot be used with Android enrollment restrictions.  

## Edit enrollment restrictions  

Edits are applied to new enrollments and do not affect devices that are already enrolled.  

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Enrollment restrictions** > choose the restriction that you want to change > **Properties**.
2. Choose **Edit** next to the settings that you want to change.
3. On the **Edit** page, make the changes that you want and proceed to the **Review + save** page, then choose **Save**.  

## Change restriction priority  

When a group is assigned multiple restrictions, the priority level determines which policy gets applied. The restriction with highest priority (*1* being the highest priority position) is applied and the other restrictions are disregarded. For example:  

1. Joe belongs to two user groups in Intune: Group A and Group B. 
2. Group A is assigned a restriction policy. Its priority level is 5.
3. Group B is assigned a restriction policy. The priority level is 2.
4. Joe is subject only to the priority 2 restrictions.

When you create a restriction, it's added to the list just above the default. You can change the priority of non-default restrictions.  

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Devices** > **Enroll devices** > **Enrollment restrictions**.
2. Select **Device type restrictions** or **Device limit restrictions** to view the priority list.               
3. In the list, hover over any restriction in the **Priority** column. When you see three vertical dots appear, select and drag the priority to the desired position in the list.   


>[!NOTE]
>Enrollment restrictions are applied to users. For enrollment scenarios that are not user-driven, such as Windows Autopilot self-deploying mode, Intune only enforces the default restrictions targeted to all users.  
 

## View enrollment reports
You can use the following reports to troubleshoot issues with enrollment restrictions and enrollment status page assignments:  
- Enrollment failures report  
- Troubleshooting + support page  
- Device enrollment page  

This section describes the purpose of each troubleshooting resource and where to find them in the admin center.  

### Enrollment failures report  
Use the enrollment failures report to view enrollment failures for all users or for select users. This report shows each failed enrollment attempt along with the date it occurred, reason for failure, OS, OS version, username, and enrollment method.  

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Devices** > **Monitor** > **Enrollment failures**.
2. Select **All users** or **Select user**, depending on the scenario you are troubleshooting.
3. Select a row in the table for more details about the failure and recommended remediation steps.  

    > [!div class="mx-imgBorder"]
    > ![Example image of the enrollment failures report, showing the enrollment failure details for a selected row.](./media/enrollment-restrictions-set/enrollment-failure-report-details-2112.png)  

### Troubleshooting + support page  
Use the enrollment failures report on the Troubleshooting + support page to view enrollment failures for a select user. This report shows every failed enrollment attempt the user encountered along with the date it occurred, reason for failure, OS, OS version, username, and enrollment method. You can also view other data about the user on this page, including all assignments, devices, and app protection statuses they're associated with.    

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Troubleshooting + support** > **Select user**.
2. Choose a user > **Select**. 
3. Under **Enrollment failures**, select a row to view more details about the failure and recommended remediation steps.  

### Device enrollment page
The device enrollment page shows the enrollment policies (both enrollment restriction and enrollment status page policies) applied to a device when it was first enrolled in Microsoft Intune. Use this report to help pinpoint the source of the failure, such as an unexpected policy, target, or filter. Data is available for iOS/iPadOS, macOS, and Windows devices, and includes: 

  * Profile name
  * User principal name
  * Profile type (either enrollment status page or device type enrollment restriction)
  * Priority
  * Target (either user or device) 
  * Filters, with a link to the filter evaluation results (only available if the enrollment policy was assigned using an assignment filter)  

To access report data:   

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Devices** > **All devices**.
2. Select an enrolled iOS/iPadOS, macOS, or Windows device.  
3. Under **Monitor**, select **Enrollment**.  
4. Review the report data. 

    > [!div class="mx-imgBorder"]
    > ![Example image of the Device enrollment page, showing a table of enrollment profiles.](./media/enrollment-restrictions-set/enrollment-page-report-2112.png)  

>[!NOTE]
>Report data is only available for devices enrolled after the Microsoft Intune 2112 service release. No results are available for devices enrolled prior to that release.  

