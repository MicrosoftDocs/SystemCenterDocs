- name: Overview
  items: 
    - name: What is VMM?
      href: overview.md
    - name: VMM network object fundamentals
      href: network-object-fundamentals.md
    - name: Arc-enabled SCVMM
      href: about-arc-enabled-system-center-virtual-machine-manager.md
    - name: What's new in VMM
      href: whats-new-in-vmm.md
- name: Get Started
  items: 
    - name: VMM build versions
      href: release-build-versions.md
    - name: Release notes - VMM
      href: release-notes-vmm.md
    - name: Turn telemetry data on/off
      href: manage-telemetry.md
    - name: Deploy a VMM cloud
      href: deploy-cloud.md
      items: 
        - name: Create a VMM cloud
          href: cloud-create.md
        - name: Manage a VMM cloud
          href: cloud-manage.md
    - name: Deploy a guarded host fabric
      href: deploy-guarded-host-fabric.md
      items: 
        - name: Deploy guarded hosts
          href: guarded-deploy-host.md
        - name: Configure fallback HGS settings
          href: guarded-fallback-hgs.md
        - name: Deploy a shielded VHDX and VM template
          href: guarded-deploy-template.md
        - name: Deploy a shielded VM
          href: guarded-deploy-vm.md
        - name: Deploy a shielded Linux VM
          href: guarded-deploy-linux-vm.md
    - name: Deploy and manage a software defined network (SDN) infrastructure
      href: deploy-sdn.md
      items: 
        - name: Deploy an SDN network controller
          href: sdn-controller.md
        - name: Deploy an SDN SLB
          href: sdn-slb.md
        - name: Deploy an SDN RAS gateway
          href: sdn-gateway.md
        - name: Deploy SDN using PowerShell
          href: sdn-powershell.md
        - name: Set up a VM network in SDN
          href: sdn-create-network.md
        - name: Encrypt VM networks in SDN
          href: sdn-encrypt-networks.md
        - name: Allow and block VM traffic with SDN port ACLs
          href: sdn-port-acls.md
        - name: Control SDN virtual network bandwidth with QoS
          href: sdn-bandwidth-qos.md
        - name: Load balance network traffic
          href: sdn-load-balance-network-traffic.md
        - name: Set up NAT for traffic forwarding in an SDN
          href: sdn-set-up-nat.md
        - name: Route traffic across networks in the SDN infrastructure
          href: sdn-route-network-traffic.md
        - name: Configure SDN guest clusters
          href: sdn-guest-clusters.md
        - name: Update the NC server certificate
          href: sdn-update-nc-server-certificate.md
        - name: Set up SDN SLB VIPs
          href: sdn-configure-slb-vip.md
        - name: Back up and restore the SDN infrastructure
          href: sdn-backup-restore.md
        - name: Remove an SDN from VMM
          href: sdn-remove.md
        - name: Manage SDN resources in the VMM fabric
          href: network-sdn.md
    - name: Deploy and manage Storage Spaces Direct
      href: s2d.md
      items: 
        - name: Set up a hyper-converged Storage Spaces Direct cluster
          href: s2d-hyper-converged.md
        - name: Deploy and manage Azure Stack HCI clusters in VMM
          href: deploy-manage-azure-stack-hci.md
        - name: Set up a disaggregated Storage Spaces Direct cluster
          href: s2d-disaggregated.md
        - name: Manage Storage Spaces Direct clusters
          href: s2d-manage.md
        - name: Assign storage QoS policies for Clusters
          href: qos-storage-clusters.md
