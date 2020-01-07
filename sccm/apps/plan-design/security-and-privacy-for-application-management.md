---
title: Security and privacy for apps
titleSuffix: Configuration Manager
description: Guidance and recommendations for security and privacy when managing applications in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Security and privacy for application management in Configuration Manager

*Applies to: Configuration Manager (current branch)*

## Security guidance for application management  

### Use the Software Center without the application catalog

<!--1358309-->

The application catalog's Silverlight user experience isn't supported as of current branch version 1806. This configuration helps you reduce the server infrastructure required to deliver applications to users.

Starting in version 1906, updated clients automatically use the management point for user-available application deployments. You also can't install new application catalog roles. Support ends for the application catalog roles with version 1910. Reducing the server infrastructure also reduces the attack surface.

To deliver a consistent and secure application experience for internet-based clients, use Azure Active Directory and the cloud management gateway.

For more information, see [Configure Software Center](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).

### Use HTTPS with the application catalog

> [!Important]  
> Support ends for the application catalog roles with version 1910. For more information, see [Remove the application catalog](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).  

Configure the application catalog website point and the application catalog web service point to accept HTTPS connections. With this configuration, the server is authenticated to users. The transmitted data is protected from tampering and viewing.

Help prevent social engineering attacks by educating users to only connect to trusted websites. Educate users about the dangers of malicious websites.

When you don't use HTTPS, don't use the branding configuration options. These settings show the name of your organization in the application catalog as proof of identity.  


### Use role separation

> [!Important]  
> Support ends for the application catalog roles with version 1910. For more information, see [Remove the application catalog](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).  

Install the application catalog website point and the application catalog web service point on separate servers. If the website point is compromised, it's separate from the web service point. This design helps to protect the Configuration Manager clients and infrastructure. This configuration is especially important if the website point accepts client connections from the internet. It makes the server more vulnerable to attack.  

### Close browser windows

> [!Important]  
> Support ends for the application catalog roles with version 1910. For more information, see [Remove the application catalog](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).  

Educate users to close the browser window when they finish using the application catalog. If users browse to an external website in the same browser window that they used for the application catalog, the browser continues to use the security settings that are suitable for trusted sites in the intranet.  

### Centrally specify user device affinity

Manually specify the user device affinity instead of letting users identify their primary device. Don't enable usage-based configuration.

Don't consider information that's collected from users or from the device to be authoritative. If you deploy software by using user device affinity that a trusted administrator doesn't specify, the software might be installed on computers and to users who aren't authorized to receive that software.  

### Don't run deployments from distribution points

Always configure deployments to download content from distribution points rather than run from distribution points. When you configure deployments to download content from a distribution point and run locally, the Configuration Manager client verifies the package hash after it downloads the content. The client discards the package if the hash doesn't match the hash in the policy.

If you configure the deployment to run directly from a distribution point, the Configuration Manager client doesn't verify the package hash. This behavior means that the Configuration Manager client can install software that's been tampered with.

If you must run deployments directly from distribution points, use NTFS least permissions on the packages on the distribution points. Also use internet protocol security (IPsec) to secure the channel between the client and the distribution points, and between the distribution points and the site server.

### <a name="bkmk_interact"></a> Don't let users interact with elevated processes
  
If you enable the options to **Run with administrative rights** or **Install for system**, don't let users interact with those applications. When you configure an application, you can set the option to **Allow users to view and interact with the program installation**. This setting allows users to respond to any required prompts in the user interface. If you also configure the application to **Run with administrative rights**, or starting in version 1802 **Install for system**, an attacker at the computer that runs the program could use the user interface to escalate privileges on the client computer.

Use programs that use Windows Installer for setup and per-user elevated privileges for software deployments that require administrative credentials. Setup must be run in the context of a user who doesn't have administrative credentials. Windows Installer per-user elevated privileges provide the most secure way to deploy applications that have this requirement.

### Restrict whether users can install software interactively

Configure the **Install permissions** client setting in the **Computer Agent** group. This setting restricts the types of users who can install software in Software Center.

For example, create a custom client setting with **Install permissions** set to **Only administrators**. Apply this client setting to a collection of servers. This configuration prevents users without administrative permissions from installing software on those servers.  

### For mobile devices, deploy only applications that are signed

Deploy mobile device applications only if they're code-signed by a certification authority (CA) that the mobile device trusts.

For example:

- An application from a vendor, which is signed by a well-known CA like VeriSign.  

- An internal application that you sign independent from Configuration Manager by using your internal CA.  

