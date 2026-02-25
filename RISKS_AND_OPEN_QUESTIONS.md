# RISKS_AND_OPEN_QUESTIONS.md
# Windward — Risks & Open Questions
# リスクと未解決問題

Version: v2.4
Author: Grok (Risk Analysis)
Integration: Claude

---

## 0. Overview / 概要

本ドキュメントは Windward の仕様上のリスクと未解決問題を記録する。
GitHubのIssueとして管理される課題の母体となる。
解決策が確定したものは「採用解」として記録し、
未解決のものは継続的に更新する。

This document records the specification risks and unresolved questions of Windward.
It serves as the source document for issues managed on GitHub.
Confirmed solutions are recorded as "adopted solutions,"
while unresolved items are continuously updated.

---

## 1. Risks / 仕様上のリスク

### R1 [!!] AI判定依存 / AI Judgment Dependency

**影響 / Impact:** 判定不信・プレイヤー萎縮・バイアス発生

**内容 / Description:**
新規性・毒性・有効性・公正評価の判定をAIに依存することで、
バイアス・誤判定・権威化のリスクが発生する。

Relying on AI for novelty, toxicity, validity, and fairness judgments
creates risks of bias, misjudgment, and authority-ization.

**採用解 / Adopted Solution:**
- AI = PreFilter + 確率提示（天気予報化）のみ
- 裁定 = 高鑑定眼プレイヤーのコミュニティ投票
- 毒性のみ = コミュニティ報告数閾値方式（AI不介入）
- 透明性 = 判定ログ公開
- 報告者の鑑定眼スコアで報告の重みを付与

**残存リスク / Remaining Risk:**
投票多数派による少数意見弾圧。
高閾値設定 + Appealフローで緩和中（U3参照）。

---

### R2 [!] AI船員助言システムの権威化 / Crew Advisory Authority Risk

**影響 / Impact:** プレイヤー主体喪失・思考停止

**内容 / Description:**
船員助言システムが一貫した存在として認識されることで、
その出力が「正解」として権威化されるリスク。
固定三人格制では「最もマシな副船長」への収束が起こりうる。

The crew advisory system being recognized as a consistent entity risks
its output being authority-ized as the "correct answer."
A fixed three-persona system may lead to convergence on "the best sub-captain."

**採用解 / Adopted Solution:**
- 流動代表制（10-20名の船員プールからランダム3名抽出）
- 観測軸固定・人格流動（距離推定軸/翻訳忠実度軸/摩擦予測軸）
- 同一組み合わせ連続不可・抽出ロジック非公開
- パズル型ドラフト（3者の組み合わせで90点到達）
- 船員間の相互批評・差異の可視化
- コピー検出 → ボーナス無効のみ（心理的罰なし）
- プレイヤーによる船員評価（逆転評価構造）
- 大潮流時に船員プールを刷新

**残存リスク / Remaining Risk:**
- 抽出パターン解析による準最適化
- 「最もマシな観測軸」への偏重
- 矛盾過多による苛立ち
- 完全解には至っていない（継続監視）

**KPI測定 / KPI Measurement:**
- コピー率の推移
- 独自出力率の推移
- アンケート「AI正解感」の低下率

---

### R3 [!] 新規プレイヤーの萎縮 / New Player Intimidation

**影響 / Impact:** 怖がり・気軽さ喪失・離脱

**内容 / Description:**
鑑定眼スコアや評価ペナルティを恐れて
新規プレイヤーが積極的に行動できなくなるリスク。

New players may be unable to act proactively due to fear of
appraisal eye scores and evaluation penalties.

**採用解 / Adopted Solution:**
- 練習港海域 = ペナルティ完全無効
- 初期ニュートラルスコア + 変動幅小
- OptOutEval（評価システムからの一時離脱オプション）
- SoftFeedback「曇り」表現（数値非表示）
- 自然発生型チュートリアル（ルールを説明しない）
- 船員助言システム：序盤は1名固定 → 中盤で3名解禁

**残存リスク / Remaining Risk:**
初期値・変動曲線のバランス調整が未完了（U5参照）。

---

### R4 [!] ルール過多・認知負荷 / Rule Overload

