# Unit Test 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Unit Testは、VTaBridge OSを構成する各コンポーネント・クラス・関数・APIロジックを最小単位で検証するためのテスト設計を定義する。

単体テストを品質保証の基盤と位置付け、変更時のリグレッション防止と安全なリファクタリングを実現する。

---

# 2. 目的

Unit Test導入目的

- 品質向上
- バグの早期検出
- リファクタリング支援
- リグレッション防止
- CI高速化
- 保守性向上

---

# 3. 対象

Frontend

- React Components
- Hooks
- Utility Functions
- Validation

Backend

- Service
- Domain
- Repository(Mock)
- Utility

AI

- Prompt Builder
- Parser
- Token Calculator

---

# 4. 利用ツール

Frontend

- Vitest
- React Testing Library

Backend

- Pytest
- pytest-mock

Coverage

- Vitest Coverage
- Coverage.py

---

# 5. ディレクトリ構成

```
src/

├── components/
│   └── CustomerCard.tsx
│
├── hooks/
│   └── useCustomer.ts
│
└── tests/
    ├── unit/
    ├── fixtures/
    ├── mocks/
    └── helpers/
```

テストコードは実装コードと対応関係が分かる構成とする。

---

# 6. 命名規則

ファイル名

```
CustomerCard.test.tsx

useCustomer.test.ts

customer_service_test.py
```

テストケース

```
should render customer name

should return engineer list

should throw validation error
```

振る舞いを明確に記述する。

---

# 7. テスト対象

確認項目

- 正常系
- 異常系
- 境界値
- Null
- Empty
- Validation
- Exception

主要な分岐を網羅する。

---

# 8. モック

利用対象

- API
- Database
- Azure SDK
- OpenAI SDK
- Blob Storage

外部依存はMock化する。

---

# 9. Test Double

利用

- Mock
- Stub
- Spy
- Fake

目的に応じて使い分ける。

---

# 10. React Component

確認項目

- Rendering
- Props
- Event
- State
- Accessibility

UI表示だけでなく操作も検証する。

---

# 11. Hooks

確認項目

- State変更
- API呼び出し
- Error
- Retry
- Cache

React Hooks Testing Library相当の手法で検証する。

---

# 12. Backend

確認項目

- Service
- Validation
- Business Logic
- Exception
- Mapping

RepositoryはMock化する。

---

# 13. AI機能

確認項目

- Prompt生成
- Token計算
- Response Parser
- Function Calling Parser

AI API自体はMockで代替する。

---

# 14. テストデータ

利用

- Fixture
- Factory
- Faker

テストデータをコードへハードコードしない。

---

# 15. カバレッジ

目標

Frontend

```
80%以上
```

Backend

```
90%以上
```

Critical Module

```
95%以上
```

---

# 16. CI/CD連携

GitHub Actionsで実施

- Unit Test
- Coverage
- Report生成

失敗時はPipelineを停止する。

---

# 17. レポート

出力内容

- Success
- Failed
- Coverage
- Duration

HTMLレポートを生成する。

---

# 18. ベストプラクティス

- 1テスト1目的
- Arrange-Act-Assert（AAA）を採用
- テスト間で状態を共有しない
- 外部サービスへ接続しない
- 実行順序へ依存しない

高速・独立・再現可能なテストを目指す。

---

# 19. パフォーマンス

目標

Unit Test全体

```
5分以内
```

個別テスト

```
100ms以内
```

高速実行を維持する。

---

# 20. 将来拡張

- AIテストケース生成
- Mutation Testing
- Snapshot Test最適化
- Property-Based Testing
- Golden Master Test
- Test Impact Analysis
- AI失敗原因分析
- 自動Mock生成
- Visual Snapshot Test
- 品質スコア可視化
