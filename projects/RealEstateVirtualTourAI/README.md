# Real Estate Virtual Tour AI

Version: 1.0

Status: Draft

Purpose: Commercial SaaS design

---

## 1. 概要

Real Estate Virtual Tour AIは、不動産物件の室内写真を複数枚アップロードすると、AIが部屋種別・写真順序・空間的なつながりを推定し、室内を歩いているように見えるイメージ動画を生成する商用SaaSである。

利用者は、生成プロンプト、動画の長さ、画角、移動速度、雰囲気、BGM、字幕、ロゴ、ウォーターマークを調整できる。

本サービスは「実在物件の正確な3D計測」ではなく、掲載写真を基にした販促用イメージ動画を生成する。生成物にはAI生成であることを明示し、物件の実際の形状・寸法・設備を誤認させない設計を必須とする。

---

## 2. 想定顧客

- 不動産仲介会社
- 不動産管理会社
- デベロッパー
- ハウスメーカー
- 建築・リフォーム会社
- 不動産ポータル運営会社
- 物件撮影代行会社

---

## 3. コア機能

1. 室内写真の複数アップロード
2. AIによる部屋種別判定
3. 写真品質チェック
4. 写真順序・ストーリーボード自動生成
5. プロンプト編集
6. 動画尺調整
7. カメラ移動・雰囲気調整
8. 動画生成ジョブ管理
9. プレビュー・再生成
10. 承認・ダウンロード・共有
11. ロゴ・字幕・BGM・ウォーターマーク
12. 利用量・課金・組織管理

---

## 4. ディレクトリ

```text
projects/RealEstateVirtualTourAI/
├── README.md
├── ProductRequirements.md
├── SystemArchitecture.md
├── AIVideoPipeline.md
├── DataModel.md
├── API.md
├── UXFlow.md
├── SecurityCompliance.md
├── SaaSOperations.md
├── Roadmap.md
└── CLAUDE.md
```

---

## 5. MVP完成条件

- 3〜20枚の画像アップロード
- JPG / PNG / WebP対応
- 部屋種別の自動分類
- 15秒 / 30秒 / 60秒動画生成
- 自由プロンプトとプリセット
- 非同期ジョブ管理
- 生成結果のプレビュー
- MP4ダウンロード
- AI生成表記
- 組織・ユーザー・利用量管理
- 決済・プラン制御
- 監査ログ
- 削除・保持期間管理
