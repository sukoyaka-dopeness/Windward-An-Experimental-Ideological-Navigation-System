# PRIVACY_AND_ETHICS_POLICY.md
# Windward — Privacy & Ethics Policy
# プライバシー・倫理方針

Version: v0.1
Author: ChatGPT (Ethics & Policy)
Integration: Claude

---

> 揺らすが、暴かない。分析するが、特定しない。保存するが、所有しない。
> Destabilize, but do not expose. Analyze, but do not identify. Store, but do not own.

---

## 0. 基本原則 / Core Principles

| ID | Principle | 説明 |
|---|---|---|
| P0-1 | Data Minimization | 必要最小限のデータのみ収集する |
| P0-2 | Purpose Limitation | 航海体験の提供のみに利用する |
| P0-3 | Human Primacy | 思想の意味決定は人間が行う |
| P0-4 | Non-Extractive | 商用再学習・第三者提供に使用しない |
| P0-5 | Reversible Participation | いつでも削除・撤回できる |

---

## 1. データ分類 / Data Classification

| ID | Type | 説明 | 機密度 |
|---|---|---|---|
| D1 | Raw Log | 日誌原文 | 最高（暗号化分離保存） |
| D2 | Processed Log | 固有表現除去済みテキスト | 高 |
| D3 | Vector Embedding | 意味ベクトル | 中（原文復元不能形式） |
| D4 | Meta Data | 時刻・距離・検証履歴 | 低 |
| D5 | System Signals | 鑑定眼内部値など | 低 |

**保存原則 / Storage Rules:**
- D1 は暗号化分離保存
- D3 は原文復元不能な形式で保存
- D1 と D3 は物理的・論理的に分離する
- D1 と D3 を紐付けるキーは別途管理する

---

## 2. ベクトル化方針 / Vectorization Policy

| ID | Rule | 内容 |
|---|---|---|
| V1 | PII自動除去 | NER + ルールベースで個人情報を除去 |
| V2 | 固有名詞の抽象化 | 例：「東京」→「大都市」 |
| V3 | ローカルEmbedding優先 | 外部APIへの送信を最小化 |
| V4 | Differential Noise注入 | 微小摂動を付加してプライバシーを強化 |
| V5 | 復元不能性テスト | 定期的に元文再構成不能性を検証する |

**禁止事項 / Prohibited:**
- 生ログの外部モデル再学習への利用
- 生ログの第三者提供
- ベクトルから原文を復元する試み

---

## 3. 匿名化設計 / Anonymization Design

| ID | Rule | 内容 |
|---|---|---|
| A1 | 島民としての提示 | 表示は常に「島民」として匿名化 |
| A2 | 時刻の範囲表示 | 例：「数日前」（正確な時刻は非表示） |
| A3 | 文体指紋の緩和 | 軽微なパラフレーズで文体特徴を緩和 |
| A4 | k-匿名性の確保 | 小規模クラスタは公開閾値を設ける（k ≥ k_min） |
| A5 | 孤立意見の保護 | 孤立意見は即公開せず、再識別リスクを評価してから公開 |

---

## 4. 他プレイヤーへの提示 / Presentation to Other Players

| ID | Rule | 内容 |
|---|---|---|
| T1 | 原文の非公開原則 | 日誌原文は原則として非公開 |
| T2 | 要約のみ提示 | 要約 + 本人確認済み再現文のみを提示 |
| T3 | 理解検証後の部分開示 | 双方検証通過後に限り部分的に開示可 |
| T4 | 直接DM機能を持たない | 構造的距離を維持するためDM機能を実装しない |

---

## 5. 思想的安全性 / Ideological Safety

| ID | Rule | 内容 |
|---|---|---|
| S1 | 違法・個人攻撃は削除対象 | 違法行為扇動・個人攻撃は即時削除 |
| S2 | 毒性は「嵐」で対応 | 可視性低下・移動速度低下として処理 |
| S3 | Banより Friction 優先 | 排除より摩擦を優先する |
| S4 | 異端思想は保護対象 | 少数意見を多数派抑圧から保護する |
| S5 | 少数派ログの補正 | 少数派意見は露出アルゴリズムで補正する |

---

## 6. 再評価プロセスの倫理 / Ethics of Re-Evaluation

| ID | Rule | 内容 |
|---|---|---|
| R1 | 無作為抽出 | 再評価者は無作為に抽出する |
| R2 | 数値採点禁止 | 点数による評価を禁止する |
| R3 | コメントの公開ログ化 | 評価コメントは公開ログとして記録する |
| R4 | 評価履歴の監査可能性 | 評価履歴は監査可能な形式で保存する |
| R5 | 運営の不介入 | 運営は思想の真偽を裁定しない |

---

## 7. AI利用倫理 / AI Ethics

### AIが行うこと / AI Does
- 距離計算（測量）
- 要約補助
- 異常検出・前処理

### AIが行わないこと / AI Does NOT
- 思想の善悪判断
- 正解の生成
- ランキング付与
- 最終裁定

### AI出力の要件 / AI Output Requirements
- 常に確信度（Confidence Level）を表示する
- 全出力をログ保存する
- 全出力を監査可能にする

---

## 8. 削除・忘却権 / Right to Deletion & Erasure

| ID | Rule | 内容 |
|---|---|---|
| F1 | 原文の即時削除 | Raw Logは要求から即時削除する |
| F2 | ベクトルの不可逆匿名化 | Vector Embeddingは削除不可能だが不可逆匿名化済み |
| F3 | 削除後の再クラスタリング | 削除後にCluster Engineが再計算を実施する |
| F4 | 退会時の全Raw消去 | 退会時にD1（Raw Log）を全て消去する |

---

## 9. 透明性 / Transparency

| ID | Rule | 内容 |
|---|---|---|
| TR1 | アルゴリズム概要の公開 | GitHubでアルゴリズム概要を公開する |
| TR2 | 年次倫理レポート | 年次倫理レポートを公開する |
| TR3 | バイアス検査結果の公開 | バイアス検査結果を定期公開する |
| TR4 | 重大変更の事前告知 | 重大な変更は事前に告知する |

---

## 10. リスクと未解決問題 / Risks & Unresolved Issues

| ID | Risk | 内容 |
|---|---|---|
| U1 | 高度Embeddingからの意味復元 | 将来的な高度モデルによる原文復元の可能性 |
| U2 | 小規模クラスタの再識別 | 小規模島での再識別リスク |
| U3 | 文体特徴からの推測 | 文体指紋による個人特定の可能性 |
| U4 | 法規制変動 | GDPR類似規制の将来的変動 |
| U5 | 国家間の法的差異 | 地域によるデータ保護法の差異 |

詳細は [docs/RISKS_AND_OPEN_QUESTIONS.md](docs/RISKS_AND_OPEN_QUESTIONS.md) を参照。

---

## 11. 倫理的立場の宣言 / Ethical Declaration

Windward は：
- 思想を収集しない
- 思想を利用しない
- 思想を売らない

Windward は：
- 思想を揺らす環境を提供するだけ

**思想の所有権は常にプレイヤーにある。**
**The ownership of thought always belongs to the player.**

Windward does not collect thought.
Windward does not use thought.
Windward does not sell thought.

Windward only provides an environment in which thought can be moved.

---

*設計担当 / Designed by*: ChatGPT (Ethics & Policy)
*統合編集 / Integration*: Claude
