---
description: This article describes the scheduling options for long-term protection.
ms.topic: article
ms.service: system-center
ms.date: 04/22/2025
title: Modify Long-Term Backup Schedule
ms.subservice: data-protection-manager
ms.assetid:
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
---

# Modify Long-Term Backup Schedule

This article describes the scheduling options for long-term protection.


You can use the **Modify Long-Term Schedule** screen to change your long-term backup schedule. The scheduling options depend on your retention range and backup frequency.

## Elements

|**Backup frequency**|**Scheduling options**|
|---|---|
|**Daily**|- Time for daily backup.<br>- Day of week and time for monthly backup.<br>- Date and time for yearly backup.|
|**Weekly**|- Day of week and time for weekly backup.<br>- Day of week and time for monthly backup.<br>- Date and time for yearly backup.|
|**Biweekly**|- Day of week and time for biweekly backup.<br>- Day of week and time for monthly backup.<br>- Date and time for yearly backup.|
|**Monthly**|- Date and time for monthly backup (monthly backups are performed on the specified day of the month).<br><br>Examples:<br>- If on Jan 10 you schedule a monthly backup to run on the 15th day of the month, the first backup will happen on January 15.<br>- If on Jan 10 you schedule a monthly backup to run on the 5th day of the month, then the first backup will happen on Feb 5.<br><br>- If you schedule a monthly backup within 24 hours from the current time and date, then the first backup will happen the next month on the specified day.<br><br>Example:<br>- If on Jan 10 3:00 P.M. you schedule a monthly backup to run on the 11th day of the month at 10:00 A.M., then the first backup will happen on Feb 11 10:00 A.M. and then every month thereafter.|
|**Quarterly**|- Date and time for quarterly backup (quarterly backups are performed in January, April, July, and October on the specified day of the month).<br><br>Examples:<br>- If on Jan 10 you schedule a quarterly backup to run on the 15th day of the month, the first backup will happen on January 15 and every three months thereafter.<br>- If on Jan 10 you schedule a quarterly backup to run on the 5th day of the month, then the first backup will happen on April 5 and then every three months thereafter.<br><br>- If you schedule a quarterly backup within 24 hours from the current time and date, then the first backup will happen the next quarter on the specified day and every three months thereafter.<br><br>Example:<br>- If on Jan 10 3:00 P.M. you schedule a quarterly backup to run on the 11th day of the month at 10:00 A.M., then the first backup will happen on April 11 at 10:00 A.M. and then every three months thereafter.|
|**Half-yearly**|- Date and time for half yearly backup (half yearly backups are performed two times in a year on the specified month and date).<br><br>Examples:<br>- If on January 10 2009 you schedule a half yearly backup to run on the January 15, then the first backup will happen on January 15 2009 and then every six months thereafter.<br>- If on January 10 2009 you schedule a half yearly backup to run on the January 5, then the first backup will happen on July 5 2009 and then every six months thereafter.<br><br>- If you schedule a half yearly backup within 24 hours from the current time and date, then the first backup will happen after six months on the specified month and date and then every six months thereafter.<br><br>Example:<br>- If on January 10 2009 3:00 P.M. you schedule a half yearly backup to run on the January 11 at 10:00 A.M., then the first backup will happen on July 11 2009 at 10:00 A.M. and then every six months thereafter.|
|**Yearly**|- Date and time for yearly backup (yearly backups are performed one time in a year on the specified month and date).<br><br>Examples:<br>- If on January 10 2009 you schedule a yearly backup to run on the January 15, then the first backup will happen on January 15 2009 and then every year thereafter.<br>- If on January 10 2009 you schedule a yearly backup to run on the January 5, then the first backup will happen on January 5 2010 and then every year thereafter.<br><br>If you schedule a yearly backup within 24 hours from the current time and date, then the first backup will happen the next year on the specified month and date and every year thereafter.<br><br>Example:<br>- If on January 10 2009 3:00 P.M. you schedule a yearly backup to run on the January 11 at 10:00 A.M., then the first backup will happen on January 11 2010 at 10:00 A.M. and then every year thereafter.|

After you modify the long-term backup schedule, select **OK**.
