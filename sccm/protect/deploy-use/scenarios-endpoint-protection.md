---
title: Scenario Endpoint Protection protects computers from malware
titleSuffix: "Configuration Manager"
description: "Learn how to implement Endpoint Protection in Configuration Manager to protect computers from malware attacks."
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
caps.latest.revision: 8
author: mestew
ms.author: mstewart
manager: doubeby

---

# Example scenario: Using System Center Endpoint Protection to protect computers from malware in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article provides an example scenario for how you can implement Endpoint Protection in Configuration Manager to protect computers in an organization from malware attacks.  

 John is the Configuration Manager administrator at Woodgrove Bank. The bank currently uses System Center Endpoint Protection to protect computers against malware attacks. Additionally, the bank uses Windows Group Policy to ensure that the Windows Firewall is enabled on all computers in the company and that users are notified when Windows Firewall blocks a new program.  

 John has been asked to upgrade the Woodgrove Bank antimalware software to System Center Endpoint Protection so that the bank can benefit from the latest antimalware features and be able to centrally manage the antimalware solution from the Configuration Manager console. This implementation has the following requirements:  

-   Use Configuration Manager to manage the Windows Firewall settings that are currently managed by Group Policy.  

-   Use Configuration Manager software updates to download malware definitions to computers. If software updates are not available, for example if the computer is not connected to the corporate network, computers must download definition updates from Microsoft Update.  

-   Users' computers must perform a quick malware scan every day. Servers, however, must run a full scan every Saturday, outside business hours, at 1 A.M.  

-   Send an email alert whenever any one of the following events occurs:  

    -   Malware is detected on any computer  

    -   The same malware threat is detected on more than 5 percent of computers  

    -   The same malware threat is detected more than 5 times in any 24-hour period  

    -   More than 3 different types of malware are detected in any 24-hour period  

-   Uninstall the existing antimalware solution.  

 John then does the following steps to implement Endpoint Protection:  

##  Steps to implement Endpoint Protection  

