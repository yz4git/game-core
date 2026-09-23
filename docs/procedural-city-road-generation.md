# Procedural City & Road Generation

都市・道路の自動生成を、見た目のランダム化ではなく「移動可能で、走りやすく、覚えやすい空間」を作るシステムとして設計する。

## 1. Start from the road graph

先に道路ネットワークを作り、その後に街区・敷地・建物を配置する。

道路を階層化する。

- arterial
- collector
- local
- alley

各階層で width / curvature / intersection density / expected speed を変える。

## 2. Connectivity first

最低限確認する。

- 主要地点が接続
- 孤立地区なし
- ループ経路が適度に存在
- dead end率
- alternative route数

ただし、connected = good driving ではない。

## 3. Driveability

車両agentで検証する。

記録:
- average speed
- braking events
- corner radius
- slope
- stuck events
- U-turns
- off-road departures

「到達できる」だけでは合格にしない。

## 4. Player-height readability

俯瞰地図では自然でも地上では迷う場合がある。

プレイヤー高度で、
- next turn
- major road
- landmark
- district transition
を読めるか確認する。

## 5. Landmarks

ランドマークは装飾ではなく位置推定に使う。

種類:
- skyline
- tower
- plaza
- bridge
- unique color mass
- terrain feature

ランドマーク同士が近すぎても遠すぎても効果が弱い。

## 6. District grammar

地区差を一つの見た目変更にしない。

セットで変える:
- road width
- block size
- building height
- setback
- color palette
- vegetation
- traffic
- signage

## 7. Terrain integration

道路生成は地形を無視しない。

考慮:
- slope
- water
- cliffs
- bridges
- tunnels

道路が地形を不自然に貫通するより、コスト付き経路探索を使う。

## 8. LOD and navigation

LOD最適化でも最後まで残す。

- road silhouette
- intersection
- landmark
- drivable boundary

装飾detailを先に削る。

## 9. Seed + version + trace

保存:
- seed
- generator version
- city preset
- biome
- branch choices
- repairs
- rejected candidates

seedだけでは生成器更新後の再現に不十分な場合がある。

## 10. Rapid procedural iteration

自動生成の価値は量産だけでなく試作速度。

道路のcurveやelevationを変えてすぐ走れる状態にし、
設計者が多数案を比較できるようにする。

## 11. Quality gates

1. Valid
2. Connected
3. Driveable
4. Readable
5. Paced
6. Distinctive
7. Fair

すべて通ったseedだけを採用する。

## 12. Automated agents

複数タイプを持つとよい。

- shortest-path driver
- high-speed driver
- cautious driver
- exploration driver

異なる走り方で破綻を探す。

## Playtest

- 目的地まで地図なしで行けるか
- 同じ街区が繰り返しに見えないか
- LOD切替で道が消えないか
- 100 seedの最悪5件を説明できるか
- agentは到達するだけでなく自然に走れるか
- seed/version/traceで不具合を完全再現できるか
