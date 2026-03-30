---
title: Microsoft Intune Service Description
description: Microsoft Intune is a cloud-based service that helps you manage Windows, iOS/iPadOS, macOS, and Android devices.
author: MandiOhlinger
ms.author: mandia
ms.date: 02/03/2026
ms.topic: article
ms.reviewer: mmikkelson, cacamp
ms.collection:
- M365-identity-device-management
- triage
---

# Microsoft Intune service description

Intune is a cloud-based endpoint management service that helps you manage and secure your organization's devices, apps, and data. By using Intune, you can:

* Manage the mobile devices your workforce uses to access organization data.
* Manage the client apps your workforce uses, including Microsoft 365 apps and many third-party partner apps.
* Protect your organization information and data by managing the way your workforce accesses and shares it.
* Ensure devices and apps are compliant with organization security requirements.

Intune integrates closely with Microsoft Entra ID for identity and access control, and native and partner services for data & endpoint protection. You can also integrate Intune with Configuration Manager to extend your management capabilities.

To learn more about how you can manage devices, apps, and protect corporate data with Intune, see [Microsoft Intune securely manages identities, apps, and devices](what-is-intune.md).

## 30-day free trial

You can start to use Intune with a 30-day free trial. To start your free trial, [go to the Intune Sign up page](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20). If your organization has an Enterprise Agreement or equivalent volume licensing agreement, contact your Microsoft representative to set up your free trial.

If your organization has a Microsoft Online Services work or school account, and you might continue with this Intune subscription in production after the trial period ends, select the **Sign in** option on that page and authenticate by using the Microsoft Entra Global Administrator account for your organization. This action ensures that your Intune trial links to your existing work or school account.

> [!IMPORTANT]
> [!INCLUDE [global-admin](../includes/global-admin.md)]

## Intune Onboarding benefit

Microsoft offers the Intune Onboarding benefit for eligible services in eligible plans. The Onboarding benefit lets you work remotely with Microsoft specialists to get your Intune environment ready for use. For more about this benefit, see [Microsoft Intune Onboarding Benefit Description](/microsoft-365/fasttrack/introduction).

## Learn how Intune service updates affect you

Because the mobile device management ecosystem changes frequently with operating system updates and mobile app releases, Microsoft regularly updates Intune. You can learn about changes in the Intune service through the following sources:

* [What's new in Microsoft Intune](whats-new.md) is updated monthly and can be updated weekly when, for example, apps such as the Company Portal app are updated.

* The [Microsoft Intune admin center](https://intune.microsoft.com) and the [Microsoft 365 admin center](https://admin.microsoft.com/) message centers announce service change notices and service health notices, including any issues in your environment that require action.

  - [**Microsoft 365 admin center**](https://admin.microsoft.com) Message Center notices are shown at **Health** > **Message center**.
  - [**Microsoft Intune admin center**](https://intune.microsoft.com) notices are shown at **Tenant administration** > **Tenant status** > **Service health and message center**.

  A few helpful hints:

  * The messages are typically targeted. So, if your organization doesn't have an Intune for Education offer, you won't receive messages about Intune for Education.

  * Messages expire. For example, the notification that your service is updated with a link to the What's new page likely expires before the next service update notification. Otherwise, you'd have a large backlog of posts that might no longer be relevant.

  * Install the [Microsoft 365 Admin mobile app](/microsoft-365/admin/admin-overview/admin-mobile-app) to receive notifications on your mobile device. You can search through all the messages and forward the notification to share it with others in your organization.

    * Under **Edit message center preferences**, you might see an **Intune** toggle so you can look at those messages posted to an Intune subscription. If you see **Mobile Device Management for Microsoft 365**, that service is different, not Intune.

    * Learn more about how to work with the [Microsoft 365 Message Center](/microsoft-365/admin/manage/message-center).

* The following blogs share new features, capabilities, and best practices for Microsoft Intune:

  * [Microsoft Intune Blog](https://aka.ms/IntuneBlog)
  * [Intune Customer Success Blog](https://aka.ms/IntuneCustomerSuccess)

> [!NOTE]
> You can monitor Intune service health in the [Microsoft 365 admin center](https://admin.microsoft.com). Choose **Service Health** in the left pane. You can also use the [Microsoft 365 Admin mobile app](/microsoft-365/admin/admin-overview/admin-mobile-app) to view service health.

## Types of notices Microsoft provides about the Intune service

To help you plan for service changes, Microsoft notifies you at least 7-90 days prior to the service change, depending on the impact of the change. These changes might include any of the following types of change:

- Changes to the end-user experience that you might want to share with your helpdesk staff or your end users. Microsoft typically provides 7 to 30 days' notice of those changes. For something like a spelling error fix, Microsoft typically doesn't call out the change in documentation. For a change in the end-user enrollment experience that's significant enough in the UI, Microsoft posts a message to customers. So, you're notified of what's changing and have time to evaluate and update your end-user guidance before the changes roll out in production.

  Changes that require you to take action are called **Plan for Change** and typically provide about 30 days' notice. In the Intune and Microsoft 365 message centers, the category specifically says **Plan for Change**. If Microsoft has an exact date for when the change is in production, there's an **Act By** date. That date gives you a visual queue and an explanation mark.

- For most deprecations, Microsoft prefers to provide 90 days' notice of that deprecation. For example, if Microsoft is no longer going to support a feature, the goal is to provide 90 days' notice. Deprecations get complicated when it's another company announcing the deprecation. So, Microsoft lets customers know we're removing support as soon as possible, but the Microsoft notification to customers might be under the 90-day period.

- In the event of Intune service retirement, you are notified 12 months in advance.

- In the rare event there's any post-incident action needed to get your service back to normal or a large change that Microsoft deems potentially disruptive based on customer feedback, Microsoft emails the service administrators using your [Microsoft 365 communication preferences](/microsoft-365/admin/manage/change-address-contact-and-more). Be sure your preferences include a valid work email address.

## Language support

Intune runs in the Azure portal, which supports the following languages: Chinese (Simplified), Chinese (Traditional), Czech, Dutch, English, French, German, Hungarian, Indonesian, Italian, Japanese, Korean, Polish, Portuguese (Brazil), Portuguese (Portugal), Russian, Spanish, Swedish, and Turkish.

In addition to all the languages that the Azure portal supports, the Microsoft Intune admin center and the user-facing mobile experiences support Danish, Greek, Finnish, Norwegian, and Romanian.

## Related content

- [Service information for Microsoft Intune release updates](intune-service-servicing-information.md)
- [What is Microsoft Intune](what-is-intune.md)
