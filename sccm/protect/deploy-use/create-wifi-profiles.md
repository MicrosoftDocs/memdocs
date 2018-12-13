---
title: "How to create Wi-Fi profiles"
titleSuffix: "Configuration Manager"
description: "Learn how to use Wi-Fi profiles in System Center Configuration Manager to deploy wireless network settings to users in your organization."
ms.date: 12/11/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Create Wi-Fi profiles

*Applies to: System Center Configuration Manager (Current Branch)*


Use Wi-Fi profiles in System Center Configuration Manager to deploy wireless network settings to users in your organization. By deploying these settings, you make it easier for your users to connect to Wi-Fi.  

 For example, you have a Wi-Fi network that you want to enable all iOS devices to connect to. Create a Wi-Fi profile containing the settings necessary to connect to the wireless network. Then, deploy the profile to all users that have iOS devices in your hierarchy. Users of iOS devices see the company network in the list of wireless networks and can readily connect to this network.  

 You can configure the following device types with Wi-Fi profiles:  

-   Devices that run Windows 8.1 32-bit  

-   Devices that run Windows 8.1 64-bit  

-   Devices that run Windows RT 8.1  

-   Devices that run Windows 10 Desktop or Mobile  

[Create Wi-Fi profiles for mobile devices](../../mdm/deploy-use/create-wifi-profiles.md) provides  information about how to use Wi-Fi profiles in Configuration Manager to deploy wireless network settings to mobile device users."

> [!IMPORTANT]  
>  To deploy profiles to Android, iOS, Windows Phone, and enrolled Windows 8.1 or later devices, these devices must be enrolled in Microsoft Intune. For information about how to get your devices enrolled, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).  

 When you create a Wi-Fi profile, you can include a wide range of security settings. These include certificates for server validation and client authentication that have been pushed using Configuration Manager certificate profiles. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

## Create a Wi-Fi Profile  

1. In the Configuration Manager console, choose **Assets and Compliance** > **Compliance Settings** >  **Company Resource Access** > **Wi-Fi Profiles**.  

2. On the **Home** tab, in the **Create** group, choose **Create Wi-Fi Profile**.  

3. On the **General** page, enter a unique name and a description for the Wi-Fi profile.  If you want to use the settings from another Wi-Fi profile, select **Import an existing Wi-Fi profile item from a file**.  

   > [!IMPORTANT]  
   >  Ensure that the Wi-Fi profile you import contains valid XML for a Wi-Fi profile. Configuration Manager does not validate the profile when you import the file.  

4. In  **Noncompliance severity for reports**, specify the severity level that is reported if the Wi-Fi profile is found to be noncompliant on client devices (for example, if the installation of the profile fails). The available severity levels are as follows:  

   -   **None**: Computers that fail this compliance rule do not report a failure severity for Configuration Manager reports.  

   -   **Information**: Computers that fail this compliance rule report a failure severity of **Information** for Configuration Manager reports.  

   -   **Warning**: Computers that fail this compliance rule report a failure severity of **Warning** for Configuration Manager reports.  

   -   **Critical**: Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports.  

   -   **Critical with event**: Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. This severity level is also logged as a Windows event in the application event log.  

5. On the **Wi-Fi Profile** page provide the name that devices will display as the network name.  

   > [!IMPORTANT]  
   >  Configuration Manager does not support using the apostrophe (**â€˜**) or comma (**,**) characters in the network name.  

6. Specify the case-sensitive **SSID**
7. Choose the other appropriate connectivity options, including.   **Connect when the network is not broadcasting its name (SSID)**, if there is a possibility that the SSID is hidden  

8. On the **Security Configuration** page, select the security protocol that the wireless network uses, or select **No authentication (Open)** if the network is unsecured.
   > [!IMPORTANT]
   >  If you're creating a Wi-Fi profile for On\-premises Mobile Device Management, the current branch of Configuration Manager only supports the following Wi-Fi security configurations:  
   > 
   >  Security types: **WPA2 Enterprise** or **WPA2 Personal**  
   > Encryption types: **AES** or **TKIP**  
   > EAP types: **Smart Card or other certificate** or **PEAP**  
   > 
   > For Android devices, the security types **WPA Personal**, **WPA2 Personal** and **WEP** are not supported.  

9. Select the encryption method that the wireless network uses.  

10. Select the EAP type that is used to authenticate with the wireless network.  

     For Windows Phone devices only: the EAP types **LEAP** and **EAP-FAST** are not supported.  

11. Click **Configure** to specify properties for the selected EAP type. This option might not be available for some selected EAP types.  

    > [!IMPORTANT]  
    >  When you click **Configure**, the dialog box that opens is a Windows dialog box. Because of this, you must ensure that the operating system of the computer that runs the Configuration Manager console supports configuring the selected EAP type.  
    >   
    >  For iOS devices, if you chose a non-EAP method for authentication, regardless of the method you choose, MS-CHAP v2 will be used for the connection.  

12. If you want to store user credentials so users do not have to enter credentials at each logon, select **Remember the user credentials at each logon**.  

13. **For iOS devices only:**  
    Configure information for any certificates that are required for the Wi-Fi connection. You must configure the client certificate and either the trusted server certificate name or the root certificate, as follows:  

    - **Trusted server certificate names**: If the server that the device connects to uses a server authentication certificate to identify the server and help secure the communication channel, enter the name or names in that certificateâ€™s subject name or subject alternative name. The name or names are typically the fully qualified domain name of the server. For example, if the server certificate has a common name of srv1.contoso.com in the certificate subject, enter **srv1.contoso.com**. If the server certificate has multiple names that are specified in the subject alternative name, enter each name, separated by a semicolon.  

      > [!TIP]  
      >  If the client certificate that you select for EAP or client authentication for an iOS device will be used to authenticate to a Remote Authentication Dial-In User Service (RADIUS) server, such as a server that is running Network Policy Server, you must set the Subject Alternative Name to the User Principal Name.  

    - **Select root certificates for server validation**: If the server that the device connects to uses a server authentication certificate that the device does not trust, select the certificate profile that contains the root certificate for the server certificate, to create a certificate chain of trust on the device.  

    - **Select a client certificate for client authentication**: If the server or network device requires a client certificate to authenticate the connecting device, select the certificate profile that contains the client authentication certificate.  

      > [!NOTE]  
      >  Before you can select the root certificate and client certificate, you must first configure and deploy them as a certificate profile. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

14. On the **Advanced Settings** page, specify advanced settings for the Wi-Fi profile such as the authentication mode, single sign-on options, and Federal Information Processing Standards compliance. For more information about these options, see your Windows documentation. Advanced settings might not be available, or might vary, depending on the options that you selected on the **Security Configuration** page of the wizard.  

15. On the **Proxy Settings** page, select   **Configure proxy settings for this Wi-Fi profile** if your wireless network uses a proxy server, and then provide the configuration information.  

16. On the **Supported Platforms** page, select the operating systems where you want to install the Wi-Fi profile. Alternatively, click **Select all** to install the Wi-Fi profile to all available operating systems.  

### Next steps
 For information about how to deploy the Wi-Fi profile, see [How to deploy Wi-Fi profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  
