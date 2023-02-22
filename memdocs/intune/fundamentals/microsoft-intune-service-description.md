---
# required metadata

title: Microsoft Intune Service Description
description: Microsoft Intune is a cloud-based service that helps you manage Windows, iOS/iPadOS, macOS, and Android devices.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 02/04/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 40fa5a2e-6c0f-4150-9740-d5ddc0cdbda0

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: cacamp
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection:
- tier2
- M365-identity-device-management
---

# Microsoft Intune service description

Intune is a cloud-based enterprise mobility management (EMM) service that helps enable your workforce to be productive while keeping your corporate data protected. With Intune, you can:

* Manage the mobile devices your workforce uses to access company data.
* Manage the client apps your workforce uses.
* Protect your company information by helping to control the way your workforce accesses and shares it.
* Ensure devices and apps are compliant with company security requirements.

Intune integrates closely with Azure Active Directory (Azure AD) for identity and access control, and Azure Information Protection for data protection. You can also integrate it with Configuration Manager to extend your management capabilities.

To learn more about how you can manage devices, apps, and protect corporate data with Intune, see the [Intune documentation](../index.yml).

## 30-day free trial

You can start to use Intune with a 30-day free trial that includes 100 user licenses. To start your free trial, [go to the Intune Sign up page](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20). If your organization has an Enterprise Agreement or equivalent volume licensing agreement, contact your Microsoft representative to set up your free trial.

> [!NOTE]
> If your organization has a Microsoft Online Services work or school account, and you might continue with this Intune subscription in production after the trial period ends, then choose the **Sign in** option on that page and authenticate by using the Global Administrator account for your organization. This action ensures that your Intune trial links to your existing work or school account.

<!--- For a list of settings that you can set up on mobile devices, see:

- [Enrolled device management capabilities of Microsoft Intune](introduction-intune.md)

--->
## Intune Onboarding benefit

Microsoft offers the Intune Onboarding benefit for eligible services in eligible plans. The Onboarding benefit lets you work remotely with Microsoft specialists to get your Intune environment ready for use. For more about the Onboarding benefit, see [Microsoft Intune Onboarding Benefit Description](/fasttrack/introduction).

## Learn how Intune service updates affect you

Because the mobile device management ecosystem changes frequently with operating system updates and mobile app releases, Microsoft updates Intune regularly. There are three ways you can learn about changes in the Intune service:

* [What's new in Microsoft Intune](whats-new.md). This topic is updated with the monthly service update and weekly when, for example, apps such as the Company Portal app are released.

* Important service updates are also announced in the [Microsoft 365 admin center](https://admin.microsoft.com/) Message Center. If you install the companion [Microsoft 365 Admin mobile app](https://support.office.com/article/Office-365-Admin-Mobile-App-e16f6421-2a1a-4142-bf9d-9846600a060a), you can receive notifications on your mobile device. Learn more about how to work with the [Microsoft 365 Message Center](https://support.office.com/client/results?Shownav=true&ns=O365ENTADMIN&version=15&ver=15&HelpID=O365E_MCManageUpdates).

  A few helpful hints:

  * The messages in the Microsoft 365 Message Center are targeted. This means that if your company doesn't have an Intune for EDU offer, we won't message you about Intune for EDU.

  * Messages expire. For example, the notification that your service has been updated with a link to the What's New page will likely expire prior to the next service update notification. Otherwise, you'd have a large backlog of posts that may no longer be relevant.

  * The Microsoft 365 admin mobile app allows you to search through all the messages and to forward the notification if you wanted to share it with peers in your organization.

  * Under Edit message center preferences, we'll eventually have a toggle for **Intune** so you can look at those messages posted to an Intune subscription. If you see Mobile Device Management for Microsoft 365, that is a different service, not Intune.

* We also use two blogs to share the EMS message and Intune support best practices:

  * [Enterprise Mobility + Security blog](https://blogs.technet.microsoft.com/enterprisemobility/)

  * [Intune support blog](https://blogs.technet.microsoft.com/intunesupport/)

> [!NOTE]
> You can monitor Intune service health in the [Microsoft 365 admin center](https://admin.microsoft.com). Choose **Service Health** in the left pane. You can also use the [Microsoft 365 Admin mobile app](https://support.office.com/article/Office-365-Admin-Mobile-App-e16f6421-2a1a-4142-bf9d-9846600a060a) to view service health.

## Types of notices Microsoft provides about the Intune service

To help you plan for service changes, we notify you at least 7-90 days prior to the service change, depending on the impact of the change. These changes might include any of the following types of change:

- Changes to the end-user experience that you may want to share with your helpdesk staff or your end users. We provide typically 7 to 30 days notice of those changes and document them on the [What's New in Intune App UI](whats-new-app-ui.md). For something like a spelling error fix, we won't typically call out in documentation. But a change in the end-user enrollment experience is significant enough in the UI that we'll both post a message to customers in the Microsoft 365 Message center and link to the What's New in the Intune App UI so you are notified of what's changing and have time to evaluate and update your end-user guidance before the changes rolling out in production.

- Changes that require you to take action are called **Plan for Change** and typically provide about 30 days notice. In the Microsoft 365 Message Center the Category specifically says Plan for Change, and if we have an exact date for when the change is in production, we also put in an **Act By** date and that gives you a visual queue and an explanation mark.

- For most deprecations, we prefer to provide 90 days notice of that deprecation. For example, if we're no longer going to support a specific version of IE, our goal is to provide 90 days notice. However, deprecations do get complicated when it's another company announcing the deprecation. For example, a browser company provided notice that they would no longer support Silverlight with their latest build, so we let customers know we were dropping support of that browser, but our notification to customers under the 90-day period.

- In the event of Intune service retirement, you would be notified 12 months in advance.

Finally, in the rare event there's any post-incident action needed to get your service back to normal or a large change that we deem potentially disruptive based on customer feedback, we will email the service administrators based on how your [Microsoft 365 communication preferences](https://support.office.com/article/Change-your-contact-preferences-for-communications-from-Microsoft-6f70de1b-a64d-4498-bfbd-be8c83a9c0fc) are set and whether you include a valid (and preferably work) email address.  

## Language support

Intune runs in the Azure portal, which supports the following languages: Chinese (Simplified), Chinese (Traditional), Czech, Dutch, English, French, German, Hungarian, Indonesian, Italian, Japanese, Korean, Polish, Portuguese (Brazil), Portuguese (Portugal), Russian, Spanish, Swedish, and Turkish.

In addition to all the languages that the Azure portal supports, the Microsoft Intune admin center and the user-facing mobile experiences support Danish, Greek, Finnish, Norwegian, and Romanian.
