root@terraform:~# terraform apply

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # metal_device.server1 will be created
  + resource "metal_device" "server1" {
      + access_private_ipv4              = (known after apply)
      + access_public_ipv4               = (known after apply)
      + access_public_ipv6               = (known after apply)
      + always_pxe                       = false
      + billing_cycle                    = "hourly"
      + created                          = (known after apply)
      + deployed_facility                = (known after apply)
      + deployed_hardware_reservation_id = (known after apply)
      + facilities                       = [
          + "dc13",
        ]
      + force_detach_volumes             = false
      + hostname                         = "first-tf-server"
      + id                               = (known after apply)
      + locked                           = (known after apply)
      + network                          = (known after apply)
      + network_type                     = (known after apply)
      + operating_system                 = "ubuntu_18_04"
      + plan                             = "c3.small.x86"
      + ports                            = (known after apply)
      + project_id                       = "b0389d5f-0f60-4075-9f9b-475a0c8a65ce"
      + root_password                    = (sensitive value)
      + ssh_key_ids                      = (known after apply)
      + state                            = (known after apply)
      + updated                          = (known after apply)
      + wait_for_reservation_deprovision = false
    }

  # metal_device.server2 will be created
  + resource "metal_device" "server2" {
      + access_private_ipv4              = (known after apply)
      + access_public_ipv4               = (known after apply)
      + access_public_ipv6               = (known after apply)
      + always_pxe                       = false
      + billing_cycle                    = "hourly"
      + created                          = (known after apply)
      + deployed_facility                = (known after apply)
      + deployed_hardware_reservation_id = (known after apply)
      + facilities                       = [
          + "dc13",
        ]
      + force_detach_volumes             = false
      + hostname                         = "second-tf-server"
      + id                               = (known after apply)
      + locked                           = (known after apply)
      + network                          = (known after apply)
      + network_type                     = (known after apply)
      + operating_system                 = "ubuntu_18_04"
      + plan                             = "c3.medium.x86"
      + ports                            = (known after apply)
      + project_id                       = "b0389d5f-0f60-4075-9f9b-475a0c8a65ce"
      + root_password                    = (sensitive value)
      + ssh_key_ids                      = (known after apply)
      + state                            = (known after apply)
      + updated                          = (known after apply)
      + wait_for_reservation_deprovision = false
    }

  # metal_port_vlan_attachment.attach-vlan-s1 will be created
  + resource "metal_port_vlan_attachment" "attach-vlan-s1" {
      + device_id  = (known after apply)
      + force_bond = false
      + id         = (known after apply)
      + native     = false
      + port_id    = (known after apply)
      + port_name  = "bond0"
      + vlan_id    = (known after apply)
      + vlan_vnid  = (known after apply)
    }

  # metal_port_vlan_attachment.attach-vlan-s2 will be created
  + resource "metal_port_vlan_attachment" "attach-vlan-s2" {
      + device_id  = (known after apply)
      + force_bond = false
      + id         = (known after apply)
      + native     = false
      + port_id    = (known after apply)
      + port_name  = "bond0"
      + vlan_id    = (known after apply)
      + vlan_vnid  = (known after apply)
    }

  # metal_project.project will be created
  + resource "metal_project" "project" {
      + backend_transfer  = false
      + created           = (known after apply)
      + id                = (known after apply)
      + name              = "adanskin project"
      + organization_id   = (known after apply)
      + payment_method_id = (known after apply)
      + updated           = (known after apply)
    }

  # metal_vlan.vlan1 will be created
  + resource "metal_vlan" "vlan1" {
      + description = "TF VLAN"
      + facility    = "dc13"
      + id          = (known after apply)
      + project_id  = "b0389d5f-0f60-4075-9f9b-475a0c8a65ce"
      + vxlan       = (known after apply)
    }

  # null_resource.build-bash-script-1 will be created
  + resource "null_resource" "build-bash-script-1" {
      + id = (known after apply)
    }

  # null_resource.build-bash-script-2 will be created
  + resource "null_resource" "build-bash-script-2" {
      + id = (known after apply)
    }

  # null_resource.clean-up-1 will be created
  + resource "null_resource" "clean-up-1" {
      + id = (known after apply)
    }

  # null_resource.clean-up-2 will be created
  + resource "null_resource" "clean-up-2" {
      + id = (known after apply)
    }

  # null_resource.configure-network-server1 will be created
  + resource "null_resource" "configure-network-server1" {
      + id = (known after apply)
    }

  # null_resource.configure-network-server2 will be created
  + resource "null_resource" "configure-network-server2" {
      + id = (known after apply)
    }

