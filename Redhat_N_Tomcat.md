
# WIP:AWS RedHat7.6(HVM)にTomcat9を入れてみた

前提条件：JDK8はインストール済み
　　　　　EC2 RedHat7.6
　　　　　T2.micro

Tomcatをデーモン起動で使用する場合、gccが必要となるのでインストール

```
# gccパッケージのインストール
$ sudo yum install -y gcc
```

Tomcatモジュールの取得 & 解凍
```
# 最新版をwgetで取得
$ wget http://ftp.yz.yamagata-u.ac.jp/pub/network/apache/tomcat/tomcat-9/v9.0.13/bin/apache-tomcat-9.0.13.tar.gz

#  解凍して/opt配下に移動
$ sudo tar zxvf apache-tomcat-9.0.13.tar.gz -C /opt/
```

Tomcatをデーモンとして使用する際に必要となるjsvcのコンパイルを行う

```
# ディレクトリに移動してコンパイル実行
$ cd /opt/apache-tomcat-9.0.13
$ sudo tar zxvf ./bin/commons-daemon-native.tar.gz

$ cd commons-daemon-1.1.0-native-src/unix/
$ ./configure --with-java=/usr/java/latest

$ make

$ sudo cp -piv jsvc /opt/apache-tomcat-9.0.13/bin/
$ cd /opt/apache-tomcat-9.0.13/

# 確認
$ sudo ls -l ./bin/jsvc
-rwxrwxr-x. 1 ec2-user ec2-user 174056 Dec 11 12:08 ./bin/jsvc
```
