# Replay Validation Operations

Replay / rollback / ghostを、競技・デバッグ・観戦で信頼できる状態に保つための運用ガイド。

## 1. Detection and diagnosis

### Detection
軽量checksum/hashで毎tickまたは一定間隔に比較する。

### Diagnosis
不一致が出たら、
- structured state dump
- field diff
で原因へ掘る。

checksumだけで根本原因まで求めない。

## 2. First divergence

最も重要なのは最初に違ったtick。

後続差分は二次的。

工具は、
- first divergent frame
- first divergent subsystem
- first divergent field
を出せることを目標にする。

## 3. State coverage

hash対象を明示する。

含める:
- player authoritative state
- RNG
- objectives
- gameplay-relevant entities

通常含めない:
- particles
- UI animation
- camera-only state

## 4. Side effects

Replay/rollbackでsimulationを再実行しても、
- sound
- vibration
- analytics
- achievement
- external network calls
を重複発火させない。

simulation eventとcommitted side effectを分離する。

## 5. Keyframes and seek

長いreplayには、
- periodic keyframes
- event index
を持たせる。

seek候補:
- death
- checkpoint
- boss
- split
- lead change

先頭から毎回再生しない。

## 6. Replay regression suite

固定replayをCIで再生し、
- final result
- event order
- state hash
を比較する。

非決定性の早期検出に使う。

## 7. Compatibility

replay header:
- format version
- game version
- map/content version
- generator version
- platform if necessary

旧版を無理に新ルールで再生しない。

## 8. Competitive validation

Leaderboard recordには、
- replay/ghost
- category
- assists
- seed
- version
を紐付ける。

条件違いを同じランキングへ混ぜない。

## 9. Privacy / retention

Replayにユーザー識別や通信内容を含む場合は、
- 必要データだけ保存
- retention期間
- access control
を設計する。

## Checklist

- first divergenceを自動特定できるか
- hash対象が明文化されているか
- rollbackで副作用が二重実行されないか
- seek indexがあるか
- replay CI regressionがあるか
