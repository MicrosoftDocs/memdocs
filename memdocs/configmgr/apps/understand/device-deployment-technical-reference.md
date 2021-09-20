---
title: App deployment to device collections technical reference
titleSuffix: Configuration Manager
description: Troubleshooting application deployments to device collections technical reference for Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Application Deployment for Device Collections

*Applies to: Configuration Manager (current branch)*

When an application is deployed to a Device collection, the policy is targeted to all the devices in the collection regardless of the deployment purpose. This article explains the policy download and deployment processing on the client.

> [!TIP]
> All the information necessary to review the client logs can be obtained by running the SQL query referenced in the [Before you begin](app-deployment-technical-reference.md#before-you-begin) section.

## Policy Download

After the policy for the application deployment is targeted to the client, the client would download the policy at the next policy polling cycle. When the client downloads the policy, it downloads related policies in addition to the deployment policy. These related policies include the policy for the application, deployment type, global conditions, etc. Policy download activity can be tracked in the **PolicyAgent.log** on the client, using either the Application or Assignment Unique ID.

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

After the policies are downloaded on the client, the Scheduler component creates schedules for deployment activation and enforcement.

## Deployment Activation

Application evaluation is initiated when the deployment is activated. Scheduler component creates a schedule to activate the assignment at the Available Time configured in the deployment. This activity can be tracked in **Scheduler.log** on the client using the Application Assignment Unique ID.

- For **Required** deployments, the activation schedule is created, but has a delay of up to two hours to avoid resource contention on Site Servers and Distribution Points. The delay helps avoid contention since application content may be downloaded during evaluation if the application is applicable based on defined Requirement Rules.

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- For **Available** deployments, the activation schedule is created to be fired off at the Available Time configured in the Deployment.

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

When the schedule time arrives, Scheduler component sends the activation message to DCM Agent to perform application evaluation.

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

DCM Agent receives the activation message, and creates a job to evaluate the application.

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## Deployment Enforcement

Application installation is initiated when the deployment is enforced.

- For **Required** deployments, Scheduler creates a deadline schedule after policy is downloaded to enforce the application at deployment deadline. The deadline schedule isn't randomized by default. Randomization behavior for activation can be controlled by the [Disable deadline randomization](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization) client setting.

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    At the deadline, Scheduler component sends the deadline message to DCM Agent. 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    DCM Agent receives the deadline message, and creates a job to enforce the application.
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > For deployments with deadline in the past, the application is activated and enforced immediately by the same DCM Agent job which performs the evaluation, download and installation actions.

- For **Available** deployments, there's no deadline schedule since the enforcement occurs when the application installation is initiated by the user from Software Center. When the user starts an installation, a DCM Agent job is created to perform application evaluation, download, and installation. This activity can be tracked in **DCMAgent.log** on the client.

## Next Steps

- [Understanding application deployment client components](client-components-technical-reference.md)
