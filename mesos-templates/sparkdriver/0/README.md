# フロントエンド - CentOS7

フロントエンドシェル用に利用できる CentOS7 イメージです。sshでログインすることができます。

## 使用方法

以下の項目を入力・選択します

- Template Version: 使用したいバージョンのテンプレートを選択します
- New Stack:Name: スタック名に使用されます
- 設定項目
  - SSH user name: sshログインするためのユーザ名(デフォルト: root)

`Launch` ボタンを押します。

上部メニューから [INFRASTRUCTURE]-[Containers] を選択します

![01.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-centos7/0/01.jpg)

コンテナ一覧から <スタック名>-<イメージ名>-<番号> の適切なコンテナを検索します。ここでは `mk2-frontend-centos7-1` を選択します。

![02.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-centos7/0/02.jpg)

コンテナの稼働状況が表示されます。右上のメニューから [View Logs] を選択すると、コンテナ起動時に設定されたユーザ名とパスワードが表示されます。

![03.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-centos7/0/03.jpg)

![04.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-centos7/0/04.jpg)

![05.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-centos7/0/05.jpg)

コンテナの稼働状況画面の左上のスタック名をクリックすると、ssh接続先のIPアドレスをポート番号を確認することができます

![06.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-centos7/0/06.jpg)

![07.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-centos7/0/07.jpg)

## sshでログイン

sshは以下のように実行します

```
$ ssh -l <ユーザ名> -p <ポート番号> <接続先IPアドレス>
```

root以外のユーザでログインした場合、管理者権限コマンドを実行するときは `sudo` を使用します

```
$ sudo <コマンド>
```
