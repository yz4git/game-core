# Adaptive Touch Ergonomics

## Goal

タッチUIを固定ゲームパッドの模写ではなく、device・hand・posture・session durationへ適応できる入力systemとして設計する。ただし適応でmotor memoryを壊さない。

## Ergonomic priority

各actionへ概算priorityを付ける:

`ergonomic priority = frequency × urgency × precision × simultaneous-use pressure`

高いactionほど自然なthumb位置、大きなhit region、短いacquisition distanceを与える。

## Reachability field

画面を単純な左右領域として扱わず、device size / safe area / selected handedness / gripごとのreach cost mapとして考える。

実装では複数anchorを持ち、control roleごとに候補位置を解く。

## Handedness

左右presetはgeometryの単純mirrorではない。

維持するもの:
- move / camera / primary / secondaryというsemantic role
- world/HUD readability
- simultaneous-action requirements

再最適化するもの:
- x/y position
- spacing
- scale
- capture region

## Dynamic controls

Floating stick等はtouch-down近辺へ出せるが:
- capture regionを限定
- safe-areaへclamp
- neutral/dead zoneを固定
- 最大移動量を制限
- session中に勝手に漂わせない

適応性とpredictabilityを両立する。

## Hit geometry ≠ visual geometry

Iconを大きくせずhit targetだけ拡張できる。

Debug modeではactual hit region、overlap、priority resolutionを表示する。

## Occlusion

Finger footprintをUI layoutの一部として扱う。

Critical telegraph、target、reticle、small textをpersistent thumb zoneへ置かない。必要なら入力地点からvisual confirmationを外側へ逃がす。

## Press confidence

押下確認は指の下だけで完結させない:
- outer glow/ring
- nearby marker
- world reticle response
- short sound
- haptic

## Function merging

空間button数を減らすときはdecisionを削らず、関連actionをまとめる。

例:
- tap / hold
- magnitude walk / run
- direct object tap instead of select button

誤認識costが高いactionには使わない。

## Haptic budget

Hapticをイベント数で埋めない。

優先候補:
- parry/guard confirmation
- collision
- lock acquisition
- grip loss
- high-priority warning

記録する:
- haptic events/minute
- pattern confusion
- intensity preference
- long-session discomfort

必ずOFF/弱化時にもゲーム情報が失われないようにする。

## Long-session / thermal QA

最低でも短時間testと30–60分testを分ける。

見るもの:
- miss rate delta
- grip reposition count
- repeated long reaches
- thumb travel
- device heat perception
- sustained-performance degradation
- haptic fatigue

## Cross-input semantic equivalence

Touch/controller/keyboardで同じbutton mapを要求しない。

比較する:
- target acquisition time
- correction time
- simultaneous actions
- precision
- local response
- attention diversion
- fatigue
- preserved tactical choices

重要なdecision bandwidthが同等なら、gestureは異なってよい。

## Input profile

一つのprofile layerへ統合する候補:
- handedness
- scale
- spacing
- position
- fixed/floating stick
- sensitivity/dead zone
- hold/toggle
- remap
- haptic intensity/off
- visual input feedback

## Playtest checklist

- 頻繁なactionが最短reachにあるか
- 大型端末でmiss率が増えないか
- left/right presetがrole confusionを生まないか
- dynamic stickがmotor memoryを壊さないか
- 指が危険telegraphを隠していないか
- hit region拡張で誤入力が増えていないか
- press confirmationが指の外から見えるか
- hapticが30分後も意味を区別できるか
- deviceが温まった後もlayoutが快適か
- touch版だけ重要な同時入力を失っていないか
