

# What is Microsoft Intune

As organizations move to support hybrid and remote workforces, they're challenged with managing the different devices that access organization resources. Users need to collaborate, work from anywhere, and securely access and connect to these resources. Admins need to protect organization data, manage end user access, and support users from wherever they work.

To help with these challenges and tasks, cloud solutions like Microsoft Intune can help. Microsoft Intune focuses on mobile device management (MDM) and mobile application management (MAM). It's 100% cloud-based and works well with on-premises Configuration Manager environments.

Microsoft Intune is a family of product and services that focus on endpoint management. This family includes Configuration Manager, Windows Autopilot, and Endpoint Analytics. With these services, you get OS deployment, app and device policy management, and reporting & analytics.

## Key features and benefits

Some key features and benefits include:

- You can **manage users and devices**, including devices owned by your organizations and personally owned devices. Microsoft Intune supports Android, Android Open Source Project (AOSP), iOS/iPadOS, macOS, and Windows client devices. With Intune, you can use these devices to secure access to organization resources with policies you create.

  For more information, go to []().

- Intune **automates policy deployment** for apps, security, device configuration, compliance, conditional access, and more. When the policies are ready, you can deploy these policies to your user groups and device groups. To receive these policies, the devices only need internet access.

  For more information, go to [Common questions and answers with device policies in Microsoft Intune](./configuration/device-profile-troubleshoot.md).

- End users can **use the self-service features** in the Company Portal app to reset a PIN/password, install apps, join groups, and more. You can customize the Company Portal app to help reduce support calls.

  For more information, go to [Configure the Intune Company Portal apps, Company Portal website, and Intune app](./apps/company-portal-app.md).

- Integrates with **mobile threat defense** services, including Microsoft Defender for Endpoint and third party/partner services. With these services, you can create policies that respond to threats, do real-time risk analysis, and automate remediation.

  For more information, go to [Mobile Threat Defense integration with Intune](./protect/mobile-threat-defense.md).

- You **use a web-based admin center** that focuses on endpoint management. You can sign into the admin center from any device that has internet access.

  For more information, go to [Walkthrough Intune in Microsoft Endpoint Manager](tutorial-walkthrough-endpoint-manager.md).


Automatic app updates

## Integrates with other Microsoft services and apps

Microsoft Intune integrates with other Microsoft products and services that focus on endpoint management, including:

- **[Configuration Manager](../configmgr/core/understand/introduction.md)** for on-premises endpoint management, including deploying software updates and managing data centers

  You can use Intune and Configuration Manager together in a co-management scenario, use tenant attach, or use both. With these options, you get the benefits of the web-based admin center and can use other features available in Intune.

  For more specific information, go to:

  - [What is co-management](../configmgr/comanage/overview.md)
  - [Frequently asked questions about co-management](../configmgr/comanage/faq.md)
  - [How to enable Microsoft Endpoint Manager tenant attach](../configmgr/tenant-attach/device-sync-actions.md)

- **[Windows Autopilot](./autopilot/windows-autopilot.md)** for modern OS deployment and provisioning

  With Windows Autopilot, you can provision new devices and send these devices directly to users from the OEM or device provider. For existing devices, you can re-image these devices to use Windows Autopilot and deploy the latest Windows version.

  For more specific information, go to:

  - [Windows Autopilot overview](./autopilot/windows-autopilot.md)
  - [Windows Autopilot deployment for existing devices](./autopilot/existing-devices.md)

- **[Endpoint Analytics](./analytics/overview.md)** for visibility and reporting on end user experiences, including device performance and reliability

  You can use Endpoint Analytics to help identify policies or hardware issues that slow down devices. It also provides guidance that can help you proactively make improvements and help reduce help desk tickets.

  For more specific information, go to:

  - [What is Endpoint analytics](./analytics/overview.md)
  - [Enroll Intune devices into Endpoint analytics](./analytics/enroll-intune.md)

