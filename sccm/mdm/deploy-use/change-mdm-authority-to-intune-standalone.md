---
# required metadata

title: [Change the MDM Authority to Intune standalone | Microsoft Docs]
description: Learn how to change the MDM Authority from Configuration Manager (hybrid) to Intune standalone.
keywords:
author: dougeby
manager: angrobe
ms.date: 10/06/2016
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
# Change the MDM Authority to Intune standalone
Use this topic to change an existing Microsoft Intune tenant configured from the Configuration Manager console (hybrid) to Intune standalone without having to unenroll and reenroll existing managed devices.

## Key Considerations
After you switch to the new MDM authority, there will likely be transition time (up to 8 hours) before the device checks in and synchronizes with the service.  You will be required to configure settings in the new MDM authority (Intune standalone) to ensure that enrolled devices will continue to be managed and protected after the switch. Note the following:
- Devices must check-in with the service after the switch so that the settings from the new authority (Intune standalone) will replace the existing settings on the device.
- After you change the MDM Authority, some of the basic settings (such as profiles) from the previous authority (hybrid) will remain on the device for up to 7 days or until the device connects to the service (Intune standalone) for the first time.  

It is recommended that you configure settings (policies, profiles, apps, etc.) in the new MDM Authority as soon as possible and deploy the settings to the user groups that contains users who have existing enrolled devices. As soon as a device connects to the service after the change in MDM Authority, it will receive the new settings from the new MDM Authority and prevent gaps in management and protection.

