# Secure your corporate data in Intune with Microsoft Edge for Business

**Authors:** 
Martinez, S., , Wu, I., Emerson, D., Turner, R., Lin, C., Askilsrud, C., Southgate, R., Kunze, C., Osorio, C., Poehlman, J., Hamilton, A.

**Applies to:**
- Mobile App Management (MAM) 
- Microsoft Edge for Business

This solution content is a comprehensive guide that provides valuable insights into secure enterprise browser configuration and implementation related to Mobile App Management and Microsoft Edge for Business.

## Target Audience

The target audience for this solution content primarily includes:

- **Intune Administrators:** The solution content provides detailed guidance on configuring and managing Microsoft Edge for Business, making it a valuable resource for IT admins.
- **Security Professionals:** With its focus on features like App Protection Policy framework, App Configuration Profiles, Data Encryption, and Conditional Access Policy, the solution content is also beneficial for security professionals looking to enhance their organization's security posture.
- **Decision Makers:** The solution content can help decision makers understand the security, productivity, and manageability benefits of Microsoft Edge for Business, aiding them in making informed decisions about browser choice in their organization.

> [!NOTE]
> Remember, the solution content is designed to empower its readers with knowledge and encourage them to leverage the full potential of Microsoft Edge for Business and Microsoft Application Management.

## Overview

**Securing your Corporate Data: A Guide to Microsoft Mobile App Management and Microsoft Edge for Business solution content** is a comprehensive guide that provides valuable insights into the concept of
Microsoft Edge for Business and secure enterprise browser configuration and its implementation. Here are some of the essential components in this solution content.

1. **Understanding Microsoft Edge for Business** This solution content explains what Microsoft Edge for Business and Microsoft Application Management is, its importance in today's digital landscape, and how it can protect your organization from various cyber threats.
2. **Creating Microsoft Edge for Business Mobile Application Management (MAM) for Windows Policy** This solution content guides you on how to create an App Protection policy for Windows, ensuring secure access and usage of enterprise applications.
3. **Mobile Application Management (MAM) for Mobile Policy** This solution content covers the creation of an App Protection policy for mobile devices, which is crucial in an era where mobile devices are extensively used for business purposes.
4. **Microsoft Entra Conditional Access Policy** This solution content shows how to create a conditional access policy, which is a critical aspect of modern security frameworks. It helps control who or what can access your business data under specific conditions.
5. **End User Experience** This solution content provides insights into the end user experience, helping you understand how security measures impact the user interaction with the system.
6. **Windows Security Center Integration** This solution content explains how the secure enterprise browser integrates with the Windows Security Center, enhancing the overall security posture of your organization.

In summary, this solution content is an essential read for those seeking to bolster their organization's browser security while maintaining a seamless user experience. It offers a detailed guide on establishing various policies and integrating services, thereby simplifying the task of managing and securing Microsoft Edge for Business. Immerse yourself in this resource and arm yourself with the knowledge needed to safeguard your organization in the digital realm. For more information about Microsoft Edge Security solution content, see [Microsoft Edge for Business: AI and protection in one secure enterprise browser](https://aka.ms/EdgeSecuritywhitepaper).

### What is Microsoft Edge for Business?

Microsoft Edge for Business is secure by default and a dedicated Microsoft Edge experience built for work that enables admins in organizations to give their users a productive and secure work browser across managed and unmanaged devices. It has the same rich set of enterprise controls, security, and productivity features that you're already familiar with in Microsoft Edge, but it's built to help meet the evolving needs of businesses.

Microsoft Edge for Business aims to address the needs of both end users and IT Pros as the browser that automatically separates work and personal browsing into dedicated browser windows with their own favorites, separate caches, and storage locations. This separation ensures that work related content doesn't get intermingled with personal browsing, preventing cognitive overload or end users from accidentally sharing sensitive information with unintended audiences. Microsoft Edge for Business is going to be the standard browser experience for organizations, activated by a Microsoft Entra entity
(formerly Azure Active Directory) sign in, upon general availability.

