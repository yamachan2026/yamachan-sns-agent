# やまちゃん株式会社 ワークスペースマップ

## このファイルの役割
全エージェントがここを最初に読むことで、どこに何があるかを即座に把握できる。

## 社長室（グローバル設定）
~/.claude/
├── CLAUDE.md            # グローバル指示書（最重要・常に参照）
├── about-me.md          # やまちゃんのプロフィール
├── brand-voice.md       # 発信スタイル・トーン定義
├── business-context.md  # 事業全体像
└── workspace-map.md     # このファイル（全体の地図）

## スキル一覧
~/.claude/skills/
├── sns/                 # SNS運用スキル
├── drm/                 # 採用DRM構築スキル
├── heartland/           # ハートランドDGP営業スキル
├── paters/              # Paters恋愛コンサルスキル
└── youtube/             # YouTube運用スキル

## エージェント一覧
~/.claude/agents/
├── sns-goal-agent.md        # SNSゴール設計・尋問エージェント
├── content-agent.md         # コンテンツ制作エージェント
├── quality-gate-agent.md    # 品質チェックエージェント（3回）
├── pdca-agent.md            # 週次PDCA・分析エージェント
├── advisory-board.md        # 諮問委員会エージェント
└── research-agent.md        # リサーチ・バズ収集エージェント

## クライアント案件
~/projects/
├── yamachan-sns/        # やまちゃん自身のSNS運用
│   ├── persona.md       # 人格設定
│   └── sns-strategy.md  # SNS戦略・KPI
├── kuroiwa/             # 黒岩さん（黒ちゃん）X運用
│   ├── persona.md
│   └── sns-strategy.md
├── senoo/               # 妹尾さん YouTube・LINE運用
│   ├── persona.md
│   └── sns-strategy.md
├── heartland/           # ハートランドDGP
└── paters/              # Paters恋愛コンサル

## コマンド一覧
~/.claude/commands/
├── new-client.md        # 新規クライアント追加
├── weekly-report.md     # 週次レポート生成
└── buzz-hunt.md         # バズ投稿収集

## 作業フローの基本
1. CLAUDE.mdを読む
2. workspace-map.mdで作業場所を確認
3. 該当するクライアントのpersona.mdを読む
4. 該当するスキルを使って作業
5. 品質ゲートを通過させてから出力

## スケジュール実行タスク（/schedule）
- 毎朝6時：バズ収集・トレンド分析
- 毎朝7時：各クライアントの投稿下書き生成
- 毎週月曜：週次PDCA・分析・改善レポート

## Google スプレッドシート連携
スプレッドシートURL：https://docs.google.com/spreadsheets/d/1FJjpypv7mlq5bDbHGVHReXsnFO1posBklvqGbM9dhg0/edit

### シート構成
- 投稿候補一覧：投稿候補の確認・管理
- バズ投稿・リサーチ結果：毎日のリサーチ結果を蓄積
- KPI・数値管理：週次の数値をトラッキング
- 週次PDCAレポート：毎週月曜の分析結果を記録

### 書き込みルール
- 投稿候補が生成されたら必ず「投稿候補一覧」シートに追記する
- リサーチ結果のバズ投稿TOP3は「バズ投稿・リサーチ結果」シートに追記する
- 週次PDCAの結果は「週次PDCAレポート」と「KPI・数値管理」シートに追記する
- Google Driveコネクタを使って直接書き込む
