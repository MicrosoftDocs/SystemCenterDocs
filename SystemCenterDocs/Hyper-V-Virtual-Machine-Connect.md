---
title: Hyper-V Virtual Machine Connect
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: 
  - hyper-v
  - techgroup-compute
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: deae35b9-7647-42b8-b6bf-45645a44c9c4
---
# Hyper-V Virtual Machine Connect
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>Virtual Machine Connection (VMConnect) is a tool that you use to connect to a virtual machine so that you can install or interact with the guest operating system in a virtual machine. Some of the tasks that you can perform by using VMConnect include <?Comment CN: What should I include about Enhanced Session mode? It is on by default for Client Hyper-V. 2014-05-07T15:44:00Z  Id='0?>the following<?CommentEnd Id='0'
    ?>:</para>
    <list class="bullet">
      <listItem>
        <para>Start and shut down a virtual machine</para>
      </listItem>
      <listItem>
        <para>Connect to a DVD image (.iso file) or a virtual floppy disk (.vfd file)</para>
      </listItem>
      <listItem>
        <para>Create a checkpoint</para>
      </listItem>
      <listItem>
        <para>Modify the settings of a virtual machine</para>
      </listItem>
    </list>
  </introduction>
  <section>
    <title>Keyboard shortcuts</title>
    <content>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Key combination</para>
            </TD>
            <TD>
              <para>Description</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>CTRL+ALT+LEFT arrow</para>
            </TD>
            <TD>
              <para>Mouse release</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>CTRL+ALT+END</para>
            </TD>
            <TD>
              <para>Equivalent of CTRL+ALT+DELETE in the virtual machine </para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>CTRL+ALT+BREAK</para>
            </TD>
            <TD>
              <para>Switch from full-screen mode back to windowed mode</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>CTRL+O</para>
            </TD>
            <TD>
              <para>Opens the settings for the virtual machine</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>CTRL+S</para>
            </TD>
            <TD>
              <para>Starts the virtual machine</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>CTRL+N</para>
            </TD>
            <TD>
              <para>Create a checkpoint</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>CTRL+E</para>
            </TD>
            <TD>
              <para>Revert to a checkpoint</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>CTRL+C</para>
            </TD>
            <TD>
              <para>Do a screen capture</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <section>
    <title>Tips for using VMConnect</title>
    <content>
      <para>You may find the following information helpful for using VMConnect:</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>To do this…</para>
            </TD>
            <TD>
              <para>Do this…</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>Send mouse clicks or keyboard input to the virtual machine</para>
            </TD>
            <TD>
              <para>Click anywhere in the virtual machine window. The mouse pointer may appear as a small dot when you connect to a running virtual machine.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Return mouse clicks or keyboard input to the physical computer</para>
            </TD>
            <TD>
              <para>Press CTRL+ALT+LEFT arrow and then move the mouse pointer outside of the virtual machine window. This mouse release key combination can be changed in the Hyper-V settings in Hyper-V Manager.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Send CTRL+ALT+DELETE key combination to a virtual machine</para>
            </TD>
            <TD>
              <para>Select <ui>Action</ui> &gt; <ui>Ctrl+Alt+Delete</ui> or use the key combination CTRL+ALT+END.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Switch from a window mode to a full-screen mode</para>
            </TD>
            <TD>
              <para>Select <ui>View</ui> &gt; <ui>Full Screen Mode</ui>. To switch back to window mode, press CTRL+ALT+BREAK.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Create a checkpoint to capture the current state of the machine for troubleshooting</para>
            </TD>
            <TD>
              <para>Select <ui>Action</ui> &gt; <ui>Checkpoint</ui> or use the key combination CTRL+N.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Change the settings of the virtual machine</para>
            </TD>
            <TD>
              <para>Select <ui>File</ui> &gt; <ui>Settings</ui>.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Connect to a DVD image (.iso file) or a virtual floppy disk (.vfd file)</para>
            </TD>
            <TD>
              <para>Select <ui>Media</ui>. </para>
              <para>Virtual floppy disks are not supported for generation 2 virtual machines. For more information about generation 2 virtual machines, see <legacyLink xlink:href="b1ddf7cd-dab8-4cc0-bd32-528f8df97540">Generation 2 Virtual Machine Overview</legacyLink>.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Use a host’s local resources on Hyper-V virtual machine like a USB drive</para>
            </TD>
            <TD>
              <para>Turn on enhanced session mode on the Hyper-V host, use VMConnect to connect to the virtual machine, and before you connect, choose the local resource that you want to use. For the specific steps, see <legacyLink xlink:href="18eface5-7518-4c6b-9282-93e2e3e87492">Use local resources on Hyper-V virtual machine with VMConnect</legacyLink>.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Change saved VMConnect settings for a virtual machine</para>
            </TD>
            <TD>
              <para>Run the following command in Windows PowerShell or the command prompt:</para><para>VMConnect.exe &lt;ServerName&gt; &lt;VMName&gt; /edit</para>
         
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Prevent a VMConnect user from taking over another user’s VMConnect session</para>
            </TD>
            <TD>
              <para>
                <legacyLink xlink:href="18eface5-7518-4c6b-9282-93e2e3e87492#BKMK_OVER">Turn on enhanced session mode on Hyper-V host</legacyLink>. </para>
              <para>Not having enhanced session mode turned on may pose a security and privacy risk. If a user is connected and logged on to a virtual machine through VMConnect and another authorized user connects to the same virtual machine, the session will be taken over by the second user and the first user will lose the session. The second user will be able to view the first user's desktop, documents, and applications.</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
    <sections>
      <section>
        <content />
        <sections>
          <section>
            <title>Additional references</title>
            <content>
              <list class="bullet">
                <listItem>
                  <para>
                    <legacyLink xlink:href="5aad349f-ef06-464a-b36f-366fbb040143">Hyper-V overview [Role/Tech Overview]</legacyLink>
                  </para>
                </listItem>
                <listItem>
                  <para>
                    <legacyLink xlink:href="8fac9371-ff4d-4ab7-9274-4c8175918b27">Client Hyper-V [redo]</legacyLink>
                  </para>
                </listItem>
                <listItem>
                  <para>
                    <legacyLink xlink:href="18eface5-7518-4c6b-9282-93e2e3e87492">Use local resources on Hyper-V virtual machine with VMConnect</legacyLink>
                  </para>
                </listItem>
                <listItem>
                  <para>
                    <legacyLink xlink:href="243b5705-96c9-4ec7-9ec5-c68a22b0d42d">Install Hyper-V and create a virtual machine</legacyLink>
                  </para>
                </listItem>
              </list>
            </content>
          </section>
        </sections>
      </section>
    </sections>
  </section>
  <relatedTopics />
</developerConceptualDocument>