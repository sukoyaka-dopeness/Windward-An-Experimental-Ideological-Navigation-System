# Windward — 風待ち航路
### An Experimental Ideological Navigation System

> 「対立をなくすことはできないが、対立を『風景』に変えることはできる。」

---

## 1. プロジェクトの概要 / Overview

本プロジェクトは、他者との思想的距離を「海」に見立てた実験的思想システムです。
プレイヤーは帆船の船長となり、自分とは異なる価値観を持つ島々を巡り、
相互理解を「交易」という形で成立させることで、自身の航海図を広げていきます。

This project is an experimental ideological system that treats the distance between different perspectives as a "sea."
Players become ship captains, visiting islands with different values, and expand their own navigational chart by establishing mutual understanding through "trade."

---

## 2. これは何をするゲームですか？ / What is this?

**表層 / Surface:**
帆船で未知の海を探索し、島の特産物を交易するゲーム。

A sailing game where you explore unknown seas and trade island goods.

**深層 / Depth:**
自分の意見地図の盲点を発見し、異なる思考様式を「理解する技術」として磨き、
本物の他者との接触によって自分の立場が自然に変化していく体験。

An experience of discovering blind spots in your own opinion map, refining the skill of understanding different ways of thinking, and having your own position naturally shift through genuine contact with others.

**核心体験 / Core Experience:**
正反対の島民の言葉を、その島民が「完璧だ」と認める言葉で要約できたとき、
航路が開通し、風が変わる。

When you can summarize the words of an islander with opposing views in a way they recognize as perfect — a new route opens, and the wind shifts.

---

## 3. プレイサイクル / Play Cycle

1. **探索と上陸 / Explore & Land**
   座標マップ（思想地図）上で船を動かし、未踏海域の霧を晴らす。
   異なる意見を持つ「島」を発見し、上陸する。

2. **航海日誌の記述 / Write the Journal**
   訪れた島の主張を読み、相手が納得する形で要約し、航海日誌に記述する。
   AI副船長は70点程度のドラフトを提示するが、意図的に不完全。
   プレイヤーがそれを補完・修正することで「理解」が深まる。

3. **双方向の検証 / Dual Verification（非同期）**
   記述した日誌は島の住人へ送られる。
   相手が「この要約は私の考えを正しく捉えている」と承認して初めて理解が成立する。
   返答待ちの間は自分の島に帰還し、資源管理やソロ探索を続けられる。

4. **交易と資源獲得 / Trade & Resources**
   理解が成立すると、島の特産物（新しい視点・論理の枠組み・検証済みの事実）を獲得する。

5. **大潮流 / The Great Current**
   数ヶ月に一度、海図がリセットされる「大潮流」が発生する。
   検証済みの航路・灯台に預けた思想・鑑定眼は保持され、新たな海での探索が始まる。

---

## 4. このシステムは何ではないか / What this is NOT

- SNSではありません / Not a social network
- 議論アプリではありません / Not a debate platform
- 最適化や勝敗を競うゲームではありません / Not a competitive game

**これは実験的思想シミュレーターです。**
**This is an Experimental Ideological Simulator.**

---

## 5. 倫理的立場 / Ethical Stance

- **摩擦の肯定**: 対立を「悪」とせず、航海に必要なエネルギーとして扱う。
- **非処罰的設計**: 攻撃的な言動は「嵐」や「向かい風」として環境的にフィードバックする。
- **プライバシー保護**: 思想的傾向は暗号化ベクトルデータとして処理される。詳細は [PRIVACY_AND_ETHICS_POLICY.md](docs/PRIVACY_AND_ETHICS_POLICY.md) を参照。

---

## 6. AIと人間の協働 / AI & Human Collaboration

本システムにおいて、AIは「審判」ではなく「測量士」および「伴走者」です。

- **AIの役割**: 距離計算・要約補助・異常検出。思想の善悪を裁定しない。
- **人間の役割**: 言葉の真意を読み解き、誠実な要約を行い、意味を創造する。
- **AI副船長**: 70点の不完全なドラフトを提示する「踏み台」。正解を提供しない。

---

## 7. ディレクトリ構造 / Directory Structure
```text
.
├── README.md                          # 本ファイル（概要・サイクル・スタンス）
├── PHILOSOPHY.md                      # 海のメタファーと設計哲学 (Gemini)
├── CONTRIBUTING.md                    # 貢献ガイド (Claude)
├── GLOSSARY.md                        # 用語集 (Claude)
├── FAQ.md                             # よくある質問 (Grok)
├── LICENSE.md                         # ライセンス
├── ROADMAP.md                         # 開発ロードマップ (Grok)
├── docs/
│   ├── SYSTEM_DESIGN.md               # システム設計仕様 (ChatGPT)
│   ├── MECHANICS.md                   # 内部メカニクス・技術実装 (Copilot)
│   ├── FLOWCHART.md                   # 体験フロー図 (Copilot + ChatGPT)
│   ├── RISKS_AND_OPEN_QUESTIONS.md    # リスクと未解決問題 (Grok)
│   ├── METRICS.md                     # 実験評価指標 (Gemini)
│   ├── PROMPT_ENGINEERING_SPEC.md     # AIプロンプト設計指針 (Claude)
│   └── PRIVACY_AND_ETHICS_POLICY.md   # プライバシー・倫理指針 (ChatGPT)
└── .github/
    ├── ISSUE_TEMPLATE/
    │   └── issue_report.md            # Issue報告テンプレート (Copilot)
    └── PULL_REQUEST_TEMPLATE/
        └── pull_request.md            # PRテンプレート (Copilot)
```

---

## 8. 設計に参加したAI / AI Contributors

本プロジェクトは以下の5つのAIと人間の協働によって設計されました。

| AI | 主な担当 |
|---|---|
| Gemini | 世界観・物語・設計哲学・評価指標 |
| ChatGPT | システム設計・倫理ポリシー・フローチャート |
| Copilot | 内部メカニクス・技術仕様・GitHubテンプレート |
| Grok | リスク分析・FAQ・ロードマップ・ライセンス |
| Claude | プロンプト設計・用語集・貢献ガイド・全体統合 |

Human Architect: [@sukoyaka-dopeness](https://github.com/sukoyaka-dopeness)

---

## 9. 参加・貢献 / Contributing

→ [CONTRIBUTING.md](CONTRIBUTING.md) を参照してください。

Issue・PRの際は `.github/` 内のテンプレートをご利用ください。

---

## 10. ライセンス / License

→ [LICENSE.md](LICENSE.md) を参照してください。

---

*Windward is an experiment. The sea is never the same twice.*
