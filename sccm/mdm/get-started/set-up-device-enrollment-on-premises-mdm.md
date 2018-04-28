---
title: "Set up device enrollment "
titleSuffix: "Configuration Manager"
description: "Grant users permission to enroll their devices for On-premises Mobile Device Management in System Center Configuration Manager."
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Set up device enrollment for On-premises Mobile Device Management in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Enabling users to enroll their devices for System Center Configuration Manager On\-premises Mobile Device Management requires you to grant them permission to do so. To grant users permission to enroll devices, follow the tasks below.

-   [Create an enrollment profile that allows users to enroll modern devices](#bkmk_createProf)  

-   [Set up additional client settings for enrolled devices](#bkmk_addClient)  

-   [Enable users to receive the modern device enrollment profile](#bkmk_enableUsers)  

-   [Store the root certificate on devices to be enrolled](#bkmk_storeCert)  

##  <a name="bkmk_createProf"></a> Create an enrollment profile that allows users to enroll modern devices  
 To push the settings required to allow users to enroll modern devices, you can add a new enrollment profile to the default client settings, which gets applied to all discovered users in the Configuration Manager site.  

1.  In the Configuration Manager console, click **Administration** > **Overview** > **Client Settings**, open **Default Client Settings** and select **Enrollment**.  

2.  Under Device Settings, specify the polling interval for modern devices.  

3.  Under User Settings, select **Yes** for **Allow users to enroll modern devices**.  

4.  Next to **Modern device enrollment profile**, click **Set Profile...** and then click **Create...**  

5.  In Create Enrollment Profile, type a name for the enrollment profile, and choose the management site code you want users with the enrollment profile to use. Click **OK** several times to exit the Default Settings page.  

> [!NOTE]  
>  If you want to deploy the enrollment profile to a subset of discovered users, you can use a user collection, and create custom client settings to deploy to that collection. For information on creating custom client settings, see [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md)  

##  <a name="bkmk_addClient"></a> Set up additional client settings for enrolled devices  
 In addition to setting up the enrollment profile fo modern devices, you can set up additional client settings for configuring devices when they're enrolled.  For  information on setting up client settings, see [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

 Not all client settings are available for On\-premises Mobile Device Management. The current branch of Configuration Manager supports the following client settings for On\-premises Mobile Device Management:  

-   Enrollment - these settings specify  the enrollment profile for managed devices. For more information on how to set up an enrollment profile, see [Create an enrollment profile that allows users to enroll modern devices](#bkmk_createProf).  

-   Client policy - theses settings specify the frequency for downloading client policy to the device. You can also enable settings for  targeting users with policy polling. For more information on client policy settings, see the Client Policy section in [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

-   Software deployment - this setting sets the interval for evaluating client devices for software deployments. For more information of software deployment settings, see the Software Deployment section in [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md)  

    > [!NOTE]  
    >  For On\-premises Mobile Device Management, software deployment settings can only be used as default client settings. Software deployment settings cannot be used with custom client settings in the current branch of Configuration Manager.  

##  <a name="bkmk_enableUsers"></a> Enable users to receive the modern device enrollment profile  
 For users to receive the modified client settings with the enrollment profile for On\-premises Mobile Device Management, they must be discovered     through the Active Directory discovery method. To make sure everyone that needs the enrollment profile gets it, run discovery for Active Directory users. For instructions on how to discover users, see [Run discovery for System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

##  <a name="bkmk_storeCert"></a> Store the root certificate on devices to be enrolled  
 Users with domain-joined devices will likely already have the required root certificate for trusted communication with the servers hosting the site system roles because the root was issued as part of the domain-joining process with Active Directory. Non-domain joined computers and mobile devices will need the root certificate manually installed on the device to allow for enrollment to take place. These devices will not automatically have the required root certificate.  

 The exported certificate file must be provided to the device for manual installation. This can be done using email, OneDrive, SD card, USB thumbdrive, or whatever method works best for your needs.  

 The root certificate you want to use on the devices is the one you exported in [Export the certificate with the same root as the web server certificate](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).  

1.  On the device to be enrolled, locate the root certificate file and double-click it.  

2.  In Certificate window, click **Install Certificate...**  

3.  In the Certificate Import Wizard, select **Local Machine**, and click **Next**.  

4.  In the User Account Control window, click **Yes**.  

5.  Select **Place all certificates in the following store**, and click **Browse**.  

6.  Click **Trusted Root Certification Authorities**, click **OK**, and then click **Next**.  

7.  Click **Finish**.  
