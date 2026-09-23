# UGC Discovery & Moderation

UGCを「作れる機能」で終わらせず、発見・評価・改善・安全運営まで含めて設計する。

## 1. Full loop

Create
→ Test
→ Publish
→ Discover
→ Play
→ Feedback
→ Improve

どこか一つが詰まるとcreator ecosystemは育ちにくい。

## 2. Discovery cold start

人気順だけでは新規作品が発見されにくい。

面を分ける:
- New
- Trending
- Personalized
- Curated
- Friends
- Random / Hidden gems

## 3. First impression

一覧画面で数秒以内に内容を理解できるようにする。

表示候補:
- cover
- title
- category
- difficulty
- estimated play time
- likes
- completion rate

## 4. Recommendation quality

プレイヤー嗜好だけでなく、
- creator opportunity
- novelty
- diversity
も考える。

同じ人気作品だけを循環させない。

## 5. Creator analytics

作者へ返す:
- impressions
- starts
- completion
- quit point
- retry
- likes
- follows

改善判断につながる指標を優先する。

## 6. Moderation by design

自由入力を増やすほど運営コストも増える。

不要なら、
- preset tags
- predefined categories
- limited text fields
でリスクを減らす。

## 7. Reporting

各UGCから、
- report
- block creator
- hide content
へすぐ到達できるようにする。

## 8. Age / parental restrictions

UGC表示可否がユーザー年齢や保護者設定で変わる場合を、配信・ghost・replayも含めて考える。

## 9. Multi-modal content

UGCが、
- text
- image
- audio
- level geometry
を含む場合、moderação対象も複数になる。

## 10. Creator feedback loop

moderation理由、非表示理由、推薦データを可能な範囲でcreatorへ返す。

不透明すぎると制作継続を損なう。

## Playtest / Ops

- 新作が最初のplayを得るまでの時間
- 人気上位への露出集中率
- reportまでの操作数
- moderation backlog
- creatorが離脱する地点
- recommendationが同じカテゴリへ偏りすぎないか
