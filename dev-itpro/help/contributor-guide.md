---
title: Extend, customize, collaborate on the Help
description: Tips and tricks for working with the GitHub repos and MarkDown files for Dynamics 365 Business Central.
author: edupont04
ms.custom: na
ms.reviewer: na
ms.topic: article
ms.service: "dynamics365-business-central"
ms.date: 03/22/2019
ms.author: edupont
---

# Extend, Customize, and Collaborate on the Help for [!INCLUDE[prodlong](../developer/includes/prodlong.md)]

The Help for the base application is available in a public GitHub repo so that you can easily extend and customize for your customers. In this section, you can learn about working with the GitHub repos and MarkDown files.  

## GitHub repos

There are different repos in GitHub for the source content and each of the languages that Microsoft translates to. The [dynamics365smb-docs](https://github.com/MicrosoftDocs/dynamics365smb-docs) repo contains the content in English (US). If you want access to the content in other languages, navigate to the relevant repo - the names follow this pattern: dynamics365smb-docs-pr.\<language>-\<country>, such as [dynamics365smb-docs-pr.da-DK](https://github.com/MicrosoftDocs/dynamics365smb-docs-pr.da-DK) for the Danish version.  

> [!NOTE]
> Microsoft accepts pull requests to the *dynamics365smb-docs* repo only, not the language-specific repos. If you have feedback about translations, you can report a GitHub issue in the relevant repo.

When Microsoft publishes an update to the content, the *live* branch in the corresponding GitHub repo is updated. The source repo is updated monthly, and the related language-specific repos are updated less frequently as new translations are made available. You can choose to update your fork with updates from the Microsoft repo on a monthly or less frequent basis depending on your preferred work processes. The GitHub platform and tooling will help you manage any potential merge conflicts if you have made changes to the same files as Microsoft has. For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/).  

> [!TIP]
> You are not required to make your GitHub repos public. When you fork a public repo, you can specify in the settings for the new repo if the repo is public, private, or available only to specific GitHub accounts.

For guidance about the Microsoft-provided content for [!INCLUDE [prodshort](../developer/includes/prodshort.md)], see [User Assistance Model](../user-assistance.md).

### Get started with GitHub

1. Fork the right repo

    You cannot work directly in the [!INCLUDE [prodshort](../developer/includes/prodshort.md)] repos in the MicrosoftDocs GitHub org, such as the dynamics365smb-docs repo, so the first thing you need to do is create a fork of the repo under your GitHub account. A fork basically is copy of this repo that lets you work freely on the content without affecting the MicrosoftDocs/dynamics365smb-docs repo. For more information, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).

