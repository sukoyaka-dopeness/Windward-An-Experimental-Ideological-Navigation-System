# GLOSSARY.md
# Windward — 用語集
# Glossary of Terms

Version: v0.1
Author: Claude (Glossary)

---

## 凡例 / Legend

各用語は以下の形式で記載する。
```
## [用語 / Term]
**読み / Reading** (日本語の場合)
**分類 / Category**: システム / UI / 哲学 / 実装
**初出 / First Appears**: 対応ファイル名
```

---

## A

### Appraisal Eye / 鑑定眼
**読み**: かんていがん
**分類**: システム
**初出**: MECHANICS.md

他者の視点を正確に再現できた能力の蓄積を示す内部変数。
数値スコアはプレイヤーに表示されない。
効果は「報酬倍率の上昇」ではなく「到達できる島の範囲の拡張」。
強くなるのではなく「風を読める範囲」が広がる。

An internal variable representing the accumulated ability to accurately
reproduce others' perspectives.
The numerical score is not displayed to players.
Its effect is not increased reward multiplier but expansion of reachable islands.
You don't become stronger — your range of readable wind expands.

内部変数:
- `ReproductionAccuracyRate`: 要約の再現精度
- `CrossClusterExposure`: 異なるクラスタへの接触量

---

### Async Engine / 非同期エンジン
**分類**: 実装
**初出**: MECHANICS.md

双方検証における非同期処理を管理するシステム。
返答待ち中はHome Islandでの活動を可能にする。
72時間無応答時にLighthouse Proxy AIを起動する。

The system managing async processing in dual verification.
Enables activities on Home Island during the wait.
Activates Lighthouse Proxy AI after 72 hours without response.

---

## C

### Canonical Vector / 正準ベクトル
**分類**: 実装
**初出**: MECHANICS.md

各Islandの核心的な主張を表すベクトル。
双方検証における要約精度の評価基準として使用される。
プレイヤーには直接開示されない。

The vector representing the core claims of each Island.
Used as the evaluation baseline for summary accuracy in dual verification.
Not directly disclosed to players.

---

### CI / Cooperation Index / 協働指数
**分類**: システム
**初出**: MECHANICS.md / RISKS_AND_OPEN_QUESTIONS.md

SCOREの計算式 `SCORE = DIST × CI × FrontierBonus` における
協働の質を示す指数。
低CI時はDISTによる報酬が消滅し、
遠くの意見を農場化するGamingを防ぐ。
具体的な多軸定義は未確定（U8参照）。

An index indicating the quality of cooperation in the score formula
`SCORE = DIST × CI × FrontierBonus`.
When CI is low, DIST-based rewards disappear,
preventing gaming by farming distant opinions.
Specific multi-axis definition is pending (see U8).

---

### Cluster Engine / クラスタエンジン
**分類**: 実装
**初出**: SYSTEM_DESIGN.md

意見ベクトルの密度ベースクラスタリングを行うモジュール。
Island生成・再編・新規性判定を担当する。
DBSCAN推奨。

The module performing density-based clustering of opinion vectors.
Responsible for Island generation, reorganization, and novelty detection.
DBSCAN recommended.

---

### Contradiction Level / 矛盾レベル
**分類**: システム
**初出**: MECHANICS.md

船員助言システムにおける3者ドラフト間の矛盾の強度。
LOW（補完）/ MID（部分対立）/ HIGH（全対立）の3段階。
各レベルで異なるゲームイベントが発生する。

The intensity of contradiction between three crew drafts
in the crew advisory system.
Three levels: LOW (complementary) / MID (partial conflict) / HIGH (full conflict).
Different game events occur at each level.

---

### Crew Advisory System / 船員助言システム
**分類**: システム / UI
**初出**: MECHANICS.md

旧称: AI副船長（AI Sub-Captain）。
10-20名の仮想船員プールから航海ごとにランダム3名が抽出され、
各々の観測軸から不完全なドラフトを提示するシステム。
プレイヤーが超えるべき「踏み台」であり、
権威化を構造的に防止するために流動代表制を採用する。