- An internal application that you sign by using Configuration Manager when you create the application type and use a signing certificate.

### Secure the location of the mobile device application signing certificate

If you sign mobile device applications by using the **Create Application Wizard** in Configuration Manager, secure the location of the signing certificate file, and secure the communication channel. To help protect against elevation of privileges and against man-in-the-middle attacks, store the signing certificate file in a secured folder.

Use IPsec between the following computers:

- The computer that runs the Configuration Manager console
- The computer that stores the certificate signing file
- The computer that stores the application source files

Alternatively, sign the application independent of Configuration Manager and before you run the **Create Application Wizard**.

### Implement access controls

To protect reference computers, implement access controls. When you configure the detection method in a deployment type by browsing to a reference computer, make sure that the computer isn't compromised.

### Restrict and monitor administrative users

Restrict and monitor the administrative users who you grant the following application management role-based security roles:

- **Application Administrator**
- **Application Author**
- **Application Deployment Manager**

Even when you configure role-based administration, administrative users who create and deploy applications might have more permissions than you realize. For example, administrative users who create or change an application can select dependent applications that aren't in their security scope.

### Configure App-V apps in virtual environments with the same trust level

When you configure Microsoft Application Virtualization (App-V) virtual environments, select applications that have the same trust level in the virtual environment. Because applications in an App-V virtual environment can share resources, like the clipboard, configure the virtual environment so that the selected applications have the same trust level.

For more information, see [Create App-V virtual environments](/sccm/apps/deploy-use/create-app-v-virtual-environments).

### Make sure macOS apps are from a trustworthy source

If you deploy applications for macOS devices, make sure that the source files are from a trustworthy source. The CMAppUtil tool doesn't validate the signature of the source package. Make sure the package comes from a source that you trust. The CMAppUtil tool can't detect whether the files have been tampered with.

### Secure the cmmac file for macOS apps

If you deploy applications for macOS computers, secure the location of the **.cmmac** file. The CMAppUtil tool generates this file, and then you import it to Configuration Manager. This file isn't signed or validated.

Secure the communication channel when you import this file to Configuration Manager. To help prevent tampering with this file, store it in a secured folder. Use IPsec between the following computers:

- The computer that runs the Configuration Manager console  
- The computer that stores the **.cmmac** file  

### Use HTTPS for web applications

If you configure a web application deployment type, use HTTPS to secure the connection. If you deploy a web application by using an HTTP link rather than an HTTPS link, the device could be redirected to a rogue server. Data that's transferred between the device and server could be tampered with.


## Security issues for application management  

- Low-rights users can copy files from the client cache on the client computer.  

     Users can read the client cache but can't write to it. With read permissions, a user can copy application installation files from one computer to another.  

- Low-rights users can change files that record software deployment history on the client computer.  

     Because the application history information isn't protected, a user can change files that report whether an application is installed.  

- App-V packages aren't signed.  

     App-V packages in Configuration Manager don't support signing. Digital signatures verify the content is from a trusted source and wasn't altered in transit. There's no mitigation for this security issue. Follow the security best practice to download the content from a trusted source and from a secure location.  

- Published App-V applications can be installed by all users on the computer.  

     When an App-V application is published on a computer, all users who sign in to that computer can install the application. You can't restrict the users who can install the application after it's published.  


## <a name="BKMK_CertificatesSilverlight5"></a> Certificates for Microsoft Silverlight 5 and elevated trust mode required for the application catalog  

> [!Important]  
> Support ends for the application catalog roles with version 1910. For more information, see [Remove the application catalog](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).  

Configuration Manager clients version 1710 and earlier require Microsoft Silverlight 5, which must run in elevated trust mode for users to install software from the application catalog. By default, Silverlight applications run in partial trust mode to prevent applications from accessing user data. If it isn't already installed, Configuration Manager automatically installs Microsoft Silverlight 5 on clients. By default, Configuration Manager sets the Computer Agent **Allow Silverlight applications to run in elevated trust mode** client setting to **Yes**. This setting lets signed and trusted Silverlight applications request elevated trust mode.  

When you install the application catalog website point site system role, the client also installs a Microsoft signing certificate in the Trusted Publishers computer certificate store on each Configuration Manager client computer. Silverlight applications signed by this certificate run in the elevated trust mode, which computers require to install software from the application catalog. Configuration Manager automatically manages this signing certificate. To increase service continuity, don't manually delete or move this Microsoft signing certificate.  

