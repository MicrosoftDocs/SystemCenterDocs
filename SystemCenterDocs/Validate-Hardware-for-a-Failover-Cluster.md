---
title: Validate Hardware for a Failover Cluster
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 140727a5-cfad-4f87-99da-fdefcc9865ab
---
# Validate Hardware for a Failover Cluster
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>You can use the Validate a Configuration Wizard, which is integrated in Failover Cluster Manager, or the <externalLink><linkText>Test-Cluster</linkText><linkUri>http://technet.microsoft.com/library/hh847274</linkUri></externalLink> <token>wps_Token> cmdlet, to run a set of focused validation tests. You can run this process on a collection of servers that you intend to use as nodes in a cluster. This tests the underlying hardware and software, directly and individually, to obtain an accurate assessment of how well Failover Clustering can be supported in a given configuration.</para>
    <alert class="important">
      <para>A cluster validation report is required by Microsoft as a condition of Microsoft support for a given configuration.</para>
    </alert>
    <para>This topic provides steps to validate the hardware for a failover cluster.</para>
    <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
      <thead>
        <tr>
          <TD>
            <para>Task</para>
          </TD>
          <TD>
            <para>Description</para>
          </TD>
        </tr>
      </thead>
      <tbody>
        <tr>
          <TD>
            <para>
              <link xlink:href="#BKMK_PREPARE">Step 1: Prepare to validate hardware for a failover cluster</link>
            </para>
          </TD>
          <TD>
            <para>Learn about cluster validation and Microsoft support for a cluster configuration, and prepare your hardware for the validation tests.</para>
          </TD>
        </tr>
        <tr>
          <TD>
            <para>
              <link xlink:href="#BKMK_RUN_TESTS">Step 2: Validate a new or existing failover cluster</link>
            </para>
          </TD>
          <TD>
            <para>Run the Validate a Configuration Wizard or the <externalLink><linkText>Test-Cluster</linkText><linkUri>http://technet.microsoft.com/library/hh847274</linkUri></externalLink> <token>wps_Token> cmdlet.</para>
          </TD>
        </tr>
        <tr>
          <TD>
            <para>
              <link xlink:href="#BKMK_VALIDATION_RESULTS">Step 3: Analyze validation results</link>
            </para>
          </TD>
          <TD>
            <para>Review the Summary Report that is created when validation completes. If there are failures and you need support, prepare a validation report for Microsoft Customer Service and Support.</para>
          </TD>
        </tr>
        <tr>
          <TD>
            <para>
              <link xlink:href="#BKMK_CHOOSE_TESTS">Advanced validation scenarios</link>
            </para>
          </TD>
          <TD>
            <para>Review these advanced scenarios if you need to validate an existing cluster and choose to test only certain aspects of cluster functionality.</para>
          </TD>
        </tr>
        <tr>
          <TD>
            <para>
              <link xlink:href="#BKMK_FAQ">Frequently asked questions</link>
            </para>
          </TD>
          <TD>
            <para>Get answers to your questions about the cluster validation process.</para>
          </TD>
        </tr>
      </tbody>
    </table>
  </introduction>
  <section address="BKMK_PREPARE">
    <title>Step 1: Prepare to validate hardware for a failover cluster</title>
    <content />
    <sections>
      <section>
        <title>What is cluster validation?</title>
        <content>
          <para>The Validate a Configuration Wizard or the <externalLink><linkText>Test-Cluster</linkText><linkUri>http://technet.microsoft.com/library/hh847274</linkUri></externalLink> <token>wps_Token> cmdlet enables you to run a set of focused tests on a collection of servers, networks, and associated storage that are planned for use as a failover cluster. The cluster validation process tests the underlying hardware and software to obtain an accurate assessment of how well Failover Clustering can be supported in a given configuration.</para>
          <para>Before you create a failover cluster, we strongly recommend that you run all the cluster validation tests.</para>
          <para>Cluster validation is intended to do the following: </para>
          <list class="bullet">
            <listItem>
              <para>Find hardware or configuration issues before a failover cluster goes into production.</para>
            </listItem>
            <listItem>
              <para>Help ensure that the clustering solution you deploy is dependable.</para>
            </listItem>
            <listItem>
              <para>Provide a way to validate changes to the hardware of an existing cluster.</para>
            </listItem>
            <listItem>
              <para>Perform diagnostic tests on an existing cluster.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section address="BKMK_SUPPORT">
        <title>Supported cluster configurations </title>
        <content>
          <para>For Microsoft Customer Service and Support to officially support a failover cluster in <token>winblue_server_Token> or <token>win8_server_Token>, the cluster solution must meet the following criteria:</para>
          <list class="bullet">
            <listItem>
              <para>All hardware and software components must meet the qualifications for the appropriate logo. For <token>winblue_server_Token>, this is the "Certified for <token>winblue_server_Token>" logo. For <token>win8_server_Token>, this is the "Certified for <token>win8_server_Token>" logo. For more information, see <externalLink><linkText>Logo Program Requirements and Policies</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkId=111561</linkUri></externalLink> on the Microsoft website. The following are descriptions of the logos.</para>
              <list class="bullet">
                <listItem>
                  <para>
                    <embeddedLabel>Certified <token>winblue_server_Token> Systems</embeddedLabel>
                  </para>
                  <para>The Certified for <token>winblue_server_Token> logo demonstrates that a server system meets Microsoft’s highest technical bar for security, reliability and manageability; and with other certified devices and drivers, it can support the roles, features and interfaces for Cloud and Enterprise workloads, as well as business critical applications.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Certified <token>winblue_server_Token> Devices</embeddedLabel>
                  </para>
                  <para>The Certified for <token>winblue_server_Token> logo demonstrates that a server system meets Microsoft’s highest technical bar for security, reliability and manageability; and with other certified devices and drivers, it can support the roles, features and interfaces for Cloud and Enterprise workloads, as well as business critical applications.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Certified for <token>win8_server_Token> Devices</embeddedLabel>
                  </para>
                  <para>Designed for line-of-business and mission-critical applications, the Certified for <token>win8_server_Token> logo demonstrates that your solution meets Microsoft’s highest technical bar for Windows fundamentals and platform compatibility. </para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Certified <token>win8_server_Token> Systems</embeddedLabel>
                  </para>
                  <para>Designed for cloud and infrastructure workloads, as well as business critical applications, the Microsoft Certified for <token>win8_server_Token> logo demonstrates that a server system meets Microsoft’s highest technical bar for security, reliability, and manageability, and with any required hardware components, can support all the roles, features, and interfaces that are supported by <token>win8_server_Token>.</para>
                </listItem>
              </list>
            </listItem>
            <listItem>
              <para>The fully configured system (servers, network, and storage) must pass all the required tests in the Validate a Configuration Wizard, which you can run from Failover Cluster Manager. Alternatively, you can run the validation tests using the <externalLink><linkText>Test-Cluster</linkText><linkUri>http://technet.microsoft.com/library/hh847274</linkUri></externalLink> <token>wps_Token> cmdlet.</para>
            </listItem>
          </list>
          <para>Microsoft support policies are also described at the <externalLink><linkText>Microsoft Support</linkText><linkUri>http://support.microsoft.com/kb/2775067</linkUri></externalLink> website.</para>
        </content>
      </section>
      <section address="BKMK_validation_scenarios">
        <title>Common validation scenarios </title>
        <content>
          <para>The following lists describe scenarios in which hardware validation is required or is useful. In general, you need to run all the validation tests (some exceptions are noted).</para>
          <list class="bullet">
            <listItem>
              <para>
                <embeddedLabel>Validation before the cluster is configured</embeddedLabel>
              </para>
              <list class="bullet">
                <listItem>
                  <para>
                    <embeddedLabel>A set of servers ready to become a failover cluster</embeddedLabel> </para>
                  <para>This is the most straightforward validation scenario. The hardware components (systems, networks, and storage) are connected, but the systems are not functioning as a cluster. Running tests in this situation has no impact on availability.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Cloned or imaged systems</embeddedLabel> </para>
                  <para>With systems that you have cloned or imaged to different hardware, you must run the Validate a Configuration Wizard as you would with any new cluster. We recommend that you run the wizard just after you connect the hardware components and install the Failover Clustering feature, before the cluster is used by clients.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Virtualized servers</embeddedLabel> </para>
                  <para>With virtualized servers in a cluster, run the Validate a Configuration Wizard as you would with any new cluster. The requirement for running the wizard is the same whether you have a "host cluster" (failover occurs between two physical computers), a "guest cluster" (failover occurs between guest operating systems on the same physical computer), or some other configuration that includes one or more virtualized servers.</para>
                </listItem>
              </list>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Validation when the cluster has only one node</embeddedLabel> </para>
              <para>You might want to run a limited number of validation tests on a single server that you intend to use in a cluster. Some tests cannot be run in this situation; for example, tests that confirm the software and software updates match between servers, and storage tests that simulate failover between nodes. You must have at least two nodes in a cluster before you can complete the cluster validation process. So if you bring more servers into the configuration, you must run the Cluster Validation Wizard again so that all the tests can be complete.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Validation after the cluster is configured and in use</embeddedLabel>
              </para>
              <list class="bullet">
                <listItem>
                  <para>
                    <embeddedLabel>To confirm validation for Microsoft support, or to rule out configuration problems</embeddedLabel> </para>
                  <para>If you need support from Microsoft, you may be required to you provide the validation report from the wizard. If you have not already run the wizard and saved the report, you might need to take the cluster offline to run the wizard. The report shows whether your configuration is supported, and it can help Microsoft customer support troubleshoot configuration issues with hardware, drivers, and the basic system configuration.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Before adding a node</embeddedLabel> </para>
                  <para>When you add a server to a cluster, we strongly recommend that you start by connecting the server to the cluster networks and storage and then run the Validate a Configuration Wizard, specifying the existing cluster nodes and the new node.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>When attaching new storage</embeddedLabel> </para>
                  <para>When you attach new storage to the cluster (which is different than exposing a new logical unit number (LUN) in existing storage), you must run the Validate a Configuration Wizard to confirm that the new storage will function correctly. To minimize the impacts to availability, we recommend that you run the wizard after you attach the storage, and before you begin to use the new LUNs in clustered services or applications.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>When making changes that affect firmware or drivers</embeddedLabel> </para>
                  <para>If you want to upgrade or make other changes to the cluster that would require changing the firmware or drivers, you must run the Validate a Configuration Wizard to confirm that the new combination of hardware, firmware, drivers, and software supports your failover cluster functionality. If the change affects the firmware or drivers for storage, we recommend that you keep a small LUN available (unused by clustered roles) so that you can run the storage validation tests without taking your clustered roles offline. For more information about running storage tests on a small unused LUN, see <link xlink:href="#BKMK_CONS_EXIST">Considerations for validating an existing cluster</link>.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>After restoring a system from backup</embeddedLabel> </para>
                  <para>After you restore a system from backup, run the Validate a Configuration Wizard to confirm that the system can function properly as part of a cluster. The system is not considered a supported system until the validation tests are completed.</para>
                </listItem>
              </list>
            </listItem>
          </list>
          <para>When you validate hardware changes to an existing cluster (as an advanced scenario), you might decide to omit certain storage tests. For more information and considerations, see <link xlink:href="#BKMK_CHOOSE_TESTS">Advanced Validation Scenarios</link>. </para>
        </content>
      </section>
      <section>
        <title>Categories of validation tests</title>
        <content>
          <para>The following table lists the categories of validation tests. The tests in each category are listed at the time you run the Validate a Configuration Wizard. A description of each test in each category is provided in the validation report that is saved after validation completes.</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Category</para>
                </TD>
                <TD>
                  <para>Description</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Cluster configuration</para>
                </TD>
                <TD>
                  <para>Lists and validates the resources that are configured for use in a cluster, including clustered roles and cluster volumes.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Hyper-V configuration</para>
                </TD>
                <TD>
                  <para>Validates the Hyper-V configuration for use in a failover cluster.</para>
                  <alert class="note">
                    <para>Hyper-V configuration tests are only required if you use or plan to use clustered virtual machines.</para>
                  </alert>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Inventory</para>
                </TD>
                <TD>
                  <para>Lists host bus adapters (HBAs), devices, processes, and drivers that are in use on the computers in the cluster.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Network</para>
                </TD>
                <TD>
                  <para>Validates the configuration of the cluster networks, IP addresses, and Windows Firewall.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Storage</para>
                </TD>
                <TD>
                  <para>Validates storage disks and file systems that are available for use in a failover cluster.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>System configuration</para>
                </TD>
                <TD>
                  <para>Validates operating systems, update levels, and service settings on the computers in the cluster.</para>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
    </sections>
  </section>
  <section address="BKMK_RUN_TESTS">
    <title>Step 2: Validate a new or existing failover cluster</title>
    <content>
      <para>This step provides procedures for running the Validate a Configuration Wizard or the <externalLink><linkText>Test-Cluster</linkText><linkUri>http://technet.microsoft.com/library/hh847274</linkUri></externalLink> <token>wps_Token> cmdlet to validate a new or existing failover cluster.</para>
      <alert class="important">
        <para>To begin the process of adding hardware (such as an additional server) to a failover cluster, connect the hardware to the failover cluster. Then run the Validate a Configuration Wizard, and specify all servers that you want to include in the cluster. The wizard tests cluster connectivity and failover, not only isolated components (such as individual servers).</para>
      </alert>
      <procedure>
        <title>To run the Validate a Configuration Wizard</title>
        <steps class="ordered">
          <step>
            <content>
              <para>Identify the server or servers that you want to test.</para>
              <list class="bullet">
                <listItem>
                  <para>If the cluster does not yet exist, choose the servers that you want to include in the cluster, and make sure that you have installed the Failover Clustering feature on those servers. If the feature is not installed, see the <externalLink><linkText>installation instructions</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkId=253342</linkUri></externalLink>.</para>
                </listItem>
                <listItem>
                  <para>If the cluster already exists, make sure that you know the name of the cluster or a node in the cluster.</para>
                </listItem>
              </list>
            </content>
          </step>
          <step>
            <content>
              <para>Review the cluster requirements for the hardware for the network or the storage that you want to validate, and confirm that it is connected to the servers. </para>
            </content>
          </step>
          <step>
            <content>
              <para>Decide whether you want to run all or only some of the available validation tests. In general, we recommend that you run all the tests, but the follow general guidelines can help you decide.</para>
              <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                <thead>
                  <tr>
                    <TD>
                      <para>Type of cluster</para>
                    </TD>
                    <TD>
                      <para>Validation tests</para>
                    </TD>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <TD>
                      <para>New or planned cluster with all hardware connected</para>
                    </TD>
                    <TD>
                      <para>All tests</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>New or planned cluster with parts of the hardware connected</para>
                    </TD>
                    <TD>
                      <para>System Configuration tests, Inventory tests, and tests that apply to the hardware that is connected (that is, network tests if the network is connected or storage tests if the storage is connected)</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Existing cluster to which you plan to add a server</para>
                    </TD>
                    <TD>
                      <para>All tests</para>
                      <alert class="note">
                        <para>Before you run the tests, be sure to connect the networks and storage for all servers that you plan to have in the cluster.</para>
                      </alert>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Troubleshooting an existing cluster</para>
                    </TD>
                    <TD>
                      <para>All tests, although you could run only the tests that relate to the apparent issue.</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
              <alert class="important">
                <para>If a clustered role is using a disk when you start the wizard, the wizard will prompt you about whether to take that clustered role offline for the purposes of testing. If you choose to take a clustered role offline, it will remain offline until the tests finish.</para>
              </alert>
            </content>
          </step>
          <step>
            <content>
              <para>To open the wizard, in Failover Cluster Manager, under <ui>Actions</ui>, click <ui>Validate Configuration</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Follow the instructions in the wizard to specify the servers (in a planned cluster) and the tests. For example, if you do not plan to use cluster features that require Hyper-V, you can omit the Hyper-V Configuration tests. The wizard then guides you to run the tests.</para>
              <alert class="note">
                <para>When you run the wizard on unclustered servers, you must enter the names of all the servers that you want to test, not only one.</para>
              </alert>
            </content>
          </step>
          <step>
            <content>
              <para>The <ui>Summary</ui> page appears after the tests run. On the <ui>Summary</ui> page, click <ui>View Report</ui> to view the test results.</para>
              <para>To view the results of the tests after you close the wizard, under <ui>Actions</ui> in Failover Cluster Manager, click <ui>View Validation Report</ui>. You can see %SystemRoot%\Cluster\Reports\Validation Report <placeholder>date and time</placeholder><ui>.html</ui> where %SystemRoot% is the folder in which the operating system is installed (for example, C:\Windows).</para>
            </content>
          </step>
        </steps>
      </procedure>
      <para>
        <mediaLinkInline>
          <image xlink:href="eda3e676-68d6-4a56-90af-dd29179cfd9b" />
        </mediaLinkInline>
        <embeddedLabel>
          <token>wps_proc_titlToken>
        </embeddedLabel>
      </para>
      <para>
        <token>wps_proc_intrToken>
      </para>
      <para>The following example runs all cluster validation tests on the nodes named <placeholder>node1</placeholder> and <placeholder>node2</placeholder>. If <placeholder>node1</placeholder> or <placeholder>node2</placeholder> is already a member of a cluster, the tests will include all nodes in that cluster.</para>
      <code language="powershell">Test-Cluster -Node node1,node2</code>
    </content>
  </section>
  <section address="BKMK_VALIDATION_RESULTS">
    <title>Step 3: Analyze validation results </title>
    <content>
      <para>After the Validate a Configuration Wizard has completed, the Failover Cluster Validation Report displays the results. All tests must pass with a green check mark, or in some cases, a yellow triangle (warning). The following table shows the symbols in the summary and explains what they mean:</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD colspan="1">
              <para>Symbol</para>
            </TD>
            <TD colspan="1">
              <para>Explanation</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <mediaLink>
                <image xlink:href="b4b0a6c7-cf6a-4aba-aff7-9b21af73701e" />
              </mediaLink>
            </TD>
            <TD colspan="1">
              <para>The corresponding validation test passed, indicating that this aspect of the cluster can be supported.</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <mediaLink>
                <image xlink:href="4ae14450-cf2c-46dd-b5ce-6051005a2c8f" />
              </mediaLink>
            </TD>
            <TD colspan="1">
              <para>The corresponding validation test produced a warning, indicating that this aspect of the cluster can be supported, but it might not meet the recommended best practices, and it should be reviewed. Microsoft customer support might ask you to investigate or address the issue if it appears to be directly linked to something that you are troubleshooting.</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <mediaLink>
                <image xlink:href="dd2bd171-ed45-4303-b07a-86a4f7bf230c" />
              </mediaLink>
            </TD>
            <TD colspan="1">
              <para>The corresponding validation test failed, and this aspect of the cluster is not supported. You must correct the issue before you can create a failover cluster that is supported.</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <mediaLink>
                <image xlink:href="bdbdde1d-5adc-43c0-a36f-7c466ad8ff2f" />
              </mediaLink>
            </TD>
            <TD colspan="1">
              <para>The corresponding validation test was canceled. This can occur when the test depended on another test that did not complete successfully.</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <para>When you look for problem areas (warning or failures), in the test results summary, click an individual test to review the details. Also review the summary statement for information about whether the cluster is a supported configuration.</para>
      <para>After you take action to correct the problem, you can rerun the wizard as needed to confirm that the configuration passes the tests.</para>
    </content>
    <sections>
      <section address="BKMK_if_fail">
        <title>What to do if a validation test fails</title>
        <content>
          <para>In most cases, if any tests in the Validate a Configuration Wizard fail, Microsoft does not consider the configuration to be supported. </para>
          <para>If any of the Hyper-V Configuration tests fail, Hyper-V on the cluster is not configured correctly. The problem must be corrected before the virtual machines in the cluster can be supported. However, failures in this category of tests do not mean that the cluster is not supported for workloads other than clustered virtual machines.</para>
          <para>The type of test that fails is a guideline to the corrective action to take. For example, if the <ui>List All Disks</ui> storage test fails, and subsequent storage tests do not run (because they would also fail), you should contact the storage vendor to troubleshoot this issue. Similarly, if a network test that is related to IP addresses fails, consult your network infrastructure team. Not all warnings or errors indicate a need to call Microsoft customer support. Most of the warnings or errors should result in working with internal teams or with a specific hardware vendor.</para>
          <para>For information about correcting failures that are listed in a validation report, see the previous section, <link xlink:href="#BKMK_validation_results">Understanding validation results</link>.</para>
          <para>After the issues have been addressed and resolved, it is necessary to rerun the Validate a Configuration Wizard. To be considered a supported configuration, all tests are required to run and complete without failures.</para>
        </content>
      </section>
      <section address="BKMK_PROVIDE_REPORT">
        <title>Provide a validation report when you request support from Microsoft </title>
        <content>
          <para>If you need to contact Microsoft customer support about a validation problem, the support team will help you collect the validation report and other relevant configuration files by using the Microsoft Support Diagnostic Tool (MSDT). (This feature replaces the MPSReports data collection utility.) If needed, Microsoft will send instructions about how to capture the data. In some situations, Microsoft may request that the contents of the C:\Windows\Cluster\Reports folder be zipped and sent for analysis. Either method will collect the required cluster validation report.</para>
        </content>
      </section>
      <section>
        <title>Updates to validation tests</title>
        <content>
          <para>The Validate a Configuration Wizard provides an accurate picture of how well failover clustering can be supported for a given configuration. If an update to the Validate a Configuration Wizard becomes available, you may need to rerun the wizard and pass all tests for your configuration to continue to be supported. This may result in some solutions that previously passed to fail. The issues that are reported in the updated tests will need to be addressed in the same manner as outlined in this guide.</para>
        </content>
      </section>
    </sections>
  </section>
  <section address="BKMK_CHOOSE_TESTS">
    <title>Advanced validation scenarios </title>
    <content>
      <para>When you make a change to an existing cluster, you might not need to run all the cluster validation tests. The following tables in this section list the kinds of changes you might make to a cluster and the corresponding tests to run.</para>
      <para>
        <embeddedLabel>Key for the required validation tests shown in the following tables</embeddedLabel>
      </para>
      <list class="bullet">
        <listItem>
          <para>
            <embeddedLabel>Full</embeddedLabel>: Run the complete set of tests. This requires some cluster downtime.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Single LUN</embeddedLabel>: Run the complete set of tests, and run the storage tests on only one LUN. The LUN might be a small LUN that you set aside for testing purposes or the witness disk (if your cluster uses a witness disk). This validates the storage subsystem, but not specifically each individual LUN or disk. You can run these validation tests without causing downtime to your clustered services or applications.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Omit storage tests</embeddedLabel>: Run the system configuration, inventory, and network tests, but not the storage tests. You can run these validation tests without causing downtime to your clustered roles.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>None</embeddedLabel>: No validation tests are needed.</para>
        </listItem>
      </list>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <caption>Server changes</caption>
        <thead>
          <tr>
            <TD colspan="1">
              <para>Change</para>
            </TD>
            <TD colspan="1">
              <para>Validation tests required</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>Physically replacing or changing a server that is used in the cluster</para>
            </TD>
            <TD colspan="1">
              <para>Full</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Adding or removing CPUs</para>
            </TD>
            <TD colspan="1">
              <para>None</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Adding or removing RAM on a server</para>
            </TD>
            <TD colspan="1">
              <para>None</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Adding, removing, or replacing a network adapter</para>
            </TD>
            <TD colspan="1">
              <para>Omit storage tests</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Updating firmware or an existing network driver</para>
            </TD>
            <TD colspan="1">
              <para>Omit storage tests</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Changing the BIOS settings or firmware version</para>
            </TD>
            <TD colspan="1">
              <para>None</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Adding or changing peripheral devices other than network or storage components, such as CD-ROM or DVD drives, tape drives, video cards, sound devices, and USB devices</para>
            </TD>
            <TD colspan="1">
              <para>None</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <caption>Operating system changes</caption>
        <thead>
          <tr>
            <TD colspan="1">
              <para>Change</para>
            </TD>
            <TD colspan="1">
              <para>Validation tests required</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>Applying operating system service pack, software updates, or hotfixes that affect the storage stack</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Applying software updates or hotfixes that do not affect the storage stack</para>
            </TD>
            <TD colspan="1">
              <para>Omit storage tests</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Installing an application that has no kernel mode or filter drivers</para>
            </TD>
            <TD colspan="1">
              <para>None</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Changing or adding new kernel mode drivers</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <caption>Cluster configuration changes</caption>
        <thead>
          <tr>
            <TD colspan="1">
              <para>Change</para>
            </TD>
            <TD colspan="1">
              <para>Validation tests required</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>Adding a new node to the cluster</para>
            </TD>
            <TD colspan="1">
              <para>Full</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Adding a new node that uses dissimilar hardware</para>
            </TD>
            <TD colspan="1">
              <para>Full</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Removing a node from the cluster</para>
            </TD>
            <TD colspan="1">
              <para>None</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Changing the quorum configuration</para>
            </TD>
            <TD colspan="1">
              <para>None</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <caption>Shared storage changes</caption>
        <thead>
          <tr>
            <TD colspan="1">
              <para>Change</para>
            </TD>
            <TD colspan="1">
              <para>Validation tests required</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>Changing or adding a storage array</para>
            </TD>
            <TD colspan="1">
              <para>Full</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Adding another SCSI hardware RAID unit of the same type, and that unit uses an HBA that is already in the configuration</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Making a minor (0.x) revision to the storage firmware</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Making a major (X.0) revision to the storage firmware</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Presenting a new disk or LUN to a cluster</para>
            </TD>
            <TD colspan="1">
              <para>Full, but test new LUNs only</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <caption>SAN (switch/hub) changes</caption>
        <thead>
          <tr>
            <TD colspan="1">
              <para>Change</para>
            </TD>
            <TD colspan="1">
              <para>Validation tests required</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>Adding or replacing a Fibre Channel switch or hub</para>
            </TD>
            <TD colspan="1">
              <para>Full</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Changing the number of ports within a switch block</para>
            </TD>
            <TD colspan="1">
              <para>None</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Making a minor (0.x) revision to the Fibre Channel switch firmware</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Making a major (X.0) revision to the Fibre Channel switch firmware</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Changing a switch configuration or zoning</para>
            </TD>
            <TD colspan="1">
              <para>Full, but test changed LUNs only</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <caption>Host bus adapter (HBA) changes</caption>
        <thead>
          <tr>
            <TD colspan="1">
              <para>Change</para>
            </TD>
            <TD colspan="1">
              <para>Validation tests required</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>Replacing an HBA (same or different type)</para>
            </TD>
            <TD colspan="1">
              <para>Full</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Adding a new HBA (same or different type)</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Changing the HBA firmware or BIOS</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Changing the HBA driver version</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <caption>Multipath software changes</caption>
        <thead>
          <tr>
            <TD colspan="1">
              <para>Change</para>
            </TD>
            <TD colspan="1">
              <para>Validation tests required</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>Changing from single path to multipath or multipath to single path</para>
            </TD>
            <TD colspan="1">
              <para>Full</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Adding a path</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Removing a path</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Updating the device specific module (DSM) version</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Changing to a DSM of a different type, for example, a DSM from a different provider</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <caption>Multisite cluster changes</caption>
        <thead>
          <tr>
            <TD colspan="1">
              <para>Change</para>
            </TD>
            <TD colspan="1">
              <para>Validation tests required</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>Modifying the networks that connect the nodes</para>
            </TD>
            <TD colspan="1">
              <para>Omit storage tests</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Making a minor (0.x) version change in the data replication software</para>
            </TD>
            <TD colspan="1">
              <para>Single LUN</para>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>Making a major (X.0) version change in the data replication software, or changing to a different type of replication software</para>
            </TD>
            <TD colspan="1">
              <para>Full</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <caption>Networking changes</caption>
        <thead>
          <tr>
            <TD colspan="1">
              <para>Change</para>
            </TD>
            <TD colspan="1">
              <para>Validation tests required</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>Modifying network firmware, software, or hardware</para>
            </TD>
            <TD colspan="1">
              <para>Omit storage tests</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
    <sections>
      <section>
        <title>Including storage tests</title>
        <content>
          <para>When you perform cluster validation tests on a configured cluster, you might not always run all storage tests. This section explains what to consider if you include storage tests or do not include storage tests.</para>
        </content>
        <sections>
          <section>
            <title>Considerations when you include storage tests</title>
            <content>
              <para>The Validate a Configuration Wizard runs all storage tests by default. All or some of the storage tests can be unselected by choosing the <ui>Run only tests I select</ui> option on the <ui>Testing Options</ui> page of the wizard. When storage tests are included, the <ui>Review Storage Status</ui> page of the wizard shows all of the disks and storage pools in the cluster and allows you to select the disks and storage pools to include in the storage tests. Storage tests require that a disk or storage pool that is assigned to a clustered role or Cluster Shared Volume be taken offline first. Therefore, anything using the storage will not have access to it during the storage tests. We recommend that any clustered role or other process that may be using the disk or storage pool is taken offline before the storage is included in the storage validation tests. </para>
              <para>The <externalLink><linkText>Test-Cluster</linkText><linkUri>http://technet.microsoft.com/library/hh847274</linkUri></externalLink> <token>wps_Token> cmdlet runs all storage tests by default. You can specify the <system>–Include</system> parameter to only run storage tests or to run a specific storage test. You can use the <system>–Disk</system> and <system>-Pool</system> parameters to enable targeted storage validation. The <system>–Disk</system> parameter or the <system>–Pool</system> parameter allows specifying, respectively, one or more disks or one or more storage pools to include in the storage validation testing. If the <system>–Disk</system> parameter or the <system>–Pool</system> parameter is used to specify a disk or storage pool that is currently online and is assigned to a clustered role or Cluster Shared Volume, you must also specify the <system>–Force</system> parameter to validate the corresponding disk or storage pool; otherwise, you must ensure that the clustered disk or storage pool is offline before running the tests. If the <system>–Disk</system> parameter or the <system>–Pool</system> parameter is not specified, <system>Test-Cluster</system> runs storage tests on all disks and storage pools that are available for cluster use or that are in the cluster resource offline or failed state. We recommend that any clustered role or other process that may be using the disk or storage pool is taken offline before the storage is included in the validation testing. </para>
              <para>
                <embeddedLabel>Storage that is not directly connected to all nodes in the cluster</embeddedLabel>
              </para>
              <para>There may be cases where the cluster design includes storage that is not connected to all nodes in the cluster. A common example is in multisite clusters where cluster nodes in <placeholder>SiteA</placeholder> are connected to one set of storage, the nodes in <placeholder>SiteB</placeholder> are connected to a different set of storage, and a non-Microsoft replication solution is used to ensure that both sets of storage have the same data. Failover cluster detects this asymmetric storage configuration, so the disks in <placeholder>SiteA</placeholder> only validate with the <placeholder>SiteA</placeholder> nodes, and the disks in <placeholder>SiteB</placeholder> only validate with nodes in <placeholder>SiteB</placeholder>.</para>
              <para>One scenario where Microsoft customer support may request that you run validation tests on production clusters is when there is a cluster storage failure that could be caused by some underlying storage configuration change or problem. It may not be advisable to take a disk that is in use offline due to the availability impact it might have on the clustered roles that use it. In this situation, you can run validation tests (including storage tests) by creating or choosing a new LUN from the same shared storage device and presenting it to all nodes in the cluster. By testing this LUN, you can avoid disruption to clustered roles that are already online within the cluster and still test the underlying storage subsystem.</para>
              <para>If a failover cluster passed the full set of validation tests and has no future hardware or software changes, it will continue to be a supported configuration. However, when you perform routine updates to software components such as drivers and firmware, it may be necessary to rerun the Configuration Wizard to ensure that the current configuration of the failover cluster is supported. The following guidelines can help you decide when this is necessary:</para>
              <list class="bullet">
                <listItem>
                  <para>All components of the storage stack should be identical across all nodes in the cluster. It is required that multipath I/O (MPIO) software and Device Specific Module (DSM) software components be identical. We recommend that the mass-storage device controllers (that is, the host bus adapter (HBA), HBA drivers, and HBA firmware) that are attached to cluster storage be identical. If you use dissimilar HBAs, you should verify with the storage vendor that you are following their supported or recommended configurations. </para>
                </listItem>
                <listItem>
                  <para>A best practice is to keep a small LUN available to allow the Validate a Configuration Wizard to run tests on available storage without negatively impacting clustered roles. If Microsoft customer support requests that you run a full set of cluster validation tests, the wizard allows you to select that disk for the storage tests to verify that the storage is working properly.</para>
                </listItem>
              </list>
            </content>
          </section>
          <section>
            <title>Considerations when you do not include storage tests</title>
            <content>
              <para>System configuration tests, inventory tests, and network tests have very low overhead, and they can be performed without significant effect on servers in a cluster.</para>
              <para>Microsoft customer support might request that you validate a production cluster as part of normal troubleshooting procedures (not focused on storage). In this scenario, you will use the wizard to inventory hardware and software, perform network testing, and validate system configuration. There may be certain scenarios in which only a subset of the full tests are needed. For example, if you are troubleshooting a network issue on a production cluster, Microsoft customer support might request that you run only the hardware and software inventory and the network tests.</para>
            </content>
          </section>
        </sections>
      </section>
    </sections>
  </section>
  <section address="BKMK_FAQ">
    <title>Frequently asked questions</title>
    <content />
    <sections>
      <section>
        <title>If a cluster passes all tests in the Validate a Configuration Wizard, is it supported?</title>
        <content>
          <para>If all the hardware and software components in the cluster meet the qualifications for the "Certified for <token>winblue_server_Token>" or "Certified for <token>win8_server_Token>" logo, and the cluster passes the validation tests, it is considered to be supported by Microsoft Customer Service and Support for Failover Clustering. For more information, see <link xlink:href="#BKMK_SUPPORT">Supported cluster configurations</link> earlier in this guide.</para>
        </content>
      </section>
      <section>
        <title>Will failover cluster solutions be listed in the Windows Server Catalog?</title>
        <content>
          <para>No, Microsoft will not maintain a list of vendor solutions for failover clusters. However, many vendors list recommended failover cluster solutions and components on their websites.</para>
        </content>
      </section>
      <section>
        <title>How does Microsoft customer support check if the solution has been validated?</title>
        <content>
          <para>The Validate a Configuration Wizard generates a simple HTML report that clearly displays whether a solution has passed all tests. This report is collected as part of the standard diagnostics tool, MSDT.</para>
        </content>
      </section>
      <section>
        <title>What if I make a change to the cluster configuration, like add a node? Do I have to run the Validate a Configuration Wizard again?</title>
        <content>
          <para>Yes, the Validate a Configuration Wizard should be run any time a change is made to an existing failover cluster. For more information, see <link xlink:href="#BKMK_validation_scenarios">Common validation scenarios</link> earlier in this guide.</para>
        </content>
      </section>
    </sections>
  </section>
  <section>
    <title>See also</title>
    <content>
      <list class="bullet">
        <listItem>
          <para>
            <legacyLink xlink:href="6eeffe4f-3558-495b-bcea-c640fe4d6c49">Failover Clustering Overview [Role/Tech Overview]</legacyLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <legacyLink xlink:href="c72342a0-7bf8-4e42-b8d2-b4a48659ba7c">Failover Clustering Hardware Requirements and Storage Options</legacyLink>
          </para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>

