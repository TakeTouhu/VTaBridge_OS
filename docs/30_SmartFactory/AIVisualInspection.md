# AI Visual Inspection 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

AI Visual Inspectionは、カメラ・照明・画像処理・AIモデルを統合し、外観検査の自動化と品質判定の標準化を実現する。

# 2. 対象

- 傷
- 欠け
- 汚れ
- 寸法異常
- 組付け不良
- 印字・ラベル不良

# 3. 処理フロー

```text
Image Capture → Preprocessing → AI Inference → Rule Evaluation → Result Storage → Feedback
```

# 4. 機能

- 画像収集
- Edge推論
- 判定結果管理
- モデル更新
- 誤判定レビュー
- 品質システム連携

# 5. KPI

- 検出率
- 過検出率
- 見逃し率
- 判定時間
- 自動検査率
- モデル劣化率

# 6. ガバナンス

モデル、学習データ、閾値、変更履歴、承認記録を一元管理する。
