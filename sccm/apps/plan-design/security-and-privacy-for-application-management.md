---
title: "Security and privacy for application management | System Center Configuration Manager"
description: "Security and privacy best practices for application management in System Center Configuration Manager."
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
caps.latest.revision: 8
author: robstackmsft

---
# Security and privacy for application management in System Center Configuration Manager

##  Security best practices for application management  

|Security best practice|More information|  
|----------------------------|----------------------|  
|Configure the Application Catalog points to use HTTPS connections and educate users about the dangers of malicious websites.|Configure the Application Catalog website point and the Application Catalog web service point to accept HTTPS connections so that the server is authenticated to users and the data that is transmitted is protected from tampering and viewing. Help to prevent social engineering attacks by educating users to connect to trusted websites only.<br /><br /> Do not use the branding configuration options that display the name of your organization in the Application Catalog as proof of identify when you do not use HTTPS.|  
|Use role separation, and install the Application Catalog website point and the Application Catalog service point on separate servers.|If the Application Catalog website point is compromised, install it on a separate server to the Application Catalog web service point. This will help to protect the Configuration Manager clients and the Configuration Manager infrastructure. This is particularly important if the Application Catalog website point accepts client connections from the Internet because this configuration makes the server vulnerable to attack.|  
|Educate users to close the browser window when they finish using the Application Catalog.|If users browse to an external website in the same browser window that they used for the Application Catalog, the browser continues to use the security settings that are suitable for trusted sites in the intranet.|  
|Manually specify the user device affinity instead of allowing users to identify their primary device; and do not enable usage-based configuration.|Do not consider the information that is collected from users or from the device to be authoritative. If you deploy software by using user device affinity that is not specified by a trusted administrative user, the software might be installed on computers and to users who are not authorized to receive that software.|  
|Always configure deployments to download content from distribution points rather than run from distribution points.|When you configure deployments to download content from a distribution point and run locally, the Configuration Manager client verifies the package hash after it downloads the content, and it discards the package if the hash does not match the hash in the policy. In comparison, if you configure the deployment to run directly from a distribution point, the Configuration Manager client does not verify the package hash, which means that the Configuration Manager client can install software that has been tampered with.<br /><br /> If you must run deployments directly from distribution points, use NTFS least permissions on the packages on the distribution points, and use IPsec to secure the channel between the client and the distribution points and between the distribution points and the site server.|  
|Do not allow users to interact with programs if the option **Run with administrative rights** is required.|When you configure a program, you can set the option **Allow users to interact with this program** so that users can respond to any required prompts in the user interface. If the program is also configured to **Run with administrative rights**, an attacker at the computer that runs the program could use the user interface to escalate privileges on the client computer.<br /><br /> Use Windows Installer-based setup programs with per-user elevated privileges for software deployments that require administrative credentials, but that must be run in the context of a user who does not have administrative credentials. Windows Installer per-user elevated privileges provides the most secure way to deploy applications that have this requirement.|  
|Restrict whether users can install software interactively by using the **Installation permissions** client setting.|Configure the **Computer Agent** client device setting **Install permissions** to restrict the types of users that can install software by using the Application Catalog or Software Center. For example, create a custom client setting with **Install permissions** set to **Only administrators**. Then apply this client setting to a collection of servers to prevent users without administrative permissions from installing software on those computers.|  
|For mobile devices, deploy only applications that are signed|Deploy mobile device applications only if they are code signed by a certification authority (CA) that is trusted by the mobile device. For example:<br /><br /> - An application from a vendor, which is signed by a well-known CA, such as VeriSign.<br /><br /> - An internal application that you sign independently from Configuration Manager, by using your internal CA.<br /><br /> - An internal application that you sign by using Configuration Manager when you create the application type and use a signing certificate.|  
|If you sign mobile device applications by using the **Create Application Wizard** in Configuration Manager, secure the location of the signing certificate file, and secure the communication channel.|To help protect against elevation of privileges and against man-in-the-middle attacks, store the signing certificate file in a secured folder and use IPsec or SMB between the following computers:<br /><br /> - The computer that runs the Configuration Manager console.<br /><br /> - The computer that stores the certificate signing file.<br /><br /> - The computer that stores the application source files.<br /><br /> Alternatively, sign the application independently from Configuration Manager and before you run the **Create Application Wizard**.|  
|Implement access controls to protect reference computers.|When an administrative user configures the detection method in a deployment type by browsing to a reference computer, make sure that the computer has not been compromised.|  
|Restrict and monitor the administrative users who are granted the role-based security roles that are related to application management:<br /><br /> - **Application Administrator**<br>- **Application Author**<br>- **Application Deployment Manager**|Even when you configure role-based administration, administrative users who create and deploy applications might have more permissions than you realize. For example, when administrative users create or modify an application, they can select dependent applications that are not in their security scope.|  
|When you configure Microsoft Application Virtualization (App-V) virtual environments, select applications in the virtual environment that have the same trust level.|Because applications in an App-V virtual environment can share resources, such as the clipboard, configure the virtual environment such that the selected applications have the same trust level.<br /><br /> For more information, see [How to create App-V virtual environments in System Center Configuration Manager](../../apps/deploy-use/create-app-v-virtual-environments.md).|  
|If you deploy applications for Mac computers, make sure that the source files are from a trustworthy source.|The CMAppUtil tool does not validate the signature of the source package, so make sure that it comes from a source that you trust. The CMAppUtil tool is not able to detect whether the files have been tampered with.|  
|If you deploy applications for Mac computers, secure the location of the **.cmmac** file and secure the communication channel when you import this file into Configuration Manager.|Because the **.cmmac** file that the CMAppUtil tool generates and that you import into Configuration Manager is not signed or validated, to help prevent tampering of this file, store it  in a secured folder and use IPsec or SMB between the following computers:<br /><br /> - The computer that runs the Configuration Manager console.<br /><br /> - The computer that stores the **.cmmac** file.|  
|If you configure a web application deployment type, use HTTPS rather than HTTP to secure the connection|If you deploy a web application by using an HTTP link rather than an HTTPS link, the device could be redirected to a rogue server and data transferred between the device and server could be tampered with.|  

