# FAQ.md
# Windward — よくある質問
# Frequently Asked Questions

Version: v0.2
Author: Grok (FAQ)
Integration: Claude

---

## Q1. このゲームは何をするゲームですか？
## What kind of game is this?

**A.**
帆船で未知の海を航海し、異なる意見を持つ島を訪れて
「特産物」（独自の視点）を交易するゲームです。

深層では、自分の意見の盲点を埋め、
他者の思考を「理解する技術」を磨き、
立場が自然に変化していく体験を提供します。

A sailing game where you navigate unknown seas and visit islands
with different opinions to trade "special goods" (unique perspectives).

At a deeper level, it provides an experience of filling blind spots
in your own opinions, refining the skill of understanding others' thinking,
and having your own position naturally shift.

---

## Q2. これはSNSや議論アプリの代替ですか？
## Is this a replacement for social media or debate apps?

**A.**
違います。

- SNSではありません
- 議論アプリではありません
- 最適化や勝敗を競うゲームではありません

**これは実験的思想シミュレーターです。**

他者を論破することではなく、
「他者を本当に理解する体験」を与えることを優先しています。

No.

- Not a social network
- Not a debate platform
- Not a competitive game

**This is an Experimental Ideological Simulator.**

It prioritizes giving you the experience of truly understanding others,
not defeating them in argument.

---

## Q3. 政治的な議論や意見対立が起きるのでは？
## Won't this cause political arguments and ideological conflict?

**A.**
架空の島・意見として抽象化しているため、
現実の政治・イデオロギー対立を直接扱いません。

攻撃的な表現は「嵐」「海賊」として構造的に抑止され、
理解・翻訳が報酬の中心です。

対立を「悪」として裁くのではなく、
航海に必要な「風」や「波」として扱います。

Because opinions are abstracted as fictional islands,
the game does not directly handle real political or ideological conflicts.

Aggressive expressions are structurally suppressed as "storms" and "pirates,"
with understanding and translation at the center of rewards.

Conflict is not judged as "evil" but treated as the "wind" and "waves"
necessary for navigation.

---

## Q4. 毒性判定や評価が怖くてプレイしづらいのでは？
## Won't toxicity judgment and evaluation make it intimidating to play?

**A.**
以下の緩衝設計を採用しています。

- **練習港海域**: 初心者はペナルティが完全に無効
- **初期ニュートラルスコア**: 鑑定眼の初期変動幅は小さく設定
- **OptOutEval**: 評価システムから一時的に離脱できるオプション
- **SoftFeedback**: 数値ではなく「曇り」などの自然現象で表現
- **自然発生型チュートリアル**: ルールを説明されることなく、体験の中で徐々に発見できる

The following buffer designs are adopted:

- **Practice Harbor**: Penalties are completely disabled for beginners
- **Initial Neutral Score**: Initial appraisal eye score variance is small
- **OptOutEval**: Option to temporarily withdraw from the evaluation system
- **SoftFeedback**: Expressed as natural phenomena like "cloudy" rather than numbers
- **Organic Tutorial**: Rules are discovered gradually through experience,
  not explained upfront

---

## Q5. 非同期で返事が来ないと詰まるのでは？
## Won't I get stuck if I don't receive async replies?

**A.**
返事待ちの間も以下の活動ができます。

- 自分の島での資源管理
- ソロ探索（新しい島の発見）
- 航海日誌の整理
- 灯台の更新

72時間無応答の場合は **Lighthouse Proxy AI** が代理応答し、
ゲームの進行を維持します。
島主が復帰した際には人間による再評価も可能です。

During the wait, you can:

- Manage resources on your home island
- Solo exploration (discovering new islands)
- Organize your ship's log
- Update your lighthouse

After 72 hours without a response, the **Lighthouse Proxy AI**
generates a provisional response to keep the game progressing.
Human re-evaluation is also available when the island owner returns.

---

## Q6. 大潮流で全部リセットされるのでは？
## Will the Great Current reset everything?

**A.**
**保全されるもの（失われない）:**
- 双方検証済みの航路
- 灯台に預けた思想
- 鑑定眼スコア
- 航海日誌・ログ
- 発見者バッジ

**流されるもの:**
- 未検証の暫定航路
- 資源の一部
- 同盟の有効期限
- 島の相対的な位置関係

大潮流の2週間前から告知され、
直前には交易ブームイベントが発生します。
「理解した内容は失われない」設計です。

**What is preserved (never lost):**
- Dual-verified routes
- Thoughts deposited at the lighthouse
- Appraisal eye score
- Ship's log and records
- Discovery badges

**What is swept away:**
- Unverified provisional routes
- Partial resources
- Alliance expiry
- Relative island positions

The Great Current is announced 2 weeks in advance,
with a trade boom event occurring just before it.
The design ensures that "what you have understood is never lost."

---

## Q7. AIが正解を教えてくれるのでは？
## Won't AI just tell me the correct answer?

