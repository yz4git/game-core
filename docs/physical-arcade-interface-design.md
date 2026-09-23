# Physical Arcade Interface Design

特殊筐体・物理controller・公共空間でのプレイから、現代のtouch/controller/Webゲームへ転用できる原則をまとめる。

## 1. Controller geometry should explain the rule

特殊controllerは珍しいだけでは弱い。

強い設計では、物理操作そのものがゲーム内変数を説明する。

例となる構造:
- 傾ける -> steering
- 高低を動かす -> target height
- wheel rotation -> heading
- lever position -> throttle / altitude

初見の人が操作結果をある程度予測できることが重要。

## 2. Continuous controls need a clear neutral

stick、wheel、slider、tilt、virtual padなどは、入力ゼロが明確であること。

必要:
- self-centering または visible center
- release時の確実なzero
- calibration drift対策
- stuck inputからのrecovery

Touchでも同じで、指を離した後に残留入力を残さない。

## 3. Physical intensity is noisy

力、振り速度、gesture speed、hold durationは身体差を含む。

競技上重要な精密入力をこれだけで決める場合は、
- calibration
- wide thresholds
- alternative input
- accessibility
が必要。

表現的入力と精密な戦術入力を分けることも検討する。

## 4. Novelty must reveal mastery

特殊操作は最初の一回を引きつける。

しかし継続には、
- line choice
- timing
- efficiency
- precision
- risk control
など改善可能な技能が必要。

**Novel input earns attention; skill expression earns repetition.**

## 5. Input compatibility is not interaction equivalence

全commandを別controllerへ割り当てても、元と同じゲームになるとは限らない。

比較する:
- acquisition time
- reversal time
- continuous precision
- direction constraints
- simultaneous actions
- fatigue
- error rate

Portではbutton mappingよりsemantic interactionを保存する。

## 6. Physical feedback should expose state

Motion、haptics、seat movement、resistanceは派手さだけに使わない。

伝えられる状態:
- grip loss
- acceleration
- collision severity
- engine/load
- instability
- parry confirmation

常時振動させると情報価値が消える。

## 7. Public controls can make intent visible

大きなwheel、body lean、lever、punch motionは観客にも操作意図が見える。

公共／party gameでは、
- avatar pose
- trail
- controller animation
- exaggerated steering/braking cue
などで同じ効果を画面内へ作れる。

## 8. Spectator readability is part of onboarding

観客が、
- 誰が操作しているか
- 何を狙ったか
- 成功／失敗
- 優勢
を理解できれば、待ち時間がtutorialになる。

公共プレイではplayer UIとspectator UIを同一視しない。

## 9. Platform differentiation must survive graphics parity

家庭用機の性能向上に対して、アーケードは歴史的に
- motion cabinet
- specialized controls
- physical scale
- shared public play
- advanced hardware
などへ差別化を移してきた。

現代Web/mobileでも「高画質」だけに依存しない。

代替しにくい強み:
- instant access
- touch-native action
- link sharing
- location/social context
- fast session turnover

## 10. The fantasy and the gesture are separable

同じゲームfantasyでも複数hardwareで成立させられる。

まずsemantic actionを定義する:
- steer
- aim
- accelerate
- guard
- select target

その後でtouch/controller/keyboardごとの最適gestureを設計する。

## 11. Shared objective + visible contribution

Local co-opではteam resultだけだと個人の手応えが消える場合がある。

表示候補:
- rescues
- assists
- saves
- passes
- setup actions
- synchronized actions

個人競争がteam objectiveを壊さない範囲で貢献を可視化する。

## 12. Post-run social summary

短いmultiplayer sessionの後に、score以外の関係を返す。

例:
- synchronization
- risk sharing
- saves
- complementary roles
- distance / formation
- comeback contribution

結果画面を「終了通知」ではなく会話のきっかけにする。

## 13. Audience expansion starts at the first action

新しい客層へ広げるとき、広告だけ変えても入口のrule burdenが同じなら参加障壁は残る。

最初の操作は、
- recognizable
- immediate
- low explanation
- visibly successful
であることを優先する。

深さはその後に段階的に開く。

## 14. Cabinet ergonomics are gameplay balance

物理controllerでは、
- reach
- control spacing
- required force
- posture
- repeated motion
が難易度へ直接入る。

Touchでも、button distanceやthumb travelを単なるUI問題として扱わない。

## Production metrics

入力方式ごとに計測する:
- first-success time
- action error rate
- reversal latency
- target acquisition time
- sustained accuracy
- fatigue after 30/60 min
- spectator comprehension
- retry rate after novelty wears off

## Playtest checklist

- 初見観客が操作結果を予測できるか
- release後のneutralが明確か
- 身体差で意図しない強弱が出ないか
- 10回後にも上達対象が残るか
- 別入力方式で重要な判断が保存されるか
- haptic/motionが状態情報として機能するか
- 観客が操作意図を読めるか
- 個人貢献とteam goalが両立するか
- result screenが会話を生むか
- 30分後に疲労で操作精度が崩れないか
