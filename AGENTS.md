# プロジェクト概要: Tailspin Shelter

このドキュメントは、AI開発アシスタントがこのプロジェクトの構造と目的を理解するための概要を提供します。

## 概要

このプロジェクトは、犬の保護施設「Tailspin Shelter」のウェブアプリケーションです。フロントエンド、バックエンド、データベースで構成されるフルスタックアプリケーションのサンプルとして、ペット（犬）の情報を管理します。

## 技術スタック

### フロントエンド (`client/`)

-   **フレームワーク:** [Astro](https://astro.build/)
-   **UIコンポーネント:** [Svelte](https://svelte.dev/)
-   **言語:** TypeScript
-   **パッケージ管理:** npm
-   **E2Eテスト:** [Playwright](https://playwright.dev/)
-   **主要ファイル:** [`client/src/pages/index.astro`](client/src/pages/index.astro), [`client/src/components/DogList.svelte`](client/src/components/DogList.svelte)

### バックエンド (`server/`)

-   **フレームワーク:** [Flask](https://flask.palletsprojects.com/) (Python)
-   **データベース:** SQLite
-   **ORM:** [SQLAlchemy](https://www.sqlalchemy.org/)
-   **主な依存関係:** `flask`, `sqlalchemy`, `flask_sqlalchemy`, `flask-cors`
-   **主要ファイル:** [`server/app.py`](server/app.py)
-   **テスト:** `unittest` ([`server/test_app.py`](server/test_app.py))

### 開発環境

-   Dev Container ([`.devcontainer/devcontainer.json`](.devcontainer/devcontainer.json))

## ディレクトリ構造

-   `client/`: Astroで構築されたフロントエンドアプリケーションのソースコードが含まれています。
    -   `src/pages/`: 各ページのコンポーネント。
    -   `src/components/`: 再利用可能なSvelteコンポーネント。
-   `server/`: Flaskで構築されたバックエンドAPIのソースコードが含まれています。
    -   `app.py`: APIエンドポイントを定義するメインファイル。
    -   `models/`: SQLAlchemyのデータベースモデル。
    -   `dogshelter.db`: SQLiteデータベースファイル。
-   `scripts/`: アプリケーションの起動などを補助するスクリプトが含まれています。

## アーキテクチャのポイント

-   **API通信:** フロントエンドは、Astroのミドルウェア ([`client/src/middleware.ts`](client/src/middleware.ts)) を使用して、`/api/*` へのリクエストをバックエンドのFlaskサーバー (デフォルト `http://localhost:5100`) に転送します。
-   **データモデル:**
    -   `Dog`: [`server/models/dog.py`](server/models/dog.py) で定義されています。
    -   `Breed`: [`server/models/breed.py`](server/models/breed.py) で定義されています。

## 開発ルール
### バックエンド

- FlaskとSQLAlchemyを使用して構築
- 型ヒントを使用

### フロントエンド

- AstroとSvelteを使用して構築
- TypeScriptはfunctionキーワードではなくアロー関数を使用すべき
- ページはモダンな外観と感触のダークモードであるべき

## 起動方法

プロジェクトのルートディレクトリで [`scripts/start-app.sh`](scripts/start-app.sh) (Linux/macOS) または [`scripts/start-app.ps1`](scripts/start-app.ps1) (Windows) を実行すると、バックエンドとフロントエンドの両方のサーバーが起動します。

```bash
./scripts/start-app.sh
```

このスクリプトは以下の処理を自動的に行います。

1.  Pythonの仮想環境 (`venv`) をセットアップし、必要な依存関係を `server/requirements.txt` からインストールします。
2.  Flaskバックエンドサーバーを `http://localhost:5100` で起動します。
3.  `npm install` を実行してフロントエンドの依存関係をインストールします。
4.  Astroフロントエンド開発サーバーを `http://localhost:4321` で起動します。

-   フロントエンド: `http://localhost:4321`
-   バックエンド: `http://localhost:5100`

### 主要なAPIエンドポイント

-   `GET /api/dogs`: 登録されているすべての犬のリストを取得します。
-   `GET /api/dogs/<id>`: 指定されたIDの犬の詳細情報を取得します。
-   `GET /api/breeds`: 登録されているすべての犬種のリストを取得します。

### データベース

-   **テーブル:** `dogs` と `breeds` の2つの主要なテーブルがあります。
-   **初期データ:** `server/models/dogs.csv` と `server/models/breeds.csv` が初期データとして提供されており、`server/utils/seed_database.py` を使ってデータベースに投入されます。
プロジェクトのルートディレクトリで [`scripts/start-app.sh`](scripts/start-app.sh) (Linux/macOS) または [`scripts/start-app.ps1`](scripts/start-app.ps1) (Windows) を実行すると、バックエンドとフロントエンドの両方のサーバーが起動します。```



- フロントエンド: `http://localhost:4321`このスクリプトは以下の処理を自動的に行います。

- バックエンド: `http://localhost:5100`

1.  Pythonの仮想環境 (`venv`) をセットアップし、必要な依存関係を `server/requirements.txt` からインストールします。
2.  Flaskバックエンドサーバーを `http://localhost:5100` で起動します。
3.  `npm install` を実行してフロントエンドの依存関係をインストールします。
4.  Astroフロントエンド開発サーバーを `http://localhost:4321` で起動します。

### 主要なAPIエンドポイント

- `GET /api/dogs`: 登録されているすべての犬のリストを取得します。
- `GET /api/dogs/<id>`: 指定されたIDの犬の詳細情報を取得します。
- `GET /api/breeds`: 登録されているすべての犬種のリストを取得します。

### データベース

- **テーブル:** `dogs` と `breeds` の2つの主要なテーブルがあります。
- **初期データ:** `server/models/dogs.csv` と `server/models/breeds.csv` が初期データとして提供されており、`server/utils/seed_database.py` を使ってデータベースに投入されます。