## Prepare to change the MDM Authority to Intune standalone
Review the following information to prepare for the process to change the MDM Authority:
- You will use the self-service function in the Configuration Manager console to change the MDM Authority. You must use Configuration Manager version 1610 or higher for this option to be available.
- Because it can take up to 8 hours for a device to check in, consider changing the MDM Authority during non-working hours. This will help to ensure that there is enough time to allow for the existing enrolled devices to check-in, detect the change in MDM authority, and then synchronize with the new authority and receive the management settings.
- Make sure all users that are currently managed by hybrid has an Intune/EMS license specifically assigned to them prior to the switch.  This will ensure that the user and their devices will be managed by Intune standalone after the change in MDM Authority.
- Make sure that the Admin user account has an Intune/EMS license assigned and confirm that the Admin user account can sign in to Intune before the change to the MDM Authority. The MDM Authority should display Set to Configuration Manager (hybrid tenant) in the Microsoft Intune administration console prior to the change in MDM Authority.
- There should be no noticeable impact to end-users during the change in MDM Authority. However, you might want to communicate this change to users to make sure that their devices are powered on and that they synchronize with the service soon after the change. This will ensure that as many devices as possible will connect and register with the service through the new authority as soon as possible.
- If you are using Configuration Manager (hybrid tenant) to manage iOS devices prior to the change in MDM Authority, you must make sure that the same Apple Push Notification service (APNs) certificate that was previously used in Configuration Manager is renewed and used to set up the tenant again in Intune standalone.
> [!IMPORTANT]  
> If a different APNs certificate is used for Intune standalone, then ALL previously enrolled iOS devices will become un-enrolled and you will have to go through the process to re-enroll them. Prior to making the MDM Authority change, make sure that you know exactly what APNs certificate was used to manage iOS devices in Configuration Manager. Find the same certificate listed in Apple Push Certificates Portal (https://identity.apple.com) and make sure the user whose Apple ID was used to create the original APNs certificate is identified and available to renew the same APNs certificate as part of the change to the new MDM Authority.  

## Change the MDM Authority to Intune standalone
You change the MDM Authority in the Configuration Manager console. The process includes the following high-level steps:  
- In the Configuration Manager console, use the Change MDM Authority to Microsoft Intune option to remove the existing Microsoft Intune subscription.
- In the Microsoft Intune administration console, set the new MDM Authority to Intune.
- Configure the Apple APNs certificate by using the same APNs certificate that you renewed.
- In the Microsoft Intune administration console, configure and deploy new settings and apps from the new MDM Authority (Intune).
- he next time devices connect to the service, it will synchronize and receive the new settings from the new MDM Authority.

#### To change the MDM Authority to Intune standalone
1.	In the Configuration Manager console, go to **Administration** &gt; **Overview** &gt; **Cloud Services** &gt; **Microsoft Intune Subscription**, and delete your existing Intune Subscription.
2.	Select **Change MDM Authority to Microsoft Intune**, and then click **Next**.
3.	Sign-in to the Intune tenant that you originally used when you set the MDM Authority in Configuration Manager.
4.	Click **Next** and complete the wizard.
5.	The MDM Authority is now reset. The Intune Subscription should no longer be displayed in the Microsoft Intune Subscriptions node of the Configuration Manager console.
6.	Login to Microsoft Intune using the same Intune tenant you used earlier.
7.	Confirm that the MDM Authority has been reset, and then set the MDM Authority as **Microsoft Intune**. After you change the MDM Authority, you should see it reflected in the console. For more information about how to set the MDM Authority, see one of the following:
    - [Azure portal](https://docs.microsoft.com/en-us/intune-azure/enroll-devices/set-mdm-authority)
    - [Microsoft Intune administration console](https://docs.microsoft.com/en-us/intune/deploy-use/prerequisites-for-enrollment#step-2-set-mdm-authority)

## Configure the APNs certificate
When you have iOS devices, you must configure the APNs certificate in Intune. There are procedures to do this in the Intune administration console and Azure portal. Use the procedure that is most relevant for you.  

#### To configure the APNs certificate from the Azure Portal
1.	Download the APNs certificate request. The process is different depending on how you connect to Intune:
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment** &gt; **Apple MDM Push Certificate**, and then select **Download your CSR** to download and save the .csr file locally.   
    <br/>
    **Microsoft Intune administration console**    
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Download the APNs certificate request**. Save the certificate signing request (.csr) file locally.

2.	Go to the [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844), and sign in with the **same** Apple ID that was used to previously create and renew the APNs certificate that you used in Configuration Manager (hybrid).

    ![Apple Push Certificates Portal sign in page](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.	Select the APNs certificate that you used in Configuration Manager (hybrid), and then click **Renew**.   

    ![Renew APNs dialog box](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.	Select the APNs certificate signing request (.csr) file that you downloaded locally, and then click **Upload**.

    ![Apple Push Certificates Portal sign in page](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)
  
5.	Select the same APNs, and then click **Download**. Download the APNs (.pem) certificate, and save the file locally.  

    ![Apple Push Certificates Portal sign in page](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.	Upload the renewed APNs certificate to the Intune tenant using the same Apple ID as before. The process is different depending on how to connect to Intune:  

    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment**  &gt; **Apple MDM Push Certificate**, enter your Apple ID in step 3, select the certificate (.pem) file in step 4, and then click **Upload**.     
    <br/>
    **Microsoft Intune administration console**    
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Upload the APNs certificate**. Go to the certificate (.pem) file, choose **Open**, and then enter your **Apple ID**.

## Next steps and validation
After the change in MDM authority is complete, review the following to validate and confirm that the change has completed successfully.
- When the Intune service detects that a tenant’s MDM Authority has changed, it will send out a notification message to all the enrolled devices to check-in and synchronize with the service (this is outside of the regularly scheduled check-in). Therefore, after the MDM Authority for the tenant has been changed from hybrid to Intune standalone, all the devices that are powered on and online will connect with the service, receive the new MDM Authority, and going forward will be managed by Intune standalone.  In this case, there will be no interruption to the management and protection of these devices.
- Devices that are either powered off or offline during (or shortly after) the change in MDM Authority will connect to and synchronize with the service under the new MDM Authority when they are powered on and online.  
    iOS devices require additional time to renew and set up the APNs certificate. Therefore, iOS devices will not receive the initial check-in request. Even if iOS devices are powered on and online during (or shortly after) the change in MDM Authority, there will be a delay of up to 8 hours (depending on the timing of the next scheduled regular check-in) before iOS devices are registered with the service under the new MDM Authority.
    > [!NOTE]
    > Between the time when you change the MDM Authority and when the renewed APNs certificate is uploaded to the new authority, new enrollment and device check-in for iOS devices will fail. Therefore, it is important that you review and upload the APNs certificate to the new authority as soon as possible after the change in MDM Authority.  

- One way for some of the users and their devices to expedite the change to the new authority will be for the users do manually initiate a check-in from the device to the service.  Users can easily do this by using the Company Portal app and initiating a device compliance check.    
- To validate that things are working correctly after devices have checked in and synchronized with the service after the change in MDM Authority, look for the devices in the Intune administrative console or Azure portal. The devices that were previously managed by Configuration Manager (hybrid) will now be displayed in the Intune administrative console as managed devices. After the change in MDM Authority and devices check-in with the service, note the following:
    - Devices will show up in both the Intune administrative console and Azure portal.
    - The updated compliance status of devices will only show up in the Azure portal immediately. There will be a delay for compliance status of devices to display in the Intune administrative console.
- There is an interim period when a device is offline during the change in MDM Authority and when that device checks in to the service. To help ensure that the device remains protected and functional during this interim period, the following will remain on the device for up to 7 days (or until the device connects with the new authority and receives new settings that will overwrite the existing ones):
    - E-mail profile
    - VPN profile
    - Cert profile
    - Wi-Fi profile
    - Configuration profiles
- Make sure the new settings that are intended to overwrite existing settings have the same name as the previous ones to ensure that the old settings are overwritten. Otherwise, the devices might end up with redundant profiles and policies.
    > [!TIP]   
    > As a best practice, you should create all management settings and configurations, as well as deployments, after the change to the MDM Authority has completed. This will help ensure that devices are protected and actively managed during the interim period.
-  After you change the MDM Authority, perform the following steps to validate that new devices are enrolled successfully to the new authority:
    - Enroll a new device
    - Make sure the newly enrolled device shows up in the Intune administration console
    - Perform an action, such as Remote Lock, from the administration console to the device. If it is successful, the device is being managed by the new MDM Authority.
- If you have issues with specific devices, you can un-enroll and re-enroll the devices to get them connected to the new authority and managed as quickly as possible.