**A.**
Windward の船員助言システムは**意図的に不完全**に設計されています。

- 10〜20名の仮想船員プールから毎回3名がランダムに選ばれる
- 3名はそれぞれ異なる視点（論理・感情・俯瞰）を担当し、
  意図的な欠損を持ったドラフトを提示する
- 3者の解釈が互いに矛盾することもある
- プレイヤーが3つのドラフトを「素材」として組み合わせることで
  初めて高品質な理解に到達できる

AIは「正解」を持ちません。正解を生成しません。
**AIは測量士であり、審判ではありません。**

Windward's crew advisory system is **intentionally imperfect**.

- 3 crew members are randomly selected each voyage from a pool of 10-20
- Each presents a draft with intentional gaps from different perspectives
  (logic, emotion, overview) that sometimes contradict each other
- Players reach high-quality understanding by combining all three drafts
  as raw materials

AI does not hold the correct answer. AI does not generate it.
**AI is a surveyor, not a judge.**

---

## Q8. 鑑定眼スコアとは何ですか？
## What is the Appraisal Eye score?

**A.**
鑑定眼は「他者の視点を正確に再現できた能力の蓄積」です。

- 数値スコアはプレイヤーに表示されません
- 「あなたは遠い島の言葉を再現できるようになってきた」
  といった物語的フィードバックで表現されます
- 効果は「報酬倍率の上昇」ではなく「到達できる島の範囲の拡張」です
- 強くなるのではなく、「風を読める範囲」が広がります

The Appraisal Eye is "an accumulation of the ability to accurately
reproduce others' perspectives."

- The numerical score is not displayed to players
- Expressed through narrative feedback such as
  "You are becoming able to reproduce the words of distant islands"
- Its effect is not "increased reward multiplier" but
  "expansion of islands you can reach"
- You don't become stronger — your "range of readable wind" expands

---

## Q9. プレイヤーのデータはどう扱われますか？
## How is player data handled?

**A.**
詳細は [PRIVACY_AND_ETHICS_POLICY.md](docs/PRIVACY_AND_ETHICS_POLICY.md) を参照してください。

要点:
- 日誌原文（Raw Log）は暗号化分離保存
- ベクトルデータは原文復元不能な形式で保存
- 商用再学習・第三者提供には使用しない
- いつでも削除・撤回できる
- **思想の所有権は常にプレイヤーにある**

For details, see [PRIVACY_AND_ETHICS_POLICY.md](docs/PRIVACY_AND_ETHICS_POLICY.md).

Key points:
- Raw logs are encrypted and stored separately
- Vector data is stored in a format that cannot reconstruct the original text
- Not used for commercial retraining or third-party provision
- Can be deleted or withdrawn at any time
- **The ownership of thought always belongs to the player**

---

## Q10. プロジェクトに参加・貢献できますか？
## Can I participate in or contribute to the project?

**A.**
はい。このプロジェクトはオープンな思想実験として公開されています。

→ [CONTRIBUTING.md](CONTRIBUTING.md) を参照してください。

Issueの報告には `.github/ISSUE_TEMPLATE/issue_report.md` を、
Pull Requestには `.github/PULL_REQUEST_TEMPLATE/pull_request.md` を使用してください。

Yes. This project is published as an open ideological experiment.

→ See [CONTRIBUTING.md](CONTRIBUTING.md).

Please use `.github/ISSUE_TEMPLATE/issue_report.md` for issue reports
and `.github/PULL_REQUEST_TEMPLATE/pull_request.md` for pull requests.

---

## Q11. なぜ5つのAIが協働して設計したのですか？
## Why did five AIs collaborate on the design?

**A.**
このプロジェクト自体が、異なる「知性の意見パーツ」を集めて統合すると
より良い設計に近づくというゲームのテーマの実証です。

- **Gemini**: 世界観・物語・設計哲学・評価指標
- **ChatGPT**: システム設計・倫理ポリシー・フローチャート
- **Copilot**: 内部メカニクス・技術仕様・GitHubテンプレート
- **Grok**: リスク分析・FAQ・ロードマップ・ライセンス
- **Claude**: プロンプト設計・用語集・貢献ガイド・全体統合

5者はそれぞれ**構造・実用・認知・体験・統合**という
異なるレイヤーを得意としており、競合ではなく補完関係にあります。

This project itself is a demonstration of the game's theme:
collecting and integrating "opinion parts from different intelligences"
leads to better design.

- **Gemini**: World-building, narrative, design philosophy, metrics
- **ChatGPT**: System design, ethics policy, flowcharts
- **Copilot**: Internal mechanics, technical specs, GitHub templates
- **Grok**: Risk analysis, FAQ, roadmap, license
- **Claude**: Prompt engineering, glossary, contributing guide, integration

The five specialize in different layers — **structure, practicality,
cognition, experience, and integration** — complementing rather than competing.

---

*設計担当 / Designed by*: Grok (FAQ)
*統合編集 / Integration*: Claude
