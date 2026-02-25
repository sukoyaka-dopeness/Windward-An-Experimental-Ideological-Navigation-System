# MECHANICS.md
# Windward — Internal Mechanics Specification
# 内部メカニクス仕様

Version: v0.2
Author: Copilot (Internal Mechanics)
Integration: Claude

---

## 0. Purpose / 目的

本書は Windward の「内部メカニクス（海の下で動く計算）」を定義する。
UI には直接表示されないが、ゲーム体験の背骨となる。

This document defines the internal mechanics of Windward —
the calculations that operate beneath the surface of the sea.
They are not directly visible in the UI, but form the backbone of the game experience.

---

## 1. Opinion-Space Model / 意見空間モデル

### 1.1 Multi-Dimensional Vector Map / 多次元ベクトルマップ

各意見はn次元ベクトル空間上の点として表現される。

Each opinion is represented as a point in n-dimensional vector space.
```
v ∈ R^n
Island = 密度ベースクラスタ（DBSCAN推奨）
Distance = コサイン距離 + 局所密度補正
dist(v1, v2) = cosine_distance(v1, v2) × density_correction_factor
```

**軸の設計原則 / Axis Design Principle:**
距離の軸は「過激さ」ではなく「論点の種類」で設計する。
極端な意見ほど有利になる歪みを防ぐ。

Distance axes are designed around "type of issue," not "degree of extremity."
This prevents the distortion where more extreme opinions score higher.

### 1.2 Frontier Bonus / フロンティアボーナス
```
FrontierBonus = f(dist_from_known_clusters)
未踏領域ほど報酬倍率が上昇する。
```

### 1.3 Seasonal Topology Shift / 大潮流
```
三層周期:
  小潮流 (毎月):     未検証航路・資源の軽微リセット
  大潮流 (3-6ヶ月):  Island座標の再計算・同盟リセット
                     活動量ベースで周期を可変調整
  大航海時代 (年1回): 新未探索海域の追加（拡張のみ）

保全: Verified Routes / Lighthouse / 鑑定眼 / Log
流失: Unverified Routes / Alliance / 資源の一部
```

---

## 2. Dual Verification Engine / 双方検証エンジン

### 2.1 Summary Matching / 要約マッチング
```
Player Summary  : S
Island Canonical Vector : C
AI Draft        : D（意図的に不完全・65-70点相当）

accuracy  = sim(S, C)   // プレイヤー要約の精度
draft_gap = sim(D, C)   // AIドラフトの精度
bonus     = max(0, accuracy - draft_gap)
// プレイヤーがAIを超えた分だけボーナス発生
```

**AI副船長の不完全性設計 / AI Imperfection Design:**
- 事実は正確だが文脈が浅い
- 論理は通っているが感情的背景を欠く
- 要点は押さえているが最重要の一文を外している
- 時に誤読・誤解釈を含む（意図的）
- 必ず確信度（Confidence Level）を表示する

### 2.2 Approval Logic / 承認ロジック
```
双方承認 → Full Reward  （航路開通・風向変化）
片側承認 → Half Reward
双方拒否 → No Reward + Crew Morale↓

数値報酬なし。報酬は環境変化のみ。
```

### 2.3 Async Deadlock Resolution / 非同期デッドロック解消
```
72時間無応答
  ↓
Lighthouse Proxy AI が代理応答を生成
  - 過去ログの単純再生ではなく「現在との差分予測」を使用
  - 確信度:低（常に曇り表示）
  - 暫定扱い
  ↓
島主復帰時に人間による再評価オプションを提示
```

---

## 3. Trade System / 交易システム

### 3.1 Trade Goods / 交易品

| 品目 | 意味 |
|---|---|
| Spice（香辛料） | 珍しい視点・反論の根拠 |
| Timber（木材） | 議論の構造・論理フレーム |
| Water（真水） | 基礎的な事実・検証済み情報 |
| Food（食料） | 対話を続けるための共感・信頼ポイント |

### 3.2 Trade Yield / 交易収量
```
yield = base × diversity_factor × kanteigan_weight
```

交易品はゲーム内行動のみで獲得可能。購入不可。

### 3.3 Same Partner Decay / 同一相手との交易逓減
```
decay = 1 / (1 + repeat_count)
// 同じ相手との交易はrepeat_countが増えるほど効率が下がる
// 3回目以降からボーナス逓減開始
```

---

## 4. Resource Model / 資源モデル

### 4.1 Resources / 資源一覧

| 資源 | 役割 | 枯渇時の効果 |
|---|---|---|
| Food（食料） | 対話継続コスト・航続距離 | 強制帰港 |
| Water（真水） | 検証コスト | 検証精度低下 |
| Crew（船員） | 並行クエスト数 | 一度に一島のみ探索可 |
| Sail/Timber（帆・木材） | 移動速度 | 近島のみ到達可 |
| Wind（風） | 毎ターン変化する変数 | 追い風=ボーナス / 逆風=コスト増 |

