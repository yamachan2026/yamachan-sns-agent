# 自動実行マスターワークフロー
# /scheduleで案件別・SNS別に自動実行される

## 役割
各案件のリサーチから投稿候補の作成まで全自動で実行する。
やまちゃんが朝起きたときには「確認して投稿ボタンを押すだけ」の状態を作る。

## 自動実行スケジュール

| 実行時間 | 案件 | SNS | 実行内容 |
|---------|------|-----|---------|
| 毎日 朝6時 | Paters | X・Threads | リサーチ→コンテンツ生成→品質チェック |
| 毎日 朝7時 | 黒岩さん | X・X記事 | リサーチ→コンテンツ生成→品質チェック |
| 月水金 朝6時 | やまちゃん | X・スレッズ | リサーチ→コンテンツ生成→品質チェック |
| 毎週水曜 朝6時 | やまちゃん | note | リサーチ→コンテンツ生成→品質チェック |
| 毎週土曜 朝6時 | やまちゃん | YouTube | リサーチ→コンテンツ生成→品質チェック |
| 毎週月曜 朝6時 | 妹尾さん | YouTube | リサーチ→コンテンツ生成→品質チェック |
| 毎週木曜 朝6時 | Paters | note | リサーチ→コンテンツ生成→品質チェック |
| 毎週月曜 朝8時 | 全案件 | 全SNS | 週次PDCA・分析・改善 |

## 各案件の自動実行フロー

### Paters 毎日自動実行（朝6時）

Step 1：research-patersを実行
- X・Threads用バズ投稿収集
- 競合確認・コンテンツアイデア生成
- 結果を~/projects/paters/daily-brief.mdに保存

Step 2：content-agentを呼び出し
- daily-brief.mdを読み込む
- ~/projects/paters/persona.mdを読み込む
- ~/projects/paters/sns-strategy.mdを読み込む
- 今日のX投稿3案・Threads投稿2案を生成

Step 3：quality-gate-agentを通す（スピード重視モード）
- フック審査→本文審査→CTA・リスク審査
- 全項目8/10以上になるまで修正
- Paters特有のリスクチェック（禁止ワード・安全表現の確認）

Step 4：投稿候補を保存
- ~/projects/paters/output/[日付]-x-[連番].mdに保存
- ~/projects/paters/output/[日付]-threads-[連番].mdに保存

Step 5：前日との比較サマリーを生成
- 前日のdaily-brief.mdと比較
- トレンドの変化・新しい競合の動きを記録

### 黒岩さん 毎日自動実行（朝7時）

Step 1：research-kuroiwaを実行
- X通常投稿・X記事用バズ投稿収集
- 競合確認・コンテンツアイデア生成
- 結果を~/projects/kuroiwa/daily-brief.mdに保存

Step 2：content-agentを呼び出し
- daily-brief.mdを読み込む
- ~/projects/kuroiwa/persona.mdを読み込む（一人称：黒ちゃん）
- ~/projects/kuroiwa/sns-strategy.mdを読み込む
- 今日のX通常投稿3案・X記事アイデア2案を生成

Step 3：quality-gate-agentを通す（スピード重視モード）
- フック審査→本文審査→CTA・リスク審査
- 黒岩さん特有のリスクチェック
  - 一人称が「黒ちゃん」になっているか
  - プラットフォーム規約に準拠した表現か
  - 過激な表現・直接的すぎる性的表現はないか

Step 4：投稿候補を保存
- ~/projects/kuroiwa/output/[日付]-x-[連番].mdに保存

Step 5：前日との比較サマリーを生成

### やまちゃん X・スレッズ 週3回自動実行（月水金 朝6時）

Step 1：research-yamachanを実行（X・スレッズモード）
- バズ投稿収集・トレンド分析
- 競合確認・コンテンツアイデア生成
- 引用RT候補3件を選定
- 結果を~/projects/yamachan-sns/daily-brief.mdに保存

Step 2：content-agentを呼び出し
- daily-brief.mdを読み込む
- ~/projects/yamachan-sns/persona.mdを読み込む
- ~/projects/yamachan-sns/sns-strategy.mdを読み込む
- 今日のX投稿3案・スレッズ投稿2案を生成

Step 3：quality-gate-agentを通す（スピード重視モード）
- フック審査→本文審査→CTA・リスク審査
- ブランドボイスとの整合性確認

Step 4：投稿候補を保存
- ~/projects/yamachan-sns/output/[日付]-x-[連番].mdに保存
- ~/projects/yamachan-sns/output/[日付]-threads-[連番].mdに保存

Step 5：引用RT候補を保存
- ~/projects/yamachan-sns/output/[日付]-quote-rt.mdに保存

### やまちゃん note 毎週水曜自動実行（朝6時）

Step 1：research-yamachanを実行（noteモード）
- SEOキーワード調査
- 競合note確認
- 記事アイデア生成

Step 2：content-agentを呼び出し
- note記事の骨格を生成
- SEOキーワードをタイトル・見出しに配置
- LINE誘導CTAを設計

Step 3：quality-gate-agentを通す（品質重視モード）
- noteは週1本なので品質重視モードで徹底的に磨く

Step 4：投稿候補を保存
- ~/projects/yamachan-sns/output/[日付]-note.mdに保存

### やまちゃん YouTube 毎週土曜自動実行（朝6時）

Step 1：research-yamachanを実行（YouTubeモード）
- YouTubeトレンド収集
- 競合チャンネル確認
- 動画テーマアイデア生成

Step 2：content-agentを呼び出し
- 動画台本の骨格を生成
- タイトル・サムネ指示を生成
- 画像生成プロンプトを出力

