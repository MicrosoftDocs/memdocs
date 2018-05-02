---
title: Security and privacy for application management
titleSuffix: Configuration Manager
description: Learn about guidance and recommendations for security and privacy when managing applications
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Security and privacy for application management in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


##  Security guidance for application management  

|Security guidance|More information|  
|----------------------------|----------------------|  
|Configure the Application Catalog points to use HTTPS connections and educate users about the dangers of malicious websites.|Configure the Application Catalog website point and the Application Catalog web service point to accept HTTPS connections. With this configuration, the server is authenticated to users, and the transmitted data is protected from tampering and viewing. Help prevent social engineering attacks by educating users to only connect to trusted websites.<br /><br /> When you do not use HTTPS, do not use the branding configuration options, which show the name of your organization in the Application Catalog, as proof of identity.|  
|Use role separation, and install the Application Catalog website point and the Application Catalog service point on separate servers.|If the Application Catalog website point is compromised, install it on a separate server from the Application Catalog web service point. This design helps to protect the Configuration Manager clients and the Configuration Manager infrastructure. This configuration is especially important if the Application Catalog website point accepts client connections from the Internet. It makes the server vulnerable to attack.|  
|Educate users to close the browser window when they finish using the Application Catalog.|If users browse to an external website in the same browser window that they used for the Application Catalog, the browser continues to use the security settings that are suitable for trusted sites in the intranet.|  
|Manually specify the user device affinity instead of letting users identify their primary device. Do not enable usage-based configuration.|Do not consider information that is collected from users or from the device to be authoritative. If you deploy software by using user device affinity that a trusted administrator does not specify, the software might be installed on computers and to users who are not authorized to receive that software.|  
|Always configure deployments to download content from distribution points rather than run from distribution points.|When you configure deployments to download content from a distribution point and run locally, the Configuration Manager client verifies the package hash after it downloads the content. The client discards the package if the hash does not match the hash in the policy. In comparison, if you configure the deployment to run directly from a distribution point, the Configuration Manager client does not verify the package hash. This behavior means that the Configuration Manager client can install software that has been tampered with.<br /><br /> If you must run deployments directly from distribution points, use NTFS least permissions on the packages on the distribution points. Also use Internet protocol security (IPsec) to secure the channel between the client and the distribution points, and between the distribution points and the site server.|  
|<a name="bkmk_interact"></a>Do not let users interact with applications if you enable the **Run with administrative rights** or **Install for system** options.|When you configure an application, you can set the option to **Allow users to view and interact with the program installation**. This setting allows users to respond to any required prompts in the user interface. If you also configure the application to **Run with administrative rights**, or starting in version 1802 **Install for system**, an attacker at the computer that runs the program could use the user interface to escalate privileges on the client computer.<br /><br /> Use programs that use Windows Installer for setup and per-user elevated privileges for software deployments that require administrative credentials. Setup must be run in the context of a user who does not have administrative credentials. Windows Installer per-user elevated privileges provide the most secure way to deploy applications that have this requirement.|  
|Restrict whether users can install software interactively by using the **Installation permissions** client setting.|Configure the **Computer Agent** client device **Install permissions** setting to restrict the types of users who can install software by using the Application Catalog or Software Center. For example, create a custom client setting with **Install permissions** set to **Only administrators**. Then, apply this client setting to a collection of servers to prevent users without administrative permissions from installing software on those computers.|  
|For mobile devices, deploy only applications that are signed.|Deploy mobile device applications only if they are code-signed by a certification authority (CA) that is trusted by the mobile device. For example:<br /><ul><li>An application from a vendor, which is signed by a well-known CA, like VeriSign.</li><li>An internal application that you sign independent from Configuration Manager by using your internal CA.</li><li>An internal application that you sign by using Configuration Manager when you create the application type and use a signing certificate.</li></ul>|  
|If you sign mobile device applications by using the **Create Application Wizard** in Configuration Manager, secure the location of the signing certificate file, and secure the communication channel.|To help protect against elevation of privileges and against man-in-the-middle attacks, store the signing certificate file in a secured folder. Use IPsec between the following computers:<br /><ul><li>The computer that runs the Configuration Manager console</li><li>The computer that stores the certificate signing file</li><li>The computer that stores the application source files</li></ul> Alternatively, sign the application independent of Configuration Manager and before you run the **Create Application Wizard**.|  
|To protect reference computers, implement access controls.|When an administrative user configures the detection method in a deployment type by browsing to a reference computer, make sure that the computer has not been compromised.|  
|Restrict and monitor the administrative users who you grant the following application management role-based security roles:<br /><ul><li>**Application Administrator**</li><li>**Application Author**</li><li> **Application Deployment Manager**</li></ul>|Even when you configure role-based administration, administrative users who create and deploy applications might have more permissions than you realize. For example, administrative users who create or change an application can select dependent applications that are not in their security scope.|  
|When you configure Microsoft Application Virtualization (App-V) virtual environments, select applications that have the same trust level in the virtual environment.|Because applications in an App-V virtual environment can share resources, like the clipboard, configure the virtual environment so that the selected applications have the same trust level.<br /><br /> For more information, see [Create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md).|  
|If you deploy applications for Mac computers, make sure that the source files are from a trustworthy source.|The CMAppUtil tool does not validate the signature of the source package, so make sure that it comes from a source that you trust. The CMAppUtil tool cannot detect whether the files have been tampered with.|  
|If you deploy applications for Mac computers, secure the location of the **.cmmac** file and secure the communication channel when you import this file to Configuration Manager.|The **.cmmac** file that the CMAppUtil tool generates and that you import to Configuration Manager is not signed or validated. To help prevent tampering with this file, store it in a secured folder, and use IPsec or SMB between the following computers:<br /><br /><ul><li>The computer that runs the Configuration Manager console</li><li>The computer that stores the **.cmmac** file</li></ul>|  
|If you configure a web application deployment type, use HTTPS rather than HTTP to secure the connection.|If you deploy a web application by using an HTTP link rather than an HTTPS link, the device could be redirected to a rogue server. Data that's transferred between the device and server could be tampered with.|  



