# ROADMAP.md
# Windward — 開発ロードマップ
# Development Roadmap

Version: v0.2
Author: Grok (Roadmap)
Integration: Claude

---

## 0. Overview / 概要

本ロードマップはWindwardの段階的な開発計画を示す。
現フェーズ（GitHub企画書）では設計の公開と
コミュニティからのフィードバック収集を優先する。
実装は設計の安定後に段階的に進める。

This roadmap shows the phased development plan for Windward.
The current phase (GitHub proposal) prioritizes publishing the design
and collecting community feedback.
Implementation proceeds incrementally after the design stabilizes.

---

## Phase 0: Design Publication / 設計公開
**現在のフェーズ / Current Phase**
**期間 / Duration**: 〜2026年Q1

### 目標 / Goals
- GitHub上での設計仕様の公開
- 5AI協働設計プロセスの記録と共有
- コミュニティからのフィードバック収集開始
- 初期Issueの設定と議論の開始

### 成果物 / Deliverables
```
✓ README.md
✓ PHILOSOPHY.md
✓ CONTRIBUTING.md
✓ GLOSSARY.md
✓ FAQ.md
✓ LICENSE.md
✓ ROADMAP.md
✓ docs/SYSTEM_DESIGN.md
✓ docs/MECHANICS.md
✓ docs/FLOWCHART.md
✓ docs/RISKS_AND_OPEN_QUESTIONS.md
✓ docs/METRICS.md
✓ docs/PROMPT_ENGINEERING_SPEC.md
✓ docs/PRIVACY_AND_ETHICS_POLICY.md
✓ .github/ISSUE_TEMPLATE/issue_report.md
✓ .github/PULL_REQUEST_TEMPLATE/pull_request.md
```

### 優先Issue / Priority Issues
```
Issue #01: AI船員助言システムの権威化（U1）
Issue #02: 大潮流のアセット保持率設計（R6）
Issue #03: 毒性報告の鑑定眼重み付け（R1・U3）
```

---

## Phase 1: MVP / 最小体験プロトタイプ
**期間 / Duration**: 2026年Q2〜Q3（目安1〜3ヶ月）

### 目標 / Goals
非同期探索ループの中核体験を実装し、
少人数でのユーザー体験テストを実施する。

Implement the core experience of the async exploration loop
and conduct user experience testing with a small group.

### 実装範囲 / Scope

**コアループ / Core Loop:**
```
- 非同期探索ループ
  （航海 → 日誌記述 → 双方検証 → 交易）
- 基本UI
  （コンパス / 船員の声 / 手紙 / 天気）
- 単一海域マップ（固定）
```

**船員助言システム / Crew Advisory System:**
```
- 流動代表制（簡易版: 3名固定 → 後のPhaseでプール化）
- 3観測軸（距離推定 / 翻訳忠実度 / 摩擦予測）
- 確信度表示
- コピー検出 → ボーナス無効
```

**資源モデル / Resource Model:**
```
- 基本資源（食料 / 真水 / 船員 / 帆・木材）
- 船員士気の基本実装
```

**灯台 / Lighthouse:**
```
- 思想の預け入れ（基本実装）
- Lighthouse Proxy AI（簡易版）
```

**毒性メタファー / Toxicity:**
```
- 嵐 / 海賊 / 暴動の基本実装
- コミュニティ報告の基本フロー
```

**鑑定眼 / Appraisal Eye:**
```
- 初期版（軽ペナルティ・練習港あり）
```

### 目標指標 / Target Metrics
```
- 双方検証の完了率 > 60%
- プレイヤー超越率 > 30%
  （AIドラフトを超えた要約の割合）
- 離脱率の測定開始
```

---

## Phase 2: Depth & Social / 深化とソーシャル
**期間 / Duration**: 2026年Q4〜2027年Q2（目安3〜9ヶ月）

### 目標 / Goals
マルチプレイの拡張とコミュニティ形成を進める。
エコーチェンバー打破効果の初期測定を開始する。

Advance multiplayer expansion and community formation.
Begin initial measurement of echo chamber breaking effectiveness.

### 実装範囲 / Scope

**段階的ルール解放 / Staged Unlock:**
```
- 中級解放: 鑑定眼強化 / 灯台強化 / 公正評価寄与
- メトロイド式解放フローの完全実装
```

**大潮流 / Tidal Wave:**
```
- 三層周期の完全実装
  （1mo小潮流 / 3-6mo大潮流 / 1yr大航海時代）
- 活動量ベース可変周期（基本実装）
- 事前告知システム + 交易ブームイベント
```

