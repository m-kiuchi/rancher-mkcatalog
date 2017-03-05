# Apache Spark 2.0.2 for Mesos on Rancher

Mesos on Rancher 環境で使用できる Apache Spark テンプレートです。

## 使用方法

### テンプレートの起動とログインパスワードの確認

以下の項目を入力・選択します

- Template Version: 使用したいバージョンのテンプレートを選択します
- New Stack:Name: スタック名に使用されます
- 設定項目
  - SSH user name: sshログインするためのユーザ名(デフォルト: spark)

`Launch` ボタンを押します。

上部メニューから [<Environment名>]-[Infrastructure] を選択します

![01.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/spark/0/01.jpg)

作成したスタック名をクリックします。ここでは `Spark` を選択します。

![02.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/spark/0/02.jpg)

`sparkdriver` を選択します

![03.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/spark/0/03.jpg)

コンテナ名を選択します。ここでは `spark-sparkdriver-1` を選択します。

![04.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/spark/0/04.jpg)

コンテナの稼働状況が表示されます。右上のメニューから [View Logs] を選択すると、コンテナ起動時に設定されたユーザ名とパスワードが表示されます。

![05.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/spark/0/05.jpg)

![06.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/spark/0/06.jpg)

![07.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/spark/0/07.jpg)

コンテナの稼働状況画面の下側で各種情報を確認することができます。

  - ssh接続先ホスト名、ポート番号
  - ジョブ実行中に使用できるSpark UIのポート番号

![08.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/spark/0/08.jpg)

### sshでログイン

sshは以下のように実行します

```
$ ssh -l <ユーザ名> -p <ポート番号> <接続先IPアドレス>
```

root以外のユーザでログインした場合、管理者権限コマンドを実行するときは `sudo` を使用します

```
$ sudo <コマンド>
```

### Sparkの起動

