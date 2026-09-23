# UGC Versioning & Remix

公開UGCを安全に更新・派生・競技利用するためのデータモデル。

## 1. Content identity vs version identity

一つの作品には、
- content ID
- version ID
を分けて持つ。

更新しても作品ページは同じでよいが、実データは新versionとして扱う。

## 2. Pin dependent records

次をversionへ固定する。

- replay
- ghost
- leaderboard
- moderation report
- rating context
- tournament result

「どの状態を評価したのか」を失わない。

## 3. Immutable published snapshots

公開versionを後から書き換えず、新versionとしてpublishすると監査しやすい。

draftは自由に更新してよい。

## 4. Remix lineage

保存:
- parent content ID
- parent version ID
- original author
- remixer
- timestamp

複数世代の派生でも辿れるようにする。

## 5. Attribution

自動クレジットは最低限として常に付ける。

さらに人間が、
- thanks
- inspiration
- what changed
を記載できるとremix文化の社会的価値を増やせる。

## 6. Moderation evidence

Reportはversionへ固定する。

作者が投稿後に内容を書き換えても、報告対象を再現できるようにする。

## 7. Removal and blocking

report後に、
- hide content
- block creator
を利用可能にする。

moderation完了まで被害を継続させない。

## 8. Repeat abuse

content単位だけでなくcreator historyを持つ。

段階:
- warning
- limited sharing
- temporary suspension
- permanent restriction

## 9. Rating after major updates

大幅変更後に旧ratingを完全継承するか、
- version-specific
- blended
- reset
のどれにするか明示する。

## 10. Remix permission

作品ごとに、
- remix allowed
- remix disabled
- specific asset restrictions
などを表現できるとよい。

法的条件だけでなくcreator expectationも管理する。

## Checklist

- content IDとversion IDが別か
- leaderboardがversion固定か
- report evidenceがversion固定か
- remix originへ辿れるか
- creator blockがあるか
- update後rating policyがあるか
