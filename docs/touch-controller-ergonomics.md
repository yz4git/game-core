# Touch & Controller Ergonomics

タッチ操作を「画面上のゲームパッド」ではなく、別の入力媒体として設計する。

## 1. Preserve decisions, not buttons

操作数ではなく、aim / dodge / route / acceleration / timingなどの意思決定を守る。入力方法は媒体に合わせて変えてよい。

## 2. Directness

objectやlocationを直接触れる方が自然ならvirtual cursor/buttonを挟まない。

## 3. No tactile landmarks

物理buttonの縁や反発がないため、oversized zones、whole-screen regions、dynamic joystick、generous hit areasを使う。

## 4. Finger occlusion

thumb footprint、hand posture、device size、orientationを考慮し、入力中に重要情報を隠さない。

## 5. Invisible controls need feedback

helper arrow、brief joystick ring、direction trail等で入力状態を確認できるoptionを用意する。

## 6. Context-sensitive input

同じgestureの意味変更は予測可能な場合だけ使う。

## 7. One-hand vs two-hand

片手はreachability/large regions、両手はsimultaneous actions/stable gripを重視する。

## 8. High-skill touch

mobileだから判断を単純化する必要はない。direct touch、large zones、multi-touchで高度な判断を維持できる。

## 9. Optional controller support

controllerを支援してもtouch版を劣化コピーにしない。

## 10. Prototype many layouts

最終判断は複数deviceの実機プレイで行う。

## 11. Safe areas and system gestures

Home indicator、Dynamic Island、rounded corners、edge gesturesを入力信頼性の境界として扱う。

## 12. Target size

見た目のiconとhit regionを分離し、高頻度操作には十分大きなtargetを与える。

## 13. Simultaneous input graph

move+camera、move+attack、aim+fire、steer+brake等を列挙し、同じthumbへ競合する必須操作を割り当てない。

## 14. Dynamic controls

unavailable actionの非表示、context icon、touch位置へのstick出現を使えるが、context変更は予測可能にする。

## 15. Press confidence

重要入力にはvisual/sound/hapticの複数channelを使い、fingerでbuttonが隠れても成功が分かるようにする。

## 16. Haptic grammar

selection/hit/danger等でpatternを一貫させ、同じpatternを別意味へ乱用しない。

## 17. Edge gesture conflicts

custom gestureを必要以上にscreen edgeへ依存させない。

## 18. Long-session fatigue

5分だけでなく30〜60分でthumb strain、grip shift、device heat、repeated reachを見る。

## 19. Reachability field

reachabilityは固定rectangleではなくdevice size、selected hand、gripで変わるcost fieldとして扱う。高頻度×高緊急×高精度のactionへ最も安いreachを割り当てる。

## 20. Handedness is semantic remapping

左右presetを単純mirrorしない。move/camera/primary等のroleを維持しつつ、position/spacing/scale/capture regionを再最適化する。

## 21. Bounded floating controls

floating stickはtouch-downへ追従できるがcapture region、safe-area clamp、neutral/dead zone、最大移動量を固定する。適応でmotor memoryを壊さない。

## 22. Measure occlusion

critical information under thumb timeを測る。failure直前にtelegraph/targetがfingerで覆われていなかったか確認する。

## 23. Haptic density budget

haptic events/minuteを記録し、parry/collision/lock/danger等の意味ある状態変化を優先する。OFFでも情報を失わせない。

## 24. Thermal ergonomics

sustained load後のgrip shift、miss-rate delta、performance degradationを測る。冷えた端末だけでlayoutを承認しない。

## 25. Semantic equivalence across inputs

Touch/controller/keyboardはbutton数ではなくacquisition time、simultaneous action、precision、correction、fatigue、preserved tactical choiceで比較する。

## Playtest

- 操作中にHUDを見る頻度
- thumbで重要対象が隠れる秒数
- 誤タップ率
- 片手／両手の疲労
- 小型／大型端末差
- high-frequency actionのreach distance
- handedness presetのrole confusion
- dynamic stickのrecenter/acquisition time
- haptic events/minuteとpattern識別
- 30〜60分後のmiss-rate delta
- device heat後のgrip reposition
- input媒体を変えて重要な判断が消えないか
