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


## 11. Moderation evidence model

Reportに最低限関連付ける。

- target user ID
- content ID + version
- content type
- reason
- evidence
- timestamp
- report origin

moderatorが後から同じ状態を調べられることを重視する。

## 12. Report + hide + block

report後、判定完了まで同じcontentを見せ続けない。

可能なら、
- hide this content
- block creator
を近接させる。

## 13. Published versions

公開後の編集は新versionとして扱う。

理由:
- rating対象
- leaderboard対象
- replay compatibility
- moderation evidence
が変わるため。

## 14. Version-pinned records

competitive UGCでは、
- score
- replay
- ghost
をlevel versionへ固定する。

level更新後に旧記録をそのまま比較しない。

## 15. Remix lineage

remixには、
- parent content
- parent version
- original creator
- remixer
を保存する。

複数世代でもoriginalへ辿れるようにする。

## 16. Attribution

自動attributionは最低限として常に付ける。

加えてremixerが、
- credit note
- inspiration note
などを追加できると、単なる機械的出典以上の社会的価値を作れる。

## 17. Removal transparency

UGCを削除／非表示にした場合、
可能な範囲でcreatorへ理由を返す。

不透明な処分だけでは改善学習ができない。

## 18. Repeat offenders

単一contentだけでなくcreator単位で、
- repeated violations
- stolen content
- severe abuse
を追跡し、共有権限制限など段階的対応を設計する。
