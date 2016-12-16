---
title: "iOS hybrid enrollment using Apple Configurator with Configuration Manager | Microsoft Docs"
descriptions: "Pre-enroll iOS devices by using Apple Configurator with Configuration Manager."
ms.custom: na
ms.date: 12/15/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: mtillmanms.author: mtillmanmanager: angrobe

---
# iOS hybrid enrollment using Apple Configurator with Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Companies that buy iOS devices to be used by employees can manage them using Microsoft Intune. You can pre-enroll iOS devices by USB-connecting them to a Mac PC running Apple Configurator 2.0. Before enrolling, you must prepare an corporate-owned device enrollment profile in the Configuration Manager console and export it to the Mac PC. The enrollment process will factory reset the device and go through the Setup Assistant process to configure the device. The following procedure is recommended for dedicated iOS devices that will have a single user who uses the device to access company email and company resources such as apps and date.  

## Prerequisites  

-   Physical access to iOS devices  

-   Device serial numbers - [How to get an iOS serial number](https://support.apple.com/en-us/HT204308)  

-   Mac computer with [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

-   USB cables for connecting devices to your Mac computer  

## Add a corporate-owned device enrollment profile

1.  In the Configuration Manager console, in the **Assets and Compliance** workspace, expand **Overview**, expand **All Corporate-owned Devices**, expand **iOS**, and click **Enrollment Profiles**. Click **Create Profile** on the **Home** tab to open the Create Profile wizard. Configure the settings on the following pages:  

2.  On the **General** page, specify the following information, and then click **Next**.  

    -   **Name** (Not visible to users)  

    -   **Description** (Not visible to users)  

    -   **User affinity** – Specifies how devices are enrolled. For most Setup Assistant scenarios, use **Prompt for user affinity**.  

        -   **Prompt for user affinity**: The device must be affiliated with a user during initial setup and could then be permitted to access company data and email as that user.  

        -   **No user affinity**: The device is not affiliated with a user. Use this affiliation for devices that perform tasks without accessing local user data. Apps requiring user affiliation won’t work.  

3.  On the **Device Enrollment Program** page, leave the **Configure Device Enrollment Program settings for this profile** checkbox unchecked, and click **Next**.  

4.  Review the summary, and then click **Next** to create the enrollment profile. Click **Close** to finish the wizard.  

## Add iOS devices to enroll with Setup Assistant

1.  In the Configuration Manager console, in the **Assets and Compliance** workspace, expand **Overview**, expand **All Corporate-owned Devices**, expand **iOS**, and click **Device Information**. and then click **Add devices**.

2.  Add devices in two ways:  

  - **Upload a CSV file containing serial numbers**

      Create a comma-separated value (.csv) list of two columns without a header, limited to 5000 devices or 5MB per csv file. For each row, the first cell is the device serial number, the second cell are device details (optional).

      This .csv file when viewed in a text editor appears as:  

      ```  
      0000000,PO 1234  
      111111111,PO 1234  
      ```  

  - **Manually add serial numbers and details**

      Enter the serial number and device details of up to five devices  

2. click **Next**.  

3. Confirm the devices to enroll. Serial numbers of devices already enrolled or enrolled by other means cannot be imported. Click **Next**.  

4. Specify the profile to assign to added devices from the list of available profiles, review the **Enrollment profile details**, and then click **Finish**.

Manually added devices can be assigned to any Enrollment profile, but DEP-synced devices must be assigned to a DEP-enabled profile.  

## Select a profile to deploy to iOS devices

1.  In the Configuration Manager console, in the **Assets and Compliance** workspace, expand **Overview**, expand **All Corporate-owned Devices**, expand **iOS**, and then click **Enrollment Profiles**.

2.  Select the enrollment profile to deploy to mobile devices and click **Export…** in the taskbar.

3.  Copy and save the **Profile URL** in a file you can edit.   

4.  To support Apple Configurator 2, the 2.0 Profile URL must be edited. Replace the following portion of the URL:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     with  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  Save the edited profile URL. You will upload it in Apple Configurator in the [next section](#prepare-the-device-with-apple-configurator) to define the Intune profile used by iOS devices.  The enrollment profile URL is valid for two weeks from when it is exported. After two weeks, you must export a new URL to enroll iOS devices.

## Prepare the device with Apple Configurator

iOS devices are connected to the Mac computer and enrolled for mobile device management.  

> [!WARNING]  
>  The devices will be reset to factory configurations during the enrollment process.  

1.  On a Mac computer, open **Apple Configurator 2**.  

2.  In the menu bar, click **Apple Configurator 2**, and click **Preferences**.  

2.  In the preferences pane, select **Servers** and click the "+" symbol below the left pane to launch the MDM Server wizard. Click **Next**.  

3.  Enter the **Name** and **Enrollment URL** you saved [earlier](#select-a-profile-to-deploy-to-iOS-devices). Click **Next**.  

   If you receive a warning about trust profile requirements for Apple TV, you may safely cancel the **Trust Profile** option by clicking the grey "X". You can also safely disregard any Anchor certificate warning. To continue, click **Next** until the wizard is complete.  

4.  On the **Servers** pane, click “Edit” beside the new server’s profile. Ensure that the Enrollment URL exactly matches the the URL you saved in step 5. Reenter the URL if it is different, and click **Save**.  

5.  Connect the iOS mobile devices to the Apple computer with a USB adapter.  

  > [!WARNING]  
  >  The devices will be reset to factory configurations during the enrollment process. As a best practice, reset the device and power it on. As a best practice, devices should be at the Hello screen when you start Setup Assistant.  

6.  Click **Prepare**. On the **Prepare iOS Device** pane, select **Manual** and then click **Next**.  

7.  On the **Enroll in MDM Server** pane, select the server name you created and then click **Next**.  

8.  On the **Enroll in MDM Server** pane, select the server name you created and then click **Next**.  

9. On the **Create an Organization** pane, choose the **Organization** or create a new organization, and then click **Next**.  

10. On the **Configure iOS Setup Assistant** pane, choose the steps presented to the user, and then click **Prepare**. If prompted, authenticate to update trust settings.  

11. When the iOS device finishes preparing, you can disconnect the USB cable.  

## Distribute devices

The devices are now ready for corporate enrollment. Power down the devices and distribute them to users. When the device is turned on, Setup Assistant will start and prompt the user for their work or school account to begin enrollment.
