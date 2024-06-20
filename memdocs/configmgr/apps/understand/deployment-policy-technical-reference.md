---
title: Application deployment policy technical reference
titleSuffix: Configuration Manager
description: Troubleshooting application deployment policies technical reference for Configuration Manager.
ms.date: 11/04/2019
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: troubleshooting
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Application Deployment Policy

*Applies to: Configuration Manager (current branch)*

## Policy Creation

When you deploy an application, an instance of [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md) class is created which represents the assignment of an application to a collection. This activity can be tracked in the **SMSProv.log**.

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

In the Configuration Manager database, this information is stored in the `CI_CIAssignments` table where `AssignmentType` 2 represents an application deployment. When the assignment is created, SMS Database Monitor component detects a change in the table then notifies Object Replication Manager to process the CI Assignment (CIA) policy. Object Replication Manager component then creates the policy for the application assignment in the database, which is stored in the `Policy` table in the database, and the Policy ID is based on the Application Unique ID. This activity can be tracked in the **objreplmgr.log** by referencing the Assignment Unique ID, which can be obtained from the SQL query referenced in the [Before You Begin](app-deployment-technical-reference.md#before-you-begin) section.

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

The policy for the application assignment can be seen in the database using a SQL query similar to below.

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## Policy Targeting

After the policy is generated, the Policy Provider component assigns this policy to the resources in the collection that's targeted by the application deployment. The policy targeting information is stored in the `ResPolicyMap` table in the database. You can use the PADBID returned by the above query to track this activity in **policypv.log**. However, the PADBID recorded in the log may not always match the PADBID returned by the above query if multiple policies are getting processed simultaneously.

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> `ResPolicyMap` table does not contain any targeting information for applications that are deployed as **Available** to User collections. Software Center queries a list of these applications from the Management Point, and policy targeting information for these applications is generated dynamically when a user requests an application from Software Center.

## Next Steps

- [Application Deployment to Device Collections](device-deployment-technical-reference.md)
- [Application Deployment to User Collections](user-deployment-technical-reference.md)
