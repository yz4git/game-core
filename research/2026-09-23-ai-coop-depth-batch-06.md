# AI, Co-op, and Layered Depth Batch 06 — 2026-09-23

## Scope

今回のバッチでは、1980年代後半〜1990年代前半のゲーム誌・業界資料から、初心者向け入口と長期的な深さ、CPU AI、公平感、非対称バランス、協力プレイの参加摩擦を抽象化した。

原文の転載・近接要約ではなく、現代のゲーム制作へ再利用できる仕組みだけを保存する。

## Sources

- Computer Gaming World, Issue 58, April 1989
- Computer Gaming World, Issue 97, August 1992
- Computer Gaming World, Issue 100, November 1992
- Gaming Alexandria — Video Game Sales: 1972–1999
  https://www.gamingalexandria.com/wp/2021/06/video-game-sales-1972-1999/
- Gaming Alexandria — Technopolis complete archive context
  https://www.gamingalexandria.com/wp/2025/09/technopolis-every-issue-now-scanned/

## 1. Beginner accessibility and depth are not opposites

### Observation
当時のスポーツゲーム批評では、すぐ遊べる簡易モードと、編成・戦術・詳細設定まで扱えるモードを同じ作品内に持つ設計が評価されている。

### Mechanism
初回プレイヤーは認知負荷を抑えてゲームの核へ触れられ、興味を持ったプレイヤーだけが奥のシステムへ進める。

### Generalized Principle
**深いゲームを初心者向けに薄くするのではなく、深さを段階的に開示する。**

### Transfer
- RPG: 自動装備 → 手動ビルド
- Racing: 基本アシスト → 詳細セットアップ
- Fighting: 基本コンボ → 高度キャンセル
- Strategy: 推奨編成 → 詳細指揮

---

## 2. AI is architecture, not polish

### Observation
ゲームAIに関する当時の開発者議論では、AIをベータ段階以降に追加すると根本構造が弱くなることが指摘されていた。

### Mechanism
AIが判断するには、ゲーム状態が適切なデータとして設計されている必要がある。後付けでは必要情報や関係がデータ構造に存在しない場合がある。

### Generalized Principle
**CPU対戦が重要なら、AIが何を見るかをルール・データ構造と同時に設計する。**

---

## 3. Predictable AI and random AI are both weak extremes

### Observation
同じ状況へ固定反応するCPUは攻略されやすい。一方、完全ランダムでは知的に見えず、プレイヤーも学習できない。

### Mechanism
状況に応じて妥当な選択肢集合を作り、その中で重み付きの変化を持たせると、傾向を学びつつ決め打ちを防げる。

### Generalized Principle
**AIの変化は「理由のある候補行動」から作る。**

---

## 4. Fairness is perceived, not only mathematical

### Observation
ゲームバランスの議論では、人間とCPUが完全に同条件である必要はなく、プレイヤーが公平だと感じられるかが重要な問題として扱われている。

### Mechanism
プレイヤーは内部数値ではなく、自分が観測できる因果関係から公平性を判断する。

### Generalized Principle
**勝率だけでなく、敗北理由をプレイヤーが納得して説明できるかを測る。**

---

## 5. Hidden AI advantages require caution

CPUだけが人間より多くの情報を使うと、強くはなるが「ズル」に見えやすい。

### Better alternatives
- 意思決定品質を上げる
- 候補手を改善する
- 位置評価を改善する
- 記憶を持たせる
- 非対称勝利条件にする

### Principle
**難易度向上を不可視チートへ依存させない。**

---

## 6. Asymmetry can be balanced through objectives

開始資源や能力を完全に同じにせず、役割に応じて勝利条件・時間・得点基準を変えることで成立するゲームがある。

### Principle
**非対称性を消すのではなく、それぞれの強みが価値になる評価条件を作る。**

---

## 7. Drop-in/drop-out is a design advantage

Gaming Alexandriaのアーケード市場史では、1980年代後半に同時協力プレイや途中参加型のゲームが、限られた設置環境でも支持された流れが整理されている。

### Mechanism
見ている人がそのまま参加者になりやすく、遊ぶための約束や準備が小さい。

### Modern transfer
- フレンドが途中参加
- 離脱してもAI代行
- 再参加で状態復帰
- ロビー待ちを短縮

### Principle
**協力ゲームの入口は、ゲーム本編より難しくしない。**

---

## 8. Co-op needs interdependence, not health scaling

人数に合わせて敵HPを増やすだけでは、協力の意味が弱い。

### Better co-op decisions
- カバー
- 救助
- ターゲット分担
- 資源共有
- 位置連携
- 一時的な役割交代

### Principle
**味方の状態を読むこと自体をゲーム判断へする。**

---

## 9. Spectacle can attract, depth retains

アーケード市場では大型筐体・光線銃・体感装置など視覚的に強い入口も重要だったが、長期的に支持されるゲームでは操作・協力・技術習得も重要だった。

### Principle
プレイヤー導線を三段にする。

1. 見てやりたくなる
2. 触って楽しい
3. 続けるほど深くなる

---

## 10. AI exploit hunting is a dedicated test

通常プレイだけではAIの固定反応や盲点が見つからない。

### Exploit attempts
- 同じフェイント
- 端で待つ
- 遠距離固定
- 障害物越し
- ターゲット切替連打
- 後退し続ける
- 高低差利用

### Principle
**CPUテストでは勝つのではなく、壊す方法を探すセッションを別に持つ。**

## Repository promotions from this batch

- Core Principles 63–72
- Opponent AI & Perceived Balance guide
- Layered Accessibility & Depth guide
- Playtest AI/co-op audits
- Strategy AI / Sports / Co-op genre heuristics
