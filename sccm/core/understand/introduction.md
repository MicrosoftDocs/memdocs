---
title: "Introduction | System Center Configuration Manager"
ms.custom: na
ms.date: 07/22/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
caps.latest.revision: 16
author: Brenduns

---
# Introduction to System Center Configuration Manager
A member of the Microsoft System Center suite of management solutions, System Center Configuration Manager can help you manage devices and users both on-premises and in the cloud.  

**Configuration Manager can help you:**   
-   Increase IT productivity and efficiency by reducing manual tasks and letting you focus on high-value projects  
-   Maximize hardware and software investments  
-   Empower end-user productivity by providing the right software at the right time  

**Configuration Manager helps you deliver more effective IT services by enabling:**  

-   Secure and scalable software deployment  
-   Compliance settings management  
-   Comprehensive asset management of servers, desktops, laptops, and mobile devices.  

**Configuration Manager extends and works alongside your existing Microsoft technologies and solutions.**  

For example, Configuration Manager integrates with:  

-   Microsoft Intune to manage a wide variety of mobile device platforms  
-   Windows Server Update Services (WSUS) to manage software updates  
-   Certificate Services  
-   Exchange Server and Exchange Online  
-   Windows Group Policy
-   DNS   
-   Windows Automated Deployment Kit (Windows ADK) and the User State Migration Tool (USMT),  
-   Windows Deployment Services (WDS)  
-   Remote Desktop and Remote Assistance  

Configuration Manager also uses:  

-   Active Directory Domain Services for security, service location, configuration, and to discover the users and devices that you want to manage.  
-   Microsoft SQL Server as a distributed change management database and integrates with SQL Server Reporting Services (SSRS) to produce reports to monitor and track the management activities.  
-   Site system roles that extend management functionality and  use the web services of Internet Information Services (IIS).  
-   Background Intelligent Transfer Service (BITS) and BranchCache to help manage the available network bandwidth.  

 To be successful with Configuration Manager, you must first thoroughly plan and test the management features before you use Configuration Manager in a production environment. As a powerful management application, Configuration Manager has the potential to affect every computer in your organization. When you deploy and manage Configuration Manager with careful planning and consideration of your business requirements, Configuration Manager can reduce your administrative overhead and total cost of ownership.  

 Use the following topics and additional sections in this topic  to learn more about Configuration Manager:  


**Related topics in this documentation library:**  

