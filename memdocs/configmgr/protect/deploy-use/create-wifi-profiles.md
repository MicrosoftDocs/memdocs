---
title: How to create Wi-Fi profiles
titleSuffix: Configuration Manager
description: Learn how to use Wi-Fi profiles in Configuration Manager to deploy wireless network settings to users in your organization.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Create Wi-Fi profiles

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, this company resource access feature is [deprecated](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 9315387 --> Use Microsoft Intune to [deploy resource access profiles](../../../intune/configuration/device-profiles.md).

Use Wi-Fi profiles in Configuration Manager to deploy wireless network settings to users in your organization. By deploying these settings, you make it easier for your users to connect to Wi-Fi.  

For example, you have a Wi-Fi network that you want to enable all Windows laptops to connect to. Create a Wi-Fi profile containing the settings necessary to connect to the wireless network. Then, deploy the profile to all users that have Windows laptops in your hierarchy. Users of these devices see your network in the list of wireless networks and can readily connect to this network.  

You can configure Wi-Fi profiles for the following OS versions:

- Windows 8.1 32-bit or 64-bit

- Windows RT 8.1

- Windows 10 or Windows 10 Mobile

You can also use Configuration Manager to deploy wireless network settings to mobile devices using on-premises mobile device management (MDM). For more general information, see [What is on-premises MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

When you create a Wi-Fi profile, you can include a wide range of security settings. These settings include certificates for server validation and client authentication that have been pushed using Configuration Manager certificate profiles. For more information about certificate profiles, see [Certificate profiles](introduction-to-certificate-profiles.md).

## Create a Wi-Fi profile

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and select the **Wi-Fi Profiles** node.

1. On the **Home** tab, in the **Create** group, choose **Create Wi-Fi Profile**.

1. On the **General** page of the Create Wi-Fi Profile Wizard, specify the following information:

    - **Name**: Enter a unique name to identify the profile in the console.

    - **Description**: Optionally add a description to provide further information for the Wi-Fi profile.

    - **Import an existing Wi-Fi profile item from a file**: Select this option to use the settings from another Wi-Fi profile. When you select this option, the remaining pages of the wizard simplify to two pages: **Import Wi-Fi Profile** and **Supported Platforms**.

        > [!IMPORTANT]
        > Make sure that the Wi-Fi profile you import contains valid XML for a Wi-Fi profile. When you import the file, Configuration Manager doesn't validate the profile.

    - **Noncompliance severity for reports**: Choose one of the following severity levels that the device reports if it evaluates the Wi-Fi profile to be noncompliant. For example, if the installation of the profile fails, it's noncompliant.

        - **None**: Computers that fail this compliance rule don't report a failure severity for Configuration Manager reports.

        - **Information**

        - **Warning**

        - **Critical**

        - **Critical with event**: Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. Devices also log the noncompliant state as a Windows event in the application event log.

1. On the **Wi-Fi Profile** page of the wizard, specify the following information:

    - **Network name**: Provide the name that devices will display as the network name.

        > [!IMPORTANT]
        > Configuration Manager doesn't support using the apostrophe (`'`) or comma (`,`) characters in the network name.

    - **SSID**: Specify the case-sensitive ID of the wireless network.

    - **Connect automatically when this network is in range**
    - **Look for other wireless network while connected to this network**
    - **Connect when the network is not broadcasting its name (SSID)**

1. On the **Security Configuration** page, specify the following information:

    > [!IMPORTANT]
    > If you're creating a Wi-Fi profile for [on-premises MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md), the current branch of Configuration Manager only supports the following Wi-Fi security configurations:  
    >
    > - Security types: **WPA2 Enterprise** or **WPA2 Personal**  
    > - Encryption types: **AES** or **TKIP**  
    > - EAP types: **Smart Card or other certificate** or **PEAP**  

    - **Security type**: Select the security protocol that the wireless network uses, or select **No authentication (Open)** if the network is unsecured.

    - **Encryption**: If the security type supports it, set the encryption method for the wireless network.

    - **EAP type**: Select the authentication protocol for the selected encryption method.

        > [!NOTE]
        > For Windows Phone devices only: the EAP types **LEAP** and **EAP-FAST** aren't supported.

        Select **Configure** to specify properties for the selected EAP type. This option isn't available for some selected EAP types.

        > [!IMPORTANT]
        > The EAP type configuration window is from Windows. Make sure that you run the Configuration Manager console on a computer that supports the selected EAP type.

    - **Remember the user credentials at each logon**: Select this option to store user credentials so users don't have to enter wireless network credentials each time they sign in to Windows.

1. On the **Advanced Settings** page of the wizard, specify additional settings for the Wi-Fi profile. Advanced settings might not be available, or might vary, depending on the options that you select on the **Security Configuration** page of the wizard. For example, authentication mode, or single sign-on options.

1. On the **Proxy Settings** page, if your wireless network uses a proxy server, select the option to **Configure proxy settings for this Wi-Fi profile**. Then provide the configuration information for the proxy.

1. On the **Supported Platforms** page, select the OS versions where this Wi-Fi profile is applicable.

1. Complete the wizard.

## Next step

> [!div class="nextstepaction"]
> [How to deploy Wi-Fi profiles](deploy-wifi-vpn-email-cert-profiles.md)