帆船設定のため石炭は不使用。
風は多様な島への接触量・交易量・季節イベントで変動する。

### 4.2 Crew Morale / 船員士気
```
同質Island訪問継続 → Morale↓ → Verification速度↓ / Pirate遭遇率↑
多様Island訪問     → Morale↑ → ボーナス航路解放
画期的発見         → 伝説の船員が加入
```

船員の不満・暴動はエコーチェンバー的航海を
内部から崩壊させる設計上のメカニクスである。

Crew dissatisfaction and mutiny are designed mechanics that cause
echo-chamber navigation to collapse from within.

---

## 5. Toxicity System / 毒性システム

### 5.1 External Toxicity = Pirates / 外部毒性＝海賊
```
コミュニティ報告数 ≥ 閾値
  ↓
海賊イベント発生
  - 視界低下
  - 資源損耗
  - Crew Morale↓
報告者の鑑定眼スコアで報告の重みを付与
```

### 5.2 Internal Toxicity = Mutiny / 内部毒性＝暴動
```
偏った航路継続（同質Island集中）
  ↓
Crew不満蓄積
  ↓
暴動発生
  - 行動制限
  - 移動速度低下
  - 強制帰港
```

### 5.3 Toxicity Layers / 毒性レイヤー

| Layer | 効果 |
|---|---|
| L1 Mild | 自船の視界低下・可視性減衰 |
| L2 Moderate | 呪われた地図取得→解読クエスト発生 |
| L3 Severe | 周辺海域の環境品質低下（全体影響） |
| L4 Recovery | 嵐解析クエスト自動配信→挽回ルート |

---

## 6. AI Sub-Captains / AI副船長（複数構造）

### 6.0 設計思想 / Design Philosophy

**単一の副船長は権威化される。**
人は一貫した存在を参照軸として権威化する傾向がある。
この問題を構造的に解決するため、副船長は複数視点構造を採用する。
副船長たちは時に矛盾し、互いに異論を出す。
「どれが正しいかわからない」状態を意図的に作ることで、
プレイヤーが自分で判断せざるを得なくなる。

**A single sub-captain will be authority-ized.**
Humans tend to create a reference axis by authority-izing a consistent entity.
To structurally resolve this, sub-captains adopt a multi-perspective structure.
Sub-captains sometimes contradict each other and present differing views.
By intentionally creating a state of "I don't know which is correct,"
players are compelled to make their own judgments.

---

### 6.1 Three Sub-Captains / 三人の副船長

| 副船長 | 通称 | 重視する視点 | 意図的な不完全さ |
|---|---|---|---|
| A | 羅針盤（Compass） | 論理・構造・距離計算 | 論理は正確だが感情的背景を欠く |
| B | 航海日誌（Journal） | 感情・文脈・文化的背景 | 感情は豊かだが論理構造が甘い |
| C | 海図（Chart） | 歴史的・比較的・俯瞰的視点 | 俯瞰的だが具体性に欠く |

3者は同一の島民意見に対して**異なる解釈**を出す。
時に互いに矛盾する。これは仕様であり、バグではない。

The three produce **different interpretations** of the same islander opinion.
They sometimes contradict each other. This is by design, not a bug.

---

### 6.2 Draft Generation / ドラフト生成
```
各副船長が独立して65-70点相当の要約案を生成

副船長A（羅針盤）:
  - 論理構造は正確
  - 感情的背景・文化的文脈を欠く
  - 距離計算ヒントを含む

副船長B（航海日誌）:
  - 感情的共鳴は豊か
  - 論理の厳密さが甘い
  - 時に過度に共感的

副船長C（海図）:
  - 歴史的・比較的な俯瞰
  - 具体性に欠ける
  - 抽象度が高すぎることがある

共通仕様:
  - 必ず確信度（Confidence Level）を表示する
  - 時に誤読・誤解釈を含む（意図的）
  - UI上で「荒天の中で書かれた解釈」として提示
```

**UI文言例 / Example UI Text:**
> 羅針盤：「方位は正しいが、島の温度が読めていない」
> 航海日誌：「風の感触はわかるが、航路の論理が甘い」
> 海図：「この島の位置は既知だが、今の潮流が考慮されていない」

---

### 6.3 Player Surpass Bonus / プレイヤー超越ボーナス
```
PlayerSummary の精度が3者全員のドラフトを上回った場合
  → 最大ボーナス発生（Full Surpass）

PlayerSummary の精度が1-2者を上回った場合
  → 部分ボーナス発生（Partial Surpass）

PlayerSummary がいずれのドラフトも下回った場合
  → ボーナスなし（通常点のみ）

bonus = max(0, sim(PlayerSummary, C) - max(sim(A,C), sim(B,C), sim(C,C)))
```

