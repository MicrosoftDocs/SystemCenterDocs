---
title: Integrating Operations Manager with Non-English Versions of Team Foundation Server (TFS) or a Customized Process Model in TFS
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d45376b-09e5-455e-98db-7fee30cf0885
author:mgoedtel
manager:cfreemanwa
---
# Integrating Operations Manager with Non-English Versions of Team Foundation Server (TFS) or a Customized Process Model in TFS
When you need to synchronize Operations Manager alerts and TFS work items, and your development team is using a non\-English process template in TFS \(included in non\-English versions of TFS\), you must configure Operations Manager so that it can synchronize alerts with TFS work items. This is a complex and detailed process.  
  
## Prerequisites  
You must be running System Center 2012 R2 Update Rollup 1 \(UR1\) or later; System Center 2012 SP1 Update Rollup 5 \(UR5\) or later.  
  
When you download an Update Rollup, you must find an updated version of the Team Foundation Server Work Item Synchronization Management Pack, which is included in the Update Rollup download.  
  
## TFS Process Templates: What to Know  
Each team project in TFS is based on a process template that can be customized for your needs. There are many versions of existing process model templates. Several are included with TFS and you can find more on the Visual Studio Gallery and other community sources. Many of these process templates are also non\-English versions. You can customize any of the process templates based on your style of managing development projects. For more information see, [Customizing Work Item Types in Team Foundation Server](https://go.microsoft.com/fwlink/?LinkId=391715). Because there are many variations of TFS process model templates, you might need to configure Operations Manager to work with the process model currently used by your team projects.  
  
## Customizing Integration  
If you are using a non\-English version of TFS or want to customize a pre\-defined Operational Issue WIDT, you must customize the integration between Operations Manager and TFS. To do this, you must modify the English version of the Work Item Type Definition \(WITD\) that comes with Operations Manager to match the process model and the language used in TFS. Your customization must follow the guidelines listed in [Localization and globalization of WITD child elements](https://go.microsoft.com/fwlink/?LinkId=392521).  
  
> [!IMPORTANT]  
> If you customized the WITD or are using your own WITD, you must manually import it into TFS because automatic import will default to an English version of a process model template with no customizations. For more information, see, [How to Manually Import an Operational Issue WITD in TFS in System Center 2012 R2](https://go.microsoft.com/fwlink/?LinkId=391717).  
  
## Preparing Operations Manager  
  
#### To prepare your Operations Manager environment to integrate with a non\-English version of TFS or to synchronize with a customized process model  
  
1.  Make sure you are using the Team Foundation Server Work Item Synchronization Management Pack that came with System Center 2012 R2 Update Rollup 1 or later and System Center 2012 SP1 Update Rollup 5 or later. This management pack is included in the Update Rollup 1 and Update Rollup 5 download. If you are using a previous TFS Work Item Synchronization management pack, you must remove it before importing the latest version.  
  
2.  Make sure you have imported the Alert Attachment management pack. For more information, see [How to Configure File Attachments for Operations Manager Alerts in System Center 2012 R2](../../om/manage/How-to-Configure-File-Attachments-for-Operations-Manager-Alerts-in-System-Center-2012-R2.md)  
  
3.  Follow the [How to Configure Integration with TFS in System Center 2012 R2](https://go.microsoft.com/fwlink/?LinkId=391721), but don't automatically import the Work Item Type Operational Issue.  
  
4.  After completing the TFS Work Item Synchronization configuration wizard, click **Create**. On the **Import Operational Issue Work Item Type Definition** page, click **Cancel**. You don't need to supply a password. Then on the **TFS Work Item Synchronization** page, click **Save** to save the integration settings without automatically importing the Operational Issue Work Item Type Definition.  
  
5.  Your configuration is saved, but you can't use it yet. You will receive an alert from the TFS Work Item Synchronization Management Pack indicating that synchronization is in an unhealthy state. This alert will disappear after you provide a valid WITD and configure the required overrides.  
  
## Synchronizing with a WITD other than the Operational Issue Work Item Type Definition  
By default, synchronization happens using Operational Issue \(as spelled in English\) WITD, but if you want to synchronize with a different WITD or if you'd like to customize or change the WITD default name, such as spelling Operational Issue WITD in a language other than English, you need to customize the Operational Issue Work Item Type template which is on the Operations Manager installation media and then manually import it to each of the team projects used in synchronization. For more information, see [How to Manually Import an Operational Issue WITD to TFS in System Center 2012 R2](https://go.microsoft.com/fwlink/?LinkId=391717). For information about customization, see [Customizing Work Item Types](https://go.microsoft.com/fwlink/?LinkId=391715).  
  
**How much can I customize?**  
  
You can change and customize many things, but the Work Item Type used in synchronization must include all of the fields that are defined by the Operational Issue WITD. Additionally, all workflows among these fields must maintain their general behavior as described in the Operational Issue WITD. The override values you enter in Operations Manager must match your WITD.  
  
**Do I need to change overrides, too?**  
  
Synchronization between Operations Manager and TFS relies on the following elements of WITD:  
  
-   WITD name  
  
-   Work item states and transitions  
  
-   Problem severity codes  
  
If you customized the WIDT and changed any of these values,  to you must also change the corresponding overrides.  
  
Additionally, you must change these overrides if you changed any of these elements in your WITD:  
  
-   Name of the Work Item Type you synchronize with  
  
-   Provide the values for the Work Item System.State codes. You need to specify which of the values of the Work Item System.State corresponds to the original definition of the Operational Issue WITD. You can keep the original English values or use values you have in your process model and\/or in the language you want.  
  
-   Provide the values for the Work Item Microsoft.VSTS.Common.Severity codes. Matching values for each of the alert severity states. You need to specify which of the values of the Work Item Microsoft.VSTS.Common.Severity corresponds to the original definition of the Operational Issue WITD. You can keep the original English values or use values you have in your process model and\/or in the language you want.  
  
### To customize the Operational Issue WITD to work with your process model in TFS  
Customizing a WITD is an advanced operation and requires a good understanding managing team artifacts in TFS. For more information see, [Customizing Work Item Types in Team Foundation Server](https://go.microsoft.com/fwlink/?LinkId=391715).  
  
1.  Locate existing OperationalIssue.xml and make a local copy of the file. You can find the correct Operational Issue WITD for your version of TFS on the installation media for Operations Manager in System Center 2012 R2 in the **SupportTools** folder.  
  
    -   For TFS 2010, the file name is **OperationalIssue.xml**.  
  
    -   For TFS 2012, the file name is **OperationalIssue\_11.xml**.  
  
    -   For TFS 2013, the file name is **OperationalIssue\_11.xml**.  
  
    > [!TIP]  
    > You might want to change the filename to match your  WITD name. It's also a good idea to make extra copies of the file in case you make a mistake during this complex process and need to revert your changes.  
  
    > [!NOTE]  
    > You can also choose to start from your own WITD in which case you will need to manually merge it with the Operational Issue WITD included in Operations Manager. This is a more complex procedure, but gives you the flexibility to reuse logic from an existing WITD.  
  
2.  Open a local copy of the file in an xml editor and find these xml nodes:  
  
    1.  Under WITD node <WORKITEMTYPE name\="Operational Issue"> \- replace "Operational Issue" with the name of your work item.  
  
        For example, replace <WORKITEMTYPE name\="**Operational Issue**"> with <WORKITEMTYPE name\="**操作问题**">.  
  
    2.  In WITD\/ WORKITEMTYPE\/FIELDS specify desired "name" value for each field used in synchronization \(they are listed below in the overrides table\).  
  
        For example, replace <FIELD name\="**Assigned To**" refname\="System.AssignedTo" type\="String" syncnamechanges\="true" reportable\="dimension"> with <FIELD name\="**关闭日期**" refname\="Microsoft.VSTS.Common.ClosedDate" type\="DateTime" reportable\="dimension">.  
  
        > [!IMPORTANT]  
        > The field names must match other WITDs in your process model for the same refname.  
  
    3.  Under WITD\/WORKITEMTYPE\/FIELDS\/FIELD where refname\="Microsoft.VSTS.Common.Severity", modify allowed values to match your own desired severity codes.  
  
        For example, replace <FIELD name\="Severity" refname\="Microsoft.VSTS.Common.Severity" type\="String" reportable\="dimension">    <ALLOWEDVALUES expanditems\="true">          <LISTITEM value\="**1 \- Critical**" \/>          <LISTITEM value\="**2 \- High**" \/>          <LISTITEM value\="**3 \- Medium**" \/>          <LISTITEM value\="**4 \- Low**" \/>        <\/ALLOWEDVALUES>     <\/FIELD> with this: <FIELD name\="严重级别" refname\="Microsoft.VSTS.Common.Severity" type\="String" reportable\="dimension">        <ALLOWEDVALUES expanditems\="true">          <LISTITEM value\="**1 \- 严重**" \/>          <LISTITEM value\="**2 \- 高**" \/>          <LISTITEM value\="**3 \- 中**" \/>          <LISTITEM value\="**4 \- 低**" \/>        <\/ALLOWEDVALUES>  
  
    4.  Under WITD\/WORKFLOW\/STATES, specify desired values for each state of the fields from step b.  
  
        For example, change <STATE value\="**Closed**"> to <STATE value\="**已关闭**">.  
  
    5.  Under WITD\/TRANSITIONS, modify each Transition from "state" to transition to "state", where states need to match the security codes you chose in step c.  
  
        For example, change <TRANSITION from\="**Accepted**" to\="**Closed**"> to <TRANSITION from\="**已批准**" to\="**已关闭**">.  
  
3.  Import WITD into each project in TFS that is used in synchronization  
  
4.  Match the values you changed in this file with the overrides in Operations Manager.  
  
5.  You might also want to change other constants and labels to match your process model.  
  
6.  Manually import the WITD that you created into TFS for each project that you want to use with synchronization.  
  
## Configuring Operations Manager to use your customized WITD in synchronization with TFS  
Now that you've changed your process model, you need to change the corresponding overrides for rules in Operations Manager so that Operations Manager and TFS synchronization can correctly recognize your customized WITD.  
  
### Rules and overrides that must be changed in Operations Manager to match your customized WITD  
  
||||||  
|-|-|-|-|-|  
|**Parameter**|**Object TFS Collection, TFS Work Item Synchronization Rule**|**Object TFS Collection, Attachment Synchronization Rule**|**Object TFS Connector, TFS Work Item Creation Rule**|**Default Value as defined in Operational Issued WITD**|  
|Work Item Type Name|Use value from customized WIDT|Use value from customized WIDT|Use value from customized WIDT|Operational Issue|  
|Operational Issue State Accepted|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|Accepted|  
|Operational Issue State Assigned|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|Assigned|  
|Operational Issue Awaiting Evidence|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|Awaiting evidence|  
|Operational Issue Closed|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|Closed|  
|Operational Issue New|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|New|  
|Operational Issue Resolved|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|Resolved|  
|Operational Issue Scheduled|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|Scheduled|  
|Operational Issue Suspended|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|Suspended|  
|Operational Issue Work In Progress|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|Work in progress|  
|Severity Critical|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|1 \- Critical|  
|Severity High|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|2 \- High|  
|Severity Medium|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|3 \- Medium|  
|Severity Information|Use value from customized WIDT|Not Applicable|Use value from customized WIDT|4 \- Low|  
  
