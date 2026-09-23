# Touch & Controller Ergonomics

タッチ操作を「画面上のゲームパッド」ではなく、別の入力媒体として設計する。

## 1. Preserve decisions, not buttons

移植で守るのはボタン配置ではなく、
- aim
- dodge choice
- route choice
- acceleration
- timing
などの意思決定。

必要なら入力方法は大きく変える。

## 2. Directness

タッチの強み:
- objectを直接触れる
- locationを直接指定できる
- multiple fingers
- gesture

対象を触る方が自然なら、virtual cursorを挟まない。

## 3. No tactile landmarks

物理ボタンのような縁や反発がないため、小さい固定ボタンは視線を奪いやすい。

対策:
- oversized zones
- whole-screen regions
- dynamic joystick
- generous hit areas

## 4. Finger occlusion

入力中に重要情報を隠さない。

考慮:
- thumb footprint
- hand posture
- device size
- landscape / portrait

## 5. Invisible controls need feedback

透明領域を使う場合、
- helper arrow
- brief joystick ring
- direction trail
などで入力状態を確認できるoptionを用意する。

## 6. Context-sensitive input

同じgestureでも状況で安全に意味を変えられるなら、ボタン数を減らせる。

ただし予測不能なcontext switchingは避ける。

## 7. One-hand vs two-hand

片手:
- reachability
- large regions
- lower precision

両手:
- simultaneous actions
- stable grip
- thumb zones

最初から対象姿勢を決める。

## 8. High-skill touch

「mobileだから簡単にする」必要はない。

精密で高速な操作でも、
- direct touch
- large zones
- multi-touch
を使えば複雑な判断を維持できる。

## 9. Optional controller support

タッチ主体でもcontroller supportは価値があるが、touch版を劣化コピーにしない。

## 10. Prototype many layouts

複数案が技術的に動いても、体感差は大きい。

最終判断は実機プレイで行う。

## Playtest

- 操作中にHUDを見る頻度
- thumbで重要対象が隠れる秒数
- 誤タップ率
- 片手／両手の疲労
- 小型／大型端末差
- 削ったボタンでゲーム判断まで消えていないか


## 11. Safe areas and system gestures

iPhoneでは、
- Home indicator
- Dynamic Island
- rounded corners
- edge system gestures
を考慮する。

主要アクションを画面端ぎりぎりへ置かない。

safe areaは単なる表示余白ではなく、入力信頼性の境界として扱う。

## 12. Target size

頻繁な操作は十分大きなtap targetを持つ。

見た目のiconよりhit regionを大きくできる。

小さな端末でも、プレイヤーがゲーム画面から視線を外さず押せることを優先する。

## 13. Simultaneous input graph

同時に必要な操作を列挙する。

例:
- move + camera
- move + attack
- aim + fire
- steer + brake

同じthumbに二つの必須操作を割り当てていないか確認する。

## 14. Dynamic controls

タッチでは、
- unavailable actionを隠す
- contextでiconを変える
- thumbstickをtouch位置へ出す
など、物理controllerにはできない変化を使える。

ただしcontext変更は予測可能にする。

## 15. Press confidence

各重要入力へ、
- visual state
- sound
- haptic
のうち複数を返す。

指がbuttonを覆っていてもpress成功が分かる表現を使う。

## 16. Haptic grammar

hapticを一貫した言語にする。

例:
- light transient = selection
- sharp impact = hit
- continuous pulse = danger

別意味を同じpatternへ割り当てすぎない。

## 17. Edge gesture conflicts

ゲームgestureがsystem gestureと競合する場合、
ユーザーがOS操作を失敗し続けないようにする。

custom gestureを必要以上にedgeへ依存させない。

## 18. Long-session fatigue

5分では快適でも30〜60分で、
- thumb strain
- grip shift
- device heat
- repeated reach
が問題になる。

短時間テストだけでcontrol layoutを決めない。
