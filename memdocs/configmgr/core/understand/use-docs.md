---
title: How to use the docs
titleSuffix: Configuration Manager
description: Learn tips on using the Configuration Manager technical documentation library.
ms.date: 04/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to use the Configuration Manager docs

*Applies to: Configuration Manager (current branch)*

This article provides resources and tips for using the Configuration Manager documentation library.

- How to search
- Submitting doc bugs, enhancements, questions and new ideas
- How to get notified of changes
- How to contribute to docs

For general help with the product, see [Find help](find-help.md).

## <a name="bkmk_searchtips"></a> Search

Use the following search tips to help you find the information that you need:

- When using your preferred search engine to locate content for Configuration Manager, include `ConfigMgr` along with your search keywords.

  - Look for results from `docs.microsoft.com/mem/configmgr` for Configuration Manager current branch. Results from `docs.microsoft.com/previous-versions` are for older product versions.

  - To further focus the search results to the current content library, include `site:docs.microsoft.com` to scope the search engine.

- Use search terms that match terminology in the user interface and online documentation. Avoid unofficial terms or abbreviations that you might see in community content. For example, search for:

  - "management point" rather than "MP"
  - "deployment type" rather than "DT"
  - "software updates" rather than "SUM"

- To search within the current article, use your browser's **Find** feature. With most modern web browsers, press **Ctrl**+**F** and then enter your search terms.

- Each article on `docs.microsoft.com` includes the following fields to assist with searching the content:

  - **Search** in the upper right corner. To search all articles, enter terms in this field. Articles in the Configuration Manager library automatically include the `ConfigMgr` scope to only search this documentation library.

  - **Filter by title** above the left table of contents. To search the current table of contents, enter terms in this field. This field only matches terms that appear in the article titles for the current node. For example, **Core Infrastructure** (`docs.microsoft.com/configmgr/core`) or **Application Management** (`docs.microsoft.com/configmgr/apps`).

