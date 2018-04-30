---
title: "Remote control security privacy"
titleSuffix: "Configuration Manager"
description: "Get security and privacy information for remote control in System Center Configuration Manager."
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Security and privacy for remote control in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This topic contains security and privacy information for remote control in System Center 2012 Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Security best practices for remote control  
 Use the following security best practices when you manage client computers by using remote control.  

|Security best practice|More information|  
|----------------------------|----------------------|  
|When you connect to a remote computer, do not continue if NTLM instead of Kerberos authentication is used.|When Configuration Manager detects that the remote control session is authenticated by using NTLM instead of Kerberos, you see a prompt that warns you that the identity of the remote computer cannot be verified. Do not continue with the remote control session. NTLM authentication is a weaker authentication protocol than Kerberos and is vulnerable to replay and impersonation.|  
|Do not enable Clipboard sharing in the remote control viewer.|The Clipboard supports objects such as executable files and text and could be used by the user on the host computer during the remote control session to run a program on the originating computer.|  
|Do not enter passwords for privileged accounts when remotely administering a computer.|Software that observes keyboard input could capture the password. Or, if the program that is being run on the client computer is not the program that the remote control user assumes, the program might be capturing the password. When accounts and passwords are required, the end user should enter them.|  
|Lock the keyboard and mouse during a remote control session.|If Configuration Manager detects that the remote control connection is terminated, Configuration Manager automatically locks the keyboard and mouse so that a user cannot take control of the open remote control session. However, this detection might not occur immediately and does not occur if the remote control service is terminated.<br /><br /> Select the action **Lock Remote Keyboard and Mouse** in the **ConfigMgr Remote Control** window.|  
|Do not let users configure remote control settings in Software Center.|Do not enable the client setting **Users can change policy or notification settings in Software Center** to help prevent users from being spied on.<br /><br /> This setting is for the computer, not for the logged-on user.|  
|Enable the **Domain** Windows Firewall profile.|Enable the client setting **Enable remote control on clients Firewall exception profiles** and then select the **Domain** Windows Firewall for intranet computers.|  
|If you log off during a remote control session and log on as a different user, ensure that you log off before you disconnect the remote control session.|If you do not log off in this scenario, the session remains open.|  
|Do not give users local administrator rights.|When you give users local administrator rights, they might be able to take over your remote control session or compromise your credentials.|  
|Use either Group Policy or Configuration Manager to configure Remote Assistance settings, but not both.|You can use Configuration Manager and Group Policy to make configuration changes to the Remote Assistance settings. When Group Policy is refreshed on the client, by default, it optimizes the process by changing only the policies that have changed on the server. Configuration Manager changes the settings in the local security policy, which might not be overwritten unless the Group Policy update is forced.<br /><br /> Setting policy in both places might lead to inconsistent results. Choose one of these methods to configure your Remote Assistance settings.|  
|Enable the client setting **Prompt user for Remote Control permission**.|Although there are ways around this client setting that prompts a user to confirm a remote control session, enable this setting to reduce the chance of users being spied upon while working on confidential tasks.<br /><br /> In addition, educate users to verify the account name that is displayed during the remote control session and disconnect the session if they suspect that the account is unauthorized.|  
|Limit the Permitted Viewers list.|Local administrator rights are not required for a user to be able to use remote control.|  

### Security issues for remote control  
 Managing client computers by using remote control has the following security issues:  

-   Do not consider remote control audit messages to be reliable.  

     If you start a remote control session and then log on by using alternative credentials, the original account sends the audit messages, not the account that used the alternative credentials.  

     Audit messages are not sent if you copy the binary files for remote control rather than install the Configuration Manager console, and then run remote control at the command prompt.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Privacy information for remote control  
 Remote control lets you view active sessions on Configuration Manager client computers and potentially view any information stored on those computers. By default, remote control is not enabled.  

 Although you can configure remote control to provide prominent notice and get consent from a user before a remote control session begins, it can also monitor users without their permission or awareness. You can configure View Only access level so that nothing can be changed on the remote control, or Full Control. The account of the connecting administrator is displayed in the remote control session, to help users identify who is connecting to their computer.  

 By default, Configuration Manager grants the local Administrators group Remote Control permissions.  

 Before you configure remote control, consider your privacy requirements.  
