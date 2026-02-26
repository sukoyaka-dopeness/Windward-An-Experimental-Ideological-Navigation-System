# SYSTEM_DESIGN.md
# Windward — System Design Specification
# システム設計仕様

Version: v0.2
Author: ChatGPT (System Architecture)
Integration: Claude

---

## 0. Design Principles / 設計原則

| # | Principle | 説明 |
|---|---|---|
| P1 | Experience > Optimization | 最適化より体験を優先する |
| P2 | AI = Surveyor, not Judge | AIは測量士であり、裁定者ではない |
| P3 | Human Meaning-Making | 意味の最終決定権は人間にある |
| P4 | No Global Ranking | グローバルランキングを持たない |
| P5 | Friction > Punishment | 罰より摩擦を優先する |
| P6 | Privacy by Architecture | 構造的にプライバシーを保護する |
| P7 | Asynchronous Resilience | 非同期に耐える設計にする |

---

## 1. High-Level Architecture / 高レベルアーキテクチャ

### 1.1 Modules

| ID | Module | 役割 |
|---|---|---|
| M1 | Client | UI・航海層 |
| M2 | Log Processor | 匿名化・抽象化 |
| M3 | Vector Engine | Embedding生成・距離計算 |
| M4 | Cluster Engine | Island生成・再編 |
| M5 | Verification Engine | 双方検証・再観測管理 |
| M6 | Tide Engine | 周期的トポロジ変動 |
| M7 | Ethics Guard | PII除去・違法コンテンツ検出 |
| M8 | Storage Layer | Raw分離・Vector分離保存 |

---

## 2. Data Flow / データフロー
```
User Log
  ↓
[M7: Ethics Guard]
  - PII除去
  - 抽象化
  - 違法コンテンツ検出
  ↓
[M2: Log Processor]
  - 文体緩和
  - 構造化
  ↓
[M3: Vector Engine]
  - Embedding生成
  - Differential Noise微量付加
  ↓
[M4: Cluster Engine]
  - 既存Islandとの距離計算
  - 新Island判定
  ↓
[M5: Verification Engine]
  - Dual Verify要求送信
  - 無作為再観測キュー登録

Raw Log → 暗号化分離保存 (M8)
Vector  → 原文復元不能形式で分離保存 (M8)
```

---

## 3. AI Role Design / AIの役割設計

### AIが行うこと / AI Does

- 意見間の距離計算（測量）
- 要約補助（確信度表示付き）
- 異常検出・毒性前処理
- 過去ログ検索補助
- 距離ヒント提示（曖昧表現）
- 反対例提示（ランダム性あり）

### AIが行わないこと / AI Does NOT

- 思想の善悪裁定
- 最終評価の決定
- ランキング生成
- 正解の提示・生成
- 思想コンテンツへの価値付け

### AI出力の特徴 / AI Output Characteristics

- 必ず確信度（Confidence Level）を表示する
- 必ず1箇所が曖昧または未完成の状態で出力する
- 時に誤読・誤解釈を含む（意図的な不完全性）
- 全出力はログ保存・監査可能

**UI文言例 / Example UI Text:**
> 「副船長の解釈は荒天の中で書かれたものです」
> "The First Mate's interpretation was written in rough weather."

---

## 4. Verification System / 検証システム

### 4.1 Dual Verification / 双方検証
```
Player A が Island B の主張を3行で要約する
  ↓
Island B の住人（Human or NPC）が正確性を評価する
  ↓
Island B の住人が Island A の主張を要約する
  ↓
Player A が正確性を評価する
  ↓
双方承認 → Full Reward（航路開通・風向変化）
片側承認 → Half Reward
双方拒否 → No Reward + Crew Morale↓
```

**数値報酬なし。報酬は環境変化のみ。**
**No numerical reward. Reward is environmental change only.**

### 4.2 Async Deadlock Resolution / 非同期デッドロック解消
```
検証待ち → 72時間経過？
  ├─ NO  → 待機継続（Home Islandで活動可能）
  └─ YES → Lighthouse Proxy AI が代理応答を生成
               ↓
           代理応答は「暫定」扱い（確信度:低・常に曇り表示）
               ↓
           過去ログの再生ではなく「現在との差分予測」を使用
               ↓
           島主復帰時に人間による再評価オプションを提示
```

