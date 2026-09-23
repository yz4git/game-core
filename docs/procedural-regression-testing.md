# Procedural Regression Testing

生成器を変更するたびに「別のseedが壊れた」を防ぐための回帰テスト設計。

## 1. Two seed pools

### Canonical
- 過去bug
- 極端条件
- 代表地形
- performance stress
- visual/LOD edge case

### Exploratory
毎回ランダムに生成する。

Exploratoryで失敗したseedはCanonicalへ追加する。

## 2. Hard invariants

失敗したら即fail。

例:
- disconnected graph
- unreachable goal
- invalid geometry
- NaN
- impossible slope
- overlapping critical nodes

## 3. Soft metrics

品質劣化を監視する。

都市／道路:
- average speed
- braking count
- U-turn
- landmark visibility
- dead-end ratio
- repetition score

## 4. Distribution monitoring

平均だけ見ない。

保存:
- median
- p95
- p99
- worst N
- failure count

generatorはtail failureが重要。

## 5. Trace diff

同seedの旧版／新版について、
- branch choice
- repair
- rejection
を比較する。

見た目が変わった理由を追える。

## 6. Version everything

記録:
- seed
- generator version
- ruleset version
- content pool version
- platform

再現性を保つ。

## 7. Agent families

一種類のbotだけでは偏る。

- shortest route
- cautious
- aggressive
- high-speed
- explorer

複数戦略で破綻を探す。

## 8. Performance regression

品質だけでなく、
- generation time
- memory
- draw calls
- navigation build time
もseed別に追跡する。

## 9. Visual / LOD regression

navigation-critical要素について、
- road silhouette
- junction
- landmark
を距離別に比較する。

画像diffだけでなくsemantic presenceも見る。

## 10. Human sampling

自動合格seedから定期的に人間が抽出プレイする。

自動metricsが捉えない、
- boring
- ugly
- confusing
を収集し、新metric候補へ戻す。

## Checklist

- canonical seed setがあるか
- exploratory seedを回しているか
- worst 1%を見ているか
- failure seedを保存しているか
- traceを比較できるか
- human rejection理由をmetricへ還元しているか
