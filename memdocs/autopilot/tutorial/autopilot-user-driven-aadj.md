---
title: Step by step tutorial for Windows Autopilot user-driven Azure AD join mode in Intune
description: Step by step tutorial for Windows Autopilot user-driven Azure AD join mode in Intune.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 02/13/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# Step by step tutorial for Windows Autopilot user-driven Azure AD join mode in Intune

*Applies to:*

- Windows 11
- Windows 10

## Overview

This step by step tutorial will guide you through using Intune to perform a Windows Autopilot user-driven scenario when the devices will be strictly Azure AD joined. The purpose of this tutorial is to provide in one article a step by step guide for all the steps required for a successful Autopilot user-driven Azure AD join deployment using Intune.

Before beginning, refer to the [How to: Plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all prerequisites are met for joining devices to Azure AD.

## Workflow

 Configure and assign Autopilot Enrollment Status Page (ESP) > Create Autopilot profile > Create device group > Assign Autopilot profile to device group > Import device > Assign Autopilot profile to device > Assign User to device (optional)

## Configure and assign Autopilot Enrollment Status Page (ESP)

The first step is to make a decision regarding whether the Enrollment Status Page (ESP) will be used. The main feature of the ESP is that it displays progress and current status to the end user while the device is being set up and enrolled. It can also be used to block a user from using the device until all required policies and applications are installed. The ESP is recommended if the device has many policies and applications that need to be installed. If the ESP is not enabled in these scenarios, it may make end users think that that the device is hung during the setup process due to the amount of time it is taking with no progress or status being displayed.

To configure and assigned an Autopilot Enrollment Status Page (ESP):

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Devices**.

2. Select **Windows** > **Windows enrollment** > **Enrollment Status Page**.

3. Select **Create**.

4. In **Basics**, enter the following properties:  
     - **Name**: Name your profile so you can easily identify it later. 
     - **Description**: Enter a description for the profile. This setting is optional, but recommended.  

5. Select **Next**.

6. In **Settings**, configure the following settings:  

    - **Show app and profile configuration progress**: Your options:
      - **No**: The enrollment status page doesn't appear during device setup. Select this option if you don't want to show the ESP to users.  
      - **Yes**: The enrollment status page appears during device setup.    

    - **Show an error when installation takes longer than specified number of minutes**: The default time-out is 60 minutes. Enter a higher value if you think more time is needed to install apps on your devices.

    - **Show custom message when time limit or error occur**: Include a message that tells people what happened and who to contact for help. Your options:  
       - **No**: The default message is shown to users when an error occurs. That message is: "Setup could not be completed. Please try again or contact your support person for help."  
       - **Yes**: Your custom message is shown to users when an error occurs. Enter your message in the provided text box.  

    - **Turn on log collection and diagnostics page for end users**: The user's logs and diagnostics could aid with troubleshooting, so we recommend turning this on. Your options:  
       - **No**: The collect logs button isn't shown to users when an installation error occurs. The Windows Autopilot diagnostics page isn't shown on devices running Windows 11.  
       - **Yes**: The collect logs button is shown to users when an installation error occurs. The Windows Autopilot diagnostics page is shown on devices running Windows 11.  

    - **Only show page to devices provisioned by out-of-box experience (OOBE)**: Your options:
       - **No**: The enrollment status page is shown on all Intune-managed and co-managed devices that go through the out-of-box experience (OOBE), and to the first user that signs in to each device. So subsequent users who sign in don't see the ESP. 
       - **Yes**: The enrollment status page is only shown on devices that go through the out-of-box experience (OOBE).

       > [!TIP]
       > If you only want the ESP to appear on Autopilot devices during initial device setup, select the **No** option. Then create a new ESP profile, choose the **Yes** option, and target the profile to an Autopilot device group.  

    - **Block device use until all apps and profiles are installed**: Your options:
       - **No**: Users can leave the ESP before Intune is finished setting up the device. 
       - **Yes**: Users can't leave the ESP until Intune is done setting up the device. This option unlocks additional settings for this scenario.  

    - **Allow users to reset device if installation error occurs**: Your options:  
        - **No**: The ESP doesn't give users the option to reset theirs devices when an installation fails.  
        - **Yes**: The ESP gives users the option to reset their devices when an installation fails.  

    - **Allow users to use device if installation error occurs**: Your options:  
         - **No**: The ESP doesn't give users the option to bypass the ESP when an installation fails.  
         - **Yes**: The ESP gives users the option to bypass the ESP and use their devices when an installation fails.

    - **Block device use until these required apps are installed if they are assigned to the user/device**: Your options:  
         - **All**: All assigned apps must be installed before users can use their devices.  
         - **Selected**: Select-apps must be installed before users can use their devices. Choose this option to select from your managed apps.  

7. Select **Next**.

8. In **Assignments**, select the groups that will receive your profile. Optionally, select **Edit filter** to restrict the assignment further.

    > [!NOTE]
    > Due to OS restrictions, a limited selection of filters are available for ESP assignments. The picker only shows filters that have rules defined for `osVersion`, `operatingSystemSKU`, and `enrollmentProfileName` properties. Filters that contain other properties aren't available.  

9. Select **Next**.  

10. Optionally, in **Scope tags**, assign a tag to limit profile management to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. Then select **Next**.   

    > [!NOTE]
    > Scope tags limit who can see and reprioritize ESP profiles in the admin center. A scoped user can tell the relative priority of their profile even if they can't see all of the other profiles in Intune. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).  

11. In **Review + create**, review your settings. After you select **Create**, your changes are saved, and the profile is assigned. Once deployed, the profile will be applied the next time the devices check in. You can access the profile from your profiles list. 

[Windows Autopilot Enrollment Status Page](/mem/autopilot/enrollment-status)
[Set up the Enrollment Status Page](/mem/intune/enrollment/windows-enrollment-status)

## Create Autopilot profile

## Create device group

[Create device groups](/mem/autopilot/enrollment-autopilot)

## Assign Autopilot profile to device group

## Import device

## Assign Autopilot profile to device

## More info

[Windows Autopilot user-driven mode](/mem/autopilot/user-driven)