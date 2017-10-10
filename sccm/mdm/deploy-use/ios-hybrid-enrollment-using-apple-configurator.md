---
title: "Enroll iOS devices Apple Configurator - Configuration Manager"
descriptions: "Pre-enroll iOS devices by using Apple Configurator with Configuration Manager."
ms.custom: na
ms.date: 08/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: mtillman
ms.author: mtillman
manager: angrobe

---
# iOS hybrid enrollment using Apple Configurator with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Companies that buy iOS devices to be used by employees can manage them using Microsoft Intune. To prepare corporate-owned iOS devices for enrollment, you configure an enrollment profile in the Configuration Manager console and then export the profile URL for use by Apple Configurator. You prepare the iOS device for enrollment by connecting it to a Mac computer with a USB cable and using Apple Configurator to set it up. Apple Configurator factory resets the device and adds the enrollment profile so that the device can be enrolled when the user first powers it up and goes through the Setup Assistant process.

The following procedure is recommended for dedicated iOS devices that will have a single user who uses the device to access company email and company resources such as apps and date.  

## Prerequisites  

-   Physical access to iOS devices  

-   Device serial numbers - [How to get an iOS serial number](https://support.apple.com/en-us/HT204308)  

-   Mac computer with [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

-   USB cables for connecting devices to your Mac computer  

## Add a corporate-owned device enrollment profile

1.  In the Configuration Manager console, go to **Assets and Compliance** > **Overview** > **All Corporate-owned Devices** > **iOS** > **Enrollment Profiles**. Click **Create Profile** to open the Create Profile wizard. Configure the settings on the following pages:  

2.  On the **General** page, specify the following information:  

    -   **Name** (Not visible to users)  

    -   **Description** (Not visible to users)  

    -   **User affinity** – Specifies how devices are enrolled. For most Setup Assistant scenarios, use **Prompt for user affinity**.  

        -   **Prompt for user affinity**: The device must be affiliated with a user during initial setup and could then be permitted to access company data and email as that user.  

        -   **No user affinity**: The device is not affiliated with a user. Use this affiliation for devices that perform tasks without accessing local user data. Apps requiring user affiliation won’t work.

    Click **Next** to continue.  

3.  On the **Device Enrollment Program** page, leave the **Configure Device Enrollment Program settings for this profile** checkbox unchecked, and click **Next**.  

4.  Review the summary, and then click **Next** to create the enrollment profile. Click **Close** to finish the wizard. You're now ready to add IMEI numbers or serial numbers for the devices you want to enroll.  

## Predeclare devices to enroll with Setup Assistant

In this step, you predeclare devices as corporate-owned by providing a list of hardware identifiers (IMEI or serial numbers).

For more information, see [Predeclare devices with IMEI and iOS serial number](predeclare-devices-with-hardware-id.md). When you're done with that task, return to this page to continue with the next step.

## Export the profile to deploy to iOS devices

1.  In the Configuration Manager console, go to **Assets and Compliance** > **Overview** > **All Corporate-owned Devices** > **iOS** > **Enrollment Profiles**.

2.  Select the enrollment profile to deploy to mobile devices and click **Export…**.

3.  Copy and save the **Profile URL** in a file you can edit.   

4.  To support Apple Configurator 2, the 2.0 Profile URL must be edited. Replace the following portion of the URL:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     with  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  Save the edited profile URL. You will use it to add the enrollment profile URL in Apple Configurator in the [next section](#step-4-prepare-the-device-with-apple-configurator).  

> [!NOTE]
> The enrollment profile URL is valid for two weeks from when it is exported. After two weeks, you must export a new URL to enroll iOS devices.

## Prepare the device with Apple Configurator

To prepare iOS devices for enrollment, you connect each device to a Mac computer and upload the enrollment profile to it.  

> [!WARNING]  
>  Apple Configurator wipes and resets devices to factory configurations.  

1.  On a Mac computer, open **Apple Configurator 2**.  

2.  In the menu bar, click **Apple Configurator 2** > **Preferences**.  

2.  In the preferences pane, select **Servers** and click the "+" symbol below the left pane to launch the MDM Server wizard. Click **Next**.  

3.  Enter the **Name** and **Enrollment URL** you saved [earlier](#step-3-export-the-profile-to-deploy-to-ios-devices). Click **Next**.  

   > [!NOTE]
   > If you receive a warning about trust profile requirements for Apple TV, you can safely cancel the **Trust Profile** option by clicking the grey "X". You can also safely disregard any Anchor certificate warning.

   To continue, click **Next** until the wizard is complete.  

4.  On the **Servers** pane, click “Edit” beside the new server’s profile. Ensure that the Enrollment URL exactly matches the URL you entered earlier. Reenter the URL if it is different, and click **Save**.  

5.  With a USB cable, connect an iOS device to the Mac computer.  

  > [!WARNING]  
  >  This process resets devices to factory configurations. Prior to connecting the device, reset the device and power it on. As a best practice, the device should be at the Hello screen before continuing.  

6.  Click **Prepare**. On the **Prepare iOS Device** pane, select **Manual**, and then click **Next**.  

7.  On the **Enroll in MDM Server** pane, select the server name you created, and then click **Next**.  

9. On the **Create an Organization** pane, choose the **Organization** or create a new organization, and then click **Next**.  

10. On the **Configure iOS Setup Assistant** pane, choose the steps to present to the user, and then click **Prepare**. If prompted, authenticate to update trust settings.  

11. When finished, you can disconnect the USB cable.  

Repeat these steps for all the devices you want to prepare for enrollment.

## Distribute devices

The devices are now ready for corporate enrollment. Power down the devices and distribute them to users. When the device is turned on, Setup Assistant will start and prompt the user for their work or school account to begin enrollment.