##  Security issues for application management  

-   Low-rights users can copy files from the client cache on the client computer.  

     Users can read the client cache but can't write to it. With read permissions, a user can copy application installation files from one computer to another.  

-   Low-rights users can change files that record software deployment history on the client computer.  

     Because the application history information isn't protected, a user can change files that report whether an application is installed.  

-   App-V packages are not signed.  

     App-V packages in Configuration Manager don't support signing. Digital signatures verify the content is from a trusted source and wasn't altered in transit. There's no mitigation for this security issue. Follow the security best practice to download the content from a trusted source and from a secure location.  

-   Published App-V applications can be installed by all users on the computer.  

     When an App-V application is published on a computer, all users who sign in to that computer can install the application. You can't restrict the users who can install the application after it's published.  

-   You cannot restrict install permissions for the company portal.  

     Although you can configure a client setting to restrict install permissions, for example, to primary users of a device or to local administrators only, this setting doesn't work for the company portal. This issue could result in an elevation of privileges. Users could install an app that they shouldn't be allowed to install.  



##  <a name="BKMK_CertificatesSilverlight5"></a> Certificates for Microsoft Silverlight 5 and elevated trust mode required for the application catalog  
 Configuration Manager clients require Microsoft Silverlight 5, which must run in elevated trust mode for users to install software from the Application Catalog. By default, Silverlight applications run in partial trust mode to prevent applications from accessing user data. If it isn't already installed, Configuration Manager automatically installs Microsoft Silverlight 5 on clients. By default, Configuration Manager sets the Computer Agent **Allow Silverlight applications to run in elevated trust mode** client setting to **Yes**. This setting lets signed and trusted Silverlight applications request elevated trust mode.  

 When you install the Application Catalog website point site system role, the client also installs a Microsoft signing certificate in the Trusted Publishers computer certificate store on each Configuration Manager client computer. Silverlight applications signed by this certificate run in the elevated trust mode, which computers require to install software from the Application Catalog. Configuration Manager automatically manages this signing certificate. To ensure service continuity, don't manually delete or move this Microsoft signing certificate.  