- **[Microsoft 365](/deployoffice/about-microsoft-365-apps)** for end user productivity Office apps, including Outlook, Teams, Sharepoint, OneDrive, and more

  Using Intune, you can deploy Microsoft 365 apps to users and devices in your organization. You can also deploy these apps when users sign in for the first time.

  For more specific information, go to:

  - [Add Microsoft 365 Apps to Windows 10/11 devices with Microsoft Intune](./apps/apps-add-office365.md)
  - [Microsoft 365 docs: Manage devices with Intune](/microsoft-365/solutions/manage-devices-with-intune-overview)

- **[Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint)** to help enterprises prevent, detect, investigate, and respond to threats

  In Intune, you can create a service-to-service connection between Intune and Microsoft Defender for Endpoint. When they're connected, you can create policies that scan files, detect threats, and report threat levels to Microsoft Defender for Endpoint. You can also create compliance policies that set an allowable level of risk. When combined with conditional access, you can block access to organization resources for devices that are noncompliant.

  For more specific information, go to:

  - [Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune](./protect/advanced-threat-protection.md)
  - [Configure Microsoft Defender for Endpoint in Intune](./protect/advanced-threat-protection-configure.md)

Windows 32 apps,

- [Deployment guide: Enroll Windows devices in Microsoft Intune](deployment-guide-enrollment-windows.md)

## Integrates with third party partner devices and apps

The Endpoint Manager admin center makes it easy to connect to different partner services, including:

- **Managed Google Play**: When you connect to your Managed Google Play account, admins can access your organization's private store for Android apps, and deploy these apps to your devices.

  For more information, go to [Add Managed Google Play apps to Android Enterprise devices with Intune](./apps/apps-add-android-for-work.md).

