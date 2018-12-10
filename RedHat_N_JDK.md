AWS RedHat7.6(HVM)にOracle JDK8 入れてみた

EC2 RedHat7.6
T2.micro

セキュリティグループとか何も設定してない

```
# とりあえずアップデートする
$ sudo yum repolist all
$ sudo yum update
```

tar.gzまたはrpmファイルからの２通りの方法があるが、
今回はrpmファイルで実施

```
# wget すら入っていないのでwgetを入れる
$ sudo yum install -y wget

# URLはChromeでJDKのライセンス条約に同意ボタン押下後、右クリックで取得できる
$ sudo wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/8u192-b12/750e1c8617c5452694857ad95c3ee230/jdk-8u192-linux-x64.rpm

# rpmをインストールする
$ sudo rpm -ivh jdk-8u192-linux-x64.rpm

# インストール後の確認
$ java -version
java version "1.8.0_192"
Java(TM) SE Runtime Environment (build 1.8.0_192-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.192-b12, mixed mode)

# 実態がどこにあるのかを確認
$ which java
/usr/bin/java

$ ls -la /usr/bin/java
lrwxrwxrwx. 1 root root 22 Dec 10 11:39 /usr/bin/java -> /etc/alternatives/java

$ ls -la /etc/alternatives/java
lrwxrwxrwx. 1 root root 41 Dec 10 11:39 /etc/alternatives/java -> /usr/java/jdk1.8.0_192-amd64/jre/bin/java
```

実態は/usr/java/jdk1.8.0_192-amd64/jre/bin/javaに作成される
