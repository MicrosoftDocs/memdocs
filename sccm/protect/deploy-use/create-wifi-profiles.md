---
title: "Create Wi-Fi profiles | System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
caps.latest.revision: 13
caps.handback.revision: 0
author: Nbigman

---
# How to create Wi-Fi profiles in System Center Configuration Manager

Use Wi-Fi profiles in System Center Configuration Manager to deploy wireless network settings to users in your organization. By deploying these settings, you make it easier for your users to connect to Wi-Fi.  
  
 For example, you installed a new Wi-Fi network named **Contoso Wi-Fi**. You now want to provision all devices that run the iOS operating system with the settings required to connect to this network. You can create a Wi-Fi profile containing the settings necessary to connect to the **Contoso Wi-Fi** wireless network. Then, you can deploy this profile to all users that have devices that run iOS in your hierarchy. Users of iOS devices see the company network in the list of wireless networks and can readily connect to this network.  
  
 You can configure the following device types with Wi-Fi profiles:  
  
-   Devices that run Windows 8.1 32-bit  
  
-   Devices that run Windows 8.1 64-bit  
  
-   Devices that run Windows RT 8.1  
  
-   Devices that run Windows Phone 8.1  
  
-   Devices that run Windows 10 Desktop or Mobile  
  
-   IPhone devices that run iOS 5, iOS 6, iOS 7 and iOS 8  
  
-   IPad devices that run iOS 5, iOS 6, iOS 7 and iOS 8  
  
-   Android devices that run version 4  
  
> [!IMPORTANT]  
>  To deploy profiles to Android, iOS, Windows Phone, and enrolled Windows 8.1 or later devices, these devices must be enrolled in Microsoft Intune]. For information about how to get your devices enrolled, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).  
  
 When you create a Wi-Fi profile, you can include a wide range of security settings. These include certificates for server validation and client authentication that have been provisioned by using Configuration Manager certificate profiles. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](../Topic/Certificate%20profiles%20in%20System%20Center%20Configuration%20Manager.md).  
  
## Steps to Create a Wi-Fi Profile  
 Use the following required steps to create a Wi-Fi profile by using the **Create Wi-Fi Profile Wizard**.  
  
