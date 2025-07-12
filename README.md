## セットアップ手順

詳細は [「スキーマ変更で障害が起きたら...」から解放！Supabase CLIで安心チーム開発](https://shiftb.dev/blog/TyuN4ipm_fA0)を参照してください。

なお、Docker がセットアップされていることが前提となります。

### 1. リポジトリのクローン

```
git clone https://github.com/shiftb-hub/tasq-sb-dev.git
cd tasq-sb-dev
```

### 2. 依存関係のインストール

```bash
npm i
```

### 3. 起動

次のコマンドで、ローカル環境に構築した Supabase を起動します。初回は時間がかかる場合があります。

```bash
npx supabase start
```

起動に成功すると、以下のように接続情報が表示されます。Supabase Studio には http://127.0.0.1:54323 からアクセス可能です。

```
Started supabase local development setup.

         API URL: http://127.0.0.1:54321
     GraphQL URL: http://127.0.0.1:54321/graphql/v1
  S3 Storage URL: http://127.0.0.1:54321/storage/v1/s3
          DB URL: postgresql://postgres:postgres@127.0.0.1:54322/postgres
      Studio URL: http://127.0.0.1:54323
    Inbucket URL: http://127.0.0.1:54324
      JWT secret: super-secret-jwt-token-with-at-least-32-characters-long
        anon key: eyJhbGc....
service_role key: eyJhbGc....
   S3 Access Key: 625729....
   S3 Secret Key: 850181....
       S3 Region: local
```

### 4. Prisma から接続するときの環境変数の設定

Next.js 環境で、Prisma からローカルの Supabase に接続するには `.env` を以下のように設定します。

```
DATABASE_URL=postgresql://postgres:postgres@127.0.0.1:54322/postgres
DIRECT_URL=postgresql://postgres:postgres@127.0.0.1:54322/postgres
NEXT_PUBLIC_SUPABASE_URL=http://127.0.0.1:54321
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhb.....
SB_SERVICE_ROLE_KEY=eyJhb.....
```

`SB_SERVICE_ROLE_KEY` は、開発環境でユーザ関連のシーディング処理を実行するために設定します。

### 5. 停止

次のコマンドで Supabase を停止します。

```bash
npx supabase stop
```

停止後、`docker ps -a` でコンテナが残っていないか確認し、不要なものがある場合は次のコマンドで削除してください。

```bash
docker rm $(docker ps -a -q --filter "name=supabase_vector_tasq-sb-dev")
```

### 6. 完全初期化

ボリューム（DB やストレージの永続化領域）を初期化する場合は、以下のコマンドを実行します。

```
docker volume ls
```

表示されたボリューム名を確認し、以下のコマンドで削除します。

```
docker volume rm supabase_config_tasq-sb-dev supabase_db_tasq-sb-dev supabase_storage_tasq-sb-dev
```