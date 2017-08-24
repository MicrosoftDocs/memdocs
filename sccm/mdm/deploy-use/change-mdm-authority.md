---
# required metadata

title: "Change your MDM authority | Microsoft Docs"
description: "Learn how to change the MDM authority from Configuration Manager (hybrid) to Intune standalone or vice versa."
keywords:
author: dougeby
manager: angrobe
ms.date: 06/02/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology:
    - configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
# Change your MDM authority
Beginning in Configuration Manager version 1610 and Microsoft Intune version 1705, you can change your MDM authority without having to contact Microsoft Support, and without having to unenroll and reenroll your existing managed devices.

## Change the MDM authority to Intune standalone
Use this section to change an existing Microsoft Intune tenant configured from the Configuration Manager console (hybrid) to Intune standalone without having to unenroll and reenroll existing managed devices.

### Key Considerations
After you change to the new MDM authority, there will likely be transition time (up to 8 hours) before the device checks in and synchronizes with the service. You will be required to configure settings in the new MDM authority (Intune standalone) to ensure that enrolled devices will continue to be managed and protected after the change. Note the following:
- Devices must connect with the service after the change so that the settings from the new MDM authority (Intune standalone) will replace the existing settings on the device.
- After you change the MDM authority, some of the basic settings (such as profiles) from the previous MDM authority (hybrid) will remain on the device for up to 7 days. It is recommended that you configure apps and settings (policies, profiles, apps, etc.) in the new MDM authority as soon as possible and deploy the settings to the user groups that contains users who have existing enrolled devices. As soon as a device connects to the service after the change in MDM authority, it will receive the new settings from the new MDM authority and prevent gaps in management and protection. Any newly targeted policies will override existing policies on the device.
- After you change to the new MDM authority, the compliance data in the Microsoft Intune administration console can take up to a week to accurately report. However, the compliance states in Azure Active Directory and on the device will be accurate so the device will still be protected.
- Devices that don't have associated users (typically, when you have iOS Device Enrollment Program or bulk enrollment scenarios), and you perform an MDM reset, then those devices are not migrated to the new MDM authority. For those devices, you will need to call support for assistance to move the devices to the new MDM authority.

