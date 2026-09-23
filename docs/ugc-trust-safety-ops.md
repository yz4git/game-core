# UGC Trust & Safety Operations

UGCの発見・評価・報告・制裁・appealを、ゲーム機能と同じく運用可能なシステムとして設計する。

## 1. Reporting baseline

In-product reportを用意する。

Report record:
- target user
- content ID/version
- content type
- reason
- evidence
- timestamp
- origin

## 2. Immediate user protection

報告後、formal reviewを待たずに、
- hide content
- block creator
を利用可能にする。

## 3. Content guidelines

投稿前に、
- allowed
- prohibited
- enforcement
を分かる形で提示する。

## 4. Restriction handling

UGC権限制限ユーザーには、
UGC部分だけを可能な限り非表示にし、core gameを不必要に丸ごとblockedにしない。

理由を明確に表示する。

## 5. Ranking abuse

対策候補:
- minimum play requirement before rating
- rate limits
- account-age / trust weighting
- anomaly detection
- suspicious cluster review

Popularityとqualityを同一視しない。

## 6. Brigading

短時間・同一source・関連account群による大量評価を検出する。

一時的にranking impactを保留する仕組みを検討する。

## 7. False reports

報告数が多いだけで自動削除しない。

- report credibility
- evidence
- severity
- content history
を組み合わせる。

## 8. Enforcement ladder

例:
1. content removal
2. warning
3. share restriction
4. temporary suspension
5. permanent restriction

違反の重大性と反復性を分ける。

## 9. Appeals

creatorに、
- action reason
- affected content/version
- appeal route
を提示する。

appeal結果もaudit logへ残す。

## 10. Version-aware moderation

content更新で証拠が消えないよう、
moderation recordをversionへ固定する。

## 11. Creator transparency

可能な範囲で、
- why removed
- which rule
- how to fix
を返す。

## 12. Operations metrics

見る:
- moderation backlog
- time-to-action
- false-positive rate
- appeal reversal rate
- repeat offender rate
- blocked-content re-exposure

## Checklist

- report dataがactionableか
- reported contentを本人へ再表示しないか
- brigading耐性があるか
- appealsが存在するか
- version更新後も証拠を追えるか
