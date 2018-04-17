---
title: "VPN profiles"
titleSuffix: "Configuration Manager"
description: "VPN Profiles on mobile devices in System Center Configuration Manager."
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: 18
caps.handback.revision: 0
author: lleonard-msft
ms.author: alleonar
manager: angrobe
---
# VPN Profiles on mobile devices in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use VPN profiles in System Center Configuration Manager to deploy VPN settings to mobile device users in your organization. When you deploy these settings, you minimize the end-user effort that's required to connect to resources on the company network.  

 For example, you want to set up all devices that run the iOS operating system by using the settings that are required to connect to a file share on the corporate network. You can create a VPN profile that has the necessary settings to connect to the corporate network and then deploy this profile to all users who have devices that run iOS in your hierarchy. Users of iOS devices see the VPN connection in the list of available networks and can connect to this network with the minimum of effort.  

 When you create a VPN profile, you can include a wide range of security settings. For example, you can specify certificates for server validation and client authentication that have been set up by using System Center Configuration Manager certificate profiles. For more about certificate profiles, see [Certificate profiles in System Center Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md).  

 ## VPN profiles when using Configuration Manager together with Intune

 To deploy profiles to iOS, Android, Windows Phone, and Windows 8.1 devices, these devices must be enrolled in Microsoft Intune. Devices on other platforms can also be enrolled to Intune. For information about how to enroll, see [Manage mobile devices with Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx). This table shows the connection type that is supported for each device platform:  

 |Connection type|iOS and macOS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop and Mobile|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|Yes|Yes|No|No|No|No|No|
 |Cisco (IPSec)|iOS only|No|No|No|No|No|No|  
 |Pulse Secure|Yes|Yes|Yes|No|Yes|Yes|Yes|  
 |F5 Edge Client|Yes|Yes|Yes|No|Yes|Yes|Yes|  
 |Dell SonicWALL Mobile Connect|Yes|Yes|Yes|No|Yes|Yes|Yes|  
 |Check Point Mobile VPN|Yes|Yes|Yes|No|Yes|Yes|Yes|  
 |Microsoft SSL (SSTP)|No|No|Yes|Yes|Yes|No|No|  
 |Microsoft Automatic|No|No|Yes|Yes|Yes|No|Yes|  
 |IKEv2|Yes (Custom policy, iOS 9 and later)|No|Yes|Yes|Yes|Yes|Yes|  
 |PPTP|Yes|No|Yes|Yes|Yes|No|Yes|  
 |L2TP|Yes|No|Yes|Yes|Yes|No|Yes (OMA-URI)|  

## Create VPN profiles
[How to Create VPN profiles in System Center Configuration Manager](../../protect/deploy-use/create-vpn-profiles.md) provides general information about how to create VPN profiles.

## Windows 10 VPN features available when using Configuration Manager with Intune  


> [!NOTE]  
> The name of a VPN profile that uses Windows 10 VPN features cannot be in Unicode or include special characters.


