---
# required metadata

title: Add corporate identifiers to Intune
description: Add corporate identifiers (enrollment method, IMEI, and serial numbers) to Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/07/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 566ed16d-8030-42ee-bac9-5f8252a83012

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

# Identify devices as corporate-owned  

**Applies to**: 
- iOS/iPadOS  
- Android  

Ensure that corporate devices are marked as *corporate-owned* as soon as they enroll by adding their corporate identifiers ahead of time in the Microsoft Intune admin center. Corporate devices unlock more device management capabilities than personal devices. For example, Microsoft Intune can collect more information about corporate-owned devices for you, such as full phone number and app inventory. 

You can upload a file of corporate identifiers in the admin center or enter each identifier separately. It isn't necessary to add corporate identifiers for all deployments. During enrollment, Intune automatically assigns corporate-owned status to devices that join to Microsoft Entra via:  

- [Device enrollment manager](device-enrollment-manager-enroll.md) account (all platforms)   
- An Apple device enrollment program such as [Apple School Manager](apple-school-manager-set-up-ios.md), Apple Business Manager, or [Apple Configurator](apple-configurator-enroll-ios.md) (iOS/iPadOS only)  
- Co-management with Microsoft Intune and group policy (GPO) 
- Azure Virtual Desktop  
- Automatic MDM enrollment via provisioning package  
- [Knox Mobile Enrollment](android-samsung-knox-mobile-enroll.md)   
- Android Enterprise management: 
   - [Coporate-owned devices with work profile](./android-corporate-owned-work-profile-enroll.md)  
   - [Fully managed devices](./android-fully-managed-enroll.md)  
   - [Dedicated devices](./android-kiosk-enroll.md).
