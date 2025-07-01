---
# required metadata

title: Explorer in Microsoft Intune queries data and shows Copilot recommendations
description: In Microsoft Intune, use Explorer to query your data in natural language and run built-in queries that match your request. Copilot summarizes the results, and provides recommendations and actions based on the query results. You can also create policies that target users and groups in the query results. Use this feature to explore your Intune data, troubleshoot issues, and create custom reports.
keywords: Security Copilot, Intune, Microsoft Intune, AI, Copilot, explorer, query, data exploration, natural language
author: MandiOhlinger
ms.author: mandia
manager: laurawi
ms.date: 06/30/2025
ms.topic: get-started
ms.service: microsoft-intune
ms.subservice:
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: rashok
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
- security-copilot
- msec-ai-copilot
---

# Explore Intune data and get Microsoft Copilot recommendations

Using natural language and your own words, you can query and explore your Intune data. An intelligent search matches your request to available query views that are built into Intune.

These queries can have parameter inputs that you enter, like the platform or device-specific info. Microsoft Copilot in Intune summarizes the query results and recommends actions you can take based on the query results.

This feature can help with situations like finding devices based on your query, identifying users with compliance issues, or finding devices that need updates. You can use this data to help troubleshoot.

You can also use the query output to add users or devices to groups, and create custom reports. For example, you can find devices that are noncompliant and out of the grace period, and then add those devices to a group. You can then target apps and policies to this group.

## Before you begin

- To use explorer:

  - Security Copilot must be enabled in your tenant.
  - Sign into the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with an account that has the **Copilot owner** or **Copilot contributor**.

  To learn more about the prerequisites for using Microsoft Copilot in Intune, see [Microsoft Copilot in Intune overview](copilot-intune-overview.md).

- The data you see is scoped to your Intune permissions. If you don't have permissions to view a resource, then it isn't included in the results.

## Explore your data

The best way to explore is to ask your specific questions in natural language. The intelligent search features built into Intune find results and Copilot can make suggestions based on your data.

There are also built-in examples that help you understand the kinds of questions you can ask. You can explore your data by asking about the relationships between devices, users, apps, policies, updates, and compliance. Your search is matched to available query views, with more queries continually being added.

### Start exploring

1. **Open Explorer**.

    In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Explorer**. When it opens, you see a prompt.

    :::image type="content" source="./media/copilot-intune-explorer/admin-center-explorer.png" alt-text="Select the Copilot Explorer in the Microsoft Intune admin center." lightbox="./media/copilot-intune-explorer/admin-center-explorer.png":::

2. **Type a request in natural language**.

    In the prompt box, type your request in natural language. When you start typing, a drop-down list of prompts similar to your text is shown. These prompts are built into Intune and list the kinds of questions you can ask. Select the prompt that best matches your request, or continue typing for more suggestions.

    For example, start typing `what are the top 5 apps`. As you type, a list of suggestions is shown.

    :::image type="content" source="./media/copilot-intune-explorer/explorer-prompt-apps-example.png" alt-text="Sample prompt in Copilot Explorer that asks about the top five apps in the Microsoft Intune admin center." lightbox="./media/copilot-intune-explorer/explorer-prompt-apps-example.png":::

    You can ask about devices, device updates, apps, app configuration, app protection, configuration policies, and compliance.

3. **Use the built-in examples**.

    There are also built-in examples that you can use and filter by category to find an example that best matches your request.

    :::image type="content" source="./media/copilot-intune-explorer/explorer-prompt-categories.png" alt-text="Select a Copilot Explorer example or filter the example list by the category in the Microsoft Intune admin center.":::

    The examples include parameter inputs that you enter. For example, if you select the **Compliance** category, there's a list of queries related to compliance. You can select one of the examples, like **Get *platform* devices that are noncompliant..**. In the prompt, select a platform, like **Windows**. The prompt is updated to show the platform.

    :::image type="content" source="./media/copilot-intune-explorer/explorer-example-compliance-category-platform.png" alt-text="In Copilot Explorer, select the compliance example and select the Windows platform in the Microsoft Intune admin center.":::

4. **Get results**.

    The **Get results** button runs your query. Copilot summarizes and helps you understand the results, suggests other queries that could help, and recommends actions you can take based on the query results.

    :::image type="content" source="./media/copilot-intune-explorer/explorer-copilot-summary.png" alt-text="In Copilot Explorer, the Copilot Summary summarizes the query results, and shows suggestions and actions in the Microsoft Intune admin center.":::

5. **Take action**.

    In the query results, you can export the results and select an item to get more information. If your query results are a list of users or devices, you can add them to a group, and target apps and policies to this group.

    :::image type="content" source="./media/copilot-intune-explorer/explorer-query-results.png" alt-text="In the Copilot Explorer, you can export the query results and add users or devices to groups in the Microsoft Intune admin center.":::

    You can select an existing group or create a new group. When finished, a progress report is automatically created. If you want to keep the report, export it now, as the report isn't available again.

    In the following example, a query found noncompliant devices that are out of the grace period. These devices are added to a group. Some devices failed to be added to the group, and the report shows the reason why. You can use the **Add filters** option to filter the results, like the devices that were successfully added to the group.

    :::image type="content" source="./media/copilot-intune-explorer/explorer-add-to-group-report.png" alt-text="In the Copilot Explorer, you can export the query results and add users or devices to groups in the Microsoft Intune admin center.":::

## Feedback and the future

Explorer is constantly improving. We continue to add more queries, more querying capabilities, more Intune data sources, and more actions. We want your feedback, including any capabilities you want to see and missing queries that you need.

:::image type="content" source="./media/copilot-intune-explorer/explorer-provide-feedback.png" alt-text="Submit feedback about Copilot Explorer in the Microsoft Intune admin center." lightbox="./media/copilot-intune-explorer/explorer-provide-feedback.png":::

## Related content

- [Use Microsoft Copilot in Intune to troubleshoot ](copilot-devices.md).
- [Use the settings catalog to create device configuration policies](../configuration/settings-catalog.md).
- [Learn about privacy and data security in Security Copilot](security-copilot.md#privacy-and-data-security-in-security-copilot).
