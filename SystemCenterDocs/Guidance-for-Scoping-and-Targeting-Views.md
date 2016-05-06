---
title: Guidance for Scoping and Targeting Views
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 32c6092a-6e1d-4bed-8b54-c3ddc49f53d8
---
# Guidance for Scoping and Targeting Views
In [!INCLUDE[om12long](../Token/om12long_md.md)], you can use groups to limit a view in the Operations console, making it easier to find the specific information you need. You can change the scope for any existing view \(other than dashboard views\) to a specific group; however, this change only applies to the user who makes it and does not persist when the console is restarted.

For persistent management, you can create views that are scoped to a specific group. You can also scope the following widgets in a dashboard view:

-   Alert

-   Instance Details

-   Performance

-   State

For example, after you create a group of objects, you can create a dashboard view in which each widget is targeted to the group, providing a single view for important information for the members of the group.

After you create views for the group, you can create a user role that is scoped to the group and limited to the views for that group, and then assign users to that user role. This enables the individuals with that user role to monitor the objects they are concerned with, while limiting them to information that only pertains to those objects.

## See Also
[Using Views in Operations Manager](../Topic/Using-Views-in-Operations-Manager.md)
[Standard Views in Operations Manager](../Topic/Standard-Views-in-Operations-Manager.md)
[Creating Views in Operations Manager](../Topic/Creating-Views-in-Operations-Manager.md)
[How to Personalize a View in Operations Manager](../Topic/How-to-Personalize-a-View-in-Operations-Manager.md)

