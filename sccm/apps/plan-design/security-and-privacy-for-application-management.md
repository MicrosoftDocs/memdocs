---
title: "Security and privacy for application management"
description: "Security and privacy best practices for application management in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
caps.latest.revision: 8
author: mattbriggsms.author: mabriggmanager: angrobe

---
# Security and privacy for application management in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*

##  Security best practices for application management  

|Security best practice|More information|  
|----------------------------|----------------------|  
|Configure the Application Catalog points to use HTTPS connections and educate users about the dangers of malicious websites.|Configure the Application Catalog website point and the Application Catalog web service point to accept HTTPS connections so that the server is authenticated to users and the data that is transmitted is protected from tampering and viewing. Help to prevent social engineering attacks by educating users to connect to trusted websites only.<br /><br /> Do not use the branding configuration options that show the name of your organization in the Application Catalog as proof of identity when you do not use HTTPS.|  
|Use role separation, and install the Application Catalog website point and the Application Catalog service point on separate servers.|If the Application Catalog website point is compromised, install it on a separate server from the Application Catalog web service point. This will help to protect the Configuration Manager clients and the Configuration Manager infrastructure. This is particularly important if the Application Catalog website point accepts client connections from the Internet because this configuration makes the server vulnerable to attack.|  
|Educate users to close the browser window when they finish using the Application Catalog.|If users browse to an external website in the same browser window that they used for the Application Catalog, the browser continues to use the security settings that are suitable for trusted sites in the intranet.|  
|Manually specify the user device affinity instead of letting users identify their primary device. Do not enable usage-based configuration.|Do not consider information that is collected from users or from the device to be authoritative. If you deploy software by using user device affinity that is not specified by a trusted administrative user, the software might be installed on computers and to users who are not authorized to receive that software.|  
|Always configure deployments to download content from distribution points rather than run from distribution points.|When you configure deployments to download content from a distribution point and run locally, the Configuration Manager client verifies the package hash after it downloads the content. The client discards the package if the hash does not match the hash in the policy. In comparison, if you configure the deployment to run directly from a distribution point, the Configuration Manager client does not verify the package hash, which means that the Configuration Manager client can install software that has been tampered with.<br /><br /> If you must run deployments directly from distribution points, use NTFS least permissions on the packages on the distribution points, and use Internet protocol security (IPsec) to secure the channel between the client and the distribution points and between the distribution points and the site server.|  
|Do not let users interact with programs if the **Run with administrative rights** option is required.|When you configure a program, you can set the **Allow users to interact with this program** option so that users can respond to any required prompts in the user interface. If the program is also configured to **Run with administrative rights**, an attacker at the computer that runs the program could use the user interface to escalate privileges on the client computer.<br /><br /> Use programs that use Windows Installer for setup and per-user elevated privileges for software deployments that require administrative credentials. Setup must be run in the context of a user who does not have administrative credentials. Windows Installer per-user elevated privileges provide the most secure way to deploy applications that have this requirement.|  
|Restrict whether users can install software interactively by using the **Installation permissions** client setting.|Configure the **Computer Agent** client device **Install permissions** setting to restrict the types of users who can install software by using the Application Catalog or Software Center. For example, create a custom client setting with **Install permissions** set to **Only administrators**. Then, apply this client setting to a collection of servers to prevent users without administrative permissions from installing software on those computers.|  
|For mobile devices, deploy only applications that are signed.|Deploy mobile device applications only if they are code-signed by a certification authority (CA) that is trusted by the mobile device. For example:<br /><br /><ul><li>An application from a vendor, which is signed by a well-known CA, like VeriSign.</li><li>An internal application that you sign independent from Configuration Manager by using your internal CA.</li><li>An internal application that you sign by using Configuration Manager when you create the application type and use a signing certificate.</li></ul>|  
|If you sign mobile device applications by using the **Create Application Wizard** in Configuration Manager, secure the location of the signing certificate file, and secure the communication channel.|To help protect against elevation of privileges and against man-in-the-middle attacks, store the signing certificate file in a secured folder and use IPsec or Server Message Block (SMB) between the following computers:<br /><br /><ul><li>The computer that runs the Configuration Manager console</li><li>The computer that stores the certificate signing file</li><li>The computer that stores the application source files</li></ul> Alternatively, sign the application independent of Configuration Manager and before you run the **Create Application Wizard**.|  
|Implement access controls to protect reference computers.|When an administrative user configures the detection method in a deployment type by browsing to a reference computer, make sure that the computer has not been compromised.|  
|Restrict and monitor the administrative users who are granted the role-based security roles that are related to application management:<br /><br /><ul><li>**Application Administrator**</li><li>**Application Author**</li><li> **Application Deployment Manager**</li></ul>|Even when you configure role-based administration, administrative users who create and deploy applications might have more permissions than you realize. For example, administrative users who create or change an application can select dependent applications that are not in their security scope.|  
|When you configure Microsoft Application Virtualization (App-V) virtual environments, select applications that have the same trust level in the virtual environment.|Because applications in an App-V virtual environment can share resources, like the clipboard, configure the virtual environment so that the selected applications have the same trust level.<br /><br /> For more information, see [Create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md).|  
|If you deploy applications for Mac computers, make sure that the source files are from a trustworthy source.|The CMAppUtil tool does not validate the signature of the source package, so make sure that it comes from a source that you trust. The CMAppUtil tool cannot detect whether the files have been tampered with.|  
|If you deploy applications for Mac computers, secure the location of the **.cmmac** file and secure the communication channel when you import this file to Configuration Manager.|The **.cmmac** file that the CMAppUtil tool generates and that you import to Configuration Manager is not signed or validated. To help prevent tampering with this file, store it in a secured folder, and use IPsec or SMB between the following computers:<br /><br /><ul><li>The computer that runs the Configuration Manager console</li><li>The computer that stores the **.cmmac** file</li></ul>.|  
|If you configure a web application deployment type, use HTTPS rather than HTTP to secure the connection.|If you deploy a web application by using an HTTP link rather than an HTTPS link, the device could be redirected to a rogue server and data that's transferred between the device and server could be tampered with.|  