- **Apple `.p7m` token** and **Apple MDM push certificate**: When they're added, your iOS/iPadOS and macOS devices can enroll in Intune and receive policies from Intune.

  For more information, go to:

  - [Get an Apple MDM push certificate](./enrollment/apple-mdm-push-certificate-get.md)
  - [Automatically enroll iOS/iPadOS devices by using Apple's Automated Device Enrollment](./enrollment/device-enrollment-program-enroll-ios.md)

- **Apple VPP token**: When it's added, admins can access your volume purchased iOS/iPad and macOS app licenses, and deploy these apps to your devices.

  For more information, go to [manage iOS and macOS apps purchased through Apple Business Manager with Microsoft Intune](./apps/vpp-apps-ios.md).

- **TeamViewer**: When you connect to your TeamViewer account, you can use TeamViewer to remotely assist devices.

  For more information, go to [Use TeamViewer to remotely administer Intune devices](./remote-actions/teamviewer-support.md).

With these services, Intune:

- Gives admins simplified access to third party partner app services.
- Can manage hundreds of third party partner apps.
- Supports public retail store apps, line of business (LOB) apps, private apps not available in the public store, custom apps, and more.

For more platform-specific requirements to enroll third party partner devices in Intune, go to:

- [Deployment guide: Enroll Android devices in Microsoft Intune](deployment-guide-enrollment-android.md)
- [Deployment guide: Enroll iOS and iPadOS devices in Microsoft Intune](deployment-guide-enrollment-ios-ipados.md)
- [Deployment guide: Enroll macOS devices in Microsoft Intune](deployment-guide-enrollment-macos.md)


## Enroll in device management, application management, or both

Organization-owned devices are enrolled in Intune for **mobile device management (MDM)**.

In Intune, you create policies that configure features & settings and provide security & protection. The devices are fully managed by your organization, including the user identities that sign in to the devices, the apps installed on the devices, and the data accessed on the devices.

When devices enroll, you can deploy your policies during the enrollment process. When enrollment completes, the device is ready to use.

On bring-your-own-devices (BYOD) and personal devices, you can use Intune for **mobile application management (MAM)**. Devices using MAM focus on apps, including authenticating apps and protecting data within the apps.

With MAM, you can:

- Publish mobile apps to users
- Configure apps and automatically update apps
- View data reports that focus on app inventory and app usage

You can also use MDM and MAM together. If your devices are enrolled in MDM and have apps that need an extra layer of security, you can also use MAM app protection policies.

For more information, go to:

- MDM enrollment
- [App protection policies overview](../apps/app-protection-policy.md)
- [Create and assign app protection policies](../apps/app-protection-policies.md)

## Protect data on any device

With Intune, you can protect data on organization-owned devices and users personally-owned devices. Organization-owned devices are enrolled in Intune for **mobile device management (MDM)** and managed using policies you create.

With MDM, you can:

- Create and deploy policies that configure security settings, deploy certificates, scan devices, remediate threats, and more.
- View data and reports that measure compliance with your security settings and rules.
- Use conditional access to only allow managed and compliant devices access to organization resources, apps, and data.
- Remove organization data if a device is lost or stolen.

On bring-your-own-devices (BYOD) and personal devices, you can use Intune for **mobile application management (MAM)**. Devices using MAM focus on apps and protecting app data.

With MAM, you can:

- Prevent organization data from being copied and pasted into personal apps.
- Use app protection policies on apps and unmanaged devices enrolled in 3rd party or partner MDM.
- Use conditional access to restrict the apps that can access email and files.
- Remove organization data within apps.

> [!NOTE]
> If you manage on-premises Windows Server, you can use Configuration Manager. 

consolidate security policies and settings

## Simplify access

Intune helps organizations support employees who can work from anywhere. There are features you can configure that allow users to connect to an organization, wherever they might be. This section includes some common features that you can configure in Intune.

### Use Windows Hello for Business instead of passwords

Windows Hello for Business helps protect against phishing attacks and other security threats. It also helps users sign in to their devices and apps more quickly and easily.

Windows Hello for Business replaces passwords using biometrics, such as fingerprint, facial recognition, or PIN. This biometric information is stored locally on the devices and is never sent to external devices or servers.

For more information, go to:

- [Windows Hello for Business Overview](/windows/security/identity-protection/hello-for-business/hello-overview)
- [Manage Windows Hello for Business on devices when they enroll in Intune](../protect/windows-hello.md)

### Create a VPN connection for remote users

VPN policies gives users secure remote access to your organization network.

Using common VPN connection partners, including Check Point, Cisco, NetMotion, Pulse Secure, and more, you can create a VPN policy with your network settings. When the policy is ready, you deploy this policy to your users and devices that need to connect to your network remotely.

In the VPN policy, you can use certificates to authenticate the VPN connection. When you use certificates, your end users don't need to enter usernames and passwords.

For more information, go to:

- [Create VPN profiles to connect to VPN servers in Intune](./configuration/vpn-settings-configure.md)
- [Use certificates for authentication in Microsoft Intune](./protect/certificates-configure.md)

### Create a Wi-Fi connection for on-premises users

For users who need to connect to your organization network on-premises, you can create a Wi-Fi policy with your network settings. For example, you can connect to a specific SSID, select an authentication method, use a proxy, and more.

In the Wi-Fi policy, you can use certificates to authenticate the Wi-Fi connection. When you use certificates, your end users don't need to enter usernames and passwords.

When the policy is ready, you deploy this policy to your on-premises users and devices that need to connect to your on-premises network.

For more information, go to:

- [Create Wi-Fi policys to connect to Wi-Fi networks in Intune](./configuration/wifi-settings-configure.md)
- [Use certificates for authentication in Microsoft Intune](./protect/certificates-configure.md)

### Enable single sign-on (SSO) to your apps and services

When you enable SSO, users can sign in to apps and services with their Azure AD organization credentials, including some mobile threat defense partner apps.

- On iOS/iPadOS and macOS devices, you can use the Microsoft Enterprise SSO plug-in to automatically sign in to apps and websites that use Azure Active Directory (AD) for authentication, including Microsoft 365.

- On Windows devices, SSO is automatically built in and used to sign in to apps and websites that use Azure AD for authentication, including Microsoft 365. You can also enable SSO on VPN and Wi-Fi policies.

- On Android devices, you can use the Microsoft Authentication Library (MSAL) to enable SSO to Android apps.

  For more information, go to:

  - [Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS and macOS devices in Microsoft Intune](./configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md).
  - [Enable cross-app SSO on Android using MSAL](/azure/active-directory/develop/msal-android-single-sign-on)

simplify app lifecycle management
Enable Office apps 
native app experiences

## Next steps

- [Manage identities using Microsoft Intune](manage-identities.md)
- [Manage devices using Microsoft Intune](manage-devices.md)
- [Manage apps using Microsoft Intune](manage-apps.md)
