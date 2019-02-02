# Redhat7.6 に Apache2.4入れてみた

EC2 RedHat7.6  
T2.micro  

セキュリティグループとか何も設定してない

```
# とりあえずアップデートする
$ sudo yum repolist all
$ sudo yum update
```

RHEL標準のApacheをインストール

```
# 標準のApache(httpd)をインストール
$ sudo yum install httpd -y
```

インストール直後にApacheの起動を確認する。

```
# 起動
$ sudo systemctl start httpd

# 状態の確認
$ sudo systemctl status httpd
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
   Active: active (running) since Sat 2019-02-02 01:06:28 UTC; 1min 21s ago
     Docs: man:httpd(8)
           man:apachectl(8)
 Main PID: 29765 (httpd)
   Status: "Total requests: 0; Current requests/sec: 0; Current traffic:   0 B/sec"
   CGroup: /system.slice/httpd.service
           ├─29765 /usr/sbin/httpd -DFOREGROUND
           ├─29766 /usr/sbin/httpd -DFOREGROUND
           ├─29767 /usr/sbin/httpd -DFOREGROUND
           ├─29768 /usr/sbin/httpd -DFOREGROUND
           ├─29769 /usr/sbin/httpd -DFOREGROUND
           └─29770 /usr/sbin/httpd -DFOREGROUND

Feb 02 01:06:28 ip-10-0-45-109.ap-northeast-1.compute.internal systemd[1]: Starting The Apache HTTP Server...
Feb 02 01:06:28 ip-10-0-45-109.ap-northeast-1.compute.internal systemd[1]: Started The Apache HTTP Server.
```

※ 環境によるが起動時にWarningが発生するの場合があるので、原因となるファイルを修正する。

```
# 「ServerName localhost:80」を追記する
$ sudo vi /etc/httpd/conf/httpd.conf
```

最後に自動起動設定を行う。

```
$ sudo systemctl enable httpd
```