Plan: 12 to add, 0 to change, 0 to destroy.
╷
│ Warning: "facilities": [DEPRECATED] Use metro attribute instead
│ 
│   on main.tf line 36, in resource "metal_device" "server1":
│   36: resource "metal_device" "server1" {
│ 
│ (and one more similar warning elsewhere)
╵

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

metal_vlan.vlan1: Creating...
metal_project.project: Creating...
metal_device.server2: Creating...
metal_device.server1: Creating...
metal_vlan.vlan1: Creation complete after 1s [id=6fa5038b-53f6-4cec-a320-51ff41420fc3]
null_resource.build-bash-script-2: Creating...
null_resource.build-bash-script-1: Creating...
null_resource.build-bash-script-1: Provisioning with 'local-exec'...
null_resource.build-bash-script-2: Provisioning with 'local-exec'...
null_resource.build-bash-script-1 (local-exec): Executing: ["/bin/sh" "-c" "echo '#!/bin/bash\napt update\napt install vlan\nmodprobe 8021q\necho \"8021q\" >> /etc/modules-load.d/networking.conf\nip link add link bond0 name bond0.1169 type vlan id 1169\nip addr add 192.168.100.1/24 brd 192.168.100.255 dev bond0.1169\nip link set dev bond0.1169 up' > network-configurator-1.script"]
null_resource.build-bash-script-2 (local-exec): Executing: ["/bin/sh" "-c" "echo '#!/bin/bash\napt update\napt install vlan\nmodprobe 8021q\necho \"8021q\" >> /etc/modules-load.d/networking.conf\nip link add link bond0 name bond0.1169 type vlan id 1169\nip addr add 192.168.100.2/24 brd 192.168.100.255 dev bond0.1169\nip link set dev bond0.1169 up' > network-configurator-2.script"]
null_resource.build-bash-script-1: Creation complete after 0s [id=3651828598102535777]
null_resource.build-bash-script-2: Creation complete after 0s [id=1719375383754693945]
metal_project.project: Creation complete after 1s [id=e23c8594-e9d8-4a3f-a58f-55a5646ab72f]
metal_device.server1: Still creating... [10s elapsed]
metal_device.server2: Still creating... [10s elapsed]
metal_device.server2: Still creating... [20s elapsed]
metal_device.server1: Still creating... [20s elapsed]
metal_device.server2: Still creating... [30s elapsed]
metal_device.server1: Still creating... [30s elapsed]
metal_device.server2: Still creating... [40s elapsed]
metal_device.server1: Still creating... [40s elapsed]
metal_device.server1: Still creating... [50s elapsed]
metal_device.server2: Still creating... [50s elapsed]
metal_device.server1: Still creating... [1m0s elapsed]
metal_device.server2: Still creating... [1m0s elapsed]
metal_device.server2: Still creating... [1m10s elapsed]
metal_device.server1: Still creating... [1m10s elapsed]
metal_device.server1: Still creating... [1m20s elapsed]
metal_device.server2: Still creating... [1m20s elapsed]
metal_device.server1: Creation complete after 1m28s [id=9e41cdf3-dbe6-481d-a1b3-f9fd51b6f17e]
null_resource.configure-network-server1: Creating...
metal_port_vlan_attachment.attach-vlan-s1: Creating...
null_resource.configure-network-server1: Provisioning with 'file'...
metal_device.server2: Still creating... [1m30s elapsed]
null_resource.configure-network-server1: Still creating... [10s elapsed]
metal_port_vlan_attachment.attach-vlan-s1: Still creating... [10s elapsed]
metal_device.server2: Still creating... [1m40s elapsed]
null_resource.configure-network-server1: Still creating... [20s elapsed]
metal_port_vlan_attachment.attach-vlan-s1: Still creating... [20s elapsed]
metal_port_vlan_attachment.attach-vlan-s1: Creation complete after 20s [id=76e13276-2f96-4a09-a8f5-f344def155dc:6fa5038b-53f6-4cec-a320-51ff41420fc3]
metal_device.server2: Still creating... [1m50s elapsed]
null_resource.configure-network-server1: Still creating... [30s elapsed]
metal_device.server2: Still creating... [2m0s elapsed]
null_resource.configure-network-server1: Still creating... [40s elapsed]
metal_device.server2: Still creating... [2m10s elapsed]
null_resource.configure-network-server1: Still creating... [50s elapsed]
metal_device.server2: Still creating... [2m20s elapsed]
null_resource.configure-network-server1: Still creating... [1m0s elapsed]
metal_device.server2: Still creating... [2m30s elapsed]
null_resource.configure-network-server1: Still creating... [1m10s elapsed]
metal_device.server2: Still creating... [2m40s elapsed]
null_resource.configure-network-server1: Still creating... [1m20s elapsed]
metal_device.server2: Still creating... [2m50s elapsed]
metal_device.server2: Creation complete after 2m52s [id=5826e02e-bc8c-49bb-a4e5-1be8574b8735]
null_resource.configure-network-server2: Creating...
metal_port_vlan_attachment.attach-vlan-s2: Creating...
null_resource.configure-network-server2: Provisioning with 'file'...
null_resource.configure-network-server1: Still creating... [1m30s elapsed]
null_resource.configure-network-server2: Still creating... [10s elapsed]
metal_port_vlan_attachment.attach-vlan-s2: Still creating... [10s elapsed]
metal_port_vlan_attachment.attach-vlan-s2: Creation complete after 10s [id=66d2165f-81cc-4385-a8f5-5bde5120edda:6fa5038b-53f6-4cec-a320-51ff41420fc3]
null_resource.configure-network-server1: Still creating... [1m40s elapsed]
null_resource.configure-network-server2: Still creating... [20s elapsed]
null_resource.configure-network-server1: Still creating... [1m50s elapsed]
null_resource.configure-network-server2: Still creating... [30s elapsed]
null_resource.configure-network-server1: Still creating... [2m0s elapsed]
null_resource.configure-network-server2: Still creating... [40s elapsed]
null_resource.configure-network-server1: Still creating... [2m10s elapsed]
null_resource.configure-network-server2: Still creating... [50s elapsed]
null_resource.configure-network-server1: Still creating... [2m20s elapsed]
null_resource.configure-network-server2: Still creating... [1m0s elapsed]
null_resource.configure-network-server1: Still creating... [2m30s elapsed]
null_resource.configure-network-server2: Still creating... [1m10s elapsed]
null_resource.configure-network-server1: Still creating... [2m40s elapsed]
null_resource.configure-network-server2: Still creating... [1m20s elapsed]
null_resource.configure-network-server1: Still creating... [2m50s elapsed]
null_resource.configure-network-server2: Still creating... [1m30s elapsed]
null_resource.configure-network-server1: Still creating... [3m0s elapsed]
null_resource.configure-network-server2: Still creating... [1m40s elapsed]
null_resource.configure-network-server1: Still creating... [3m10s elapsed]
null_resource.configure-network-server2: Still creating... [1m50s elapsed]
null_resource.configure-network-server1: Still creating... [3m20s elapsed]
null_resource.configure-network-server2: Still creating... [2m0s elapsed]
null_resource.configure-network-server1: Still creating... [3m30s elapsed]
null_resource.configure-network-server2: Still creating... [2m10s elapsed]
null_resource.configure-network-server1: Still creating... [3m40s elapsed]
null_resource.configure-network-server2: Still creating... [2m20s elapsed]
null_resource.configure-network-server1: Still creating... [3m50s elapsed]
null_resource.configure-network-server2: Still creating... [2m30s elapsed]
null_resource.configure-network-server1: Still creating... [4m0s elapsed]
null_resource.configure-network-server2: Still creating... [2m40s elapsed]
null_resource.configure-network-server1: Still creating... [4m10s elapsed]
null_resource.configure-network-server2: Still creating... [2m50s elapsed]
null_resource.configure-network-server1: Still creating... [4m20s elapsed]
null_resource.configure-network-server2: Still creating... [3m0s elapsed]
null_resource.configure-network-server1: Still creating... [4m30s elapsed]
null_resource.configure-network-server2: Still creating... [3m10s elapsed]
null_resource.configure-network-server1: Still creating... [4m40s elapsed]
null_resource.configure-network-server2: Still creating... [3m20s elapsed]
null_resource.configure-network-server1: Still creating... [4m50s elapsed]
null_resource.configure-network-server2: Still creating... [3m30s elapsed]
null_resource.configure-network-server2: Still creating... [3m40s elapsed]
null_resource.configure-network-server2: Still creating... [3m50s elapsed]
null_resource.configure-network-server2: Still creating... [4m0s elapsed]
null_resource.configure-network-server2: Still creating... [4m10s elapsed]
null_resource.configure-network-server2: Still creating... [4m20s elapsed]
null_resource.configure-network-server2: Still creating... [4m30s elapsed]
null_resource.configure-network-server2: Still creating... [4m40s elapsed]
null_resource.configure-network-server2: Still creating... [4m50s elapsed]
╷
│ Error: timeout - last error: SSH authentication failed (root@136.144.57.65:22): ssh: handshake failed: ssh: unable to authenticate, attempted methods [none publickey], no supported methods remain
│ 
│ 
╵
╷
│ Error: timeout - last error: SSH authentication failed (root@145.40.89.77:22): ssh: handshake failed: ssh: unable to authenticate, attempted methods [none publickey], no supported methods remain
│ 
│ 
╵
root@terraform:~#
