# プロジェクト概要: Tailspin Shelter# AGENTS.md



このドキュメントは、AI開発アシスタントがこのプロジェクトの構造と目的を理解するための概要を提供します。## プロジェクト概要



## 概要このプロジェクトは、ペット（犬）の情報を管理するためのWebアプリケーションです。フロントエンド、バックエンド、データベースで構成されるフルスタックアプリケーションのサンプルです。



このプロジェクトは、犬の保護施設「Tailspin Shelter」のウェブアプリケーションです。フロントエンドとバックエンドが分離された構成になっています。### 技術スタック



- **フロントエンド (`client/`):** [Astro](https://astro.build/) と [Svelte](https://svelte.dev/) で構築されたウェブサイトです。犬のリスト表示、詳細表示、施設についての情報を提供します。- **フロントエンド (client/)**

- **バックエンド (`server/`):** [Flask](https://flask.palletsprojects.com/) (Python) で構築されたAPIサーバーです。犬と犬種に関するデータをSQLiteデータベースから提供します。  - **フレームワーク:** [Astro](https://astro.build/)

  - **UIコンポーネント:** [Svelte](https://svelte.dev/)

## 主要な技術スタック  - **言語:** TypeScript

  - **パッケージ管理:** npm

- **バックエンド:**  - **E2Eテスト:** [Playwright](https://playwright.dev/)

  - フレームワーク: Flask

  - データベース: SQLite- **バックエンド (server/)**

  - ORM: SQLAlchemy  - **フレームワーク:** [Flask](https://flask.palletsprojects.com/) (Python)

  - 主要ファイル: [`server/app.py`](server/app.py)  - **データベース:** SQLite

- **フロントエンド:**  - **ORM:** [SQLAlchemy](https://www.sqlalchemy.org/)

  - フレームワーク: Astro, Svelte  - **主な依存関係:** `flask`, `sqlalchemy`, `flask_sqlalchemy`, `flask-cors`

  - スタイリング: Tailwind CSS

  - 主要ファイル: [`client/src/pages/index.astro`](client/src/pages/index.astro), [`client/src/components/DogList.svelte`](client/src/components/DogList.svelte)### ディレクトリ構造の要点

- **テスト:**

  - バックエンド: `unittest` ([`server/test_app.py`](server/test_app.py))- `client/`: Astroで構築されたフロントエンドアプリケーションのソースコードが含まれています。

  - フロントエンド (E2E): Playwright ([`client/e2e-tests/`](client/e2e-tests/))  - `src/pages/`: 各ページのコンポーネント。

- **開発環境:**  - `src/components/`: 再利用可能なSvelteコンポーネント。

  - Dev Container ([`.devcontainer/devcontainer.json`](.devcontainer/devcontainer.json))- `server/`: Flaskで構築されたバックエンドAPIのソースコードが含まれています。

  - `app.py`: APIエンドポイントを定義するメインファイル。

## アーキテクチャのポイント  - `models/`: SQLAlchemyのデータベースモデル。

  - `dogshelter.db`: SQLiteデータベースファイル。

- **API通信:** フロントエンドは、Astroのミドルウェア ([`client/src/middleware.ts`](client/src/middleware.ts)) を使用して、`/api/*` へのリクエストをバックエンドのFlaskサーバー (デフォルト `http://localhost:5100`) に転送します。- `scripts/`: アプリケーションの起動などを補助するスクリプトが含まれています。

- **データベース:** データベースは [`server/dogshelter.db`](server/dogshelter.db) という単一のSQLiteファイルです。- `content/`: アプリケーションで使用される静的なコンテンツが含まれている可能性があります。

- **データモデル:**

  - `Dog`: [`server/models/dog.py`](server/models/dog.py) で定義されています。### 起動方法

  - `Breed`: [`server/models/breed.py`](server/models/breed.py) で定義されています。

- **初期データ:** [`server/utils/seed_database.py`](server/utils/seed_database.py) スクリプトが [`server/models/dogs.csv`](server/models/dogs.csv) と [`server/models/breeds.csv`](server/models/breeds.csv) からデータベースに初期データを投入します。リポジトリのルートディレクトリで以下のコマンドを実行することで、開発環境が起動します。



## 起動方法```bash

./scripts/start-app.sh

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
