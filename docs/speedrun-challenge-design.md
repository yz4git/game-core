# Speedrun & Challenge Design

高難度・タイムアタック・スピードランを、長い待ち時間ではなく高速な学習と再試行のゲームとして設計する。

## 1. Restart latency is difficulty

失敗 → 次の意味ある入力までの時間を測る。

高難度ほど、
- death animation
- result screen
- loading
- repeated dialogue
- menu navigation
を短くする価値が高い。

難しさと待ち時間を混同しない。

## 2. Deterministic mastery surface

記録競争では特に、
- movement
- collision
- timer
- spawn rules
を再現可能にする。

変化を入れる場合は、プレイヤーが読んで適応する対象として明示する。

## 3. Fixed seed vs random seed

procedural gameではカテゴリを分けられる。

### Fixed seed
execution / routing optimization。

### Random seed
adaptation / risk management。

同じランキングへ混ぜない。

## 4. Timer integrity

ゲーム内タイマーを用意する場合、
- loading
- pause
- cutscene
- retry
を含む／含まない規則を固定する。

version変更でtimer semanticsを変えない。

## 5. Fast practice

長いゲームほど、
- checkpoint practice
- boss practice
- section select
- ghost
- replay
を用意すると上達ループが短くなる。

本番runの価値を下げずに練習コストを下げる。

## 6. Sequence breaks

想定外skipを発見しても即削除しない。

分類:
- crash / corruption
- competitive unfairness
- trivial dominant skip
- difficult expressive route
- harmless oddity

skillfulで再現可能なskipは、ゲーム文化を作る場合がある。

## 7. Route choice

最速ルートが完全一本道だと、実行精度だけの競争になる。

可能なら、
- safe vs risky
- resource vs time
- difficult shortcut
- optional power-up
を置き、routingにも判断を残す。

## 8. Low-power viability

speedrunでは強化取得を飛ばす場合がある。

skipを許すなら、低装備状態でも後半が理論上成立するか確認する。

## 9. Versioning

physics / collision / RNG変更は記録比較を壊す可能性がある。

- game version
- ruleset
- seed
をrun metadataとして保存する。

## 10. Speedrun as QA

高速プレイは、
- streaming
- trigger order
- animation cancel
- collision
- state transition
の境界を強く叩く。

通常QAとは別のstress testとして利用できる。

## Playtest

- retryまで何秒／何入力か
- 同じ入力が同じ結果になるか
- random variationを事前に読めるか
- section practiceが可能か
- shortcutがskillか単なる破綻か
- low-power routeが詰まらないか
- version/seed/timer ruleをrunから再現できるか
