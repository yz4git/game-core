# Camera & Targeting Design

3Dゲームのカメラを映像演出ではなく、移動・照準・敵スケジューリングを成立させるゲームシステムとして扱う。

## 1. Three coordinate frames

3D操作では最低でも、
- player facing
- camera facing
- target direction
が存在する。

失敗原因が技能ではなく軸の不一致になっていないか確認する。

## 2. Lock-on collapses ambiguity

精密な近接戦、会話、調査などでは、一時的にplayer-camera-target関係を固定すると意図が伝わりやすい。

ロックオンはaim assistではなく、座標系を単純化する機構でもある。

## 3. Target state must be explicit

最低限、
- acquired
- switched
- lost
を即座に判別できること。

マーカーは世界観に統合してよいが、装飾のために状態差を弱くしない。

## 4. Camera and enemy scheduling are coupled

カメラが同時に見せられる高優先脅威数には限界がある。

敵を、
- active attacker
- visible pressure
- queued attacker
- repositioning enemy
に分け、全員が独立して最大攻撃しないようにする。

## 5. Automatic common case, manual exception

通常は自動追従で負担を減らし、特殊な地形・探索では低摩擦な手動修正を許す。

プレイヤーが常時カメラを操作し続けないと遊べないなら、自動側が弱い可能性がある。

## 6. Camera distance changes difficulty

近い:
- キャラが大きい
- 接触感が強い
- 周辺脅威が見えにくい

遠い:
- 状況把握しやすい
- 距離感や迫力が弱くなる場合がある

演出だけでなく戦闘難度として調整する。

## 7. Occlusion handling

壁・敵・エフェクトが操作対象を隠す場合、
- camera collision
- fade
- silhouette
- transparency
- angle correction
を使う。

カメラが壁を避けた結果、急回転して入力方向まで反転する副作用もテストする。

## 8. Verticality

高低差がある戦闘では、水平ロックオンだけでは距離を誤認しやすい。

- target elevation
- landing point
- projectile arc
を読める画角を確保する。

## 9. Mobile touch

タッチではカメラ操作と攻撃入力が同じ指領域を奪いやすい。

検討:
- auto-centering
- target lock
- swipe dead zone
- context camera
- temporary recenter button

操作数を増やす前に自動化できる部分を探す。

## Playtest

- ミスがplayer/camera/targetのどの軸から起きたか
- ロック対象切替を誤認しないか
- 画面外から高優先攻撃が来ないか
- カメラ距離変更で難易度が壊れないか
- 壁際で入力方向が急変しないか
- タッチ中にカメラ操作が攻撃を妨げないか


## 10. Speed-based framing

高速移動時は、キャラクター周囲より進行方向の未来情報を優先する。

- distance
- forward offset
- FOV
を速度に応じて調整する。

## 11. Visibility priority

カメラ衝突解決では、
1. player / target visibility
2. control stability
3. composition
の順に優先する。

「壁には入らないが敵が見えない」状態を成功とみなさない。

## 12. Level-authored overrides

万能アルゴリズムへ依存せず、
- boss arena
- narrow corridor
- fall
- high-speed segment
- puzzle view
へレベル側からカメラ指示を出せるようにする。
