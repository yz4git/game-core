# Sports Game Abstraction

実競技の全動作を再現するのではなく、競技らしい判断・位置・時間・チーム意図をゲーム操作へ圧縮する。

## 1. Preserve the decision loop

最初に実競技の中心判断を書く。

例:
- space creation
- timing
- passing lane
- risk of commitment
- matchup
- positioning

身体動作の再現度より、これらがプレイヤー判断として残ることを優先する。

## 2. Abstraction is not simplification of meaning

ボタン数を減らしても、入力結果が位置・速度・味方・相手・タイミングで変われば深さは残る。

「操作が少ない = 浅い」と考えない。

## 3. Camera and controls are coupled

スポーツカメラは観戦映像の再現だけで決めない。

カメラ方向が変わると、
- stick direction
- pass direction
- player switching
- defensive positioning
のmental modelも変わる。

Alternate cameraは操作系として再テストする。

## 4. Team AI first

チームスポーツAIは個体の自然さだけでは成立しない。

優先:
1. team objective
2. formation / spacing
3. assignment
4. local movement
5. animation polish

個体が自然でもチーム意図に反する動きなら不自然に見える。

## 5. Off-ball behavior is gameplay

ボールを持っていない味方が、
- spaceを作る
- markする
- support angleを作る
- runを開始する
ことで、ボール保持者の選択肢が変わる。

オフボールAIを背景演出として扱わない。

## 6. Player switching

操作対象切替では、最も近い選手だけでなく、
- play direction
- threat
- intended receiver
- defensive assignment
を考慮する。

切替候補が予測できるフィードバックを持たせる。

## 7. Layer tactical complexity

初心者には、
- recommended play
- basic formation
- context command
を優先する。

熟練者には、
- full playbook
- matchup
- formation adjustment
- off-ball command
を展開する。

深さを削るのではなく段階表示する。

## 8. Authenticity vs playability

本物らしいカメラ・物理・操作が、必ずしもゲームとして読みやすいとは限らない。

Authenticityを、
- visual
- tactical
- physical
- emotional
に分け、どれを再現したいか決める。

## 9. Match ending

試合結果が実質確定しているのに長く続くと、終盤が消化時間になる。

競技ルールを壊さない範囲で、
- comeback possibility
- mercy rule
- overtime condition
- accelerated dead time
など、最後まで意味ある状態を保つ方法を検討する。

## 10. Telemetry

スポーツゲームは選択肢が多いため、
- play selection
- unused commands
- switch errors
- quit timing
- matchup imbalance
をtelemetryで見る価値が高い。

初心者が高度機能を使わないことと、存在を知らないことを区別する。

## Playtest

- artを単純図形にしても競技らしい判断が残るか
- camera変更後に方向入力ミスが増えないか
- AI teamの意図を一文で説明できるか
- off-ball teammateが選択肢を増やしているか
- player switchingの予測ができるか
- noviceが最初のplay開始まで何択を処理するか
- advanced playerに戦術上の追加判断が残るか
