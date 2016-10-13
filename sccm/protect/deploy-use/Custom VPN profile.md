---
# required metadata

title: Create a custom VPN profile | System Center Configuration Manager
description: Create VPN profiles for Windows 8 and later devices.
keywords:
ms.author: nbigman
ms.manager: angerobe
ms.date: 10/10/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:- configmgr-other
ms.assetid: 53a8c892-8ebc-4d1e-8332-0ff43003ec3d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Create a custom configuration
You can use custom configurations to create VPN profiles for Windows 8 and later devices when using Configuration Manager with Microsoft Intune. 

> [!IMPORTANT]
>
> After you deploy a custom VPN profile, removing the profile will not uninstall the profile from the device. Here are several ways to remove the profile from the device, ranked from easiest to most difficult:
> 
> 1. Deploy a non-custom profile with the same name to those devices, overwriting the custom profile.
> 2. Manually remove the VPN profile from the device.
> 3. Un-enroll, then re-enroll the device.
> 4. Wipe and restore the device.

To create a custom configuration profile:

   1. In the admin console, go to **Assets and Compliance** > **Overview** > **Compliance Settings** > **Configuration Items** > **Create configuration item** to start the Create Configuration Item wizard.
   2. Choose the supported platforms for the profile.
   3. At the bottom of the **Device Settings** page, choose **Configure additional settings that are not in the default setting groups** and click **Next**.
   4. Choose **Add** > **Create Setting**.
   5. In the **Create setting** dialog, provide the OMA-URI as shown in this example:
   
   ![oma-uri-create-setting_new](/Image/oma-uri-create-setting_new.png)
   
   6. After you create the setting and click **OK**, choose the new setting on the **Browse settings** dialog, and choose **Select**.
   
   ![oma-uri-browse-settings](/Image/oma-uri-browse-settings.png)
    
   6. Create a rule to specify the value as shown in this example:
   
   ![oma-uri-create_rule-new](/Image/oma-uri-create_rule-new.png)
    
   7. Repeat the setting and rule creation for each setting in the profile.
   
   8. Complete the Create Configuration Item wizard. You can now add the  item to a configuration baseline and deploy it to a collection.
   
> [!NOTE]
> For Windows 10, you can create a profile in XML and then save it as the value for the ProfileXML setting.
  
   

## Example of URI settings for a custom VPN profile configuration

Here are example entries for URI values to create a custom configuration for a VPN in a fictitious company called Contoso. For more information, like the data type for each entry, see [VPNv2 CSP](https://msdn.microsoft.com/library/windows/hardware/dn914776.aspx).

Native Contoso VPN (IKEv2):
./Vendor/MSFT/VPNv2/ContosoVPN/NativeProfile/Servers

vpn.contoso.com
./Vendor/MSFT/VPNv2/ContosoVPN/NativeProfile/NativeProtocolType

Ikev2
./Vendor/MSFT/VPNv2/ContosoVPN/NativeProfile/RoutingPolicyType

SplitTunnel
./Vendor/MSFT/VPNv2/ContosoVPN/NativeProfile/Authentication/UserMethod

Eap
./Vendor/MSFT/VPNv2/ContosoVPN/NativeProfile/Authentication/Eap/Configuration
&lt;EapHostConfig xmlns="http://www.microsoft.com/provisioning/EapHostConfig"&gt;&lt;EapMethod&gt;&lt;Type xmlns="http://www.microsoft.com/provisioning/EapCommon"&gt;13&lt;/Type&gt;&lt;VendorId xmlns="http://www.microsoft.com/provisioning/EapCommon"&gt;0&lt;/VendorId&gt;&lt;VendorType xmlns="http://www.microsoft.com/provisioning/EapCommon"&gt;0&lt;/VendorType&gt;&lt;AuthorId xmlns="http://www.microsoft.com/provisioning/EapCommon"&gt;0&lt;/AuthorId&gt;&lt;/EapMethod&gt;&lt;Config xmlns="http://www.microsoft.com/provisioning/EapHostConfig"&gt;&lt;Eap xmlns="http://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"&gt;&lt;Type&gt;13&lt;/Type&gt;&lt;EapType xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"&gt;&lt;CredentialsSource&gt;&lt;CertificateStore&gt;&lt;SimpleCertSelection&gt;true&lt;/SimpleCertSelection&gt;&lt;/CertificateStore&gt;&lt;/CredentialsSource&gt;&lt;ServerValidation&gt;&lt;DisableUserPromptForServerValidation&gt;false&lt;/DisableUserPromptForServerValidation&gt;&lt;ServerNames&gt;&lt;/ServerNames&gt;&lt;/ServerValidation&gt;&lt;DifferentUsername&gt;false&lt;/DifferentUsername&gt;&lt;PerformServerValidation xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"&gt;false&lt;/PerformServerValidation&gt;&lt;AcceptServerName xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"&gt;false&lt;/AcceptServerName&gt;&lt;/EapType&gt;&lt;/Eap&gt;&lt;/Config&gt;&lt;/EapHostConfig&gt;

**./Vendor/MSFT/VPNv2/ContosoVPN/ByPassForLocal**
True

**./Vendor/MSFT/VPNv2/ContosoVPN/RememberCredentials**
1

**./Vendor/MSFT/VPNv2/ContosoVPN/DomainNameInformationList/1/DomainName**
Corp.Contoso.com

**./Vendor/MSFT/VPNv2/ContosoVPN/DnsSuffix**
Corp.Contoso.com

**./Vendor/MSFT/VPNv2/ContosoVPN/TrustedNetworkDetection**
Corp.Contoso.com

**./Vendor/MSFT/VPNv2/ContosoVPN/RouteList/1/Address**
10.0.0.0

**./Vendor/MSFT/VPNv2/ContosoVPN/RouteList/1/PrefixSize**
8

**./Vendor/MSFT/VPNv2/ContosoVPN/AlwaysOn**
true

**./Vendor/MSFT/VPNv2/ContosoVPN/AppTriggerList/0/App/Id**
%PROGRAMFILES%\Internet Explorer\iexplore.exe

**./Vendor/MSFT/VPNv2/ContosoVPN/AppTriggerList/1/App/Id**
%PROGRAMFILES% (x86)\Internet Explorer\iexplore.exe

**./Vendor/MSFT/VPNv2/ContosoVPN/AppTriggerList/2/App/Id**
Microsoft.MicrosoftEdge_8wekyb3d8bbwe

**./Vendor/MSFT/VPNv2/ContosoVPN/TrafficFilterList/0/App/Id**
%PROGRAMFILES% (x86)\Internet Explorer\iexplore.exe

**./Vendor/MSFT/VPNv2/ContosoVPN/TrafficFilterList/1/App/Id**
Microsoft.MicrosoftEdge_8wekyb3d8bbwe

For any questions about how these settings should be used or more details about what they do, see the [configuration service provider (CSP) documentation](https://msdn.microsoft.com/en-us/library/windows/hardware/dn914776.aspx).