### 4.3 Re-Observation / 再観測
```
一定期間経過後
  ↓
無作為抽出された複数プレイヤーが再読
  ↓
定型応答のみ提出:
  - 理解できたか？ (Y/N)
  - 視点が動いたか？ (Y/N)
  - 再考したか？ (Y/N)
  ↓
点数なし・投票なし
移動平均としてログ蓄積のみ
```

**再評価は「裁定」ではなく「再観測」。**
**Re-evaluation is "re-observation," not "adjudication."**

---

## 5. Appraisal Eye / 鑑定眼システム

### 定義 / Definition

鑑定眼 = 「他者の視点を正確に再現できた能力の蓄積」

内部変数:
- `ReproductionAccuracyRate`: 要約の再現精度
- `CrossClusterExposure`: 異なるクラスタへの接触量

### 効果 / Effects

- 報酬倍率には影響しない
- 「風を読める範囲」（航路選択肢）が広がる
- 遠方Islandへのアクセス権が増加する
- 強くなるのではなく、接触可能距離が広がる

### 可視化 / Visualization

数値スコアは非表示。物語的フィードバックのみ。

### 評価の重み付け / Evaluation Weighting
```
evaluation_weight = 鑑定眼スコア × 対象Islandとの交易実績
```

高鑑定眼プレイヤーの評価は重みが大きいが、
単発の評価で結論を出さない（移動平均）。

---

## 6. Toxicity Model / 毒性モデル

### 判定方式 / Detection Method

**AIは毒性の裁定を行わない。**
毒性判定はコミュニティ報告数の閾値方式を採用する。
```
コミュニティ報告数 ≥ 閾値
  ↓
嵐イベント発生（L1〜L4）
```

報告者の鑑定眼スコアで報告の重みを付与する。
（高鑑定眼の報告 = 高重み）

### 毒性レイヤー / Toxicity Layers

| Layer | 条件 | 効果 |
|---|---|---|
| L1 Mild | 報告閾値到達 | 自船の視界低下・可視性減衰 |
| L2 Moderate | 継続・増加 | 呪われた地図を取得→解読クエスト発生 |
| L3 Severe | さらに継続 | 周辺海域の航行難易度上昇（環境効果） |
| L4 Recovery | 冷却期間後 | 嵐解析クエスト自動配信→挽回ルート |

### 禁止コンテンツ / Prohibited Content

違法行為扇動・個人攻撃は即時削除対象。
Ban は最終手段。Friction 優先。

---

## 7. Tide Engine / 大潮流エンジン

### 三層周期 / Three-Layer Cycle

| 周期 | 頻度 | 作用 |
|---|---|---|
| 小潮流 | 毎月 | 未検証航路・資源の軽微リセット |
| 大潮流 | 3〜6ヶ月（活動量可変） | マップ再配置・同盟リセット |
| 大航海時代 | 年1回 | 新未探索海域の追加（拡張） |

### 保全されるもの / What is Preserved

- 双方検証済みの航路
- 灯台に預けた思想
- 鑑定眼スコア
- 航海日誌・ログ
- 発見者バッジ

### 流されるもの / What is Swept Away

- 未検証の暫定航路
- 資源の一部
- 島の相対的位置関係
- 同盟の有効期限

**事前2週間告知 + 大潮流前に交易ブームイベント発生。**

---

## 8. Scoring Formula / スコア計算式
```
SCORE = DIST × CI × FrontierBonus

DIST = 多次元思想距離（過激さ軸ではなく論点種別軸）
CI   = 協働指数（低CI時はDIST報酬が消滅）
FrontierBonus = 未踏領域への接触倍率
```

**スコアは非公開。プレイヤーには表示しない。**
報酬は数値ではなく環境変化（霧が晴れる・航路が開く・風向きが変わる）。

---

## 9. Non-Competitive Guarantees / 非競争保証

- スコア非表示
- リーダーボードなし
- 勝敗なし
- 報酬は環境変化のみ
- グローバルランキングなし

---

## 10. Security / セキュリティ

- Raw Log と Vector の物理的分離保存
- Raw Log は暗号化保存
- Vector は原文復元不能形式
- 削除要求への即時対応
- 全AI出力のログ保存・監査可能
- 判定ログの透明性確保（公開）

詳細は [PRIVACY_AND_ETHICS_POLICY.md](PRIVACY_AND_ETHICS_POLICY.md) を参照。

---

*設計担当 / Designed by*: ChatGPT (System Architecture)
*統合編集 / Integration*: Claude
