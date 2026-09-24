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

## Batch 26 — Adversarial procedural QA review

- random seed数だけでcoverage達成と判断していないか
- canonical / random / adversarial cohortを別集計しているか
- hard invalidだけでなくnear-failure marginを保存しているか
- geometry/topologyを通過したseedをdynamic simulationでも検証しているか
- local adjacencyが正しくてもglobal progressionが破綻していないか
- novice/baseline/expert/exploit-seeking等で結果が大きく食い違わないか
- adversarial searchが見た目の奇妙さではなくplayer-relevant failureを最大化しているか
- solution/action traceがほぼ同じseedをcosmetic diversityとして水増ししていないか
- RGB screenshotだけでなくdepth / collision / semantic / affordance差分を見られるか
- objective / hazard / road / landmark等を装飾より重くvisual diffしているか
- generator version更新でbehavior clusterが消失・過密化していないか
- rolling new-cluster discovery rateが本当に飽和したか
- rolling severe-failure discoveryもrandom/adversarial双方で飽和したか
- severe failureを小さなreproへ自動縮小できるか
- 人間が発見した反復・迷い・理不尽を次回からmachine predicateへ変換したか

## Batch 32 — Client prediction / trust-boundary review

- clientがfinal position/damage/reward等、authorityが再導出できない結果を直接確定できないか
- 値の範囲だけでなく入力順序・action rate・cooldown・tick windowを検証しているか
- lag compensationの最大rewindとclient timestamp clampが明示されているか
- duplicate/retry/reconnect replayでhit・pickup・purchase・unique rewardが二重確定しないか
- ownership取得が不要なstate write権限まで与えていないか
- authority transfer後の旧generation packetが勝てないか
- listen-host/shared/relay matchの結果がtrusted-server matchと同じrank/reward poolへ無条件で入らないか
- correctionはcanonical stateを優先し、visual smoothingがcollisionやaffordanceへ逆流しないか
- anti-cheat invariantをhonest jitter/loss/reorder/background/resume/host migrationでfalse-positive検証したか
- clientへfog-of-war/private/debug/future stateを不要にreplicateしていないか
- security telemetryがopaque scoreだけでなく具体的なinvariant violationを残すか
- durable rewardほどmovement predictionより強いauthority tierを要求しているか

## Batch 33 — Network-quality matchmaking review

- playabilityのhard floorとcandidate rankingのpreferenceを分離しているか
- skill一致がnetwork floor違反を相殺していないか
- 全員が許容できるcommon feasible regionを選んでいるか
- median pingだけでなくjitter / loss / burst lossも実match品質と照合しているか
- expansionが一気に「何でも可」にならず段階的なquality-loss curveになっているか
- build/protocol/trust等のinvariantが待ち時間でoptionalにならないか
- genreで最も重要な品質を最後まで保護するrelaxation順序になっているか
- party平均が一人のunplayable edgeを隠していないか
- queue/pool分割ごとのpopulation taxをeligible candidate数とwait p95で測っているか
- QoS measurement ageを保存し、stale measurementを無条件に再利用していないか
- pre-match QoSと実match RTT/jitter/loss/rollback/disconnectを同じsessionで追跡できるか
- thresholdごとにfalse accept / false reject / added waitを比較したか
- ranked/tournamentとcasualで同じnetwork envelopeを無条件共有していないか
- 検索範囲を広げた場合、そのtrade-offをplayerが理解できるか
