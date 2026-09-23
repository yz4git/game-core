# Touch Production QA

iPhone / iPadの実機で、タッチ操作を長時間・複数端末・OS gesture環境まで含めて検証する。

## 1. Safe-area matrix

複数端末・orientationで確認する。

- rounded corners
- Dynamic Island
- Home indicator
- edge gestures

主要アクションをシステム領域と競合させない。

## 2. Thumb reach

safe-area内でも、
「親指が自然に届くか」は別問題。

横画面では左右のthumb arcを基準にし、
頻繁操作を自然な位置へ置く。

## 3. Target size

頻繁操作は44ptを基準にする。

見た目のiconよりhit targetを大きくする。

プレイヤーがゲームから視線を外さず押せることを優先する。

## 4. Simultaneous input graph

必要な同時操作を書き出す。

例:
- move + attack
- move + camera
- steer + brake
- aim + fire

同じthumbへ同時要求が集中していないかを見る。

## 5. Press feedback

重要操作には、
- visible press state
- sound
- optional haptic
を組み合わせる。

指がUIを覆っていても成功を理解できるようにする。

## 6. Haptic semantics

haptic patternの意味を固定する。

多用しすぎない。
OFFでもゲーム情報を失わない。

## 7. System gesture conflicts

画面端gestureと、
- dodge swipe
- camera drag
- virtual button
が競合しないか実機で測る。

## 8. Fatigue test

5分だけでなく、
- 30 min
- 60 min
で評価する。

記録:
- thumb pain
- grip changes
- mis-taps
- hand repositioning
- device heat discomfort

## 9. Handedness

必要なら左右配置mirrorを検討する。

片手ゲームでは特に左右利き差が大きい。

## 10. Device-size matrix

小型／大型iPhoneで、
- reach
- occlusion
- control separation
を確認する。

## Checklist

- safe areaとthumb comfortの両方を満たすか
- 44pt未満の頻繁操作がないか
- haptics OFFでも理解できるか
- 60分後も操作姿勢が維持できるか
- system gesture誤発火率を測っているか
