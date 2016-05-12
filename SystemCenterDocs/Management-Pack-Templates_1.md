---
title: Management Pack Templates_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f50eed1-55a3-4a04-b0e6-eb0273c4c494
---
# Management Pack Templates_1
*Management Pack Templates* provide *Monitoring wizards* that let you create complete monitoring scenarios with minimal input. The wizard creates the required monitors, rules, and even targets to implement the particular scenario. There is no requirement for you to understand the management pack elements that are created. You can modify the configuration of the wizard itself if you want to change the way that monitoring is being performed.

**Conceptual view of a monitoring wizards**

![](Image/OM12Author_MonitoringWizard.gif)

If a management pack template is available for your particular monitoring requirement, using the template most likely is your best strategy. In many cases, you could create the individual rules and monitors yourself, but this exercise is significantly more complex than using an available template. In addition, some templates perform actions that you cannot perform in any other way in the Operations console.

The following table lists the management pack templates that are part of the standard [!INCLUDE[om12short](Token/om12short_md.md)] installation. You can install other management packs that might provide additional templates. Each of these templates is covered in detail in subsequent sections of this guide.

|Template|Description|
|------------|---------------|
|[.NET Application Performance Monitoring Template](.NET-Application-Performance-Monitoring-Template.md)|Monitor .NET applications to get details about application performance and reliability.|
|[OLE DB Data Source Template](OLE-DB-Data-Source-Template.md)|Monitor a database accessible with OLE DB.|
|[Process Monitoring Template](Process-Monitoring-Template.md)|Discover and monitor instances of a particular Windows process.|
|[TCP Port Template](TCP-Port-Template.md)|Monitor the availability of an application that is listening on a specific port.|
|[UNIX or Linux Log File](UNIX-or-Linux-Log-File.md)|Monitor a UNIX or Linux log file for a specific entry.|
|[UNIX or Linux Process](UNIX-or-Linux-Process.md)|Monitor a UNIX or Linux process.|
|[Web Application Availability Monitoring Template](Web-Application-Availability-Monitoring-Template.md)|Monitor the availability of one or more web application URLs and run these monitoring tests from internal locations.|
|[Web Application Transaction Monitoring Template](Web-Application-Transaction-Monitoring-Template.md)|Monitor the availability, operation, and performance of a web application.|
|[Windows Service Template](Windows-Service-Template.md)|Discover and monitor instances of a particular Windows service.|

## See Also
[Creating Management Pack Templates](Creating-Management-Pack-Templates.md)
[Watcher Nodes](Watcher-Nodes.md)


