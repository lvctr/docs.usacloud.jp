# サーバ(VNC接続情報): sakuracloud_server_vnc_info

サーバのVNC接続情報を参照するためのデータソース

## Example Usage

```hcl
data "sakuracloud_server_vnc_info" "foobar" {
  server_id = sakuracloud_server.foobar.id
}
```

## Argument Reference

* `server_id` - (Required) サーバのID
* `zone` - (Optional) 対象ゾーンの名前 (例: `is1a`, `tk1a`)  

## Attribute Reference

* `id` - サーバのID
* `host` - VNC接続先ホスト名
* `password` - VNC接続パスワード
* `port` - VNC接続先ポート番号

