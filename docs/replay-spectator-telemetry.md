# Replay, Spectator & Run Telemetry

リプレイを録画機能ではなく、学習・競技・デバッグ・観戦・共有を支える共通基盤として設計する。

## 1. Decide the replay model early

主方式:

### Video capture
見た目をそのまま保存するが、ゲーム状態分析には弱い。

### State recording
柔軟だがデータ量が多い。

### Input replay
軽量だがdeterminismが必要。

用途に合わせて選ぶ。

## 2. Determinism

Input replayでは、
- RNG seed
- update order
- clocks
- physics
- initial state
を揃える。

小さな差が後で大きな差になる。

## 3. Debug state assertions

開発中は主要状態を一定間隔で保存・比較し、
リプレイがいつ原本からずれたか検出できるようにする。

## 4. Version metadata

replay / ghost / leaderboard recordに保存する。

- game version
- map version
- generator version
- platform if relevant
- seed
- run settings

パッチ後の互換性を明示する。

## 5. Kill cam as explanation

Kill camは演出だけでなく、
- attacker
- angle
- timing
- resource state
- telegraph
を見せ、死因理解へ使う。

## 6. Ghosts

ゴーストは、
- pace comparison
- route teaching
- optimization
に有効。

要件:
- no collision
- readable but unobtrusive
- easy on/off
- split difference display

## 7. Spectator focus

観戦では複数事件を同時に見せすぎない。

焦点候補:
- objective
- ball
- leader
- major fight
- record attempt

## 8. Continuous readability

観客は途中から来る。

常時見せる:
- objective
- score
- leader
- current danger
- remaining time
- important resource

## 9. Camera modes

用途に応じて用意する。

- focus camera
- free camera
- player POV
- follow camera
- tactical overview

実況者が重要場面へすぐ移れることが重要。

## 10. Highlight detection

派手な数値だけでなく状態変化を見る。

候補:
- lead change
- rescue
- clutch
- record split
- large risk success
- comeback

## 11. Run telemetry

challenge / speedrun用に、
- split
- deaths
- route
- seed
- version
- assists
- category
を保存する。

## 12. Replay as QA

再現困難bugでも、入力・RNG・初期状態が揃えば再現できる可能性が高まる。

リプレイ基盤をデバッグ機能として利用する。

## Playtest

- 同じrunを10回再生して同じ結果か
- replayを見て死亡理由を理解できるか
- version違いを誤ってleaderboard比較しないか
- spectatorが30秒で状況を理解できるか
- highlightが本当に意味ある瞬間か


## 13. Hybrid replay

完全なinput replayと完全state recordingの中間を使える。

例:
- 通常はinput/eventを記録
- 数秒ごとにkey state
- divergence時は近いkey stateから再開

これにより、
- file size
- seek speed
- determinism robustness
を両立しやすい。

## 14. State checksums

重要状態からhash/checksumを作り、一定tickごとに記録する。

候補:
- player transforms
- score
- RNG state
- objective state
- active entity count

再生時に比較し、最初のdivergenceを特定する。

## 15. Compression

毎frameの完全transformを保存する前に、
- delta
- quantization
- event-based recording
- keyframe
を検討する。

競技／デバッグで必要な精度と、観戦の見た目精度を分ける。

## 16. Rewindable debugging

短時間の状態ring bufferを常時保持すると、
クラッシュ／AI異常の直前へ戻って調査できる。

これはinput replayの完全determinismとは別のデバッグ価値を持つ。

## 17. Compatibility policy

replay formatには明示的なversionを持つ。

方針例:
- same-version only
- migration support
- video fallback
- metadata-only archive

中途半端な互換再生で誤った競技結果を見せない。

## Additional QA

- 1時間runで最初のdivergence tickはどこか
- checksum overheadは許容範囲か
- seekに何秒かかるか
- keyframe間隔を変えた時のfile size
- patch後に旧ghostをどう扱うか