- Having problems finding something? [File feedback!](#bkmk_docfeedback) When filing the issue, provide the search engine you're using, the keywords you tried, and the target article. This feedback helps Microsoft optimize the content for better search.

> [!TIP]
> Starting in Configuration Manager version 1902, there's a **Documentation** node in the new **Community** workspace of the Configuration Manager console. This node includes up-to-date information about Configuration Manager documentation and support articles. For more information, see [Using the Configuration Manager console](../servers/manage/admin-console.md#bkmk_doc-dashboard).

## <a name="bkmk_docfeedback"></a> Feedback

Select the **Feedback** link in the upper right of any article to go to the Feedback section at the bottom. This section integrates with GitHub Issues. For more information about integration with GitHub Issues, see the [docs platform blog post](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs).

To share feedback on the Configuration Manager product itself, select **Product feedback**. For more information, see [Product feedback](find-help.md#product-feedback).

A [GitHub account](https://github.com/join) is a prerequisite for providing documentation feedback. Once you sign in, there's a one-time authorization for the MicrosoftDocs organization. Then when you select **Content feedback**, enter a title and comment, and then **Submit feedback**. This action files a new issue for the target article in the [SCCMdocs repository](https://github.com/MicrosoftDocs/SCCMdocs/issues).

This integration also displays any existing open or closed issues for the target article. If any exist, review them before submitting a new issue. If you find a related issue, select the face icon to add a reaction, or you can expand it to add a comment.

#### Types of feedback

Use GitHub Issues to submit the following types of feedback:

- Doc bug: The content is out of date, unclear, confusing, or broken.
- Doc enhancement: A suggestion to improve the article.
- Doc question: You need help with finding existing documentation.
- Doc idea: A suggestion for a new article. Use this method instead of UserVoice for documentation feedback.
- Kudos: Positive feedback about a helpful or informative article!
- Localization: Feedback about content translation.
- Search engine optimization (SEO): Feedback about problems searching for content. Include the search engine, keywords, and target article in the comments.

If you create an issue for non-doc-related topics, Microsoft will close the issues. For example:

- [Product feedback](find-help.md#product-feedback)
- [Product questions](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)
- [Support requests](https://aka.ms/cmcbsupport)

To share feedback on the fundamental docs.microsoft.com platform, see [Docs feedback](https://aka.ms/sitefeedback). The platform includes all of the wrapper components such as the header, table of contents, and right menu. Also how the articles render in the browser, such as the font, alert boxes, and page anchors.

## <a name="bkmk_notifications"></a> Notifications

To receive notifications when content changes in the documentation library, use the following steps:

1. Use the [docs search](https://docs.microsoft.com/search/index?scope=ConfigMgr) to find an article or set of articles. For example:

    - Search for a single article by title, ["Log files for troubleshooting - Configuration Manager"](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr)

    - Search for any article about [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr)

2. In the upper right corner, select the **RSS** link.

3. Use this feed in any RSS application to receive notifications when there's a change to any of the search results.

> [!TIP]
> You can also **Watch** the [SCCMdocs repository](https://github.com/MicrosoftDocs/SCCMdocs) on GitHub. This method generates many notifications. It also doesn't include changes from a private repository used by Microsoft.

## <a name="bkmk_contribute"></a> Contribute

The Configuration Manager documentation library, like most content on docs.microsoft.com, is open-sourced on GitHub. This library accepts and encourages community contributions. For more information on how to get started, see the [Contributor Guide](https://docs.microsoft.com/contribute). The only prerequisite is to create a [GitHub account](https://github.com/join).

### Basic steps to contribute to SCCMdocs

1. From the target article, select **Edit**. This action opens the source file in GitHub.

2. To edit the source file, select the pencil icon.

3. Make changes in the markdown source. For more information, see [How to use Markdown for writing Docs](https://docs.microsoft.com/contribute/markdown-reference).

4. In the Propose file change section, enter the public commit comment describing *what* you changed. Then select **Propose file change**.

5. Scroll down and verify the changes you made. Select **Create pull request** to open the form. Describe *why* you made this change. Tag the article author and request that they review. Select **Create pull request**.

### What to contribute

If you want to contribute, but don't know where to start, see the following suggestions:

- Search the list of issues for the community-targeted labels:

  - [good-first-issue](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)
  - [help-wanted](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Microsoft authors assign these labels to issues that are good candidates for community contribution.

- Review an article for accuracy. Then update the **ms.date** metadata using `mm/dd/yyyy` format. This contribution helps keep the content fresh.

- Add clarifications, examples, or guidance based on your experience. This contribution uses the power of the community to share knowledge.

- Correct translations in a non-English language. This contribution improves the usability of localized content.

> [!NOTE]
> Large contributions require signing a Contribution License Agreement (CLA) if you aren't a Microsoft employee. GitHub automatically requires you to sign this agreement when a contribution meets the threshold.

### Tips

Follow these general guidelines when you contribute to Configuration Manager docs:

- Don't surprise us with large pull requests. Instead, [file an issue](#bkmk_docfeedback) and start a discussion. Then we can agree on a direction before you invest a large amount of time.

- Read the [Microsoft style guide](https://aka.ms/MicrosoftStyle). Know the [Top 10 tips for Microsoft style and voice](https://docs.microsoft.com/style-guide/top-10-tips-style-voice).

- Use the [pull request template](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md) as the starting point of your work.

- Follow the [GitHub Flow workflow](https://guides.github.com/introduction/flow/).

- Blog and tweet (or whatever) about your contributions, frequently!

(This list was borrowed from the [.NET contributing guide](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts).)

## Consolidation of documentation for Microsoft Endpoint Manager

To better support combined scenarios for Intune and Configuration Manager, their documentation libraries are consolidated on the [Microsoft Endpoint Manager site](https://docs.microsoft.com/mem). The Intune documentation is now at [docs.microsoft.com/mem/intune](https://docs.microsoft.com/mem/intune), and the Configuration Manager documentation is now at [docs.microsoft.com/mem/configmgr](https://docs.microsoft.com/mem/configmgr). If you still use an old URL, it will automatically redirect, so you don't need to make any changes for reading this content.

If you provide feedback or contribute to articles, some changes will be necessary:

- Existing GitHub issues remain in the original repository, [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs/issues) or [SCCMDocs](https://github.com/MicrosoftDocs/SCCMDocs/issues).

  - These issues won't show as open or closed issues in the Feedback section of the linked article.

  - We'll continue to work towards resolving these issues.

  - In some instances, we may make the tough decision to close an issue that we don't think we can address.

  - If you have an issue in the existing repository, and are passionate about it, file feedback on the migrated article in the [MEMDocs repository](https://github.com/MicrosoftDocs/MEMDocs).

- Now when you file feedback or edit an article, the issue or pull request goes to the MEMDocs repository.
