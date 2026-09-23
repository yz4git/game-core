# Procedural CI Operations

大量seedを継続的に回し、自動生成の破綻・品質劣化・性能回帰を本番前に検出する。

## 1. Seed pools

二つを常設する。

### Canonical
- 過去bug
- worst case
- edge case
- representative cases

### Exploratory
毎回ランダム生成する。

Exploratoryで失敗したseedはCanonicalへ昇格する。

## 2. Headless execution

可能なら描画なしで、
- generation
- navigation
- agent traversal
- invariant checks
を高速実行する。

目的は「人間が見る前に壊れたseedを落とす」こと。

## 3. Hard failures

例:
- unreachable goal
- disconnected critical road
- NaN / Inf
- invalid geometry
- impossible required resource
- generation crash

一つでも出たらCI fail。

## 4. Quality warnings

例:
- excessive braking
- high U-turn rate
- repetitive blocks
- poor landmark visibility
- too many dead ends
- difficulty spike

自動failにするかは閾値で決める。

## 5. Tail metrics

平均だけでなく、
- median
- p95
- p99
- worst 10
- fail count
を記録する。

rare catastrophic seedsを隠さない。

## 6. Performance budgets

seedごとに、
- generation ms
- memory
- nav build time
- object count
- draw-call estimate
を記録する。

品質は良いが極端に重いseedも弾く。

## 7. Failure artifacts

失敗時に自動保存:
- seed
- generator version
- content/ruleset version
- screenshot/thumbnail
- metrics
- trace
- route/agent log

人間が再現情報を集め直さないようにする。

## 8. Trace comparison

同じseedの旧版と新版で、
- branch choice
- repair pass
- rejected candidate
を比較する。

結果差の「原因」を追う。

## 9. Human sampling

自動合格seedから一定割合を人間がプレイする。

人間だけが感じる、
- boring
- ugly
- confusing
を記録し、新しいmetric候補へ戻す。

## 10. Release gate

release前に、
- canonical 100%
- exploratory N seeds
- performance budget
- worst-N review
を通す。

## Checklist

- Canonical seed setは増え続けているか
- failure artifactはワンクリックで再現できるか
- p99が悪化していないか
- generation performanceをseed別に見ているか
- human rejection理由をmetric化しているか
