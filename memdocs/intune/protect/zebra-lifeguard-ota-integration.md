---
# required metadata

title: Zebra LifeGuard Over-the-Air Integration with Microsoft Intune
description: Use Microsoft Intune to manage firmware updates for supported Zebra devices.
keywords:
author: Smritib17 
ms.author: smbhardwaj
manager: dougeby
ms.date: 05/10/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: Jessica Yang
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---
# Zebra LifeGuard Over-the-Air Integration with Microsoft Intune

Microsoft Intune supports/provides integration with Zebra LifeGuard Over-the-Air (LG OTA), so that you can have a single area for managing firmware updates for supported Zebra devices. Zebra LifeGuard Over-the-Air (LG OTA) is a service offered by Zebra Technologies that allows deployment of updates to their Android devices in a hands-free and automated manner.

Microsoft Intune allows you to manage firmware updates for supported Zebra devices directly through the Intune admin center.  

Intune manages the creation, management, and monitoring of these deployments through APIs provided by Zebra. Zebra's services and on-device clients handle other complexities (such as evaluating customer entitlements and device compatibility), update hosting, update delivery, and installation.

## Supported Devices

LG OTA is supported on the following devices:

- [Android Enterprise dedicated devices](../fundamentals/deployment-guide-enrollment-android.md#android-enterprise-dedicated-devices)
- [Android Enterprise fully managed devices](../fundamentals/deployment-guide-enrollment-android.md#android-enterprise-fully-managed)

The following aren't supported in public preview:

- Graph assignment with inclusions/exclusions
- Scope tags

## Prerequisites

- [Set up Managed Google Play for your tenant](../enrollment/connect-intune-android-enterprise.md)

- Administrators must have all the required RBAC (role-based access control) permissions:

  - Mobile Apps (to create and deploy app configuration profiles)
  - Android FOTA (to manage firmware OTA updates)

- Access to all appropriate Zebra licenses, and entitlements to use the LG OTA service. For more information, contact Zebra support or see [Zebra's TechDocs](https://techdocs.zebra.com/lifeguard/faq/).

## Process overview  

The process for using LG OTA via Intune is as follows:

1. [Set up Zebra connector](#step-1-set-up-zebra-connector).
2. [Enroll devices with Zebra LG OTA service](#step-2-enroll-devices-with-zebra-lg-ota-service).  
    3. [Approve and deploy required apps for your tenant](#2a-approve-and-deploy-required-apps-for-your-tenant).  
    4. [Create app configuration policy](#2b-create-app-configuration-policy).  
5. [Create and assign deployments in Intune](#step-3-create-and-assign-deployments).
6. [View and manage deployments](#step-4-view-and-manage-deployments).

## Before you start  

You must enroll devices separately with the Zebra LG OTA service before devices can be updated. We recommend that you identify the devices to use with LG OTA, and create a group containing only those devices, to make the enrollment process easier.

## Step 1: Set up Zebra Connector

In the Microsoft Intune admin center, you can link Intune and Zebra.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Connectors and tokens** > **Firmware over-the-air update**.
3. Select **Zebra**. A context panel appears and guides you through the process of setting up your tenant for LG OTA.
4. Select **Connect** and consent to data sharing with Zebra. The context panel is refreshed, and a temporary authorization link becomes enabled in the context panel.  
5. Select the authorization link and follow the prompts on the Zebra portal to authorize access for Intune.

  > [!NOTE]
  > This authorization link expires in 10 minutes. If it expires, select **Refresh** to generate a new link.

6. After the authorization process is complete, an enrollment token will auto-populate within the context panel. If the token doesn't appear, select **Refresh**. Copy the enrollment token to your clipboard, as you'll need the token later.

## Step 2: Enroll Devices with Zebra LG OTA Service

You must enroll devices separately with the Zebra LG OTA service before devices can be updated. We recommend that you identify which devices need to be updated and used with LG OTA. Then create a group containing only those devices, to make the enrollment process easier.

### 2a: Approve and deploy required apps for your tenant

Zebra requires two apps present on the device to perform enrollment with the LG OTA service. 

The apps required are:

- Zebra Enrollment Manager
- Zebra Common Transport Layer

Use Managed Google Play to add them to your tenant. For information on how to add them to your tenant, see [Add and assign Managed Google Play apps to Android Enterprise devices](../apps/apps-add-android-for-work.md)

Next, assign **Zebra Enrollment Manager** and **Zebra Common Transport Layer** as Required apps for all the Zebra devices you want to update and use with LG OTA. The apps are deployed automatically to those devices.

> [!NOTE]
> If you're planning to use LG OTA to update a device running on a version higher than Android 11, you need to enable an additional Zebra package as a system app. For more information on how to enable system apps, see [Manage Android Enterprise system apps in Microsoft Intune](../apps/apps-ae-system.md)

|Build|System app to be enabled|
|--------|------------------------------|
|Any build of Android 11 that is earlier than 11-20-18.00-RG-U00 |com.symbol.tool.stagenow|
|11-20-18.00-RG-U00 or 11-20-18.00-RG-U02|com.zebra.devicemanager|
|Any build of Android 11 that is later than 11-20-18.00-RG-U02 |(None required)|

### 2b: [Create app configuration policy](https://go.microsoft.com/fwlink/?linkid=2210453)

From the context panel in the Set up Zebra connector screen, select the link - **Go to app configuration policies**. You need to create an app configuration policy for managed devices for each of the two required apps.

For more information, see [Add app configuration policies for managed Android Enterprise devices](../apps/app-configuration-policies-use-android.md)

#### Policy targeting Zebra Enrollment Manager app

1. Select **Add** and then select **Managed Devices**.  

2. Complete the fields in the **Basic** tab and select **Next**.

3. In the **Settings** tab, under the **Permissions** section, select **Add** to add the following permission override:

    1. **Permission**: Phone state (read)  
    2. **Permission state**: set to Auto grant

4. In the **Settings** tab, under the **Configuration Settings** section, select **Add** to add the following two configuration settings:

    1. **Action**: Set Configuration value to Claim Device.  
    2. **Claim Device Token**: Paste the enrollment token that you copied in the earlier step into the **Configuration value** field.

5. Assign this configuration policy to all the same devices that you assigned the app earlier.
6. Navigate through the tabs and complete the fields.  

#### Policy targeting Zebra Common Transport Layer app 

1. Select **Add** and then select **Managed Devices**.  
2. Complete the fields in the **Basic** tab and select **Next**.  
3. In the **Settings** tab, under the **Permissions** section, select **Add** to add the following permission override: 

    1. **Permission**: Phone state (read) 
    2. **Permission state**: set to Auto grant 

4. Assign this configuration policy to all the same devices that you assigned the app earlier.
5. Navigate through the tabs and complete the fields.  

Wait at least 15 minutes for the required apps and app configuration policy to reach the devices. If needed, use the Intune app on the device to force a sync by navigating to the Intune app > select the ellipses (**...**), and select **Sync**.  

After synchronization is complete, the devices that support LG OTA will contact Zebra LG OTA service to be enrolled in the LG OTA service and are associated with the  Microsoft Intune/Zebra accounts. You can then deploy firmware updates to these LG OTA enrolled devices.

## Step 3: Create and Assign Deployments

> [!NOTE]
> LG OTA deployments are fire and forget actions and are not persistent policies that enforce compliance. Therefore, Microsoft refers to them as deployments rather than policy. For example, if an upgrade fails initially but later the issue is remediated, LG OTA will not try to update the device even after the issue is remediated.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Android** > **Android FOTA deployments** to create and manage FOTA deployments.
3. Select **Create deployment**.
4. On the **Basics** tab, specify a name for this policy, specify a description (optional), and then select **Next**.  
5. On the **Settings** tab, configure the deployment settings you'd like to use.

    > [!NOTE]
    > Zebra does not support firmware downgrades through LG OTA. Downgrading the operating system on a device causes an Enterprise Reset, wiping all user data and potentially leaving the device in an unmanaged state.  
    > For more information on available settings, see [Zebra documentation](https://techdocs.zebra.com/lifeguard).

    1. In the **Update** area, configure the following options:

        1. Select the target firmware or update to deploy for the devices in this deployment. 
            1. **Release**: Select if you want to install the *Latest release* available for the device, or *Custom* to choose specific firmware.
            1. **Model**: Choose the device model you want to target with this deployment. If you're not sure which firmware to select, or for model and version compatibility, see [Zebra documentation](https://techdocs.zebra.com/lifeguard).
        > [!NOTE]
        > If you assign the deployment to a group containing devices of other models, only devices of the selected model are updated.

    1. In the **Deployment Schedule** area, configure the following options:

        1. Select when the update is deployed.
        1. **Schedule Mode**: Choose when you want the deployment to start running.
            1. **Run as soon as possible**: The deployment starts running immediately and lasts for 28 days after you select **Create** at the end of this flow.
            1. **Scheduled**: More options are available when you select **Scheduled**.
        1. **Time zone**: Select a time zone for the devices being updated.
        1. **Start**: Specify when the deployment must start running.
        1. **End**: If you don't specify an end time, the deployment runs for 28 days.

    1. In the **Installation Schedule** area, configure the following options:

        1. Select when the installation can take place. If you don't specify, devices are updated as soon as they receive the deployment.
            1. **Time zone**: select the time zone for the devices being updated. The time zone you select must match the time zone selected in **Deployment schedule**, if you defined a deployment schedule.
        1. **Start/End**: Specify when you want to allow the updates to be installed. Once installation begins, a complete installation is attempted even if it's past the end time.
        1. **Delay installation until**: On devices Android 10 and earlier, Zebra supports delaying installation to a specific time after the device downloads an update. On Android 11 and later, this setting doesn't do anything, as updates are installed in the background while being downloaded.

    1. In the **Device conditions** area, configure the following options:

        1. Specify device conditions that must be met for downloading and installation to take place.
            1. **Minimum battery level**: battery level between 30-100%
            1. **Require device to be connected to charger**: yes/no
            1. **Network type**: choose the type of network the device must be connected to for downloading and installation to take place.
1. When ready, select **Next** to continue to *Assignments*.
1. On the **Assignments** tab, choose **+ Select groups to include** and then assign your deployments to one or more groups. Use **+ Select groups to exclude** to fine-tune the assignment. When ready, select **Next** to continue.

    When you create an LG OTA deployment, Intune sends information about the deployment to the Zebra LG OTA service, which processes the request and updates eligible devices accordingly. Eligible refers to a Zebra device that is successfully enrolled with the LG OTA service. Deployments can't be modified after they're created. As a result, these deployments have different assignment behavior from many other policies in Intune.

    When you assign a deployment to a group, only eligible Zebra devices, at the time the deployment was created, are included in the deployment request that Intune sends to Zebra for processing by the Zebra LG OTA service. So, the dynamic group membership updates aren't reflected in LG OTA deployments.

    If devices are later removed from an assigned group after the deployment is created, those devices may still be updated if they were already part of this deployment request sent to the LG OTA service. You should assume that all eligible Zebra devices that were ever added to the assigned groups are updated, even if they're removed from the group afterwards.

    **Example**
    - You have a dynamic group, G, that contains three TC57 devices A, B, and C. Every time a new TC57 device is enrolled in your tenant, it's automatically added to the dynamic group. A, B, and C devices start off running firmware version v1.  
    - On January 1, you use Intune and LG OTA to update devices in G from v1 to v2. All three devices are now on v2.
    - On February 1, a new TC57 device, D, is enrolled in the tenant. D is automatically added to the group, and now there are four devices in group G.
    - On February 15, you create a deployment that runs as soon as possible, to update devices in G from v2 to v3. Now, devices A, B, C, and D are all on v3.
    - On March 1, you use Intune and LG OTA to create a deployment that starts on April 1 and will update devices in G from v3 to v4. Intune sends this deployment to the Zebra service on March 1 after you select **Create**.
    - On March 15, you remove devices A and B from group G.  
    - On April 1, the deployment starts running as scheduled. Now, devices A, B, C, D are updated from v3 to v4.

    > [!NOTE]
    > A device can only be part of one deployment at a time.
    > Deployments are only supported for devices, not users. For example, if you assign a deployment to a group containing a device A and a user B who is associated with device B, only device A will receive the deployment.  
    > Assignment filters are not currently supported.
    > Deployments that are assigned to empty groups, or groups containing no eligible devices, will fail.
    > If you assigned to or targeted an empty group, it will fail.

1. On the **Review + create** tab, review your settings.
1. When ready, select **Create** to create the deployment. The deployment is created with Zebra, and Intune sends Zebra the request to create a deployment for the list of assigned devices.  

## Step 4: View and Manage Deployments

After deployments are completed, you can view them from Devices > Android > Android FOTA deployments (Preview).  

Reporting displays information for eligible devices only. For example, if you assign a deployment to a group containing non-Zebra devices, those devices aren't included in the Android FOTA deployments reports.

Each deployment displays details related to:  

- **Deployment status**: The status of the deployment. For more information, see the following table.  

- **Completed devices**: The number of eligible devices where the update is completed.  

- **Failed devices**: The number of devices where the update failed.

- **Total devices**: The total number of eligible devices targeted.  

- **Release**: The associated firmware release.

The status of a deployment is different from the status of individual devices in the deployment. For example, if you create a deployment that targets two devices and only one is successfully updated, the deployment is considered *Completed*. However, it shows one device as failed and one as successful.

|Intune deployment status|Description|
|--------|------------------------------|
|Creation in progress |Intune has sent a deployment request to Zebra service.|
|Failed to create |Failed to create deployment in the Zebra service.|
|Created|Deployment is created but start date hasn't been reached.|
|Deployment in progress|Start date has been reached, and end date hasn't passed.|
|Completed|The deployment end date has passed.|
|Cancellation requested|Intune has sent a cancellation request to the Zebra service.|
|Canceled|Deployment is successfully canceled with the Zebra service.|

By selecting the **More (…)** menu next to a deployment, or by selecting the deployment details, you can attempt to **Cancel a deployment** that is in progress or **Delete** a completed deployment from Intune. Zebra doesn't support editing of already created deployments.

### View device level details of a deployment

1. Select a deployment name to view more details.  
2. The **Device status** chart shows a breakdown of the status for assigned devices.
3. Select **View report** to view device-level information, where you can filter by status and view error codes (if applicable).
4. Each device displays its update status alongside:

- A Zebra deployment ID. This ID can be useful when contacting Zebra support.
- A Status detail, if applicable. If an error code is displayed
  - Code NOTAPPLICABLE: the device isn't enrolled with the LG OTA service, or not eligible for this update
  - Numeric error code. For example, 4009. Contact Zebra support for more details on next steps.




