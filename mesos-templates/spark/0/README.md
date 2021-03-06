# Apache Spark 2.0.2 for Mesos on Rancher

Mesos on Rancher 環境で使用できる Apache Spark テンプレートです。Lightbend Activatorを含むAkkaフレームワークが同梱されています。

## 注意事項

Mesos slave上でスムーズにジョブが実行されるように、事前にMesos slave上で `docker pull` コマンドを使用して、Spark Executor イメージを事前展開することをおすすめします。

```shell
$ sudo docker pull mkiuchicl/sparkexecutor
```

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
  - Lightbend activator ui起動中に使用できるポート番号

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

#### Spark Shellの起動

sshログイン後に、コマンドプロンプトから以下のようにタイプします。必ず root アカウントで実行する必要があります。

```shell
$ sudo su -
# spark-shell
```

以下のように Spark Shell が起動することがわかります。

```shell
Using Spark's default log4j profile: org/apache/spark/log4j-defaults.properties
Setting default log level to "WARN".
To adjust logging level use sc.setLogLevel(newLevel).
17/03/05 06:41:55 WARN NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
I0305 06:41:56.855275   212 sched.cpp:222] Version: 0.28.1
I0305 06:41:56.861089   204 sched.cpp:326] New master detected at master@10.42.133.167:5050
I0305 06:41:56.861368   204 sched.cpp:336] No credentials provided. Attempting to register without authentication
I0305 06:41:56.869216   204 sched.cpp:703] Framework registered with 50396a44-db5d-4d3d-8857-5c93b6bf71f3-0022
17/03/05 06:41:57 WARN SparkContext: Use an existing SparkContext, some configuration may not take effect.
Spark context Web UI available at http://10.42.255.42:4040
Spark context available as 'sc' (master = mesos://10.42.133.167:5050, app id = 50396a44-db5d-4d3d-8857-5c93b6bf71f3-0022).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.0.2
      /_/
         
Using Scala version 2.11.8 (OpenJDK 64-Bit Server VM, Java 1.8.0_121)
Type in expressions to have them evaluated.
Type :help for more information.

scala>
```
#### Spark submit でジョブをサブミットする

sshログイン後に、コマンドプロンプトから以下のようにタイプします。必ず root アカウントで実行する必要があります。

(例)

```shell
$ sudo su -
# spark-submit --class org.apache.spark.examples.SparkPi /opt/spark/examples/jars/spark-examples_2.11-2.0.2.jar 10
```

以下のように実行されます

```shell
17/03/05 08:24:12 WARN NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
I0305 08:24:13.786136   201 sched.cpp:222] Version: 0.28.1
I0305 08:24:13.789535   198 sched.cpp:326] New master detected at master@10.42.133.167:5050
I0305 08:24:13.789885   198 sched.cpp:336] No credentials provided. Attempting to register without authentication
I0305 08:24:13.796597   198 sched.cpp:703] Framework registered with 50396a44-db5d-4d3d-8857-5c93b6bf71f3-0035
17/03/05 08:24:14 WARN SparkContext: Use an existing SparkContext, some configuration may not take effect.
Pi is roughly 3.1423391423391425                                                
17/03/05 08:24:36 WARN MesosCoarseGrainedSchedulerBackend: Timed out waiting for 3 remaining executors to terminate within 10000 ms. This may leave temporary files on the mesos nodes.
I0305 08:24:36.502816   151 sched.cpp:1903] Asked to stop the driver
I0305 08:24:36.502991   193 sched.cpp:1143] Stopping framework '50396a44-db5d-4d3d-8857-5c93b6bf71f3-0035'
```
### Lightbend Actibator UIの起動

Lightbend Activatorを起動する

```shell
$ activator ui -Dhttp.address=0.0.0.0
```

ブラウザからコンテナのポート番号8888(ホスト側ではリダイレクトされて他のポート番号になっています)を開きます

