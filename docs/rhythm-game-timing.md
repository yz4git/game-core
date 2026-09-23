# Rhythm Game Timing

音ゲー／リズムゲームで、判定精度・同期・校正・学習フィードバックを設計するためのガイド。

## 1. Audio clock first

ゲーム全体の基準時刻は、描画フレームではなく音声システムの高精度時刻に置く。

ノート位置・判定・エフェクトを音声時刻から計算し、フレーム差分を積み上げて同期しない。

## 2. Account for offset

曲頭の無音や実際の最初の拍位置をデータとして持つ。

BPMが正しくても、最初の拍オフセットがずれると全譜面がずれる。

## 3. Calibration

プレイヤー環境ごとに遅延は違う。

最低でも、
- Audio offset
- Visual offset
- Input offset
の考え方を分ける。

BluetoothやTV処理など、ゲーム外の遅延も吸収できるようにする。

## 4. Judgment windows

Perfect / Great / Good / Miss を単なるスコア帯にしない。

判定結果から、
- Early
- Late
をプレイヤーが理解できるようにする。

練習画面では平均偏差や傾向を見せてもよい。

## 5. Difficulty

難度はノーツ密度だけで増やさない。

増やせる要素:
- リズムの複雑さ
- 同時入力
- 交互入力
- オフビート
- 長押し
- 視線移動
- 体力／持久性

上級譜面でも音楽構造と対応していることを優先する。

## 6. Preserve musical flow

ミス時でも曲自体は流し続ける方が、タイミングの基準を保ちやすい。

失敗表現は、
- プレイヤー音だけ外れる
- 一時的に音量／エフェクトが変わる
- スコア／ゲージで返す
などを使う。

## 7. Controller quality

専用コントローラやタッチ入力では、
- デッドゾーン
- 連打
- 同時押し
- 物理反発
- 押下深度
を実機で評価する。

不安定な入力装置では公平な判定窓を作れない。

## 8. Mobile / browser

Web Audio APIではAudioContextの時刻を基準にし、requestAnimationFrameの時刻だけで判定しない。

iPhoneでは、
- ユーザー操作後のAudioContext開始
- Bluetooth遅延
- 省電力／負荷
も検証する。

## Playtest

- 5分プレイ後にEarly/Late偏りがないか
- Bluetoothで校正可能か
- 30fps相当でも音と判定が維持されるか
- 画面録画時でも同期が崩れないか
- 初心者が拍を理解して上達できるか
