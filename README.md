# 新規事業構想エージェント環境

Claude Codeで開いてチャットするだけで、8つの専門エージェントが協調して新規事業の構想を練る環境です。

## セットアップ

### 1. リポジトリをclone

```bash
git clone git@github.com:Archines/new_product_agent.git
cd new_product_agent
```

### 2. Python依存パッケージのインストール

```bash
pip install -r requirements.txt
```

### 3. Claude Codeで開く

```bash
claude
```

### 4. 自社情報の設定（任意）

`company_profile/` 配下のファイルに自社の情報を記入します。チャット中に口頭で伝えても構いません。

| ファイル | 内容 |
|---------|------|
| `company_profile/assets.md` | 技術・データ・人的・ブランド等のアセット |
| `company_profile/existing_business.md` | 既存事業の詳細 |
| `company_profile/strengths.md` | SWOT分析、業界ポジション |

※ 現在は株式会社エイチジェイの情報が入っています。別の会社で使う場合は書き換えてください。

## 使い方

### 壁打ちモード

アイデアの初期段階で軽く相談したいときに使います。

```
こんなのどう思う？ティーン向けのAIスタイリングサービス
```

→ エージェント群は起動せず、軽く打ち返し・視点の提案・自社アセットとの接点を示唆します。

### フルモード

具体的な事業アイデアや議事録を共有すると、自動的にフルモードで動きます。

```
以下の議事録の内容で新規事業を検討してほしい。
---
（議事録をペースト）
```

```
ティーン向けライブコマースプラットフォームの事業計画を作ってほしい
```

→ 8つのエージェントが並列で調査・分析を行い、最終的に事業計画書・CF/PL・企画書を出力します。

## エージェント構成

### 調査・分析フェーズ（並列実行）

| エージェント | 役割 |
|---|---|
| リサーチャー | 市場規模、競合、業界トレンド、ターゲット顧客の調査 |
| 先行事例リサーチャー | 国内外の成功・失敗事例の調査、パターン抽出 |
| クリティカルシンカー | リスク、弱点、失敗パターン、見落としの指摘 |
| ストラテジスト | 事業戦略、差別化、ポジショニング、Go-to-Market戦略 |
| アセットアナリスト | 自社アセットとのシナジー分析、競争優位性の構築 |
| 規制・法務チェッカー | 法規制、コンプライアンスリスクの洗い出し |

### 顧客検証フェーズ

| エージェント | 役割 |
|---|---|
| インタビュー設計 | 検証すべき仮説の整理、インタビューガイド作成 |

### 成果物作成フェーズ

| エージェント | 役割 |
|---|---|
| ファイナンスモデラー | CF・PL作成、収益モデル、シナリオ分析 |
| ドキュメントライター | 事業計画書・企画書（PowerPoint）の作成 |

## 出力される成果物

`output/` ディレクトリに出力されます。

| ファイル | 内容 |
|---------|------|
| `market_research.md` | 市場調査レポート |
| `competitor_analysis.md` | 競合分析 |
| `case_study.md` | 先行事例分析 |
| `risk_analysis.md` | リスク分析 |
| `legal_check.md` | 規制・法務チェックリスト |
| `interview_guide.md` | ユーザーインタビューガイド |
| `business_plan.md` | 事業計画書 |
| `financial_model.xlsx` | CF・PL（Excel） |
| `pitch_deck.pptx` | 企画書（PowerPoint） |

## HJ事業適合スコアリング

事業アイデアを以下の10軸で自動評価します（各0-10点、合計100点満点）。

- SNSフォロワー活用度
- タレント連動可能性
- イベントクロス展開
- 既存顧客基盤の活用
- ブランド親和性
- パートナー活用度
- 初期投資の少なさ
- 収益化スピード
- スケーラビリティ
- 組織適合性

## ワークスペース

`workspace/` にセッション間の議論経緯が自動保存されます。前回の続きから再開する場合は「前回の続きから」と伝えてください。

## ディレクトリ構成

```
new_product_agent/
├── CLAUDE.md                 # エージェント群の定義・ワークフロー
├── README.md                 # このファイル
├── requirements.txt          # Python依存パッケージ
├── .claude/settings.json     # Claude Code権限設定
├── .gitignore
├── agents/                   # エージェントプロンプト定義
│   ├── researcher.md
│   ├── case_researcher.md
│   ├── critical_thinker.md
│   ├── strategist.md
│   ├── asset_analyst.md
│   ├── legal_checker.md
│   ├── interview_designer.md
│   ├── finance_modeler.md
│   └── document_writer.md
├── company_profile/          # 自社情報
│   ├── assets.md
│   ├── existing_business.md
│   └── strengths.md
├── workspace/                # 議論の経緯・意思決定ログ
│   ├── decisions.md
│   ├── ideas.md
│   └── questions.md
└── output/                   # 成果物出力先（.gitignore対象）
```
