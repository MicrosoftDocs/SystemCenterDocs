---
title: How to Change an Existing Incident
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb8118ec-94ac-404a-be0d-bc34b8996cfa
translation.priority.mt: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to Change an Existing Incident
In [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], you can use the following procedures to change the urgency of an incident, edit an unassigned incident from [!INCLUDE[om12short](../../../sm/deploy/upgrade/includes/om12short_md.md)], link a knowledge article to an incident, and validate the changes. Users create simplified incidents using the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)], based on the Incident portal template. Because user\-created incidents are simplified, analysts often need to revise new incidents with additional information. Additionally, there is no functional difference between incidents created with the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)], using either the **Need help with a problem** or **Need repair or fix** options.  
  
> [!NOTE]  
>  Incidents are automatically created by [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] when the Operations Manager Alert connector is enabled. You can edit the new incidents that are generated when an Operations Manager alert is raised and then assign the incidents to analysts. [!INCLUDE[crdefault](../../../sm/manage/author/includes/crdefault_md.md)] “Importing Data and Alerts from Operations Manager 2007” in [System Center Service Manager 2012 Administrator's Guide](http://go.microsoft.com/fwlink/p/?LinkID=209669).  
  
### To change the urgency of an incident  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Incident Management**, and then click **All Open E\-Mail Incidents**.  
  
3.  In the **All Open E\-Mail Incidents** view, select the original incident. For example, select the **Unable to print checks** incident.  
  
4.  In the **Tasks** pane, click **Edit**.  
  
5.  In the **Incident** form, in the **Urgency** list, select **High**.  
  
6.  Optionally, type a comment in the **Action Log** box. If you do not want end users to be able to read the comment, select the **Private** check box that is above the **Action Log** box. For example, in the **Action Log** box, type **The user called to say that the backup printer is unavailable and that this issue is now urgent**. Then, click **Add**. The new comment appears as a log entry.  
  
7.  Click **OK** to close the form and to save your changes.  
  
### To edit an unassigned incident from Operations Manager  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Incident Management**, and then click **All Open Operations Manager Incidents**.  
  
3.  In the **All Open Operations Manager Incidents** view, select an incident that was created automatically from an Operations Manager alert.  
  
4.  In the **Tasks** pane, click **Edit**.  
  
5.  In the **Incident** form, under **Support Group**, select **Tier 1**.  
  
6.  Under **Assigned to**, enter the name of the help desk analyst who will investigate the problem.  
  
7.  Click **OK** to close the form and to save your changes.  
  
### To link a knowledge article to an incident  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Incident Management**, and then click **All Open Operations Manager Incidents**.  
  
3.  In the **All Open Operations Manager Incidents** view, select the incident that was created automatically from an Operations Manager alert.  
  
4.  In the **Tasks** list, click **Search for Knowledge Articles**.  
  
5.  In the **Knowledge Search** dialog box, type a search term in the **Search for** box, and then click **Go**. For example, type **MICR Check Printer Article**.  
  
6.  Select the article, click **Link to \<IncidentName\>**, click **OK** to close the informational dialog box, and then click **Close**.  
  
### To validate incident edits  
  
-   Open the incident, and then verify that your changes appear. For example, verify that the comment you entered appears as a log entry.  
  
## See Also  
 [Managing Incidents](../../../sm/manage/operate/Managing-Incidents.md)