##  Security issues for application management  

-   Low-rights users can copy files from the client cache on the client computer.  

     Users can read the client cache, but cannot write to it. With read permissions, a user can copy application installation files from one computer to another.  

-   Low-rights users can modify files that record software deployment history on the client computer.  

     Because the application history information is not protected, a user can modify files that report whether an application installed.  

-   App-V packages are not signed.  

     App-V packages in Configuration Manager do not support signing to verify that the content is from a trusted source and that it has not been altered in transit. There is no mitigation for this security issue; make sure that you follow the security best practice to download the content from a trusted source and from a secure location.  

-   Published App-V applications can be installed by all users on the computer.  

     When an App-V application is published on a computer, all users who log on to that computer can install the application. This means that you cannot restrict which users can install the application after it is published.  

-   You cannot restrict install permissions for the company portal  

     Although you can configure a client setting to restrict install permissions, for example, to primary users of a device, or to local administrators only, this setting does not work for the company portal. This could result in an elevation of privileges because a user could install an app that they should not be allowed to install.  

##  Certificates for Microsoft Silverlight 5, and elevated trust mode required for the application catalog  
 Configuration Manager clients require Microsoft Silverlight 5, which must run in elevated trust mode for users to install software from the Application Catalog. By default, Silverlight applications run in partial trust mode to prevent applications from accessing user data. Configuration Manager automatically installs Microsoft Silverlight 5 on clients if it is not already installed, and by default, it configures the Computer Agent client setting **Allow Silverlight applications to run in elevated trust mode** to **Yes**. This setting allows signed and trusted Silverlight applications to request elevated trust mode.  

 When you install the Application Catalog website point site system role, the client also installs a Microsoft signing certificate in the Trusted Publishers computer certificate store on each Configuration Manager client computer. This certificate allows Silverlight applications that are signed by this certificate to run in the elevated trust mode that computers require to install software from the Application Catalog. Configuration Manager automatically manages this signing certificate. To ensure service continuity, do not manually delete or move this Microsoft signing certificate.  