- name: How To
  items: 
    - name: Plan
      items: 
        - name: System requirements - VMM
          href: system-requirements.md
        - name: Plan VMM installation
          href: plan-install.md
        - name: Plan a VMM high availability deployment
          href: plan-ha-install.md
        - name: Identify VMM ports and protocols
          href: plan-ports-protocols.md
        - name: Plan the VMM compute fabric
          href: plan-compute.md
        - name: Plan the VMM networking fabric
          href: plan-network.md
        - name: Identify supported storage arrays
          href: supported-arrays.md
    - name: Upgrade and install
      items: 
        - name: Upgrade VMM
          href: upgrade-vmm.md
        - name: Install VMM
          href: install.md
        - name: Install the VMM console
          href: install-console.md
        - name: Enable enhanced console session
          href: enhanced-console-session.md
        - name: Deploy VMM for high availability
          href: high-availability.md
          items: 
            - name: Deploy a highly available VMM management server
              href: ha-server.md
            - name: Deploy a highly available SQL Server database for VMM
              href: ha-sql.md
            - name: Deploy a highly available VMM library
              href: ha-library.md
        - name: Set up TLS 1.2
          href: install-tls.md
        - name: Deploy update rollups
          href: update-rollups.md
        - name: Back up and restore VMM
          href: backup.md
    - name: Manage the VMM library
      items: 
        - name: Library overview
          href: manage-library-server.md
        - name: Add file-based resources to the VMM library
          href: library-files.md
        - name: Add profiles to the VMM library
          href: library-profiles.md
        - name: Add VM templates to the VMM library
          href: library-vm-templates.md
        - name: Add service templates to the VMM library
          href: library-service-templates.md
        - name: Manage VMM library resources
          href: library-resources.md
    - name: Manage virtualization servers
      items: 
        - name: Manage VMM host groups
          href: host-groups.md
        - name: Add existing Hyper-V hosts and clusters to the fabric
          href: hyper-v-existing.md
        - name: Add a Nano server as a Hyper-V host or cluster
          href: hyper-v-nano.md
        - name: Run a script on host
          href: run-script-host.md
        - name: Create a cluster from standalone Hyper-V hosts
          href: hyper-v-standalone.md
        - name: Provision a Hyper-V host or cluster from bare-metal
          href: hyper-v-bare-metal.md
        - name: Create a guest Hyper-V cluster from a service template
          href: hyper-v-guest-cluster.md
        - name: Set up networking for Hyper-V hosts and clusters
          href: hyper-v-network.md
        - name: Set up storage for Hyper-V hosts and clusters
          href: hyper-v-storage.md
        - name: Manage MPIO for Hyper-V hosts and clusters
          href: hyper-v-mpio.md
        - name: Manage Hyper-V extended port ACLs
          href: hyper-v-acls.md
        - name: Manage Hyper-V clusters
          href: hyper-v-cluster.md
        - name: Update Hyper-V hosts and clusters
          href: hyper-v-update.md
        - name: Run a rolling upgrade of Hyper-V clusters
          href: hyper-v-rolling-upgrade.md
        - name: Service Hyper-V hosts for maintenance
          href: hyper-v-service.md
        - name: Manage VMware servers
          href: manage-vmware-hosts.md
    - name: Manage management servers
      items: 
        - name: Manage infrastructure servers
          href: infrastructure-server.md
        - name: Manage update servers
          href: update-server.md
    - name: Manage networking
      items: 
        - name: Network fabric overview
          href: manage-networks.md
        - name: Set up logical networks
          href: network-logical.md
        - name: Set up logical networks in UR1
          href: network-logical-ur1.md
        - name: Set up logical networks in VMM
          href: network-logical-2022.md
        - name: Set up VM networks
          href: network-virtual.md
        - name: Set up IP address pools
          href: network-pool.md
        - name: Add a network gateway
          href: network-gateway.md
        - name: Set up port profiles
          href: network-port-profile.md
        - name: Set up logical switches
          href: network-switch.md
        - name: Set up MAC address pools
          href: network-mac.md
        - name: Integrate NLB with service templates
          href: network-nlb.md
        - name: Set up an IPAM server
          href: network-ipam.md
    - name: Manage storage
      items: 
        - name: Set up storage fabric
          href: manage-storage.md
        - name: Set up storage classifications
          href: storage-classification.md
        - name: Add storage devices
          href: storage-device.md
        - name: Allocate storage to host groups
          href: storage-host-group.md
        - name: Set up a Microsoft iSCSI Target Server
          href: storage-iscsi.md
        - name: Set up a Virtual Fibre Channel
          href: storage-fibre-channel.md
        - name: Set up file storage
          href: storage-file.md
        - name: Set up Storage Replica in VMM
          href: storage-replica.md
    - name: Manage SOFS
      items: 
        - name: Set up a scale-out file server (SOFS)
          href: sofs.md
        - name: Perform a rolling upgrade on SOFS
          href: sofs-rolling-upgrade.md
        - name: Add an existing SOFS to the VMM fabric
          href: sofs-existing.md
        - name: Create an SOFS cluster from standalone servers
          href: sofs-cluster.md
        - name: Provision SOFS from bare-metal computers
          href: sofs-bare-metal.md
        - name: Manage SOFS settings
          href: sofs-settings.md
        - name: Set QoS for storage resources
          href: manage-sofs-qos.md
    - name: Manage virtual machines
      items: 
        - name: Provision VMs
          href: provision-vms.md
        - name: Deploy VMs from a blank VHD
          href: vm-blank-disk.md
        - name: Deploy VMs from an existing VHD
          href: vm-existing-disk.md
        - name: Clone existing VMs
          href: vm-clone.md
        - name: Deploy VMs with rapid provisioning using SAN copy
          href: vm-san-copy.md
        - name: Deploy VMs from a VM template
          href: vm-template.md
        - name: Deploy VMs from the VMM library
          href: manage-vm-library.md
        - name: Deploy Linux VMs
          href: vm-linux.md
        - name: Deploy nested VMs
          href: vm-nested-virtualization.md
        - name: Convert VMware VMs to Hyper-V
          href: vm-convert-vmware.md
        - name: Install an operating system on a VM
          href: vm-install-operating-system.md
        - name: Manage VM settings
          href: vm-settings.md
        - name: Manage dynamic and power optimization for VMs
          href: vm-optimization.md
        - name: Configure VM failover between virtual networks
          href: manage-vm-failover-virtual-networks.md
        - name: Create VM role templates with VMM and Azure Pack
          href: vm-role-template.md
    - name: Migrate VMs
      items: 
        - name: Migration overview
          href: migrate.md
        - name: Migrate a VM
          href: migrate-vm.md
        - name: Migrate VM storage
          href: migrate-storage.md
        - name: Run a live migration
          href: migrate-live.md
    - name: Manage roles and accounts
      items: 
        - name: Roles and accounts overview
          href: manage-account.md
        - name: Set up user roles
          href: account-user-role.md
        - name: Set up Run As accounts
          href: account-runas.md
        - name: Manage self-service users
          href: self-service.md
        - name: Perform self-service user tasks
          href: self-service-tasks.md
    - name: Monitor VMM
      items: 
        - name: Monitoring overview
          href: monitor.md
        - name: Set up monitoring and reporting with Operations Manager
          href: monitors-ops-manager.md
    - name: Integrate with Azure
      items: 
        - name: Add an Azure subscription in VMM
          href: azure-subscription.md
        - name: VM update management
          href: vm-update-management.md
        - name: Manage Azure VMs
          href: manage-azure-vms.md
        - name: Manage Azure Resource Manager-based and region-specific Azure subscriptions
          href: vms-manage-azure-ad-and-region-specific.md
    - name: Troubleshoot
      items: 
        - name: Resources for Troubleshooting VMM
          href: troubleshoot.md
