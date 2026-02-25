# MECHANICS.md
# Windward — Internal Mechanics Specification
# 内部メカニクス仕様

Version: v0.3
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
Player Summary          : S
Island Canonical Vector : C
Crew Draft (composite)  : D（船員ドラフトの複合・意図的に不完全）

accuracy  = sim(S, C)
draft_gap = max(sim(D_1,C), sim(D_2,C), sim(D_3,C))
bonus     = max(0, accuracy - draft_gap)
// プレイヤーが全船員ドラフトを超えた分だけボーナス発生
```

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

## 6. Crew Advisory System / 船員助言システム（旧：AI副船長）

### 6.0 設計思想 / Design Philosophy

**副船長を「人格」にしない。副船長を「流動する観測代表」にする。**

単一の、あるいは固定された副船長は権威化される。
人は一貫した存在を参照軸として権威化する傾向がある。
この問題を構造的に解決するため、以下の設計を採用する。

- 船員AIは多数存在するが非公開（クラスタ群）
- 各航海で3名のみがランダムに抽出される
- 同一組み合わせは連続して選出されない
- 抽出ロジックは非公開
- 各船員は継続的な記憶を持たない
- 出力は「副船長の言葉」ではなく「船員の噂話」として提示される

**Do not give the first mate a personality. Make them a fluid observational representative.**

A single or fixed sub-captain will be authority-ized.
Humans tend to create a reference axis by authority-izing a consistent entity.
To structurally resolve this, the following design is adopted.

---

### 6.1 Crew Pool Structure / 船員プール構造
```
船員プール: 10-20名の仮想船員（性格・専門をランダム生成）
各航海:     プールから3名をランダム抽出
連続制限:   同一組み合わせは連続不可
抽出ロジック: 非公開（メタ最適化を防止）
記憶:       各船員は継続的記憶を持たない
大潮流時:   プールを刷新（シャッフル）
```

---

### 6.2 Observation Axes / 観測軸

**人格は流動するが、観測軸は固定する。**
権威を人格ではなく「測定軸」に帰属させる。

**Personas are fluid, but observation axes are fixed.**
Authority is attributed to "measurement axes," not to personas.

| 軸 | 内容 | 意図的な不完全さ |
|---|---|---|
| 距離推定軸 | 論理・構造・距離計算重視 | 論理は正確だが感情的背景を欠く |
| 翻訳忠実度軸 | 感情・文脈・文化的背景重視 | 感情は豊かだが論理構造が甘い |
| 摩擦予測軸 | 歴史的・比較的・俯瞰的視点 | 俯瞰的だが具体性に欠ける |

各航海で抽出された3名の船員が
それぞれ異なる観測軸を担当する。
担当軸は毎回異なる船員が担う。

---

### 6.3 Draft Generation / ドラフト生成
```
各船員が独立してドラフトを生成

共通仕様:
  - 65-70点相当（意図的に不完全）
  - 必ず確信度（Confidence Level）を表示する
  - 時に誤読・誤解釈を含む（意図的）

パズル型設計（Gemini提案採用）:
  - 各ドラフトには意図的な欠損を設ける
    （伏せ字・矛盾・主語の欠落など）
  - 3者のドラフトを「素材」として組み合わせることで
    90点以上の理解に到達できる構造
  - どれか1つを選ぶのではなく全員を素材として使うことを促す
```

**UI提示形式 / UI Presentation:**
「船員たちの噂話」として提示する。権威性を物語レベルで低下させる。

> 例：「荒天の中で書かれた暫定解釈」
> 例：「観測条件：視界不良」
> 例：「解釈信頼度：揺らぎあり」

AIを人格ではなく環境・天候に近づける。

---

### 6.4 Contradiction Handling / 矛盾の制御

矛盾レベルを3段階で設計し、それぞれ異なるゲームイベントを発生させる。

| レベル | 状態 | ゲームイベント |
|---|---|---|
| 低 | 補完・互換 | 一致ボーナス |
| 中 | 部分対立 | 船員議論アニメ（選択を促す） |
| 高 | 全対立 | プレイヤー仲裁クエスト（報酬大） |

高レベル矛盾時：
> 「船員たちの意見が真っ向から対立しています。あなたはどう読みますか？」

矛盾が多いほどその島の意見の複雑さを示す。
高レベル矛盾でのPlayerSurpassボーナスは最大倍率。

---

### 6.5 Inter-Crew Critique / 船員間の相互批評
```
船員AがBの解釈に異議を唱えることがある
不一致はUI上に可視化される
AIが合意するのではなく「差異」を提示する
→ AIに正解が存在しないことを構造的に示す
```

---

### 6.6 Player Surpass Bonus / プレイヤー超越ボーナス
```
bonus = max(0, sim(S, C) - max(sim(D_1,C), sim(D_2,C), sim(D_3,C)))

Full Surpass   : 全ドラフトを超えた → 最大ボーナス
Partial Surpass: 1-2者を超えた     → 部分ボーナス
No Surpass     : いずれも超えず    → 通常スコアのみ
Copy Detected  : コピー検出        → ボーナス無効のみ
                                    （心理的罰は与えない）
```

**コピー抑止設計について / Copy Deterrence Design:**
コピー検出時はボーナス無効のみとする。
「船員不満」などの心理的罰は最小化する。
翻訳成功との誤判定リスクを避けるため。
P1（Friction > Punishment）に従う。

---

### 6.7 Player Trust Rating / プレイヤーによる船員評価
```
プレイヤーは各船員ドラフトを評価できる
評価はゲーム内で変動する
→ 権威化の方向を逆転させる
   （AI→人間ではなく、人間→AIの評価構造）
```

---

### 6.8 Difficulty & Accessibility / 難易度とアクセシビリティ
```
初心者:   序盤は1名固定 → 中盤で3名解禁（練習港では制限なし）
中級者:   3名表示（デフォルト）
ベテラン: 船員オフ（高報酬倍率・完全自力）

UI:
  デフォルト: 音声・アイコン中心（認知負荷を最小化）
  覗き窓:    詳細比較表（任意表示）
```

---

### 6.9 U1 Resolution Status / U1解決状況
```
U1: AI副船長の正解権威化

以前の状態: 根本解なし
現在の状態: 構造的耐性が大幅に向上（実質的部分解決）

採用した構造:
  - 流動代表制（プールからランダム抽出）
  - 観測軸固定・人格流動
  - パズル型ドラフト（組み合わせで90点到達）
  - 相互批評・差異の可視化
  - 逆転評価構造（人間→AI）
  - 定期的なプールシャッフル

残存リスク:
  - 抽出パターン解析による準最適化
  - 「最もマシな観測軸」への偏重
  - 矛盾過多による苛立ち
  - 完全解には至っていない（継続監視）

KPI測定:
  - コピー率の推移
  - 独自出力率の推移
  - アンケート「AI正解感」の低下率
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
- 暫定バッジを即時付与 → 確定バッジは検証後

**灯台の固定化リスク / Lighthouse Fixation Risk:**
大潮流後も灯台は保全されるが、
長期間変化しない灯台は「霧化」するリスクがある（検討中・U6参照）。

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
返答待ち中 → Home Island で資源管理・ソロ探索・日誌整理・灯台更新
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
CrewPoolShuffle:     大潮流時に船員プールを刷新
```

---

*設計担当 / Designed by*: Copilot (Internal Mechanics)
*統合編集 / Integration*: Claude
