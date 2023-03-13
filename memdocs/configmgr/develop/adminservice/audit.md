---
title: How to view authorization failure message in administration service
titleSuffix: Configuration Manager
description: Learn how to audit authorization failure message in administration service.
ms.date: 03/30/2023
ms.prod: configuration-manager
ms.topic: how-to
author: Banreet
ms.author: banreetkaur
manager: sunitashaw
---

# How to view authorization failure message in administration service.

*Applies to version 2303 or later.*

You can view audit messages about authorization failure in admin service along with request details and status messages. 

These messages are shown in 'All Status Message' at 'Status Message Queries' in 'Monitoring' ribbon. Previously these failures were logged in log files.

With the audit messages we intend to avoid inconvenience of log files rollback. Details about the user, resource access attempts and the number of attempts for all the authorized requests made by user in a day are available. You can also audit read operations for HTTPS requests and for cloud-initiated operations. This is to help admins to scope permission and roles of users while also determining if there are any malicious users.

> [!NOTE]
> All unauthorized requests are aggregated for 24 hours before being sent to the status message viewer. The status message viewer includes a count of the total number of unauthorized requests received by administration service a day before.

## Steps to view the audit messages: 
- Navigate to Monitoring on the console.
- Select Status Message Queries in the System Status Folder.
- From the list of all queries, right click on the "All Status Messages" query.
- From the pop up, click on Show Messages.

:::image type="content" source="media/13022894-audit-admin-service-show-messages.png" alt-text="Pop up with Show messages option":::

- Select the duration of status messages from the “All Status Messages” pop-up window.

:::image type="content" source="media/13022894-audit-admin-service-duration-of-status-messages.png" alt-text="Wizard showing option to select duration of status message":::

- After clicking the OK button all the messages will be shown in Status Messages viewer
- You can then filter messages related to only Unauthorized Users. 
- Click on funnel icon on top bar to show "Filter Status Message" popup.
- In Filter Status Messages popup fill Message ID as **11618**

:::image type="content" source="media/13022894-audit-admin-service-filter-status-message.png" alt-text="Wizard showing option to filter status messages.":::

- All the messages related to unauthorized users request will be filtered out with message description. Details about the user and their action will be shown.

:::image type="content" source="media/13022894-audit-admin-service-show-filtered-messages.png" alt-text="Wizard showing filtered status messages.":::
