# Replay Determinism & Regression

Replayを、観戦だけでなくバグ再現・ghost・leaderboard検証へ使うための実装原則。

## 1. Pick the guarantee

Replay用途ごとに必要保証を決める。

### Debug
原因状態へ戻れること。

### Competitive
同一runが同じ結果になること。

### Spectator
見た目が自然であること。

### Ghost
位置・ペースが十分正確であること。

一つの方式ですべてを満たそうとしない。

## 2. Input replay

記録:
- input events
- RNG seed/state
- initial state
- authoritative clock
- version

利点:
- 小容量
- ghost向き

欠点:
- determinism依存

## 3. Snapshot replay

一定tickごとにstateを保存する。

利点:
- seek
- rewind
- debugging

欠点:
- 大容量

## 4. Hybrid

Input/events + periodic key snapshotsを組み合わせる。

実用上、
- replay
- seek
- divergence recovery
のバランスを取りやすい。

## 5. State hashes

一定tickごとに重要状態hashを保存する。

不一致時に、
> どのtickからズレたか
を特定する。

最終scoreだけの比較より原因探索が速い。

## 6. Compression

順に検討:
1. 不要状態を保存しない
2. event recording
3. delta
4. quantization
5. keyframe interval

圧縮で競技結果の精度を落とさない。

## 7. Versioning

Replay header:
- schema version
- game version
- map/content version
- generator version
- category/settings

旧版が非互換なら、誤再生より明示的に拒否する。

## 8. CI regression

代表replayを固定テストにする。

変更後に、
- checksum
- final score
- events
を比較する。

意図したbalance changeによる差と、非意図的determinism regressionを分ける。

## 9. Rewind debugging

開発buildでは数十秒分のring-buffer snapshotを保持すると、
「今起きた変な挙動」の直前へ戻って調査できる。

## Checklist

- authoritative time sourceは一つか
- RNGを再現できるか
- replay hashを定期比較できるか
- replay schema versionがあるか
- patch後の互換方針があるか
- ghostとdebug replayで必要精度を分けているか