-   [Features and capabilities of System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md)  
-   [Choose a device management solution for System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  
-   [What's changed in System Center Configuration Manager from System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)
-   [Fundamentals of System Center Configuration Manager](../../core/understand/fundamentals.md)  
-   [Evaluate System Center Configuration Manager by building your own lab environment](../../core/get-started/evaluate-with-lab-environment.md)  
-   [Find help for using System Center Configuration Manager](../../core/understand/find-help.md)  
-   [Removed and deprecated features for System Center Configuration Manager](../../core/plan-design/changes/removed-and-deprecated-features.md)  

##  <a name="BKMK_Console"></a> The Configuration Manager console  
 After you install Configuration Manager, use the Configuration Manager console to configure sites and clients, and to run and monitor management tasks. This console is the main point of administration and lets you manage multiple sites.  

 You can use the console to run secondary consoles that provide support for specific client management tasks, like:  

-   **Resource Explorer**, to view hardware and software inventory information.  
-   **Remote control**, to remotely connect to a client computer to perform troubleshooting tasks.  

 You can install the Configuration Manager console on additional computers, and restrict access and limit what administrative users can see in the console by using   
                Configuration Manager role-based administration.  

 For more information, see [Install System Center Configuration Manager consoles](../../core/servers/deploy/install/install-consoles.md)

##  <a name="BKMK_ApplicationCatalog"></a> The Application Catalog, Software Center, and the Company Portal  
 The **Application Catalog** is a website where users can browse for and request software for their Windows-based PCs. To use the Application Catalog, you must install the Application Catalog web service point and the Application Catalog website point for the site.  

 **Software Center** is an application that is installed when the Configuration Manager client is installed on Windows-based computers. Users run this application to request software and manage the software that is deployed to them by using Configuration Manager. Software Center lets users do the following:  

-   Browse for and install software from the Application Catalog  
-   View their software request history.  
-   Configure when Configuration Manager can install software on their devices  
-   Configure access settings for remote control, if an administrative user enabled remote control  

 **The company portal** is an app or website that provides similar functions to the Application Catalog, but for mobile devices that are enrolled by Microsoft Intune  

 For more information, see the [Get started with application management in System Center Configuration Manager](../../apps/understand/get-started-with-application-management.md) topic.  

###  <a name="BKMK_Client"></a> Configuration Manager Properties (on Windows PCs)  
 When the Configuration Manager client is installed on Windows computers, Configuration Manager is installed in Control Panel. Typically, you do not have to configure this application because the client configuration is performed in the Configuration Manager console. This application helps administrative users and the help desk troubleshoot problems with individual clients.  

 For more information about client deployment, see [Client installation methods in System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md).  

##  <a name="BKMK_ExampleScenarios"></a> Example scenarios for Configuration Manager  
 The following example scenarios demonstrate how a company named Trey Research uses System Center Configuration Manager to empower users to:  

-   Be more productive  
-   Unify their compliance management for devices for a more streamlined administration experience  
-   Simplify device management to reduce IT operating costs  

 In all scenarios, Adam is the main administrator for Configuration Manager.  

###  <a name="BKMK_ScenarioEmpower"></a> Example Scenario: Empower users by ensuring access to applications from any device  
 Trey Research wants to ensure that employees have access to the applications that they require and as efficiently as possible. Adam maps these company requirements to the following scenarios:  

|Requirement|Current client management state|Future client management state|  
|-----------------|-------------------------------------|------------------------------------|  
|New employees can work efficiently from day one.|When employees join the company, they have to wait for applications to be installed after they first log on.|When employees join the company, they log on and their applications are installed and are ready to be used.|  
|Employees can quickly and easily request additional software that they need.|When employees require additional applications, they file a ticket with the help desk, and then typically wait two days for the ticket to be processed and the applications are installed.|When employees require additional applications, they can request them from a website and they are installed immediately if there are no licensing restrictions. If there are licensing restrictions, users must first ask for approval before they can install the application.<br /><br /> The website shows users only the applications that they are allowed to install.|  
|Employees can use their mobile devices at work if the devices comply with security policies that are monitored and enforced.<br /><br /> These policies include enforcing a strong password, locking a device after period of inactivity, and remote wipe of lost or stolen devices.|Employees connect their mobile devices to Exchange Server for email service  but there is limited reporting to confirm that they are in compliance with the security policies in the default Exchange ActiveSync mailbox policies. The personal use of mobile devices is at risk of being prohibited unless IT can confirm adherence to policy.|The IT organization can report mobile device security compliance with the required settings. This confirmation lets users continue to use their mobile device at work. Users can remotely wipe their mobile device if it is lost or stolen, and the help desk can wipe any user's mobile device that is reported as lost or stolen.<br /><br /> Provide mobile device enrollment in a PKI environment for additional security and control.|  
|Employees can be productive even if they are not at their desk.|When employees are not at their desk and do not have portable computers, they cannot access their applications by using the kiosk computers that are available throughout the company.|Employees can use kiosk computers to access their applications and data.|  
|Usually, business continuity takes precedence over installing required applications and software updates.|Applications and software updates that are required install during the day and frequently disrupt users from working because their computers slow down or restart during the installation.|Users can configure their working hours to prevent required software from installing while they are using their computer.|  

 To meet the requirements, Adam uses these Configuration Manager management capabilities and configuration options:  

-   Application management  
-   Mobile device management  

 He implements these by using the configuration steps in the following table.  

|Configuration steps|Outcome|  
|-------------------------|-------------|  
|Adam makes sure that the new users have user accounts in Active Directory and creates a new query-based collection in Configuration Manager for these users. He then defines user device affinity for these users by creating a file that maps the user accounts to the primary computers that they will use and imports this file into Configuration Manager.<br /><br /> The applications that the new users must have are already created in Configuration Manager. He then deploys these applications that have the purpose of Required to the collection that contains the new users.|Because of the user device affinity information, the applications are installed to each user's primary computer or computers before the user log on.<br /><br /> The applications are ready to use as soon as the user successfully logs on.|  
|Adam installs and configures the Application Catalog site system roles so that users can browse for applications to install. He creates application deployments that have the purpose of Available, and then deploys these applications to the collection that contains the new users.<br /><br /> For the applications that have a restricted number of licenses, Adam configures these applications to require approval.|By configuring applications as available to these users and by using the Application Catalog, users can now browse the applications that they are allowed to install. Users can then either install the applications immediately or request approval and return to the Application Catalog to install them after the help desk has approved their request.|  
|Adam creates an Exchange Server connector in Configuration Manager to manage the mobile devices that connect to the company's on-premises Exchange Server. He configures this connector with security settings that include the requirement for a strong password and lock the mobile device after a period of inactivity.<br /><br /> For additional management for devices that run Windows Phone 8, Windows RT, and iOS, Adam obtains a Microsoft Intune subscription and then installs the Service connection point site system role. This mobile device management solution gives the company greater management support for these devices. This includes making applications available for users to install on these devices, and extensive settings management. In addition, mobile device connections are secured by using PKI certificates that are automatically created and deployed by Intune. After configuring the service connection point and subscription for use with Configuration Manager Adam sends an email message to the users who own these mobile devices for them to click a link to start the enrollment process.<br /><br /> For the mobile devices to be enrolled by Microsoft Intune, Adam uses compliance settings to configure security settings for these mobile devices. These settings include the requirement to configure a strong password and lock the mobile device after a period of inactivity.|With these two mobile device management solutions, the IT organization can now provide reporting information about the mobile devices that are being used on the company network and their compliance with the configured security settings.<br /><br /> Users are shown how to remotely wipe their mobile device by using the Application Catalog or the company portal if their mobile device is lost or stolen. The help desk is also instructed how to remotely wipe a mobile device for users by using the Configuration Manager console.<br /><br /> In addition, for the mobile devices that are enrolled by Microsoft Intune, Adam can now deploy mobile applications for users to install, collect more inventory data from these devices, and have better management control over these devices by being able to access more settings.|  
|Trey Research has several kiosk computers that are used by employees who visit the office. The employees want their applications to be available to them wherever they log on. However, Adam does not want to locally install all the applications on each computer.<br /><br /> To achieve this, Adam creates the required applications that have two deployment types:<br /><br /> **The first:** A full, local installation of the application that has a requirement that it can only be installed on a user's primary device.<br /><br /> **The second:** A virtual version of the application that has the requirement that it must not be installed on the user's primary device.|When visiting employees log on to a kiosk computer, they see the applications that they require displayed as icons on the kiosk computer's desktop. When they run the application, it is streamed as a virtual application. This way, they can be as productive as if they are sitting at their desktop.|  
|Adam lets users know that they can configure their business hours in Software Center and select options to prevent software deployment activities during this time period and when the computer is in presentation mode.|Because users can control when Configuration Manager deploys software to their computers, users remain more productive during their work day.|  

 These configuration steps and outcomes let Trey Research successfully empower their employees by ensuring access to applications from any device.  

###  <a name="BKMK_ScenarioUnify"></a> Example scenario: Unify compliance management for devices  
 Trey Research wants a unified client management solution that ensures that their computers run antivirus software that is automatically kept up-to-date. That is:  

-   Windows Firewall is enabled  
-   Critical software updates are installed  
-   Specific registry keys are set  
-   Managed mobile devices cannot install or run unsigned applications  

 The company also wants to extend this protection to the Internet for laptops that move from the intranet to the Internet.  

 Adam maps these company requirements to the following scenarios:  

|Requirement|Current client management state|Future client management state|  
|-----------------|-------------------------------------|------------------------------------|  
|All computers run antimalware software that has up-to-date definition files and enables Windows Firewall.|Different computers run different antimalware solutions that are not always kept up-to-date and although Windows Firewall is enabled by default, users sometimes disable it.<br /><br /> Users are asked to contact the help desk if malware is detected on their computer.|All computers run the same antimalware solution that automatically downloads the latest definition update files and automatically re-enables Windows Firewall if users disable it.<br /><br /> The help desk is automatically notified by email if malware is detected.|  
|All computers install critical software updates within the first month of release.|Although software updates are installed on computers, many computers do not automatically install critical software updates until two or three months after they are released. This leaves them vulnerable to attack during this time period.<br /><br /> For the computers that do not install the critical software updates, the help desk first sends out email messages asking users to install the updates. For computers that remain noncompliant, engineers remotely connect to these computers and manually install the missing software updates.|Improve the current compliance rate within the specified month to over 95% without sending email messages or asking the help desk to manually install them.|  
|Security settings for specific applications are regularly checked and remediated if it is necessary.|Computers run complex startup scripts that rely on computer group membership to reset registry values for specific applications.<br /><br /> Because these scripts only run at startup and some computers are left on for days, the help desk cannot check for configuration drift on a timely basis.|Registry values are checked and automatically remediated without relying on computer group membership or restarting the computer.|  
|Mobile devices cannot install or run unsafe applications.|Users are asked not to download and run potentially unsafe applications from the Internet but there are no controls in place to monitor or enforce this.|Mobile devices that are managed with Microsoft Intune or Configuration Manager automatically prevent unsigned applications from installing or running.|  
|Laptops that move from the intranet to the Internet must be kept secure.|For users who travel, they frequently cannot connect over the VPN daily and these laptops become out of compliance with security requirements.|An Internet connection is all that is required for laptops to be kept in compliance with security requirements. Users do not have to log on or use the VPN.|  

 To meet the requirements, Adam uses these Configuration Manager management capabilities and configuration options:  

-   Endpoint Protection  
-   Software updates  
-   Compliance settings  
-   Mobile device management  
-   Internet-based client management  

 He implements these by using the configuration steps in the following table.  

|Configuration steps|Outcome|  
|-------------------------|-------------|  
|Adam configures Endpoint Protection and enables the client setting to uninstall other antimalware solutions and enables Windows Firewall. He configures automatic deployment rules so that computers check for and install the latest definition updates regularly.|The single antimalware solution helps protect all computers by using minimal administrative overhead. Because the help desk is automatically notified by email message if antimalware is detected, problems can be resolved quickly. This helps prevent attacks on other computers.|  
|To help increase compliance rates, Adam uses automatic deployment rules, defines maintenance windows for servers, and investigates the advantages and disadvantages of using Wake on LAN for computers that hibernate.|Compliance for critical software updates increases and reduces the requirement for users or the help desk to install software updates manually.|  
|Adam uses compliance settings to check for the presence of the specified applications. When the applications are detected, configuration items then check the registry values and automatically remediate them if they are out of compliance.|By using configuration items and configuration baselines that are deployed to all computers and that check for compliance every day, separate scripts that rely on computer membership and computer restarts are no longer required.|  
|Adam uses compliance settings for enrolled mobile devices and configures the Exchange Server connector so that unsigned applications are prohibited from installing and running on mobile devices.|By prohibiting unsigned applications, mobile devices are automatically protected from potentially harmful applications.|  
|Adam makes sure that site system servers and computers have the PKI certificates that Configuration Manager requires for HTTPS connections, and then he installs additional site system roles in the perimeter network that accept client connections from the Internet.|Computers that move from the intranet to the Internet automatically continue to be managed by Configuration Manager when they have an Internet connection. Those computers do not rely on users logging on to their computer or connecting to the VPN.<br /><br /> These computers continue to be managed for antimalware and Windows Firewall, software updates, and configuration items. As a result, compliance levels automatically increase.|  

 These configuration steps and outcomes result in Trey Research successfully unifying their compliance management for devices.  

###  <a name="BKMK_ScenarioSimplify"></a> Example scenario: Simplify client management for devices  
 Trey Research wants all new computers to automatically install their company's base computer image that runs Windows 7. After the operating image is installed on these computers, they must be managed and monitored for additional software that users install. Computers that store highly confidential information require more restrictive management policies than the other computers. For example, help desk engineers must not connect to them remotely, BitLocker PIN entry must be used for restarts, and only local administrators can install software.  

 Adam maps these company requirements to the following scenarios:  

|Requirement|Current client management state|Future client management state|  
|-----------------|-------------------------------------|------------------------------------|  
|New computers are installed with Windows 7.|The help desk installs and configures Windows 7 for users and then sends the computer to the respective location.|New computers go straight to the final destination, are plugged into the network, and they automatically install and configure Windows 7.|  
|Computers must be managed and monitored. This includes hardware and software inventory to help determine licensing requirements.|The Configuration Manager client is deployed by using automatic client push and the help desk investigates installation failures and clients that do not send inventory data when expected.<br /><br /> Failures are frequent because of installation dependencies that are not met and WMI corruption on the client.|Client installation and inventory data that is collected from computers is more reliable and requires less intervention from the help desk. Reports show software usage for license information.|  
|Some computers must have more rigorous management policies.|Because of the more rigorous management policies, these computers are currently not managed by Configuration Manager.|Manage these computers by using Configuration Manager without additional administrative overhead to accommodate the exceptions.|  

 To meet the requirements, Adam uses these Configuration Manager management capabilities and configuration options:  

-   Operating system deployment  
-   Client deployment and client status  
-   Compliance settings  
-   Client settings  
-   Inventory and Asset Intelligence  
-   Role-based administration  

 He implements these by using the configuration steps in the following table.  

|Configuration steps|Outcome|  
|-------------------------|-------------|  
|Adam captures an operating system image from a computer that has Windows 7 installed and that is configured to the company specifications. He then deploys the operating system to the new computers by using unknown computer support and PXE. He also installs the Configuration Manager client as part of the operating system deployment.|New computers are up and running more quickly without intervention from the help desk.|  
|Adam configures automatic site-wide client push installation to install the Configuration Manager client on any computers that are discovered. This ensures that any computers that were not imaged with the client still install the client so that the computer is managed by Configuration Manager.<br /><br /> Adam configures client status to automatically remediate any client issues that are discovered. Adam also configures client settings that enable the collection of inventory data that is required, and configures Asset Intelligence.|Installing the client together with the operating system is quicker and more reliable than waiting for Configuration Manager to discover the computer and then try to install the client source files on the computer. However, leaving the automatic client push option enabled provides a backup means for a computer that already has the operating system installed to install the client when the computer connects to the network.<br /><br /> Client settings ensure that clients send their inventory information to the site regularly. This, in addition to the client status tests, help to keep the client running with minimal intervention from the help desk. For example, WMI corruptions are detected and automatically remediated.<br /><br /> The Asset Intelligence reports help monitor software usage and licenses.|  
|Adam creates a collection for the computers that must have more rigorous policy settings and then creates a custom client device setting for this collection that includes disabling remote control, enables BitLocker PIN entry, and lets only local administrators to install software.<br /><br /> Adam configures role-based administration so that help desk engineers do not see this collection of computers to help ensure that they are not accidentally managed as a standard computer.|These computers are now managed by Configuration Manager but with specific settings that do not require a new site.<br /><br /> The collection for these computers is not visible to the help desk engineers to help reduce the possibility that they are accidentally sent deployments and scripts for standard computers.|  

 These configuration steps and outcomes result in Trey Research successfully simplifying client management for devices.  

##  <a name="BKMK_NextSteps"></a> Next steps  
 Before you install Configuration Manager, you can become familiar with some basic concepts and terms that are specific to Configuration Manager.  

-   If you are familiar with System Center 2012 Configuration Manager, see [What's changed in System Center Configuration Manager from System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) to understand the new capabilities.  
-   For a high-level technical overview of System Center Configuration Manager, see [Fundamentals of System Center Configuration Manager](../../core/understand/fundamentals.md).  

 When you are familiar with the basic concepts, use the System Center Configuration Manager documentation to help you successfully deploy and use Configuration Manager.  
