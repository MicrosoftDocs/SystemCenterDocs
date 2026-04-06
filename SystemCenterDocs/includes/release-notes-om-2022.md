---
title: include file
description: include file that summarizes the release notes for Operations Manager 2022.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 03/09/2026
ms.service: system-center
ms.assetid:
ms.subservice: operations-manager
ms.topic: include
ms.update-cycle: 1095-days
---

## Operations Manager 2022 release notes

This article summarizes the release notes for Operations Manager 2022.

### *Show/Hide Details* error in Web Console

**Description**: In the System Center Operations Manager Web Console, the **Show/Hide Details** option in Health Explorer fails and shows a **ToggleDisplayMode is not defined** error.

**Workaround**: Add the following script to *ViewTypeHealthExplorer.aspx* within the `head` section so the function is available in the global scope before UpdatePanel content is injected.

```javascript
<script type="text/javascript">
function ToggleDisplayMode(node)
{
    var tableHeader = document.getElementById(node);

    if (null != tableHeader)
    {
        var row = tableHeader.nextSibling;

        while (row != null)
        {
            if (row.style.display != "none")
                row.style.display = "none";
            else
                row.style.display = "";

            row = row.nextSibling;
        }
    }
}
</script>
```

###  Operations console fails to connect with Operations Manager 2019 management group

**Description**: Operations console for Operations Manager 2022 fails to connect with Operations Manager 2019 management group.

**Workaround**:
- Use Operations Manager 2019 operations console to connect with Operations Manager 2022 management group.

  or

- Use separate console machines for Operations Manager 2019 and Operations Manager 2022, and use them to connect to the respective servers.
