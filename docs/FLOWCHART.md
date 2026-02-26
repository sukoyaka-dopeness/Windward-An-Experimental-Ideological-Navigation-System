# FLOWCHART.md
# Windward — Player Experience Flow
# プレイヤー体験フロー図

Version: v0.2
Author: Copilot + ChatGPT (Flow Design)
Integration: Claude

---

## 0. 凡例 / Legend
```
[ ]  = アクション・状態 / Action or State
{ }  = 分岐 / Branch
→   = フロー / Flow
↓   = 継続 / Continue
```

---

## 1. Core Loop / コアループ
```mermaid
flowchart TD
    A[Start Voyage / 航海開始] --> B[Move Across Sea / 海域を移動]
    B --> C[Reach Island / 島に到着]
    C --> D[Read Island Log / 島の日誌を読む]
    D --> E[Vice-Captains Present Drafts / 副船長たちがドラフトを提示]
    E --> F[Player Writes Summary / プレイヤーが要約を記述]
    F --> G{Dual Verification / 双方検証}
    G -->|Both Approve / 双方承認| H[Full Reward / フル報酬]
    G -->|One Approves / 片側承認| I[Half Reward / 半報酬]
    G -->|Both Reject / 双方拒否| J[No Reward + Morale↓ / 報酬なし＋士気低下]
    H --> K[Route Opens + Wind Shifts / 航路開通＋風向変化]
    I --> K
    J --> L[Adjust Route / 航路を見直す]
    K --> M{Crew Morale Check / 船員士気確認}
    L --> M
    M -->|Low / 低| N[Mutiny Risk↑ / 暴動リスク上昇]
    M -->|High / 高| O[Bonus Route Unlocked / ボーナス航路解放]
    N --> P[Forced Return / 強制帰港]
    O --> Q[Explore Further / さらに探索]
    P --> R[Home Island / 自分の島へ]
    Q --> R
    R --> S{Tidal Wave? / 大潮流？}
    S -->|No / なし| A
    S -->|Yes / あり| T[Map Reconfiguration / 地図再配置]
    T --> A
```

---

## 2. Dual Verification Flow / 双方検証フロー
```mermaid
flowchart TD
    A[Player A writes summary of Island B / プレイヤーAがIsland Bを要約] --> B{Island B confirms? / Island Bが承認？}
    B -->|Reject / 拒否| C{Retry count < 3? / リトライ3回未満？}
    C -->|Yes / はい| A
    C -->|No / いいえ| D[No Reward / 報酬なし]
    B -->|Timeout 72h / タイムアウト| E[Lighthouse Proxy AI responds / 灯台ProxyAIが代理応答]
    E --> F[Tentative Approval / 暫定承認]
    F --> G[Human Re-evaluation on Return / 島主復帰時に再評価]
    B -->|Approve / 承認| H[Island B writes summary of A / Island BがAを要約]
    H --> I{Player A confirms? / プレイヤーAが承認？}
    I -->|Reject / 拒否| J[Half Reward / 半報酬]
    I -->|Approve / 承認| K[Verification Complete / 検証完了]
    K --> L[Full Reward + Route Opens / フル報酬＋航路開通]
```

---

## 3. AI Vice-Captain Flow / AI副船長フロー
```mermaid
flowchart TD
    A[Player requests help / プレイヤーが補助を要求] --> B[Three Vice-Captains generate drafts / 三人の副船長がドラフトを生成]
    B --> C[Compass: Logic focus / 羅針盤：論理重視]
    B --> D[Journal: Emotion focus / 航海日誌：感情重視]
    B --> E[Chart: Overview focus / 海図：俯瞰重視]
    C --> F{Contradiction detected? / 矛盾あり？}
    D --> F
    E --> F
    F -->|Yes / あり| G[Notify Player: Captains disagree / 副船長たちの意見が分かれています]
    F -->|No / なし| H[Present drafts with confidence level / 確信度付きでドラフトを提示]
    G --> H
    H --> I[Player edits or ignores / プレイヤーが編集または無視]
    I --> J{Player surpasses all drafts? / 全ドラフトを超えた？}
    J -->|Full Surpass / 完全超越| K[Maximum Bonus / 最大ボーナス]
    J -->|Partial Surpass / 部分超越| L[Partial Bonus / 部分ボーナス]
    J -->|No Surpass / 超越なし| M[Normal Score / 通常スコア]
    J -->|Copy detected / コピー検出| N[No Bonus + Crew dissatisfied / ボーナスなし＋船員不満]
```

---