### Prepare to change the MDM authority to Intune standalone
Review the following information to prepare for the change to the MDM authority:
- You must have Configuration Manager version 1610 or higher for the option to change the MDM authority to be available.
- It can take up to 8 hours for a device to connect to the service after you change to the new MDM authority.
- Make sure all users that are currently managed by hybrid have an Intune/EMS license specifically assigned to them prior to the change in MDM authority. This will ensure that the user and their devices will be managed by Intune standalone after the change in MDM authority. For more information, see [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Make sure that the Admin user account has an Intune/EMS license assigned and confirm that the Admin user account can sign in to Intune before the change to the MDM authority. The MDM authority should display **Set to Configuration Manager** (hybrid tenant) in the Microsoft Intune administration console prior to the change in MDM authority.
- In the Configuration Manager console, remove all Device Enrollment Manager roles. Go to **Administration** > **Cloud Services** > **Microsoft Intune Subscriptions**, select the Microsoft Intune subscription, click **Properties**, click the **Device Enrollment Manager** tab, and remove all Device Enrollment Manager roles.
- In the Configuration Manager console, remove existing device categories. Go to **Assets and Compliance** > **Overview** > **Device Collections**, choose **Manage Device Categories**, and remove existing device categories.
- There should be no noticeable impact to end-users during the change in MDM authority. However, you might want to communicate this change to users to make sure that their devices are powered on and that they connect with the service soon after the change. This will ensure that as many devices as possible will connect and register with the service through the new authority as soon as possible.
- If you are using Configuration Manager (hybrid tenant) to manage iOS devices prior to the change in MDM authority, you must make sure that the same Apple Push Notification service (APNs) certificate that was previously used in Configuration Manager is renewed and used to set up the tenant again in Intune standalone.

    > [!IMPORTANT]  
    > If a different APNs certificate is used for Intune standalone, then ALL previously enrolled iOS devices will become unenrolled and you will have to go through the process to reenroll them. Prior to making the MDM authority change, make sure that you know exactly what APNs certificate was used to manage iOS devices in Configuration Manager. Find the same certificate listed in Apple Push Certificates Portal (https://identity.apple.com) and make sure the user whose Apple ID was used to create the original APNs certificate is identified and available to renew the same APNs certificate as part of the change to the new MDM authority.  

### Change the MDM authority to Intune standalone
The process to change the MDM authority to Intune standalone includes the following high-level steps:  
- In the Configuration Manager console, use the **Change MDM Authority to Microsoft Intune** option to remove the existing Microsoft Intune subscription.
- In the Microsoft Intune administration console, set the new MDM authority to **Intune**.
- Configure the Apple APNs certificate by using the same APNs certificate that you renewed.
- In the Microsoft Intune administration console, configure and deploy new settings and apps from the new MDM authority (Intune).
- The next time devices connect to the service, it will synchronize and receive the new settings from the new MDM authority.

#### To change the MDM authority to Intune standalone
1.	In the Configuration Manager console, go to **Administration** &gt; **Overview** &gt; **Cloud Services** &gt; **Microsoft Intune Subscription**, and delete your existing Intune Subscription.
2.	Select **Change MDM Authority to Microsoft Intune**, and then click **Next**.

    ![Download the APNs certificate request](/sccm/mdm/deploy-use/media/mdm-change-delete-subscription.png)
3.	Sign-in to the Intune tenant that you originally used when you set the MDM authority in Configuration Manager.
4.	Click **Next** and complete the wizard.
5.	The MDM authority is now reset. The Intune Subscription should no longer be displayed in the Microsoft Intune Subscriptions node of the Configuration Manager console.
6.	Login to the [Microsoft Intune administration console](http://manage.microsoft.com) using the same Intune tenant you used earlier.
7.	Confirm that the MDM authority has been reset, and then set the MDM authority as **Microsoft Intune**. After you change the MDM authority, you should see it reflected in the console. For more information, see [How to set the MDM authority](https://docs.microsoft.com/en-us/intune/deploy-use/prerequisites-for-enrollment#step-2-set-mdm-authority).
<!-- [Azure portal](https://docs.microsoft.com/en-us/intune-azure/enroll-devices/set-mdm-authority) -->


### Configure the APNs certificate
When you have iOS devices, you must configure the APNs certificate in Intune.

#### To configure the APNs certificate
1.	Download the APNs certificate request.
    <!--The process is different depending on how you connect to Intune:
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment** &gt; **Apple MDM Push Certificate**, and then select **Download your CSR** to download and save the .csr file locally.   
    <br/>
    **Microsoft Intune administration console**   -->
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Download the APNs certificate request**. Save the certificate signing request (.csr) file locally.
    > [!IMPORTANT]    
    > You must download a new certificate signing request. Do not use an existing file or it will fail.

    ![Download the APNs certificate request](/sccm/mdm/deploy-use/media/mdm-change-download-apns-certificate.png)

2.	Go to the [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844), and sign in with the **same** Apple ID that was used to previously create and renew the APNs certificate that you used in Configuration Manager (hybrid).

    ![Apple Push Certificates Portal sign in page](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.	Select the APNs certificate that you used in Configuration Manager (hybrid), and then click **Renew**.   

    ![Renew APNs dialog box](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.	Select the APNs certificate signing request (.csr) file that you downloaded locally, and then click **Upload**.

    ![Apple Push Certificates Portal sign in page](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)
  
5.	Select the same APNs, and then click **Download**. Download the APNs (.pem) certificate, and save the file locally.  

    ![Apple Push Certificates Portal sign in page](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.	Upload the renewed APNs certificate to the Intune tenant using the same Apple ID as before.
<!--The process is different depending on how to connect to Intune:  
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment**  &gt; **Apple MDM Push Certificate**, enter your Apple ID in step 3, select the certificate (.pem) file in step 4, and then click **Upload**.     
    <br/>
    **Microsoft Intune administration console**    -->
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Upload the APNs certificate**. Go to the certificate (.pem) file, choose **Open**, and then enter your **Apple ID**.   

    ![Upload the APNs certificate](/sccm/mdm/deploy-use/media/mdm-change-upload-apns-certificate.png)

### Next steps
After the change in MDM authority is complete, review the following steps:
- When the Intune service detects that a tenant’s MDM authority has changed, it will send out a notification message to all the enrolled devices to check-in and synchronize with the service (this is outside of the regularly scheduled check-in). Therefore, after the MDM authority for the tenant has been changed from hybrid to Intune standalone, all the devices that are powered on and online will connect with the service, receive the new MDM authority, and be managed by Intune standalone going forward. There will be no interruption to the management and protection of these devices.
- Devices that are either powered off or offline during (or shortly after) the change in MDM authority will connect to and synchronize with the service under the new MDM authority when they are powered on and online.  

  iOS devices require additional time to renew and set up the APNs certificate. Therefore, iOS devices will not receive the initial check-in request. Even if iOS devices are powered on and online during (or shortly after) the change in MDM authority, there will be a delay of up to 8 hours (depending on the timing of the next scheduled regular check-in) before iOS devices are registered with the service under the new MDM authority.    

  > [!IMPORTANT]
  > Between the time when you change the MDM authority and when the renewed APNs certificate is uploaded to the new authority, new device enrollments and device check-in for iOS devices will fail. Therefore, it is important that you review and upload the APNs certificate to the new authority as soon as possible after the change in MDM authority.   

- Users can quickly change to the new MDM authority by manually starting a check-in from the device to the service. Users can easily do this by using the Company Portal app and initiating a device compliance check.
- To validate that things are working correctly after devices have checked-in and synchronized with the service after the change in MDM authority, look for the devices the [Microsoft Intune administration console](http://manage.microsoft.com). The devices that were previously managed by Configuration Manager (hybrid) will now be displayed as managed devices.    
- There is an interim period when a device is offline during the change in MDM authority and when that device checks in to the service. To help ensure that the device remains protected and functional during this interim period, the following will remain on the device for up to 7 days (or until the device connects with the new MDM authority and receives new settings that will overwrite the existing ones):
    - E-mail profile
    - VPN profile
    - Cert profile
    - Wi-Fi profile
    - Configuration profiles
- Make sure the new settings that are intended to overwrite existing settings have the same name as the previous ones to ensure that the old settings are overwritten. Otherwise, the devices might end up with redundant profiles and policies.
    > [!TIP]   
    > As a best practice, you should create all management settings and configurations, as well as deployments, shortly after the change to the MDM authority has completed. This will help ensure that devices are protected and actively managed during the interim period.   
-  After you change the MDM authority, perform the following steps to validate that new devices are enrolled successfully to the new authority:   
    - Enroll a new device
    - Make sure the newly enrolled device shows up in the Intune administration console.
    - Perform an action, such as Remote Lock, from the administration console to the device. If it is successful, the device is being managed by the new MDM authority.
- If you have issues with specific devices, you can unenroll and reenroll the devices to get them connected to the new authority and managed as quickly as possible.

<!-- After the change in MDM authority and devices check-in with the service, note the following:      - The updated compliance status of devices will only display in the Azure portal immediately.
- There will be a delay for compliance status of devices to display in the Intune administrative console.-->


## Change the MDM authority to Configuration Manager (hybrid)
Use this section to change an existing Microsoft Intune tenant configured from Intune and with the MDM authority set to **Microsoft Intune** (standalone) to **Configuration Manager** (hybrid) without having to unenroll and reenroll existing managed devices.

### Key Considerations
After you switch to the new MDM authority, there will likely be transition time (up to 8 hours) before the device checks in and synchronizes with the service. You will be required to configure settings in the new MDM authority (hybrid) to ensure that enrolled devices will continue to be managed and protected after the change. Note the following:
- Devices must connect with the service after the change so that the settings from the new MDM authority (Intune standalone) will replace the existing settings on the device.
- After you change the MDM authority, some of the basic settings (such as profiles) from the previous MDM authority (Intune standalone) will remain on the device for up to 7 days or until the device connects to the service for the first time. It is recommended that you configure apps and settings (policies, profiles, apps, etc.) in the new MDM authority (hybrid) as soon as possible and deploy the settings to the user groups that contains users who have existing enrolled devices. As soon as a device connects to the service after the change in MDM authority, it will receive the new settings from the new MDM authority and prevent gaps in management and protection.
- Devices that don't have associated users (typically, when you have iOS Device Enrollment Program or bulk enrollment scenarios), and you perform an MDM reset, then those devices are not migrated to the new MDM authority. For those devices, you will need to call support for assistance to move the devices to the new MDM authority.

### Prepare to change the MDM authority to Configuration Manager (hybrid)
Review the following information to prepare for the change to the MDM authority:
- You must have Configuration Manager version 1610 or higher for the option to change the MDM authority to be available.
- It can take up to 8 hours for a device to connect to the service after you change to the new MDM authority.
- Create a Configuration Manager user collection with all users currently managed by Intune Standalone that you will use when you set up the Intune subscription in the Configuration Manager console. This will help ensure that the user and their devices will have a Configuration Manager license assigned and be managed in the hybrid environment after the change to the MDM authority.
- Make sure that the IT Admin user is in this user collection too.  
- Before the change, the MDM Authority will show as **Set to Microsoft Intune** (standalone) in the Intune administration console.
- The MDM authority should display **Set to Microsoft Intune** (standalone tenant) in the Microsoft Intune administration console prior to the change in MDM authority.
    > [!NOTE]    
    > If your MDM authority displays **Managed by Intune and Office 365**, then your Office 365 managed MDM devices will no longer be managed when you change your MDM authority to **Configuration Manager** (hybrid). We recommend that you license those users for Intune or Enterprise Mobility Suite before you change the MDM authority.   

- In the [Microsoft Intune administration console](http://manage.microsoft.com), remove the Device Enrollment Manager role. For details, see [Delete a device enrollment manager from Intune](/intune-classic/deploy-use/enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune#delete-a-device-enrollment-manager-from-intune).
- Turn off any device group mappings that are configured. For details, see [Categorize devices with device group mapping in Microsoft Intune](/intune-classic/deploy-use/categorize-devices-with-device-group-mapping-in-microsoft-intune).
- There should be no noticeable impact to end-users during the change in MDM authority. However, you might want to communicate this change to users to make sure that their devices are powered on and that they connect with the service soon after the change. This will ensure that as many devices as possible will connect and register with the service through the new authority as soon as possible.
- If you are using Intune standalone to manage iOS devices prior to the change in MDM authority, you must make sure that the same Apple Push Notification service (APNs) certificate that was previously used in Intune is renewed and used to set up the tenant again in Configuration Manager (hybrid).    

    > [!IMPORTANT]  
    > If a different APNs certificate is used for hybrid, then ALL previously enrolled iOS devices will become unenrolled and you will have to go through the process to reenroll them. Prior to making the MDM authority change, make sure that you know exactly what APNs certificate was used to manage iOS devices in Intune. Find the same certificate listed in Apple Push Certificates Portal (https://identity.apple.com) and make sure the user whose Apple ID was used to create the original APNs certificate is identified and available to renew the same APNs certificate as part of the change to the new MDM authority.  

### Change the MDM authority to Configuration Manager
The process to change the MDM authority to Configuration Manager (hybrid) includes the following high-level steps:  
- In the Configuration Manager console, add the Microsoft Intune subscription.
- Configure the Apple APNs certificate by using the same APNs certificate that you renewed.
- In the Configuration Manager console, configure and deploy new settings and apps from the new MDM authority (hybrid).
- The next time devices connect to the service, it will synchronize and receive the new settings from the new MDM authority.

#### To change the MDM authority to Configuration Manager
1.	In the Configuration Manager console, go to **Administration** &gt; **Overview** &gt; **Cloud Services** &gt; **Microsoft Intune Subscription**, and select to add an Intune Subscription.
2.	Sign-in to the Intune tenant that you originally used when you set the MDM authority in Intune, and click **Next**.
3.	Select **Change my MDM Authority to Configuration Manager**, and click **Next**.
4.  Select the user collection that will contain all of the users that will continue to be managed by the new hybrid MDM authority.
5.  Click **Next** and complete the wizard.  
5.	The MDM authority is now changed to **Configuration Manager**.
6.	Login to the [Microsoft Intune administration console](http://manage.microsoft.com) using the same Intune tenant and confirm that the MDM authority has been changed to **Set to Configuration Manager**.


### Enable iOS enrollment
When you have iOS devices, you must configure the APNs certificate in Configuration Manager.

#### To enable iOS enrollment and configure the APNs certificate

1. **Download a certificate signing request**

    1.  In the Configuration Manager console, go to **Administration** &gt; **Cloud Services** &gt; **Microsoft Intune Subscriptions**, and select **Create APNs certificate request** to open the **Request Apple Push Notification Service Certificate Signing Request** dialog box.  
    2.  **Browse** to the path to save the new certificate signing request (.csr) file. Save the certificate signing request (.csr) file locally.  
    3.  Click **Download**. The new Microsoft Intune .csr file downloads and is saved by Configuration Manager.   

    > [!IMPORTANT]
    > You must download a new certificate signing request. Do not use an existing file or it will fail.  

2.	Go to the [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844), and sign in with the **same** Apple ID that was used to previously create and renew the APNs certificate that you used in Intune standalone.

    ![Apple Push Certificates Portal sign in page](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.	Select the APNs certificate that you used in Intune standalone, and then click **Renew**.   

    ![Renew APNs dialog box](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.	Select the APNs certificate signing request (.csr) file that you downloaded locally, and then click **Upload**.

    ![Apple Push Certificates Portal sign in page](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)
  
5.	Select the same APNs, and then click **Download**. Download the APNs (.pem) certificate, and save the file locally.  

    ![Apple Push Certificates Portal sign in page](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.	Upload the renewed APNs certificate to the hybrid tenant using the same Apple ID as before.

    1.  In the Configuration Manager console, go to **Administration** &gt; **Cloud Services** &gt; **Microsoft Intune Subscription**, and choose **Configure Platforms** &gt; **iOS**.  
    2.  In the **Microsoft Intune Subscription Properties** dialog box, select the **APNs Certificate** tab and click to select the **Enable iOS and MAC OS X (MDM) enrollment** checkbox.  
    3.  Click **Browse**, and go to the APNs certificate (.cer) file downloaded from Apple. Configuration Manager displays the APNs certificate information. Click **OK** to save the APNs certificate to Intune.  

        ![Intune Subscription properties page - iOS](/sccm/mdm/deploy-use/media/mdm-change-subscription-properties-ios.png)

### Enable Android enrollment
1. In the Configuration Manager console, go to **Administration** &gt; **Cloud Services** &gt; **Microsoft Intune Subscription**, and choose **Configure Platforms** &gt; **Android**.  
2. Select **Enable Android enrollment** and click **OK**.

### Enable Windows enrollment
1. In the Configuration Manager console, go to **Administration** &gt; **Cloud Services** &gt; **Microsoft Intune Subscription**, and choose **Configure Platforms** &gt; **Windows**.  
2. Select **Enable Windows enrollment** and click **OK**.

### Enable Windows Phone enrollment
1. In the Configuration Manager console, go to **Administration** &gt; **Cloud Services** &gt; **Microsoft Intune Subscription**, and choose **Configure Platforms** &gt; **Windows Phone**.  
2. Select the platform that you want to enable, and click **OK**.


### Next steps
After the change in MDM authority is complete, review the following steps:
- When the Intune service detects that a tenant’s MDM authority has changed, it will send out a notification message to all the enrolled devices to check-in and synchronize with the service (this is outside of the regularly scheduled check-in). Therefore, after the MDM authority for the tenant has been changed from Intune standalone to hybrid, all the devices that are powered on and online will connect with the service, receive the new MDM authority, and be managed by hybrid going forward. There will be no interruption to the management and protection of these devices.
- Even for devices that are powered on and online during (or shortly after) the change in MDM authority, there will be a delay of up to 8 hours (depending on the timing of the next scheduled regular check-in) before devices are registered with the service under the new MDM authority.    

  > [!IMPORTANT]
  > Between the time when you change the MDM authority and when the renewed APNs certificate is uploaded to the new authority, new device enrollments and device check-in for iOS devices will fail. Therefore, it is important that you review and upload the APNs certificate to the new authority as soon as possible after the change in MDM authority.

- Users can quickly change to the new MDM authority by manually starting a check-in from the device to the service. Users can easily do this by using the Company Portal app and initiating a device compliance check.
- To validate that things are working correctly after devices have checked-in and synchronized with the service after the change in MDM authority, look for the devices the Configuration Manager console. The devices that were previously managed by Intune will now be displayed as managed devices in the Configuration Manager console.    
- There is an interim period when a device is offline during the change in MDM authority and when that device checks in to the service. To help ensure that the device remains protected and functional during this interim period, the following will remain on the device for up to 7 days (or until the device connects with the new MDM authority and receives new settings that will overwrite the existing ones):
    - E-mail profile
    - VPN profile
    - Cert profile
    - Wi-Fi profile
    - Configuration profiles
- After you change to the new MDM authority, the compliance data in the Microsoft Intune administration console can take up to a week to accurately report. However, the compliance states in Azure Active Directory and on the device will be accurate so the device will still be protected.
- Make sure the new settings that are intended to overwrite existing settings have the same name as the previous ones to ensure that the old settings are overwritten. Otherwise, the devices might end up with redundant profiles and policies.
    > [!TIP]   
    > As a best practice, you should create all management settings and configurations, as well as deployments, shortly after the change to the MDM authority has completed. This will help ensure that devices are protected and actively managed during the interim period.   
-  After you change the MDM authority, perform the following steps to validate that new devices are enrolled successfully to the new authority:   
    - Enroll a new device
    - Make sure the newly enrolled device shows up in the Configuration Manager console.
    - Perform an action, such as Remote Lock, from the administration console to the device. If it is successful, the device is being managed by the new MDM authority.
- If you have issues with specific devices, you can unenroll and reenroll the devices to get them connected to the new authority and managed as quickly as possible.
