# 🎓 CLaaS — Campus Life as a Service

> 大学生活のすべてを、一つのアプリで。

---

## CLaaSとは？

**CLaaS（Campus Life as a Service）** は、大学生の「困った」を解決し、「もったいない」をなくすプラットフォームです。

### 解決する課題

| 課題 | CLaaSの解決策 |
|---|---|
| 履修選択が難しい・情報がない | 楽単情報・過去問の共有 + AIシラバス解析 |
| 時間割作りが面倒 | AIが最適な時間割を自動生成 |
| 空きコマの時間を持て余す | 空きコマに合わせたコンテンツ提案・マッチング |
| 使い終わった教科書が捨てられない | 教材マーケットプレイス |
| 情報共有への動機がない | ガクチカクレジットエコノミー |

---

## ドキュメント構成

審査員の方は以下の順番でお読みください。

### 📋 Step 1: アプリの概要を理解する
**→ [要件分析](aidlc-docs/inception/requirements/requirements-analysis.md)**

CLaaSが解決する課題、ターゲットユーザー、主要機能の概要をまとめています。

### 👤 Step 2: ユーザー視点で機能を理解する
**→ [ユーザーストーリー](aidlc-docs/inception/user-stories/user-stories.md)**

大学生・企業・管理者それぞれの視点から、CLaaSがどう使われるかを具体的なシナリオで説明しています。

### 📐 Step 3: 詳細な要件を確認する
**→ [要件定義書](aidlc-docs/inception/requirements/requirements.md)**

17の要件と受け入れ基準を定義しています。

### 🏗️ Step 4: 技術設計を確認する
**→ [アプリケーション設計](aidlc-docs/inception/application-design/design.md)**

システムアーキテクチャ、17のマイクロサービス、ER図、39の正確性プロパティを定義しています。

### 📦 Step 5: 実装計画を確認する
**→ [Unit of Work 計画](aidlc-docs/inception/units/unit-of-work.md)**

実装を段階的に進めるための作業単位の計画です。

### 📊 Step 6: プロジェクト状態を確認する
**→ [AI-DLC State](aidlc-docs/aidlc-state.md)**

AI-DLCワークフローの進捗状態です。

---

## 主要機能サマリー

```
CLaaS
├── 🎯 コア機能
│   ├── 楽単情報・過去問・ノートの共有
│   ├── AIシラバス解析（難易度スコア1-10）
│   └── AI自動時間割生成（3パターン以上）
│
├── 💰 ガクチカクレジットエコノミー
│   ├── 投稿・出席・代返でクレジット獲得
│   ├── 企業クーポン使用でクレジット獲得
│   └── 空きコマ情報提供でクレジット獲得
│
├── 🤝 コミュニティ機能
│   ├── 空きコママッチング
│   ├── リアルタイムチャット
│   └── 趣味コミュニティ（スポーツ・ゲーム等）
│
├── 🏪 マーケットプレイス
│   └── 教材の譲渡・売買（無料/クレジット/現金）
│
└── 🏢 企業向け機能
    ├── クーポン発行・管理
    └── 空きコマ統計データ（匿名化・集計）
```

---

## 技術スタック

| レイヤー | 技術 |
|---|---|
| フロントエンド | React Native (Expo) |
| バックエンド | Node.js + Express (TypeScript) |
| データベース | PostgreSQL + Redis |
| AI | OpenAI GPT-4o |
| ストレージ | AWS S3 |
| 通知 | Firebase Cloud Messaging |
| リアルタイム | Socket.io |
| 地図 | Google Maps API |
| 決済 | Stripe |

---

## AI-DLC 開発プロセス

本プロジェクトは **AWS AI-DLC（AI-assisted Development Lifecycle）** を使用して開発しています。

- ✅ **Inception フェーズ完了** — 要件分析・ユーザーストーリー・アプリケーション設計・Unit of Work計画
- ⬜ Construction フェーズ（実装）
- ⬜ Operations フェーズ（デプロイ・運用）
