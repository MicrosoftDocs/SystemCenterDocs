<properties title="" pageTitle="File names and locations for System Center technical articles" description="Explains the file structure for articles and the naming conventions you should follow when you create a new article." metaKeywords="" services="" solutions="" documentationCenter="" authors="Jim-Parker" videoId="" scriptId="" manager="required" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="03/14/2016" ms.author="jimpark; tysonn" />

#File names and locations for System Center technical articles

Here's what you need to know.

##Rules

- Files names can contain ONLY lowercase letters, numbers, and hyphens.
- No spaces or punctuation characters. Use the a single hyphen to separate words and numbers in the file name.
- No more than 80 characters - this is a publishing system limit
- Use action verbs that are specific, such as develop, buy, build, troubleshoot. No -ing words.
- No small words - don't include a, and, the, in, or, etc.
- All files must be in markdown and use the .md file extension.
- Spell the words out; avoid unapproved or unnecessary acronyms in file names
- Do not include "system-center" in the filename.
- Do not include version numbers/indicators in the filename.

Acronyms and initialisms in file names - specific guidelines:

- Follow existing Microsoft guidance for acceptable System Center component name abbreviations
- Other industry-standard abbreviations are acceptable as necessary in file names.

##File name approval

It's the job of the pull request reviewer to review file names when a new file is submitted to the repository for the first time. Pull request reviewers should review the file name and provide feedback via the pull request comment stream if changes are needed. The file name needs to be corrected before the pull request is accepted. Contributors can easily push the update to the pending pull request.

##Folder names in the repo

Folders should be created only for the component, plus plan, deploy, get-started, manager, and media subfolders. Use only letters and hyphens, and use all lowercase letters. Obtain approval from the repository admin before you create a new folder that is not for a released service.

Media folders exist under the component level folder.

##Changing case in file names

Windows operating systems are case insensitive, so if you need to change a file name to fix casing, it is better to make a substantive change, unless you are able to make the change on a Linux or Mac. For example:

  biztalk-administration-and-Development-Task-List-in-BizTalk-Services --> biztalk-services-administration-and-development-task-list

Use the following command to rename a file:
```
  git mv <SystemCenterDocs/component-folder/subfolder/current-file-name.md> <SystemCenterDocs/component-folder/subfolder/new-file-name>
```

###Contributors' Guide Links

- [Overview article](./../README.md)
- [Index of guidance articles](./contributor-guide-index.md)
