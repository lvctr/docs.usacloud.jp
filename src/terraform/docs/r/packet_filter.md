# パケットフィルタ: sakuracloud_packet_filter

## Example Usage

```hcl
resource "sakuracloud_packet_filter" "foobar" {
  name        = "foobar"
  description = "description"

  expression {
    protocol  = "tcp"
    dest_port = "22"
  }

  expression {
    protocol  = "tcp"
    dest_port = "80"
  }

  expression {
    protocol  = "tcp"
    dest_port = "443"
  }

  expression {
    protocol = "icmp"
  }

  expression {
    protocol = "fragment"
  }

  expression {
    protocol    = "udp"
    source_port = "123"
  }

  expression {
    protocol  = "tcp"
    dest_port = "32768-61000"
  }

  expression {
    protocol  = "udp"
    dest_port = "32768-61000"
  }

  expression {
    protocol    = "ip"
    allow       = false
    description = "Deny ALL"
  }
}
```

!!! Note
    パケットフィルタのルール(`expression`)にサーバのIPアドレスを利用したい場合にリソースの循環参照エラーとなることがあります。  
    その場合はパケットフィルタルールリソース(`sakuracloud_packet_filter_rules`)をご利用ください。

## Argument Reference

* `name` - (Required) 説明 / `1`-`512`文字で指定
* `expression` - (Optional) フィルタリングルールのリスト。詳細は[expressionブロック](#expression)を参照

#### Common Arguments

* `description` - (Optional) 説明 / `1`-`512`文字で指定
* `zone` - (Optional) リソースを作成する対象ゾーンの名前(例: `is1a`, `tk1a`) / この値を変更するとリソースの再作成が行われる

---

#### expressionブロック

* `protocol` - (Required) プロトコル / 次のいずれかを指定 [`http`/`https`/`tcp`/`udp`/`icmp`/`fragment`/`ip`]
* `allow` - (Optional) マッチしたパケットを許可するフラグ
* `destination_port` - (Optional) 宛先ポート、または宛先ポート範囲 (例:`1024`, `1024-2048`)
* `source_network` - (Optional) 送信元IPアドレス、または送信元CIDRブロック (例: `192.0.2.1`, `192.0.2.0/24`)
* `source_port` - (Optional) 送信元ポート番号、または送信元ポート番号範囲 (例: `1024`, `1024-2048`)
* `description` - (Optional) 説明

### Timeouts

`timeouts`ブロックで[カスタムタイムアウト](https://www.terraform.io/docs/configuration/resources.html#operation-timeouts)が設定可能です。  

* `create` - 作成 (デフォルト: 5分)
* `update` - 更新 (デフォルト: 5分)
* `delete` - 削除 (デフォルト: 20分)

## Attribute Reference

* `id` - ID