|Option|More information|Connection type|  
    |------------|----------------------|---------------------|  
    |**Bypass VPN when connected to company Wi-Fi network**|The VPN connection will not be used when the device is connected to the company Wi-Fi network. Enter the trusted network name that's  used to determine if the device is connected to the company network.|All|  
    |**Network traffic rules**|Set the protocols, local port, remote port, and address ranges that will be enabled for the VPN connection.<br /><br /> **Note:** If you do not create a network traffic rule, all protocols, ports, and address ranges are enabled. After you create a rule, only the protocols, ports, and address ranges that you specify in that rule or in additional rules will be used by the VPN connection.|All|  
    |**Routes**|Routes that will use the VPN connection. Note that creation of more than 60 routes may cause the policy to fail. |All|  
    |**DNS servers**|DNS servers that are used by the VPN connection after the connection has been established.|All|  
    |**Apps that automatically connect to the VPN**|You can add apps or import lists of apps that will automatically use the VPN connection. The type of app will determine the app identifier. For a desktop app, provide the file path of the app. For a universal app, provide the package family name (PFN). To learn how to find the PFN for an app, see [Find a package family name for per-app VPN](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |All|

> [!IMPORTANT]
> We recommend that you secure all lists of associated apps that you compile for use in configuration of per-app VPN. If an unauthorized user changes your list and you import it to the per-app VPN app list, you will potentially authorize VPN access to apps that should not have access. One way you can secure app lists is by using an access control list (ACL).

1. On the **Supported Platforms** page of the **Create VPN Profile Wizard**, select the operating systems on which the VPN profile will be installed, or choose **Select all** to install the VPN profile on all available operating systems.  
2.  On the **Authentication Method** page of the wizard, specify:  

    -   **Authentication method**: Select the authentication method that the VPN connection will use. Available methods depend on the connection type as shown in this table.  

        |Authentication method|Supported&nbsp;connection&nbsp;types|  
        |---------------------------|--------------------------------|  
        |**Certificates**<br /><br /> **Notes:**<ul><li>If the client certificate authenticates to a RADIUS server, like a Network Policy Server, the Subject Alternative Name in the certificate must be set to the User Principal Name.</li><li>For Android deployments, select the EKU identifier and the certificate issuer thumbprint hash value.  Otherwise, users must select the appropriate certificate manually.</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> Check Point Mobile VPN</li></ul>|  
        |**Username and Password**|<ul><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> Check Point Mobile VPN</li></ul>|  
        |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
        |**Microsoft protected EAP (PEAP)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Microsoft secured password (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Smart Card or other certificate**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**RSA SecurID** (iOS only)|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Use machine certificates**|<ul><li>IKEv2</li></ul>|  

         Depending on the selected options, you might be asked to specify more information, like:  

        -   **Remember the user credentials at each logon**: User credentials are remembered so that users don't have to enter them each time they connect.  

        -   **Select a client certificate for client authentication**: Select the previously created client [SCEP certificate](create-pfx-certificate-profiles.md) that will be used to authenticate the VPN connection.   

            > [!NOTE]  
            >  For iOS devices, the SCEP profile that you select will be embedded in the VPN profile. For other platforms, an applicability rule is added to ensure that the VPN profile is not installed if the certificate is not present or is not compliant.  
            >   
            >  If the SCEP certificate that you specify is not compliant or has not been deployed, then the VPN profile
            >  will not be installed on the device.
            >  
            >  Devices that run iOS support only RSA SecurID and MSCHAP v2 for the authentication method when the connection type is PPTP. To avoid reporting errors, deploy a separate PPTP VPN profile to devices that run iOS.  

        - **Conditional access**
			- Choose **Enable conditional access for this VPN connection** to ensure that devices that connect to the VPN are tested for conditional access compliance before connecting. Compliance policies are described in [Device compliance policies in System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/device-compliance-policies.md).
			- Choose **Enable single sign-on (SSO) with alternate certificate** to choose a certificate other than the VPN Authentication certificate for device compliance. If you choose this option, provide the **EKU** (comma-separated list) and **Issuer Hash**, for the correct certificate that the VPN client should locate.

         - For **Windows Information Protection**, provide the enterprise-managed corporate identity, which is usually your organization's primary domain, for example, *contoso.com*. You can specify multiple domains that you organization owns by separating them with the "|" character. For example, *contoso.com|newcontoso.com*.   
	      	For more about Windows Information Protection, see [Create a Windows Information Protection (WIP) policy using Microsoft Intune](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Configure conditional access for VPN](media/vpn-conditional-access.png)

         When supported by the version of Windows that runs Configuration Manager _and_ the selected authorization method, you can choose **Configure** to open the Windows properties dialog box and configure authentication method properties.  If **Configure** is disabled, use a different means to configure authentication method properties.

3.  On the **Proxy Settings** page of the **Create VPN Profile Wizard**, check the **Configure proxy settings for this VPN profile** box if your VPN connection uses a proxy server. Then, provide the proxy server information. For more information, see the Windows Server documentation.  

	> [!NOTE]  
	>  On Windows 8.1 computers, the VPN profile will not show the proxy information until you connect to the VPN by using that computer.  


4. Configure further DNS settings (if required).  

5. Finish the wizard. The **VPN Profiles** node in the **Assets and Compliance** workspace shows the new VPN profile.  


**Deploy**: See [Deploy Wi-Fi, VPN, email, and certificate profiles](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) for more about how to deploy VPN profiles.

## Next steps  
 Use the following topics to help you plan for, set up, operate, and maintain VPN profiles in Configuration Manager.  

-   [Prerequisites for VPN profiles in System Center Configuration Manager](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Security and privacy for VPN profiles in System Center Configuration Manager](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
