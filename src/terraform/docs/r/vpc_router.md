---
layout: "sakuracloud"
page_title: "SakuraCloud: sakuracloud_vpc_router"
subcategory: "Appliance"
description: |-
  Manages a SakuraCloud VPC Router.
---

# sakuracloud_vpc_router

Manages a SakuraCloud VPC Router.

## Example Usage

```hcl
resource "sakuracloud_vpc_router" "standard" {
  name                = "standard"
  description         = "description"
  tags                = ["tag1", "tag2"]
  internet_connection = true
}

resource "sakuracloud_vpc_router" "premium" {
  name        = "premium"
  description = "description"
  tags        = ["tag1", "tag2"]
  plan        = "premium"

  internet_connection = true

  switch_id    = sakuracloud_internet.foobar.switch_id
  vip          = sakuracloud_internet.foobar.ip_addresses[0]
  ip_addresses = [sakuracloud_internet.foobar.ip_addresses[1], sakuracloud_internet.foobar.ip_addresses[2]]
  aliases      = [sakuracloud_internet.foobar.ip_addresses[3]]
  vrid         = 1

  network_interface {
    index        = 1
    switch_id    = sakuracloud_switch.foobar.id
    vip          = "192.168.11.1"
    ip_addresses = ["192.168.11.2", "192.168.11.3"]
    netmask      = 24
  }

  dhcp_server {
    interface_index = 1

    range_start = "192.168.11.11"
    range_stop  = "192.168.11.20"
    dns_servers = ["8.8.8.8", "8.8.4.4"]
  }

  dhcp_static_mapping {
    ip_address  = "192.168.11.10"
    mac_address = "aa:bb:cc:aa:bb:cc"
  }

  firewall {
    interface_index = 1

    direction = "send"
    expression {
      protocol            = "tcp"
      source_network      = ""
      source_port         = "80"
      destination_network = ""
      destination_port    = ""
      allow               = true
      logging             = true
      description         = "desc"
    }

    expression {
      protocol            = "ip"
      source_network      = ""
      source_port         = ""
      destination_network = ""
      destination_port    = ""
      allow               = false
      logging             = true
      description         = "desc"
    }
  }

  l2tp {
    pre_shared_secret = "example"
    range_start       = "192.168.11.21"
    range_stop        = "192.168.11.30"
  }

  port_forwarding {
    protocol     = "udp"
    public_port  = 10022
    private_ip   = "192.168.11.11"
    private_port = 22
    description  = "desc"
  }

  pptp {
    range_start = "192.168.11.31"
    range_stop  = "192.168.11.40"
  }

  site_to_site_vpn {
    peer              = "192.0.2.1"
    remote_id         = "192.0.2.1"
    pre_shared_secret = "example"
    routes            = ["192.0.2.0/8"]
    local_prefix      = ["192.168.21.0/24"]
  }

  static_nat {
    public_ip   = sakuracloud_internet.foobar.ip_addresses[3]
    private_ip  = "192.168.11.12"
    description = "desc"
  }

  static_route {
    prefix   = "172.16.0.0/16"
    next_hop = "192.168.11.99"
  }

  user {
    name     = "username"
    password = "password"
  }
}

resource "sakuracloud_internet" "foobar" {
  name = "foobar"
}

resource sakuracloud_switch "foobar" {
  name = "foobar"
}
```

## Argument Reference

* `name` - (Required) The name of the VPCRouter. The length of this value must be in the range [`1`-`64`].
* `internet_connection` - (Optional) The flag to enable connecting to the Internet from the VPC Router. Default:`true`.
* `plan` - (Optional) The plan name of the VPCRouter. This must be one of [`standard`/`premium`/`highspec`/`highspec4000`]. Changing this forces a new resource to be created. Default:`standard`.
* `syslog_host` - (Optional) The ip address of the syslog host to which the VPC Router sends logs.
* `vrid` - (Optional) The Virtual Router Identifier. This is only required when `plan` is not `standard`. Changing this forces a new resource to be created.

#### Network

* `aliases` - (Optional) A list of ip alias to assign to the VPC Router. This can only be specified if `plan` is not `standard`.
* `ip_addresses` - (Optional) The list of the IP address to assign to the VPC Router. This is required only one value when `plan` is `standard`, two values otherwise. Changing this forces a new resource to be created.
* `network_interface` - (Optional) A list of additional network interface setting. This doesn't include primary network interface setting.
* `switch_id` - (Optional) The id of the switch to connect. This is only required when when `plan` is not `standard`%!(EXTRA string=VPCRouter). Changing this forces a new resource to be created.
* `vip` - (Optional) The virtual IP address of the VPC Router. This is only required when `plan` is not `standard`. Changing this forces a new resource to be created.

#### Static Route

* `static_route` - (Optional) One or more `static_route` blocks as defined below.

#### Firewall

* `firewall` - (Optional) One or more `firewall` blocks as defined below.

#### Site to Site VPN

* `site_to_site_vpn` - (Optional) One or more `site_to_site_vpn` blocks as defined below.

#### DHCP/NAT/Forwarding

* `dhcp_server` - (Optional) One or more `dhcp_server` blocks as defined below.
* `dhcp_static_mapping` - (Optional) One or more `dhcp_static_mapping` blocks as defined below.
* `port_forwarding` - (Optional) One or more `port_forwarding` blocks as defined below.
* `static_nat` - (Optional) One or more `static_nat` blocks as defined below.

#### Remote Access

