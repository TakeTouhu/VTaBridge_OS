# Command and Control 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Command and Controlは、クラウドまたは業務システムからIoTデバイスへ安全に指示を送信し、実行結果を追跡する仕組みを定義する。

# 2. 対象コマンド

- Start / Stop
- Configuration Change
- Firmware Update
- Reset
- Diagnostic Request
- Set Point Change

# 3. フロー

```text
Operator → Approval → Command Queue → Device → Acknowledgement → Audit
```

# 4. 制御要件

- コマンド承認
- 対象検証
- 有効期限
- 冪等性
- 再送制御
- 実行結果確認

# 5. セキュリティ

- RBAC
- MFA
- 署名付きコマンド
- 最小権限
- 完全監査

# 6. KPI

- 実行成功率
- 応答時間
- 再送率
- 期限切れ件数
- 不正コマンド検知数
