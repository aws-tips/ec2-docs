# 【AWSメモ④】aws-cli セットアップ（Amazon Linux 2）

## 環境

・Amazon Linux 2  

・Python2.7.14（デフォルト）



## pip のインストール

Amazon Linux 2 には、pip が入っていない（何もいじっていなければ）ので、

以下のコマンドを実行してインストールする。

```shell
$ curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
$ sudo python get-pip.py
```



## aws-cli のインストール

pip コマンドで aws-cli をインストール



```shell
$ sudo pip install awscli
```



## aws-cli の設定

aws-cli の設定を行う。  

AWS アクセスキー ID 、 AWS シークレットアクセスキー（アカウントの認証情報）とデフォルトに指定するリージョン（別にどこでも良い）、aws-cli を使用した際に画面上に表示される出力結果のフォーマットを指定（JSON、text、table のいずれか）する。  

※ アクセスキーが不明な場合は、マネジメントコンソールのIAM設定から認証情報を確認すること。



```shell
$ aws configure
AWS Access Key ID [None]: ABCDEFGXXXXXXXXXXX
AWS Secret Access Key [None]: hogehogehoge/DEDEDEDE/XXXXXXXXXXXXX
Default region name [None]: ap-northeast-1
Default output format [None]: json
```

以上で、セットアップは完了。
