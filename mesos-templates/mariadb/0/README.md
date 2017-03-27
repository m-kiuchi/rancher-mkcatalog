# MariaDB 10.1.22

Rancher 環境で使用できる MariaDB テンプレートです。

## 使用方法

### テンプレートの起動とログインパスワードの確認

以下の項目を入力・選択します

- Template Version: 使用したいバージョンのテンプレートを選択します
- New Stack:Name: スタック名に使用されます
- 設定項目
  - root password of mariadb: MariaDBのrootアカウントにセットするパスワードを指定します。(デフォルト: "maria")

`Launch` ボタンを押します。

### MariaDBとの接続

コンテナ状況表示画面より、MariaDBとの接続に使用する IP アドレス、ポート番号を確認します。

Rancherコンテナ内部から接続する場合、
   - IPアドレスは 10.42.0.0/16 のアドレスになります
   - ポート番号は MariaDB デフォルトポート番号である、 3306 になります

Rancherコンテナの外から接続する場合、
   - IPアドレスは MariaDB コンテナをホストしている Rancher Host のIPアドレスになります
   - ポート番号は、Rancherのコンテナ状況表示画面に表示されたポート番号になります

MariaDB クライアントから、以下のコマンドで接続します

```shell
$ mysql --host=<IPアドレス> --port=<ポート番号> --user=root --password=<パスワード>
```


