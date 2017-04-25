---
title: "VPN Profiles in System Center Configuration Manager | Microsoft Docs"
description: "VPN Profiles on mobile devices in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
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

Use VPN profiles in System Center Configuration Manager to deploy VPN settings to mobile device users in your organization. By deploying these settings, you minimize the end-user effort required to connect to resources on the company network.  

 For example, you want to provision all devices that run the iOS operating system with the settings required to connect to a file share on the corporate network. You can create a VPN profile containing the settings necessary to connect to the corporate network and then deploy this profile to all users that have devices that run iOS in your hierarchy. Users of iOS devices see the VPN connection in the list of available networks and can connect to this network with the minimum of effort.  

 When you create a VPN profile, you can include a wide range of security settings, including certificates for server validation and client authentication that have been provisioned by using System Center Configuration Manager certificate profiles. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md).  

 ## VPN profiles when using Configuration Manager together with Intune

 To deploy profiles to iOS, Android, Windows Phone, and Windows 8.1 devices, these devices must be enrolled into Microsoft Intune. Devices on other platforms can also be enrolled to Intune. For information about how to enroll, see [Manage mobile devices with Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx). This table shows which connection type is supported for each device platform:  

 |Connection type|iOS    and Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop and Mobile|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|Yes|Yes|No|No|No|No|Yes (OMA-URI)|  
 |Pulse Secure|Yes|Yes|Yes|No|Yes|Yes|Yes|  
 |F5 Edge Client|Yes|Yes|Yes|No|Yes|Yes|Yes|  
 |Dell SonicWALL Mobile Connect|Yes|Yes|Yes|No|Yes|Yes|Yes|  
 |Check Point Mobile VPN|Yes|Yes|Yes|No|Yes|Yes|Yes|  
 |Microsoft SSL (SSTP)|No|No|Yes|Yes|Yes|No|No|  
 |Microsoft Automatic|No|No|Yes|Yes|Yes|No|Yes (OMA-URI)|  
 |IKEv2|Yes (Custom policy)|No|Yes|Yes|Yes|Yes|Yes (OMA-URI)|  
 |PPTP|Yes|No|Yes|Yes|Yes|No|Yes (OMA-URI)|  
 |L2TP|Yes|No|Yes|Yes|Yes|No|Yes (OMA-URI)|  

## Create VPN Profiles
[How to Create VPN profiles in System Center Configuration Manager](../../protect/deploy-use/create-vpn-profiles.md) provides general information about creating VPN profiles.

###   Windows 10 VPN features, available when using Configuration Manager with Intune  


> [!NOTE]  
> The name of a VPN profile that uses Windows 10 VPN features cannot be in unicode or include special characters.


