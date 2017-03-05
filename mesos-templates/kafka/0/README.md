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

