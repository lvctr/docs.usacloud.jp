# サーバ: sakuracloud_server

サーバの情報を参照するためのデータソース

## Example Usage

```hcl
data "sakuracloud_server" "foobar" {
  filter {
    names = ["foobar"]
  }
}
```

## Argument Reference

* `filter` - (Optional) 参照対象をフィルタリングするための条件。詳細は[filterブロック](#filter)を参照 
* `zone` - (Optional) 対象ゾーンの名前 (例: `is1a`, `tk1a`)  

##### filterブロック

* `condition` - (Optional) APIリクエスト時に利用されるフィルタリング用パラメータ。詳細は[conditionブロック](#condition)を参照  
* `id` - (Optional) 対象リソースのID 
* `names` - (Optional) 対象リソースの名前。指定値と部分一致するリソースが参照対象となる。複数指定した場合はAND条件となる  
* `tags` - (Optional) 対象リソースが持つタグ。指定値と完全一致するリソースが参照対象となる。複数指定した場合はAND条件となる

##### conditionブロック

* `name` - (Required) 対象フィールド名。大文字/小文字を区別する  
* `values` - (Required) 対象フィールドの値。複数指定した場合はAND条件となる


## Attribute Reference

* `id` - ID
* `cdrom_id` - サーバに挿入されているCD-ROMのID
* `commitment` - vCPUの割り当て方式。次のいずれかとなる 
    - `standard`: 通常  
    - `dedicatedcpu`: コア専有  
* `core` - vCPU数
* `description` - 説明
* `disks` - サーバに接続されているディスクのIDのリスト
* `dns_servers` - サーバが属するゾーンのDNSサーバのIPアドレスのリスト
* `gateway` - ゲートウェイIPアドレス
* `icon_id` - アイコンID
* `interface_driver` - NICのドライバー。次のいずれかとなる [`virtio`/`e1000`]
* `ip_address` - IPアドレス
* `memory` - メモリサイズ(GiB単位)
* `name` - 名前
* `netmask` - サブネットマスク長
* `network_address` - ネットワークアドレス
* `network_interface` - NIC設定。詳細は[network_interfaceブロック](#network_interface)を参照
* `private_host_id` - 専有ホストのID
* `private_host_name` - 専有ホストの名前
* `tags` - タグ

##### network_interfaceブロック

* `mac_address` - MACアドレス
* `packet_filter_id` - パケットフィルタのID
* `upstream` - 上流ネットワーク設定。次のいずれかとなる
    - `shared`: 共有セグメント(100Mbps)
    - `disconnect`: 切断
    - `<switch id>`: スイッチ(ID)


