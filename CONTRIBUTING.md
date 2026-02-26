# CONTRIBUTING.md
# Windward — 貢献ガイド
# Contributing Guide

Version: v0.1
Author: Claude (Contributing Guide)

---

## 0. はじめに / Introduction

Windward は実験的思想シミュレーターです。
このプロジェクトへの貢献は、
ゲームの設計を改善するだけでなく、
プロジェクト自体が体現している
「異なる視点を持つ者が対話を通じて
より良い設計に近づく」というテーマの実証でもあります。

Windward is an Experimental Ideological Simulator.
Contributing to this project is not only about improving the game design —
it is also a demonstration of the theme the project itself embodies:
those with different perspectives approaching better design through dialogue.

**貢献を歓迎します / Contributions are welcome:**
- 仕様の追加・改善提案
- 世界観・物語の拡張
- リスク・未解決問題への解決案
- 技術的実装の提案
- ドキュメントの誤りの指摘
- 翻訳・多言語対応

---

## 1. 行動規範 / Code of Conduct

本プロジェクトはWindwardの設計原則を
コントリビューションの場においても適用します。

This project applies Windward's design principles
to the contribution space as well.
```
P1: Friction > Punishment
    意見の相違は排除ではなく摩擦として歓迎する

P5: Bridge > Victory
    論破ではなく架け橋を目指す

P10: AI は測量士、審判は人間コミュニティ
     AIの意見も人間の意見も等しく検討の対象

P12: Experience > Optimization
     最適化より体験・思想実験を優先する
```

**禁止事項 / Prohibited:**
- 個人攻撃・ハラスメント
- 特定の政治的立場の押し付け
- 他者の意見の一方的な否定
- プライバシーの侵害

---

## 2. リポジトリ構造 / Repository Structure
```text
.
├── README.md                          # プロジェクト概要
├── PHILOSOPHY.md                      # 設計哲学
├── CONTRIBUTING.md                    # 本ファイル
├── GLOSSARY.md                        # 用語集
├── FAQ.md                             # よくある質問
├── LICENSE.md                         # ライセンス
├── ROADMAP.md                         # 開発ロードマップ
├── docs/
│   ├── SYSTEM_DESIGN.md               # システム設計仕様
│   ├── MECHANICS.md                   # 内部メカニクス仕様
│   ├── FLOWCHART.md                   # 体験フロー図
│   ├── RISKS_AND_OPEN_QUESTIONS.md    # リスクと未解決問題
│   ├── METRICS.md                     # 実験評価指標
│   ├── PROMPT_ENGINEERING_SPEC.md     # AIプロンプト設計指針
│   └── PRIVACY_AND_ETHICS_POLICY.md   # プライバシー・倫理方針
└── .github/
    ├── ISSUE_TEMPLATE/
    │   └── issue_report.md            # Issue報告テンプレート
    └── PULL_REQUEST_TEMPLATE/
        └── pull_request.md            # PRテンプレート
```

---

## 3. Issueの作成 / Creating Issues

Issueは以下の種類に対応しています。
`.github/ISSUE_TEMPLATE/issue_report.md` を使用してください。

| 種類 | 内容 |
|---|---|
| 仕様追加 | 新しいメカニクス・システムの提案 |
| 世界観・物語 | Lore・Narrativeの追加・修正 |
| リスク・未解決問題 | 新しいリスクの発見・未解決問題への解決案 |
| バグ・不整合 | 仕様書間の矛盾・不整合の報告 |
| その他 | 上記に当てはまらない提案 |

**優先して取り組むIssue / Priority Issues:**

以下は初期Issueとして設定された最重要課題です。
```
Issue #01: AI船員助言システムの権威化（U1）
  → 「最もマシな観測軸」への収束を防ぐ構造的設計を募集

Issue #02: 大潮流のアセット保持率設計（R6）
  → 保持率とボーナス設計の最適値を募集

Issue #03: 毒性報告の鑑定眼重み付け（R1・U3）
  → 報告者の重み付け計算式とAppealフローを募集
```

詳細は [docs/RISKS_AND_OPEN_QUESTIONS.md](docs/RISKS_AND_OPEN_QUESTIONS.md) を参照。

---

## 4. Pull Requestの作成 / Creating Pull Requests

`.github/PULL_REQUEST_TEMPLATE/pull_request.md` を使用してください。

### PRを作成する前に / Before Creating a PR
```
□ 関連するIssueが存在するか確認する
  （なければIssueを先に作成することを推奨）
□ 変更するファイルと影響するシステムを特定する
□ GLOSSARY.md の用語と整合しているか確認する
□ 既存の設計原則（P1-P12）と矛盾しないか確認する
```

### レビュープロセス / Review Process

Windwardは5つのAIと人間が協働して設計されています。
PRのレビューにおいては、以下の観点から確認を依頼できます。

