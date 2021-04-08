---
title: Deploy resource access profiles
titleSuffix: Configuration Manager
description: Learn how to deploy Wi-Fi, VPN, and certificate profiles in Configuration Manager.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: mestew
ms.author: mstewart
manager: dougeby
---

# Deploy resource access profiles in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, this company resource access feature is [deprecated](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 9315387 --> Use Microsoft Intune to [deploy resource access profiles](../../../intune/configuration/device-profiles.md).

After you create one of the following resource access profiles, deploy it to one or more collections:

- [Wi-Fi](create-wifi-profiles.md)
- [VPN](create-vpn-profiles.md)
- [Certificate](create-certificate-profiles.md)

When you deploy these profiles, you specify the target collection, and specify how often the client evaluates the profile for compliance.  

## Deploy a profile

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Expand **Compliance Settings**, expand **Company Resource Access**, and then choose the appropriate profile node. For example, **Wi-Fi Profiles**.

1. In the list of profiles, select the profile that you want to deploy. Then in the **Home** tab of the ribbon, in the **Deployment** group, select **Deploy**.  

1. In the deploy profile window, specify the following information:  

    - **Collection**: Select the collection where you want to deploy the profile.

    - **Generate an alert**: Enable this option to configure an alert. The site generates this alert if the profile compliance is less than the specified percentage by the specified date and time. You can also select whether you want an alert to be sent to System Center Operations Manager.

    - **Random delay (hours)**: For certificate profiles that contain Simple Certificate Enrollment Protocol (SCEP) settings, specify a delay window to avoid excessive processing on the Network Device Enrollment Service (NDES). The default value is `64` hours.  

    - **Specify the compliance evaluation schedule for this...profile**: Specify how often the client evaluates compliance for this profile. Select a **Simple schedule** or configure a **Custom schedule**. By default, the simple schedule is every `12` hours.

1. Select **OK** to close the window and create the deployment.

## Delete a deployment

If you want to delete a deployment, select it from the list. In the details pane, switch to the **Deployments** tab. Select the deployment, and then in the **Deployment** tab of the ribbon, select **Delete**.

> [!IMPORTANT]
> When you remove a VPN profile deployment, Configuration Manager doesn't remove the VPN profile from Windows. If you want to remove the profile from devices, manually remove it.

## Next steps

[Monitor Wi-Fi and VPN profiles](monitor-wifi-email-vpn-profiles.md)

[Monitor certificate profiles](monitor-certificate-profiles.md)
