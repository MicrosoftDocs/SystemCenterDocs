---
title: Manually Create a New Incident
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f5d5399-1014-4587-b10a-773725cd03d4
---
# Manually Create a New Incident
In System Center 2016 Technical Preview \- Service Manager, incidents are automatically created from email requests by users. However, you can use the following procedures to manually create a new incident in the Service Manager console and then validate it. For example, you might want to manually create a new incident for a person who is experiencing an email\-related problem. You can link other affected items, such as various computers, to indicate that the issue affects more than one computer.

### To create a new incident from a configuration item view

1.  In the Service Manager console, select **Configuration Items**.

2.  In the **Configuration Items** pane, expand **Configuration Items**, expand **Computers**, and then click **All Windows Computers**.

3.  In the **All Windows Computers** view, filter for the computer for which you want to create an incident, and then select the computer. For example, select **Exchange01.woodgrove.com**.

4.  In the **Tasks** pane, click **Create Related Incident**.

5.  In the **Tasks** pane, click **Apply Template**.

6.  Under **Templates** in the **Apply Template** dialog box, select **Software Issue Incident Template**, and then click **OK**.

7.  In the **Title** box, type a new description or modify the description inserted by the template. For example, type **User unable to open e\-mail that has restricted permissions.**

8.  In the **Affected user** box, select the user who reported this incident. For example, select **Joe Andreshak**.

9. In the **Alternate Contact Method** box, enter additional contact information for the affected user \(optional\).

10. Click the **Related Items** tab.

11. In the **Attached Files** area, click **Add**.

12. In the **Open** dialog box, select the file that you want to attach to this incident, and then click **Open**. For example, select the screen shot of an error message that the affected user has received.

13. Click **OK**.

### To create a new incident by email

1.  In an email program, create a new email message, and enter the help desk alias or email address in the **To** box. For example, enter **Helpdesk@Helpdesk.Woodgrove.com** in the **To** box.

2.  In the **Subject** box, type a subject. For example, enter **Unable to print checks**.

3.  In the message body, type additional information that the help desk analyst can use to correct the problem. For example, enter **The check printer has a paper jam. I will use a backup printer until the jam is fixed**.

4.  Optionally, attach files that the help desk analyst can use to correct the problem.

### To validate creation of a new incident

1.  In the Service Manager console, click **Work Items**.

2.  In the **Work Items** pane, expand **Incident Management**, and then click **All Incidents**. New incidents appear in the **All Incidents** view.

## See Also