| レビュアー | 確認観点 |
|---|---|
| Claude | 構造整合性・用語の一貫性・全体統合 |
| Gemini | 世界観・物語・設計哲学との整合性 |
| ChatGPT | システム設計・仕様の論理的整合性 |
| Grok | リスク評価・未解決問題への影響 |
| Copilot | 技術的実装可能性・メカニクスとの整合性 |

PRテンプレートの `Verification` セクションで
どのAIへのレビューを依頼するか明示してください。

---

## 5. ドキュメントの記述規則 / Documentation Guidelines

### 5.1 言語 / Language
```
基本方針: 英語 → 日本語の順で記述する
例外: PHILOSOPHY.md・README.md は日本語 → 英語

理由:
GitHubに公開する以上、国際的な読者が最初に
目にする言語が英語であることが自然。
ただしPHILOSOPHY.md・README.mdはGeminiが
日本語で書いた文章が核心であるため、
日本語を正文として扱う。
```

### 5.2 ファイルヘッダー / File Header

全ての `.md` ファイルは以下のヘッダーを含める。
```markdown
# ファイル名.md
# Windward — [ファイルの説明 English]
# [ファイルの説明 日本語]

Version: vX.X
Author: [担当AI名] ([担当領域])
Integration: Claude  ← Claudeが統合編集した場合のみ
```

### 5.3 用語の使用 / Terminology

[GLOSSARY.md](GLOSSARY.md) に定義された用語を使用する。
新しい用語を導入する場合は GLOSSARY.md への追記も行う。

### 5.4 設計原則との整合 / Alignment with Design Principles

全ての変更は以下の原則と整合していることを確認する。
```
P1:  Friction > Punishment
P2:  NonAmplify > Deletion
P3:  Translation > Distance
P4:  Reconstruction > Collection
P5:  TopologyChange > Score
P6:  Bridge > Victory
P7:  Understanding persists through any tidal wave
P8:  Privacy = 必須要件
P9:  ルールは説明しない、体験させる
P10: AI は測量士、審判は人間コミュニティ
P11: 数値は隠す、ただし覗き窓は残す
P12: Experience > Optimization
```

---

## 6. AI協働プロジェクトとしての注意事項
## Notes on AI Collaboration

本プロジェクトは5つのAIと人間の協働によって設計されました。
AIへの変更提案・貢献においては以下に留意してください。

This project was designed through collaboration between five AIs and a human.
Please note the following when proposing changes or contributing via AI.
```
1. AIへの依頼時は担当領域を明示する
   （どのAIに何を依頼するかをPRテンプレートに記載）

2. AI出力はそのままコミットしない
   人間によるレビューと編集を経ること

3. AI出力の帰属を明示する
   Author フィールドに担当AIを記載する

4. 複数AIに同じ問いを投げて比較することを推奨する
   Windward のテーマそのものの実践

5. AIの意見が一致しない場合は
   RISKS_AND_OPEN_QUESTIONS.md に記録する
```

---

## 7. 未解決問題への貢献 / Contributing to Open Questions

[docs/RISKS_AND_OPEN_QUESTIONS.md](docs/RISKS_AND_OPEN_QUESTIONS.md) に記載された
未解決問題（U1〜U11）への解決案は特に歓迎します。

Proposed solutions to open questions (U1-U11) listed in
[docs/RISKS_AND_OPEN_QUESTIONS.md](docs/RISKS_AND_OPEN_QUESTIONS.md)
are especially welcome.
```
最重要未解決問題 / Most Critical Open Question:

U1: AI船員助言システムの権威化・根本解
    流動代表制・パズル型ドラフト・相互批評によって
    大幅に緩和されたが根本解には至っていない。
    あなたの提案をお待ちしています。

The most critical open question:
U1: Fundamental solution to AI crew advisory authority risk.
    Substantially mitigated through fluid representative model,
    puzzle-type drafts, and inter-crew critique,
    but a fundamental solution has not been reached.
    Your proposals are welcome.
```

---

## 8. 謝辞 / Acknowledgments

本プロジェクトの設計に参加した全ての知性に感謝します。

We thank all intelligences who participated in the design of this project.

| 貢献者 | 担当領域 |
|---|---|
| [@sukoyaka-dopeness](https://github.com/sukoyaka-dopeness) | Human Architect・全体構想 |
| Gemini | 世界観・物語・設計哲学・評価指標 |
| ChatGPT | システム設計・倫理ポリシー・フローチャート |
| Copilot | 内部メカニクス・技術仕様・GitHubテンプレート |
| Grok | リスク分析・FAQ・ロードマップ・ライセンス |
| Claude | プロンプト設計・用語集・貢献ガイド・全体統合 |

---

## 9. 連絡先 / Contact

GitHub Issues を通じてご連絡ください。
DMには対応していません。

Please contact us through GitHub Issues.
We do not respond to DMs.

Repository: https://github.com/sukoyaka-dopeness/windward
*(リポジトリURL確定後に更新 / To be updated after repository creation)*

---

*設計担当 / Designed by*: Claude (Contributing Guide)