|Option|More information|Connection type|  
    |------------|----------------------|---------------------|  
    |**Bypass VPN when connected to company Wi-Fi network**|The VPN connection will not be used when the device is connected to the company Wi-Fi network. Enter the trusted network name,  used to determine if the device is connected to the company network.|All|  
    |**Network traffic rules**|Set which protocols, local and remote port and address ranges will be enabled for the VPN connection.<br /><br /> **Note:** If you do not create a network traffic rule, all protocols, ports and address ranges are enabled. Once you create a rule, only the protocols, ports and address ranges that you specify in that rule or in additional rules will be used by the VPN connection.|All|  
    |**Routes**|Which routes will use the VPN connection. Note that creation of more than 60 routes may cause the policy to fail. |All|  
    |**DNS servers**|Which DNS servers are used by the VPN connection once the connection has been established.|All|  
    |**Apps that automatically connect to the VPN**|You can add apps, or import lists of apps, that will automatically use the VPN connection. The type of app will determine the app identifier. For a desktop app, provide the file path of the app. For a universal app, provide the package family name (PFN). To learn how to find the PFN for an app, see [Find a package family name for per-app VPN](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |All|

> [!IMPORTANT]
> We recommend that you secure all lists of associated apps that you compile for use in configuration of per-app VPN. If an unauthorized user modifies your list and you import it into the per-app VPN app list, you will potentially authorize VPN access to apps that should not have access. One way you can secure app lists is by using an access control list (ACL).


1.  On the **Authentication Method** page of the wizard, specify:  

    -   **Authentication method:** Select the authentication method that the VPN connection will use. Available methods depend on the connection type as shown in this table.  

        |Authentication method|Supported&nbsp;connection&nbsp;types|  
        |---------------------------|--------------------------------|  
        |**Certificates**<br /><br /> **Notes:**<br />- If the client certificate authenticates to a RADIUS server, such as a Network Policy Server, the Subject Alternative Name in the certificate must be set to the User Principal Name.<br/><br />- For Android deployments, select the EKU identifier and the certificate issuer thumbprint hash value.  Otherwise, users must select the appropriate certificate manually.  |- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Username and Password**|- Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Microsoft EAP-TTLS**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - IKEv2<br /><br /> - L2TP|  
        |**Microsoft protected EAP (PEAP)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Microsoft secured password (EAP-MSCHAP v2)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Smart Card or other certificate**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**MSCHAP v2**|-  Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**RSA SecurID** (iOS only)|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Use machine certificates**|IKEv2|  

         Depending on the options you select, you might be asked to specify further information, such as:  

        -   **Remember the user credentials at each logon**: User credentials are remembered so that the user does not have to enter them each time they connect.  

        -   **Select a client certificate for client authentication** - Select the client [SCEP certificate](create-pfx-certificate-profiles.md) that you previously created that will be used to authenticate the VPN connection.   

            > [!NOTE]  
            >  For iOS devices, the SCEP profile you select will be embedded in the VPN profile. For other platforms, an applicability rule is added to ensure that the VPN profile is not installed if the certificate is not present, or not compliant.  
            >   
            >  If the SCEP certificate you specify is not compliant, or has not been deployed, then the VPN profile
            >  will not be installed on the device.
            >  
            >  Devices that run iOS support only RSA SecurID and MSCHAP v2 for the authentication method when the connection type is PPTP. To avoid reporting errors, deploy a separate PPTP VPN profile to devices that run iOS.  

        - **Conditional access**
			- Choose **Enable conditional access for this VPN connection** to ensure that devices that connect to the VPN are tested for conditional access compliance before connecting. Compliance policies are described in [Device compliance policies in System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md)
			- Choose **Enable single sign-on (SSO) with alternate certificate** to choose a certificate other than the VPN Authentication cert for device compliance. If you choose this option, provide the **EKU** (comma-separated list) and **Issuer Hash**, for the correct certificate that the VPN Client should locate.

         - **Windows Information Protection** - provide the enterprise-managed corporate identity, which is usually your organization's primary domain, for example, *contoso.com*. You can specify multiple domains owned by your organization by separating them with the "|" character. For example, *contoso.com|newcontoso.com*.   
	      	For information about Windows Information Protection, see [Create a Windows Information Protection (WIP) policy using Microsoft Intune](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Configure conditional access for VPN](media/vpn-conditional-access.png)


> [!NOTE]  
> For some authentication methods, you can click **Configure** to open the Windows properties dialog box (if the version of Windows on which you are running the Configuration Manager console supports this authentication method) where you can configure the authentication method properties.  

2.  On the **Proxy Settings** page of the **Create VPN Profile Wizard**, select the **Configure proxy settings for this VPN profile** check box if your VPN connection uses a proxy server. Then, provide the proxy server information. For more information, see the Windows Server documentation.  

	> [!NOTE]  
	>  On Windows 8.1 computers, the VPN profile will not display the proxy information until you connect to the VPN with that computer.  


3. Configure Further DNS Settings (if required)  
 On the **Configure Automatic VPN connection** page , you can configure the following:  

	-   **Enable VPN on-demand** Use if you want to configure further DNS settings for Windows Phone 8.1 devices. This setting applies only to Windows Phone 8.1 devices and should only be enabled on VPN profiles that are going to be deployed to Windows Phone 8.1 devices.

	-   DNS Suffix list (Windows Phone 8.1 devices only) - Configures domains that will establish a VPN connection. For each domain you specify, add the DNS suffix, the DNS server address, and one of the following on-demand actions:  

    	-   **Never establish** - Never open a VPN connection  

	    -   **Establish if needed** - Only open a VPN connection if the device needs to connect to resources  

	    -   **Always establish** - Always open the VPN connection  

	-   **Merge** -  Copies any DNS suffices you configured into the **Trusted network list**.  

	-   **Trusted network list** (Windows Phone 8.1 devices only) - Specify one DNS suffix on each line. If the device is in a trusted network, the VPN connection will not be opened.  

	-   **Suffix search list** (Windows Phone 8.1 devices only) - Specify one DNS suffix on each line. Each DNS suffix will be searched when connecting to a website using a short name.  

     For example, you specify the DNS suffices **domain1.contoso.com** and **domain2.contoso.com** and then visit the URL **http://mywebsite**. The following addresses will be searched:  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

	> [!NOTE]  
	>  For Windows Phone 8.1 devices only  
	>   
	>  If the **Send all network traffic through the VPN connection** option is selected, and the VPN connection is using full tunneling, for the first profile provisioned on the device, the VPN connection will automatically open. If you want a different profile to automatically open a connection, you must make it the default profile on the device.  
	>   
	>  If the **Send all network traffic through the VPN connection** option is not selected, and the VPN connection is using split-tunneling, a VPN connection can automatically be opened if you configure routes, or a connection specific DNS suffix.  


4. On the **Supported Platforms** page of the **Create VPN Profile Wizard**, select the operating systems on which the VPN profile will be installed, or click **Select all** to install the VPN profile on all available operating systems.  

5. Complete the wizard. The new VPN profile is displayed in the **VPN Profiles** node in the **Assets and Compliance** workspace.  


**Deploy:** See [Deploy Wi-Fi, VPN, email, and certificate profiles](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) for information about deploying VPN profiles.

### Next steps  
 Use the following topics to help you plan for, configure, operate, and maintain VPN profiles in Configuration Manager.  

-   [Prerequisites for VPN profiles in System Center Configuration Manager](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Security and privacy for VPN profiles in System Center Configuration Manager](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
