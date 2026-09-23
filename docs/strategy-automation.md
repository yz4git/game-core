# Strategy Automation vs Meaningful Micromanagement

ストラテジー／シミュレーションで、クリック量を減らしながら戦略上の所有感を残す。

## 1. Ask what the command decides

反復操作ごとに、
> この入力によって何を決めているのか
を問う。

答えが「毎回同じ最適操作を実行するだけ」なら自動化候補。

## 2. Automate execution, preserve intent

例:
- worker chooses exact path automatically
- player chooses road/network priority
- squad maintains formation automatically
- player chooses formation/objective
- production repeats automatically
- player chooses composition/priority

戦術意図はプレイヤー、低レベル実行はシステムへ分担できる。

## 3. Automation must be legible

自動化したシステムには、
- current task
- destination
- queue
- priority
- reason for idle
- blocked state
を見せる。

結果だけ動いて理由が見えないAIは、便利でも信頼されにくい。

## 4. Override points

プレイヤーが必要な時だけ介入できるようにする。

- cancel
- priority
- lock
- manual target
- temporary direct control

常時手動に戻さなくても修正できることが重要。

## 5. Automation should not erase tradeoffs

auto-buildが常に完璧な経済を作るなら、経済設計自体が消える。

automationは、
- repetitive placement
- path choice
- routine replenishment
を減らし、
- what to build
- when
- where to invest
は残す。

## 6. Macro personality for AI

AIの個性を、
- rush
- expansion
- tech
- map control
- defense
などのpriority policyで表す。

数値ボーナスだけで性格を作らない。

## 7. Micro supports macro

micro behaviorは長期戦略を支える。

例:
- damaged unit pullback
- kite
- focus fire
- hold ground

局所行動がmacro intentと矛盾しないようにする。

## 8. Difficulty through decision capability

Easy AIを単に反応遅延だけで作らない。

調整候補:
- strategy breadth
- tech timing
- scouting
- micro repertoire
- response frequency
- planning horizon

プレイヤーが「何が上手くなったか」を読める難度差にする。

## 9. Tactical clarity

AIが賢くても、一度に大量行動を見せると学習不能になる。

- group trivial moves
- sequence important actions
- minimize camera travel
- emphasize highest threat

AI action presentationにも帯域制限を置く。

## 10. Automated validation agents

開発用AIはプレイヤーAIとは別目的で使える。

- thousands of seeds
- car × track
- economy deadlock
- path connectivity
- dominant strategy
を自動検査し、人間はoutlierのfeelを評価する。

## Playtest

- この反復入力を消すと何の判断が消えるか
- automationの次行動を予測できるか
- interventionが数操作でできるか
- AI personalityを名前なしで判別できるか
- Easy/Hard差を行動から説明できるか
- AI turn後に重要な2〜3行動を思い出せるか
- automated agentで代替できる反復QAは何か