Formerly: AI Sub-Captain.
A system where 3 crew members are randomly selected per voyage
from a pool of 10-20 virtual crew members,
each presenting an imperfect draft from their observation axis.
A "stepping stone" for players to surpass,
adopting a fluid representative model to structurally prevent authority-ization.

---

### Crew Morale / 船員士気
**分類**: システム
**初出**: MECHANICS.md

船員の満足度を示す内部変数。
同質Island訪問で低下し、多様Island訪問で上昇する。
低下するとVerification速度低下・Pirate遭遇率上昇。
エコーチェンバー的航海を内部から崩壊させる設計メカニクス。

An internal variable indicating crew satisfaction.
Decreases with visits to homogeneous Islands, increases with diverse visits.
When low: verification speed decreases and pirate encounter rate increases.
A design mechanic that causes echo-chamber navigation to collapse from within.

---

## D

### DIST / Ideological Distance / 思想的距離
**分類**: システム
**初出**: MECHANICS.md

SCOREの計算式における多次元思想距離。
「過激さ」ではなく「論点の種類」で設計された軸で測定される。
コサイン距離 + 局所密度補正を使用。

The multi-dimensional ideological distance in the score formula.
Measured on axes designed around "type of issue," not "degree of extremity."
Uses cosine distance + local density correction.

---

### Dual Verification / 双方検証
**読み**: そうほうけんしょう
**分類**: システム
**初出**: SYSTEM_DESIGN.md / MECHANICS.md

WindwardのコアメカニクスのひとつO。
プレイヤーAが島Bの主張を要約し、
島Bの住人がその正確性を評価する。
さらに島Bの住人がAの主張を要約し、
AがそれをO評価する。双方の承認で初めて交易が成立する。
Contact ≠ Understanding の原則を体現する。

One of Windward's core mechanics.
Player A summarizes Island B's claims, and Island B's resident evaluates accuracy.
Then Island B's resident summarizes A's claims, and A evaluates that.
Trade is established only when both parties approve.
Embodies the principle that Contact ≠ Understanding.

---

## E

### Echo Chamber / エコーチェンバー
**分類**: 哲学
**初出**: PHILOSOPHY.md

自分と同じ意見だけが反響し増幅される認知・情報環境。
Windwardが構造的に打破することを目指す現象。
ゲーム内では「霧」「同質Island」「Crew不満」として表現される。

A cognitive and information environment where only opinions like one's own
echo and amplify.
The phenomenon Windward aims to structurally break.
Expressed in-game as "fog," "homogeneous Islands," and "crew dissatisfaction."

---

### Ethics Guard / 倫理ガード
**分類**: 実装
**初出**: SYSTEM_DESIGN.md

データ前処理モジュール。
PII除去・固有名詞の抽象化・違法コンテンツ検出を担当する。
思想の善悪を裁定しない。

The data preprocessing module.
Responsible for PII removal, abstraction of proper nouns, and illegal content detection.
Does not judge the right or wrong of thought.

---

## F

### Fog / 霧
**分類**: UI / 哲学
**初出**: PHILOSOPHY.md / README.md

未探索の思想領域を表すゲーム内のビジュアル表現。
認知バイアス・エコーチェンバーのメタファー。
プレイヤーが航海することで晴れていく。

The in-game visual representation of unexplored ideological territory.
A metaphor for cognitive bias and echo chambers.
Clears as players navigate.

---

### Frontier Bonus / フロンティアボーナス
**分類**: システム
**初出**: MECHANICS.md

未踏領域への到達に付与される報酬倍率。
`FrontierBonus = f(dist_from_known_clusters)`
既存クラスタから離れるほど倍率が上昇する。

The reward multiplier granted for reaching unexplored territory.
`FrontierBonus = f(dist_from_known_clusters)`
The multiplier increases as distance from known clusters increases.

---

## G

