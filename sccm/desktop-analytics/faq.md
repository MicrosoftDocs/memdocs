---
title: FAQ for Desktop Analytics
titleSuffix: Configuration Manager
description: Frequently asked questions for Desktop Analytics.
ms.date: 10/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Desktop Analytics FAQ

## Prerequisites

### <a name="bkmk_intune"></a> Can I use Desktop Analytics with Intune-managed devices? 

The vast majority of customers that can benefit from the Desktop Analytics workflow use Configuration Manager to deploy Windows. We know Intune customers love the additional insights from Analytics data, and we're working on ways to share insights with them as well.

### It's been over 72 hours and the portal is still processing data, what next? 

When you first set up Desktop Analytics, the reports in Configuration Manager and the Desktop Analytics portal may not show complete data right away. It can take 2-3 days for the service to process the data. If it's been over 72 hours, and the portal is still processing data, follow these steps:

- To confirm that active devices are properly configured, use the [Connection Health dashboard](/sccm/desktop-analytics/monitor-connection-health). This dashboard doesn't update in real time.
- Make sure devices are sending diagnostic data to the Desktop Analytics service. For more information, see [Enable data sharing](/sccm/desktop-analytics/enable-data-sharing).
- Provision [Azure AD applications](/sccm/desktop-analytics/troubleshooting#bkmk_AzureADApps) on your Azure AD.
- Check devices that you've associated with your organization in the last seven days. In the [Desktop Analytics portal](https://aka.ms/desktopanalytics), go to the **Connected services** pane. Select **Enroll devices**, and **View recent data**

If devices are properly configured, and you're still not seeing data in your workspace, [contact Microsoft support](https://support.microsoft.com/hub/4343728/support-for-business).

## Connect Configuration Manager

### Can I change the target or additional collections?

Yes, use the following process:

- In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node. Open the properties for the entry associated with your Desktop Analytics service.

- On the **Desktop Analtyics Connection** tab, change the **Target Collection** or manage the additional collections.

> [!IMPORTANT]  
> Configuration Manager uses a settings policy to configure devices in the target collection. This policy includes the diagnostic data settings to enable devices to send data to Microsoft. Changing the target collection doesn't undo the settings policy on devices no longer in the target collection. If you don't want your devices to continue sending diagnostic data, [reconfigure the devices](/sccm/desktop-analytics/account-close#reconfigure-clients).

## Windows upgrade

### Can I upgrade Windows and change architecture?

Desktop Analytics is designed to best support in-place upgrades. In-place upgrades don't support migrations from 32-bit to 64-bit architecture. If you need to migrate computers in this scenario, use the refresh scenario. Desktop Analytics insights are still valuable in this scenario, but you can ignore upgrade-specific guidance.

For more information, see [Refresh an existing computer with a new version of Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).

### Can I change from BIOS to UEFI when upgrading Windows?

Yes. For more information, see [Convert from BIOS to UEFI during an in-place upgrade](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### Can I use Desktop Analytics with Windows 10 LTSC?

While you can use Desktop Analytics to assist with updating devices from Windows 10 Long-Term Servicing Channel (LTSC) to Windows 10 Semi-Annual Channel, Desktop Analytics doesn't support updates to Windows 10 LTSC. This channel of Windows 10 isn't intended for broad use, and doesn't receive feature updates, so it's not a supported target with Desktop Analytics. For more information, see [Windows as a service overview](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

### Can I reduce the amount of time it takes for data to refresh in my Desktop Analytics portal?

There are two types of data in the Desktop Analytics portal: Administrator data and diagnostic data. To refresh administrator data on-demand, open the data currency flyout and select **Apply changes**. This action immediately triggers a one-time refresh of any pending administrator changes in your workspaces. The changes propagate and are generally available within 15-60 minutes. The timing depends on the size of your workspace and the scope of pending changes. You can request an on-demand data refresh up to six times within a 24-hour period.

All data is updated automatically once daily, even if you don't request an on-demand data refresh. There's no way to trigger an on-demand refresh of diagnostic data. For more information about the different types of data in Desktop Analytics, see [Data latency](/sccm/desktop-analytics/troubleshooting#data-latency).

## Privacy

### Can Desktop Analytics be used without a direct client connection to the Microsoft Data Management Service?

No, the entire service is powered by Windows diagnostic data, which requires that devices have this direct connectivity.

### Can I choose the data center location?

For Azure Log Analytics: Yes, when you set up Desktop Analytics and create the Log Analytics workspace.

For the Microsoft Data Management Service and Analytics Azure Storage: No, these two services are hosted in the United States.

### Where is my organization's data stored?

Windows diagnostic data from your computers is encrypted, sent to, and processed at Microsoft-managed secure data centers located in the United States. Our analysis of the Desktop Analytics-related data is then provided to you through the Desktop Analytics solution in the Azure portal. Desktop Analytics is supported in all Azure regions. Selecting an international Azure region doesn't prevent diagnostic data from being sent to and processed in Microsoft's secure data centers in the US.

## Existing Windows Analytics customers

### Can I migrate inputs from Windows Analytics?

Yes, when you set an existing Windows Analytics workspace as Desktop Analytics workspace during [Initial onboarding](/sccm/desktop-analytics/set-up#initial-onboarding). If you create a new workspace, or select one that's not a Windows Analytics workspace, Desktop Analytics doesn't migrate your inputs.

#### Migration scope

| Input type | Will migrate? |
|------------|---------------|
| Importance | Yes |
| App owner | Yes |
| Upgrade decision | No |
| Test plan | No |
| Test result | No |

#### Importance mapping

| Windows Analytics | Desktop Analytics |
|-------------------| ------------------|
| Low install count | (Not applicable) <br> Note: Desktop Analytics runs its own heuristic to determine Low install count |
| Not reviewed | Not Reviewed |
| Review in progress | Not Reviewed |
| Mission critical | Critical |
| Business critical | Critical |
| Important | Important |
| Best effort | Important |
| Ignore | Not Important |

### Can I migrate from multiple Windows Analytics workspaces?

No, you can only select one Windows Analytics workspace from which to migrate inputs. If you own multiple Windows Analytics workspaces, select one that best benefits your organization.

### I've chosen to migrate, where can I find the inputs on Desktop Analytics?

Once devices are enrolled, to see the migrated inputs in the Desktop Analytics portal, go to **Manage > Assets > Apps**.

### When can I see my migrated inputs?

The migration process is transactional. You'll see either all inputs migrated without corruption, or no migrated inputs at all. If you don't see the migrated inputs in 24 hours, contact Microsoft Support. Start tagging apps as you see the migrated inputs. If you've already tagged some apps, Desktop Analytics keeps those inputs in case they conflict with the inputs from Windows Analytics.

### How long do I have to migrate my data?

Windows Analytics Upgrade Readiness solution is being [retired on January 31st, 2020](https://http://aka.ms/waretirement). After that, based on the Log Analytics workspace retention policy, data will go away over time, so customers willing to keep data will need to migrate or export before that happens.

### Can I migrate after the initial onboarding?

Yes.<!-- 5202803 -->  Existing Windows Analytics customers can now migrate data afteras long as they set an existing Widnows Analytics worksapce as Desktop Analytics worskspace during [Initial onboarding](/sccm/desktop-analytics/set-up#initial-onboarding). Go to **Connected services** in the Desktop Analytics portal, and select the option to migrate data from Windows Analytics.

### Can I use Update Compliance together with Desktop Analytics?

Yes. If you use [Update Compliance](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started) in the Azure portal today, you can continue to do so now and beyond January 2020.

For more information, see [KB 4521815: Windows Analytics retirement on January 31, 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### Are there any Windows Analytics features that aren't available in Desktop Analytics?

<!-- 3616924 -->
Yes, the following Windows Analytics features will either be retired or aren't yet available in Desktop Analytics:

#### General

- Support for scenarios that don't require Configuration Manager. For example, [Intune support](#bkmk_intune).
- Licensing prerequisite of any valid Windows license versus E3, E5
- Support for multiple workspaces per Azure AD tenant
- Ability to run custom queries and export raw solution data
- Data model documentation for custom reports

#### Upgrade Readiness

- Internet Explorer Site Discovery data
- Office add-in insights (now [available in Configuration Manager](#bkmk_office))
- Feedback Hub insights

#### Update Compliance

- Support for Windows Update for Business
- Delivery Optimization insights
- Support for Windows 10 long-term servicing channel (LTSC)
- Windows Insider reports
- Windows Defender status

> [!Note]
> All existing Update Compliance features, including those not available in Desktop Analytics, remain available in the [Update Compliance](/windows/deployment/update/update-compliance-get-started) solution in the Azure portal.

#### Device Health

- Driver health
- App health (outside of a deployment plan)
- Frequently crashing devices or driver-induced crashes
- Windows sign-in health
- Windows Information Protection
- Support for Windows Server

## Other

### <a name="bkmk_office"></a> Can I use Desktop Analytics for my Office 365 ProPlus upgrades?

No, Desktop Analytics is focused on Windows. Microsoft developed Desktop Analytics in close collaboration with many customers. Customer feedback is about how Desktop Analytics improves their ability to confidently manage Windows deployments. They also tell us they want [Office 365 ProPlus readiness](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness) more closely integrated with Office management tools in Configuration Manager and Intune. Microsoft continues to invest in those areas, while focusing on Windows scenarios in Desktop Analytics.

### How can I provide feedback about Desktop Analytics?

To share your feedback about Desktop Analytics, select the **Send a Smile** icon at the top of the portal. Include a screenshot with your submission to help Microsoft better understand your feedback. You can also submit product suggestions and upvote other ideas on [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805).

> [!Note]
> Never share private information via Send a Smile or UserVoice. Such private information includes your Tenant Id or Commercial Id. Microsoft doesn't provide support via the Send a Smile or UserVoice channels. To get help with your Desktop Analytics workspace, select the **Help and Support** link in the navigation menu to open a support ticket.
