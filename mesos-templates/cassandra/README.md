# Cassandra

Apache Cassandra 分散 Key-value 型データベースです。

## 使用方法

以下の項目を入力・選択します

- Template Version: 使用したいバージョンのテンプレートを選択します
- New Stack:Name: スタック名に使用されます
- 設定項目
  - NODE_COUNT: Cassandraのノード数。ただしシードノードを除く(デフォルト: 2)
  - SSH user name: sshログインするためのユーザ名(デフォルト: cassandra)

`Launch` ボタンを押します。

上部メニューから [<Environment名>]-[Infrastructure] を選択します

![01.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/cassandra/0/01.jpg)

作成したスタック名をクリックします。ここでは `cassandra` を選択します。

![02.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/cassandra/0/02.jpg)

サービス名を選択します。ここでは `seed` を選択します。

![03.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/cassandra/0/03.jpg)

コンテナの稼動状態が表示されます。コンテナにはsshログインすることができます。

sshログインのための情報を取得するには、コンテナ名をクリックします。

![04.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/cassandra/0/04.jpg)

コンテナの稼働状況が表示されます。コンテナの稼働状況画面の下側でsshログインのための各種情報を確認することができます。

  - ssh接続先ホスト名、ポート番号
  - cassandra内部同期用ポート番号

![05.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/cassandra/0/05.jpg)

また、コンテナ稼働状況の右上のメニューから [View Logs] を選択すると、コンテナ起動時に設定されたユーザ名とパスワードが表示されます。

![06.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/cassandra/0/06.jpg)

![07.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/cassandra/0/07.jpg)

![08.jpg](https://github.com/m-kiuchi/rancher-mkcatalog/raw/master/mesos-templates/cassandra/0/08.jpg)

## sshでログイン

sshは以下のように実行します

```
$ ssh -l <ユーザ名> -p <ポート番号> <接続先IPアドレス>
```

root以外のユーザでログインした場合、管理者権限コマンドを実行するときは `sudo` を使用します

```
$ sudo <コマンド>
```

## Cassandra の動作確認

`nodetool status` および `nodetool info` コマンドを使用します

```shell
$ nodetool status
Datacenter: datacenter1
=======================
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address        Load       Tokens       Owns (effective)  Host ID                               Rack
UN  10.42.115.169  113.36 KiB  256          67.0%             8fd66a4f-f6d0-4a50-ab99-a20ebc4b53dc  rack1
UN  10.42.97.238   108.52 KiB  256          68.1%             b92d5548-d9ad-43d2-932c-831c946b4d3a  rack1
UN  10.42.147.83   113.2 KiB  256          64.9%             59a17d0c-5c59-4455-9e76-e1f3879ea920  rack1
```

```shell
$ nodetool info
ID                     : b92d5548-d9ad-43d2-932c-831c946b4d3a
Gossip active          : true
Thrift active          : false
Native Transport active: true
Load                   : 108.52 KiB
Generation No          : 1489289182
Uptime (seconds)       : 354
Heap Memory (MB)       : 78.96 / 1936.00
Off Heap Memory (MB)   : 0.00
Data Center            : datacenter1
Rack                   : rack1
Exceptions             : 0
Key Cache              : entries 11, size 896 bytes, capacity 96 MiB, 42 hits, 58 requests, 0.724 recent hit rate, 14400 save period in seconds
Row Cache              : entries 0, size 0 bytes, capacity 0 bytes, 0 hits, 0 requests, NaN recent hit rate, 0 save period in seconds
Counter Cache          : entries 0, size 0 bytes, capacity 48 MiB, 0 hits, 0 requests, NaN recent hit rate, 7200 save period in seconds
Chunk Cache            : entries 17, size 1.06 MiB, capacity 452 MiB, 30 misses, 170 requests, 0.824 recent hit rate, 343.499 microseconds miss latency
Percent Repaired       : 100.0%
Token                  : (invoke with -T/--tokens to see all 256 tokens)
```

## Cassandra の使用

Cassandraへのアクセスは `cqlsh` コマンドを使用します。

```shell
$ cqlsh
Connected to mkdefault at 127.0.0.1:9042.
[cqlsh 5.0.1 | Cassandra 3.9 | CQL spec 3.4.2 | Native protocol v4]
Use HELP for help.
cqlsh>
```

### キースペースの作成

キースペースとは、MySQLでいうところのデータベースです。 `CREATE KEYSPACE` 句で作成します。

```shell
cqlsh> CREATE KEYSPACE mkkeyspace WITH replication ={'class': 'SimpleStrategy', 'replication_factor': 2};
```

作成したキースペースを使用するには、 `USE` 句を使用します。

```shell
cqlsh> USE mkkeyspace;
cqlsh:mkkeyspace>
```

### カラムファミリーの作成

カラムファミリーとは、MySQLでいうところのテーブルになります。 カラムファミリーを作成するには、 `CREATE TABLE` 句を使用します。

```shell
cqlsh:mkkeyspace> CREATE TABLE mktable ( mkname text PRIMARY KEY, mkvalue text );
```

作成したカラムファミリーを確認します

```shell
cqlsh:mkkeyspace> SELECT * FROM mktable;

 mkname | mkvalue
--------+---------

(0 rows)
```

### データの投入

`INSERT INTO` 句を使用して、カラムファミリーにデータを投入します。

```shell
cqlsh:mkkeyspace> INSERT INTO mktable (mkname, mkvalue) VALUES ('Mitsutoshi Kiuchi', 'Author');
```

投入したデータを確認します。

```shell
cqlsh:mkkeyspace> SELECT * FROM mktable;

 mkname            | mkvalue
-------------------+---------
 Mitsutoshi Kiuchi |  Author

(1 rows)
```

### カラムファミリーの削除

カラムファミリーを削除するには、 `DROP TABLE` 句を使用します。

```shell
cqlsh:mkkeyspace> DROP TABLE mktable;
```

### キースペースの削除

キースペースを削除するには、 `DROP KEYSPACE` 句を使用します。

```shell
cqlsh> DROP KEYSPACE mkkeyspace;
```

