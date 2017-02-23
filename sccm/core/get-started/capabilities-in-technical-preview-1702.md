---
title: "Capabilities in Technical Preview 1702 Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1702."
ms.custom: na
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1702 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*



This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1702. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

##  Send feedback from the Configuration Manager console

This preview introduces new feedback options in the Configuration Manager console. The Feedback options lets you send feedback directly to the development team, by way of the Configuration Manager UserVoice feedback website.  

>You can find the **Feedback** option:
-  In the ribbon, at the far left of the Home tab of each node.  
   ![Ribbon](./media/feedback-home.png)

-  When you right-click on any object in the console.   
    ![Righ-click option](./media/feedback-option.png)   

Choosing **Feedback** opens your browser to the Configuration Manager UserVoice feedback website, at https://configurationmanager.uservoice.com/forums/300492-ideas.
##  Changes for Updates and Servicing
The following are introduced with this preview.

**Simpler update choices**  
The next time your infrastructure qualifies for two or more updates, only the latest update is downloaded. For example, if your current site version is two or more older than the most recent version that is available, only that most recent update version is downloaded automatically.  

You have the option to download and install the other available updates, even when they are not the most current version. However, you will receive a warning that the update has been replaced by a newer one. To download an update that is *Available to Download*, select the update in the console and then click **Download**.

**Improved cleanup of older updates**   
We added an automatic clean-up function that deletes the unneeded downloads from the ‘EasySetupPayload’ folder on your site server.  


## Peer Cache improvements
Starting with this release, a peer cache source computer will reject a request for content when the peer cache source computer meets any of the following conditions:  
 - 	Is in low battery mode.
 -  CPU load exceeds 80% at the time the content is requested.
 -  Disk I/O has an *AvgDiskQueueLength* that exceeds 10.
 -  There are no more available connections to the computer.   

When the computer rejects a request for the content, the requesting computer will continue to seek content form alternate sources in its pool of available content source locations.   

## <a name="azurediscovery"></a> Use Azure Active Directory Domain Services to manage devices, users, and groups

With this technical preview version you can manage devices that are joined to an Azure Active Directory (AD) Domain Services managed domain. You can also discover devices, users, and groups in that domain with various Configuration Manager Discovery methods.


### Set up Configuration Manager to use Azure AD
To use Azure AD with Configuration Manager, you’ll need the following:
-	Azure subscription.
-	Azure AD with Domain Services (DS).
-	A Configuration Manager site that runs on an Azure VM that is joined to your Azure AD.
-	Configuration Manager clients that run in the same Azure AD environment.

To configure Azure AD Domain Service, see [Get started with Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started).

### Discover resources
After you set up Configuration Manager to run in Azure AD, you can use the following Active Directory discovery methods to search for resources:  
- Active Directory System Discovery
- Active Directory User Discovery
- Active Directory Group Discovery  

For each method you use, edit the LDAP query to search the Azure AD OU structures instead of the containers that are typical to on-premises Active Directory. This requires you to direct the query to search your Active Directory in your Azure subscription.  

The following examples use an Azure AD of *contoso.onmicrosoft.com*:
 - **System Discovery**   
Azure AD stores devices under the **AADDC Computers** OU.  Configure the following:  
  -	*LDAP://OU=AADDC Computers,DC=contoso,DC=onmicrosoft,DC=com*  


- **User Discovery**
AAD stores users under the **AADDC Users** OU.  Configure the following:
  - *LDAP://OU=AADDC Users,DC= contoso,DC=onmicrosoft,DC=com*


- **Group Discovery**  
Azure AD does not have an OU that stores groups. Instead, use the same general structure as the System or User queries and configure the LDAP query to point to the OU that contains the groups you want to discover.

See the following for more information about Azure AD:  
 - [Azure Active Directory Domain Services](https://azure.microsoft.com/en-us/services/active-directory-ds) on azure.microsoft.com.
 - [Active Directory Domain Services Documentation](https://docs.microsoft.com/azure/active-directory-domain-services) on docs.microsoft.com.

## Conditional access device compliance policy improvements

A new device compliance policy rule is available to help you block access to corporate resources that support conditional access, when users are using apps that are part of a non-compliant list of apps. The non-compliant list of apps can be defined by the admin when adding the new compliant rule **Apps that cannot be installed**. This rule requires the admin to enter the **App Name**, the **App ID**, and the **App Publisher** (optional) when adding an app to the non-compliant list. This setting only applies to iOS and Android devices.

Additionally, this helps organizations to mitigate data leakage through unsecured apps, and prevent excessive data consumption through certain apps.

- Learn more [how device compliance policies work](https://docs.microsoft.com/sccm/protect/deploy-use/device-compliance-policies).
- Learn more [how to create device compliance policies](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy).

### Try it out

**Scenario:** Identify apps that might be causing data leakage by sending corporate data outside your company, or that are causing excessive data consumption, then [create a conditional access device compliance policy](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy) that adds these apps into the non-compliant list of apps. This will block access to corporate resources that support conditional access until the user can remove the blocked app.

## Antimalware client version alert
Beginning with this preview version, Configuration Manager Endpoint Protection provides an alert if more than 20% (default) of managed clients are using an expired version of the antimalware client (i.e. Windows Defender or Endpoint Protection client).

### Try it out
Ensure Endpoint Protection is enabled on all desktop and server clients using client settings policy. You can now view **Antimalware Client Version** and **Endpoint Protection Deployment Status** by going **Assets and Compliance** > **Overview** > **Devices** > **All Desktops and Serve Clients**. To check for an alert, view **Alerts** in the **Monitoring** workspace. If more than 20% of managed clients are running an expired version of antimalware software, the Antimalware client version is outdated alert is displayed. This alert doesn’t appear on the **Monitoring** > **Overview** tab. To update expired antimalware clients, enable software updates for antimalware clients.

To configure the percentage at which the alert is generated, expand **Monitoring** > **Alerts** > **All Alerts**, double-click **Antimalware clients out of date** and modify the **Raise alert if percentage of managed clients with an outdated version of the antimalware client is more than** option.
