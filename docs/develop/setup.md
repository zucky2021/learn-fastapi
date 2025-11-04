# 環境構築

## 前提

- uv インストール済みであること

```sh
uv -V 
uv 0.9.6 (Homebrew 2025-10-29)
```

## 手順

```sh
# プロジェクトの初期化（仮想環境も自動作成）
uv init

# uvicorn(ASGIサーバー)のインストール
uv add "uvicorn[standard]"

# FastAPIも追加
uv add fastapi

# アプリの実行
uv run uvicorn main:app --reload
```
