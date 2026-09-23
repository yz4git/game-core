# Arcade Operations & Session Economics

アーケード史のoperator視点から、短時間ゲーム・公共プレイ・ライブ調整へ転用できる設計原則をまとめる。

## 1. Session length is a design target

長ければ良い、短ければ儲かる、のどちらでもない。

短すぎると:
- 学習前に終わる
- 不公平感
- 再挑戦理由が見えない

長すぎると:
- 待ち時間増加
- 一回で満腹
- public playの回転低下

狙うのは「一回で理解が進み、次を試したくなる長さ」。

## 2. Tune for the location

同じゲームでも、
- 初心者中心
- 熟練者中心
- bar
- family venue
- convention
で適切な初期難度は変わる。

公開場所向けbuildは家庭用の通常設定をそのまま使わない。

## 3. Attract mode is pre-play onboarding

Attract modeで見せる:
- objective
- core action
- success feedback
- score / progress

最高難度の派手なプレイだけを見せると「自分には無理」に見える場合がある。

## 4. Convert spectators into players

公共空間では観客もユーザー候補。

有効:
- short rounds
- visible score
- obvious objective
- readable motion
- fast turnover

待っている時間をルール学習時間へ変える。

## 5. Price, difficulty and duration are coupled

coin-opでは価格変更が期待価値を変え、難度がplay timeを変え、play timeがthroughputを変える。

現代でも、
- retry token
- energy
- ad
- queue
- event ticket
などの再挑戦コストがあるなら同じ構造が残る。

## 6. Operator controls = deploy-time tuning

歴史的にはoperatorが、
- difficulty
- bonus threshold
- time per coin
- pricing
- payout
を調整できた。

現代ではremote configやevent presetに相当する。

ただしルールの一貫性を壊す変数までライブ変更しない。

## 7. Every tuning knob needs telemetry

調整可能なら、結果を測る。

候補:
- median session length
- first-session survival
- retry rate
- completion
- quit point
- spectator wait
- revenue / token efficiency

変更前後を比較できないknobは運用上危険。

## 8. Attract audio is optional attention, not permanent noise

公共空間では音も集客手段だが、複数台が競合する。

- attract sound on/off
- frequency
- peak loudness
を運営側で調整できる余地を持つ。

## 9. High score is social persistence

短いセッションでもhigh scoreが残ると、前のプレイヤーが次のプレイヤーの目標になる。

オンラインランキングだけでなく、
- local daily best
- venue best
- friend best
など近い比較対象を使える。

## 10. Difficulty changes should preserve learnability

難度を上げてsessionを短縮するだけではrepeat playを壊す。

高難度でも、
- death cause
- next improvement
- reachable intermediate goal
が見えること。

## Playtest

- 初見30秒でobjectiveを説明できるか
- 一回終了後に「次は何を変えるか」が言えるか
- 観客が途中から見てscoreと優勢を理解できるか
- 2分、5分、15分の各session targetで満足度はどう変わるか
- retry costを変えたとき許容難度は変わるか
- public/demo audienceとhome audienceで成功率がどう違うか
- live-tuning変数ごとにrollback判断metricがあるか
