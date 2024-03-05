---
# required metadata

title: Troubleshoot securing data with Microsoft Edge for Business
titleSuffix:
description: Troubleshoot securing your corporate data in Microsoft Intune with Microsoft Edge for Business.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/04/2024
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:

# optional metadata

#audience:
#ROBOTS: 
ms.reviewer: samarti
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier1
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Troubleshoot securing data with Microsoft Edge for Business

Troubleshooting Mobile Application Management (MAM) for Windows can involve several steps. Here are some common issues and potential solutions:

1. **Ensure that the policy is assigned to the correct user group**: Make sure that the MAM policy is being applied to the intended users.

2. **Check that the necessary conditions and settings are properly defined in the policy**: Review the settings in your MAM policy to ensure they're configured as intended.

3. **Update Microsoft Edge to the latest version**: If an app is crashing during MAM initialization, make sure the app version and OS Meet the conditions.

If you continue to experience issues, it may be helpful to contact **Microsoft Support** for further assistance. Let me know if you need help with anything else.

:::image type="content" alt-text="Sign in with your work account - Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing_data_edge_for_business63.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business63.png":::

The following error means that you selected the incorrect enrollment method, you may have left the checkmark or select on No, sign into this app only, please redo the enrollment without this. Otherwise, you won't be MAM Enable.


:::image type="content" alt-text="Enrollment Window - Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing_data_edge_for_business64.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business64.png":::

## FAQ

**Does Microsoft Edge for Business require a separate download?**  

No. Microsoft Edge for Business is automatically triggered by signing in
with a Microsoft Entra.

**is Windows home version supported for MAM for Windows?**

MAM for Windows does support Windows Home Edition.

**Will all policies and configurations previously set by IT be applied to Edge for Business?** 

Yes, all policies and configurations currently in place will be inherited by Microsoft Edge for Business.

**What impact will this cause to my default browser settings?** 

There's no impact on users\' default browser settings. 

**What happens to favorites, passwords, etc.?**  

Passwords, favorites, and data currently associated with the user's work profile will be maintained in Microsoft Edge for Business. Passwords, favorites, and data aren't shared between the work browser window and the personal browser window. 

**MAM for Windows vs Microsoft Edge management service**

There are key differences between the management options, it's important to highlight that if you're using Microsoft Intune today to focus on creating app protection policies for your users and ensure a Secure Enterprise Browser configuration is in place. If you aren't using Microsoft Intune the Microsoft Edge management service is for you, and you are able to configure Microsoft Edge for Business policy and configuration for your organization. For more information about Microsoft Edge management service, see [Microsoft Edge for Business: AI and protection in one secure enterprise browser](https://aka.ms/EdgeSecurityWhitepaper).

## Conclusion

- We guide you through different scenarios to configure a **Microsoft Edge for Business** and **Microsoft Application Management** experience, from concept to implementation.

- We explain what an **App Protection Policy framework** is and how it can enhance security in your environment. This framework provides a robust layer of security for your environment. It allows admins to control how data is accessed and handled, ensuring that sensitive information is always protected.

- **Intune Device Encryption and Password Single Sign-On**: With Intune encryption, data is secured at rest and in transit. The password single sign-on feature in Microsoft Edge for Business enhances user convenience without compromising security.

- We provide a baseline of **the App Configuration Policy** that helps achieve another level of security, from Intune encryption to password single sign-on in Microsoft Edge for Business.

- We demonstrate how to configure the **Conditional Access Policy**. This feature allows IT admins to define and implement policies based on conditions such as user role, location, and risk level. It's a powerful tool for achieving a zero-trust security model.

- We present the **end-user experience**, showing what behavior can be expected once you implement the Microsoft Intune App Protection Policy for Windows devices.

- We provide key **troubleshooting examples**, some of them presented during research and other suggestions by the field.

- Finally, we've collected a series of **references** for deeper learning by reading and researching the material used to write this whitepaper.