### Great Current / 大潮流
**読み**: おおしおながれ
**分類**: システム / UI
**初出**: MECHANICS.md / SYSTEM_DESIGN.md

定期的なマップ再配置イベント。
三層周期（小潮流/大潮流/大航海時代）で構成される。
検証済みの成果は保全され、未検証の仮状態が流される。
固定化を防止する根本的なシステム設計。

The periodic map reconfiguration event.
Consists of three-layer cycles (Minor Current / Great Current / Age of Exploration).
Verified achievements are preserved; unverified provisional states are swept away.
The foundational system design for preventing fixation.

---

## H

### Home Island / 本拠島
**分類**: UI / システム
**初出**: README.md

プレイヤー自身の意見・立場を示す島。
航海中は自動帰港先となる。
返答待ち中の活動拠点。
灯台（Lighthouse）が設置されている。

The island representing the player's own opinions and position.
The automatic return destination during voyages.
Activity base during the wait for replies.
Has a Lighthouse installed.

---

## I

### IDI / Ideological Diversity Index / 思想的多様性指数
**分類**: システム / 実装
**初出**: METRICS.md

プレイヤーが交易成立させた島々の
初期座標からの平均距離を示す指標。
`IDI = Σ dist(player_origin, island_i) / n`
エコーチェンバー打破の効果測定に使用する。

An index showing the average distance from the player's initial coordinates
to islands where trade has been established.
`IDI = Σ dist(player_origin, island_i) / n`
Used to measure the effectiveness of echo chamber breaking.

---

### Island / 島
**分類**: UI / システム
**初出**: README.md / PHILOSOPHY.md

特定の意見・価値観のクラスタを表すゲーム内の地理的単位。
プレイヤーが訪問し、交易する対象。
現実の政治・人物とは直接対応しない（抽象化済み）。

The in-game geographic unit representing a cluster of specific opinions and values.
What players visit and trade with.
Does not directly correspond to real politics or individuals (abstracted).

---

## L

### Lighthouse / 灯台
**読み**: とうだい
**分類**: システム / UI
**初出**: MECHANICS.md

プレイヤーが自分の思想を預託する場所。
Home Islandに設置されている。
大潮流後も保全される。
新大陸発見のための思想預け入れ窓口でもある。
長期間変化しない灯台の固定化リスクが未解決（U6参照）。

The place where players deposit their thoughts.
Installed on the Home Island.
Preserved even after the Great Current.
Also serves as the deposit window for thoughts aimed at new island discovery.
Fixation risk of long-unchanged lighthouses is unresolved (see U6).

---

### Lighthouse Proxy AI / 灯台代理AI
**分類**: システム / 実装
**初出**: SYSTEM_DESIGN.md / MECHANICS.md

72時間無応答時に起動する代理応答システム。
過去ログの単純再生ではなく「現在との差分予測」を使用する。
確信度は常に低。暫定扱い。
島主復帰時に人間による再評価を促す。

The proxy response system activated after 72 hours without response.
Uses "prediction of difference with the present" rather than simple replay of past logs.
Confidence level is always low. Treated as provisional.
Prompts human re-evaluation when the island owner returns.

---

## M

### Mutiny / 暴動
**読み**: ぼうどう
**分類**: システム / UI
**初出**: MECHANICS.md

内部毒性の最終形態。
同質Island訪問の継続によるCrew不満が臨界点を超えると発生する。
行動制限・移動速度低下・強制帰港を引き起こす。
エコーチェンバー的航海への内部からの自浄作用。

The final form of internal toxicity.
Occurs when crew dissatisfaction from continued homogeneous Island visits
exceeds a critical point.
Causes action restrictions, movement speed decrease, and forced return.
Internal self-correction mechanism against echo-chamber navigation.

---

## O

### Observation Axis / 観測軸
**分類**: システム / 実装
**初出**: MECHANICS.md / PROMPT_ENGINEERING_SPEC.md

船員助言システムにおける固定された測定軸。
人格は流動するが観測軸は固定される。
三軸: 距離推定軸 / 翻訳忠実度軸 / 摩擦予測軸

