---
title: "How to Create VPN profiles "
titleSuffix: "Configuration Manager"
description: "Learn how to create VPN profiles in System Center Configuration Manager."
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Create VPN profiles in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The connection types available for the different device platforms are described in [VPN profiles in System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

For third-party VPN connections, distribute the VPN app before deploying the VPN profile. If you don't deploy the app, users will be prompted to do so when they try to connect to the VPN. To learn how to deploy apps, see [Deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

### Create a VPN profile   

1.  In the Configuration Manager console, choose **Assets and Compliance** > **Compliance Settings** > **Company Resource Access** > **VPN Profiles**.  

2.  On the **Home** tab, in the **Create** group, choose **Create VPN Profile**.  


3.  Complete the **General** page. Note the following:  

    - Select the appropriate **Platform**.

       - If you select the Windows 8.1 platform, you have the option to select **Import an existing VPN profile item from a file** to import VPN profile information that was exported to an XML file.

   	- Do not use the characters \\/:*?&lt;>&#124;, or the space character in the VPN profile name. These characters are not supported by the Windows Server VPN profile.  


4.  On the **Connection** page, specify:  

    -   **Connection type**: Choose the VPN connection type. You can choose from the connection types in the following table.  

    -   **Server list**: Add a new server to use for the VPN connection. Depending on the connection type, you can add one or more VPN servers and specify the default server.  

        > [!NOTE]  
        >  Devices that run iOS do not support using multiple VPN servers. If you configure multiple VPN servers and then deploy the VPN profile to an iOS device, only the default server is used.  

     This table provides options for connection types. See your VPN server documentation for more information.

| &nbsp;&nbsp;Option&nbsp;&nbsp; | More information | &nbsp;&nbsp;Connection&nbsp;type&nbsp;&nbsp; |  
|----------------|----------------------|---------------------|  
|**Realm**     |The authentication realm that you want to use. An authentication realm is a grouping of authentication resources that is used by the Pulse Secure connection type.|Pulse Secure|    
|**Role**        |The user role that has access to this connection. |Pulse Secure|  
|**Login group or domain** |The name of the login group or domain that you want to connect to.|Dell SonicWALL Mobile Connect|  
|**Fingerprint**  |A string, for example "Contoso Fingerprint Code" that will be used to verify that the VPN server can be trusted.<br /><br /> A fingerprint can be:<br /><br /> - Sent to the client so it knows to trust any server presenting that same fingerprint when connecting.<br /><br /> - If the device doesn't already have the fingerprint it will prompt the user to trust the VPN server they are connecting to while showing the fingerprint (the user manually verifies the fingerprint and chooses **trust** to connect).|Check Point Mobile VPN|  
|**Send all network traffic through the VPN connection** |If this option is not selected, you can specify additional routes for the connection (for **Microsoft SSL (SSTP)**, **Microsoft Automatic**, **IKEv2**, **PPTP** and **L2TP** connection types), which is known as split or VPN tunneling.<br /><br /> Only connections to the company network are sent over a VPN tunnel. VPN tunneling is not used when you connect to resources on the Internet. |All|  
|**Connection specific DNS suffix** |The connection-specific Domain Name System (DNS) suffix for the connection.|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
|**Bypass VPN when connected to company Wi-Fi network**  |The VPN connection will not be used when the device is connected to the company Wi-Fi network.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
|**Bypass VPN when connected to home Wi-Fi network**  |The VPN connection will not be used when the device is connected to a home Wi-Fi network.|All|  
|**Per App VPN (iOS 7 and later, Mac OS X 10.9 and later )** |Associate this VPN connection with an iOS app so that the connection will be opened when the app is run. You can associate the VPN profile with an app when you deploy it.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
|**Custom XML (optional)** |Specify custom XML commands that configure the VPN connection.<br /><br /> Examples:<br /><br /> For **Pulse Secure**:<br /><br /> **&lt;pulse-schema><br /> &nbsp; &lt;isSingleSignOnCredential>true&lt;/isSingleSignOnCredential\><br />&lt;/pulse-schema>**<br /><br /> For **CheckPoint Mobile VPN**:<br /><br /> **&lt;CheckPointVPN <br /> &nbsp; port="443" name="CheckPointSelfhost" <br /> &nbsp; sso="true" <br /> &nbsp; debug="3"<br />/>**<br /><br /> For **Dell SonicWALL Mobile Connect**:<br /><br /> **&lt;MobileConnect\><br />&nbsp; &nbsp; &lt;Compression\>false&lt;/Compression\><br />&nbsp; &nbsp; &lt;debugLogging\>True&lt;/debugLogging\><br />&nbsp; &nbsp; &lt;packetCapture\>False&lt;/packetCapture\><br />&lt;/MobileConnect\>**<br /><br /> For **F5 Edge Client**:<br /><br /> **&lt;f5-vpn-conf>&lt;single-sign-on-credential>&lt;/f5-vpn-conf>**<br /><br /> Refer to each manufacturers VPN documentation for more information about how to write custom XML commands.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  

> [!NOTE]  
>  For information specific to creating VPN profiles for mobile devices, see [Create VPN Profiles](../../mdm/deploy-use/create-vpn-profiles.md)  

Complete the wizard. The new VPN profile is displayed in the **VPN Profiles** node in the **Assets and Compliance** workspace.

### Next steps

- For third-party VPN connections, distribute the VPN app before deploying the VPN profile. If you don't deploy the app, users will be prompted to do so when they try to connect to the VPN. To learn how to deploy apps, see [Deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

- Deploy the VPN profile as described in [How to deploy profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  
