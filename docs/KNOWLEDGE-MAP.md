# Knowledge Map

game-core の知識を、プレイヤー体験が成立する順序で整理した地図。

## 1. Input — 意図を正しく受け取る
入力遅延、誤操作、タッチ領域、同時入力、キャリブレーション。

→ [Touch & Controller Ergonomics](touch-controller-ergonomics.md)  
→ [Input Calibration & Diagnostics](input-calibration-and-diagnostics.md)

## 2. Feedback — 入力と結果を理解させる
視覚、音、振動、ヒット反応、危険度の文法。

→ [Audio as Gameplay](audio-as-gameplay.md)  
→ [Core Principles](core-principles.md)

## 3. Information — 状況を読ませる
カメラ、UI、テレグラフ、目的、優先順位。

→ [Camera & Targeting](camera-and-targeting.md)  
→ [Strategy UI & Information](strategy-ui-information.md)  
→ [Encounter & Camera Design](encounter-and-camera-design.md)

## 4. Decision — 選択を作る
距離、タイミング、資源、ルート、対象、リスクと報酬。

→ [Core Principles](core-principles.md)  
→ [Genre Heuristics](genre-heuristics.md)

## 5. Challenge — 理解したルールを組み合わせる
敵、AI、地形、時間、複数脅威、難易度。

→ [Opponent AI & Balance](opponent-ai-and-balance.md)  
→ [Layered Accessibility & Depth](layered-accessibility-and-depth.md)

## 6. Failure — 失敗を次の情報にする
死因、再挑戦、損失量、セーブ、復帰。

→ [Save & Failure Design](save-and-failure-design.md)  
→ [Playtest Review](playtest-review.md)

## 7. Learning — 予測可能にする
教える→試す→ひねる、規則性、フィードバック、再確認。

→ [Teaching & Documentation](teaching-and-documentation.md)

## 8. Mastery — 上達で別の遊びを見せる
効率、スコア、別解、リスクの取り方、キャラクター差。

→ [Core Principles](core-principles.md)  
→ 各 [Genre Index](GENRE-INDEX.md)

## 9. Replay / Variation — 同じ理解を別状況で試す
自動生成、ランダム性、別ルート、リプレイ、ランキング。

→ [Procedural Generation Quality](procedural-generation-quality.md)  
→ [Replay, Spectator & Telemetry](replay-spectator-telemetry.md)

## 10. Community / Longevity — ゲーム外へ知識を拡張する
攻略共有、UGC、復帰、観戦、メタゲーム。

→ [Community, UGC & Metagame](community-ugc-metagame.md)  
→ [Long-Term Comeback Design](long-term-comeback-design.md)

## 診断ルール
後段の問題を直す前に前段を確認する。

たとえば「ボスが面白くない」とき、技を追加する前に Input → Feedback → Information が壊れていないかを見る。「自動生成が単調」なら生成種類を増やす前に Decision の種類が本当に増えているかを見る。

症状から直接探す場合は [Problem Index](PROBLEM-INDEX.md) を使う。
