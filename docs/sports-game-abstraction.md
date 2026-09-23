# Sports Game Abstraction

実競技の全動作を再現するのではなく、競技らしい判断・位置・時間・チーム意図をゲーム操作へ圧縮する。

## 1. Preserve the decision loop
実競技の中心判断（space creation / timing / passing lane / commitment risk / matchup / positioning）を先に定義する。身体動作の再現度より、これらがプレイヤー判断として残ることを優先する。

## 2. Abstraction is not simplification of meaning
ボタン数を減らしても、結果が位置・速度・味方・相手・タイミングで変われば深さは残る。

## 3. Camera and controls are coupled
カメラ方向はstick/pass/player-switch/defensive positioningのmental modelを変える。Alternate cameraは操作系として再テストする。

## 4. Team AI first
優先順は team objective → formation/spacing → assignment/role → local movement → animation polish。個体が自然でもチーム意図に反すれば不自然になる。

## 5. Off-ball behavior is gameplay
Space creation、mark、support angle、runはボール保持者の選択肢を変える。接触・得点・possessがなくても、defender displacementやlane openingはAI contributionとして記録する。

## 6. Roles are behavioral contracts
Roleは能力値ラベルではなく、positioning・risk・target choice・support behaviorの予測可能な契約にする。名前を隠しても行動からroleを推測できる状態を目標にする。

## 7. Relational spatial reasoning
Nearest targetだけでなくopen angle、support distance、congestion、cover、escape lane、opponent relationをAI stateへ入れる。チームAIは点の集合ではなく関係として空間を読む。

## 8. Fast reaction, slow intent
Local adjustmentは高頻度でも、run/cover/assignment/target intentにはhysteresisやminimum commitmentを持たせる。賢さを上げて小刻みな方針転換を増やさない。

## 9. Anticipatory support
味方はcommand後に動き始めるだけでなく、probable next stateへ準備する。必要になった瞬間にsupport positionへ到着していることを評価する。

## 10. Contextual imperfection
常にperfect reception/controlにすると、その前のpositioningやpressureが無意味になる場合がある。失敗をrandomにするのでなく、speed/angle/pressure/preparationへ因果的に結びつける。

## 11. Tactical assistance preserves agency
Recommended tacticはAIに自動実行させるだけでなく、理由と予想効果をplayerへ見せて選択可能にする。拒否して別戦術を取れることを残す。

## 12. Behavioral team identity
Team/faction差はheatmap、spacing、risk、run frequency、pressing、role distributionなど行動分布で検証する。名前やartを隠したblind testも使う。

## 13. Player switching is AI design
Switch候補はnearestだけでなくplay direction、threat、intended receiver、assignmentを考慮する。自律AIとcontrol transferが同じteam-intent modelを共有する。

## 14. Macro invariants before micro polish
Automated QAでclustering、uncovered critical zones、assignment duplication、isolated agent、formation breakを先に検出する。個々のanimationが自然でもteam shapeが壊れていれば失敗。

## 15. Counterfactual AI tests
固定game stateから一人のposition/role/pressureだけを変えて再実行し、option qualityやoutcome deltaを比較する。Win rateだけでなく「近傍により良い判断があったか」を調べる。

## 16. Telemetry
- useful option created
- support angle / lane openness
- spacing histogram / congestion heatmap
- assignment duplication
- uncovered-zone time
- action cancellation before value
- off-ball outcome: receive / lane open / defender displaced / no effect
- switch prediction error
- tactical suggestion accepted/rejected
- team role/action distribution

## Playtest
- placeholder artでも競技らしい判断が残るか
- AI teamの意図を一文で説明できるか
- off-ball teammateが選択肢を増やすか
- roleを行動から推測できるか
- AIが有効なrunを途中キャンセルしていないか
- player switchingを事前予測できるか
- names/artを隠してteam styleを区別できるか
- 一人のpositionを変えるcounterfactualでoption qualityがどう変化するか
- novice向けsuggestionがagencyを奪わないか
- advanced playerに追加の戦術判断が残るか
