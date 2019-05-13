# DockerでWordPressを構築(ついでにVirtualHostもやる)最小構成

WordPressってローカルで環境構築するためにはサーバーが必要だったりDBの連携がうまくいかなかったりですごく面倒になった経験はありませんか？

私はあります。なので必要最低限の構成でサクッとDockerで構築できるようにしておきました。

## Githubから一瞬で環境構築
```
git clone git@github.com:usu-blog/docker-wp-min.git
```

構成は以下です。
```
.
├── README.md
├── db-data  # volumes
├── docker-compose.yml
├── .env # 環境変数
└── wp-content # volumes
```

docker-composeで構築した時volumeがなければデータはdownした時に消えてしまうのでセーブデータが欲しければホストマシンに必要な部分だけ残すのが仕様です。

## セーブするために必要な箇所
- MySQLやMariaDBは`/var/lib/mysql`以下のデータがあればセーブできる。
- WordPressは`/var/www/html/wp-content`以下のデータがあればセーブできる。


## 環境変数とVirtualHostを設定
まず`.env`を編集してDB名とかパスワードとかVirtualHost名を決めます。
決めたVirtualHostはホストマシンの`/etc/hosts`に登録することで使えるようになります。
localhostの右に半角の空白を入れたあと横に並べて書けば準備完了。

- `/etc/hosts`
```
127.0.0.1 localhost [host名]
```

## 起動！！

それでは起動します。
```
docker-compose up -d
```

ブラウザを確認
http://[host名]

終了は以下のコマンド
```
docker-compose down
```

## 注意点
ドメインを変えることで複数のWordPressを立ち上げることができるはずです。  
気をつけないといけないのは、DBのホスト名がかぶった時に動かなくなるので気をつける必要があります。

## ひとこと  
とても簡単だったと思います。  
これでローカルのWordPress構築で手こずることはなくなったはずです。  
今後も最小構成をGithubに上げておいて乱用することで作業効率を上げていきましょう！