AIドラフトをそのままコピーすると：
- ボーナス発生なし（通常点のみ）
- 「模倣」として船員が不満を漏らす（心理的抑止）
- 3者の中から1つを選んでコピーしても同様

---

### 6.4 Contradiction Handling / 矛盾の扱い
```
3者が矛盾した解釈を出した場合:
  → プレイヤーへの通知:
     「副船長たちの意見が分かれています。あなたはどう読みますか？」

矛盾の種類:
  A vs B: 論理と感情の対立
  A vs C: 具体と抽象の対立
  B vs C: 感情と俯瞰の対立
  A vs B vs C: 三者三様

矛盾が多いほど → その島の意見の複雑さを示す
矛盾した状況でのPlayerSurpassボーナス → 最大倍率
```

---

### 6.5 Difficulty Toggle / 難易度トグル
```
ベテラン: 副船長オフ（高報酬倍率・完全自力）
中級者:   副船長1名選択（中報酬倍率）
初心者:   副船長3名全表示（低報酬倍率・練習港では制限なし）
```

プレイヤーはどの副船長を参考にするか、あるいは全員無視するかを選べる。
参考にしないことも有効な戦略である。

Players can choose which sub-captain to reference, or ignore all of them.
Ignoring all is also a valid strategy.

---

### 6.6 U1 Resolution Status / U1解決状況
```
U1: AI副船長の正解権威化
  従来の暫定解: わざとな不完全設計 + 免責UI表示
  追加の構造解: 複数副船長 + 矛盾設計

評価:
  単一副船長の権威化リスク → 大幅に低減
  「どれが正しいかわからない」状態 → 構造的に達成
  プレイヤーの主体性 → 強制的に担保

残存リスク:
  「3者の中で最もマシな副船長」への収束は起こりうる
  → 副船長の性格を定期的にシャッフルすることで対応（検討中）
```

---

## 7. Lighthouse System / 灯台システム

### 7.1 Thought Deposit / 思想の預け入れ
```
Player が自身の立場・思想を灯台に預託
  ↓
AI がクラスタ距離を計算し Novelty 候補として登録
  ↓
複数の高鑑定眼プレイヤーが独立して承認
  ↓
新Island（新大陸）として確定 + 発見者バッジ（永続）
```

**新島確定の条件 / New Island Confirmation:**
- 報酬は即時ではなく検証後に付与（奇抜狙い防止）
- 複数の独立したプレイヤーの承認が必要
- 暫定バッジを即時付与→確定バッジは検証後

**灯台の固定化リスク / Lighthouse Fixation Risk:**
大潮流後も灯台は保全されるが、
長期間変化しない灯台は「霧化」するリスクがある（検討中）。

### 7.2 Lighthouse Proxy AI / 灯台代理AI
```
72時間無応答時に代理応答を生成
- 過去ログの単純再生ではなく「現在との差分予測」
- 確信度:低（常に曇り表示）
- 暫定扱い・島主復帰時に再評価オプション提示
```

---

## 8. Synthesis System / 止揚合成システム

### 8.1 Integration / 統合
```
対立する意見パーツ A + B
  ↓
Player が自分の言葉で統合文 I を記述
  ↓
Wisdom Card = f(A, B, I)
上位カードとして島のコレクションに追加
```

品質評価は高鑑定眼プレイヤーの人間評価 + AI補助で実施。
詳細フローは未確定（OPEN QUESTION U9）。

---

## 9. Score Formula / スコア計算式
```
SCORE = DIST × CI × FrontierBonus

DIST          = 多次元思想距離（論点種別軸）
CI            = 協働指数（低CI時はDIST報酬消滅）
FrontierBonus = 未踏領域倍率

スコアはプレイヤーに非表示。
報酬は環境変化のみ（霧が晴れる・航路が開く・風向きが変わる）。
```

---

## 10. Async Engine / 非同期エンジン
```
ターン終了 → 自動帰港（Home Island）
返答待ち中 → Home Island で資源管理・ソロ探索・日誌整理
72時間経過 → Lighthouse Proxy AI が暫定応答
島主復帰時 → 人間による再評価オプション提示
Push通知   → 返答到着時にオプトイン通知
```

---

## 11. Anti-Fixation System / 固定化防止システム
```
SamePartnerDecay:    同一相手との交易逓減（3回目以降）
CoopSoloAlternation: 協力フェーズとソロフェーズを交互に推奨
AllianceExpiry:      同盟は大潮流でリセット
LargeAllianceRule:   N人以上の同盟は外部交易を義務化
MatchingBias:        船団マッチングは思想的距離が遠い相手を優先
```

---

*設計担当 / Designed by*: Copilot (Internal Mechanics)
*統合編集 / Integration*: Claude
