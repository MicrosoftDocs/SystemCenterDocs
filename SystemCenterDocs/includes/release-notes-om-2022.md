---
title: include file
description: include file that summarizes the release notes for Operations Manager 2022.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 15/05/2026
ms.service: system-center
ms.assetid:
ms.subservice: operations-manager
ms.topic: include
ms.update-cycle: 1095-days
---

## Operations Manager 2022 UR3 hotfix release notes

The following sections summarize the release notes for Operations Manager 2022 UR3, and include the known issues and workarounds.

For the problems fixed in UR3 hotfix and the installation instructions for UR3 hotfix, see the [KB article](https://support.microsoft.com/kb/5071859).

### Known issue 

After you install 2022 UR3 hotfix, the updated hotfix version doesn't immediately appear in the Operations Console. This issue is limited to the version of display only and doesn't affect the installation or functionality of the hotfix.

### Management Pack Update behavior 

**Description**: The following Management Packs included in this hotfix might not update automatically after installation. 
- Microsoft.SystemCenter.DataWarehouse.Report.Library.mp 
- Microsoft.SystemCenter.DataWarehouse.ChangeTrackingReport.Library.mp 
- Microsoft.SystemCenter.DataWarehouse.Reports.mp 
- Microsoft.SystemCenter.DataWarehouse.ServiceLevel.Report.Library.mp 
- Microsoft.SystemCenter.OperationsManager.Reports.2007.mp 
- ODR.mp 

**Workaround**: Manually import the updated Management Packs included in the hotfix package. For more information about how to import Management Packs, see [Import, export, and remove an Operations Manager management pack](/system-center/scom/manage-mp-import-remove-delete?view=sc-om-2025).

## Operations Manager 2022 release notes

The following sections summarize the release notes for Operations Manager 2022, and include the known issues and workarounds.

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