## 4. Toxicity / Storm Flow / 毒性・嵐フロー
```mermaid
flowchart TD
    A[Community Reports / コミュニティ報告] --> B{Reports ≥ Threshold? / 報告数が閾値以上？}
    B -->|No / 未満| C[Continue / 継続]
    B -->|Yes / 以上| D{Severity Level? / 深刻度？}
    D -->|L1 Mild / 軽微| E[Visibility↓ / 視界低下]
    D -->|L2 Moderate / 中程度| F[Cursed Map + Decryption Quest / 呪われた地図＋解読クエスト]
    D -->|L3 Severe / 深刻| G[Area Weather Degrades / 周辺海域の環境悪化]
    D -->|Illegal / 違法| H[Immediate Deletion / 即時削除]
    E --> I[Cooldown Period / 冷却期間]
    F --> I
    G --> I
    I --> J[Storm Analysis Quest delivered / 嵐解析クエスト配信]
    J --> K{Quest completed? / クエスト完了？}
    K -->|Yes / はい| L[Restore + Recovery Bonus / 回復＋回復ボーナス]
    K -->|No / いいえ| M[Conditions remain / 状態継続]
```

---

## 5. Tidal Wave Flow / 大潮流フロー
```mermaid
flowchart TD
    A{Cycle Triggered? / 周期到来？} -->|小潮流 Monthly| B[Minor Reset / 軽微リセット]
    A -->|大潮流 3-6mo| C[Pre-announcement 2 weeks / 2週間前告知]
    A -->|大航海時代 Annual| D[New Sea Area Added / 新海域追加]
    B --> E[Unverified routes reset / 未検証航路リセット]
    B --> F[Partial resource reset / 資源軽微リセット]
    C --> G[Trade Boom Event / 交易ブームイベント]
    G --> H[Map Reconfiguration / マップ再配置]
    H --> I[Alliance Expiry Reset / 同盟期限リセット]
    I --> J{What is preserved? / 保全されるもの}
    J --> K[Verified Routes / 検証済み航路]
    J --> L[Lighthouse / 灯台]
    J --> M[Appraisal Eye / 鑑定眼]
    J --> N[Logs & Badges / ログ・バッジ]
    D --> O[Expansion only / 拡張のみ・喪失なし]
    O --> P[New fog areas appear / 新たな霧の海域出現]
```

---

## 6. Re-Observation Flow / 再観測フロー
```mermaid
flowchart TD
    A[Time Elapsed / 一定期間経過] --> B[Random Player Pool Selected / 無作為プレイヤー抽出]
    B --> C[Re-read Log / ログを再読]
    C --> D[Submit fixed responses / 定型応答を提出]
    D --> E{Understood? / 理解できたか？ Y/N}
    D --> F{Perspective shifted? / 視点が動いたか？ Y/N}
    D --> G{Reconsidered? / 再考したか？ Y/N}
    E --> H[Aggregate as moving average / 移動平均としてログ蓄積]
    F --> H
    G --> H
    H --> I[No ranking generated / ランキング生成なし]
    I --> J[Environmental feedback only / 環境フィードバックのみ]
```

---

## 7. Async Player Flow / 非同期プレイヤーフロー
```mermaid
flowchart TD
    A[Submit Verification / 検証を提出] --> B[Auto-return to Home Island / 自動帰港]
    B --> C[Home Island Activities / 自島での活動]
    C --> D[Resource Management / 資源管理]
    C --> E[Solo Exploration / ソロ探索]
    C --> F[Journal Writing / 日誌整理]
    C --> G[Lighthouse Update / 灯台更新]
    D --> H{Push Notification? / プッシュ通知？}
    E --> H
    F --> H
    G --> H
    H -->|Received / 受信| I[Return to Active Voyage / 航海再開]
    H -->|Not yet / 未着| C
    I --> J{Result? / 結果は？}
    J -->|Approved / 承認| K[Reward + Next Island / 報酬＋次の島へ]
    J -->|Rejected / 拒否| L[Revise Summary / 要約を修正]
    J -->|Proxy Response / 代理応答| M[Tentative + Re-evaluate later / 暫定＋後日再評価]
```

---

## 8. New Island Discovery Flow / 新大陸発見フロー
```mermaid
flowchart TD
    A[Player deposits thought at Lighthouse / 灯台に思想を預ける] --> B[AI calculates cluster novelty / AIがクラスタ新規性を計算]
    B --> C{Outside existing clusters? / 既存クラスタの外？}
    C -->|No / いいえ| D[Assigned to nearest cluster / 最近傍クラスタに配属]
    C -->|Yes / はい| E[Tentative New Island Badge / 暫定新大陸バッジ付与]
    E --> F[Peer Validation Period / Peer検証期間]
    F --> G[Multiple independent players confirm / 複数の独立プレイヤーが承認]
    G --> H{Sufficient confirmations? / 確認数十分？}
    H -->|No / いいえ| I[Remain tentative / 暫定のまま]
    H -->|Yes / はい| J[New Island Confirmed / 新大陸確定]
    J --> K[Permanent Discovery Badge / 永続発見者バッジ]
    J --> L[Delayed Reward Released / 遅延報酬解放]
    J --> M[Island appears on map / 地図に島が出現]
```

---

*設計担当 / Designed by*: Copilot + ChatGPT (Flow Design)
*統合編集 / Integration*: Claude