##  Security issues for application management  

-   Low-rights users can copy files from the client cache on the client computer.  

     Users can read the client cache but cannot write to it. With read permissions, a user can copy application installation files from one computer to another.  

-   Low-rights users can change files that record software deployment history on the client computer.  

     Because the application history information is not protected, a user can change files that report whether an application is installed.  

-   App-V packages are not signed.  

     App-V packages in Configuration Manager do not support signing to verify that the content is from a trusted source and that it has not been altered in transit. There is no mitigation for this security issue. Make sure that you follow the security best practice to download the content from a trusted source and from a secure location.  

-   Published App-V applications can be installed by all users on the computer.  

     When an App-V application is published on a computer, all users who sign in to that computer can install the application. This means that you cannot restrict the users who can install the application after it is published.  

-   You cannot restrict install permissions for the company portal.  

     Although you can configure a client setting to restrict install permissions, for example, to primary users of a device or to local administrators only, this setting does not work for the company portal. This could result in an elevation of privileges because users could install an app that they should not be allowed to install.  

##  <a name="BKMK_CertificatesSilverlight5"></a> Certificates for Microsoft Silverlight 5 and elevated trust mode required for the application catalog  
 Configuration Manager clients require Microsoft Silverlight 5, which must run in elevated trust mode for users to install software from the Application Catalog. By default, Silverlight applications run in partial trust mode to prevent applications from accessing user data. Configuration Manager automatically installs Microsoft Silverlight 5 on clients if it is not already installed. By default, Configuration Manager sets the Computer Agent **Allow Silverlight applications to run in elevated trust mode** client setting to **Yes**. This setting lets signed and trusted Silverlight applications request elevated trust mode.  

 When you install the Application Catalog website point site system role, the client also installs a Microsoft signing certificate in the Trusted Publishers computer certificate store on each Configuration Manager client computer. This certificate lets Silverlight applications that are signed by this certificate run in the elevated trust mode that computers require to install software from the Application Catalog. Configuration Manager automatically manages this signing certificate. To ensure service continuity, do not manually delete or move this Microsoft signing certificate.  

