![](https://img.shields.io/badge/Ansible-vsphere-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments. The author does not guarantee the accuracy, completeness, reliability, and availability of the role content. Under no circumstances will the author be held responsible or liable in any way for any claims, damages, losses, expenses, costs or liabilities whatsoever, including, without limitation, any direct or indirect damages for loss of profits, business interruption or loss of information.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。作者不对角色内容之准确性、完整性、可靠性、可用性做保证。在任何情况下，作者均不对任何索赔，损害，损失，费用，成本或负债承担任何责任，包括但不限于因利润损失，业务中断或信息丢失而造成的任何直接或间接损害。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_vmware.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [vsphere Versions](#vsphere-versions)
- [ Role variables](#Role-variables)
  * [Main Configuration](#Main-parameters)
  * [Other Configuration](#Other-parameters)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Hosts inventory file](#Hosts-inventory-file)
  * [Vars in role configuration](#vars-in-role-configuration)
  * [Combination of group vars and playbook](#combination-of-group-vars-and-playbook)
- [License](#license)
- [Author Information](#author-information)
- [Donations](#Donations)

## Overview

## Requirements

### vSphere versions

The following list of supported the vSphere releases:

* vSphere 6, 7

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:
* `vcenter_hostname`: The hostname or IP address of the vSphere vCenter server.
* `vcenter_username`: The username of the vSphere vCenter server.
* `vcenter_password`: The password of the vSphere vCenter server.
* `vcenter_datacenter`: The datacenter name to use for the operation.
* `vcenter_cluster`: The cluster name where the resource will run.
* `vcenter_cluster_drs`: Define high availability parameters.
* `vcenter_cluster_ha`: Define distributed resource scheduler parameters.
* `vcenter_licenses`: Define license keys.
* `vcenter_esxi_hosts`: The hostname or IP address of the ESXi servers.
* `vcenter_esxi_username`: The username of the ESXi server.
* `vcenter_esxi_password`: The password of the ESXi server.
* `vcenter_host_portgroup`: Define Port Group parameters on a VMware Standard Switch (vSS) for given ESXi hosts.
* `vcenter_dvs_portgroup`: Define Distributed vSwitch portgroup parameters.
* `vcenter_host_datastore`: Define storage datastore parameters.
* `vcenter_tag`: Define tag parameters.

### Other parameters

## Dependencies
- Ansible versions >= 2.15.5
- Python >= 3.9.0

## Example
### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`.

```yaml
---
vcenter_datacenter: "cn-north-1"
vcenter_cluster: "dev"
vcenter_esxi_hosts: ["node01.esxi.lab", "node02.esxi.lab"]
vcenter_esxi_username: "root"
vcenter_esxi_password: "2ZaD8UP3V^u9"
vcenter_licenses:
  - { name: "vCenter", key: "MA6NU-00000-00000-WA1XP-87ALF" }
  - { name: "ESXi", key: "0G0X0-00000-00000-0C3GK-1Z2J6" }
vcenter_cluster_drs:
  default_vm_behavior: "manual"
vcenter_cluster_ha:
  auto_compute_percentages: false
  failover_level: 1
  cpu_failover_resources_percent: 50
  memory_failover_resources_percent: 50
vcenter_host_datastore:
  - {
      name: "ds-san-lun0",
      type: "vmfs",
      device_name: "naa.600140510d73f7c9e544374adb91cb9f",
      version: 6,
    }
  - {
      name: "ds-san-lun1",
      type: "vmfs",
      device_name: "naa.6001405317d9e3acc0e4ae881b2c9bbb",
      version: 6,
    }
vcenter_tag:
  - { category: "default", name: "managed-by-ansible" }
  - { category: "k8s-region", name: "cn-north-1" }
  - { category: "k8s-zone", name: "norther" }
  - { category: "k8s-zone", name: "souther" }
vcenter_dvs_portgroup:
  - {
      switch: "DSwitch01",
      version: "7.0.3",
      mtu: "1600",
      uplink: 1,
      vmnics: ["vmnic1"],
      portgroup_name: "vlan-trunk-portrgoup",
      vlan_id: "0",
    }
```

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Donations
Please donate to the following monero address.

    46CHVMbb6wQV2PJYEbahb353SYGqXhcdFQVEWdCnHb6JaR5125h3kNQ6bcqLye5G7UF7qz6xL9qHLDSAY3baagfmLZABz75
<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/xmr_address.png" align="left" /></p>