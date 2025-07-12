## セットアップ手順

詳細は [「スキーマ変更で障害が起きたら...」から解放！Supabase CLIで安心チーム開発](https://shiftb.dev/me/blog/TyuN4ipm_fA0)を参照してください。

### 1. リポジトリのクローン

```
git clone https://github.com/shiftb-hub/tasq.git
cd tasq
```

上記でクローンすると、カレントフォルダのなかに `tasq` というフォルダが新規作成されて展開されます。別名にしたいときは、たとえば `hoge` というフォルダにクローンしたいときは、次のようにしてください。

```
git clone https://github.com/shiftb-hub/tasq.git hoge
cd hoge
```

### 2. 依存関係のインストール

```bash
npm i
```

### 3. 起動

次のコマンドで Supabase を起動します。

```bash
npx supabase start
```

起動すると以下のように接続情報が表示されます。http://127.0.0.1:54323 で SupabaseStudio に接続できます。

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

### 4. Prisma から接続するときの環境変数設定

```
DATABASE_URL=postgresql://postgres:postgres@127.0.0.1:54322/postgres
DIRECT_URL=postgresql://postgres:postgres@127.0.0.1:54322/postgres
NEXT_PUBLIC_SUPABASE_URL=http://127.0.0.1:54321
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJxxxxxxxxxxxx
```

### 5. 停止

次のコマンドで Supabase を停止します。

```bash
npx supabase stop
```

停止後、`docker ps -a` を実行し、コンテナの残骸が残っているときは、次のコマンドで掃除してください。

```bash
docker rm $(docker ps -a -q --filter "name=supabase_vector_tasq-sb-dev")
```
