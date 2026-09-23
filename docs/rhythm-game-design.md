# Rhythm Game Design

リズムゲームを「ノーツを時間内に押す」だけでなく、同期・予測・身体感覚・表現・失敗後の学習として設計する。

## 1. Timing window is an emotional control

判定幅は単なる難易度数値ではない。

- 広い: 流れを保ちやすい、初心者が音楽へ乗りやすい
- 狭い: 集中、緊張、演奏感が強くなる

クリア判定と高ランク判定を同じ幅にする必要はない。

## 2. Audio is the authority

譜面表示は音楽を説明する補助であり、音と判定がずれてはいけない。

確認する遅延:
- audio output
- display
- touch/controller input
- game loop
- scheduling

固定遅延は校正できるが、揺れる遅延は別問題として扱う。

## 3. Feedback must identify the exact judged event

ノーツごとに、
- hit
- early
- late
- wrong input
- miss
を区別できるようにする。

グローバルなスコア変化だけでは学習が遅い。

## 4. Preserve musical continuity for beginners

練習では曲を途中停止しない選択肢を持つ。

失敗を記録しつつ最後まで演奏させ、終了後に弱い小節を示す。

## 5. Read ahead, do not react late

ノーツは反射だけでなく予測させる。

- 一定のスクロール
- 拍の基準線
- 小節構造
- 次フレーズの予告

プレイヤーが「来たから押す」から「来る時刻を予測して押す」へ移ることが上達。

## 6. Chart difficulty is not only density

難度軸:
- subdivision
- syncopation
- simultaneous inputs
- alternating limbs/fingers
- movement distance
- pattern memory
- tempo changes
- visual reading

単純にノーツ数だけを増やさない。

## 7. Expert expression

基礎同期を習得した後、正解列をなぞる以外の表現を許せる。

例:
- fills
- freestyle phrase
- optional ornament
- alternate hand/foot pattern
- riskier scoring route

## 8. Failure should stay musical

ミスSEや画面演出が曲そのものを壊しすぎないようにする。

失敗の情報は明確にしつつ、連続ミスで音楽がノイズ化しないよう優先順位を調整する。

## 9. Calibration

Web/mobileでは環境差を前提にする。

- 端末内蔵スピーカー
- 有線
- Bluetooth
- 外部画面
などを区別する。

校正は一度の数値入力ではなく、実際に拍へ入力して測れる形が望ましい。

## Playtest

- 音だけを信じても高精度で叩けるか
- 画面だけを見た場合とズレないか
- 一回のmiss原因を説明できるか
- 初心者が曲の最後まで拍を感じる時間を持てるか
- 高難度が密度以外の技能も要求するか
- 上級者に表現／最適化の余地があるか