-   [Step 1: Start the Create Wi-Fi Profile Wizard](#BKMK_Step1)  
  
-   [Step 2: Provide General Information about the Wi-Fi Profile](#BKMK_Step2)  
  
-   [Step 3: Provide Information about the Wireless Network](#BKMK_Step3)  
  
-   [Step 4: Configure Security for the Wi-Fi Profile](#BKMK_Step4)  
  
-   [Step 5: Configure Advanced Settings for the Wi-Fi Profile](#BKMK_Step5)  
  
-   [Step 6: Configure Proxy Settings for the Wi-Fi Profile](#BKMK_Step6)  
  
-   [Step 7: Configure Supported Platforms for the Wi-Fi Profile](#BKMK_Step7)  
  
-   [Step 8: Complete the Wizard](#BKMK_Step8)  
  
##  <a name="BKMK_Step1"></a> Step 1: Start the Create Wi-Fi Profile Wizard  
  
1.  In the Configuration Manager console, click **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then click **Wi-Fi Profiles**.  
  
3.  On the **Home** tab, in the **Create** group, click **Create Wi-Fi Profile**.  
  
##  <a name="BKMK_Step2"></a> Step 2: Provide General Information about the Wi-Fi Profile  
  
1.  On the **General** page of the Create Wi-Fi Profile Wizard, enter a unique name and description for the Wi-Fi profile. You can use a maximum of 256 characters.  
  
2.  If you want to use the settings from another Wi-Fi profile, select **Import an existing Wi-Fi profile item from a file**.  
  
    > [!IMPORTANT]  
    >  Ensure that the Wi-Fi profile you import contains valid XML for a Wi-Fi profile. Configuration Manager does not validate the profile when you import the file.  
  
3.  In  
                            **Noncompliance severity for reports**, specify the severity level that is reported if the Wi-Fi profile is found to be noncompliant on client devices (for example, if the installation of the profile fails). The available severity levels are as follows:  
  
    -   **None**: Computers that fail this compliance rule do not report a failure severity for Configuration Manager reports.  
  
    -   **Information**: Computers that fail this compliance rule report a failure severity of **Information** for Configuration Manager reports.  
  
    -   **Warning**: Computers that fail this compliance rule report a failure severity of **Warning** for Configuration Manager reports.  
  
    -   **Critical**: Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports.  
  
    -   **Critical with event**: Computers that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. This severity level is also logged as a Windows event in the application event log.  
  
##  <a name="BKMK_Step3"></a> Step 3: Provide Information about the Wireless Network  
  
1.  On the **Wi-Fi Profile** page of the Create Wi-Fi Profile Wizard, specify the descriptive name for the wireless Internet connection by using a maximum of 32 characters. This is the name that devices will display as the network name.  
  
    > [!IMPORTANT]  
    >  Configuration Manager does not support using the apostrophe (**â€˜**) or comma (**,**) characters in the network name.  
  
2.  In **SSID**, specify the name (SSID), of the wireless network that you want devices to be able to connect to. You can use a maximum of 32 characters. The SSID name is case-sensitive, so be sure to enter it exactly as it is configured.  
  
3.  If you want to allow devices to automatically reconnect to the wireless network when it is in range, select **Connect automatically when this network is in range**.  
  
4.  If you want to allow devices to continue to scan for other wireless networks when they are connected to this network, select  
                            **Look for other wireless networks while connected to this network**.  
  
5.  If you want to allow devices to connect to the network when it is not visible in the list of networks (because it is hidden and not broadcasting its name), select **Connect when the network is not broadcasting its name (SSID)**,  
  
##  <a name="BKMK_Step4"></a> Step 4: Configure Security for the Wi-Fi Profile  
  
> [!IMPORTANT]  
>  If you're creating a Wi-Fi profile for On\-premises Mobile Device Management, the current branch of Configuration Manager only supports the following Wi-Fi security configurations:  
>   
>  Security types: **WPA2 Enterprise** or **WPA2 Personal**  
> Encryption types: **AES** or **TKIP**  
> EAP types: **Smart Card or other certificate** or **PEAP**  
  
1.  On the **Security Configuration** page of the Create Wi-Fi Profile Wizard, Select the security protocol that the wireless network uses, or select **No authentication (Open)** if the network is unsecured.  
  
     For Android devices only: the security types **WPA â€“ Personal**, **WPA2 â€“ Personal** and **WEP** are not supported.  
  
2.  Select the encryption method that the wireless network uses.  
  
3.  Select the EAP type that is used to authenticate with the wireless network.  
  
     For Windows Phone devices only: the EAP types **LEAP** and **EAP-FAST** are not supported.  
  
4.  Click **Configure** to specify properties for the selected EAP type. This option might not be available for some selected EAP types.  
  
    > [!IMPORTANT]  
    >  When you click **Configure**, the dialog box that opens is a Windows dialog box. Because of this, you must ensure that the operating system of the computer that runs the Configuration Manager console supports configuring the selected EAP type.  
    >   
    >  For iOS devices, if you chose a non-EAP method for authentication, regardless of the method you choose, MS-CHAP v2 will be used for the connection.  
  
5.  If you want to store user credentials so users do not have to enter credentials at each logon, select **Remember the user credentials at each logon**.  
  
### For iOS devices only:  
 Configure information for any certificates that are required for the Wi-Fi connection. You must configure the client certificate and either the trusted server certificate name or the root certificate, as follows:  
  
-   **Trusted server certificate names**: If the server that the device connects to uses a server authentication certificate to identify the server and help secure the communication channel, enter the name or names in that certificateâ€™s subject name or subject alternative name. The name or names are typically the fully qualified domain name of the server. For example, if the server certificate has a common name of srv1.contoso.com in the certificate subject, enter **srv1.contoso.com**. If the server certificate has multiple names that are specified in the subject alternative name, enter each name, separated by a semicolon.  
  
    > [!TIP]  
    >  If the client certificate that you select for EAP or client authentication for an iOS device will be used to authenticate to a Remote Authentication Dial-In User Service (RADIUS) server, such as a server that is running Network Policy Server, you must set the Subject Alternative Name to the User Principal Name.  
  
-   **Select root certificates for server validation**: If the server that the device connects to uses a server authentication certificate that the device does not trust, select the certificate profile that contains the root certificate for the server certificate, to create a certificate chain of trust on the device.  
  
-   **Select a client certificate for client authentication**: If the server or network device requires a client certificate to authenticate the connecting device, select the certificate profile that contains the client authentication certificate.  
  
> [!NOTE]  
>  Before you can select the root certificate and client certificate, you must first configure and deploy them as a certificate profile. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](../Topic/Certificate%20profiles%20in%20System%20Center%20Configuration%20Manager.md).  
  
##  <a name="BKMK_Step5"></a> Step 5: Configure Advanced Settings for the Wi-Fi Profile  
 On the **Advanced Settings** page of the Create Wi-Fi Profile Wizard, specify advanced settings for the Wi-Fi profile such as the authentication mode, single sign-on options, and Federal Information Processing Standards compliance. For more information about these options, see your Windows documentation.  
  
> [!NOTE]  
>  Advanced settings might not be available, or might vary, depending on the options that you selected on the **Security Configuration** page of the wizard.  
  
##  <a name="BKMK_Step6"></a> Step 6: Configure Proxy Settings for the Wi-Fi Profile  
  
1.  On the **Proxy Settings** page of the Create Wi-Fi Profile Wizard, select the **Configure proxy settings for this Wi-Fi profile** check box if your wireless network uses a proxy server.  
  
2.  Specify details about your proxy server and its settings. For more information, see your Windows Server documentation.  
  
##  <a name="BKMK_Step7"></a> Step 7: Configure Supported Platforms for the Wi-Fi Profile  
 On the **Supported Platforms** page of the Create Wi-Fi Profile Wizard, select the operating systems where you want to install the Wi-Fi profile. Alternatively, click **Select all** to install the Wi-Fi profile to all available operating systems.  
  
##  <a name="BKMK_Step8"></a> Step 8: Complete the Wizard  
 On the **Summary** page of the Wizard, review the actions that the wizard will take, and then complete the wizard. The new Wi-Fi profile appears in the **Wi-Fi Profiles** node in the **Assets and Compliance** workspace.  
  
 For information about how to deploy the Wi-Fi profile, see [How to deploy Wi-Fi profiles in System Center Configuration Manager](../../protect/deploy-use/deploy-wifii-profiles.md).  
  
### See also  

 [Operations and maintenance for Wi-Fi Profiles in System Center Configuration Manager](../Topic/Operations%20and%20maintenance%20for%20Wi-Fi%20Profiles%20in%20System%20Center%20Configuration%20Manager.md)