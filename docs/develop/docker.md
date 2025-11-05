# Docker環境での実行

## 前提

- Dockerがインストール済みであること
- Docker Composeがインストール済みであること

```sh
docker --version
docker compose version
```

## 開発環境と本番環境

このプロジェクトでは、マルチステージビルドを使用して開発環境（`dev`）と本番環境（`prod`）を分けています。

### 開発環境（dev）

- 開発依存関係もインストール
- ホットリロード機能が有効
- デバッグに適した設定

### 本番環境（prod）

- 本番依存関係のみインストール（軽量）
- ヘルスチェック機能が有効
- セキュリティとパフォーマンスを最適化

### 使い分け

```sh
# 開発環境（docker-compose.ymlで自動的にdevステージを使用）
docker compose up

# 本番環境のイメージをビルド
docker build --target prod -t learn-fastapi:prod .
```

## 手順

### 1. イメージのビルドと起動

```sh
# コンテナをビルドして起動（バックグラウンドで実行）
docker compose up -d

# ログを確認
docker compose logs -f

# コンテナを停止
docker compose down
```

### 2. 開発モード（ホットリロード）

`docker-compose.yml`では、コード変更が自動的に反映されるようになっています。

```sh
# 起動
docker compose up

# コードを編集すると自動でリロードされます
```

### 3. その他の便利なコマンド

```sh
# コンテナの状態を確認
docker compose ps

# コンテナ内でコマンドを実行
docker compose exec api bash

# ログを確認
docker compose logs api

# コンテナを再起動
docker compose restart

# イメージを再ビルド
docker compose build --no-cache
```

## アクセス

起動後、以下のURLでアクセスできます：

- API: <http://localhost:8000>
- APIドキュメント: <http://localhost:8000/docs>
- 代替APIドキュメント: <http://localhost:8000/redoc>

## トラブルシューティング

### ポートが既に使用されている場合

`docker-compose.yml`の`ports`セクションを変更：

```yaml
ports:
  - "8001:8000"  # ホストの8001ポートを使用
```

### 依存関係を再インストールする場合

```sh
# コンテナを再ビルド
docker compose build --no-cache
docker compose up -d
```
