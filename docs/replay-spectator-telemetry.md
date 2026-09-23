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

Input replayでは、RNG seed、update order、clocks、physics、initial stateを揃える。小さな差が後で大きな差になる。

## 3. Debug state assertions

開発中は主要状態を一定間隔で保存・比較し、リプレイがいつ原本からずれたか検出できるようにする。

## 4. Version metadata

replay / ghost / leaderboard recordにgame version、map version、generator version、platform、seed、run settingsを保存し、パッチ後の互換性を明示する。

## 5. Kill cam as explanation

Kill camは演出だけでなくattacker、angle、timing、resource state、telegraphを見せ、死因理解へ使う。

## 6. Ghosts

ゴーストはpace comparison、route teaching、optimizationに有効。no collision、readable but unobtrusive、easy on/off、split difference displayを満たす。

## 7. Spectator focus

観戦では複数事件を同時に見せすぎない。objective、ball、leader、major fight、record attemptなどから焦点を選ぶ。

## 8. Continuous readability

観客は途中から来る。objective、score、leader、current danger、remaining time、important resourceを常時読めるようにする。

## 9. Camera modes

focus camera、free camera、player POV、follow camera、tactical overviewを用途に応じて用意し、重要場面へすぐ移れるようにする。

## 10. Highlight detection

派手な数値だけでなくlead change、rescue、clutch、record split、large risk success、comebackなど状態変化を見る。

## 11. Run telemetry

challenge / speedrun用にsplit、deaths、route、seed、version、assists、categoryを保存する。

## 12. Replay as QA

再現困難bugでも、入力・RNG・初期状態が揃えば再現できる可能性が高まる。リプレイ基盤をデバッグ機能として利用する。

## 13. Hybrid replay

通常はinput/eventを記録し、数秒ごとにkey stateを置き、divergence時は近いkey stateから再開するなど、input replayとstate recordingを組み合わせられる。file size、seek speed、determinism robustnessを両立しやすい。

## 14. State checksums

player transforms、score、RNG state、objective state、active entity countなどからhash/checksumを作り一定tickごとに記録し、最初のdivergenceを特定する。

## 15. Compression

毎frameの完全transformを保存する前にdelta、quantization、event-based recording、keyframeを検討する。競技／デバッグで必要な精度と観戦の見た目精度を分ける。

## 16. Rewindable debugging

短時間の状態ring bufferを常時保持すると、クラッシュ／AI異常の直前へ戻って調査できる。これはinput replayの完全determinismとは別のデバッグ価値を持つ。

## 17. Compatibility policy

replay formatには明示的なversionを持つ。same-version only、migration support、video fallback、metadata-only archiveなど方針を決め、中途半端な互換再生で誤った競技結果を見せない。

## 18. Retention is part of compatibility

interactive replayの保存期間を用途別に定義する。recent learning用は短期、明示的にpinした記録や大会証跡は長期などに分ける。patch境界で再生保証が切れるならUIで明示する。

## 19. Replay truth should follow authority

競技結果の検証ではclient presentationではなくauthoritative state、またはそれに照合可能な記録を基準にする。prediction/reconciliationの見た目を公式結果と混同しない。

## 20. Spectators are least-authority clients

観戦者はread-only roleとして扱い、通常のgameplay command pathを拒否する。大規模観戦ではmatch serverから一度生成したsnapshot/replay streamを別のreplicator/distributionへ渡し、観客数がsimulation負荷へ直結しない構成を検討する。

## 21. Replay export is a privacy boundary

raw replayにはUIで見えないaccount ID、session情報、private/debug stateが含まれ得る。共有時は用途に不要な識別子・認証情報・private stateを除去し、必要ならraw replayではなくrendered clipを使う。

## 22. Analysis controls are core UX

pause、step、speed、event jump、camera switch、entity follow、bookmarkを優先する。Replayの価値は保存精度だけでなく、疑問の瞬間へ何秒で到達できるかで決まる。

## 23. Spectator telemetry should measure comprehension

watch timeだけでなく、camera switch、rewind、event jump、tactical overlay使用、exit地点などを集計し、「盛り上がって見返した」のか「理解できず見返した」のかをプレイテストで切り分ける。個人識別が不要ならaggregateで収集する。

## 24. Long-term evidence needs a less coupled representation

interactive replayはsimulation codeへ依存する。重要な記録にはvalidated result metadata、integrity hash、主要stats、必要ならrendered video/highlightを残し、旧simulationが動かなくなっても証跡を維持する。

## Playtest / QA

- 同じrunを10回再生して同じ結果か
- replayを見て死亡理由を理解できるか
- version違いを誤ってleaderboard比較しないか
- spectatorが30秒で状況を理解できるか
- highlightが本当に意味ある瞬間か
- 1時間runの最初のdivergence tickはどこか
- checksum overheadは許容範囲か
- seekに何秒かかるか
- keyframe間隔を変えた時のfile sizeはどう変わるか
- patch後に旧ghost/replayをどう扱うか
- pinned replayが自動evictionから守られるか
- spectator clientからauthoritative stateを変更できないか
- spectator数増加でplayer latencyが悪化しないか
- export replayに不要なprivate identifierが残っていないか
- authoritative resultとreplay reconstructionが一致するか
