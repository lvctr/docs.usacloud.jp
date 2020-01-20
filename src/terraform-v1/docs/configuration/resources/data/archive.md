# アーカイブ(sakuracloud_archive)

---

### 設定例

```hcl
# アーカイブの参照(パブリックアーカイブ)
data "sakuracloud_archive" "centos" {
  os_type = "centos"
}

# アーカイブの参照(名称 or タグ指定)
data "sakuracloud_archive" "ubuntu" {
  name_selectors = ["Ubuntu", "LTS"]
  tag_selectors  = ["current-stable", "os-linux"]
}
```

### パラメーター

|パラメーター         |必須  |名称                |初期値     |設定値                    |補足                                          |
|-------------------|:---:|--------------------|:--------:|------------------------|----------------------------------------------|
| `os_type`         | -   | OS種別             | -        | 文字列                  | 設定可能な値は[os_typeに指定可能な値](#os_type)欄を参照 ※1 |
| `name_selectors`  | -   | 検索条件(名称)      | -        | リスト(文字列)           | 複数指定した場合はAND条件 ※1 |
| `tag_selectors`   | -   | 検索条件(タグ)      | -        | リスト(文字列)           | 複数指定した場合はAND条件 ※1 |
| `filter`          | -   | 検索条件(その他)    | -        | オブジェクト             | APIにそのまま渡されます。検索条件を指定してもAPI側が対応していない場合があります。 |
| `zone`            | -   | ゾーン | - | `is1a`<br />`is1b`<br />`tk1a`<br />`tk1v` | - |

※1: `os_type`の指定をした場合、`name_selectors`と`tag_selectors`は指定できません。

### os_typeに指定可能な値

`os_type`に指定可能な値は以下の通りです。

|値|詳細                                          |
|---------------------------|--------------------|
| `centos`                  | CentOS(最新安定板)|
| `centos8`                  | CentOS 8|
| `centos7`                  | CentOS 7|
| `centos6`                  | CentOS 6|
| `ubuntu`                  | Ubuntu(最新安定板)|
| `ubuntu1804`              | Ubuntu 18.04|
| `ubuntu1604`              | Ubuntu 16.04|
| `debian`                  | Debian(最新安定板) |
| `debian10`                  | Debian10 |
| `debian9`                  | Debian9 |
| `coreos`                  | CoreOS|
| `rancheros`               | RancherOS|
| `k3os`                    | k3OS|
| `kusanagi`                | Kusanagi(CentOS7)|
| `sophos-utm`              | Sophos-UTM(*1)|
| `netwiser`                | Netwiser Virtual Edition(*2) |
| `opnsense`                | OPNsense |
| `freebsd`                 | FreeBSD|
| `windows2016`             | Windows 2016|
| `windows2016-rds`         | Windows 2016(RDS)|
| `windows2016-rds-office`  | Windows 2016(RDS + Office)|
| `windows2016-sql-web`     | Windows 2016 SQLServer(Web)|
| `windows2016-sql-standard`| Windows 2016 SQLServer(Standard)|
| `windows2016-sql2017-standard`| Windows 2016 SQLServer 2017(Standard)|
| `windows2016-sql-standard-all` | Windows 2016 SQLServer(Standard,RDS + Office)|
| `windows2016-sql2017-standard-all` | Windows 2016 SQLServer 2017(Standard,RDS + Office)|
| `windows2019`             | Windows 2019|

> *1: Sophos-UTMを利用する場合、ディスクの修正機能は利用できません。  
>     詳細は[さくらのクラウド ドキュメント](https://manual.sakura.ad.jp/cloud/os-packages/sophosutm.html)を参照してください。

> *2: Netwiser Virtual Editionを利用する場合、ディスクの修正機能は利用できません。  
>     詳細は[さくらのクラウド ドキュメント](https://manual.sakura.ad.jp/cloud/os-packages/netwiser/about.html)を参照してください。

### os_type指定時の注意点

詳細は[ディスクリソースの"コピー元アーカイブ/ディスクの指定 / アーカイブID変更時のリソース再生成の抑制"セクション](https://sacloud.github.io/terraform-provider-sakuracloud/configuration/resources/disk/)を参照してください。

### 属性

|属性名                | 名称                    | 補足                                        |
|---------------------|------------------------|--------------------------------------------|
| `id`                | アーカイブID             | -                                          |
| `name`              | アーカイブ名             | -         |
| `size`              | アーカイブサイズ(GB単位)  | -        |
| `archive_file`      | アーカイブファイルパス    | -          |
| `hash`              | アーカイブファイルのMD5ハッシュ値| `archive_file`の変更検知用MD5ハッシュ |
| `icon_id`           | アイコンID         |  - |
| `description`       | 説明  | -  |
| `tags`              | タグ | -  |
| `zone`              | ゾーン | -  |

