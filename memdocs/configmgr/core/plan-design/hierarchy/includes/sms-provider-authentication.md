---
author: banreet
ms.author: banreetkaur
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: include
ms.date: 05/04/2021
ms.localizationpriority: medium
---

<!--1357013-->
You can specify the minimum authentication level for administrators to access Configuration Manager sites. This feature enforces administrators to sign in to Windows with the required level before they can access Configuration Manager. It applies to all components that access the SMS Provider. For example, the Configuration Manager console, SDK methods, and Windows PowerShell cmdlets.

Configuration Manager supports the following authentication levels:

- **Windows authentication**: Require authentication with Active Directory domain credentials. This setting is the previous behavior, and the current default setting.

- **Certificate authentication**: Require authentication with a valid certificate that's issued by a trusted PKI certificate authority. You don't configure this certificate in Configuration Manager. Configuration Manager requires the administrator to be signed into Windows using PKI.

- **Windows Hello for Business authentication**: Require authentication with strong two-factor authentication that's tied to a device and uses biometrics or a PIN. For more information, see [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-identity-verification).

    > [!IMPORTANT]
    > When you select this setting, the SMS Provider and administration service require the user's authentication token to contain a multi-factor authentication (MFA) claim from Windows Hello for Business. In other words, a user of the console, SDK, PowerShell, or administration service has to authenticate to Windows with their Windows Hello for Business PIN or biometric. Otherwise the site rejects the user's action.
    >
    > This behavior is for _Windows Hello for Business_, not Windows Hello.<!-- SCCMDocs#2088 -->

For more information on how to configure this setting, see [Configure SMS Provider authentication](../../security/configure-security.md#sms-provider-authentication).
