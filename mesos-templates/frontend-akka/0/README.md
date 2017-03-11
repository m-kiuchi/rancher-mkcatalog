# フロントエンド - Akka

フロントエンドシェル用に利用できる CentOS7 イメージです。Lightbend Activatorを含むAkkaフレームワークが同梱されています。sshでログインすることができます。

## 使用方法

以下の項目を入力・選択します

- Template Version: 使用したいバージョンのテンプレートを選択します
- New Stack:Name: スタック名に使用されます
- 設定項目
  - SSH user name: sshログインするためのユーザ名(デフォルト: root)

`Launch` ボタンを押します。

上部メニューから [<Environment名>]-[Infrastructure] を選択します

![01.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-akka/0/01.jpg)

作成したスタック名をクリックします。ここでは `frontend-akka` を選択します。

![02.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-akka/0/02.jpg)

サービス名を選択します。ここでは `frontend-akka` を選択します。

![03.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-akka/0/03.jpg)

コンテナの稼動状態が表示されます。コンテナにはsshログインすることができます。

sshログインのための情報を取得するには、コンテナ名をクリックします。

![04.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-akka/0/04.jpg)

コンテナの稼働状況が表示されます。コンテナの稼働状況画面の下側でsshログインのための各種情報を確認することができます。

  - ssh接続先ホスト名、ポート番号
  - activator ui用ポート番号(activator ui起動後、ブラウザで開くことができます)

![05.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-akka/0/05.jpg)

また、コンテナ稼働状況の右上のメニューから [View Logs] を選択すると、コンテナ起動時に設定されたユーザ名とパスワードが表示されます。

![06.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-akka/0/06.jpg)

![07.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-akka/0/07.jpg)

![08.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/frontend-akka/0/08.jpg)

## sshでログイン

sshは以下のように実行します

```
$ ssh -l <ユーザ名> -p <ポート番号> <接続先IPアドレス>
```

root以外のユーザでログインした場合、管理者権限コマンドを実行するときは `sudo` を使用します

```
$ sudo <コマンド>
```

## Lightbend Activatorを起動する

```shell
$ activator ui -Dhttp.address=0.0.0.0
```

ブラウザからコンテナのポート番号8888(ホスト側ではリダイレクトされて他のポート番号になっています)を開きます
