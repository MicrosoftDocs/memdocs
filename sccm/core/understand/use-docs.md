---
title: How to use the docs
titleSuffix: Configuration Manager
description: Learn tips on using the Configuration Manager technical documentation library.
ms.date: 04/30/2018
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# How to use the Configuration Manager docs

*Applies to: System Center Configuration Manager (Current Branch)*

This article provides the following sections with multiple resources and tips for using the Configuration Manager documentation library:  

- [How to search](#bkmk_searchtips)  

- [Submitting doc bugs, enhancements, questions and new ideas](#bkmk_docfeedback)  

- [How to get notified of changes](#bkmk_notifications)  

- [How to contribute to docs](#bkmk_contribute)  


For general help with the product, see [Find help](/sccm/core/understand/find-help).


##  <a name="bkmk_searchtips"></a> Search   
 Use the following search tips to help you find the information that you need:  

-   When using your preferred search engine to locate content for Configuration Manager, include `SCCM` along with your search keywords.  

    - Look for results from docs.microsoft.com for Configuration Manager current branch. Results from technet.microsoft.com or msdn.microsoft.com are for older product versions.  

    - To further focus the search results to the current content library, include `site:docs.microsoft.com` to scope the search engine.  

-   Use search terms that match terminology in the user interface and online documentation. Avoid unofficial terms or abbreviations that you might see in community content. For example, search for "management point" rather than "MP"; "deployment type" rather than "DT"; and "software updates" rather than "SUM."  

-   To search within an article you are currently viewing, use your browser's **Find** feature. With most modern web browsers, press **Ctrl**+**F** and then enter your search terms.  

-   Each article on docs.microsoft.com includes the following fields to assist with searching the content:  

    - **Search** in the upper right corner. To search all articles enter terms in this field. Articles in the Configuration Manager library automatically include the "ConfigMgr" scope.  

    - **Filter by title** above the left table of contents. To search the current table of contents, enter terms in this field. This field only matches terms that appear in the article titles for the current node. For example, Core Infrastructure or Application Management.  

- Having problems finding something? [File feedback!](#bkmk_docfeedback) When filing the issue, provide the search engine you're using, the keywords you tried, and the target article. This feedback helps Microsoft optimize the content for better search.  



## <a name="bkmk_docfeedback"></a> Feedback

Go to the Feedback section at the bottom by clicking the **Feedback** link in the upper right of any article. This section is integrated with GitHub Issues. For more information about integration with GitHub Issues, see the [docs platform blog post](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs).

To share feedback on the Configuration Manager product itself, click **Give product feedback**. For more information, see [Product feedback](/sccm/core/understand/find-help#product-feedback). 

A [GitHub account](https://github.com/join) is a prerequisite for providing documentation feedback. Once you sign in, there is a one-time authorization for MicrosoftDocs. Then when you click **Give documentation feedback**, enter a title and comment, and then **Submit feedback**. This action files a new issue for the target article in the [SCCMdocs repository](https://github.com/MicrosoftDocs/SCCMdocs/issues).

This integration also displays any existing open or closed issues for the target article. If any exist, review them before submitting a new issue. If you find a related issue, click the face icon to add a reaction, or you can expand it to add a comment. 

#### Types of feedback
Use GitHub Issues to submit the following types of feedback:
- Doc bug: The content is out of date, unclear, confusing, or broken.
- Doc enhancement: A suggestion to improve the article.
- Doc question: You need help finding existing documentation.
- Doc idea: A suggestion for a new article. Use this method instead of UserVoice for documentation feedback.
- Kudos: Positive feedback about a helpful or informative article!
- Localization: Feedback about content translation.
- Search engine optimization (SEO): Feedback about problems searching for content. Include the search engine, keywords, and target article in the comments.

If issues are raised for non-doc-related topics, such as [product feedback](/sccm/core/understand/find-help#product-feedback), [product questions](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB), or [support requests](https://aka.ms/cmcbsupport), these issues will be closed and the user redirected to the proper feedback channel.

To share feedback on the docs.microsoft.com platform, see [Docs feedback](https://aka.ms/sitefeedback). The platform includes all of the wrapper components such as the header, table of contents, and right menu. Also how the articles render in the browser, such as the font, alert boxes, and page anchors.



## <a name="bkmk_notifications"></a> Notifications

To receive notifications when content changes in the documentation library, use the following steps:

1. Use the [docs search](https://docs.microsoft.com/search/index?scope=ConfigMgr) to find an article or set of articles. For example:
    - Search for a single article by title: ["Log files for troubleshooting - Configuration Manager"](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr)
    - Search for any article regarding [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr)
2. In the upper right corner, click the **RSS** link. 
3. Use this feed in any RSS application to receive notifications when there is a change to any of the search results.


> [!Tip]  
> You can also **Watch** the [SCCMdocs repository](https://github.com/MicrosoftDocs/SCCMdocs) on GitHub. This method generates a lot of notifications. It also doesn't include changes from a private repository used by Microsoft.  



## <a name="bkmk_contribute"></a> Contribute

The Configuration Manager documentation library, like most content on docs.microsoft.com, is open-sourced on GitHub. This library accepts and encourages community contributions. For more information on how to get started, see the [Contributor Guide](https://docs.microsoft.com/contribute). Creating a [GitHub account](https://github.com/join) is the only prerequisite.

#### Basic steps to contribute to SCCMdocs
1. From the target article, click **Edit**. This action opens the source file in GitHub.
2. To edit the source file, click the pencil icon.
3. Make changes in the markdown source. For more information, see [How to use Markdown for writing Docs](https://docs.microsoft.com/contribute/how-to-write-use-markdown). 
4. In the Propose file change section, enter the public commit comment describing *what* you changed. Then click **Propose file change**.
5. Scroll down and verify the changes you made. Click **Create pull request** to open the form. Describe *why* you made this change. Tag the article author and request that they review. Click **Create pull request**.

### What to contribute
If you're interested in contributing but don't know where to start, see the following suggestions:
- Review an article for accuracy. Then update the **ms.date** metadata using `mm/dd/yyyy` format. This contribution helps keep the content fresh.
- Add clarifications, examples, or guidance based on your experience. This contribution uses the power of the community to share knowledge.  
- Correct translations in a non-English language. This contribution improves the usability of localized content.
- Search the list of issues for the community-targeted labels [good-first-issue](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue) and [help-wanted](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted). These labels are assigned by Microsoft authors to issues that are good candidates for community contribution.