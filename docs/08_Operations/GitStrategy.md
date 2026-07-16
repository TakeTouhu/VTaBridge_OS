# Git Strategy

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Git Strategyは、VTaBridge OSにおけるソースコード管理・ブランチ運用・Pull Request・レビュー・リリースフローを定義する。

GitHubを標準リポジトリとして採用し、品質・保守性・開発効率を高める運用を実施する。

---

# 2. 目的

Git Strategy導入目的

- 品質向上
- 変更履歴管理
- チーム開発
- リリース管理
- コードレビュー
- CI/CD連携
- コンフリクト削減
- 保守性向上

---

# 3. 採用方式

GitHub Flowをベースとする。

長期間のブランチ保持は避け、小さな単位で頻繁にマージする。

---

# 4. ブランチ構成

```
main

develop

feature/*

fix/*

hotfix/*

release/*
```

---

# 5. ブランチ用途

| Branch | 用途 |
|---------|------|
| main | 本番環境 |
| develop | 開発統合 |
| feature | 新機能 |
| fix | 不具合修正 |
| hotfix | 緊急修正 |
| release | リリース準備 |

---

# 6. ブランチ命名規則

例

```
feature/customer-api

feature/engineer-ui

feature/ai-chat

fix/login-error

hotfix/payment-bug

release/v1.0.0
```

小文字・ケバブケースを採用する。

---

# 7. コミットメッセージ

Conventional Commitsを採用する。

例

```
feat: add customer api

fix: resolve login issue

docs: update architecture

refactor: optimize workflow

test: add unit tests

chore: update dependencies
```

---

# 8. Pull Request

Pull Requestは必須とする。

PRには以下を記載する。

- 概要
- 変更内容
- 影響範囲
- テスト結果
- スクリーンショット（UI変更時）
- 関連Issue

---

# 9. レビュー

レビュー条件

- 2名以上承認
- CI成功
- コンフリクトなし
- CodeQL成功
- テスト成功

承認後にマージする。

---

# 10. マージ戦略

採用

```
Squash Merge
```

履歴をシンプルに保つ。

---

# 11. タグ

Semantic Versioningを採用する。

例

```
v1.0.0

v1.1.0

v1.2.0

v2.0.0
```

---

# 12. Release

Release Branchを利用する。

フロー

```
develop

↓

release

↓

main

↓

Tag

↓

Deploy
```

---

# 13. Issue管理

GitHub Issuesを利用する。

種類

- Feature
- Bug
- Task
- Epic
- Documentation

---

# 14. GitHub Projects

利用

- Sprint
- Kanban
- Backlog
- Release管理

プロジェクト進捗を可視化する。

---

# 15. コード品質

必須チェック

- ESLint
- Ruff
- Type Check
- Unit Test
- Build
- Security Scan

CI成功後のみマージ可能とする。

---

# 16. セキュリティ

実装

- Branch Protection
- Signed Commit（推奨）
- Secret Scan
- Dependabot
- CodeQL

mainブランチへの直接Pushは禁止する。

---

# 17. バージョン管理

対象

- Frontend
- Backend
- API
- Database
- Infrastructure

すべてGitで管理する。

---

# 18. ドキュメント管理

管理対象

- 設計書
- API仕様
- DB設計
- README
- ADR

ソースコードと同一リポジトリで管理する。

---

# 19. 運用ルール

実施内容

- 小さなPRを推奨
- 長期間のFeature Branchは禁止
- レビューコメントへ対応
- マージ後はBranch削除
- 定期的にdevelopを同期

---

# 20. 将来拡張

- GitHub Copilot Code Review
- AI Commit Message生成
- AI Pull Requestレビュー
- AI Conflict Resolution
- Release Note自動生成
- Conventional Commit自動チェック
- GitHub Merge Queue
- CODEOWNERS自動管理
- Policy as Code
- AI開発分析
