---
title: Security and privacy for apps
titleSuffix: Configuration Manager
description: Guidance and recommendations for security and privacy when managing applications in Configuration Manager.
ms.date: 08/10/2021
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Security and privacy for application management in Configuration Manager

*Applies to: Configuration Manager (current branch)*

## Security guidance

### Centrally specify user device affinity

Manually specify the user device affinity instead of letting users identify their primary device. Don't enable usage-based configuration.

Don't consider information that's collected from users or from the device to be authoritative. If you deploy software by using user device affinity that a trusted administrator doesn't specify, the software might be installed on computers and to users who aren't authorized to receive that software.

### Don't run deployments from distribution points

Always configure deployments to download content from distribution points rather than run from distribution points. When you configure deployments to download content from a distribution point and run locally, the Configuration Manager client verifies the package hash after it downloads the content. The client discards the package if the hash doesn't match the hash in the policy.

If you configure the deployment to run directly from a distribution point, the Configuration Manager client doesn't verify the package hash. This behavior means that the Configuration Manager client can install software that's been tampered with.

If you must run deployments directly from distribution points, use NTFS least permissions on the packages on the distribution points. Also use internet protocol security (IPsec) to secure the channel between the client and the distribution points, and between the distribution points and the site server.

### <a name="bkmk_interact"></a> Don't let users interact with elevated processes
  
If you enable the options to **Run with administrative rights** or **Install for system**, don't let users interact with those applications. When you configure an application, you can set the option to **Allow users to view and interact with the program installation**. This setting allows users to respond to any required prompts in the user interface. If you also configure the application to **Run with administrative rights** or **Install for system**, an attacker at the computer that runs the program could use the user interface to escalate privileges on the client computer.

Use programs that use Windows Installer for setup and per-user elevated privileges for software deployments that require administrative credentials. Setup must be run in the context of a user who doesn't have administrative credentials. Windows Installer per-user elevated privileges provide the most secure way to deploy applications that have this requirement.

> [!NOTE]
> When the user starts the application installation process from Software Center, the option to **Allow users to view and interact with the program installation** can't control user interactions with any other processes created by the application installer. Because of this behavior, even if you don't select this option, the user may still be able to interact with an elevated process. To avoid this issue, don't deploy applications that create other processes with user interactions. If you have to install this type of application, deploy it as **Required** and configure the user notification experience to **Hide in Software Center and all notifications**.<!-- 10303284 -->

### Restrict whether users can install software interactively

Configure the **Install permissions** client setting in the **Computer Agent** group. This setting restricts the types of users who can install software in Software Center.

For example, create a custom client setting with **Install permissions** set to **Only administrators**. Apply this client setting to a collection of servers. This configuration prevents users without administrative permissions from installing software on those servers.

