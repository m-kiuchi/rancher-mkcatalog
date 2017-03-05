# Apache Kafka 0.10.2

Rancher 環境で使用できる Apache Kafka テンプレートです

## 使用方法

### テンプレートの起動とログインパスワードの確認

以下の項目を入力・選択します

- Template Version: 使用したいバージョンのテンプレートを選択します
- New Stack:Name: スタック名に使用されます
- 設定項目
  - NODE_COUNT: Kafka Broker数(デフォルト: 3)
  - SSH user name: sshログインするためのユーザ名(デフォルト: kafka)

`Launch` ボタンを押します。

上部メニューから [<Environment名>]-[Infrastructure] を選択します

![01.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/kafka/0/01.jpg)

作成したスタック名をクリックします。ここでは `kafka` を選択します。

![02.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/kafka/0/02.jpg)

サービス名を選択します。ここでは `kafka` を選択します。

![03.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/kafka/0/03.jpg)

各コンテナ(Broaker)の稼動状態が表示されます。いずれのBroakerにもsshログインすることができます。

sshログインのための情報を取得するには、各コンテナをクリックします。

![04.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/kafka/0/04.jpg)

コンテナの稼働状況が表示されます。コンテナの稼働状況画面の下側でsshログインのための各種情報を確認することができます。

  - ssh接続先ホスト名、ポート番号

![05.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/kafka/0/05.jpg)

また、コンテナ稼働状況の右上のメニューから [View Logs] を選択すると、コンテナ起動時に設定されたユーザ名とパスワードが表示されます。

![06.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/kafka/0/06.jpg)

![07.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/kafka/0/07.jpg)

![08.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/kafka/0/08.jpg)

### sshでログイン

sshは以下のように実行します

```
$ ssh -l <ユーザ名> -p <ポート番号> <接続先IPアドレス>
```

root以外のユーザでログインした場合、管理者権限コマンドを実行するときは `sudo` を使用します

```
$ sudo <コマンド>
```

### kafkaの使用方法

#### トピックの作成

- replication-factor: 入力されたメッセージのレプリカ数。増やすほど冗長度が上がる
- partitions: トピックのパーティション数。増やすほど並列処理になる( 推奨: (1-100) * broker数 * レプリケーション数 )
- topic: トピック名。任意の文字

(例)

```shell
$ kafka-topics --create --replication-factor 3 --partitions 9 --topic my-replicated-topic
```
#### トピックの稼働状況を表示

- topic: トピック名。任意の文字

(例)

```shell
$ kafka-topics --describe --topic my-replicated-topic
```

#### トピックの削除

- topic: トピック名。任意の文字

(例)

```shell
$ kafka-topics --delete --topic my-replicated-topic
```

#### トピックのリバランス

Brokerノードが増減して負荷に偏りが出た時に、各 partition のリーダーを平滑化し、負荷を平準する

(例)

```shell
$ kafka-preferred-replica-election
```
