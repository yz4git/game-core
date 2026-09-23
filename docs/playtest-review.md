# Playtest Review Framework

「画面を見てプレイチェックして改善する」ための共通レビュー手順。

## 0. 最初に見ること

プレイ開始後30秒以内に確認する。

- 何をすればよいか分かるか
- 操作対象が明確か
- 最重要ボタンが自然に見つかるか
- 初回入力に即座の反応があるか
- UIがゲーム画面を邪魔していないか
- タッチ／マウス／パッドで誤入力が起きないか

## 1. Core Feel

操作そのものを評価する。

- 入力遅延
- 加速／減速
- 旋回
- ジャンプ／回避／攻撃の出始め
- キャンセル可否
- ヒットストップ
- カメラ追従
- 被弾時の反応
- 効果音と視覚反応

**原則:** ここに重大な問題がある場合、新コンテンツ追加より先に直す。

## Batch 25 — Replay highlight / spectator safety review

- 自動highlight top-kに「派手だが意味の薄い」hard negativeが混ざらないか
- clipがpeak瞬間だけでなくsetup→decision→resolutionを含むか
- 初見viewerが「何が変わったか／なぜ重要か」を説明できるか
- 5本のhighlightが同じkill/score型だけにcollapseしていないか
- coaching / entertainment / personal memoryで同じrankingを無理に共有していないか
- modality別scoreを保持し、映像・音・reactionの不一致を調査できるか
- spectator stateにfog-of-war、private inventory、future RNG、team-only marker等が含まれないか
- delayを0にしても公開してよいfieldだけがspectator schemaに存在するか
- configured delay後でもcollusionに使える情報が残らないか
- public replay exportがallowlist方式でprivate/debug fieldを除外しているか
- detected eventをseek/camera/render APIから人手なしで再現clip化できるか
- highlight telemetryがraw chat/voice/face/account IDを不要に保存していないか
- level/seed別highlight signatureが単一パターンへ偏っていないか
- longest low-highlight intervalが意図した休息なのか、判断密度低下なのか確認したか