* `l2tp` - (Optional) A `l2tp` block as defined below.
* `pptp` - (Optional) A `pptp` block as defined below.
* `user` - (Optional) One or more `user` blocks as defined below.

#### Common Arguments

* `description` - (Optional) The description of the VPCRouter. The length of this value must be in the range [`1`-`512`].
* `icon_id` - (Optional) The icon id to attach to the VPCRouter.
* `tags` - (Optional) Any tags to assign to the VPCRouter.
* `zone` - (Optional) The name of zone that the VPCRouter will be created. (e.g. `is1a`, `tk1a`). Changing this forces a new resource to be created.


---

A `dhcp_server` block supports the following:

* `interface_index` - (Required) The index of the network interface on which to enable the DHCP service. This must be in the range [`1`-`7`].
* `range_start` - (Required) The start value of IP address range to assign to DHCP client.
* `range_stop` - (Required) The end value of IP address range to assign to DHCP client.
* `dns_servers` - (Optional) A list of IP address of DNS server to assign to DHCP client.

---

A `dhcp_static_mapping` block supports the following:

* `ip_address` - (Required) The static IP address to assign to DHCP client.
* `mac_address` - (Required) The source MAC address of static mapping.

---

A `firewall` block supports the following:

* `direction` - (Required) The direction to apply the firewall. This must be one of [`send`/`receive`].
* `expression` - (Required) One or more `expression` blocks as defined below.
* `interface_index` - (Optional) The index of the network interface on which to enable filtering. This must be in the range [`0`-`7`].

---

A `expression` block supports the following:

* `protocol` - (Required) The protocol used for filtering. This must be one of [`tcp`/`udp`/`icmp`/`ip`].
* `allow` - (Required) The flag to allow the packet through the filter.
* `destination_network` - (Optional) A destination IP address or CIDR block used for filtering (e.g. `192.0.2.1`, `192.0.2.0/24`).
* `destination_port` - (Optional) A destination port number or port range used for filtering (e.g. `1024`, `1024-2048`). This is only used when `protocol` is `tcp` or `udp`.
* `source_network` - (Optional) A source IP address or CIDR block used for filtering (e.g. `192.0.2.1`, `192.0.2.0/24`).
* `source_port` - (Optional) A source port number or port range used for filtering (e.g. `1024`, `1024-2048`). This is only used when `protocol` is `tcp` or `udp`.
* `logging` - (Optional) The flag to enable packet logging when matching the expression.
* `description` - (Optional) The description of the expression. The length of this value must be in the range [`0`-`512`].

---

A `l2tp` block supports the following:

* `pre_shared_secret` - (Required) The pre shared secret for L2TP/IPsec.
* `range_start` - (Required) The start value of IP address range to assign to L2TP/IPsec client.
* `range_stop` - (Required) The end value of IP address range to assign to L2TP/IPsec client.

---

A `network_interface` block supports the following:

* `index` - (Required) The index of the network interface. This must be in the range [`1`-`7`].
* `ip_addresses` - (Required) A list of ip address to assign to the network interface. This is required only one value when `plan` is `standard`, two values otherwise.
* `netmask` - (Required) The bit length of the subnet to assign to the network interface.
* `switch_id` - (Required) The id of the connected switch.
* `vip` - (Optional) The virtual IP address to assign to the network interface. This is only required when `plan` is not `standard`.

---

A `port_forwarding` block supports the following:

* `private_ip` - (Required) The destination ip address of the port forwarding.
* `private_port` - (Required) The destination port number of the port forwarding. This will be a port number on a private network.
* `protocol` - (Required) The protocol used for port forwarding. This must be one of [`tcp`/`udp`].
* `public_port` - (Required) The source port number of the port forwarding. This must be a port number on a public network.
* `description` - (Optional) The description of the port forwarding. The length of this value must be in the range [`0`-`512`].

---

A `pptp` block supports the following:

* `range_start` - (Required) The start value of IP address range to assign to PPTP client.
* `range_stop` - (Required) The end value of IP address range to assign to PPTP client.

---

A `site_to_site_vpn` block supports the following:

* `local_prefix` - (Required) A list of CIDR block of the network under the VPC Router.
* `peer` - (Required) The IP address of the opposing appliance connected to the VPC Router.
* `pre_shared_secret` - (Required) The pre shared secret for the VPN. The length of this value must be in the range [`0`-`40`].
* `remote_id` - (Required) The id of the opposing appliance connected to the VPC Router. This is typically set same as value of `peer`.
* `routes` - (Required) A list of CIDR block of VPN connected networks.

---

A `static_nat` block supports the following:

* `private_ip` - (Required) The private IP address used for the static NAT.
* `public_ip` - (Required) The public IP address used for the static NAT.
* `description` - (Optional) The description of the static nat. The length of this value must be in the range [`0`-`512`].

---

A `static_route` block supports the following:

* `next_hop` - (Required) The IP address of the next hop.
* `prefix` - (Required) The CIDR block of destination.

---

A `user` block supports the following:

* `name` - (Required) The user name used to authenticate remote access.
* `password` - (Required) The password used to authenticate remote access.


### Timeouts

The `timeouts` block allows you to specify [timeouts](https://www.terraform.io/docs/configuration/resources.html#operation-timeouts) for certain actions:

* `create` - (Defaults to 60 minutes) Used when creating the VPC Router
* `update` - (Defaults to 60 minutes) Used when updating the VPC Router
* `delete` - (Defaults to 20 minutes) Used when deleting VPC Router

## Attribute Reference

* `id` - The id of the VPC Router.
* `public_ip` - The public ip address of the VPC Router.