For more information, see the [build announcement](https://blogs.windows.com/msedgedev/2023/05/23/microsoft-edge-build-2023-innovations-in-AI-productivity-management-sidebar-apps/#business).

Microsoft Edge for Business is available on managed PCs starting in Stable release version **116**, and available in public preview on unmanaged devices.

### Is this a new browser?

No, this isn't a new browser. This is a new, dedicated Microsoft Edge experience built for work that enables organizations to configure it to maximize productivity and security. It has the same functionality that you're already familiar with in Microsoft Edge plus the optional automatic switching built to help meet the evolving needs of users and businesses. Signing in with Microsoft Entra will automatically enable Microsoft Edge for Business.  

### Benefits to customers

Microsoft Edge for Business has several benefits for customers. For IT, Microsoft Edge for Business can reduce the surface area for cyberattacks, heightening the organization's security posture, since it offers the opportunity to streamline down to one browser for all use cases. For end users who are signed in with work and personal profiles, Microsoft Edge for Business can provide better browsing experience with automatic switching, which has security and privacy benefits.

**Work Browser (Visual Refresh):** The Microsoft Edge for Business icon replaces the existing Microsoft Edge icon in the taskbar and other shortcuts:

:::image type="content" alt-text="" source="././media/securing_data_edge_for_business.png" lightbox="././media/securing_data_edge_for_business1.png":::

**Enhanced Security:** Using App protection policies ensures a more secure and protected browsing experience by making sure the enterprise
data remain secured.

**Centralized Management:** Microsoft Intune provides a management experience that simplifies the process of managing a Microsoft Edge for Business policy experience.

You can enable protected Mobile Application Management (MAM) access to org data on personal devices. This capability uses the following functionality:
- Intune Application Configuration Policies (ACP) to customize the org user experience.
- Intune Application Protection Policies (APP) to secure org data and ensure the client device is healthy.
- Windows Security Center client threat defense integrated with Intune APP to detect local health threats on personal Windows devices.
- Microsoft Entra Conditional Access to ensure the device is protected and healthy before granting protected services access via Microsoft Entra.

## Zero Trust Methodology

The Zero Trust methodology aims to bring a new way of thinking to how an organization should approach security and is increasingly becoming the standard for security strategy. Prior best practices revolved around the model of "trust but verify," however attacks in today's landscape can take advantage of the trust inherent in that model, driving a need for change in tackling this challenge. As a result, organizations are changing their security strategy to align with three principles based on the concept of "never trust, always verify":

**Verify explicitly** -- always authenticate and authorize based on all available data points, including user identity, location, device health, service or workload, data classification, and anomalies.

**Use least-privilege access** -- limiting user access via just-in-time and just-enough-access (JIT/JEA), risk-based adaptive policies, and data protection to help secure both data and productivity.

**Assume breach** -- minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses.

#### Complements Zero Trust

Microsoft Edge for Business is built with Chromium, giving it the well-engineered and tested security architecture design at its foundation. Because of this foundation, Microsoft Edge releases security updates and patches quickly to help stay ahead of security threats, such as zero-day exploits, to minimize the impact of compromise. Additionally, Microsoft Edge is built with its own unique protection features on top of Chromium and supports Microsoft Security solutions from Microsoft Defender, Microsoft Entra (formerly known as Azure Active Directory), Microsoft Intune and Microsoft Purview. Currently, Microsoft Edge for Business offers the following features that support the Zero Trust methodology:
- Microsoft Purview Data Loss Prevention (DLP)
- Microsoft Defender SmartScreen\*
- Enhanced security mode (ESM)
- Website typo protection
- Native support for Microsoft Entra Conditional Access\*
- Password Monitoring and Generator
- Microsoft Edge management service (EMS)
- Unmanaged device support with Microsoft Intune Mobile Application Management (MAM)