The fixed measurement axes in the crew advisory system.
Personas are fluid, but observation axes are fixed.
Three axes: Distance Estimation / Translation Fidelity / Friction Prediction.

---

### OptOutEval / 評価一時離脱
**分類**: システム / UI
**初出**: RISKS_AND_OPEN_QUESTIONS.md

評価システムから一時的に離脱できるオプション。
新規プレイヤーの萎縮防止・疲労回復のための緩衝設計。
離脱中は評価ペナルティが発生しない。

The option to temporarily withdraw from the evaluation system.
Buffer design for preventing new player intimidation and fatigue recovery.
No evaluation penalties occur during withdrawal.

---

## P

### Pirates / 海賊
**分類**: システム / UI
**初出**: MECHANICS.md

外部毒性の表現形態。
コミュニティ報告数が閾値を超えたとき発生するゲームイベント。
視界低下・資源損耗・Crew Morale低下を引き起こす。

The expression of external toxicity.
A game event occurring when community reports exceed the threshold.
Causes visibility reduction, resource loss, and Crew Morale decrease.

---

### Practice Harbor / 練習港
**読み**: れんしゅうみなと
**分類**: UI / システム
**初出**: RISKS_AND_OPEN_QUESTIONS.md

初心者向けの保護海域。
鑑定眼ペナルティ・評価プレッシャーが完全に無効化される。
一定の航海数を経過すると本海域へ移行する。

The protected sea area for beginners.
Appraisal eye penalties and evaluation pressure are completely disabled.
Players transition to the main sea after a certain number of voyages.

---

### Proxy Response / 代理応答
**分類**: システム
**初出**: SYSTEM_DESIGN.md

Lighthouse Proxy AIが生成する暫定的な検証応答。
常に「暫定」「確信度:低」として提示される。
島主復帰後に人間による再評価が可能。

The provisional verification response generated by Lighthouse Proxy AI.
Always presented as "provisional" with "Confidence: Low."
Human re-evaluation is possible after the island owner returns.

---

## R

### Re-Observation / 再観測
**読み**: さいかんそく
**分類**: システム
**初出**: SYSTEM_DESIGN.md

一定期間経過後、無作為抽出された複数プレイヤーが
過去のログを再読する仕組み。
定型応答（理解できたか/視点が動いたか/再考したか）のみ提出。
点数なし・ランキングなし。移動平均として記録される。
「裁定」ではなく「再観測」。

A mechanism where multiple randomly selected players re-read past logs
after a certain period.
Only fixed responses are submitted (understood / perspective shifted / reconsidered).
No scores, no rankings. Recorded as moving averages.
"Re-observation," not "adjudication."

---

## S

### Same Partner Decay / 同一相手との交易逓減
**分類**: システム
**初出**: MECHANICS.md

同じ相手との交易を繰り返すと交易効率が下がるメカニクス。
`decay = 1 / (1 + repeat_count)`
3回目以降からボーナス逓減開始。
Guild固定化・エコーチェンバー再現を防ぐ設計。

The mechanic where trade efficiency decreases with repeated trade with the same partner.
`decay = 1 / (1 + repeat_count)`
Bonus reduction begins from the third trade.
Designed to prevent guild fixation and echo chamber reproduction.

---

### SCORE Formula / スコア計算式
**分類**: システム / 実装
**初出**: MECHANICS.md

`SCORE = DIST × CI × FrontierBonus`

プレイヤーには表示されない内部計算式。
報酬は数値ではなく環境変化として表現される。
低CI時はDIST報酬が消滅し、Gamingを防ぐ。

The internal calculation formula not displayed to players.
Rewards are expressed as environmental changes, not numbers.
When CI is low, DIST rewards disappear to prevent gaming.

---

### Silent Fixation / 静かな固定化
**分類**: 哲学 / システム
**初出**: RISKS_AND_OPEN_QUESTIONS.md

