---
title: "Enable the Partner Notification API"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 99994d2a-dbc5-4ae0-b77c-4cbfdbd8bcd6searchScope: - ConfigMgr SDK
caps.latest.revision: 13
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Enable the Partner Notification API
The Partner Notification API allows third-party partners to use the Wake on LAN feature of System Center Configuration Manager to receive a list of computers that need to be woken up based on advertisements for software distribution.  

 Before you can enable the Partner Notification API, you must configure Wake on LAN for each primary site for which you want to enable this feature.  For more information about configuring Wake on LAN, see [How to configure Wake on LAN in System Center Configuration Manager](https://technet.microsoft.com/en-us/library/mt757110.aspx).  

### To enable the Partner Notification API  

1.  Set the following registry keys on the computer for each primary site where you want to enable this feature:  

    -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_WAKEONLAN_MANAGER\CreatePartnerNotification` Set the value to 1 to enable the Partner Notification API and create a partner notification file. This key is set to 0 by default.  

    -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_WAKEONLAN_MANAGER\DeletePartnerNotificationOlderThanDays` Deletes partner notification files older than the indicated number of days. The default value is 3 days.  

         The partner notification file is a .csv file that contains a list of computers, by their FQDN, that you can wake with your custom code.  

2.  Restart the SMS_EXECUTIVE service on each computer where you updated the registry keys.  

3.  Create an advertisement  by using the [SMS_Advertisement Server WMI Class](../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md). Set the `OfferType` value to 0 and the `AdvertFlags` value to 0x00400000. For more information about advertisements, see [How to Create an Advertisement](../../../../develop/core/servers/configure/how-to-create-an-advertisement.md) and [How to Configure a Software Distribution Mandatory Advertisement for Wake On LAN](../../../../develop/core/servers/configure/how-to-configure-a-mandatory-advertisement-for-wake-on-lan.md).  

4.  Use the `AssignedSchedule` and `AssignedScheduleEnabled` properties to set a schedule for your advertisement.  

     When the advertisement deadline is met, and Configuration Manager attempts to wake the computers, a partner notification file is generated and stored in the following location: \<Configuration Manager Installation Directory>\inboxes\WOLMGR.box\Partners.  If the `OfferType` property in the advertisement is not set to 0, Configuration Manager will not try to wake up computers through Wake on LAN, thus notification files are not generated.  

5.  Use the list of computers in the partner notification file to wake the computers with your custom code.  

## See Also  
 [Software Distribution Wake On LAN](../../../../develop/core/servers/configure/software-distribution-wake-on-lan.md)   
 [How to Create an Advertisement](../../../../develop/core/servers/configure/how-to-create-an-advertisement.md)   
 [How to Configure a Software Distribution Mandatory Advertisement for Wake On LAN](../../../../develop/core/servers/configure/how-to-configure-a-mandatory-advertisement-for-wake-on-lan.md)
