# Crafting System Design

クラフトをレシピ数・素材数ではなく、理解・選択・準備のゲームとして設計する。

## 1. Progressive recipe reveal

新設備を解禁した瞬間に数十レシピを全部見せない。

- 最初の数件
- 新素材取得
- 新用途発見

に合わせて段階的に開示する。

## 2. Logical transformations

レシピ手順が世界の因果と結びつくと覚えやすい。

- cut
- heat
- combine
- refine

意味のある工程を優先する。

## 3. Material roles

各素材に、
- common base
- rare catalyst
- fuel
- structural
など役割を持たせる。

名前だけ違う大量素材を避ける。

## 4. Reverse lookup

素材から、
> 何に使えるか
を調べられるようにする。

レシピ名を知らないと用途が分からない状態を避ける。

## 5. Favorites / pinning

頻繁に作るものは、
- favorite
- pin
- shopping list
で追えるようにする。

## 6. Collection pressure

素材収集が、
- 探索
- 危険地帯
- 経済
の選択を作るなら意味がある。

ただ同じ敵を何十回も倒すだけなら必要量を見直す。

## 7. Crafting clutter

用途のない素材を残さない。

対策:
- auto-convert
- sell category
- future-use indicator
- storage separation

## 8. Observable crafting

協力ゲームでは、材料と工程が世界に見えると、他人の作業を見るだけで学習できる。

## 9. Crafting and progression

クラフト解禁が単なる数値上位装備ではなく、
- 新しい戦法
- 新しい移動
- 新しい環境対応

へつながると成長が強くなる。

## Playtest

- 一度に何レシピ増えるか
- 初見で素材用途を推測できるか
- 必要素材を何周で集めるか
- wikiなしで目的物を作れるか
- 素材100種のうち実際に選択を作るものは何種か