Windward最大のリスク。
攻撃的な行動ではなく、
思想が静かに動かなくなることを指す。
思想が動かなくなった瞬間、実験は失敗する。

The greatest risk in Windward.
Not aggressive behavior, but thought quietly ceasing to move.
The moment thought stops moving, the experiment fails.

---

### Storm / 嵐
**分類**: UI / システム
**初出**: MECHANICS.md / PHILOSOPHY.md

毒性行動への環境的フィードバック。
Banではなく摩擦として機能する（Friction > Punishment）。
L1〜L4の段階があり、L4では回復クエストが発生する。

Environmental feedback for toxic behavior.
Functions as friction, not ban (Friction > Punishment).
Has stages L1-L4; at L4, a recovery quest is generated.

---

### Synthesis / 止揚
**読み**: しよう
**分類**: システム / 哲学
**初出**: MECHANICS.md

ヘーゲル哲学の止揚（Aufhebung）に由来。
対立する2つの意見をプレイヤーが統合し、
上位概念としてWisdom Cardを生成するシステム。
二項対立を超えた新しい視点の創造を促す。

Derived from Hegel's Aufhebung (dialectical synthesis).
A system where players integrate two opposing opinions
to generate a Wisdom Card as a higher-level concept.
Encourages the creation of new perspectives transcending binary opposition.

---

## T

### Tidal Wave / 大潮流
→ Great Current / 大潮流 を参照

---

### Trade Goods / 交易品
**分類**: システム / UI
**初出**: MECHANICS.md

双方検証成立後に交換できる4種の資源。

| 品目 | 意味 |
|---|---|
| Spice（香辛料） | 珍しい視点・反論の根拠 |
| Timber（木材） | 議論の構造・論理フレーム |
| Water（真水） | 基礎的な事実・検証済み情報 |
| Food（食料） | 対話継続のための共感・信頼ポイント |

The four types of resources exchangeable after dual verification is established.

---

### Translation / 翻訳
**読み**: ほんやく
**分類**: 哲学
**初出**: PHILOSOPHY.md

Windwardにおける中心概念。
相手の言葉を相手が納得する形で言い換える能力・行為。
距離を超えるための技術であり、勝利ではなく発見の手段。

The central concept in Windward.
The ability and act of rephrasing another's words in a way they find accurate.
A technique for crossing distance; a means of discovery, not victory.

---

## V

### Vector Embedding / ベクトル埋め込み
**分類**: 実装
**初出**: SYSTEM_DESIGN.md / PRIVACY_AND_ETHICS_POLICY.md

意見テキストを多次元ベクトル空間に変換したデータ。
原文復元不能な形式で保存される（プライバシー保護）。
Raw Logとは物理的・論理的に分離して管理される。

Data representing opinion text converted into multi-dimensional vector space.
Stored in a format that cannot reconstruct the original text (privacy protection).
Managed physically and logically separate from Raw Logs.

---

## W

### Wind / 風
**分類**: UI / システム / 哲学
**初出**: README.md / PHILOSOPHY.md

ゲーム内の移動コスト変数であり、
プロジェクトタイトル「Windward（風待ち航路）」の核心的メタファー。
追い風 = 多様な接触・交易による恩恵。
逆風 = 同質的航海・毒性行動によるコスト増。
風は待つものであり、自ら向かっていくものでもある。

The movement cost variable in-game and the core metaphor of the project title
"Windward / 風待ち航路."
Tailwind = benefits from diverse contact and trade.
Headwind = increased costs from homogeneous navigation and toxic behavior.
Wind is something to wait for, and also something to sail into.

---

### Wisdom Card / 知恵カード
**分類**: システム / UI
**初出**: MECHANICS.md

止揚合成システムによって生成される上位概念カード。
対立する2つの意見をプレイヤーが統合した成果物。
島のコレクションに追加され、他プレイヤーから参照される。

The higher-level concept card generated by the synthesis system.
The product of a player integrating two opposing opinions.
Added to the island's collection and referenced by other players.

---

*設計担当 / Designed by*: Claude (Glossary)
