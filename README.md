# oss-data-platform-document
- OSSで構築するデータ基盤

![Image](images/AdobeStock_144803025.png)

## 概要
- データ基盤を導入したいがコストを掛けられない状況で、OSSのみを駆使して基盤を構築していくケースを想定した仮想プロジェクト。

## Getting Started

### リソースの取得とコンテナ実行

```bash
# プロジェクトディレクトリの作成
mkdir oss-data-platform
cd $_

# リソースの取得
git clone https://github.com/LowSE01/oss-data-platform-airflow.git
git clone https://github.com/LowSE01/oss-data-platform-dbt-datamart.git
git clone https://github.com/LowSE01/oss-data-platform-dbt-datawarehouse.git
git clone https://github.com/LowSE01/oss-data-platform-docker.git
git clone https://github.com/LowSE01/oss-data-platform-embulk.git

# ビルド
cd oss-data-platform-docker
docker compose build --no-cache

# コンテナ起動
docker compose up -d

# 全てのコンテナのSTATUSがhealthyになるまで暫し待つ。
docker ps --format 'table {{.Names}}\t{{.Status}}'
```

#### trouble shoot
- docker compose up -d実行時に下記のエラーが表示される場合は、Docker DesktopのFileSharing権限を確認してください。

```
Error response from daemon: invalid mount config for type "bind": bind source path does not exist
```

### 各コンテナイメージのサービス
- 下記の各種サービスが立ち上がる。

#### MySQL：基幹システム、各種業務システムなど、データの源泉となるシステム群に相当
- host: localhost
- port: 3306
- username: mysql
- password: mysql

#### PostgreSQL：データ基盤本体
- host: localhost
- port: 5432
- username: postgres
- password: postgres

#### [Apache Airflow](http://localhost:8080/)：ジョブフロー管理
- username: admin
- password: admin

#### dbt Docs：dbtプロジェクトドキュメント
* [for datawarehouse](http://localhost:8081/)
* [for datamart](http://localhost:8082/)
