# oss-data-platform-document
- OSSで構築するデータ基盤

![Image](images/AdobeStock_144803025.png)

## 概要
- データ基盤を導入したいがコストを掛けられない状況で、OSSのみを駆使して基盤を構築していくケースを想定した仮想プロジェクト。

## Getting Started

```bash
# プロジェクトディレクトリの作成
mkdir oss-data-platform
cd $_

# リソースの取得
git clone https://github.com/LowSE01/oss-data-platform-airflow.git
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