**影響 / Impact:** 参入障壁・離脱

**内容 / Description:**
仕様の複雑さがプレイヤーの参入障壁となり、
初期離脱を引き起こすリスク。

The complexity of the specification may become a barrier to entry
and cause early player dropout.

**採用解 / Adopted Solution:**
- メトロイド式段階解放（Trade → Eval/Lighthouse → Tide/NewContinent）
- UI = コンパス・船員の声・手紙のみ表示（デフォルト）
- 覗き窓（航海士の手帳）で数値を任意表示
- 自然発生型チュートリアル（物語の中でルールを発見させる）
- ルールはNautical Metaphorに埋め込みUI上で説明しない

**残存リスク / Remaining Risk:**
段階解放が人工的にならないようNarrative統合が必要。

---

### R5 [!] 非同期デッドロック / Async Deadlock

**影響 / Impact:** 進行不能・虚無感

**内容 / Description:**
双方検証において相手が長期間応答しない場合、
プレイヤーの進行が完全に停止するリスク。

In dual verification, if the other party does not respond for an extended period,
the player's progress may completely stop.

**採用解 / Adopted Solution:**
- 72時間無応答 → Lighthouse Proxy AIが代理応答生成
- 代理応答は「現在との差分予測」を使用（過去ログの単純再生ではない）
- 確信度:低（常に曇り表示）・暫定扱い
- 島主復帰時に人間による再評価オプションを提示
- Push通知のオプトイン設計

**残存リスク / Remaining Risk:**
Proxy AIの代理応答品質管理フローが未確定（U4参照）。

---

### R6 [!] 大潮流の喪失感 / Tidal Wave Loss Aversion

**影響 / Impact:** 離脱・Casual vs Hardcore非対称

**内容 / Description:**
定期的なマップ再配置によってプレイヤーが
「積み上げたものを失った」と感じるリスク。
カジュアルプレイヤーとヘビープレイヤーの非対称も問題。

The periodic map reconfiguration risks players feeling they have
"lost what they built up."
Asymmetry between casual and hardcore players is also an issue.

**採用解 / Adopted Solution:**
- 三層周期（1mo小潮流 / 3-6mo大潮流 / 1yr大航海時代）
- 活動量ベースの可変周期（カジュアル≒6mo / ヘビー≒3mo）
- 保全：検証済み航路・灯台・鑑定眼・ログ・バッジ
- 流失：未検証航路・資源の一部・同盟有効期限
- 事前2週間告知 + 大潮流前の交易ブームイベント
- 大航海時代は拡張のみ（喪失なし）
- 保持率予測表示（大潮流前にプレイヤーに提示）

**残存リスク / Remaining Risk:**
活動量ベース周期の具体的計算式が未確定（U5参照）。

---

### R7 Gaming / Spam（奇抜狙い・農場化）

**影響 / Impact:** 品質低下・最適化歪み

**内容 / Description:**
「遠いが簡単な意見」を大量収集することで
報酬を農場化するリスク。
または注目狙いの奇抜な新島生成のスパム。

The risk of farming rewards by mass-collecting "distant but easy opinions,"
or spamming novel-looking new island generation for attention.

**採用解 / Adopted Solution:**
- SCORE = DIST × CI × FrontierBonus（低CI時はDIST報酬消滅）
- 新大陸報酬は即時ではなく複数独立プレイヤーの検証後に付与
- 鑑定眼スコアの低下が評価影響力を下げる

**残存リスク / Remaining Risk:**
Novelty判定の客観基準が未確定（U2参照）。

---

### R8 Guild固定化・深関係阻害 / Guild Fixation

**影響 / Impact:** 多様接触の減少・表面的交流化

**内容 / Description:**
同じプレイヤーとの交流が固定化し、
エコーチェンバーをゲーム内で再現するリスク。

The risk of interaction with the same players becoming fixed,
reproducing echo chambers within the game.

**採用解 / Adopted Solution:**
- SamePartnerDecay（3回目以降から交易ボーナス逓減）
- CoopSolo交互推奨（船団フェーズとソロフェーズ）
- 船団マッチングは思想的距離が遠い相手を優先
- N人以上の同盟は外部交易を義務化
- 大潮流による同盟リセット