Harnessing the power of these features, IT admins have the ability to construct an environment that isn't only secure and efficient, but also user-friendly. With Microsoft Edge for Business and Microsoft Application Management, you hold the key to fortifying your environment. Remember, the journey to security isn\'t a single sprint but a continuous marathon of enhancement and adaptation to emerging challenges. Keep pushing the boundaries and elevating your security posture! As your next step, we strongly urge you to implement the steps outlined in this whitepaper within your own environment. Continue to unlock the full potential of Microsoft Edge for Business and the secure Microsoft Application Management. You have the power to make a difference!

## Additional information

- [What is Conditional Access in Microsoft Entra? \| Microsoft Learn](/entra/identity/conditional-access/overview)

- [App protection policy settings for Windows - Microsoft Intune \| Microsoft Learn](/mem/intune/apps/app-protection-policy-settings-windows)

- [Use app-based Conditional Access policies with Intune - Microsoft Intune \| Microsoft Learn](/MEM/intune/protect/app-based-conditional-access-intune)

- [Data protection for Windows MAM \| Microsoft Learn](/mem/intune/apps/protect-mam-windows)

- [Data protection framework using app protection policies - Microsoft Intune \| Microsoft Learn](/mem/intune/apps/app-protection-framework)

- [Use role-based access control (RBAC) and scope tags for distributed IT - Microsoft Intune \| Microsoft Learn](/mem/intune/fundamentals/scope-tags)

- [Data protection for Windows MAM \| Microsoft Learn](/mem/intune/apps/protect-mam-windows)

- [Create Mobile Threat Defense (MTD) app protection policy with Intune - Microsoft Intune \| Microsoft Learn](/mem/intune/protect/mtd-app-protection-policy#to-create-an-mtd-app-protection-policy-for-windows)

- [Microsoft Edge security for your business \| Microsoft Learn](/deployedge/ms-edge-security-for-business)

- [Microsoft Edge for Business \| Microsoft Learn](/deployedge/microsoft-edge-for-business)

- [Browse more safely with Microsoft Edge \| Microsoft Learn](/deployedge/microsoft-edge-security-browse-safer)

- [What's New in Web Experiences, ignite 2020: Need to secure your remote workers? Choose Microsoft Edge as your browser for business \| Windows Experience Blog](https://blogs.windows.com/windowsexperience/2020/09/22/whats-new-in-web-experiences-ignite-2020-need-to-secure-your-remote-workers-choose-microsoft-edge-as-your-browser-for-business/)

- [Mobile Threat Defense with Microsoft Intune - Microsoft Intune \| Microsoft Learn](/mem/intune/protect/mobile-threat-defense)

- [Enable Mobile Threat Defense connector in Microsoft Intune - Microsoft Intune \| Microsoft Learn](/mem/intune/protect/mtd-connector-enable)

- [Set up the Better Mobile Threat Defense Connector with Intune \| Microsoft Learn](/mem/intune/protect/better-mobile-threat-defense-connector)

- [Troubleshoot user issues for Microsoft Intune app protection policies - Intune \| Microsoft Learn](/troubleshoot/mem/intune/app-protection-policies/troubleshoot-mam)

- [The Secure Enterprise Browser \| Microsoft Edge for Business](https://www.microsoft.com/en-us/edge/business?form=MA13FJ)

- [Microsoft Edge management service \| Microsoft Learn](/deployedge/microsoft-edge-management-service?form=MT00IS)

- [Manage Microsoft Edge on iOS and Android with Intune \| Microsoft Learn](/mem/intune/apps/manage-microsoft-edge)

- [Create and deploy app protection policies - Microsoft Intune \| Microsoft Learn](/mem/intune/apps/app-protection-policies)

- [Protect Your Organization from Online Threats \| Microsoft Edge for Business](https://www.microsoft.com/en-in/edge/business/security?form=MA13I2)
