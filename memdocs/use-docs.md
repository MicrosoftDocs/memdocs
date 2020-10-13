---
title: How to use the docs
titleSuffix: Microsoft Endpoint Manager
description: Learn how to search the docs, provide doc feedback, and contribute to the docs for Microsoft Endpoint Manager. These docs include Configuration Manager, Intune, and Autopilot.
ms.date: 10/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 54d19001-7e2b-489a-ba52-1fee3ff25bae
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to use the docs

This article provides resources and tips for using the Microsoft Endpoint Manager documentation library for Configuration Manager, Microsoft Intune, and Autopilot:

- How to search
- Submitting doc bugs, enhancements, questions, and new ideas
- How to get notified of changes
- How to contribute to docs

For general help and support, see:

- [Find help for Configuration Manager](configmgr/core/understand/find-help.md)
- [Get support for Intune](intune/fundamentals/get-support.md)

> [!TIP]
> Visit the **Documentation** node in the **Community** workspace of the Configuration Manager console. This node includes up-to-date information about Configuration Manager documentation and support articles. For more information, see [Using the Configuration Manager console](configmgr/core/servers/manage/admin-console.md#bkmk_doc-dashboard).

Information in this article also applies to the [Configuration Manager PowerShell documentation](/powershell/sccm/overview) in the [sccm-docs-powershell-ref repository](https://github.com/MicrosoftDocs/sccm-docs-powershell-ref).

## Search

Use the following search tips to help you find the information that you need:

- When using your preferred search engine to locate content, include a keyword along with your search keywords. For example, `ConfigMgr` for Configuration Manager and `Intune` for Intune.

  - Look for results from `docs.microsoft.com/mem`. Results from `docs.microsoft.com/previous-versions`, `technet.microsoft.com`, or `msdn.microsoft.com` are for older product versions.

  - To further focus the search results to the current content library, include `site:docs.microsoft.com` in your query to scope the search engine.

- Use search terms that match terminology in the user interface and online documentation. Avoid unofficial terms or abbreviations that you might see in community content. For example, search for:

  - "management point" rather than "MP"
  - "deployment type" rather than "DT"
  - "Intune management extension" rather than "IME"

- To search within the current article, use your browser's **Find** feature. With most modern web browsers, press **Ctrl**+**F** and then enter your search terms.

- Each article on `docs.microsoft.com` includes the following fields to assist with searching the content:

  - **Search** in the upper right corner. To search all articles, enter terms in this field. Articles in this content library automatically include one of the following search scopes: `ConfigMgr` or `Intune`.

    :::image type="content" source="media/docs-search-field.png" alt-text="Docs search field in header":::

  - **Filter by title** above the left table of contents. To search the current table of contents, enter terms in this field. This field only matches terms that appear in the article titles for the current node. For example, **Configuration Manager Core Infrastructure** (`docs.microsoft.com/mem/configmgr/core`) or **Intune Apps** (`https://docs.microsoft.com/mem/intune/apps/`). The last item in the search results gives you the option to search for the terms in the entire content library.

    :::image type="content" source="media/docs-filter-toc.gif" alt-text="Animation of using the table of contents filter":::

Having problems finding something? [File feedback!](#feedback) When you file an issue regarding search results, provide the search engine you're using, the keywords you tried, and the target article. This feedback helps Microsoft optimize the content for better search.

## Feedback

Select the **Feedback** link in the upper right of any article to go to the Feedback section at the bottom. Feedback is integrated with GitHub Issues. For more information about this integration with GitHub Issues, see the [docs platform blog post](/teamblog/a-new-feedback-system-is-coming-to-docs).

:::image type="content" source="media/docs-feedback.png" alt-text="Screenshot of the feedback section on a docs article":::

To share non-docs feedback about the product itself, select **This product**. This action opens the product's UserVoice site.

To share docs feedback about the current article, select **This page**. A [GitHub account](https://github.com/join) is a prerequisite for providing documentation feedback. Once you sign in, there's a one-time authorization for the MicrosoftDocs organization. It then opens the GitHub new issue form. Add a descriptive title and detailed feedback in the body, but don't modify the document details section. Then select **Submit new issue** to file a new issue for the target article in the [MEMDocs GitHub repository](https://github.com/MicrosoftDocs/memdocs/issues).

To see whether there's already feedback for this article, select **View all page feedback**. This action opens a GitHub issue query for this article. By default it displays both open and closed issues. Review any existing feedback before you submit a new issue. If you find a related issue, select the face icon to add a reaction, add a comment to the thread, or **Subscribe** to receive notifications.

### Types of feedback

Use GitHub Issues to submit the following types of feedback:

- Doc bug: The content is out of date, unclear, confusing, or broken.
- Doc enhancement: A suggestion to improve the article.
- Doc question: You need help with finding existing documentation.
- Doc idea: A suggestion for a new article. Use this method instead of UserVoice for documentation feedback.
- Kudos: Positive feedback about a helpful or informative article!
- Localization: Feedback about content translation.
- Search engine optimization (SEO): Feedback about problems searching for content. Include the search engine, keywords, and target article in the comments.

If you create an issue for non-doc-related topics, Microsoft will close the issue and redirect you to a better feedback channel. For example:

- Product feedback for [Configuration Manager](configmgr/core/understand/find-help.md#product-feedback) or [Intune](https://microsoftintune.uservoice.com/forums/291681-ideas)
- [Product questions](/answers/products/mem)
- Support requests for [Configuration Manager](https://aka.ms/cmcbsupport) or [Intune](intune/fundamentals/get-support.md)

To share feedback on the fundamental docs.microsoft.com platform, see [Docs feedback](https://aka.ms/sitefeedback). The platform includes all of the wrapper components such as the header, table of contents, and right menu. Also how the articles render in the browser, such as the font, alert boxes, and page anchors.

## Notifications

To receive notifications when content changes in the documentation library, use the following steps:

1. Use the [docs search](/search/) to find an article or set of articles. For example:

    - Search for a single article by title, ["What's new in Microsoft Intune - Azure"](/search/index?scope=Intune&search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22)

        > [!TIP]
        > To refine a single article search to a single article, use the full title that displays in the docs.microsoft.com search results. This title is what appears in the browser tab.

    - Search for any Configuration Manager article about [BitLocker](/search/index?scope=ConfigMgr&search=BitLocker)

1. At the bottom of the list of results, select the **RSS** link.

    :::image type="content" source="media/docs-search-rss.png" alt-text="Screenshot of search results and RSS link":::

1. Use this feed in any RSS application to receive notifications when there's a change to any of the search results.

Several popular articles in this content library have a tip at the top with a ready-made link to the RSS feed.

> [!TIP]
> You can also **Watch** the [MEMDocs repository](https://github.com/MicrosoftDocs/memdocs) on GitHub. This method can generate _many_ notifications. It also doesn't include changes from the private repository that Microsoft uses.

## Contribute

The Microsoft Endpoint Manager documentation library, like most content on docs.microsoft.com, is open-sourced on GitHub. This library accepts and encourages community contributions. For more information on how to get started, see the [Contributor Guide](/contribute). The only prerequisite is to create a [GitHub account](https://github.com/join).

### Basic steps to contribute

1. From the target article, select **Edit** in the upper right corner. This action opens the source file in GitHub.

1. To edit the source file, select the pencil icon.

    :::image type="content" source="media/docs-github-edit.png" alt-text="Screenshot of GitHub source file header":::

1. Make changes in the markdown source. For more information, see [How to use Markdown for writing Docs](/contribute/markdown-reference).

1. In the Propose file change section, enter the public commit comment describing _what_ you changed. Then select **Propose file change**.

1. Scroll down and verify the changes you made. Select **Create pull request** to open the form. Describe _why_ you made this change. Select **Create pull request**.

The writing team receives your pull request, and assigns it to the appropriate writer. The author reviews the text, and does a quick edit pass on it. They'll either approve and merge the changes, or contact you for more information about the update.

### What to contribute

If you want to contribute, but don't know where to start, see the following suggestions:

- Review an article for accuracy. Then update the **ms.date** metadata using `mm/dd/yyyy` format. This contribution helps keep the content fresh.

- Add clarifications, examples, or guidance based on your experience. This contribution uses the power of the community to share knowledge.

- Correct translations in a non-English language. This contribution improves the usability of localized content.

- Search the list of issues for the community-targeted labels:

  - **good first issue**
  - **help wanted**

    Microsoft authors can assign these labels to issues that are good candidates for community contribution. They're primarily used for [Configuration Manager PowerShell docs](https://github.com/MicrosoftDocs/sccm-docs-powershell-ref/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22).

> [!NOTE]
> Large contributions require signing a Contribution License Agreement (CLA) if you aren't a Microsoft employee. GitHub automatically requires you to sign this agreement when a contribution meets the threshold. You only need to sign this agreement once.

### Tips

Follow these general guidelines when you contribute:

- Don't surprise us with large pull requests. Instead, [file an issue](#feedback) and start a discussion. Then we can agree on a direction before you invest a large amount of time.

- Read the [Microsoft style guide](https://aka.ms/MicrosoftStyle). Know the [Top 10 tips for Microsoft style and voice](/style-guide/top-10-tips-style-voice).

- Follow the [GitHub Flow workflow](https://guides.github.com/introduction/flow/).

- Blog and tweet (or whatever) about your contributions, frequently!

(This list was borrowed from the [.NET contributing guide](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts).)