2. Install GitHub Desktop (optional) and clone your forked repo.

    GitHub Desktop makes is easy to work and collaborate with repos locally from your own desktop. For more information, see [GitHub Desktop](https://desktop.github.com/).  

3. Get hold of your favorite MarkDown editor, and start making changes.

    The help content is stored in the *business-central* folder of the repo. Articles use a syntax for formatting text called GitHub Flavored Markdown, which is widely popular in the MarkDown community. To learn more about working with markdown, see [Getting started with writing and formatting on GitHub](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/).

    If you want to work locally, you can edit using any text editor. Just save the file as a .md type. Here are a couple good tools that provide you with some nice features, such as Preview:

    - [Visual Studio Code](https://code.visualstudio.com/) with the [Docs Authoring Pack for Visual Studio Code](/contribute/how-to-write-docs-auth-pack)  
    - [Atom](https://atom.io/) (this has spell check and is good for managing many files)

You can also find guidance for how to get started with MarkDown in the [Docs Contributor Guide](https://docs.microsoft.com/en-us/contribute/), which is published by the team that built the Docs.microsoft.com site where the Business Central team publishes their docs.

### Get updates from Microsoft

Microsoft makes frequent changes to the [!INCLUDE [prodshort](../developer/includes/prodshort.md)] content, and those changes show up in the public GitHub repos. The base repo, MicrosoftDocs/dynamics365smb-docs, is updated weekly, and the translations are updated monthly. But you can choose to get updates monthly, twice a year, or once a year, for example. That is entirely up to you.  

When you decide it is time to get the latest version of the content from Microsoft, you can do that using GitBash or GitHub Desktop. In the Help for GitHub, you can see [an example of how this works in GitBash](https://help.github.com/en/articles/merging-an-upstream-repository-into-your-fork), but in GitHub Desktop, you simply use the *Merge into current branch* menu item to pull changes from the origin into your fork.  

However, if your solution is available in more than one country, then you are likely to want to make content available in multiple languages. Microsoft has a GitHub repo for each supported language, but the configuration files are only available in the English (US) source repo, MicrosoftDocs/dynamics365smb-docs. To help you get the content that you need, you might want to run a PowerShell script that picks up content from the various GitHub repos.  

The following example is based on a script that a Danish partner developed in order to get the Microsoft source for a number of languages, and then build HTML files for the legacy Dynamics NAV Help Server. The script is provided in agreement with the partner without further support.

```powershell
$languages = $("da-dk","de-ch","de-de")
$git = "C:\Program Files\Git\cmd\git.exe"
$docfx = "C:\GitHub\DocFx\docfx.exe"
$365docs = "C:\GitHub\MSFT\dynamics365smb-docs"
$langDir = "c:\GitHub\MSFT\dynamics365smb-docs-pr."

Start-Process -FilePath $git -ArgumentList "clone --single-branch --branch live https://github.com/MicrosoftDocs/dynamics365smb-docs.git" -WorkingDirectory "C:\working\Help" -Wait
foreach ($language in $languages)
{
    $arguments = $("clone --single-branch --branch live https://github.com/MicrosoftDocs/dynamics365smb-docs-pr." + $language + ".git")
    Start-Process -FilePath $git -ArgumentList $arguments -WorkingDirectory "C:\working\Help" -Wait
    Copy-Item $($365docs + "\business-central\NAVdocfx.json") $($langDir + $language + "\business-central")
    Copy-Item $($365docs + "\business-central\media") $($langDir + $language + "\business-central") -Recurse -Force
    Copy-Item $($365docs + "\business-central\LocalFunctionality") $($langDir + $language + "\business-central") -Recurse -Force
    Copy-Item $($365docs + "\Templates") $($langDir + $language) -Recurse -Force
    Set-Content -Path $($langDir + $language + "\business-central\NAVdocfx.json") -Value (get-content -Path $($365docs + "\business-central\NAVdocfx.json") | Select-String -Pattern 'dest": "c:\working\output",' -NotMatch)
    Start-Process -FilePath $docfx -ArgumentList $("C:\working\help\dynamics365smb-docs-pr." + $language + "\business-central\NAVdocfx.json" + " --output c:\working\output\" + $language)
```

Because the Microsoft repos are public, you do not need a valid GitHub account in order to get the content. However, we recommend that your organization has a system account with access to GitHub at a minimum.  

### Contributing

A benefit of GitHub is the ability for you to contribute to the core content that the Microsoft team provides in the dynamics365smb-docs repo. For example, you might have a new article that you think would be beneficial or you might have a correction to an existing article. If you would like to contribute to the MicrosoftDocs/dynamics365smb-docs repo, you create what is called a *pull request* from your repo to the MicrosoftDocs/dynamics365smb-docs repo. The Microsoft team will then review the request and include the changes as appropriate.

For example, to create a pull request to the MicrosoftDocs/dynamics365smb-docs repo by using GitHub Desktop, do the following:

1. Commit the changes to your repo that you want to include in the pull request.
2. Choose **Sync** to push the changes up to your repo on GitHub.
3. When the sync is completed, choose **Pull Request**, make sure that the pull request points at the *live* branch, and then choose send **Pull Request**.

## Building HTML files

For publishing to your own website, you can use tools such as [DocFx](https://dotnet.github.io/docfx/). For example, if you want to preview your content locally, or if you want to publish to the legacy Microsoft Dynamics NAV Help Server. DocFX is an open source tool for converting markdown files. This section provides some guidance on how you can use DocFX to publish HTML files for the Dynamics NAV Hep Server.

1. Install DocFX on your computer.

    For more information, see [DocFx](https://dotnet.github.io/docfx/).

2. Specify the output folder in which to store the generated HTML files.

    By default the files will be saved in the folder *c:/output*. The output folder is set in the NAVdocfx.json file. If you want to change this folder, do the following:

    a. In the folder where your local clone is, such as *C:\GitHub\dynamics365smb-docs\business-central*, open the NAVdocfx.json file in your preferred editor.  
    b.  Set the **"dest:"** parameter to your output folder, and save the changes.  

3. Go to your desktop and open a command prompt.

4. Go to the docfx installation folder.

5. Run the following command:

    ```powershell
    docfx "c:\GitHub\dynamics365smb-docs\business-central\NAVdocfx.json"
    ```

The files are generated as .html files and stored in the specified output.

> [!NOTE]
> The root of the MicrosoftDocs repos contain files that are related to internal Microsoft processes, such as .openpublishing.build.ps1. These scripts are used to validate and preview content, but they rely on internal Microsoft resources that are not publicly available.  

## Authoring in Markdown

The content is styled using a Markdown syntax as described below.

<!--INTERNAL
### Properties and tags
All topics must start with a YAML header with the following set of attributes.

```yml
---
title: 'Short title with a couple of buzzwords for the feature. Preferably the same as your heading for the topic.'
description: 'A longer description that identifies the topic in search results with lots of keywords.'
author: MyGitHubAccount
ms-service: dynamics365-business-central
ms.topic: article
ms.search.keywords:keyword1, keyword2
ms.date: MM/DD/YYYY

---
```

The ms.date tag must be updated to the date when you make the change. The ms.date property must follow the US date format of MM/DD/YYYY.
-->

### Headings

Use ```#``` for headings.

Examples:
```#``` Heading 1, looks like:
# Heading 1

```##``` Heading 2, looks like:
## Heading 2

```###``` Heading 3, looks like:
### Heading 3

### Bulleted lists

Use - to create bullets, for example:

The following options are available:
```
- first option
- second option
- third option
```

### Ordered lists

Use numbers for ordered lists. No space between the lines, we'll let the template take care of that.

```
1. Choose the ![Lightbulb that opens the Tell Me feature](media/ui-search/search_small.png "Tell me what you want to do") icon, enter **Payment Journal**, and then choose the related link.
2. In the **Payment Journal** window, on the first journal line, enter the relevant information about the payment entry.
3. To apply a single vendor ledger entry:
4. In the **Applies-to Doc. No.** field, choose the field to open the **Apply Vendor Entries** window.
```

### Bold and italics syntax

Use ```**bold**``` and ```*italics*```

### Tables

For tables in the body, use the markdown syntax.

```
| To   | See                       |
|------|---------------------------|
|<text>|<link>|
| | |
| | |
```

For nested tables in ordered and unordered lists use HTML-syntax. Markdown does not support tables very well. If you use the markdown syntax the list will be broken, the table will align left and list will be renumbered.

### Comment syntax

Useful for sections that are not ready and will not pass the build check.
```
<!-- Comments -->
```
Examples
```
<!-- [Managing Payables](payables-manage-payables.md)-->
<!-- This is a paragraph that spans more lines and I can just put the comment tag
at the beginning and end of it -->
```

### Links

Ordinary link to a different topic in the same folder

These links have the format ```[link text](filename.md)```.

Example:
```[Managing Payables](payables-manage-payables.md)```

### Link to a topic in a subfolder of the source topic

These links have the format ```[link text](subfolder/filename.md)```.

For example, you want to link to payables-manage-payables.md from ui-work-general-journals.md, where the folder structure is as follows:

- articles
    - ui-work-general-journals.md
- ManagePayables
    - payables-manage-payables.md

Here is the link:
```[Manage Payables](ManagePayables/payables-manage-payables.md)```

### Link to a topic in a different folder than source topic

These links have the format ```[link text](../folder/filename.md)```.

For example, you want to link to payables-manage-payables.md from receivables-manage-receivables.md, where the folder structure is as follows:

- articles
  - ManageReceivables
    - receivables-manage-receivables.md
    - ui-work-general-journals.md
    - ManagePayables
      - payables-manage-payables.md

Here is the link:
```[Manage Payables](../ManagePayables/payables-manage-payables.md)```

### Link to a place in the same article

From within an article, you can create a link to a specific heading in the same article. You can create the link like other links except with the following format:

```[link text](#target-heading)```

target-heading is the text of the heading that you want to link to, except it is all lowercase and spaces between words are replaced with hyphens. For example, here is the link:
```[How Autoscaling Works](#how-autoscaling-works)```

To the heading:
```## How Autoscaling Works```

### Link to a place in a different article

From an article, you can create a link to a specific heading in another article. You can create the link like other links except with the following format:

```[link text](targetarticlename#target-heading)```

targetarticlename is the file name of the article, including the .md file type.
target-heading is the text of the heading that you want to link to, except it is all lowercase and spaces between words are replaced with hyphens.

For example, to link to the heading "How Autoscaling Works" in the article Autoscaling.md", add the following code:
```[link text](Autoscaling.md#how-autoscaling-works)```

### Line breaks (soft return)

In the editor, add two blank spaces at the end of the sentence and hit return. This is used in the See Also list. (See Also must be heading 2.)

### Continue steps after a non-step para

Enter four spaces in front of the non-step para. Otherwise, the non-step para will restart the step sequence.

### TOC

The TOC structure of the TOC file is as follows:

```
#[Overview](overview.md)
 ##[Topic 1](topic-1.md)
 ##[Topic 2](topic-2.md)
 ##[Topic 3](topic-3.md)
 ##[Topic 4](topic-4.md)
```

### Standard Phrases

All fields in Business Central have tooltips. Therefore, do not document fields in Help. To refer readers to the tooltips, use this standard phrase where relevant:    
"Choose a field to read a short description of the field or link to more information."
For more information, see [Dynamics 365 Business Central User Assistance Model](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/user-assistance).

### Topic Titles

- Use imperative verb form for step-based topics ("Pay vendors").
- Use gerund verb form for conceptual, non-step topics. ("Paying Vendors")
- Use nouns for highest-level topics. ("Sales")

### File Naming

#### Rules

- No spaces or punctuation characters. Use hyphens to separate the words in the file name.
- Use all lowercase letters
- No more than 80 characters - this is a publishing system limit
- Use action verbs that are specific such as develop, buy, build, troubleshoot. No -ing words.
- No small words - don't include a, and, the, in, or, etc.
- All files must be in markdown and use the .md file extension.

#### Examples

|Topic title |Naming  |
|------------|--------|
|Select a Company|ui-how-select-company.md|
|Enter Criteria in Filters|ui-enter-criteria-filters.md|
|Troubleshooting: Record Locked by Another User|ui-troubleshoot-record-locked-another-user.md|
|Changing Basic Settings|ui-change-basic-settings.md|
|Sales|sales-manage-sales.md|
|Set Up Currencies|finance-setup-currencies.md|
|Set Up Purchasers|purchases-how-setup-purchasers.md|
|Understanding Session Timeouts|admin-understand-session-timeouts.md|
|Manage Data Encryption|admin-manage-data-encryption.md|

### Country-specific content

To simplify content localization and translation, country-specific articles live in country-specific folders. The TOC entries live under the "Local Functionality" parent node.

## See also

[Business Central User Assistance Model](../user-assistance.md)  
[Configuring the Help Experience](../deployment/configure-help.md)  
[Docs Contributor Guide](/contribute/)  
[Docs Authoring Pack for Visual Studio Code](/contribute/how-to-write-docs-auth-pack)  
[Getting started with writing and formatting on GitHub](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)  
[Visual Studio Code](https://code.visualstudio.com/)  
[Atom](https://atom.io/)  
[DocFx](https://dotnet.github.io/docfx/)  