> [!WARNING]  
>  When enabled, the client setting **Allow Silverlight applications to run in elevated trust mode** allows all Silverlight applications that are signed by certificates in the Trusted Publishers certificate store in either the computer store or the user store to run in elevated trust mode. The client setting cannot enable elevated trust mode specifically for the Configuration Manager Application Catalog or for the Trusted Publishers certificate store in the computer store. If malware adds a rogue certificate in the Trusted Publishers store, for example, in the user store, malware that uses its own Silverlight application can now also run in elevated trust mode.  

 If you configure the client setting **Allow Silverlight applications to run in elevated trust mode** to be **No**, this does not remove the Microsoft signing certificate from clients.  

 For more information about trusted applications in Silverlight, see [Trusted Applications](http://go.microsoft.com/fwlink/p/?LinkId=252842).  

##  Privacy information for application management  
 Application management allows you to run any application, program, or script on any client computer or client mobile device in the hierarchy. Configuration Manager has no control over what types of applications, programs, or scripts you run or what type of information they transmit. During the application deployment process, Configuration Manager might transmit information between clients and servers that identify the device and logon accounts.  

 Configuration Manager maintains status information about the software deployment process. Software deployment status information is not encrypted during transmission unless the client communicates by using HTTPS. The status information is not stored in encrypted form in the database.  

 The use of Configuration Manager application installation to remotely, interactively, or silently install software on clients might be subject to software license terms for that software, and is separate from the Software License Terms for System Center Configuration Manager. Always review and agree to the Software Licensing Terms before you deploy software by using Configuration Manager.  

 Application deployment does not happen by default and requires several configuration steps.  

 Two optional features that help efficient software deployment are user device affinity and the Application Catalog:  

-   User device affinity maps a user to devices so that a Configuration Manager administrator can deploy software to a user, and the software is automatically installed on one or more computers that the user uses most often.  

-   The Application Catalog is a website that allows users to request software to install.  

 View the following sections for privacy information about user device affinity and the Application Catalog.  

 Before you configure application management, consider your privacy requirements.  

##  User device affinity  
-  Configuration Manager might transmit information between clients and management point site systems that identify the computer and logon account and the summarized usage for logon accounts.  
-  The information that is transmitted between the client and server is not encrypted unless the management point is configured to require clients communicate by using HTTPS.  
-  The computer and logon account usage information that is used to map a user to a device is stored on client computers, sent to management points, and then stored in the Configuration Manager database. The old information is deleted from the database by default after 90 days. The deletion behavior is configurable by setting the **Delete Aged User Device Affinity Data** site maintenance task.
-  Configuration Manager maintains status information about user device affinity. Status information is not encrypted during transmission unless clients are configured to communicate with management points by using HTTPS. Status information is not stored in encrypted form in the database.  
-  Computer, logon account usage information, and status information is not sent to Microsoft.  
-  Computer and logon usage information that is used to establish user and device affinity is always enabled. In addition, users and administrative users can supply user device affinity information.  

##  Application Catalog  
-  The Application Catalog allows the Configuration Manager administrator to publish any application or program or script for users to run. Configuration Manager has no control over what types of programs or scripts are published in the catalog, or what type of information they transmit.    
-  Configuration Manager might transmit information between clients and the Application Catalog site system roles that identify the computer and logon accounts. The information that is transmitted between the client and servers is not encrypted unless these site system roles are configured to require that clients connect by using HTTPS.  
-  The information about the application approval request is stored in the Configuration Manager database. The requests that are canceled or denied are deleted by default after 30 days, along with the corresponding request history entries. The deletion behavior is configurable by setting the **Delete Aged Application Request Data** site maintenance task. The application approval requests that are in approved and pending states are never deleted.  
-  Information that is sent to and from the Application Catalog is not sent to Microsoft.  
-  The Application Catalog is not installed by default. This installation requires several configuration steps.  
