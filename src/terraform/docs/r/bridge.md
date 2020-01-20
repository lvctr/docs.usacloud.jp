---
layout: "sakuracloud"
page_title: "SakuraCloud: sakuracloud_bridge"
subcategory: "Networking"
description: |-
  Manages a SakuraCloud Bridge.
---

# sakuracloud_bridge

Manages a SakuraCloud Bridge.

## Example Usage

```hcl
resource "sakuracloud_switch" "is1a" {
  name        = "is1a"
  description = "description"
  bridge_id   = sakuracloud_bridge.foobar.id
  zone        = "is1a"
}

resource "sakuracloud_switch" "is1b" {
  name        = "is1b"
  description = "description"
  bridge_id   = sakuracloud_bridge.foobar.id
  zone        = "is1b"
}

resource "sakuracloud_bridge" "foobar" {
  name        = "foobar"
  description = "description"
}
```
## Argument Reference

* `name` - (Required) The name of the Bridge. The length of this value must be in the range [`1`-`64`].

#### Common Arguments

* `description` - (Optional) The description of the Bridge. The length of this value must be in the range [`1`-`512`].
* `zone` - (Optional) The name of zone that the Bridge will be created. (e.g. `is1a`, `tk1a`). Changing this forces a new resource to be created.

### Timeouts

The `timeouts` block allows you to specify [timeouts](https://www.terraform.io/docs/configuration/resources.html#operation-timeouts) for certain actions:

* `create` - (Defaults to 20 minutes) Used when creating the Bridge
* `update` - (Defaults to 20 minutes) Used when updating the Bridge
* `delete` - (Defaults to 20 minutes) Used when deleting Bridge

## Attribute Reference

* `id` - The id of the Bridge.
