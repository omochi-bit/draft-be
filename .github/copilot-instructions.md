# copilot-instructions.md

## TODO Webアプリケーション（Spring Boot版） システム仕様草案

### 概要
本アプリケーションはSpring Bootを用いたバックエンドAPIにより、TODO管理ができるWebアプリケーションです。  
ユーザー登録、認証、タスク管理、編集、検索、状態管理など、基本的なTODO機能を備えます。

---

### 主な機能

1. **ユーザー管理**
   - ユーザー登録・ログイン・ログアウト
   - パスワード変更／リセット
   - 認証にはJWT（JSON Web Token）あるいはSpring Securityを利用

2. **TODOタスク管理**
   - タスクの新規登録（タイトル・説明・期限・重要度・ステータスなど）
   - タスク一覧表示（ログインユーザーごと）
   - タスク詳細表示
   - タスク編集・削除
   - タスク完了・未完了ステータス管理
   - タスク検索・フィルタリング（重要度順、期限順、完了状態 等）

3. **API設計**
   - RESTfulなエンドポイント提供（JSON返却）
   - 一部操作は認証必須
   - Swagger/OpenAPIによるAPIドキュメント自動生成

4. **例外・エラーハンドリング**
   - 共通的なAPIエラー応答（標準化されたレスポンス形式）
   - バリデーションエラー対応

5. **セキュリティ＆認証**
   - Spring Securityによる認証・認可制御
   - パスワードはハッシュ化保存
   - CORS対応（外部フロントエンドとの分離を考慮）

6. **テスト**
   - ユニットテスト（JUnit・Mockitoなど）
   - 統合テスト

---

### データモデル（例）

```
User
- id: Long
- username: String
- password: String (hashed)
- email: String
- createdAt: DateTime

Todo
- id: Long
- title: String
- description: String
- dueDate: DateTime
- priority: int
- status: enum (TODO, IN_PROGRESS, DONE)
- owner: User (外部キー)
```

---

### 技術要素・構成

- 開発：Spring Boot（Java）、Spring Security、JPA/Hibernate
- テスト：JUnit、Mockito
- DB：H2/SQLite/PostgreSQLなど選択可
- API設計：REST/JSON、Swagger(OpenAPI)
- ドキュメント：README、API仕様書

---

### 今後の拡張例（参考）

- タスクにタグ／コメント機能追加
- タスクの通知機能
- 他のユーザーとの共有・コラボ
- フロントエンド（React等）との連携

---

#### 目的に合わせて内容調整・拡張してください。