**残存リスク / Remaining Risk:**
強制的な分断による社交疲れ。

---

### R9 実装コスト / Implementation Cost

**影響 / Impact:** 開発負荷・スケール困難

**内容 / Description:**
AI判定・クラスタ計算・非同期インフラの
実装コストが高く、プロトタイプ段階での実現が困難なリスク。

High implementation costs for AI judgment, cluster calculation,
and async infrastructure make realization at the prototype stage difficult.

**採用解 / Adopted Solution:**
- 現フェーズ（GitHub企画書）では設計のみ
- MVP優先（CoreLoopを先に実装・ROADMAP参照）
- CloudML + OSSの活用
- ROADMAPに従い段階的に実装

**残存リスク / Remaining Risk:**
プロトタイプ実装のリソースが未確定。

---

### R10 静かな固定化 / Silent Fixation

**影響 / Impact:** 思想実験の失敗

**内容 / Description:**
攻撃的な行動ではなく、思想が静かに動かなくなることが最大のリスク。
高鑑定眼者コミュニティが新しい権威層になる可能性。
Lighthouseが思想の固定装置になる可能性。

> Windward最大の敵は「攻撃」ではなく「静かな固定化」。
> 思想が動かなくなった瞬間、実験は失敗する。

The greatest risk is not aggressive behavior,
but thought quietly ceasing to move.
The moment thought stops moving, the experiment fails.

**採用解 / Adopted Solution:**
- 裁定を「人」ではなく時間×多視点×再解釈に分散
- 単発評価で結論を出さない（移動平均方式）
- 評価は時間で揺らぐ構造
- 流動代表制による権威分散（R2の採用解と連動）
- 大潮流による定期的なネットワーク再配置

**残存リスク / Remaining Risk:**
Lighthouse固定化への具体的対策が未確定（U6参照）。
高鑑定眼者の権威層化への対策が未確定（U11参照）。

---

## 2. Open Questions / 未解決問題

優先順位 / Priority: U1 > U2/U3/U4/U5 > U6〜U11

---

### U1 AI船員助言システムの権威化・根本解
### AI Crew Advisory Authority — Fundamental Solution

**内容:**
流動代表制・パズル型ドラフト・相互批評の採用により
大幅に緩和されたが、根本的な解決には至っていない。
「最もマシな観測軸」への偏重は依然として起こりうる。

**現状の採用解:**
- 流動代表制 + パズル型ドラフト + 相互批評
- 定期的なプールシャッフル（大潮流時）

**継続募集:** 全AIへの提案を歓迎する。

---

### U2 Novelty客観基準 / Novelty Objective Criteria

**内容:**
新大陸発見の判定において、
「新規性」を客観的に測定するMetricの設計が未確定。
複数案の比較検討が必要。

**候補アプローチ:**
- 既存クラスタ重心からの最小距離による閾値設定
- 複数の高鑑定眼プレイヤーによる独立評価の一致率
- 両者の組み合わせ

---

### U3 毒性閾値・Appealフロー / Toxicity Threshold & Appeal Flow

**内容:**
コミュニティ報告数の閾値の具体値が未確定。
Appealフローの詳細設計が未確定。
鑑定眼重み付けの具体的計算式が未確定。

**考慮事項:**
- 閾値が低すぎると少数意見弾圧のリスク
- 閾値が高すぎると毒性抑止が機能しない
- Appealは誰が最終判断するか（運営不介入原則との整合）

---

### U4 Peer検証人数・Proxy品質管理
### Peer Verification Count & Proxy Quality

**内容:**
新大陸確定に必要な独立承認者の人数が未確定。
Lighthouse Proxy AIの代理応答品質管理フローが未確定。

**Proxy品質管理の候補アプローチ:**
- 代理応答には常に「暫定・確信度低」のラベルを付与
- 島主復帰後の再評価を必須にする
- Proxy応答の品質を事後的に鑑定眼スコアで評価

---

### U5 大潮流ActivityBased計算式
### Tidal Wave Activity-Based Formula