> [!WARNING]  
> When enabled, the **Allow Silverlight applications to run in elevated trust mode** client setting lets all Silverlight applications, which are signed by certificates in the Trusted Publishers certificate store in either the computer store or the user store, run in elevated trust mode. The client setting can't enable elevated trust mode specifically for the Configuration Manager application catalog or for the Trusted Publishers certificate store in the computer store. If malware adds a rogue certificate in the Trusted Publishers store, malware that uses its own Silverlight application can now also run in elevated trust mode.  

If you set the **Allow Silverlight applications to run in elevated trust mode** setting to **No**, clients don't remove the Microsoft signing certificate.  

For more about trusted applications in Silverlight, see [Trusted Applications](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/ee721083\(v=vs.95\)).  


## Privacy information for application management  

Application management lets you run any application, program, or script on any client in the hierarchy. Configuration Manager has no control over the types of applications, programs, or scripts that you run or the type of information that they transmit. During the application deployment process, Configuration Manager might transmit information that identifies the device and sign-in accounts between clients and servers.  

Configuration Manager maintains status information about the software deployment process. Software deployment status information isn't encrypted during transmission unless the client communicates by using HTTPS. The status information isn't stored in encrypted form in the database.  

The use of Configuration Manager application installation to remotely, interactively, or silently install software on clients might be subject to software license terms for that software. This use is separate from the Software License Terms for Configuration Manager. Always review and agree to the Software Licensing Terms before you deploy software by using Configuration Manager.  

Configuration Manager collects diagnostics and usage data about applications, which is used by Microsoft to improve future releases. For more information, see [Diagnostics and usage data](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).

Application deployment doesn't happen by default and requires several configuration steps.  

The following features help efficient software deployment:

- **User device affinity** maps a user to devices. A Configuration Manager administrator deploys software to a user. The client automatically installs the software on one or more computers that the user uses most often.  

- **Software Center** is installed automatically on a device when you install the Configuration Manager client. Users change settings, browse for and install software from Software Center.  

- The **application catalog** is a website that lets users request software to install.  

    > [!Important]  
    > Support ends for the application catalog roles with version 1910. For more information, see [Remove the application catalog](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).  

### <a name="bkmk_privacy-uda"></a> User device affinity privacy information

- Configuration Manager might transmit information between clients and management point site systems. The information might identify the computer and sign-in account and the summarized usage for sign-in accounts.  

- The information that's transmitted between the client and server isn't encrypted, unless the management point is configured to require clients to communicate by using HTTPS.  

- The computer and sign-in account usage information, which is used to map a user to a device, is stored on client computers, sent to management points, and then stored in the Configuration Manager database. The old information is deleted from the database by default after 90 days. The deletion behavior is configurable by setting the **Delete Aged User Device Affinity Data** site maintenance task.  

- Configuration Manager maintains status information about user device affinity. Status information isn't encrypted during transmission, unless clients are configured to communicate with management points by using HTTPS. Status information isn't stored in encrypted form in the database.  

- Computer and sign-in usage information that's used to establish user and device affinity is always enabled. Users and administrative users can supply user device affinity information.  

### <a name="bkmk_privacy-userex"></a> Software Center privacy information

- Software Center lets the Configuration Manager admin publish any application or program or script for users to run. Configuration Manager has no control over the types of programs or scripts that are published in the catalog or the type of information that they transmit.  

- Configuration Manager might transmit information between clients and the management point. The information might identify the computer and sign-in accounts. The information that's transmitted between the client and servers isn't encrypted, unless you configure the management point to require clients connect by using HTTPS.  

- The information about the application approval request is stored in the Configuration Manager database. Requests that are canceled or denied and the corresponding request history entries are deleted by default after 30 days. The deletion behavior is configurable by setting the **Delete Aged Application Request Data** site maintenance task. Application approval requests that are in approved and pending states are never deleted.  

- Software Center is installed automatically when you install the Configuration Manager client on a device.  

### Application catalog privacy information

> [!Important]  
> Support ends for the application catalog roles with version 1910. For more information, see [Remove the application catalog](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).  

- The application catalog isn't installed by default. This installation requires several configuration steps.  

- The application catalog lets the Configuration Manager admin publish any application or program or script for users to run. Configuration Manager has no control over the types of programs or scripts that are published in the catalog or the type of information that they transmit.  

- Configuration Manager might transmit information between clients and the application catalog site system roles. The information might identify the computer and sign-in accounts. The information that's transmitted between the client and servers isn't encrypted, unless these site system roles are configured to require clients connect by using HTTPS.  
