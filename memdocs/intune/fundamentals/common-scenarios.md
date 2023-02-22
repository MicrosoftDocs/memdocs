---
# required metadata

title: Common ways to use Microsoft Intune
description: Learn about six of the most common tasks that Microsoft Intune can help you manage.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 02/04/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection:
- tier1
- M365-identity-device-management
  - highpri
---

# Common ways to use Microsoft Intune

Before diving into implementation tasks, it's important to align your company's enterprise mobility stakeholders around the business goals of using Intune. Stakeholder alignment is important, whether you are new to enterprise mobility or migrating from another product.  

The needs around enterprise mobility are dynamically evolving, and Microsoft's approach to addressing them is sometimes different from other solutions in the market. The best way to align around business goals is to express your goals in terms of the scenarios you want to enable for your employees, partners, and IT department.  

Following are short introductions to the six most common scenarios that rely on Intune, accompanied with links to more information about how to plan and deploy each of them.

> [!NOTE]
> - Want to know how Microsoft IT uses Intune to give corporate access on mobile devices, while also keeping corporate data protected? Check out the [IT Showcase Library](https://www.microsoft.com/itshowcase), and search for "Intune".
> - The [Microsoft Security and Compliance blogs](https://techcommunity.microsoft.com/t5/microsoft-security-and/bg-p/MicrosoftSecurityandCompliance) are a great resource. You can filter on areas that interest you, including Enterprise Mobility + Security, data loss prevention, identity & access management, and more.

## Protecting your on-premises email and data so it can be safely accessed by mobile devices

Most enterprise mobility strategies begin with a plan to enable secure access to email for employees with mobile devices that connect to the Internet. Many organizations still have on-premises data and application servers, such as Microsoft Exchange, that are hosted on their corporate network.

Intune and Microsoft Enterprise Mobility + Security (EMS) provide a uniquely integrated [Conditional Access solution](../protect/conditional-access.md) for Exchange Server, which ensures that no mobile app can access email until that device is enrolled with Intune. You can implement this type of email access without deploying another gateway machine to the edge of your corporate network.

Intune also supports enabling access to mobile apps that require secure access to on-premises data, such as line-of-business app servers. This type of access is typically done using [Intune-managed certificates](../protect/certificates-configure.md) for access control, combined with a standard VPN gateway or proxy in the perimeter such as Microsoft Azure Active Directory Application Proxy.

In these cases, the only way to access corporate data is to enroll the device into management. Once the devices are enrolled, the management system ensures that they are compliant with your policies before they can access corporate data. Additionally, Intune's [App Wrapping Tool and App SDK](../developer/apps-prepare-mobile-application-management.md) can help contain the accessed data within your line-of-business app, so that it can't pass corporate data to consumer apps or services.

<!-- Learn more about how to plan and deploy Intune to help secure on-premises email and data. -->

## Protecting your Microsoft 365 email and data so it can be safely accessed by mobile devices

Protecting corporate data in Microsoft 365 (email, documents, instant messages, contacts) could not be easier for you or more seamless for your users.

Intune and Microsoft Enterprise Mobility + Security provide a uniquely integrated Conditional Access solution that ensures no users, apps, or devices can access Microsoft 365 data unless they meet your company's compliance requirements (performed [multi-factor authentication](../enrollment/multi-factor-authentication.md), enrolled with Intune, using managed app, supported OS version, device pin, low user risk profile, etc.).

The Office mobile apps in their respective app stores are ready to go with data containment policies that you can configure via Intune. This enables you to prevent data from being shared with apps (for example, with native email apps) and storage locations (for example, Dropbox) that aren't managed by IT. All this functionality is built into Microsoft 365 and EMS. You don't have to deploy additional infrastructure to get this value.

A common Microsoft 365 deployment practice is to require devices to enroll into management if they need to be fully set up with corporate apps, certs, Wi-Fi, or VPN configurations, a common scenario for corporate-owned devices.

However, if your user simply needs to access corporate email and documents, which is often the case for personally owned devices, then you can require the user to use the Office mobile apps (to which you have applied [app protection policies](../apps/app-protection-policies.md)) and skip enrolling the device altogether.

Either way, the Microsoft 365 data will be secured by policies you've defined.

<!-- Learn more about how to plan and deploy Intune to help secure Microsoft 365 email and data. -->

## Offer a bring your own device program to all employees

Bring your own device (BYOD) continues to grow in popularity among organizations as a means to reduce hardware expenditures or increase mobile productivity choices for employees. Just about everyone has a personal phone these days so why put another one in their pocket? The main challenge has always been to convince employees to enroll their personal device into management, as they are fearful of what their IT department will be able to see and do with their device.

When device enrollment is not a viable option, Intune offers an alternative BYOD approach of simply [managing the apps that contain corporate data](../apps/app-protection-policies.md). Intune protects the corporate data even if the app in question accesses both corporate and personal data, as is the case for Office mobile apps.

As an administrator, you can require users to access Microsoft 365 from the Office mobile apps and configure the apps with policies that keep the data protected (such as encrypting it, protecting it with a pin, and so on). These app protection policies prevent data loss from unmanaged apps and storage locations -- inside or outside of those apps. For example, the policies prevent a user from copying text from a corporate email profile into a consumer email profile even if both profiles are configured within Outlook Mobile. Similar configurations can be deployed for other services and applications that are required by your BYOD users.

<!-- Learn more about how to plan and deploy Intune to support BYOD.-->

## Issue corporate-owned phones to your employees

Many employees are mobile these days, making productivity on mobile devices an imperative to be competitive. These employees need seamless access to all corporate apps and data, at any time, wherever they are. You need to ensure that corporate data is secure and administrative costs are low.

Intune offers [bulk provisioning and management solutions](../enrollment/device-enrollment.md) that are integrated with the major corporate device management platforms on the market today, including the Apple Device Enrollment Program and the Samsung Knox mobile security platform. Centralized authoring of device configurations with Intune helps make provisioning of corporate devices something that can be highly automated.

Picture this: hand an employee an unopened iPhone box. The employee powers it on and is walked through a corporate-branded setup flow where they must authenticate themselves. The iPhone is seamlessly configured with [security policies](../configuration/device-profiles.md).

Then the employee launches the Intune Company Portal app to access the optional corporate apps that are available to them.

<!-- Learn more about how to plan and deploy Intune to support corporate owned devices. -->

## Issue limited-use shared tablets to your employees

Employees are increasingly making use of mobile technologies. For example, shared tablets are now commonly used by retail store employees.  Whether they're used to process a sale or instantly check inventory, tablets help create great customer interactions.

Simplicity of the user experience is critical in this case. For this reason, tablets are usually provided to employees in a limited-use mode, such that a single line-of-business app is the only thing that the employee can interact with. Intune enables you to bulk provision, secure, and centrally manage these shared [iOS and Android](../configuration/device-profiles.md) devices that can be configured to run in this limited-use mode.

<!-- Learn more about how to plan and deploy Intune to support shared tablets. -->

## Enable your employees to securely access Microsoft 365 from an unmanaged public kiosk

Sometimes your employees need to use devices, apps, or browsers that you can't manage, such as the public computers at trade shows and in hotel lobbies.

Should you allow your employees to access corporate email from them? With Intune and Microsoft Enterprise Mobility + Security, the answer can simply be "no", by [limiting email access to devices that are managed by your organization](../protect/conditional-access.md). This ensures that your strongly authenticated employee doesn't accidentally leave corporate data on the untrusted computer.

## Next steps

- [Microsoft Intune planning guide](intune-planning-guide.md)
- [Intune guided scenarios](guided-scenarios-overview.md)