> [!WARNING]  
>  When enabled, the **Allow Silverlight applications to run in elevated trust mode** client setting lets all Silverlight applications that are signed by certificates in the Trusted Publishers certificate store in either the computer store or the user store run in elevated trust mode. The client setting cannot enable elevated trust mode specifically for the Configuration Manager Application Catalog or for the Trusted Publishers certificate store in the computer store. If malware adds a rogue certificate in the Trusted Publishers store, for example, in the user store, malware that uses its own Silverlight application can now also run in elevated trust mode.  

 If you set the **Allow Silverlight applications to run in elevated trust mode** client setting to **No**, this does not remove the Microsoft signing certificate from clients.  

 For more about trusted applications in Silverlight, see [Trusted Applications](http://go.microsoft.com/fwlink/p/?LinkId=252842).  

##  Privacy information for application management  
 Application management lets you to run any application, program, or script on any client computer or client mobile device in the hierarchy. Configuration Manager has no control over the types of applications, programs, or scripts that you run or the type of information that they transmit. During the application deployment process, Configuration Manager might transmit information that identifies the device and sign-in accounts between clients and servers.  

 Configuration Manager maintains status information about the software deployment process. Software deployment status information is not encrypted during transmission unless the client communicates by using HTTPS. The status information is not stored in encrypted form in the database.  

 The use of Configuration Manager application installation to remotely, interactively, or silently install software on clients might be subject to software license terms for that software. This use is separate from the Software License Terms for System Center Configuration Manager. Always review and agree to the Software Licensing Terms before you deploy software by using Configuration Manager.  

 Application deployment does not happen by default and requires several configuration steps.  

 Two optional features that help efficient software deployment are user device affinity and the Application Catalog:  

-   User device affinity maps a user to devices so that a Configuration Manager admin can deploy software to a user, and the software is automatically installed on one or more computers that the user uses most often.  

-   The Application Catalog is a website that lets users request software to install.  

 View the following sections for privacy information about user device affinity and the Application Catalog.  

 Before you configure application management, consider your privacy requirements.  

##  User device affinity  
-  Configuration Manager might transmit information between clients and management point site systems. The information might identify the computer and sign-in account and the summarized usage for sign-in accounts.  
-  The information that is transmitted between the client and server is not encrypted unless the management point is configured to require clients to communicate by using HTTPS.  
-  The computer and sign-in account usage information that is used to map a user to a device is stored on client computers, sent to management points, and then stored in the Configuration Manager database. The old information is deleted from the database by default after 90 days. The deletion behavior is configurable by setting the **Delete Aged User Device Affinity Data** site maintenance task.
-  Configuration Manager maintains status information about user device affinity. Status information is not encrypted during transmission unless clients are configured to communicate with management points by using HTTPS. Status information is not stored in encrypted form in the database.  
-  Computer, sign-in account usage information, and status information are not sent to Microsoft.  
-  Computer and sign-in usage information that is used to establish user and device affinity is always enabled. In addition, users and administrative users can supply user device affinity information.  

##  Application Catalog  
-  The Application Catalog lets the Configuration Manager admin publish any application or program or script for users to run. Configuration Manager has no control over the types of programs or scripts that are published in the catalog or the type of information that they transmit.    
-  Configuration Manager might transmit information between clients and the Application Catalog site system roles. The information might identify the computer and sign-in accounts. The information that is transmitted between the client and servers is not encrypted unless these site system roles are configured to require that clients connect by using HTTPS.  
-  The information about the application approval request is stored in the Configuration Manager database. Requests that are canceled or denied and the corresponding request history entries are deleted by default after 30 days. The deletion behavior is configurable by setting the **Delete Aged Application Request Data** site maintenance task. Application approval requests that are in approved and pending states are never deleted.  
-  Information that is sent to and from the Application Catalog is not sent to Microsoft.  
-  The Application Catalog is not installed by default. This installation requires several configuration steps.  
