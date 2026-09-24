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
- 初見viewerが「何が変わったか／なぜ重要だったか」を説明できるか
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

## Batch 34 — Protocol / version migration review

- player-facing version文字列だけで互換性を判定していないか
- RPC/command/replicated-state schemaのfingerprint mismatchをREADY前に拒否できるか
- build IDの違いとprotocol incompatibilityを同一視してpopulationを不要に分断していないか
- N/N-1などadvertiseしたmixed-version pathを実際にpairwise CIしているか
- required capabilityとoptional capabilityを分離してnegotiationしているか
- queue expansionがprotocol cohortを越えないか
- rolling deploy中に旧clientが接続可能な旧server cohortを失わないか
- running matchのsession protocol epochがdeploymentで途中変更されないか
- app update後のreconnectが元session epochを再検証するか
- host migration候補がlatency評価より前にcheckpoint/schema compatibilityを通過するか
- 古いinvite/reconnect tokenがdeployment後にcached endpointへ直結しないか
- stale web/PWA clientを通常のcompatibility caseとして試験しているか
- unsupported clientがgeneric network errorではなく明確なupdate/compatibility理由を受け取るか
- old cohort retirementをactive-session数とversion adoption率で判断しているか

## Batch 35 — Procedural 3D visibility / road continuity review

- roadが見た目で接続しているだけでなくnav graph / lane / collisionでも連続しているか
- connected component数だけでなくarticulation point / bridge / alternate-route余裕を測っているか
- seamで曲率・勾配・幅が急変し、想定速度では実質通れなくなっていないか
- baseline driverが道路継ぎ目で緊急steer/brake/reverseを要求されないか
- landmarkをeditor cameraではなく実際のgameplay camera/FOVから評価しているか
- landmarkのvisible frame数だけでなくfirst-visible距離・最長遮蔽・decision前の連続可視時間を測っているか
- landmarkが細い遮蔽物やLOD境界でvisible/hiddenを短時間に繰り返していないか
- junctionの分岐差が安全なsteer/brake deadlineより前に読めるか
- RGB差分だけでなくdepth / semantic / road-lane / collision bufferを比較しているか
- facade/weather差で同じ都市構造を多様と誤認せずskyline signatureを比較しているか
- landmarkを常時見せるのではなく、必要なdecisionで再出現するreveal scheduleになっているか
- random screenshotだけでなくvisibility marginを最小化するadversarial camera searchを行ったか
- worst-N seedだけでなくworst-N camera/route positionもregression fixtureに残しているか
- 人間が「道が消えた・分岐が読めない・街が全部同じ」と感じったケースを次の自動predicateへ変換したか

## Batch 37 — Dynamic visibility / interior / lighting review

- moving traffic/crowd/door/enemyがdecision直前だけcritical cueを隠していないか
- visibilityを静止画ではなく時間列として記録し、commitment前のstable-visible時間を測っているか
- dynamic objectのrenderer上のoccluder/occludee設定とgameplay上の遮蔽役割を混同していないか
- 高速camera旋回時の1-frame popと、配置そのものによる長時間遮蔽を別原因として扱っているか
- traffic/crowd seedを変えたときのdeadline occlusion確率とp5 visibilityを測っているか
- global landmarkが見えなくなるinteriorでfloor/zone/junction-local cueへ自然にhandoffするか
- 「見える物体数」が増えただけでwayfinding改善と判定せず、branch ambiguityが減ったか確認しているか
- stairs/elevator/ramp後にfloor/zoneとfacing directionをmapなしで再構築できるか
- open/closed/locked/destroyed等のportal stateごとにreachabilityとvisibility graphを再検査しているか
- day/dusk/night/weatherでline-of-sightだけでなくlandmark identification marginを確認しているか
- tunnel出入口やauto-exposure遷移中にmandatory decisionを置いていないか
- doorframe/window/corner/stair mouth等のvisibility-cell境界をworst-case fixtureとして残しているか
- route全体でglobal→district→floor→junction→destinationのcue handoff gapを測っているか
- occlusion severityを時間だけでなくpredictability / agency / consequenceでも評価しているか
- camera × portal × occupancy × lighting × deviceの全組合せを盲目的にrenderせず、cheap predicateでworst-Nを選んでいるか
