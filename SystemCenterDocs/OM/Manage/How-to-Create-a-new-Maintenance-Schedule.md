---
title: How to Create a new Maintenance Schedule
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cecbf000-42f3-4c50-9edc-98600f50e1bf
---
# How to Create a new Maintenance Schedule
Maintenance mode is a feature in Operations Manager to suspend monitoring of an object during regular software or hardware maintenance activities such as software updates or hardware replacements. When an object is placed into Maintenance Mode, all work\-flows targeted against that object are suspended during that specific interval.

## Maintenance Schedules
You can see all the entities in your environment that are in Maintenance mode by opening the Maintenance Schedule screen from the Operations Manager Administration Pane. You can create new maintenance schedules from this screen.

##### To Create a new Maintenance Schedule

1.  Click Create Maintenance Schedule

2.  Select objects to add to the schedule by clicking on the Add\/Remove objects button and clicking on the named objects to add them to the list.

3.  Select either to only add the items you have added to the list, or, to add items contained within the listed item, by selecting either the **Selected Objects Only** or the **Selected Objects and all their contained objects**, button.

    An example of objects contained within other objects would be a computer and the services running on that computer, such as the SQL Service, or IIS.

4.  Set the frequency, duration and start date  for the maintenance schedule by selecting the appropriate items from the scheduling screen.

5.  Add a name to the schedule on the details screen, select the category from the drop\-down list, and click finish to complete creation of the schedule.

    You can also prevent the schedule from starting by removing the check from  the **Enable Schedule c**heck\-box.


