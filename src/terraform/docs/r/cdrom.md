# CD-ROM(ISOイメージ): sakuracloud_cdrom

## Example Usage

```hcl
resource "sakuracloud_cdrom" "foobar" {
  name           = "foobar"
  size           = 5
  iso_image_file = "example.iso"
  description    = "description"
  tags           = ["tag1", "tag2"]
}
```

## Argument Reference

* `name` - (Required) 名前 / `1`-`64`文字で指定
* `content` - (Optional) アップロードするCD-ROMのコンテンツ /  [`iso_image_file`]と同時に指定できません
* `content_file_name` - (Optional) `content`を指定した場合の作成するファイル名 / [`iso_image_file`]と同時に指定できません /  デフォルト:`config`
* `iso_image_file` - (Optional) アップロードするファイルのパス / [`content`]と同時に指定できません
* `hash` - (Optional) コンテンツをBASE64エンコードしたものから算出されたMD5チェックサム
* `size` - (Optional) サイズ(GiB単位) / 次のいずれかを指定 [`5`/`10`] / この値を変更するとリソースの再作成が行われる / デフォルト:`5`

#### Common Arguments

* `description` - (Optional) 説明 / `1`-`512`文字で指定
* `icon_id` - (Optional) アイコンID
* `tags` - (Optional) タグ
* `zone` - (Optional) リソースを作成する対象ゾーンの名前(例: `is1a`, `tk1a`) / この値を変更するとリソースの再作成が行われる


### Timeouts

`timeouts`ブロックで[カスタムタイムアウト](https://www.terraform.io/docs/configuration/resources.html#operation-timeouts)が設定可能です。  

* `create` - 作成 (デフォルト: 24時間)
* `update` - 更新 (デフォルト: 24時間)
* `delete` - 削除 (デフォルト: 20分)

## Attribute Reference

* `id` - ID

