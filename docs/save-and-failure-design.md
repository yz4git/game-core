# Save & Failure Design

セーブ、チェックポイント、Game Over、永続損失を「難しさ」ではなく、学習と損失量の設計として扱う。

## 1. Save changes the cost of experimentation

保存間隔が長いほど、
- 慎重になる
- 未知を試しにくくなる
- 同じ区間の再実行が増える

何を学ばせたいかに合わせる。

## 2. Risk save vs convenience save

二種類を分ける。

### Challenge Save
ゲーム内の緊張・資源管理に関わる保存。

### Suspend Save
現実の都合で中断するための保存。

後者まで制限すると、生活時間が難易度になる。

## 3. Measure loss

死亡時に失うものを明示する。

- 時間
- 移動
- 会話
- 戦闘
- アイテム整理
- ランダムドロップ
- 成長

「10分戻る」と「10分考え直せる」は同じではない。

## 4. Place checkpoints before target skill

高難度アクションを試させたいなら、その直前へ戻す。

長い簡単区間を再実行させても対象スキルは鍛えられない。

## 5. Autosave safety

オートセーブで、
- HP1
- 資源ゼロ
- 逃げ不能
などの詰み状態を固定しない。

複数世代保持、巻き戻し、復帰時補正などを検討する。

## 6. Permanent loss

永続損失を使うなら、ゲームの核と一致させる。

良い例:
- リスク判断
- 経済
- ローグライクの長期緊張

弱い例:
- 単なるプレイ時間の消失

## 7. Failure should produce information

Game Over後に、
- 原因
- 改善可能点
- 次の目標
が見えるようにする。

## 8. Save schema is a compatibility contract

一度公開したsave形式は、休止プレイヤーが何年後かに持ち帰る可能性がある。

- schema versionを明示する
- 過去versionのmigrationを保持する
- game build versionとは分離する
- 過去save fixtureをCIに残す

## 9. Save writes should be transactional

唯一の正常saveを直接上書きしない。

**candidate write → integrity/semantic validation → commit → previous known-good保持**

途中終了や容量不足を「全進行消失」に変換しない。

## 10. Parse success is not state validity

JSON等を読めたこととゲーム状態が正しいことは別。

migration/load後に、ID、数値範囲、inventory、progression、world identity等のinvariantを検証する。

## 11. Backup needs time diversity

直近5回のautosaveが短時間に同じ破損を複製する場合がある。

recent backupだけでなく、session-startやmilestoneなど時間的に離れた復旧点を残す。

## 12. Cloud conflict is competing history

localとcloudの両方が正しい進行を持つ場合がある。

単純なtimestamp勝者ではなく、revision、device/session、進行要約を使い、安全に自動解決できない場合はプレイヤーへ意味のある差を示す。

## 13. Unknown future saves are read-only problems

古いbuildが新しいschemaを見た場合、推測して読み込み・autosaveしない。

元データを保持し、対応buildが必要なことを示す。

## Playtest

- 一回の失敗で何分失うか
- 中断だけしたい人を罰していないか
- オートセーブが詰み状態を作らないか
- 戻される部分に判断が残っているか
- 永続損失がゲームの中心体験に必要か
- 全released schemaのfixtureをcurrentへmigrationできるか
- save途中の各地点で強制終了してもknown-goodが残るか
- parse可能だが不正なstateを拒否できるか
- corruption発見が遅れても古い復旧点が残るか
- cloud/local競合で望む進行を選べるか
- 古いbuildが新しいsaveを破壊しないか
