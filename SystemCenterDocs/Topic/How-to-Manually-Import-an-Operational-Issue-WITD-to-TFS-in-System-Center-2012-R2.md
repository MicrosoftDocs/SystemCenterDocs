---
title: How to Manually Import an Operational Issue WITD to TFS in System Center 2012 R2
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab965a68-fe24-4f40-9728-d1522bc70fec
---
# How to Manually Import an Operational Issue WITD to TFS in System Center 2012 R2
[!INCLUDE[omblue_1](../Token/omblue_1_md.md)] integration with Team Foundation Server \(TFS\) uses the work item type *Operational Issue*, which must be present in each team project that synchronization uses. Generally, the TFS Work Item Synchronization Configuration Wizard can import this work item type definition \(WITD\). In some cases, however, you must manually import the WITD directly to TFS. You must manually import the Operational Issue WITD in the following cases:

-   A separate TFS administrator controls the development process model in TFS.

-   You are running the TFS 2010 Object Model to integrate with TFS 2012 or TFS 2013.

-   You are running the TFS 2012 Object Model to integrate with TFS 2010 or TFS 2013.

-   You are configuring synchronization with a non\-English version of TFS.

-   An external procedure has removed the Operational Issue WITD from the team projects in TFS, and you still want to synchronize with this team project.

> [!CAUTION]
> The Operational Issue work item type can be renamed and customized, but you also need to customize synchronization as described in [Integrating Operations Manager with Non-English Versions of Team Foundation Server &#40;TFS&#41; or a Customized Process Model in TFS](../Topic/Integrating-Operations-Manager-with-Non-English-Versions-of-Team-Foundation-Server--TFS--or-a-Customized-Process-Model-in-TFS.md).

### To manually import the Operational Issue WITD file

1.  Locate the correct Operational Issue WITD for your version of TFS on the installation media for [!INCLUDE[om12short](../Token/om12short_md.md)] in [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] in the **SupportTools** folder. For TFS 2010, the file name is OperationalIssue.xml. For TFS 2012, the file name is OperationalIssue\_11.xml. For TFS 2013, the file name is OperationalIssue\_11.xml.

2.  Use TFS administrator credentials to run the **witadmin** command\-line tool in TFS and import the Operational Issue WITD to each TFS project you plan to use with synchronization.

    Example for TFS 2010: `witadmin importwitd /collection:http://tfs.contoso.com:8080/tfs /p:ProjectName /f:OperationalIssue.xml`

    Example for TFS 2012: `witadmin importwitd /collection:http://tfs.contoso.com:8080/tfs /p:ProjectName /f:OperationalIssue_11.xml`

    Example for TFS 2013: `witadmin importwitd /collection:http://tfs.contoso.com:8080/tfs /p:ProjectName /f:OperationalIssue_11.xml`

3.  Repeat the previous step for each team project that will be used in synchronization.

## See Also
[witAdmin: Administering Objects for Tracking Work Items](http://go.microsoft.com/fwlink/p/?LinkId=271477)

