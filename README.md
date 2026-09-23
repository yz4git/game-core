# game-core

ゲームを「見た目」だけでなく、操作・判断・学習・攻略・リプレイ性まで含めて強くするための知識ベースです。

このリポジトリは、ゲーム雑誌、開発資料、プレイテスト、既存ゲームの観察などから得た知見を、**著作権を侵害しない抽象化された設計原則**として蓄積します。原文・誌面・画像・攻略記事の転載場所にはしません。

## 目的

- 面白さを実装可能な設計原則に落とす
- プレイチェック時の見落としを減らす
- 「要素を増やす」ではなく「判断を深くする」改善を優先する
- ジャンルが違っても再利用できるゲームデザイン知識を蓄積する
- スマホ／Webゲームにも適用できる形にする

## Index

- [Core Principles](docs/core-principles.md) — ジャンル横断の設計原則
- [Playtest Review](docs/playtest-review.md) — プレイチェックと改善の観点
- [Production Loop](docs/production-loop.md) — 企画からPolishまでの実践開発順序
- [Opponent AI & Balance](docs/opponent-ai-and-balance.md) — 読めるAI、公平感、CPU対戦設計
- [Layered Accessibility & Depth](docs/layered-accessibility-and-depth.md) — 初心者の入口と上級者の深さを両立
- [Fighting Game Design](docs/fighting-game-design.md) — 間合い、状態遷移、対抗策、マッチアップ
- [Racing Game Design](docs/racing-game-design.md) — 予告距離、ライン、ライバル、分岐
- [Shooter Recovery & Encounters](docs/shooter-recovery-and-encounters.md) — 復帰、パワー曲線、敵配置
- [Puzzle Planning](docs/puzzle-planning.md) — 未来情報、計画、速度、リセット
- [Arcade Session & Attract](docs/arcade-session-and-attract.md) — 初心者導入、セッション、デモ
- [Game Economy & Interface](docs/game-economy-and-interface.md) — 通貨、消耗品、反復UI、因果
- [Audio as Gameplay](docs/audio-as-gameplay.md) — 音による危険、方向、状態の情報設計
- [Horror Tension Design](docs/horror-tension-design.md) — 予告、不確実性、安全、恐怖周期
- [Save & Failure Design](docs/save-and-failure-design.md) — セーブ、損失量、中断、永続損失
- [Teaching & Documentation](docs/teaching-and-documentation.md) — マニュアル、ヘルプ、実践教授
- [Encounter & Camera Design](docs/encounter-and-camera-design.md) — 脅威方向、画面外、公平な大群戦
- [Community, UGC & Metagame](docs/community-ugc-metagame.md) — 攻略文化、エディタ、想定外技、共有
- [Rhythm Game Design](docs/rhythm-game-design.md) — 判定幅、演奏、表現
- [Rhythm Game Timing](docs/rhythm-game-timing.md) — 音声時刻、校正、Early/Late
- [Camera & Targeting](docs/camera-and-targeting.md) — 3D座標、ロックオン、視認性
- [Procedural Generation Quality](docs/procedural-generation-quality.md) — 品質ゲート、シード、制約
- [Inventory Ergonomics](docs/inventory-ergonomics.md) — 容量、検索、比較、不要作業
- [Strategy UI & Information](docs/strategy-ui-information.md) — micro/macro、通知、ホットキー
- [Local Multiplayer Design](docs/local-multiplayer-design.md) — 同室、共有画面、待ち時間
- [Accessibility Options](docs/accessibility-options.md) — 負荷別Assist、冗長情報、操作設定
- [Rewards & Retention](docs/rewards-and-retention.md) — 報酬と継続を義務化しない設計
- [Crafting System Design](docs/crafting-system-design.md) — レシピ教授、素材、作業負荷
- [Genre Heuristics](docs/genre-heuristics.md) — ジャンル別の重点項目
- [Copyright & Sources](docs/copyright-and-sources.md) — 参照資料の扱い方
- [Research Notes](research/README.md) — 調査ごとの抽象化メモ

## 基本思想

良いゲームは、必ずしも入力数・敵数・ステージ数・演出量が多いゲームではありません。

重視するのは次の流れです。

1. 入力した瞬間に反応が気持ちよい
2. ルールが読める
3. 状況を見て選択できる
4. 選択にリスクと結果がある
5. 経験によって予測できるようになる
6. 上達すると新しい遊び方が見える
7. クリア後も効率・スコア・秘密・別戦略を追える

この階層が増えるほど、コンテンツ量以上にゲームの密度が上がります。

## 更新方針

新しい資料から得た知見は、まず `research/` に短い抽象化メモとして追加します。複数資料で繰り返し確認できた原則は `docs/` に昇格させます。

固有ゲームの仕様をそのままコピーせず、「なぜ機能しているか」「どんな判断を生むか」「別ジャンルへどう転用できるか」に変換して記録します。