Step 3：quality-gate-agentを通す（品質重視モード）
- YouTubeは重要コンテンツなので品質重視モード

Step 4：投稿候補を保存
- ~/projects/yamachan-sns/output/[日付]-youtube.mdに保存

### 妹尾さん YouTube 毎週月曜自動実行（朝6時）

Step 1：research-senooを実行
- YouTubeトレンド収集
- 競合チャンネル確認
- 動画テーマアイデア生成

Step 2：content-agentを呼び出し
- ~/projects/senoo/persona.mdを読み込む（かなこ先生の設定）
- 動画台本の骨格を生成
- アスタリスク使用禁止・セリフのみで出力
- LINE登録CTAを設計

Step 3：quality-gate-agentを通す（品質重視モード）
- かなこ先生特有のチェック
  - アスタリスク（星マーク）が使われていないか
  - ト書きが含まれていないか
  - 脳科学・心理学の根拠が入っているか
  - ターゲット（40〜60代ハイステイタス男性）に刺さるか

Step 4：投稿候補を保存
- ~/projects/senoo/output/[日付]-youtube.mdに保存

### Paters note 毎週木曜自動実行（朝6時）

Step 1：research-patersを実行（noteモード）
- SEOキーワード調査
- 競合note確認
- 記事アイデア生成

Step 2：content-agentを呼び出し
- 無料記事のみ・有料記事禁止
- SEOキーワードをタイトル・見出しに配置
- 安全な表現フレーミングを使う
- LINE誘導CTAを設計

Step 3：quality-gate-agentを通す（品質重視モード）
- Paters特有のリスクチェックを徹底

Step 4：投稿候補を保存
- ~/projects/paters/output/[日付]-note.mdに保存

### 週次PDCA 毎週月曜自動実行（朝8時）

Step 1：pdca-agentを全案件分実行
- 各案件のデータを収集・分析
- KPI達成率・SNS→LINE転換率を確認
- バズった投稿・伸びなかった投稿を分析

Step 2：成功パターンを蓄積
- ~/projects/[クライアント名]/success-patterns/[日付].mdに保存
- quality-gate-agentが参照できるように整理

Step 3：来週の戦略を更新
- 各案件のsns-strategy.mdに改善内容を追記
- 来週月曜の最初の投稿を1本生成

Step 4：週次レポートを保存
- ~/projects/[クライアント名]/weekly-report/[日付].mdに保存

## 出力物の管理

### フォルダ構造
~/projects/[クライアント名]/
├── persona.md              # 人格設定
├── sns-strategy.md         # SNS戦略・KPI
├── daily-brief.md          # 今日のブリーフィング（毎日上書き）
├── weekly-brief.md         # 今週のブリーフィング（妹尾さんのみ）
├── output/                 # 投稿候補
│   ├── [日付]-x-01.md
│   ├── [日付]-x-02.md
│   ├── [日付]-threads-01.md
│   ├── [日付]-note.md
│   ├── [日付]-youtube.md
│   └── [日付]-quote-rt.md
├── success-patterns/       # 成功パターンDB
│   └── [日付].md
└── weekly-report/          # 週次レポート
    └── [日付].md

## Google スプレッドシート書き込みルール

スプレッドシートURL：
https://docs.google.com/spreadsheets/d/1FJjpypv7mlq5bDbHGVHReXsnFO1posBklvqGbM9dhg0/edit

### 投稿候補一覧への書き込み（毎回の投稿生成後）
Google Driveコネクタを使って「投稿候補一覧」シートに以下を追記する：
- 日付：実行日
- 案件：クライアント名
- SNS：対象プラットフォーム
- ステータス：確認待ち
- フック：採用したフック
- 本文：生成した本文
- CTA：CTAの文言
- 品質スコア：quality-gate-agentの合計スコア
- 投稿済み：×（初期値）

### バズ投稿・リサーチ結果への書き込み（毎回のリサーチ後）
Google Driveコネクタを使って「バズ投稿・リサーチ結果」シートに以下を追記する：
- 日付：実行日
- 案件：クライアント名
- SNS：収集元プラットフォーム
- 投稿内容：バズった投稿の内容（TOP3）
- いいね数：いいね数
- RT数：RT数
- バズった理由：分析結果
- 転用アイデア：やまちゃんへの転用案

### KPI・数値管理への書き込み（週次PDCA後）
Google Driveコネクタを使って「KPI・数値管理」シートに以下を追記する：
- 週：対象週（例：2026/03/23〜03/29）
- 案件：クライアント名
- SNS：対象プラットフォーム
- KPI名：測定したKPI
- 目標：設定した目標値
- 実績：実際の数値
- 達成率：達成率（%）
- LINE転換率：SNS→LINE登録の転換率
- フォロワー増減：前週比のフォロワー増減数

### 週次PDCAレポートへの書き込み（週次PDCA後）
Google Driveコネクタを使って「週次PDCAレポート」シートに以下を追記する：
- 週：対象週
- 案件：クライアント名
- 一言サマリー：先週の総括（3行以内）
- バズTOP3：バズった投稿TOP3の内容と数字
- 改善アクション：優先度A・B・Cの改善アクション
- 来週方針：来週のコンテンツ方針

## やまちゃんの朝のルーティン

朝起きたらやること（5分以内で完了）：

1. 各案件のoutput/フォルダを確認
2. 投稿候補を読んで「OK」か「修正」かを判断
3. OKなら投稿ボタンを押す
4. 修正が必要なら「/create-post [クライアント名] [SNS名]」で手動修正

やまちゃんがやるのはこれだけ。
リサーチ・企画・制作・品質チェックは全部AIが自動でやる。
