# Local FaunaDB with Docker 🕊🐳

開発時のローカルでの動作確認等を目的としたものです。
お使いの環境に合わせて `docker-compose.yml` に記述されている設定を変更してお使いください。

公式のドキュメントが参考になります。
https://docs.fauna.com/fauna/current/start/dev

## セットアップ

### 必要なもの・環境条件等

- Node.js
- Docker

### コンテナ構築

公式のDockerイメージである**fauna/faunadb**を利用します。

```bash
docker-compose up -d
```

参考 : https://hub.docker.com/r/fauna/faunadb

### fauna-shellの導入

```bash
npm i -g fauna-shell
```

以上で、`fauna`コマンドがインストールできました。続いて、ローカルのエンドポイントを追加します。

```bash
fauna add-endpoint http://localhost:8443

# もしくはファイルに直接編集する方法もあります
vi ~/.fauna-shell
```

ファイルを書き込む場合は、内容を次のようにします。

```
[localhost]
domain=127.0.0.1
port=8443
scheme=http
secret=secret
```

次のコマンドで**localhost**が現れることを確認します。

```bash
fauna list-endpoints
```

最後に接続してみます。

```bash
fauna shell --endpoint localhost

# もしくはデフォルトでlocalhostとする場合
fauna default-endpoint localhost
fauna shell
```

接続後にAdd関数を実行します。以下のように`2`が出力されれば大丈夫です🎉

```
> Add(1, 1)
2
```

参考 : https://github.com/fauna/fauna-shell

## おまけ

主なDockerの操作コマンドを載せておきます。

```bash
# コンテナ構築と起動（必要に応じて、dオプションをつけてください）
docker-compose up -d

# コンテナ起動
docker-compose start

# 停止
docker-compose stop

# 削除
docker-compose down

# データボリュームの削除 (docker volume lsで探す)
docker volume rm ボリューム名
```
