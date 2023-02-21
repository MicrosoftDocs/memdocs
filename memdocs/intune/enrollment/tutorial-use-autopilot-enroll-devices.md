---
# required metadata

title: Tutorial - Use Autopilot to enroll devices in Intune
titleSuffix: Microsoft Intune
description: In this tutorial, you'll set up Windows Autopilot to enroll devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/25/2022
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 
Customer intent: As an Intune admin, I want to set up Windows Autopilot so that users can enroll in Intune.

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Tutorial: Use Autopilot to enroll Windows devices in Intune

[Windows Autopilot](../../autopilot/index.yml) simplifies enrolling devices. With Microsoft Intune and Autopilot, you can give new devices to your end users without the need to build, maintain, and apply custom operating system images.

In this tutorial, you'll learn how to:
> [!div class="checklist"]
> * Add devices to Intune
> * Create an Autopilot device group
> * Create an Autopilot deployment profile
> * Assign the Autopilot deployment profile to the device group
> * Distribute Windows devices to users

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

For an overview of Autopilot benefits, scenarios, and prerequisites, see [Overview of Windows Autopilot](/windows/deployment/windows-autopilot/windows-10-autopilot).


## Prerequisites
- [Set up Windows automatic enrollment](quickstart-setup-auto-enrollment.md)
- [Azure Active Directory Premium subscription](/azure/active-directory/active-directory-get-started-premium) <!--&#40;[trial subscription](https://go.microsoft.com/fwlink/?LinkID=816845)&#41;-->


## Add devices

The first step in setting up Windows Autopilot is to add the Windows devices to Intune. All you have to do is create a CSV file and import it into Intune.

1. In any text editor, create a list of comma-separated values (CSV) that identify the Windows devices. Use the following format:
    
    *serial-number*, *windows-product-id*, *hardware-hash*, *optional-Group-Tag*
    
    The first three items are required, but the Group Tag (previously known "order ID") is optional.

2. Save the CSV file.

3. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and go to **Devices** > **Windows** > **Windows Enrollment**. 

4.  Under **Windows Autopilot Deployment Program**, select **Devices**.   

    ![Screenshot of Windows Autopilot devices](./media/enrollment-autopilot/autopilot-import-device.png)  

5. Select **Import**.  

6. The **Add Autopilot devices** pane opens. Choose the **Select a file** folder icon and browse to your CSV file.  

5. Select **Import** to start importing device information. Importing can take several minutes.  

4. After import is complete, return to **Windows Autopilot Deployment Program** > **Devices**, and select **Sync**.   Synchronization might take a few minutes to complete, depending on how many devices you're synchronizing. 

5. Select **Refresh** to see the imported devices.

## Create an Autopilot device group

Next, you'll create a device group and put the Autopilot devices you just loaded into it.

1. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Groups** > **New group**.
2. Configure the settings for your new **Group** as follows:    
    1. For **Group type**, select **Security**.  
    2. For **Group name**, enter *Autopilot Group*.  
    3. For **Group description**, enter *Test group for Autopilot devices*.  
    4. For **Membership type**, select **Assigned**.
    5. Select the link under **Members** to add Autopilot devices to the group. Autopilot devices that aren't yet enrolled are devices where the name equals the serial number of the device.
4. Choose **Create**.  

## Create an Autopilot deployment profile

After creating a device group, you must create a deployment profile so that you can configure the Autopilot devices.

1. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Windows** > **Windows enrollment**. 
2. Select **Deployment Profiles**. 
3. Select **Create profile** > **Windows PC**.  
4. On the **Basics** page, name the profile *Autopilot Profile*. In **Description**, enter *Test profile for Autopilot devices*.
5. Set **Convert all targeted devices to Autopilot** to **Yes**. This setting makes sure that all devices in the list get registered with the Autopilot deployment service. Allow 48 hours for processing.
6. Select **Next**.  
7. Configure the **Out-of-box experience (OOBE)** settings. 
    * **Deployment mode**: Select **User-driven**. Devices with this profile are associated with the user enrolling the device. User credentials are required to enroll the device.
    * **Join to Azure AD as**: Select **Azure AD joined**.
8. Configure the following settings. 
    - **Microsoft Software License Terms**: Select **Hide**.  
    - **Privacy settings**: Select **Show**
    - **User account type**: Select **Standard**.    
 Leave all other settings on the page set to the default.    
9. Select **Next**.  
10. Optionally, add scope tags to limit the admins who can access and manage this profile in the admin center.  
11. Select **Next**.  
12. On the **Assignments** page, under **Included groups**, select **Add groups**.   
10. Pick **Autopilot Group** > **Select**.  
11. Select **Next**.
12. On the **Review + Create** page, select **Create** to finish creating the profile.

## Hardware change detection  
Microsoft Intune notifies you when it detects a hardware change on an Autopilot-registered device. When a hardware change occurs, Intune updates the device's profile status to one of the following states:

* **Attention required**: The device can't receive the Autopilot profile until you reset and re-register the device.  
* **Fix pending**: Intune tries to register the new hardware. If successful, Intune updates the profile status at the next check-in.  

To view all devices and their current states, go to **Devices** > **Windows Autopilot devices**.   

## Distribute devices to users

You can now distribute the Windows devices to your users. When they sign in for the first time, the Autopilot system will automatically enroll and configure the devices. 

## Clean up resources

If you don't want to use Autopilot devices anymore, you can delete them.

1. If the devices are enrolled in Intune, you must first [delete them from the Azure Active Directory portal](../remote-actions/devices-wipe.md#delete-devices-from-the-azure-active-directory-portal).

2. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Windows** > **Windows enrollment**. 

3. Under **Windows Autopilot Deployment Program**, select **Devices**.  

3. Choose the devices you want to delete, and then select **Delete**.

4. When prompted to, select **Yes** to confirm the deletion. It can take a few minutes to delete. 

## Next steps

You can find more information about other options available for Windows Autopilot.

> [!div class="nextstepaction"]
> [In-depth Autopilot enrollment article](../../autopilot/enrollment-autopilot.md)