- Android Open Source Project (AOSP) management:
   - [Corporate-owned user-associated devices](./android-aosp-corporate-owned-user-associated-enroll.md)
   - [Corporate-owned userless devices](./android-aosp-corporate-owned-userless-enroll.md)  
   - [Google Zero Touch](android-dedicated-devices-fully-managed-enroll.md#enroll-by-using-google-zero-touch)  

Microsoft Intune marks devices that register with Microsoft Entra as personal.    

## Role based access control  
You must be an Intune administrator or global administrator to add corporate identifiers, or a custom Intune role assigned corporate device identifier permissions. Permissions include:     

* Update
* Read
* Delete
* Create

## Supported corporate identifiers  

 Before you begin, determine the type of corporate identifiers you want to add. You can add one type of corporate identifier per CSV file. Devices that enroll without corporate identifiers are marked as *personal*.  Intune supports the following identifiers:   

- IMEI    
- Serial number  

### Support by platform 

The following table shows the identifiers supported for each platform. When a device with a matching identifier enrolls, Intune marks it as corporate-owned. 


| Platform | IMEI number | Serial number |   
|---|---|---|
| Windows| Not supported | Not supported | 
| iOS/iPadOS | ✔️ <br></br> Supported in some cases. For more information, see [Step 1: Create CSV file](#step-1-create-csv-file). | ✔️ <br></br> We recommend using a serial number for iOS/iPadOS identification when possible.  |
| macOS | Not supported | ✔️ |
| Android device administrator | ✔️ <br></br> Supported with Android 9 and earlier. | ✔️ <br></br> Supported with Android 9 and earlier. |
| Android Enterprise, personally owned work profile  | ✔️ <br></br> Supported with Android 11 and earlier. | ✔️ <br></br> Supported with Android 11 and earlier. |

<!-- When you upload serial numbers for corporate-owned iOS/iPadOS devices, they must be paired with a corporate enrollment profile. Devices must then be enrolled using either Apple's Automated Device Enrollment or Apple Configurator to have them appear as corporate-owned. -->  

## Step 1: Create CSV file  
Create a list of corporate identifiers and save it as a CSV file. You can add up to 5,000 rows or 5 MB of data per file, whichever comes first. Don't add headers. 

>[!IMPORTANT]
> Remember, only add one type of corporate identifier per CSV file. 

To add corporate identifiers Android and iOS/iPadOS platforms, list one IMEI or serial number per line as shown in the following example.      

```
01234567890123,device details  
02234567890123,device details  
```

Remove all periods, if applicable, from the serial number before you add it to the file. You can add device details after each corporate identifier. Details are limited to 128 characters and are for administrative use only. They don't appear on the device.  

Android and iOS/iPadOS devices can have multiple IMEI numbers. Intune reads and records one IMEI per enrolled device. If you import an IMEI that's different from the one already in Intune, Intune will mark the device as personal. If you import multiple IMEI numbers for the same device, the identifiers that haven't been inventoried appear with an *unknown* enrollment status. 

Android serial numbers are not guaranteed to be unique or present. Check with your device supplier to find out if the serial number is a reliable device ID. Serial numbers reported by the device to Intune might not match the ID shown on the device in Android settings or Android device information. Verify the type of serial number reported by the device manufacturer.  

## Step 2: Add corporate identifiers in admin center  

You can upload a CSV file of corporate identifiers, or manually enter the corporate identifiers in the Microsoft Intune admin center.  

### Upload CSV file  

Upload the CSV file you created in [Step 1: Create CSV file](#step-1-create-csv-file) to add corporate identifiers.   

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Go to **Devices** > **Enrollment**.     
1. Select the **Corporate device identifiers** tab.  
1. Choose **Add** > **Upload CSV file**.  
1. Select the identifier type. Your options:  
   - **IMEI**
   - **Serial**    
1. Under **Import identifiers**, find and select the CSV file. 
1. Wait while Intune validates the CSV file. When the total device identifiers count appears onscreen, validation is complete.   

   > [!TIP]
   > If your import fails, check that the CSV file meets formatting requirements.    

1. Select **Add**, and then look for the success notification at the top of the admin center to confirm that the file is imported.

   > [!NOTE] 
   > A pop-up window prompting you to review duplicate identifiers appears if the CSV file contains corporate identifiers that are already in Intune but have different device details. To resolve the duplicates, select the identifiers that you want to overwrite in Intune. Then select **Ok** to add the identifiers. Intune only compares the first duplicate of each identifier.  

### Manually enter corporate identifiers  

*Applies to Android and iOS/iPadOS*  

Enter corporate identifiers in the Microsoft Intune admin center to add corporate identifiers.  

1. In the Microsoft Intune admin center, go to **Devices** > **Enrollment**.     
1. Select the **Corporate device identifiers** tab.   
1. Choose **Add** > **Enter manually**.  
1. Select the identifier type. Your options:  
   - **IMEI**  
   - **Serial**  
1. Enter the corporate identifier and details. When you're done entering identifiers, select **Add**.  
1. Select **Refresh** to reload your list. The corporate identifiers you added should now be visible.  

   > [!NOTE] 
   > A pop-up window prompting you to review duplicate identifiers appears if your entries contain corporate identifiers that are already in Intune but have different device details. To resolve the duplicates, select the identifiers that you want to overwrite. Then select **Ok** to add the identifiers. Intune only compares the first duplicate of each identifier.  

### Check enrollment status  

Follow up on imported devices to ensure that they enroll in Intune. After you add corporate identifiers, you can see the status of the devices in the admin center:  

* **Enrolled**: The device completed enrollment.  
* **Not contacted**: The device hasn't made contact with the Microsoft Intune service. 
* **Not applicable**: 
* **Failed**: The device did not complete enrollment.  

## Delete corporate identifiers

2. In the admin center, go to **Devices** > **Enrollment**.     
2. Select the **Corporate device identifiers** tab.  
3. Select the device identifiers you want to delete, and choose **Delete**.
4. Confirm the deletion.  

Deleting a corporate identifier for an enrolled device does not change the device's ownership. 

## Change device ownership

To edit a device's identification after enrollment, change its ownership setting in the admin center.  An ownership property appears for each device record in Microsoft Intune.  

1. Go to **Devices** > **All devices**.      
2. Select a device.  
3. Choose **Properties**.  
4. For **Device ownership**,  select **Personal** or **Corporate**.  

   :::image type="content" source="./media/corporate-identifiers-add/device-properties.png" alt-text="Screenshot of the Managed device properties showing Device category and Device ownership options.":::

When you change a device's ownership type from *corporate* to *personal*, Intune deletes all app information previously collected from that device within seven days. If applicable, Intune also deletes the phone number on record. Intune still collects the inventory of apps installed by the IT admin on the device, and a partial phone number. 

When you change the ownership of an iOS/iPad or Android device from *personal* to *corporate*, a push notification is sent through the Company Portal app to inform the device user of the change. To configure push notifications, go to **Tenant administration** > **Customization**. For more information, see [Company Portal - Configuration](../apps/company-portal-app.md#configuration).  

## Block personal devices   

To prevent all personal devices from enrolling, configure an [enrollment platform restriction](create-device-platform-restrictions.md#create-a-device-platform-restriction) for personal devices.  

To confirm the reason for an enrollment failure, go to **Devices** > **Enrollment failures** and look in the table under **Failure reason**. In this case, the reason is **Enrollment restriction not met**.  Select the reason to open failure details.   

## Resources      

For details about International Mobile Equipment Identifiers, see [3GGPP TS 23.003](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=729).  