**内容:**
活動量ベースの大潮流周期可変計算式の具体的設計が未確定。

**候補式 / Candidate Formula:**
```
CycleLength = BaseCycle / (ActiveDays / 30)
// 例: BaseCycle=90日, ActiveDays=15日 → CycleLength=180日
// 検討中・未確定
```

---

### U6 Lighthouse固定化対策 / Lighthouse Fixation Countermeasure

**内容:**
長期間変化しない灯台が思想の固定装置になるリスクへの
具体的対策が未確定。

**候補案 / Candidate Solutions:**
- 長期未更新の灯台を「霧化」する
- 複数方向からのみ観測可能にする
- 灯台自身に翻訳義務を課す（定期的に他島への要約を求める）
- 大潮流時に灯台の位置を微妙にシフトさせる

---

### U7 評価可視化レベル / Evaluation Visibility Level

**内容:**
覗き窓（航海士の手帳）でどこまでの数値を
プレイヤーに開示するかの最適レベルが未確定。

**設計原則との整合:**
P11（数値は隠す、ただし覗き窓は残す）に従い、
デフォルト非表示・任意開示の方針は確定。
開示内容の詳細レベルが未確定。

---

### U8 CI数値化手法 / CI Quantification Method

**内容:**
SCORE = DIST × CI × FrontierBonusにおける
協働指数（CI）の多軸定義と具体的計算手法が未確定。

**候補軸 / Candidate Axes:**
- 対話の双方向性（一方的な発信ではないか）
- 異なるクラスタとの接触頻度
- 検証成功率の多様性
- SamePartnerDecayとの整合性

---

### U9 止揚合成品の品質評価フロー
### Synthesis Quality Evaluation Flow

**内容:**
対立意見の止揚合成によって生成された
Wisdom Cardの品質評価フローの詳細が未確定。
AI補助 + 高鑑定眼人間評価の組み合わせを予定。

---

### U10 船団マッチング公平性 / Fleet Matching Fairness

**内容:**
思想的距離を優先した船団マッチングにおいて、
マイノリティな思想を持つプレイヤーが
孤立しないための公平性アルゴリズムが未確定。

---

### U11 高鑑定眼者の権威層化
### High-Appraisal Authority Stratification

**内容:**
高鑑定眼プレイヤーに裁定権が集中することで、
新たな思想的エリート層が形成されるリスクへの対策が未確定。

**候補案 / Candidate Solutions:**
- 裁定を時間×多視点×再解釈に分散（ChatGPT提案）
- 高鑑定眼者の影響力に上限を設ける
- 高鑑定眼者を無作為抽出（特定プレイヤーへの集中を防ぐ）
- 高鑑定眼は「接触可能距離の拡張」のみに使用し裁定権を与えない

---

## 3. GitHub Issues / GitHubイシュー

以下はGitHubのIssueとして最初に掲げるべき課題。
`.github/ISSUE_TEMPLATE/issue_report.md` を使用すること。

---

**Issue #01: AI船員助言システムの権威化（U1）**

AIの出力が「唯一の正解」として扱われないよう、
流動代表制・パズル型ドラフト・相互批評を採用したが
根本解には至っていない。
「最もマシな観測軸」への収束を防ぐ
追加の構造的設計を募集する。

Related Systems: AI副船長
Priority: 最重要

---

**Issue #02: 大潮流のアセット保持率設計（R6）**

大潮流においてプレイヤーが「捨てられた」と感じず、
「新たなフロンティアが開けた」と感じるための
保持率とボーナス設計の最適値を求む。
活動量ベース計算式の具体案も募集する（U5）。

Related Systems: Tidal Wave
Priority: 高

---

**Issue #03: 毒性報告の鑑定眼重み付け（R1・U3）**

嵐を発生させるコミュニティ投票が
「嫌いな意見の弾圧」に使われないための
報告者の鑑定眼スコアに基づく重み付け計算式と
Appealフローの詳細設計を求む。

Related Systems: Toxicity, Evaluation
Priority: 高

---

*設計担当 / Designed by*: Grok (Risk Analysis)
*統合編集 / Integration*: Claude