> [!WARNING]  
>  When enabled, the **Allow Silverlight applications to run in elevated trust mode** client setting lets all Silverlight applications, which are signed by certificates in the Trusted Publishers certificate store in either the computer store or the user store, run in elevated trust mode. The client setting can't enable elevated trust mode specifically for the Configuration Manager Application Catalog or for the Trusted Publishers certificate store in the computer store. If malware adds a rogue certificate in the Trusted Publishers store, malware that uses its own Silverlight application can now also run in elevated trust mode.  

 If you set the **Allow Silverlight applications to run in elevated trust mode** setting to **No**, clients don't remove the Microsoft signing certificate.  

 For more about trusted applications in Silverlight, see [Trusted Applications](https://go.microsoft.com/fwlink/p/?LinkId=252842).  

 > [!NOTE]
 > Starting in Configuration Manager 1802, Silverlight is no longer installed automatically. The primary functionality of the Application Catalog is now included in Software Center. Support for the Application Catalog web site ends with the first update released after June 1, 2018.



##  Privacy information for application management  
 Application management lets you run any application, program, or script on any client in the hierarchy. Configuration Manager has no control over the types of applications, programs, or scripts that you run or the type of information that they transmit. During the application deployment process, Configuration Manager might transmit information that identifies the device and sign-in accounts between clients and servers.  

 Configuration Manager maintains status information about the software deployment process. Software deployment status information isn't encrypted during transmission unless the client communicates by using HTTPS. The status information isn't stored in encrypted form in the database.  

 The use of Configuration Manager application installation to remotely, interactively, or silently install software on clients might be subject to software license terms for that software. This use is separate from the Software License Terms for System Center Configuration Manager. Always review and agree to the Software Licensing Terms before you deploy software by using Configuration Manager.  

 Application deployment doesn't happen by default and requires several configuration steps.  

 Two optional features that help efficient software deployment are user device affinity and the Application Catalog:  

-   User device affinity maps a user to devices. A Configuration Manager administrator deploys software to a user. The client automatically installs the software on one or more computers that the user uses most often.  

-   The Application Catalog is a website that lets users request software to install.  

 View the following sections for privacy information about user device affinity and the Application Catalog.  

 Before you configure application management, consider your privacy requirements.  



##  User device affinity  
-  Configuration Manager might transmit information between clients and management point site systems. The information might identify the computer and sign-in account and the summarized usage for sign-in accounts.  
-  The information that is transmitted between the client and server isn't encrypted, unless the management point is configured to require clients to communicate by using HTTPS.  
-  The computer and sign-in account usage information, which is used to map a user to a device, is stored on client computers, sent to management points, and then stored in the Configuration Manager database. The old information is deleted from the database by default after 90 days. The deletion behavior is configurable by setting the **Delete Aged User Device Affinity Data** site maintenance task.
-  Configuration Manager maintains status information about user device affinity. Status information is not encrypted during transmission unless clients are configured to communicate with management points by using HTTPS. Status information is not stored in encrypted form in the database.  
-  Computer, sign-in account usage information, and status information are not sent to Microsoft.  
-  Computer and sign-in usage information that is used to establish user and device affinity is always enabled. In addition, users and administrative users can supply user device affinity information.  



##  Application Catalog  
-  The Application Catalog lets the Configuration Manager admin publish any application or program or script for users to run. Configuration Manager has no control over the types of programs or scripts that are published in the catalog or the type of information that they transmit.    
-  Configuration Manager might transmit information between clients and the Application Catalog site system roles. The information might identify the computer and sign-in accounts. The information that is transmitted between the client and servers isn't encrypted, unless these site system roles are configured to require clients connect by using HTTPS.  
-  The information about the application approval request is stored in the Configuration Manager database. Requests that are canceled or denied and the corresponding request history entries are deleted by default after 30 days. The deletion behavior is configurable by setting the **Delete Aged Application Request Data** site maintenance task. Application approval requests that are in approved and pending states are never deleted.  
-  Information that is sent to and from the Application Catalog is not sent to Microsoft.  
-  The Application Catalog is not installed by default. This installation requires several configuration steps.  
