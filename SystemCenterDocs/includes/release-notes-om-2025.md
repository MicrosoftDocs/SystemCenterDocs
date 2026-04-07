---
title: include file
description: Include file that summarizes the release notes for Operations Manager 2025.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 03/31/2026
ms.service: system-center
ms.assetid:
ms.subservice: operations-manager
ms.topic: include
ms.update-cycle: 1095-days
---

## Operations Manager 2025 UR1 release notes

The following sections summarize the release notes for Operations Manager 2025 UR1, and include the known issues and workarounds.

For the problems fixed in UR1 and the installation instructions for UR1, see the [KB article](https://support.microsoft.com/kb/5068304).

### File `KB5068304-amd64-Agent.msp` isn't automatically copied

**Description**: After you apply System Center Operations Manager 2025 UR1 Gateway Patch, the file **KB5068304-amd64-Agent.msp** isn't automatically copied to the `AgentManagement\amd64` directory.

**Workaround**: Manually copy the **KB5068304-amd64-Agent.msp** file into the `AgentManagement\amd64` folder.

### Known issue

The **About** page on Operations Console shows RTM version (10.25.10324.0) instead of UR1 version. The accurate version number is displayed starting from Operations Manager 2025 UR2. To verify the accurate version, check **Operations Console** > **Management server** page.

### Resource pool communication issue

**Description**: After installation of System Center Operations Manager Update Rollup 1, resource pool stops sending heartbeats; Agents or gateways connected to secondary management servers are greyed out.

**Workaround**: Apply [System Center Operations Manager Update Rollup 1 hotfix](https://support.microsoft.com/kb/5080648).

## Operations Manager 2025 release notes

The following sections summarize the release notes for Operations Manager 2025, and include the known issues and workarounds.

- Fixed broken behavior of Web Console where allow-popups and allow-forms settings weren't added after applying security changes.
- Fixed failure of favorite reports with `HttpParseException` in Web Console.

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