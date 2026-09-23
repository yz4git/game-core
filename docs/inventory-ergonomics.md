# Inventory Ergonomics

インベントリ制限を単なる不便ではなく、装備構成・準備・優先順位のゲームにする。

## 1. Constraint must create a decision

容量不足時に毎回「安いゴミを捨てる」だけなら制限は作業になっている。

迷いが生まれる候補:
- 火力 vs 回復
- 即応性 vs 将来価値
- 軽量装備 vs 重装備
- 汎用性 vs 特化

## 2. Spatial inventory

アイテム形状が異なる場合、配置そのものを最適化問題にできる。

ただし整理頻度が高すぎるとパズルではなく家事になる。

## 3. Capacity progression

容量アップは制約を消すのではなく、選択肢を増やす方向に使う。

序盤の窮屈さを永久に維持する必要はないが、終盤も時々ロードアウト判断が残る程度を狙う。

## 4. Quick-use path

高頻度アイテムは一覧を毎回開かせない。

- quick slot
- contextual use
- favorite
- last-used
を検討する。

## 5. Comparison before replacement

装備変更前に、
- 現在品
- 候補
- 増減
- 特殊効果
を同じ視線範囲で比較できるようにする。

## 6. Junk policy

価値のないアイテムを大量に持たせる場合、
- auto-mark
- sell all
- category lock
- crafting relevance
を明示する。

プレイヤーに価値判定を何百回も再実行させない。

## 7. Sorting should preserve intention

自動ソートが便利でも、プレイヤーが意図した配置やquick accessを壊す場合がある。

lock/favorite領域を尊重する。

## 8. Inventory as preparation

戦闘中ではなく安全地帯でロードアウトを組むゲームなら、整理そのものを準備フェーズとして成立させられる。

戦闘テンポを切る頻度との交換を見る。

## Playtest

- full時に何秒整理するか
- その整理に意思決定があるか
- 同じ不要品を何回個別処理するか
- 回復使用まで何手か
- 装備比較に画面往復が必要か
- auto-sortがプレイヤー意図を壊さないか