For more information, see [About client settings](../../core/clients/deploy/about-client-settings.md#install-permissions).

### For mobile devices, only deploy signed applications

Deploy mobile device applications only if they're code-signed by a certification authority (CA) that the mobile device trusts.

For example:

- An application from a vendor, which is signed by a public and globally trusted certificate provider.

- An internal application that you sign independent from Configuration Manager by using your internal CA.

- An internal application that you sign by using Configuration Manager when you create the application type and use a signing certificate.

### Secure the location of the mobile device application signing certificate

If you sign mobile device applications by using the **Create Application Wizard** in Configuration Manager, secure the location of the signing certificate file, and secure the communication channel. To help protect against elevation of privileges and man-in-the-middle attacks, store the signing certificate file in a secured folder.

Use IPsec between the following computers:

- The computer that runs the Configuration Manager console
- The computer that stores the certificate signing file
- The computer that stores the application source files

Instead, sign the application independent of Configuration Manager and before you run the **Create Application Wizard**.

### Implement access controls

To protect reference computers, implement access controls. When you configure the detection method in a deployment type by browsing to a reference computer, make sure that the computer isn't compromised.

### Restrict and monitor administrative users

Restrict and monitor the administrative users who you grant the following application management role-based security roles:

- **Application Administrator**
- **Application Author**
- **Application Deployment Manager**

Even when you [configure role-based administration](../../core/servers/deploy/configure/configure-role-based-administration.md), administrative users who create and deploy applications might have more permissions than you realize. For example, administrative users who create or change an application can select dependent applications that aren't in their security scope.

### Configure App-V apps in virtual environments with the same trust level

When you configure Microsoft Application Virtualization (App-V) virtual environments, select applications that have the same trust level in the virtual environment. Because applications in an App-V virtual environment can share resources, like the clipboard, configure the virtual environment so that the selected applications have the same trust level.

For more information, see [Create App-V virtual environments](../deploy-use/create-app-v-virtual-environments.md).

### Make sure macOS apps are from a trustworthy source

If you deploy applications for macOS devices, make sure that the source files are from a trustworthy source. The CMAppUtil tool doesn't validate the signature of the source package. Make sure the package comes from a source that you trust. The CMAppUtil tool can't detect whether the files have been tampered with.

### Secure the cmmac file for macOS apps

If you deploy applications for macOS computers, secure the location of the `.cmmac` file. The CMAppUtil tool generates this file, and then you import it to Configuration Manager. This file isn't signed or validated.

Secure the communication channel when you import this file to Configuration Manager. To help prevent tampering with this file, store it in a secured folder. Use IPsec between the following computers:

- The computer that runs the Configuration Manager console
- The computer that stores the `.cmmac` file

### Use HTTPS for web applications

If you configure a web application deployment type, use HTTPS to secure the connection. If you deploy a web application by using an HTTP link rather than an HTTPS link, the device could be redirected to a rogue server. Data that's transferred between the device and server could be tampered with.

## Security issues

- Low-rights users can change files that record software deployment history on the client computer.

    Because the application history information isn't protected, a user can change files that report whether an application is installed.

- App-V packages aren't signed.

    App-V packages in Configuration Manager don't support signing. Digital signatures verify the content is from a trusted source and wasn't altered in transit. There's no mitigation for this security issue. Follow the security best practice to download the content from a trusted source and from a secure location.  

- Published App-V applications can be installed by all users on the computer.

    When an App-V application is published on a computer, all users who sign in to that computer can install the application. You can't restrict the users who can install the application after it's published.

## Privacy information

Application management lets you run any application, program, or script on any client in the hierarchy. Configuration Manager has no control over the types of applications, programs, or scripts that you run or the type of information that they transmit. During the application deployment process, Configuration Manager might transmit information that identifies the device and sign-in accounts between clients and servers.

Configuration Manager maintains status information about the software deployment process. Unless the client communicates by using HTTPS, software deployment status information isn't encrypted during transmission. The status information isn't stored in encrypted form in the database.

The use of Configuration Manager application installation to remotely, interactively, or silently install software on clients might be subject to software license terms for that software. This use is separate from the Software License Terms for Configuration Manager. Always review and agree to the Software Licensing Terms before you deploy software by using Configuration Manager.

Configuration Manager collects diagnostics and usage data about applications, which is used by Microsoft to improve future releases. For more information, see [Diagnostics and usage data](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).

Application deployment doesn't happen by default and requires several configuration steps.

The following features help efficient software deployment:

- **User device affinity** maps a user to devices. A Configuration Manager administrator deploys software to a user. The client automatically installs the software on one or more computers that the user uses most often.

- **Software Center** is installed automatically on a device when you install the Configuration Manager client. Users change settings, browse for software, and install software from Software Center.

### <a name="bkmk_privacy-uda"></a> User device affinity privacy information

- Configuration Manager might transmit information between clients and management point site systems. The information might identify the computer, the sign-in account, and the summarized usage for sign-in accounts.

- Unless you configure the management point to require HTTPS communication, the information that's transmitted between the client and server isn't encrypted.

- The computer and sign-in account usage information is used to map a user to a device. Configuration Manager stores this information on client computers, sends it to management points, and then stores it in the site database. By default, the site deletes old information from the database after 90 days. The deletion behavior is configurable by setting the [Delete Aged User Device Affinity Data](../../core/servers/manage/reference-for-maintenance-tasks.md#delete-aged-user-device-affinity-data) site maintenance task.

- Configuration Manager maintains status information about user device affinity. Unless you [configure clients](../../core/plan-design/security/configure-security.md#signing-and-encryption) to communicate with management points by using HTTPS, they don't encrypt status information during transmission. The site doesn't store status information in encrypted form in the database.

- Computer and sign-in usage information that's used to establish user and device affinity is always enabled. Users and administrative users can supply user device affinity information.

### <a name="bkmk_privacy-userex"></a> Software Center privacy information

- Software Center lets the Configuration Manager administrator publish any application, program, or script for users to run. Configuration Manager has no control over the types of programs or scripts that are published in Software Center or the type of information that they transmit.

- Configuration Manager might transmit information between clients and the management point. The information might identify the computer and sign-in accounts. Unless you configure the management point to require clients connect by using HTTPS, the information that's transmitted between the client and servers isn't encrypted.

- The information about the application approval request is stored in the Configuration Manager database. For requests that are canceled or denied, the corresponding request history entries are deleted after 30 days by default. You can configure this deletion behavior with the [Delete Aged Application Request Data](../../core/servers/manage/reference-for-maintenance-tasks.md#delete-aged-application-request-data) site maintenance task. The site never deletes application approval requests that are in approved and pending states.

- When you install the Configuration Manager client on a device, it automatically installs Software Center.
