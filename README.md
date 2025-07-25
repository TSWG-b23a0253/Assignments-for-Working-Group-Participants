# アプリケーション要件

本ドキュメントは、アプリケーションの要件について記述しています。</br>
「日本時間の表示機能」と「TODOアプリとそれのユーザー管理機能」を含みます。

</br></br>

## 1. システム構成

本アプリケーションは以下のマイクロサービスで構成されます。

- **フロントエンドサーバー** </br>
※フロントエンドサーバーはJavaScriptかTypeScriptどちらかになります。
  - ユーザーインターフェースを提供
  - バックエンドおよびAPIサーバーと通信してデータを取得・表示

- **バックエンドサーバー** </br>
※バックエンドサーバーはどの言語を用いてくれても問題ありません。こだわりなければJavaでいいと思います。
  - フロントエンドからのリクエストを受け取り、必要に応じてAPIサーバーへ中継
  - 日本時間の取得やTODO機能の一部処理を担当

- **APIサーバー** </br>
※APIサーバーもどの言語を用いてくれても問題ありません。構成に必要なファイルが少ないフレームワークだと楽です(Javaは不向き)。
  - データベースとのやり取りを担当
  - 日本時間取得APIおよびTODO関連のCRUD処理を非同期で実行

- **DBサーバー** </br>
※DBサーバーはRDBでもNoSQLを使用しても問題ありません。
  - MySQLなどのリレーショナルデータベースを提供
  - ユーザー情報、TODOメモなどの永続データを管理

</br></br>

## 2. メイン画面

※ここでの目的としては、ルーティング機能について学んでもらおうと思います。</br>

以降の機能を考慮して、リンクを3つほど用意し、それぞれアクセスするごとに別のHTMLなどが表示されるような機能を作成してください。

</br></br>

## 3. 日本時間の表示

※ここでの目的としては、各言語間での連携方法を学ぶために簡易的に作ってもらう感じです。

- バックエンドサーバーから取得した日本標準時（JST）をフロントエンドに表示。
- APIサーバーから取得した日本標準時（JST）をフロントエンドに表示。

</br></br>

## 4. TODOアプリ機能

※レベル1が完了したら、レベル2に進んでください。

### レベル1 新規の機能

- **ユーザー認証**
  - ログイン機能
  - ユーザー登録機能
  - ログインユーザーのパスワード変更機能

### レベル2 新規の機能

- **TODO管理**
  - ログインユーザーのTODOメモ一覧表示
  - TODOメモの特定文字列検索
  - TODOメモの追加、更新、削除機能

### レベル3 機能の追加

- TODOリストのCSV出力機能
- CSVファイルからのTODOメモ登録機能
- 管理者向けユーザー管理画面

### レベル4 機能の追加

- ログイン機能に2要素認証機能を搭載
- パスワード変更機能に2要素認証機能を搭載
- ユーザーセッション管理機能（多端末ログイン管理、セッションタイムアウト）

</br></br>

## 5. 技術的要件

- 各マイクロサービスは独立して開発・デプロイ可能とし、API通信はHTTP/RESTやgRPCを利用する。
- DockerやDocker Composeなどのコンテナ技術で各サービスを管理。
- DBサーバーにはDockerボリュームをマウントし、永続化を実現する（例：volumes: - db_data:/var/lib/mysql）。
- サービス間通信は内部ネットワークを利用し、外部に不要なサービスは公開しない。
- 各機能はメイン画面からの遷移によるアクセスのみ許可し、直接URL入力によるアクセスは制限する
  - 特定の機能を実装したURLに直接アクセスした場合、メイン画面にリダイレクトするようにする。
- 時刻管理はすべて日本標準時（Asia/Tokyo）に統一。
- データベースはAPIサーバーが直接アクセスし、他サービスはAPI経由でデータ操作を行う。

</br></br>

## 6. その他

- セキュリティ対策として、認証・認可機能はバックエンドで適切に実装。
- 各サービスはログ管理を行い、運用監視しやすくすること。
- フロントエンドはユーザビリティを重視し、レスポンシブ対応を推奨。

</br></br>

## 7. 成果物

各フェーズごと、ひな型をchatgptさんに作成してもらって構いません。

### 7-1. 要件定義フェーズ

| 成果物          | 内容                                  |
| ------------ | ----------------------------------- |
| **要件定義書**    | システムの機能要件、非機能要件、業務フロー、利用シナリオをまとめた文書 |
| **業務フロー図**   | 現行業務および新業務の流れを図示                    |
| **機能一覧表**    | 提供する機能を一覧化（優先度、概要含む）                |
| **画面要件定義書**  | 各画面で必要な項目やUI要件を整理                   |
| **非機能要件定義書** | パフォーマンス、セキュリティ、可用性など                |

</br>

### 7-2. 基本設計フェーズ

| 成果物          | 内容                                  |
| ------------ | ----------------------------------- |
| **要件定義書**    | システムの機能要件、非機能要件、業務フロー、利用シナリオをまとめた文書 |
| **業務フロー図**   | 現行業務および新業務の流れを図示                    |
| **機能一覧表**    | 提供する機能を一覧化（優先度、概要含む）                |
| **画面要件定義書**  | 各画面で必要な項目やUI要件を整理                   |
| **非機能要件定義書** | パフォーマンス、セキュリティ、可用性など                |

</br>

### 7-3. 基本設計フェーズ

| 成果物              | 内容                      |
| ---------------- | ----------------------- |
| **基本設計書（外部設計）**  | 画面設計、API仕様、データフロー、入出力仕様 |
| **画面設計書（UI設計書）** | 画面レイアウト、操作フロー、ワイヤーフレーム  |
| **データベース基本設計書**  | エンティティ一覧、テーブル設計、ER図     |
| **外部I/F設計書**     | 外部システムやAPIとの連携仕様        |

</br>

### 7-4. 詳細設計フェーズ

| 成果物              | 内容                           |
| ---------------- | ---------------------------- |
| **詳細設計書（内部設計書）** | モジュール構造、クラス図、処理ロジック、パラメータ仕様  |
| **プログラム設計書**     | 各機能のアルゴリズム、入力／出力仕様、エラーハンドリング |

</br>

### 7-5. 実装フェーズ

| 成果物            | 内容            |
| -------------- | ------------- |
| **ソースコード**     | 実装したコード       |
| **単体テスト仕様書** | モジュール単位のテスト仕様 |
| **単体テスト結果報告書** | 実施結果          |

</br></br>

## 8. フォルダ構成例

```
📂 my-project/
 ├── README.md  # プロジェクト概要
 ├── docs/
 │    ├── basic-design.md   # 基本設計書
 │    ├── detail-design.md  # 詳細設計書
 │    ├── db-design.md      # DB設計書
 │    ├── api-spec.md       # API仕様
 │    └── architecture.md   # システム構成図
```
