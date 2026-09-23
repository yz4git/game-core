# Returning Player Matchmaking Operations

長期休止ユーザーを、本人にも対戦相手にも極端な不公平を作らず再校正する。

## 1. Rating vs uncertainty

分ける:
- estimated skill
- uncertainty / confidence

inactivityで増やすのは主にuncertainty。

## 2. Faster adaptation

復帰後の数戦では、
通常より結果をratingへ強く反映できる。

弱くなっていれば下へ、
強くなっていれば上へ、
両方向へ速く動く。

## 3. Warm-up

Ranked前に任意で、
- training
- bot
- unranked
- control recap
を提示する。

再学習とrating再推定を分ける。

## 4. Do not hard-code decay assumptions

休止期間だけでratingを機械的に大幅減少させない。

類似ゲームでskillを維持している可能性がある。

## 5. Opponent fairness

Returner本人だけを見ると危険。

対戦相手側の、
- stomp rate
- predicted win probability
- quit/rematch
も追う。

## 6. Abuse resistance

休止で簡単な相手に当たりやすくなるなら悪用可能。

直接rating低下よりuncertainty increaseの方が悪用余地を抑えやすい。

## 7. Groups

復帰者が現役友人とpartyを組む場合、
skill spreadが大きくなる。

casual / unranked / wide groupingなどの再合流経路を用意する。

## 8. Season interaction

分離する:
- visible rank reset
- rewards
- MMR
- uncertainty

毎season全skill memoryを消さない。

## 9. Return telemetry

minimum:
- first 10 games win rate
- opponent MMR
- rating delta
- uncertainty delta
- quit rate
- queue time

通常player cohortと比較する。

## 10. Exit condition

数試合後、
- match quality
- rating confidence
が通常ユーザー帯へ戻ればreturner modeを終了する。

## Checklist

- inactivityでuncertaintyが増えるか
- 強弱どちらへも速く再校正できるか
- opponent側を監視しているか
- abuse pathがないか
- season resetとMMRを分離しているか