|Process|Reference|  
|-------------|---------------|  
|John reviews the available information about the basic concepts for Endpoint Protection in Configuration Manager.|For overview information about Endpoint Protection, see [Endpoint Protection in System Center Configuration Manager](endpoint-protection.md).|  
|John reviews and implements the required prerequisites to use Endpoint Protection.|For information about the prerequisites for Endpoint Protection, see [Planning for Endpoint Protection](../plan-design/planning-for-endpoint-protection.md).|  
|John installs the Endpoint Protection site system role on one site system server only, at the top of the Woodgrove Bank hierarchy.|For more information about how to install the Endpoint Protection site system role, see "Prerequisites" in [Configure Endpoint Protection](configure-endpoint-protection.md).|  
|John configures Configuration Manager to use an SMTP server to send the email alerts.<br /><br /> **Note:** You must configure an SMTP server only if you want to be notified by email when an Endpoint Protection alert is generated.|For more information, see [Configure alerts in Endpoint Protection](endpoint-configure-alerts.md).|  
|John creates a device collection that contains all computers and servers to install the Endpoint Protection client. He names this collection **All Computers Protected by Endpoint Protection**.<br /><br /> **Tip:** You cannot configure alerts for user collections.|For more information about how to create collections, see [How to create collections in System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|He configures the following alerts for the collection: <br /><br />1) **Malware is detected**: John configures an alert severity of **Critical**. <br /><br />2) **The same type of malware is detected on a number of computers**: John configures an alert severity of **Critical** and specifies that the alert will be generated when more than 5 percent of computers have malware detected. <br /><br />3) **The same type of malware is repeatedly detected within the specified interval on a computer**: John configures an alert severity of **Critical** and specifies that the alert will be generated when malware is detected more than 5 times in a 24-hour period. <br /><br />4) **Multiple types of malware are detected on the same computer within the specified interval**: John configures an alert severity of **Critical** and specifies that the alert will be generated when more than 3 types of malware are generated in a 24-hour period.<br /><br /> The value for **Alert Severity** indicates the alert level that will be displayed in the Configuration Manager console and in alerts that he receives in an email message.<br /><br /> He additionally selects the option **View this collection in the Endpoint Protection dashboard** so that he can monitor the alerts in the Configuration Manager console.|See "Configure Alerts for Endpoint Protection" in [Configuring Endpoint Protection in System Center Configuration Manager](endpoint-configure-alerts.md).|  
|John configures Configuration Manager software updates to download and deploy definition updates three times a day by using an automatic deployment rule.|For more information, see the "Using Configuration Manager Software Updates to Deliver Definition Updates" section in [Use Configuration Manager software updates to deliver definition updates](endpoint-definitions-configmgr.md).|  
|John examines the settings in the default antimalware policy, which contains recommended security settings from Microsoft. For computers to perform a quick scan every day to, he changes the following settings:<br /><br /> 1) **Run a daily quick scan on client computers**: **Yes**.<br /><br /> 2) **Daily quick scan schedule time**:  **9:00 AM**.<br /><br /> John notes that **Updates distributed from Microsoft Update** is selected by default as a definition update source. This fulfills the business requirement that computers download definitions from Microsoft Update when they cannot receive Configuration Manager software updates.|See [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|John creates a collection that contains only the Woodgrove Bank servers named **Woodgrove Bank Servers**.|See [How to create collections in System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|John creates a custom antimalware policy named **Woodgrove Bank Server Policy**. He adds only the settings for **Scheduled scans** and makes the following changes:<br /><br /> **Scan type**:  **Full**<br /><br /> **Scan day**:  **Saturday**<br /><br /> **Scan time**: **1:00 AM**<br /><br /> **Run a daily quick scan on client computers**:  **No**.|See [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|John deploys the **Woodgrove Bank Server Policy** custom antimalware policy to the **Woodgrove Bank Servers** collection.|See "To deploy an antimalware policy to client computers" [How to create and deploy antimalware policies for Endpoint Protection](endpoint-antimalware-policies.md) article.|  
|John creates a new set of custom client device settings for Endpoint Protection and names these **Woodgrove Bank Endpoint Protection Settings**.<br /><br /> **Note:** If you do not want to install and enable Endpoint Protection on all clients in your hierarchy, make sure that the options **Manage Endpoint Protection client on client computers** and **Install Endpoint Protection client on client computers** are both configured as **No** in the default client settings.|For more information, see [Configure Custom Client Settings for Endpoint Protection](endpoint-protection-configure-client.md).|  
|He configures the following settings for Endpoint Protection:<br /><br /> **Manage Endpoint Protection client on client computers**:  **Yes**<br /><br /> This setting and value ensures that any existing Endpoint Protection client that is installed becomes managed by Configuration Manager.<br /><br /> **Install Endpoint Protection client on client computers**:  **Yes**.</br></br>**Note** Starting in Configuration Manager 1802, Windows 10 devices do not need to have the Endpoint Protection agent installed. If it is already installed on Windows 10 devices, Configuration Manager will not remove it.<br /><br /> **Automatically remove previously installed antimalware software before Endpoint Protection is installed**:  **Yes**.<br /><br /> This setting and value fulfills the business requirement that the existing antimalware software is removed before Endpoint Protection is installed and enabled.|For more information, see [Configure Custom Client Settings for Endpoint Protection](endpoint-protection-configure-client.md).|  
|John deploys the **Woodgrove Bank Endpoint Protection Settings** client settings to the **All Computers Protected by Endpoint Protection** collection.|See "Configure Custom Client Settings for Endpoint Protection" in [Configuring Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md).|  
|John uses the Create Windows Firewall Policy Wizard to create a policy by configuring the following settings for the domain profile:<br /><br /> 1) **Enable Windows Firewall**: **Yes**<br /><br /> 2)<br />                    **Notify the user when Windows Firewall blocks a new program**: **Yes**|See [How to create and deploy Windows Firewall policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|John deploys the new firewall policy to the collection **All Computers Protected by Endpoint Protection** that he created earlier.|See "To deploy a Windows Firewall policy" in the [How to create and deploy Windows Firewall policies for Endpoint Protection in System Center Configuration Manager](create-windows-firewall-policies.md)|  
|John uses the available management tasks for Endpoint Protection to manage antimalware and Windows Firewall policies, perform on-demand scans of computers when necessary, force computers to download the latest definitions, and to specify any further actions to take when malware is detected.|See [How to manage antimalware policies and firewall settings for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-firewall.md)|  
|John uses the following methods to monitor the status of Endpoint Protection and the actions that are taken by Endpoint Protection:<br /><br /> 1) By using the **Endpoint Protection Status** node under **Security** in the **Monitoring** workspace.<br /><br /> 2) By using the **Endpoint Protection** node in the **Assets and Compliance** workspace.<br /><br /> 3) By using the built-in Configuration Manager reports.|See [How to monitor Endpoint Protection in System Center Configuration Manager](monitor-endpoint-protection.md)|  

 John reports a successful implementation of Endpoint Protection to his manager, and confirms that the computers at Woodgrove Bank are now protected from antimalware, according to the business requirements that he was given.
