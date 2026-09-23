# Procedural Generation Quality

プロシージャル生成を「毎回違う」機能ではなく、一定以上のゲームプレイ品質を自動的に供給するシステムとして設計する。

## 1. Start from the target verb

最初に生成アルゴリズムではなく、プレイヤーに何をさせたいかを書く。

例:
- 探索
- 高速走行
- 隠密
- 遠距離戦
- 近距離群戦
- 資源探索

生成地形がその行動を実際に誘発するか評価する。

## 2. Quality gates

生成物を段階的に検査する。

1. Valid — データとして壊れていない
2. Solvable — 開始から目標へ到達できる
3. Mechanically useful — 狙った技術を使う場面がある
4. Paced — 密度に山谷がある
5. Distinctive — 前のseedと体験差がある
6. Fair — 初見回避不能や詰みがない

Solvableだけで出荷しない。

## 3. Reproducible seeds

QA記録には、
- seed
- generator version
- biome/theme
- difficulty
- platform
を残す。

生成器更新後も旧seedを再現する必要がある場合はgeneration versionを固定する。

## 4. Robust components

ランダム配置する敵・障害ほど、局所ルールを単純かつ明確にする。

配置依存が強い特殊敵は、許可地形を狭くするか専用テンプレートへ置く。

## 5. Authored grammar + random assembly

完全自由配置より、
- authored room
- encounter grammar
- landmark rule
- transition rule
を組み合わせる。

手作業の意図とランダムの再現性を分担する。

## 6. Pacing constraints

連続して、
- 高密度戦闘
- 同じ地形
- 同じ報酬
- 同じ敵役割
が続かないよう履歴制約を持つ。

生成器は現在地点だけでなく直前の数区間を見る。

## 7. Landmark placement

ランダム世界でも方向感覚を作る。

- 遠景ランドマーク
- 色／形の地区差
- 固有建築
- 高低差
- 道路階層

ランドマークを単なる飾りではなくナビゲーションへ使う。

## 8. Surprise from combinations

基本物理や敵反応は安定させ、
- 配置
- 組み合わせ
- 順序
- 資源状況
を変える。

毎seedでルール自体が変わると学習が蓄積しにくい。

## 9. Regeneration policy

品質ゲートを落ちたseedは、修正不能なら捨てて再生成する。

「すべてのseedを何とか使う」ことを目標にしない。

ただし不合格率が高いならフィルタではなくgenerator本体を直す。

## 10. Human review sampling

自動検証だけでなく、seed群を定期的に人間がプレイする。

見るもの:
- 数値上は違うが体験が同じ
- 美観の破綻
- 不自然な道路／建築
- 意味のない袋小路
- 退屈な安全区間

## Playtest

- valid seedのうち実際に面白い割合
- 目的技能が使われる頻度
- 同じ敵／地形が連続する最大長
- landmarkなしで迷う率
- seedを100%再現できるか
- 自動合格したseedを人間が却下する理由は何か


## 11. Automated feasibility checks

アクションゲームでは単純な経路探索だけでなく、可能ならゲーム物理を使うbot/agentで生成面を試す。

特に、
- 最大ジャンプ
- 慣性
- 移動速度
- 必須技
を含めて到達可能性を確認する。

## 12. Difficulty by constraint relaxation

序盤は厳しい安全制約を使い、進行とともに、
- gap
- hazard count
- enemy combinations
- route ambiguity
などの許容範囲を広げる。

乱数の振れ幅ではなく、制約の段階で難度を作る。

## 13. Player capability and generator co-design

生成器の出力範囲とプレイヤー能力を別々に固定しない。

新しい移動手段や補助能力によって、
以前不適切だった地形を面白い課題へ変えられることがある。


## 14. City road hierarchy

都市生成では道路を一種類として扱わない。

- arterial
- collector
- local
- alley
などの階層ごとに、
- width
- curvature
- intersection density
- speed
を変える。

## 15. Driveability validation

道路グラフのconnectivityだけでなく、車両agentを走らせて、
- corner radius
- slope
- braking frequency
- stuck rate
を検証する。

## 16. Player-height validation

俯瞰で自然な都市が、地上視点でも理解しやすいとは限らない。

自動／人間テストをプレイヤー高さでも行い、
- route readability
- landmark visibility
- repetitive frontage
を確認する。

## 17. LOD must preserve navigation

LODで削除してよいものと、残すべきものを分ける。

優先保持:
- road silhouette
- intersection
- landmark
- drivable boundary

装飾detailよりnavigation informationを優先する。

## 18. Generation trace

seedだけでなく、主要な生成判断をtraceとして保存すると、
「なぜこの道路になったか」を追跡しやすい。

最低:
- generator version
- branch decisions
- rejected candidates
- repair steps
をデバッグ時に参照可能にする。
