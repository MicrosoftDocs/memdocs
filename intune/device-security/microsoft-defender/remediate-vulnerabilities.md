---
title: Use Intune to remediate vulnerabilities found by Microsoft Defender for Endpoint
description: Integrate Microsoft Defender Vulnerability Management with Intune to create security tasks, track remediation, and reduce vulnerability exposure across managed devices.
ms.date: 04/08/2026
ms.topic: how-to
ms.reviewer: aanavath
ms.collection:
- M365-identity-device-management
- sub-secure-endpoints
---

# Use Microsoft Intune security tasks to remediate device vulnerabilities identified by Microsoft Defender for Endpoint

When you [integrate Microsoft Defender for Endpoint with Microsoft Intune](./configure-integration.md#connect-defender-for-endpoint-to-intune), you can use Microsoft Defender Vulnerability Management through Intune security tasks. These tasks help Intune admins understand and address current vulnerabilities based on guidance from Defender for Endpoint. This integration enhances the discovery and prioritization of vulnerabilities, improving remediation response times across your environment.

[Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management) is part of [Microsoft Defender for Endpoint](/defender-endpoint/microsoft-defender-endpoint).

## Prerequisites

**Subscriptions**:

- Intune Plan 1
- Defender for Endpoint ([Sign up for a free trial](https://www.microsoft.com/security/business/endpoint-security/microsoft-defender-endpoint).)

Intune configurations for Defender for Endpoint:

- Configure a service-to-service connection with Microsoft Defender for Endpoint, and enable the **Microsoft Intune connection** in the Microsoft Defender portal. This connection allows security admins to create Intune security tasks when submitting remediation requests. For setup instructions, see [Connect Microsoft Defender for Endpoint to Intune](./configure-integration.md#connect-defender-for-endpoint-to-intune).
- Deploy policies to onboard devices to Defender for Endpoint and enable risk assessment. See [Configure Microsoft Defender for Endpoint with Intune](./configure-integration.md).

## How integration works

After you integrate Intune with Defender for Endpoint, Defender Vulnerability Management identifies vulnerabilities on your managed devices.

In the Defender portal, [security admins can review endpoint vulnerabilities](/defender-vulnerability-management/defender-vulnerability-management#remediation-and-tracking) and create Intune security tasks for remediation. These tasks appear in the Intune admin center, where Intune admins can act and remediate issues based on Defender's guidance:

- Defender for Endpoint identifies vulnerabilities through scans and assessments.
- Not all identified vulnerabilities support remediation through Intune; only compatible vulnerabilities result in security tasks.

Security tasks identify:

- The type of vulnerability
- Priority
- Status
- Steps for remediation

Intune admins can view a security task and then choose to accept or reject it. For accepted tasks, the admin follows the guidance provided to use Intune for remediation. Once the remediation is successful, the admin sets the task to **Complete Task**, which updates its status in both Intune and Defender for Endpoint where security admins can verify the revised status of the vulnerability.

### Workflow example

The following example shows the workflow for discovering and remediating an application vulnerability:

- A Defender for Endpoint scan identifies a vulnerability in the app Contoso Media Player v4, which is an unmanaged app that isn't deployed by Intune. A security admin in the Defender portal creates an Intune security task to update the app.
- The security task appears in the Intune admin center with a status of **Pending**.
- The Intune admin views the task details and selects **Accept**, which changes the status of the task to **Accepted** in both Intune and Defender for Endpoint.
- The admin follows the remediation guidance provided. For managed apps, Intune might include instructions or links to update the app. For unmanaged apps, Intune can only provide text instructions.
- After addressing the vulnerability, the Intune admin marks the task as **Complete Task**. This action updates the status in both Intune and Defender for Endpoint, where security admins confirm the remediation is successful and complete.

### Types of security tasks

Each security task has a *Remediation Type*:

- **Application**: For example, Defender for Endpoint finds a vulnerability in an app like *Contoso Media Player v4*. An admin creates a task to update the app, which might involve applying a security update or installing a new version.
- **Configuration**: For instance, if devices lack protection from *Potentially Unwanted Applications* (PUA), an admin creates a task to configure the setting in the Microsoft Defender Antivirus profile.

When Intune doesn't support implementation of a suitable remediation, Defender for Endpoint doesn't create a security task.

### Remediation actions

Common security task remediations include:

- **Block** an application from running.
- **Deploy** an operating system update to mitigate the vulnerability.
- **Deploy** endpoint security policy to mitigate the vulnerability.
- **Modify** a registry value.
- **Disable** or **Enable** a configuration to affect the vulnerability.
- **Require Attention**, which alerts the admin when no suitable recommendation is available.

## Work with security tasks

Before you can manage security tasks in the Intune admin center, a security admin must first create them in the Defender portal. Security admins create tasks by submitting remediation requests through Defender Vulnerability Management. For instructions, see [Remediate vulnerabilities with Microsoft Defender Vulnerability Management](/defender-vulnerability-management/tvm-remediation#request-remediation) in the Defender documentation.

[!INCLUDE [manage-admin-tasks](../../includes/manage-admin-tasks.md)]

To manage security tasks:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Security tasks**.
3. Choose a security task to view its details. In the task window, you can select additional links, including:
   - MANAGED APPS - View the app that's vulnerable. When the vulnerability applies to multiple apps, Intune displays a filtered list of apps.
   - DEVICES - View a list of the *Vulnerable devices* from which you can link through to an entry with more details for the vulnerability on that device.
   - REQUESTOR - Use the link to send mail to the admin who submitted this security task.
   - NOTES - Read custom messages submitted by the requestor when opening the security task.

4. Select **Accept** or **Reject** to send notification to Defender for Endpoint for your planned action. When you accept or reject a task, you can submit notes, which are sent to Defender for Endpoint.

5. After accepting a task, reopen the security task (if it closed), and follow the REMEDIATION details to remediate the vulnerability. The instructions provided by Defender for Endpoint in the security task details vary depending on the vulnerability involved.

6. After completing the remediation steps, open the security task and select **Complete Task**. This action updates the security task status in both Intune and Defender for Endpoint.

> [!NOTE]
> Each remediation request in Defender for Endpoint is [limited to 10,000 devices](/defender-vulnerability-management/tvm-remediation#remediation-request-steps). If a vulnerability affects more devices, the resulting security task in Intune covers only 10,000 of them.

Successful remediation can reduce the risk exposure score in Defender for Endpoint based on subsequent status updates from the remediated devices. You can [monitor these risk levels](./monitor.md) to track compliance improvements over time.

## Troubleshooting

If security tasks don't appear in Intune:

- Verify the Intune connection is enabled in the Defender portal.
- Confirm devices are onboarded to Defender for Endpoint.
- Check that security admins create tasks for vulnerabilities that Intune can remediate.
- Allow time for task synchronization between portals.

## Next steps

- [Set up the integration](./overview.md) - Complete prerequisites and connect services.
- [Monitor compliance for risk levels](./monitor.md) - Track device risk scores.
- [Review Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management) - Understand security recommendations.
- [Learn about Mobile Threat Defense](../mobile-threat-defense/overview.md) - Explore other threat protection options for Intune.
