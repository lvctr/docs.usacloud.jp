# 専有ホスト: sakuracloud_private_host

ディスクの情報を参照するためのデータソース

## Example Usage

```hcl
data "sakuracloud_private_host" "foobar" {
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
* `assigned_core` - サーバに割り当てたCPUコアの総数
* `assigned_memory` - サーバに割り当てたメモリ(GiB単位)の総数
* `class` - クラス。次のいずれかとなる [`dynamic`/`ms_windows`]
* `description` - 説明
* `hostname` - ホスト名
* `icon_id` - アイコンID
* `name` - 名前
* `tags` - タグ