**新大陸発見 / New Island Discovery:**
```
- Novelty判定フロー
- Peer検証遅延報酬システム
- 発見者バッジ
```

**船員助言システム強化 / Crew Advisory Enhancement:**
```
- 船員プール（10-20名）の完全実装
- パズル型ドラフトの実装
- 矛盾制御レベル（LOW/MID/HIGH）
- 船員間の相互批評
- プレイヤーによる船員評価（逆転評価構造）
- 大潮流時のプールシャッフル
```

**船団・同盟 / Fleet & Alliance:**
```
- 船団システム
- SamePartnerDecay
- CoopSolo交互推奨
- 同盟外交易義務化
```

**止揚合成 / Synthesis:**
```
- 止揚合成システムの基本実装
- Wisdom Cardの生成
```

**毒性判定強化 / Toxicity Enhancement:**
```
- コミュニティ投票型毒性判定
- 鑑定眼重み付けの実装
- Appealフロー
```

### 目標指標 / Target Metrics
```
- IDI（思想的多様性指数）の測定開始
- 嵐発生後の回復率 > 50%
- 架け橋プレイヤー率 > 20%
```

---

## Phase 3: Expansion & Polish / 拡張と洗練
**期間 / Duration**: 2027年Q3以降（目安9ヶ月〜）

### 目標 / Goals
実験的公開を継続しながら、
論文・研究共有向けのデータ蓄積を進める。

Continue experimental publication while accumulating data
for academic papers and research sharing.

### 実装範囲 / Scope

**多海域 / Multiple Sea Areas:**
```
- 大航海時代イベントの完全実装
  （年1回の新規海域追加）
- 複数海域間の航行
```

**活動量ベース潮流 / Activity-Based Tidal Wave:**
```
- 具体的計算式の確定と実装
  （U5の解決後）
```

**高度AI判定 / Advanced AI Judgment:**
```
- ToxiGen + コミュニティ重みのハイブリッド実装
- Novelty判定の精度向上
  （U2の解決後）
```

**止揚合成強化 / Synthesis Enhancement:**
```
- 合成品質評価フローの詳細実装
  （U9の解決後）
```

**モバイル対応 / Mobile:**
```
- モバイル最適化
- Push通知の強化
```

**研究データ基盤 / Research Data:**
```
- データ分析ダッシュボード
  （エコーチェンバー打破効果の測定）
- 匿名化済み研究データの公開準備
- 論文・研究共有向けドキュメントの整備
```

### 目標指標 / Target Metrics
```
- IDI上昇率の経時変化測定
- 翻訳超越率 > 50%
- 「対話の減速」指標の測定
  （Journal送信数 / Reply送信数の比率）
- 「理解の資産化」指標
  （灯台に反対意見要約を展示するプレイヤー率）
```

---

## 未解決問題の解決スケジュール
## Open Question Resolution Schedule

各フェーズでの未解決問題への取り組み優先度。

| ID | 問題 | 目標フェーズ |
|---|---|---|
| U1 | AI船員助言の権威化 | Phase 1〜継続 |
| U2 | Novelty客観基準 | Phase 2 |
| U3 | 毒性閾値・Appealフロー | Phase 2 |
| U4 | Peer検証人数・Proxy品質 | Phase 1〜2 |
| U5 | 大潮流ActivityBased計算式 | Phase 2〜3 |
| U6 | Lighthouse固定化対策 | Phase 2〜3 |
| U7 | 評価可視化レベル | Phase 1〜2 |
| U8 | CI数値化手法 | Phase 1〜2 |
| U9 | 止揚合成品質評価 | Phase 2〜3 |
| U10 | 船団マッチング公平性 | Phase 2 |
| U11 | 高鑑定眼者権威層化 | Phase 2〜継続 |

---

## 実験的成功の定義（再掲）
## Definition of Experimental Success (Recap)

以下の状態が観測されたとき、本システムは実験的に成功したとみなす。

1. **脱・固定化**: 大潮流後もプレイヤーが異なる島を目指して航海する
2. **対話の減速**: Journalの送信数がReplyを上回る
3. **理解の資産化**: 反対意見の要約を灯台に誇りを持って展示する

詳細は [docs/METRICS.md](docs/METRICS.md) を参照。

---

*設計担当 / Designed by*: Grok (Roadmap)
*統合編集 / Integration*: Claude
