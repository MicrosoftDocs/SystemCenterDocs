---
title: Optimize the size of staging folders
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8a66fda-b6ab-4a0d-8fe3-adeb2eb5489f
---
# Optimize the size of staging folders
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>DFS Replication uses staging folders for each replicated folder to act as caches for new and changed files that are ready to be replicated from sending members to receiving members. These files are stored under the local path of the replicated folder in the DfsrPrivate\Staging folder. </para>
    <para>By default, the quota size of each staging folder is 4,096 MB, and the quota size of each Conflict and Deleted folder is 660 MB. The size of each folder on a member is cumulative per volume, so if there are multiple replicated folders on a member, DFS Replication creates multiple staging and Conflict and Deleted folders, each with its own quota.</para>
    <para>Optimizing the size of the staging folder can improve performance and reduce the likelihood of replication failing. When adjusting the size of the staging folder, consider the following factors: </para>
    <list class="bullet">
      <listItem>
        <para>If a staging folder quota is configured to be too small, DFS Replication might consume additional CPU and disk resources to regenerate the staged files. Replication might also slow down, or even stop, because the lack of staging space can effectively limit the number of concurrent transfers with partners.</para>
        <alert class="important">
          <para>For the initial replication of existing data on the primary member, the staging folder quota must be large enough so that replication can continue even if multiple large files remain in the staging folder because partners cannot promptly download the files.</para>
          <para>To properly size the staging folder for initial replication, you must take into account the size of the files to be replicated. At a minimum, the staging folder quota should be at least the size of the 32 largest files in the replicated folder, or the 16 largest files for read-only replicated folders. To improve performance, set the size of the staging folder quota as close as possible to the size of the replicated folder.</para>
          <para>To determine the size of the largest files in a replicated folder using Windows Explorer, sort by size and add the 32 largest file sizes (16 if it’s a read-only replicated folder) to get the minimum staging folder size. To get the recommended minimum staging folder size (in gigabytes) from a Windows PowerShell® command prompt, use this Windows PowerShell command where <placeholder>&lt;replicatedfolderpath&gt;</placeholder> is the path to the replicated folder (change <codeInline>32</codeInline> to <codeInline>16</codeInline> for read-only replicated folders): </para>
          <para>
            <codeInline>(Get-ChildItem</codeInline> <placeholder> &lt;replicatedfolderpath&gt;</placeholder><codeInline> -recurse –force | Sort-Object length -descending | select-object -first 32 | measure-object -property length -sum).sum /1gb</codeInline></para>
        </alert>
      </listItem>
      <listItem>
        <para>Increase the staging folder quota when you must replicate multiple large files that change frequently. </para>
      </listItem>
      <listItem>
        <para>If possible, increase the staging folder quota on hub members that have many replication partners. </para>
      </listItem>
      <listItem>
        <para>If free disk space is a concern, you might need to configure the staging quota to be lower than the default quota when several replicated folders share staging space on the same volume. </para>
      </listItem>
      <listItem>
        <para>During normal operation, if the event that indicates the staging quota (event ID 4208 in the DFS Replication event log) is over its configured size and is logged multiple times in an hour, increase the staging quota by 20 percent. </para>
      </listItem>
      <listItem>
        <para>To improve input/output (I/O) throughput, locate staging folders and replicated folders on different physical disks. This can be done by editing the path of the staging folder.</para>
      </listItem>
    </list>
    <alert class="note">
      <para>The staging quota for DFS Replication is not a hard limit, and it can grow over its configured size, unlike the staging quota for FRS. When the quota is reached, DFS Replication deletes old files from the staging folder to reduce the disk usage under the quota. The staging folder does not reserve hard disk space, and it only consumes as much disk space as is currently needed.</para>
    </alert>
  </introduction>
  <relatedTopics />
</developerConceptualDocument>